---
title: Gestione dello stato del client
description: Scopri come Adobe Experience Platform Edge Network gestisce lo stato del client
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: client;stato;gestione;edge;rete;gateway;api
source-git-commit: eaeab8fe96a9af399f8288b62b6ca9f31d949cfa
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 2%

---


# Gestione dello stato del client

La rete Edge stessa è senza stato (non mantiene la propria sessione). Tuttavia, esistono alcuni casi d’uso che richiedono la persistenza dello stato lato client, ad esempio:

* Identificazione coerente del dispositivo (vedi [identificazione visitatore](visitor-identification.md))
* Raccogliere e applicare il consenso degli utenti
* Mantenere l’ID della sessione di personalizzazione

La rete Edge utilizza un protocollo di gestione dello stato, che delega l’aspetto di archiviazione al proprio client/SDK e include le voci dello stato nelle risposte. Per i browser, le voci sono memorizzate come cookie.

La responsabilità del cliente è quella di memorizzarle e includerle in tutte le richieste successive. Il client deve inoltre provvedere alla corretta scadenza delle voci, come indicato dal gateway. Quando le voci sono state archiviate come cookie, il browser esegue tutto questo automaticamente.

Anche se le voci dello stato hanno sempre un valore normale `String` (visibile al chiamante/SDK), non utilizzare o manomettere i valori in alcun modo. La struttura/il formato del valore o anche il nome stesso potrebbero cambiare in qualsiasi momento, il che potrebbe causare un comportamento imprevisto per i client che utilizzano lo stato internamente. Lo stato deve essere sempre utilizzato dal gateway stesso o da altri servizi edge.

## Stato client persistente come metadati

Stato restituito da [!DNL Edge Network] nel corpo della risposta è un `Handle` oggetto con il tipo `state:store`.

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
| `key` | Stringa | **Obbligatorio**. Nome della voce. |
| `value` | Stringa | *Facoltativo*. Valore immesso. |
| `maxAge` | Intero | *Facoltativo* Il time-to-live (TTL) in secondi. Se mancante, le voci devono essere memorizzate solo per la sessione corrente. |
| `attrs` | `Map<String, String>` | *Facoltativo*. Un elenco facoltativo di attributi di ingresso. Per tutte le connessioni sicure con un&#39;intestazione HTTP referente sicura, il `SameSite` attributo impostato su `None`. |


Per supportare l’assegnazione di più tag (ovvero più istanze SDK nella stessa proprietà, che possono fare riferimento a organizzazioni diverse), tutte le voci dello stato hanno automaticamente il prefisso `kndctr_` e l&#39;ID organizzazione sicuro per gli URL.

Quando l’SDK client riceve un `state:store` nella risposta, deve effettuare le seguenti operazioni:

* Archiviare le voci lato client, rispettando il tempo di scadenza fornito dal gateway.
* Caricali dall’archivio client e includi tutte le voci non scadute nelle richieste successive.

Ecco un esempio di richiesta che passa nello stato memorizzato sul lato client:

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

## Stato client persistente nei cookie del browser

Quando si lavora con i client del browser, la rete Edge può persistere automaticamente le voci come cookie del browser. Questo consente il supporto trasparente dello stato di archiviazione, poiché i browser rispettano il protocollo di gestione dello stato per impostazione predefinita.

Quasi tutte le voci vengono materializzate come cookie di prime parti quando sono abilitate e supportate (vedi la nota qui di seguito), ma il gateway potrebbe anche memorizzare alcuni cookie di terze parti quando `adobedc.demdex.net` dominio utilizzato.

Poiché le voci sono sempre associate a un ambito specifico (dispositivo/applicazione) in base alla loro definizione, solo il sottoinsieme compatibile con il contesto della richiesta corrente verrà scritto da Edge Network. Le voci non scritte vengono restituite all&#39;interno di un `state:store` manico.

Come regola generale, le voci con ambito applicazione sono sempre scritte come cookie di prime parti, mentre le voci con ambito dispositivo sono scritte come cookie di terze parti. La decisione è completamente trasparente per il chiamante, il gateway decide quali voci possono essere scritte, a seconda del contesto della chiamata.

Il chiamante deve abilitare esplicitamente il supporto per l’archiviazione dello stato client come cookie tramite `meta.state.cookiesEnabled` bandiera:

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
| `cookiesEnabled` | Booleano | Quando è impostato, abilita il supporto per i cookie. Il valore predefinito è `false`. |
| `domain` | Stringa | Obbligatorio quando `cookiesEnabled: true`. Dominio di primo livello in cui devono essere scritti i cookie. Edge Network utilizzerà questo valore per decidere se lo stato può essere mantenuto come cookie. |

Anche se il supporto dei cookie è abilitato tramite la funzione `cookiesEnabled` flag , Adobe Experience Platform Edge Network scriverà le voci dello stato solo se il dominio di primo livello della richiesta corrisponde al `domain` specificato dal chiamante. In caso di mancata corrispondenza, le voci vengono restituite in un `state:store` manico.

I cookie di prime parti non possono essere scritti (anche se il supporto è abilitato) nei seguenti casi:

* La richiesta viene inoltrata da terze parti `adobedc.demdex.net` dominio.
* Richiesta in arrivo su una prima parte `CNAME` , diverso da quello specificato dal chiamante in `meta.state.domain`.

## Sicurezza dei cookie

Tutti i cookie hanno [Flag Secure](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies) quando possibile.

Tutti i cookie protetti hanno [Attributo SameSite](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) impostato su `None`, ovvero i cookie vengono inviati in tutti i contesti, sia di prima parte che tra origini diverse.

* Per i cookie di prime parti (`kndcrt_*`), `Secure` Il flag viene impostato solo quando il contesto della richiesta è protetto (HTTPS) e quando il referente ([Intestazione HTTP referente](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer)) è anche HTTPS. Se il referente non è protetto (HTTP), la `Secure` Questo flag viene omesso per consentire all&#39;SDK Web di leggerli. Impossibile leggere un cookie protetto da un contesto non protetto.
* Per il cookie di terze parti (demdex), il `Secure` Il flag è sempre impostato, poiché tutte le richieste sono HTTPS, quindi il contesto della richiesta è protetto e questo cookie non viene mai letto da JavaScript.

La `Secure` il flag non è presente nel [rappresentazione dei metadati dei cookie](#state-as-metadata). Solo il `SameSite` attributo incluso. In questo caso, è responsabilità del cliente impostare correttamente il `Secure` ogni volta che `SameSite` attributo presente. Cookie con `SameSite=None` deve inoltre specificare `Secure` , poiché richiedono un contesto protetto (HTTPS).
