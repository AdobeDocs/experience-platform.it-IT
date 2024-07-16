---
title: Gestione stato client
description: Scopri come l’Edge Network di Adobe Experience Platform gestisce lo stato del client
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: client;stato;gestione;edge;rete;gateway;api
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 1%

---

# Gestione stato client

L’Edge Network stesso è senza stato (non mantiene la propria sessione). Tuttavia, in alcuni casi d’uso è necessaria la persistenza dello stato lato client, ad esempio:

* Identificazione coerente del dispositivo (vedi [identificazione visitatore](visitor-identification.md))
* Raccogliere e applicare il consenso degli utenti
* Mantenimento dell’ID della sessione di personalizzazione

L&#39;Edge Network utilizza un protocollo di gestione dello stato, delegando l&#39;aspetto di archiviazione al relativo client/SDK, e include voci di stato nelle risposte. Per i browser, le voci sono memorizzate come cookie.

La responsabilità del cliente è quella di archiviarli e includerli in tutte le richieste successive. Il client deve inoltre provvedere alla scadenza corretta per le voci, come indicato dal gateway. Quando le voci sono state memorizzate come cookie, il browser esegue automaticamente tutto questo lavoro.

Anche se le voci di stato hanno sempre un valore `String` normale (visibile al chiamante/SDK), non utilizzare o manomettere in alcun modo i valori. La struttura/il formato del valore o anche il nome stesso potrebbero cambiare in qualsiasi momento, il che potrebbe portare a un comportamento imprevisto per i client che utilizzano lo stato internamente. Lo stato deve essere sempre utilizzato dal gateway stesso o da altri servizi Edge.

## Stato client persistente come metadati

Lo stato restituito da [!DNL Edge Network] nel corpo della risposta è un oggetto `Handle` di tipo `state:store`.

```json
{
   "requestId":"421036b3-a7ff-480b-a9ab-30adba6eb4f0",
   "handle":[
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1",
               "maxAge":7200,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiY1NDc1ODIxNzIzODk5MDY5MzQzMTIzNjQ1NTczNzExNjE4OTA1MFINCLGOvszNLhABGAEgBKABsY6-zM0uqAGHz-z2y82cul3wAbGOvszNLg==",
               "maxAge":34128000,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent",
               "value":"general=in",
               "maxAge":15552000,
               "attrs":{
                  "SameSite":"None"
               }
            }
         ],
         "type":"state:store"
      }
   ]
}
```

| Attributo | Tipo | Descrizione |
| --- | --- | --- |
| `key` | Stringa | **Richiesto**. Il nome della voce. |
| `value` | Stringa | *Facoltativo*. Il valore di ingresso. |
| `maxAge` | Intero | *Facoltativo* Tempo (in secondi) alla scadenza della voce. Se mancano, le voci devono essere memorizzate solo per la sessione corrente. |
| `attrs` | `Map<String, String>` | *Facoltativo*. Elenco facoltativo di attributi di voce. Per tutte le connessioni sicure con un&#39;intestazione HTTP del referente sicuro, l&#39;attributo `SameSite` è impostato su `None`. |


Per supportare l&#39;assegnazione di più tag (ovvero più istanze SDK nella stessa proprietà, che potenzialmente fanno riferimento a organizzazioni diverse), tutte le voci di stato vengono automaticamente precedute da `kndctr_` e dall&#39;ID organizzazione sicuro per gli URL.

Quando l&#39;SDK client riceve un handle `state:store` nella risposta, deve eseguire le operazioni seguenti:

* Memorizza le voci lato client, rispettando il tempo di scadenza fornito dal gateway.
* Caricali dall’archivio client e includi tutte le voci non scadute nelle richieste successive.

Di seguito è riportato un esempio di richiesta che passa nello stato memorizzato lato client:

```json
{
   "meta":{
      "state":{
         "entries":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1"
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_personalization_sessionId",
               "value":"0a88f43e-044b-41a6-a4f3-6c2848bbc672"
            }
         ]
      }
   }
}
```

