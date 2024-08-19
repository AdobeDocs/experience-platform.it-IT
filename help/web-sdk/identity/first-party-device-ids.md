---
title: ID dispositivo di prime parti in Web SDK
description: Scopri come configurare gli ID dispositivo di prime parti (FPID) per Adobe Experience Platform Web SDK.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: b35a4316ca4ef82e545a7718f1b986f978003a0e
workflow-type: tm+mt
source-wordcount: '1990'
ht-degree: 0%

---


# ID dispositivo di prime parti in Web SDK

Adobe Experience Platform Web SDK assegna [ID Adobe Experience Cloud (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=it) ai visitatori del sito Web utilizzando i cookie per monitorare il comportamento degli utenti. Per tenere conto delle restrizioni del browser sulla durata dei cookie, puoi invece scegliere di impostare e gestire gli identificatori dei tuoi dispositivi. Questi sono denominati ID dispositivo di prime parti (FPID, first party device ID).

>[!NOTE]
>
>Il supporto per ID dispositivo di prime parti è disponibile solo quando si inviano dati all’Edge Network di Platform tramite l’SDK web per Platform.

>[!IMPORTANT]
>
>Gli ID dispositivo di prime parti non sono compatibili con la funzionalità [cookie di terze parti](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity) in Web SDK.
>Puoi utilizzare gli ID dispositivo di prime parti oppure cookie di terze parti, ma non puoi utilizzare entrambe le funzioni contemporaneamente.

Questo documento illustra come configurare gli ID dispositivo di prime parti per l’implementazione di Platform Web SDK.

## Prerequisiti

Questa guida presuppone che tu abbia familiarità con il funzionamento dei dati di identità per Platform Web SDK, incluso il ruolo di ECID e `identityMap`. Per ulteriori informazioni, consulta la panoramica sui [dati di identità nell&#39;SDK per web](./overview.md).

## Utilizzo degli FPID

Gli FPID tengono traccia dei visitatori utilizzando cookie di prime parti. I cookie di prime parti sono più efficaci quando vengono impostati utilizzando un server che utilizza un [record A](https://datatracker.ietf.org/doc/html/rfc1035) DNS (per IPv4) o un [record AAAA](https://datatracker.ietf.org/doc/html/rfc3596) DNS (per IPv6), anziché un codice CNAME o JavaScript DNS.

>[!IMPORTANT]
>
>I record `A` o `AAAA` sono supportati solo per l&#39;impostazione e il tracciamento dei cookie. Il metodo principale per la raccolta dei dati è tramite un CNAME DNS. In altre parole, gli FPID vengono impostati utilizzando un record A o AAAA e quindi inviati ad Adobe utilizzando un CNAME.
>
>Il [programma di certificazione gestito da Adobe](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) è ancora supportato per la raccolta dati di prime parti.

Una volta impostato un cookie FPID, il relativo valore può essere recuperato e inviato all’Adobe durante la raccolta dei dati dell’evento. Gli FPID raccolti vengono utilizzati come seed per generare ECID, che continuano a essere gli identificatori primari nelle applicazioni Adobe Experience Cloud.

Per inviare un FPID per un visitatore del sito Web all&#39;Edge Network di Platform, è necessario includere l&#39;FPID in `identityMap` per tale visitatore. Per ulteriori informazioni, vedere la sezione più avanti in questo documento relativa all&#39;utilizzo di FPID in `identityMap`](#identityMap) per [.

### Requisiti di formattazione degli ID

L&#39;Edge Network di Platform accetta solo ID conformi al formato [UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). Gli ID dispositivo non in formato UUIDv4 verranno rifiutati.

La generazione di un UUID si tradurrà quasi sempre in un ID casuale univoco, con una probabilità di collisione trascurabile. Non è possibile eseguire il seeding di UUIDv4 utilizzando indirizzi IP o qualsiasi altra informazione personale identificabile (PII). Gli UUID sono onnipresenti e le librerie possono essere trovate praticamente per ogni linguaggio di programmazione per generarli.

## Impostazione di un cookie ID di prima parte nell’interfaccia utente degli stream di dati {#setting-cookie-datastreams}

È possibile specificare il nome di un cookie nell&#39;interfaccia utente di Datastreams, dove può risiedere [!DNL FPID], anziché dover leggere il valore del cookie e includere l&#39;FPID nella mappa identità.

>[!IMPORTANT]
>
>Questa funzionalità richiede l&#39;abilitazione di [Raccolta dati di prime parti](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=en).

Per informazioni dettagliate su come configurare uno stream di dati, consulta la [documentazione sugli stream di dati](../../datastreams/configure.md).

Durante la configurazione dello stream di dati, abilita l&#39;opzione **[!UICONTROL Cookie ID di prime parti]**. Questa impostazione indica all&#39;Edge Network di fare riferimento a un cookie specificato durante la ricerca di un ID dispositivo di prime parti, anziché cercare questo valore in [Identity Map](#identityMap).

Consulta la documentazione su [cookie di prime parti](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=it) per ulteriori dettagli sul loro funzionamento con Adobe Experience Cloud.

![Immagine dell&#39;interfaccia utente di Platform che mostra la configurazione dello stream di dati evidenziando l&#39;impostazione del cookie ID di prime parti](../assets/first-party-id-datastreams.png)

Quando abiliti questa impostazione, devi fornire il nome del cookie in cui si prevede che l’ID venga memorizzato.

Quando utilizzi ID di prime parti, non puoi eseguire sincronizzazioni ID di terze parti. Le sincronizzazioni ID di terze parti si basano sul servizio [!DNL Visitor ID] e sul `UUID` generati da tale servizio. Quando si utilizza la funzionalità ID di prima parte, l&#39;ECID viene generato senza l&#39;utilizzo del servizio [!DNL Visitor ID], rendendo impossibile le sincronizzazioni ID di terze parti.

Quando si utilizzano gli ID di prime parti, le funzionalità di Audience Manager mirate all&#39;attivazione nelle piattaforme partner non sono supportate, dato che le sincronizzazioni degli ID partner di Audience Manager si basano principalmente su `UUIDs` o `DIDs`. L&#39;ECID derivato da un ID di prima parte non è collegato a un `UUID`, rendendolo non indirizzabile.

## Impostazione di un cookie con il tuo server

Quando imposti un cookie utilizzando un server di tua proprietà, è possibile utilizzare diversi metodi per impedire che il cookie venga limitato a causa dei criteri del browser:

* Generare cookie utilizzando linguaggi di script lato server
* Imposta i cookie in risposta a una richiesta API effettuata a un sottodominio o a un altro endpoint sul sito
* Generare cookie utilizzando un CMS
* Generare cookie utilizzando una rete CDN

>[!IMPORTANT]
>
>I cookie impostati con il metodo `document.cookie` di JavaScript non saranno quasi mai protetti dai criteri del browser che limitano la durata dei cookie.

### Quando impostare il cookie

Il cookie FPID dovrebbe idealmente essere impostato prima di effettuare qualsiasi richiesta all’Edge Network. Tuttavia, negli scenari in cui ciò non è possibile, un ECID viene comunque generato utilizzando i metodi esistenti e funge da identificatore primario finché il cookie esiste.

Supponendo che l’ECID sia infine interessato da un criterio di eliminazione del browser, ma l’FPID non lo è, l’FPID diventerà l’identificatore primario alla visita successiva e verrà utilizzato per seed l’ECID a ogni visita successiva.

### Impostazione della scadenza per il cookie

Impostare la scadenza di un cookie è un aspetto che deve essere attentamente considerato quando si implementa la funzionalità FPID. Nel decidere questa opzione, è necessario considerare i paesi o le aree geografiche in cui l&#39;organizzazione opera insieme alle leggi e alle politiche in ognuna di queste aree.

Come parte di questa decisione, puoi adottare un criterio di impostazione dei cookie a livello aziendale o diverso a seconda delle impostazioni internazionali.

Indipendentemente dall’impostazione scelta per la scadenza iniziale di un cookie, è necessario assicurarsi di includere una logica che estenda la scadenza del cookie ogni volta che si verifica una nuova visita al sito.

## Impatto dei flag dei cookie

Esistono diversi flag di cookie che influiscono sul modo in cui i cookie vengono trattati nei diversi browser:

* [&quot;HTTPOnly&quot;](#http-only)
* [&quot;Secure&quot;](#secure)
* [&quot;SameSite&quot;](#same-site)

### `HTTPOnly` {#http-only}

Impossibile accedere ai cookie impostati con il flag `HTTPOnly` utilizzando script lato client. Ciò significa che se si imposta un flag `HTTPOnly` durante l&#39;impostazione dell&#39;FPID, è necessario utilizzare un linguaggio di script lato server per leggere il valore del cookie da includere in `identityMap`.

Se si sceglie di fare in modo che l&#39;Edge Network di Platform legga il valore del cookie FPID, l&#39;impostazione del flag `HTTPOnly` garantisce che il valore non sia accessibile da alcuno script lato client, ma non avrà alcun impatto negativo sulla capacità dell&#39;Edge Network di Platform di leggere il cookie.

>[!NOTE]
>
>L&#39;utilizzo del flag `HTTPOnly` non ha alcun impatto sui criteri dei cookie che possono limitare la durata dei cookie. Tuttavia, è ancora qualcosa da considerare quando imposti e leggi il valore dell’FPID.

### `Secure` {#secure}

I cookie impostati con l&#39;attributo `Secure` vengono inviati solo al server con una richiesta crittografata tramite il protocollo HTTPS. L’utilizzo di questo flag può contribuire a garantire che gli aggressori man-in-the-middle non possano accedere facilmente al valore del cookie. Quando possibile, è sempre consigliabile impostare il flag `Secure`.

### `SameSite` {#same-site}

L&#39;attributo `SameSite` consente ai server di determinare se i cookie vengono inviati con richieste intersito. L’attributo fornisce una certa protezione contro gli attacchi di tipo cross-site forgery. Esistono tre valori possibili: `Strict`, `Lax` e `None`. Consulta il team interno per determinare quale impostazione è corretta per la tua organizzazione.

Se non viene specificato alcun attributo `SameSite`, l&#39;impostazione predefinita per alcuni browser è ora `SameSite=Lax`.

## Utilizzo di FPID in `identityMap` {#identityMap}

Di seguito è riportato un esempio di impostazione di un FPID in `identityMap`:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ]
  }
}
```

Come con altri tipi di identità, è possibile includere l&#39;FPID con altre identità all&#39;interno di `identityMap`. Di seguito è riportato un esempio dell’FPID incluso con un ID del sistema di gestione delle relazioni con i clienti autenticato:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": false
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Se l’FPID è contenuto in un cookie letto dall’Edge Network quando la raccolta dati di prime parti è abilitata, devi acquisire solo l’ID CRM autenticato:

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Il seguente `identityMap` genererebbe una risposta di errore da parte dell&#39;Edge Network poiché manca l&#39;indicatore `primary` per l&#39;FPID. Almeno uno degli ID presenti in `identityMap` deve essere contrassegnato come `primary`.

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-12d3-a456-426614174000",
        "authenticatedState": "ambiguous"
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

La risposta di errore restituita dall’Edge Network in questo caso è simile alla seguente:

```json
{
    "type": "https://ns.adobe.com/aep/errors/EXEG-0306-400",
    "status": 400,
    "title": "No primary identity set in request (event)",
    "detail": "No primary identity found in the input event. Update the request accordingly to your schema and try again.",
    "report": {
        "requestId": "{REQUEST_ID}",
        "configId": "{CONFIG_ID}",
        "orgId": "{ORG_ID}"
    }
}
```

## Gerarchia ID

Quando sono presenti sia un ECID che un FPID, all’ECID viene assegnata la priorità di identificare l’utente. In questo modo, quando un ECID esistente è presente nell’archivio dei cookie del browser, rimane l’identificatore principale e i conteggi dei visitatori esistenti non rischiano di essere interessati. Per gli utenti esistenti, l’FPID non diventerà l’identità principale fino alla scadenza dell’ECID o alla sua eliminazione in seguito a una policy del browser o a un processo manuale.

Le identità hanno la priorità nel seguente ordine:

1. ECID incluso in `identityMap`
1. ECID memorizzato in un cookie
1. FPID incluso in `identityMap`
1. FPID memorizzato in un cookie

## Migrazione agli ID dispositivo di prime parti

Se stai eseguendo la migrazione a utilizzando gli FPID da un’implementazione precedente, potrebbe essere difficile visualizzare l’aspetto della transizione a un livello basso.

Per illustrare questo processo, considera uno scenario che coinvolge un cliente che ha già visitato il tuo sito e quale impatto avrebbe una migrazione FPID su come quel cliente viene identificato nelle soluzioni Adobe.

![Diagramma che mostra come i valori ID di un cliente vengono aggiornati tra le visite dopo la migrazione a FPID](../assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>Il cookie `ECID` ha sempre la priorità rispetto a `FPID`.

| Visita | Descrizione |
| --- | --- |
| Prima visita | Supponiamo che non abbiate ancora iniziato a impostare il cookie FPID. L&#39;ECID contenuto nel cookie [AMCV](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) sarà l&#39;identificatore utilizzato per identificare il visitatore. |
| Seconda visita | Rollout della soluzione ID dispositivo di prime parti avviato. L’ECID esistente è ancora presente e rimane l’identificatore primario per l’identificazione dei visitatori. |
| Terza visita | Tra la seconda e la terza visita, è trascorso abbastanza tempo da consentire l’eliminazione dell’ECID a causa dei criteri del browser. Tuttavia, poiché l’FPID è stato impostato utilizzando un record A DNS, l’FPID persiste. L’FPID è ora considerato l’ID primario e viene utilizzato per seed l’ECID, che viene scritto sul dispositivo dell’utente finale. L’utente viene ora considerato un nuovo visitatore nelle soluzioni Adobe Experience Platform e Experience Cloud. |
| Quarta visita | Tra la terza e la quarta visita, è trascorso abbastanza tempo da consentire l’eliminazione dell’ECID a causa dei criteri del browser. Come la visita precedente, l’FPID rimane dovuto al modo in cui è stato impostato. Questa volta viene generato lo stesso ECID della visita precedente. L’utente viene visualizzato in tutte le soluzioni di Experience Platform e Experience Cloud come lo stesso utente della visita precedente. |
| Quinta visita | Tra la quarta e la quinta visita, l’utente finale ha cancellato tutti i cookie nel suo browser. Viene generato un nuovo FPID e utilizzato per la creazione di un nuovo ECID. L’utente viene ora considerato un nuovo visitatore nelle soluzioni Adobe Experience Platform e Experience Cloud. |

{style="table-layout:auto"}

## Domande frequenti

Di seguito è riportato un elenco di risposte alle domande più frequenti sugli ID dispositivo di prime parti.

### In che modo il seeding di un ID è diverso dalla semplice generazione di un ID?

Il concetto di seeding è unico in quanto l&#39;FPID passato a Adobe Experience Cloud viene convertito in un ECID utilizzando un algoritmo deterministico. Ogni volta che lo stesso FPID viene inviato all’Edge Network Adobe Experience Platform, viene generato lo stesso ECID dall’FPID.

### Quando deve essere generato l’ID dispositivo di prime parti?

Per ridurre l’inflazione di visitatori potenziali, è necessario generare l’FPID prima di effettuare la prima richiesta utilizzando l’SDK per web. Tuttavia, se non riesci a eseguire questa operazione, per tale utente verrà comunque generato un ECID che verrà utilizzato come identificatore primario. L’FPID generato non diventerà l’identificatore primario fino a quando l’ECID non sarà più presente.

### Quali metodi di raccolta dati supportano gli ID dispositivo di prime parti?

Attualmente solo Web SDK supporta gli FPID.

### Gli FPID sono memorizzati su qualsiasi piattaforma o soluzione Experience Cloud?

Una volta utilizzato per il seeding di un ECID, l&#39;FPID viene rimosso da `identityMap` e sostituito con l&#39;ECID generato. L’FPID non viene memorizzato in alcuna soluzione Adobe Experience Platform o Experience Cloud.
