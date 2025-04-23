---
title: Utilizzare gli ID dispositivo di prime parti in Web SDK
description: Scopri come configurare gli ID dispositivo di prime parti (FPID) in Adobe Experience Platform Web SDK.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: c7be2fff2cd94677b745e6ed095454bc46f8a37b
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 0%

---


# Utilizzare gli ID dispositivo di prime parti in Web SDK

Adobe Experience Platform Web SDK assegna [ID Adobe Experience Cloud (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=it) ai visitatori del sito Web che utilizzano i cookie per monitorare il comportamento degli utenti. Per risolvere le restrizioni del browser relative alla durata dei cookie, puoi impostare e gestire gli identificatori dei tuoi dispositivi, noti come ID dispositivo di prime parti (FPID, first party device ID).

>[!NOTE]
>
>Il supporto per gli ID dispositivo di prime parti è disponibile solo quando si inviano dati ad Experience Platform Edge Network tramite Web SDK.

>[!IMPORTANT]
>
>Gli ID dispositivo di prime parti non sono compatibili con la funzionalità [cookie di terze parti](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity) in Web SDK. Puoi utilizzare sia ID dispositivo di prima parte che cookie di terze parti, ma non entrambi simultaneamente.

## Prerequisiti {#prerequisites}

Prima di iniziare, assicurati di conoscere il funzionamento dei dati di identità nel Web SDK, inclusi gli ECID e `identityMap`. Per ulteriori informazioni, vedere la panoramica sui [dati di identità nel Web SDK](./overview.md).

## Requisiti di formattazione degli ID dispositivo di prime parti {#formatting-requirements}

Edge Network accetta solo ID conformi al formato [UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). Gli ID dispositivo non in formato UUIDv4 verranno rifiutati.

* [!DNL UUIDs] sono univoci e casuali, con una probabilità di collisione trascurabile.
* Impossibile eseguire il seeding di [!DNL UUIDv4] utilizzando indirizzi IP o qualsiasi altra informazione personale identificabile (PII).
* Le librerie per generare [!DNL UUIDs] sono disponibili per ogni linguaggio di programmazione.

## Imposta il cookie [!DNL FPID] utilizzando il tuo server {#set-cookie-server}

Quando imposti un cookie tramite il tuo server, puoi utilizzare diversi metodi per impedire che il cookie sia soggetto a restrizioni a causa dei criteri del browser:

* Generare cookie utilizzando linguaggi di script lato server
* Imposta i cookie in risposta a una richiesta API effettuata a un sottodominio o a un altro endpoint sul sito
* Genera cookie utilizzando [!DNL CMS]
* Genera cookie utilizzando [!DNL CDN]

Inoltre, è sempre necessario impostare il cookie FPID sotto il record `A` del dominio.

>[!IMPORTANT]
>
>I cookie impostati con il metodo `document.cookie` di JavaScript non saranno quasi mai protetti dai criteri del browser che limitano la durata dei cookie.

### Quando impostare il cookie {#when-to-set-cookie}

Il cookie [!DNL FPID] dovrebbe idealmente essere impostato prima di effettuare qualsiasi richiesta ad Edge Network. Tuttavia, negli scenari in cui ciò non è possibile, [!DNL ECID] viene ancora generato utilizzando i metodi esistenti e funge da identificatore primario finché il cookie esiste.

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

Se si sceglie di fare in modo che Edge Network legga il valore del cookie [!DNL FPID], l&#39;impostazione del flag `HTTPOnly` garantisce che il valore non sia accessibile da alcuno script lato client, ma non avrà alcun impatto negativo sulla capacità di Edge Network di leggere il cookie.

>[!NOTE]
>
>L&#39;utilizzo del flag `HTTPOnly` non ha alcun impatto sui criteri dei cookie che possono limitare la durata dei cookie. Tuttavia, si tratta comunque di un aspetto da considerare durante l&#39;impostazione e la lettura del valore di [!DNL FPID].

### `Secure` {#secure}

I cookie impostati con l&#39;attributo `Secure` vengono inviati solo al server con una richiesta crittografata tramite il protocollo [!DNL HTTPS]. L’utilizzo di questo flag può contribuire a garantire che gli aggressori man-in-the-middle non possano accedere facilmente al valore del cookie. Quando possibile, è sempre consigliabile impostare il flag `Secure`.

### `SameSite` {#same-site}

L&#39;attributo `SameSite` consente ai server di determinare se i cookie vengono inviati con richieste intersito. L’attributo fornisce una certa protezione contro gli attacchi di tipo cross-site forgery. Esistono tre valori possibili: `Strict`, `Lax` e `None`. Consulta il team interno per determinare quale impostazione è corretta per la tua organizzazione.

Se non viene specificato alcun attributo `SameSite`, l&#39;impostazione predefinita per alcuni browser è ora `SameSite=Lax`.

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
| Quarta visita | Tra la terza e la quarta visita, è trascorso abbastanza tempo che [!DNL ECID] è stato eliminato a causa dei criteri del browser. Analogamente alla visita precedente, [!DNL FPID] rimane dovuto al modo in cui è stato impostato. Questa volta viene generato lo stesso [!DNL ECID] della visita precedente. L’utente viene visualizzato nelle soluzioni Experience Platform e Experience Cloud come lo stesso utente della visita precedente. |
| Quinta visita | Tra la quarta e la quinta visita, l’utente finale ha cancellato tutti i cookie nel suo browser. Viene generato un nuovo [!DNL FPID] e utilizzato per la creazione di un nuovo [!DNL ECID]. L’utente viene ora considerato un nuovo visitatore nelle soluzioni Adobe Experience Platform e Experience Cloud. |

{style="table-layout:auto"}

## Utilizzo degli ID dispositivo di prime parti (FPID) {#using-fpid}

Gli ID dispositivo di prime parti ([!DNL FPIDs]) tengono traccia dei visitatori utilizzando cookie di prime parti. I cookie di prime parti sono più efficaci quando vengono impostati utilizzando un server che utilizza un [record A](https://datatracker.ietf.org/doc/html/rfc1035) DNS (per IPv4) o un [record AAAA](https://datatracker.ietf.org/doc/html/rfc3596) DNS (per IPv6), anziché un codice DNS [!DNL CNAME] o [!DNL JavaScript].

>[!IMPORTANT]
>
>I record [!DNL A] o [!DNL AAAA] sono supportati solo per l&#39;impostazione e il tracciamento dei cookie. Il metodo principale per la raccolta dei dati è tramite [!DNL DNS CNAME]. [!DNL FPIDs] sono impostati utilizzando un record [!DNL A] o [!DNL AAAA] e inviati ad Adobe utilizzando un [!DNL CNAME].
>
>Il [programma di certificazione gestito da Adobe](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) è supportato anche per la raccolta dati di prime parti.

Una volta impostato il cookie [!DNL FPID], il relativo valore può essere recuperato e inviato ad Adobe durante la raccolta dei dati dell&#39;evento. I [!DNL FPIDs] raccolti vengono utilizzati per generare [!DNL ECIDs], che sono gli identificatori primari nelle applicazioni Adobe Experience Cloud.

È possibile utilizzare [!DNL FPIDs] in due modi:

* **[Metodo 1](#setting-cookie-datastreams)**: configurare [!DNL CNAME] per le chiamate Web SDK e includere il nome del cookie [!DNL FPID] nella configurazione dello stream di dati.
* **[Metodo 2](#identityMap)**: includere [!DNL FPID] nella mappa delle identità. Per ulteriori informazioni, consulta la sezione più avanti in questo documento sull&#39;utilizzo degli FPID in `identityMap`](#identityMap) per [.

### Metodo 1: configurare un CNAME per le chiamate Web SDK e impostare un cookie ID di prime parti nello stream di dati {#setting-cookie-datastreams}

Per impostare un cookie [!DNL FPID] dal proprio dominio, è necessario configurare il proprio [!DNL CNAME] (nome canonico) per le chiamate di Web SDK, quindi abilitare la funzionalità [!DNL First Party ID Cookie] nella configurazione dello stream di dati.

**Passaggio 1. Configurare un CNAME per il dominio di distribuzione di Web SDK**

Un record [!DNL CNAME] nel DNS consente di creare un alias da un nome di dominio a un altro. Questo può aiutare a far apparire i servizi di terze parti come se facessero parte del tuo dominio, rendendo così i loro cookie simili ai cookie di prima parte.

**Esempio**

Si supponga di voler implementare Web SDK nel sito Web `mywebsite.com`. Il Web SDK invia i dati ad Edge Network al dominio `edge.adobedc.net`.

| Senza [!DNL CNAME] | Con [!DNL CNAME] |
|---------|----------|
| <ul><li>Il sito Web `mywebsite.com` utilizza il dominio Web SDK `edge.adobedc.net` per inviare dati ad Edge Network.</li><li>I cookie impostati da `edge.adobedc.net` sono considerati cookie di terze parti poiché non provengono dal dominio `mywebsite.com`. A seconda degli utenti e dei browser utilizzati, i cookie di terze parti potrebbero essere bloccati e i dati non raggiungono Edge Network.</li></ul> | <ul><li>Si crea un sottodominio in cui viene distribuito Web SDK, ad esempio `metrics.mywebsite.com`.</li><li>Hai impostato un record [!DNL CNAME] nel tuo sistema DNS in modo che `metrics.mywebsite.com` punti a `edge.adobedc.net`.</li><li>Quando il sito Web imposta i cookie tramite `metrics.mywebsite.com`, appariranno come provenienti da `mywebsite.com` (prime parti) invece di `edge.adobedc.net` (terze parti). In questo modo il cookie ID di prima parte ha meno probabilità di essere bloccato e viene quindi garantita una raccolta più accurata dei dati.</li></ul> |

Quando la raccolta dati di prime parti viene abilitata utilizzando [!DNL CNAME], tutti i cookie per il dominio verranno inviati su richieste effettuate all&#39;endpoint di raccolta dati.

Per utilizzare questa funzionalità, è necessario impostare il cookie [!DNL FPID] al livello principale del dominio anziché a un sottodominio specifico. Se lo imposti su un sottodominio, il valore del cookie non verrà inviato all&#39;Edge Network e la soluzione [!DNL FPID] non funzionerà come previsto.

>[!IMPORTANT]
>
>Questa funzionalità richiede l&#39;abilitazione di [Raccolta dati di prime parti](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=en).

**Passaggio 2. Abilita la funzionalità**[!UICONTROL  Cookie ID di prime parti ]**per lo stream di dati**

Dopo aver configurato il tuo CNAME, devi abilitare l&#39;opzione **[!UICONTROL Cookie ID di prime parti]** per il tuo flusso di dati. Questa impostazione indica ad Edge Network di fare riferimento a un cookie specificato durante la ricerca di un ID dispositivo di prime parti, invece di cercare questo valore nella [mappa identità](#identityMap).

Consulta la [documentazione sulla configurazione dello stream di dati](../../datastreams/configure.md#advanced-options) per scoprire come impostare lo stream di dati.

Consulta la documentazione su [cookie di prime parti](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=it) per ulteriori dettagli sul loro funzionamento con Adobe Experience Cloud.

![Immagine dell&#39;interfaccia utente di Platform che mostra la configurazione dello stream di dati evidenziando l&#39;impostazione del cookie ID di prime parti](../assets/first-party-id-datastreams.png)

Quando si abilita questa impostazione, è necessario fornire il nome del cookie in cui è prevista la memorizzazione di [!DNL FPID].

>[!NOTE]
>
>Quando utilizzi ID di prime parti, non puoi eseguire sincronizzazioni ID di terze parti. Le sincronizzazioni ID di terze parti si basano sul servizio [!DNL Visitor ID] e sul `UUID` generati da tale servizio. Quando si utilizza la funzionalità ID di prima parte, [!DNL ECID] viene generato senza l&#39;utilizzo del servizio [!DNL Visitor ID], rendendo impossibile le sincronizzazioni ID di terze parti.
><br> Quando si utilizzano ID di prime parti, le funzionalità [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager) mirate all&#39;attivazione nelle piattaforme partner non sono supportate, dato che le sincronizzazioni degli ID partner Audience Manager sono basate principalmente su `UUIDs` o `DIDs`. [!DNL ECID] derivato da un ID di prima parte non è collegato a un `UUID`, rendendolo non indirizzabile.

## Metodo 2: utilizzare gli FPID in `identityMap` {#identityMap}

In alternativa all&#39;archiviazione di [!DNL FPID] nel proprio cookie, è possibile inviare [!DNL FPID] ad Edge Network tramite la mappa delle identità.

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

Se [!DNL FPID] è contenuto in un cookie letto da Edge Network quando è abilitata la raccolta dati di prime parti, è necessario acquisire solo [!DNL CRM ID] autenticato:

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

`identityMap` genererebbe una risposta di errore da parte di Edge Network poiché manca l&#39;indicatore `primary` per [!DNL FPID]. Almeno uno degli ID presenti in `identityMap` deve essere contrassegnato come `primary`.

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

La risposta di errore restituita da Edge Network in questo caso è simile alla seguente:

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

## Domande frequenti {#faq}

Di seguito è riportato un elenco di risposte alle domande più frequenti sugli ID dispositivo di prime parti.

### In che modo il seeding di un ID è diverso dalla semplice generazione di un ID?

Il concetto di seeding è univoco in quanto [!DNL FPID] passato a Adobe Experience Cloud viene convertito in [!DNL ECID] utilizzando un algoritmo deterministico. Ogni volta che lo stesso [!DNL FPID] viene inviato ad Edge Network, lo stesso [!DNL ECID] viene preimpostato da [!DNL FPID].

### Quando deve essere generato l’ID dispositivo di prime parti?

Per ridurre l&#39;inflazione di visitatori potenziali, è necessario generare [!DNL FPID] prima di effettuare la prima richiesta tramite Web SDK. Tuttavia, se non è possibile eseguire questa operazione, verrà comunque generato un [!DNL ECID] per tale utente che verrà utilizzato come identificatore primario. Il [!DNL FPID] generato diventerà l&#39;identificatore primario solo dopo che [!DNL ECID] non sarà più presente.

### Quali metodi di raccolta dati supportano gli ID dispositivo di prime parti?

Attualmente solo Web SDK supporta gli ID dispositivo di prime parti.

### Gli ID dispositivo di prime parti sono memorizzati su qualsiasi soluzione Platform o Experience Cloud?

Una volta che [!DNL FPID] è stato utilizzato per il seeding di un [!DNL ECID], viene eliminato da `identityMap` e sostituito con [!DNL ECID] generato. [!DNL FPID] non è archiviato in alcuna soluzione Adobe Experience Platform o Experience Cloud.