## Persistenza dello stato del client nei cookie del browser

Quando si lavora con i client del browser, l’Edge Network può rendere le voci persistenti come cookie del browser. Questo consente il supporto dello stato di archiviazione trasparente, in quanto i browser rispettano il protocollo di gestione dello stato per impostazione predefinita.

Quasi tutte le voci vengono materializzate come cookie di prima parte se abilitate e supportate (vedi la nota seguente), ma il gateway potrebbe anche memorizzare alcuni cookie di terze parti quando viene utilizzato il dominio `adobedc.demdex.net` di terze parti.

Poiché le voci sono sempre associate a un ambito specifico (dispositivo/applicazione) in base alla loro definizione, solo il sottoinsieme compatibile con il contesto della richiesta corrente verrà scritto dall’Edge Network. Le voci non scritte sono
ha restituito in un handle `state:store`.

Come regola generale, le voci con ambito applicazione vengono sempre scritte come cookie di prima parte, mentre le voci con ambito dispositivo vengono scritte come cookie di terze parti. La decisione è completamente trasparente per il chiamante, il gateway decide quali voci possono essere scritte, a seconda del contesto della chiamata.

Il chiamante deve abilitare esplicitamente il supporto per l&#39;archiviazione dello stato del client come cookie tramite il flag `meta.state.cookiesEnabled`:

```json
{
   "meta":{
      "state":{
         "cookiesEnabled":true,
         "domain":"foo.com"
      }
   }
}
```

| Attributo | Tipo | Descrizione |
| --- | --- | --- |
| `cookiesEnabled` | Booleano | Se questa opzione è impostata, abilita il supporto per i cookie. Il valore predefinito è `false`. |
| `domain` | Stringa | Richiesto quando `cookiesEnabled: true`. Il dominio di primo livello in cui devono essere scritti i cookie. L’Edge Network utilizzerà questo valore per decidere se lo stato può essere mantenuto come cookie. |

Anche se il supporto dei cookie è abilitato tramite il flag `cookiesEnabled`, l&#39;Edge Network di Adobe Experience Platform scriverà le voci di stato solo se il dominio di primo livello della richiesta corrisponde a `domain` specificato dal chiamante. In caso di mancata corrispondenza, le voci vengono restituite in un handle `state:store`.

I cookie di prime parti non possono essere scritti (anche se il supporto è abilitato) nei seguenti casi:

* La richiesta proviene dal dominio `adobedc.demdex.net` di terze parti.
* La richiesta proviene da un dominio `CNAME` di prime parti, diverso da quello specificato dal chiamante in `meta.state.domain`.

## Sicurezza dei cookie

Tutti i cookie hanno il [flag Secure](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies) abilitato quando possibile.

Tutti i cookie protetti hanno l&#39;attributo [SameSite](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) impostato su `None`, il che significa che i cookie vengono inviati in tutti i contesti, sia di prima parte che tra origini diverse.

* Per i cookie di prime parti (`kndcrt_*`), il flag `Secure` viene impostato solo quando il contesto della richiesta è protetto (HTTPS) e quando il referente ([Intestazione HTTP referente](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer)) è anche HTTPS. Se il referente non è protetto (HTTP), il flag `Secure` viene omesso per consentire all&#39;SDK Web di leggerli. Impossibile leggere un cookie protetto da un contesto non sicuro.
* Per il cookie di terze parti (demdex), il flag `Secure` è sempre impostato, poiché tutte le richieste sono HTTPS, pertanto il contesto della richiesta è sicuro e questo cookie non viene mai letto da JavaScript.

Il flag `Secure` non è presente nella rappresentazione dei metadati [dei cookie](#state-as-metadata). È incluso solo l&#39;attributo `SameSite`. In questo caso è responsabilità del client impostare correttamente il flag `Secure` ogni volta che è presente l&#39;attributo `SameSite`. I cookie con `SameSite=None` devono inoltre specificare l&#39;attributo `Secure`, poiché richiedono un contesto protetto (HTTPS).
