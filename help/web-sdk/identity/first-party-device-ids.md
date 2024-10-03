---
title: ID dispositivo di prime parti in Web SDK
description: Scopri come configurare gli ID dispositivo di prime parti (FPID) in Adobe Experience Platform Web SDK.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: 04ef39cbfc614369cb15f4d947474b491c34ef33
workflow-type: tm+mt
source-wordcount: '2055'
ht-degree: 0%

---


# ID dispositivo di prime parti in Web SDK

Adobe Experience Platform Web SDK assegna [ID Adobe Experience Cloud (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=it) ai visitatori del sito Web utilizzando i cookie per monitorare il comportamento degli utenti. Per tenere conto delle restrizioni del browser sulla durata dei cookie, puoi invece scegliere di impostare e gestire gli identificatori dei tuoi dispositivi. Tali ID sono denominati ID dispositivo di prime parti (`FPIDs`).

>[!NOTE]
>
>Il supporto per gli ID dispositivo di prime parti è disponibile solo quando si inviano dati all’Edge Network Experience Platform tramite Web SDK.

>[!IMPORTANT]
>
>Gli ID dispositivo di prime parti non sono compatibili con la funzionalità [cookie di terze parti](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity) in Web SDK.
>Puoi utilizzare gli ID dispositivo di prime parti oppure cookie di terze parti, ma non puoi utilizzare entrambe le funzioni contemporaneamente.

Questo documento spiega come configurare gli ID dispositivo di prime parti per l’implementazione dell’SDK web.

## Prerequisiti

Questa guida presuppone che tu abbia familiarità con il funzionamento dei dati di identità per Platform Web SDK, incluso il ruolo di ECID e `identityMap`. Per ulteriori informazioni, consulta la panoramica sui [dati di identità nell&#39;SDK per web](./overview.md).

## Utilizzo degli ID dispositivo di prime parti (FPID) {#using-fpid}

Gli ID dispositivo di prime parti ([!DNL FPIDs]) tengono traccia dei visitatori utilizzando cookie di prime parti. I cookie di prime parti sono più efficaci quando vengono impostati utilizzando un server che utilizza un [record A](https://datatracker.ietf.org/doc/html/rfc1035) DNS (per IPv4) o un [record AAAA](https://datatracker.ietf.org/doc/html/rfc3596) DNS (per IPv6), anziché un codice DNS [!DNL CNAME] o [!DNL JavaScript].

>[!IMPORTANT]
>
>I record [!DNL A] o [!DNL AAAA] sono supportati solo per l&#39;impostazione e il tracciamento dei cookie. Il metodo primario per la raccolta dati è tramite un [!DNL DNS] [!DNL CNAME]. In altre parole, [!DNL FPIDs] sono impostati utilizzando un record [!DNL A] o [!DNL AAAA] e vengono quindi inviati ad Adobe utilizzando un [!DNL CNAME].
>
>Il [programma di certificazione gestito da Adobe](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) è ancora supportato per la raccolta dati di prime parti.

Una volta impostato il cookie [!DNL FPID], il relativo valore può essere recuperato e inviato all&#39;Adobe durante la raccolta dei dati dell&#39;evento. I [!DNL FPIDs] raccolti vengono utilizzati come seed per generare [!DNL ECIDs], che continuano a essere gli identificatori primari nelle applicazioni Adobe Experience Cloud.

Per inviare un [!DNL FPID] per un visitatore del sito Web all&#39;Edge Network, è necessario includere [!DNL FPID] in `identityMap` per tale visitatore. Per ulteriori informazioni, consulta la sezione più avanti in questo documento sull&#39;utilizzo degli FPID in `identityMap`](#identityMap) per [.

### Requisiti di formattazione degli ID dispositivo di prime parti {#formatting-requirements}

L&#39;Edge Network accetta solo [!DNL IDs] conformi al formato [UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). Gli ID dispositivo non nel formato [!DNL UUIDv4] verranno rifiutati.

La generazione di un [!DNL UUID] produrrà quasi sempre un ID casuale univoco, con una probabilità di collisione trascurabile. Impossibile eseguire il seeding di [!DNL UUIDv4] utilizzando indirizzi IP o altre informazioni personali identificabili ([!DNL PII]). [!DNL UUIDs] sono onnipresenti e le librerie possono essere trovate praticamente per ogni linguaggio di programmazione per generarle.

## Impostazione di un cookie ID di prime parti nell’interfaccia utente dei flussi di dati {#setting-cookie-datastreams}

È possibile specificare il nome di un cookie nell&#39;interfaccia utente di Datastreams, dove può risiedere [!DNL FPID], anziché dover leggere il valore del cookie e includere [!DNL FPID] nella mappa delle identità.

>[!IMPORTANT]
>
>Questa funzionalità richiede l&#39;abilitazione di [Raccolta dati di prime parti](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=en).

Per informazioni dettagliate su come configurare uno stream di dati, consulta la [documentazione sugli stream di dati](../../datastreams/configure.md).

Durante la configurazione dello stream di dati, abilita l&#39;opzione **[!UICONTROL Cookie ID di prime parti]**. Questa impostazione indica all&#39;Edge Network di fare riferimento a un cookie specificato durante la ricerca di un ID dispositivo di prime parti, anziché cercare questo valore nella [mappa identità](#identityMap).

Consulta la documentazione su [cookie di prime parti](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=it) per ulteriori dettagli sul loro funzionamento con Adobe Experience Cloud.

![Immagine dell&#39;interfaccia utente di Platform che mostra la configurazione dello stream di dati evidenziando l&#39;impostazione del cookie ID di prime parti](../assets/first-party-id-datastreams.png)

Quando abiliti questa impostazione, devi fornire il nome del cookie in cui si prevede che l’ID venga memorizzato.

Quando utilizzi ID di prime parti, non puoi eseguire sincronizzazioni ID di terze parti. Le sincronizzazioni ID di terze parti si basano sul servizio [!DNL Visitor ID] e sul `UUID` generati da tale servizio. Quando si utilizza la funzionalità ID di prima parte, [!DNL ECID] viene generato senza l&#39;utilizzo del servizio [!DNL Visitor ID], rendendo impossibile le sincronizzazioni ID di terze parti.

Quando si utilizzano ID di prime parti, le funzionalità [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager) mirate all&#39;attivazione nelle piattaforme partner non sono supportate, dato che le sincronizzazioni degli ID partner Audience Manager sono per lo più basate su `UUIDs` o `DIDs`. [!DNL ECID] derivato da un ID di prima parte non è collegato a un `UUID`, rendendolo non indirizzabile.

## Impostazione di un cookie con il tuo server {#set-cookie-server}

Quando imposti un cookie utilizzando un server di tua proprietà, puoi utilizzare diversi metodi per impedire che il cookie sia soggetto a restrizioni a causa dei criteri del browser:

* Generare cookie utilizzando linguaggi di script lato server
* Imposta i cookie in risposta a una richiesta API effettuata a un sottodominio o a un altro endpoint sul sito
* Genera cookie utilizzando [!DNL CMS]
* Genera cookie utilizzando [!DNL CDN]

>[!IMPORTANT]
>
>I cookie impostati con il metodo `document.cookie` di JavaScript non saranno quasi mai protetti dai criteri del browser che limitano la durata dei cookie.

### Quando impostare il cookie {#when-to-set-cookie}

Il cookie [!DNL FPID] dovrebbe idealmente essere impostato prima di effettuare qualsiasi richiesta all&#39;Edge Network. Tuttavia, negli scenari in cui ciò non è possibile, [!DNL ECID] viene ancora generato utilizzando i metodi esistenti e funge da identificatore primario finché il cookie esiste.

Supponendo che [!DNL ECID] sia infine interessato da un criterio di eliminazione del browser, ma [!DNL FPID] non lo è, [!DNL FPID] diventerà l&#39;identificatore primario alla visita successiva e verrà utilizzato per seed [!DNL ECID] a ogni visita successiva.

### Impostazione della scadenza per il cookie {#set-expiration}

L&#39;impostazione della scadenza di un cookie è un&#39;operazione da considerare attentamente durante l&#39;implementazione della funzionalità [!DNL FPID]. Nel decidere questa opzione, è necessario considerare i paesi o le aree geografiche in cui l&#39;organizzazione opera insieme alle leggi e alle politiche in ognuna di queste aree.

Come parte di questa decisione, puoi adottare un criterio di impostazione dei cookie a livello aziendale o diverso a seconda delle impostazioni internazionali.

Indipendentemente dall’impostazione scelta per la scadenza iniziale di un cookie, è necessario assicurarsi di includere una logica che estenda la scadenza del cookie ogni volta che si verifica una nuova visita al sito.

## Impatto dei flag dei cookie {#cookie-flag-impact}

Esistono diversi flag di cookie che influiscono sul modo in cui i cookie vengono trattati nei diversi browser:

* [&quot;HTTPOnly&quot;](#http-only)
* [&quot;Secure&quot;](#secure)
* [&quot;SameSite&quot;](#same-site)

### `HTTPOnly` {#http-only}

Impossibile accedere ai cookie impostati con il flag `HTTPOnly` utilizzando script lato client. Ciò significa che se si imposta un flag `HTTPOnly` durante l&#39;impostazione di [!DNL FPID], è necessario utilizzare un linguaggio di script lato server per leggere il valore del cookie da includere in `identityMap`.

Se si sceglie di far leggere all&#39;Edge Network il valore del cookie [!DNL FPID], l&#39;impostazione del flag `HTTPOnly` garantisce che il valore non sia accessibile da alcuno script lato client, ma non avrà alcun impatto negativo sulla capacità dell&#39;Edge Network di leggere il cookie.

>[!NOTE]
>
>L&#39;utilizzo del flag `HTTPOnly` non ha alcun impatto sui criteri dei cookie che possono limitare la durata dei cookie. Tuttavia, si tratta comunque di un aspetto da considerare durante l&#39;impostazione e la lettura del valore di [!DNL FPID].

### `Secure` {#secure}

I cookie impostati con l&#39;attributo `Secure` vengono inviati solo al server con una richiesta crittografata tramite il protocollo [!DNL HTTPS]. L’utilizzo di questo flag può contribuire a garantire che gli aggressori man-in-the-middle non possano accedere facilmente al valore del cookie. Quando possibile, è sempre consigliabile impostare il flag `Secure`.

### `SameSite` {#same-site}

L&#39;attributo `SameSite` consente ai server di determinare se i cookie vengono inviati con richieste intersito. L’attributo fornisce una certa protezione contro gli attacchi di tipo cross-site forgery. Esistono tre valori possibili: `Strict`, `Lax` e `None`. Consulta il team interno per determinare quale impostazione è corretta per la tua organizzazione.

Se non viene specificato alcun attributo `SameSite`, l&#39;impostazione predefinita per alcuni browser è ora `SameSite=Lax`.

## Utilizzo di FPID in `identityMap` {#identityMap}

Di seguito è riportato un esempio di come impostare un [!DNL FPID] in `identityMap`:

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

Come con altri tipi di identità, è possibile includere [!DNL FPID] con altre identità all&#39;interno di `identityMap`. Di seguito è riportato un esempio di [!DNL FPID] incluso con un [!DNL CRM ID] autenticato:

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

Se [!DNL FPID] è contenuto in un cookie letto dall&#39;Edge Network quando la raccolta dati di prime parti è abilitata, è necessario acquisire solo [!DNL CRM ID] autenticato:

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

`identityMap` genererebbe una risposta di errore dall&#39;Edge Network poiché manca l&#39;indicatore `primary` per [!DNL FPID]. Almeno uno degli ID presenti in `identityMap` deve essere contrassegnato come `primary`.

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

## Impostazione di un FPID sul proprio dominio {#setting-fpid-domain}

Oltre a impostare [!DNL FPID] nella mappa delle identità, puoi impostare il cookie [!DNL FPID] sul tuo dominio, se hai configurato una raccolta dati di prime parti [!DNL CNAME].

Quando la raccolta dati di prime parti viene abilitata utilizzando [!DNL CNAME], tutti i cookie per il dominio verranno inviati su richieste effettuate all&#39;endpoint di raccolta dati.

Vengono eliminati tutti i cookie non rilevanti ai fini della raccolta dati di Adobe. Per [!DNL FPID], è possibile specificare il nome del cookie [!DNL FPID] nella configurazione dello stream di dati. In questo caso, l&#39;Edge Network leggerà il contenuto del cookie [!DNL FPID] invece di cercare [!DNL FPID] nella mappa delle identità.

Per utilizzare questa funzionalità, è necessario impostare [!DNL FPID] al livello principale del dominio anziché a un sottodominio specifico. Se viene impostato su un sottodominio, il valore del cookie non verrà inviato all&#39;Edge Network e la soluzione [!DNL FPID] non funzionerà come previsto.

## Gerarchia ID {#id-hierarchy}

Quando sono presenti sia un [!DNL ECID] che un [!DNL FPID], l&#39;utente [!DNL ECID] ha la priorità nell&#39;identificazione dell&#39;utente. In questo modo, quando un [!DNL ECID] esistente è presente nell&#39;archivio dei cookie del browser, rimane l&#39;identificatore primario e i conteggi dei visitatori esistenti non rischiano di essere interessati. Per gli utenti esistenti, [!DNL FPID] non diventerà l&#39;identità primaria fino alla scadenza di [!DNL ECID] o all&#39;eliminazione a seguito di un criterio del browser o di un processo manuale.

Le identità hanno la priorità nel seguente ordine:

1. [!DNL ECID] inclusi in `identityMap`
1. [!DNL ECID] archiviato in un cookie
1. [!DNL FPID] inclusi in `identityMap`
1. [!DNL FPID] archiviato in un cookie

## Migrazione agli ID dispositivo di prime parti {#migrating-to-fpid}

Se stai eseguendo la migrazione agli ID dispositivo di prime parti da un’implementazione precedente, potrebbe essere difficile visualizzare l’aspetto della transizione a un livello basso.

Per illustrare questo processo, considera uno scenario che coinvolge un cliente che ha già visitato il tuo sito e quale impatto avrebbe una migrazione di [!DNL FPID] sul modo in cui tale cliente viene identificato nelle soluzioni Adobe.

![Diagramma che mostra come i valori ID di un cliente vengono aggiornati tra le visite dopo la migrazione a FPID](../assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>Il cookie `ECID` ha sempre la priorità rispetto a `FPID`.

| Visita | Descrizione |
| --- | --- |
| Prima visita | Si supponga di non aver ancora iniziato a impostare il cookie [!DNL FPID]. Il [!DNL ECID] contenuto nel [cookie AMCV](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) sarà l&#39;identificatore utilizzato per identificare il visitatore. |
| Seconda visita | Rollout della soluzione [!DNL FPID] avviato. [!DNL ECID] esistente è ancora presente e rimane l&#39;identificatore primario per l&#39;identificazione dei visitatori. |
| Terza visita | Tra la seconda e la terza visita, è trascorso abbastanza tempo che [!DNL ECID] è stato eliminato a causa dei criteri del browser. Tuttavia, poiché [!DNL FPID] è stato impostato utilizzando un record [!DNL A] di [!DNL DNS], [!DNL FPID] persiste. [!DNL FPID] è ora considerato l&#39;ID primario ed è utilizzato per eseguire il seeding di [!DNL ECID], che viene scritto sul dispositivo dell&#39;utente finale. L’utente viene ora considerato un nuovo visitatore nelle soluzioni Adobe Experience Platform e Experience Cloud. |
| Quarta visita | Tra la terza e la quarta visita, è trascorso abbastanza tempo che [!DNL ECID] è stato eliminato a causa dei criteri del browser. Analogamente alla visita precedente, [!DNL FPID] rimane dovuto al modo in cui è stato impostato. Questa volta viene generato lo stesso [!DNL ECID] della visita precedente. L’utente viene visualizzato in tutte le soluzioni di Experience Platform e Experience Cloud come lo stesso utente della visita precedente. |
| Quinta visita | Tra la quarta e la quinta visita, l’utente finale ha cancellato tutti i cookie nel suo browser. Viene generato un nuovo [!DNL FPID] e utilizzato per la creazione di un nuovo [!DNL ECID]. L’utente viene ora considerato un nuovo visitatore nelle soluzioni Adobe Experience Platform e Experience Cloud. |

{style="table-layout:auto"}

## Domande frequenti {#faq}

Di seguito è riportato un elenco di risposte alle domande più frequenti sugli ID dispositivo di prime parti.

### In che modo il seeding di un ID è diverso dalla semplice generazione di un ID?

Il concetto di seeding è univoco in quanto [!DNL FPID] passato a Adobe Experience Cloud viene convertito in [!DNL ECID] utilizzando un algoritmo deterministico. Ogni volta che lo stesso [!DNL FPID] viene inviato all&#39;Edge Network, lo stesso [!DNL ECID] viene preimpostato da [!DNL FPID].

### Quando deve essere generato l’ID dispositivo di prime parti?

Per ridurre l&#39;inflazione di visitatori potenziali, è necessario generare [!DNL FPID] prima di effettuare la prima richiesta tramite Web SDK. Tuttavia, se non è possibile eseguire questa operazione, verrà comunque generato un [!DNL ECID] per tale utente che verrà utilizzato come identificatore primario. Il [!DNL FPID] generato diventerà l&#39;identificatore primario solo dopo che [!DNL ECID] non sarà più presente.

### Quali metodi di raccolta dati supportano gli ID dispositivo di prime parti?

Attualmente solo Web SDK supporta gli ID dispositivo di prime parti.

### Gli ID dispositivo di prime parti sono memorizzati su qualsiasi piattaforma o soluzione Experience Cloud?

Una volta che [!DNL FPID] è stato utilizzato per il seeding di un [!DNL ECID], viene eliminato da `identityMap` e sostituito con [!DNL ECID] generato. [!DNL FPID] non è archiviato in alcuna soluzione Adobe Experience Platform o Experience Cloud.
