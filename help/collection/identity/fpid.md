---
title: Utilizzare gli ID dispositivo di prime parti nella raccolta dati
description: Configura gli ID dispositivo di prime parti (FPID) per l’identità durevole nelle implementazioni web che inviano dati ad Edge Network.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1905'
ht-degree: 0%

---

# Utilizzare gli ID dispositivo di prime parti nella raccolta dati

L’Edge Network di Experience Platform utilizza gli Experience Cloud ID (ECID) per identificare i visitatori del sito web. Per migliorare la durata dell’identità nelle proprietà di tua proprietà, puoi impostare e gestire i tuoi identificatori di dispositivo, noti come ID dispositivo di prime parti (FPID, first party device ID). Edge Network utilizza l’FPID per seed l’ECID utilizzato dalle soluzioni Adobe.

In questa pagina si presuppone che tu abbia familiarità con gli ECID e `identityMap`. Per ulteriori informazioni, vedere [Identità nella raccolta dati](./overview.md).

## Quando utilizzare gli FPID {#when-to-use}

Le restrizioni relative ai browser possono ridurre la durata dei cookie utilizzati da Adobe per riconoscere i visitatori di ritorno. Se hai bisogno di un’identità più durevole sui siti di proprietà e controllo della tua organizzazione, gli FPID ti consentono di gestire il tuo identificatore del dispositivo e di utilizzarlo per seed l’ECID.

Gli FPID sono supportati per le implementazioni web che utilizzano Web SDK, inclusa l’estensione tag Web SDK. Sono ideali quando l’obiettivo principale è una persistenza dell’identità più forte sui domini di proprietà della tua organizzazione oppure desideri una maggiore continuità per il reporting e la personalizzazione sulle proprietà web di proprietà. Consentono inoltre di impostare e gestire un cookie di prime parti dall’infrastruttura controllata.

Gli FPID non sono lo strumento giusto quando l’obiettivo principale è lo scambio da app a web o la continuità delle identità tra più domini. Per questi scenari, vedi [condivisione delle identità da dispositivo mobile a Web](./mobile-to-web.md) e [condivisione tra domini](./cross-domain-sharing.md).

I vantaggi dell&#39;utilizzo degli FPID includono:

* Persistenza più elevata sulle proprietà possedute.
* Maggiore controllo sulla modalità di generazione e gestione dell’identificatore del dispositivo.
* Una base solida per l’analisi e la personalizzazione.

I compromessi per l’utilizzo degli FPID includono:

* Maggiore responsabilità nell’implementazione rispetto al comportamento di identità predefinito.
* Coordinamento nella logica dei cookie lato server e nella configurazione della raccolta dati.
* Convalida aggiuntiva per confermare che l’identificatore è utilizzato come previsto.

### Percorso di configurazione di alto livello

1. Genera e gestisci un ID dispositivo di prime parti sull’infrastruttura che controlli.
1. Configura l&#39;implementazione per leggere tale ID da un [cookie di prime parti](#setting-cookie-datastreams) o dal [payload di identità](#identityMap).
1. Verifica che i visitatori di ritorno mantengano un’identità coerente nel tempo sulle proprietà di tua proprietà.

## Funzionamento degli FPID {#how-fpids-work}

L’FPID passato a Adobe Experience Cloud viene convertito in un ECID utilizzando un algoritmo deterministico. Ogni volta che lo stesso FPID viene inviato all’Edge Network, viene generato lo stesso ECID dall’FPID. Una volta utilizzato per il seeding di un ECID, l&#39;FPID viene rimosso da `identityMap` e sostituito con l&#39;ECID generato. L&#39;FPID non è memorizzato nelle soluzioni Adobe Experience Platform o Experience Cloud.

Quando esistono sia un ECID che un FPID, l’ECID viene sempre utilizzato per identificare prima l’utente. Con questa definizione di priorità, quando un ECID esistente è presente nell’archivio dei cookie del browser, rimane l’identificatore primario e i conteggi dei visitatori esistenti non rischiano l’inflazione. Per gli utenti esistenti, l’FPID non diventa l’identità primaria fino alla scadenza dell’ECID o alla sua eliminazione in seguito a criteri del browser o azioni manuali.

Le identità hanno la priorità nel seguente ordine:

1. ECID incluso in `identityMap`
1. ECID memorizzato in un cookie
1. FPID incluso in `identityMap`
1. FPID memorizzato in un cookie

## Generare e impostare il cookie FPID {#set-fpid-cookie}

Edge Network accetta solo ID conformi al formato [UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). Gli ID dispositivo non in formato UUIDv4 vengono rifiutati.

* Gli UUID sono univoci e casuali, con una probabilità di collisione trascurabile.
* Non è possibile eseguire il seeding di UUIDv4 utilizzando indirizzi IP o altre informazioni personali (PII, personally identifiable information).
* Le librerie per la generazione di UUID sono disponibili per ogni linguaggio di programmazione.

### Impostazione dei cookie lato server {#set-cookie-server}

Quando imposti un cookie tramite il tuo server, puoi utilizzare diversi metodi per evitare che i criteri del browser limitino il cookie:

* Generare cookie utilizzando linguaggi di script lato server
* Imposta i cookie in risposta a una richiesta API effettuata a un sottodominio o a un altro endpoint sul sito
* Generare cookie utilizzando un sistema di gestione dei contenuti (CMS)
* Generare cookie utilizzando una rete CDN (Content Delivery Network)

I cookie di prime parti sono più efficaci quando vengono impostati utilizzando un server che utilizza un [record A](https://datatracker.ietf.org/doc/html/rfc1035) DNS (per IPv4) o un [record AAAA](https://datatracker.ietf.org/doc/html/rfc3596) DNS (per IPv6), anziché un codice DNS `CNAME` o JavaScript.

>[!IMPORTANT]
>
>I cookie impostati con il metodo `document.cookie` di JavaScript (incluso l&#39;utilizzo del metodo tag [`cookie.set()`](../tags/cookie.md)) non sono quasi mai protetti dai criteri del browser che limitano la durata dei cookie.

I record `A` o `AAAA` sono supportati solo per l&#39;impostazione e il tracciamento dei cookie. Il metodo principale per la raccolta dei dati è tramite un DNS `CNAME`. Gli FPID vengono impostati utilizzando un record `A` o `AAAA` e inviati ad Adobe utilizzando un `CNAME`. Il [programma di certificazione gestito da Adobe](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) consente di configurare `CNAME` per la raccolta dati.

### Quando impostare il cookie {#when-to-set-cookie}

Il cookie FPID viene impostato idealmente prima di inviare dati ad Edge Network. Se l&#39;implementazione richiede il consenso prima di raccogliere i dati, consulta [Consenso con ID dispositivo di prime parti](./consent.md#consent-with-fpids) per informazioni su come coordinare il cookie FPID con il flusso di consenso. L’inflazione dei visitatori viene ridotta quando si assicura che l’FPID sia disponibile per seed l’ECID dalla prima richiesta. Negli scenari in cui ciò non è possibile, un ECID viene comunque generato utilizzando i metodi esistenti e funge da identificatore primario finché il cookie esiste. L’FPID generato non diventa l’identificatore primario fino a quando l’ECID non è più presente. Supponendo che l’ECID sia infine interessato da un criterio di eliminazione del browser, ma l’FPID non lo è, l’FPID diventa l’identificatore primario nella visita successiva e viene utilizzato per seed l’ECID in ogni visita successiva.

### Impostazione della scadenza {#set-expiration}

Adobe consiglia di considerare attentamente la durata del cookie FPID. Assicurati di tenere in considerazione l’informativa sulla privacy della tua organizzazione insieme alle leggi e alle politiche dei paesi o delle aree geografiche in cui opera l’organizzazione. A seconda della configurazione dell’organizzazione, è possibile adottare un criterio di impostazione dei cookie a livello aziendale o diverso a seconda delle impostazioni internazionali in cui si opera. Indipendentemente dalla scadenza iniziale dei cookie, accertati di includere una logica che estenda la scadenza ogni volta che si verifica una nuova visita al sito.

### Flag per cookie {#cookie-flags}

Esistono diversi flag di cookie che influiscono sul modo in cui i cookie vengono trattati nei diversi browser:

* **`HTTPOnly`**: impossibile accedere ai cookie impostati con il flag `HTTPOnly` utilizzando script lato client. Ciò significa che se si imposta un flag `HTTPOnly` durante l&#39;impostazione dell&#39;FPID, è necessario utilizzare un linguaggio di script lato server per leggere il valore del cookie da includere in `identityMap`. Se scegli di fare in modo che Edge Network legga il valore del cookie FPID, l&#39;impostazione del flag `HTTPOnly` assicura che il valore non sia accessibile dagli script lato client, ma non influisca negativamente sulla capacità di Edge Network di leggere il cookie. L&#39;utilizzo del flag `HTTPOnly` non influisce sui criteri dei cookie che possono limitare la durata dei cookie. Tuttavia, è ancora qualcosa da considerare quando imposti e leggi il valore dell’FPID.
* **`Secure`**: i cookie impostati con l&#39;attributo `Secure` vengono inviati solo al server con una richiesta crittografata tramite il protocollo HTTPS. L’utilizzo di questo flag può contribuire a garantire che gli aggressori man-in-the-middle non possano accedere facilmente al valore del cookie. Quando possibile, è sempre consigliabile impostare il flag `Secure`.
* **`SameSite`**: l&#39;attributo `SameSite` consente ai server di determinare se i cookie vengono inviati con richieste cross-site. L’attributo fornisce una certa protezione contro gli attacchi di tipo cross-site forgery. Esistono tre valori possibili: `Strict`, `Lax` e `None`. Consulta il team interno per determinare quale impostazione è corretta per la tua organizzazione. Se non viene specificato alcun attributo `SameSite`, l&#39;impostazione predefinita per alcuni browser è `SameSite=Lax`.

## Inviare l’FPID ad Edge Network {#send-fpid}

Puoi inviare gli FPID ad Edge Network in due modi:

* **[Metodo 1](#setting-cookie-datastreams)**: configurare `CNAME` per le chiamate Web SDK e includere il nome del cookie FPID nella configurazione dello stream di dati.
* **[Metodo 2](#identityMap)**: includere l&#39;FPID nella mappa delle identità.

### Metodo 1: configurare `CNAME` e impostare un cookie ID di prime parti nel flusso di dati {#setting-cookie-datastreams}

Per impostare un cookie FPID dal tuo dominio, devi configurare `CNAME` per le chiamate al Web SDK, quindi abilitare la funzionalità cookie ID di prime parti nella configurazione dello stream di dati. Un record `CNAME` nel DNS consente di creare un alias da un nome di dominio a un altro. Questo alias può aiutare a far apparire i servizi di terze parti come se facessero parte del tuo dominio, rendendo i loro cookie simili ai cookie di prime parti. Quando la raccolta dati di prime parti viene abilitata utilizzando `CNAME`, tutti i cookie per il dominio vengono inviati su richieste effettuate all&#39;endpoint di raccolta dati.

1. Utilizzare Adobe per creare un record `CNAME` da utilizzare per la raccolta dati nell&#39;organizzazione. Consulta il [programma di certificazione gestito da Adobe](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert) per l&#39;intero processo.
1. Abilita l&#39;opzione **[!UICONTROL First Party ID Cookie]** nello stream di dati. Questa impostazione indica all’Edge Network di fare riferimento al cookie specificato durante la ricerca di un ID dispositivo di prime parti invece di cercare il valore nella mappa delle identità. Quando abiliti questa impostazione, devi fornire il nome del cookie in cui si prevede che venga memorizzato l’FPID. Per ulteriori informazioni, vedere [Creare e configurare gli stream di dati](/help/datastreams/configure.md#advanced-options).

   ![Immagine dell&#39;interfaccia utente di Platform che mostra la configurazione dello stream di dati evidenziando l&#39;impostazione del cookie ID di prime parti](/help/collection/js/assets/first-party-id-datastreams.png)

### Metodo 2: utilizzare gli FPID in `identityMap` {#identityMap}

In alternativa all’archiviazione dell’FPID nel cookie, puoi inviare l’FPID ad Edge Network tramite la mappa identità.

Di seguito è riportato un esempio di come impostare un FPID in `identityMap`:

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

Come con altri tipi di identità, è possibile includere l&#39;FPID con altre identità all&#39;interno di `identityMap`. L’esempio seguente include l’FPID con un ID CRM autenticato:

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
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Se l’FPID è contenuto in un cookie letto da Edge Network quando è abilitata la raccolta dati di prime parti, acquisisci solo l’ID CRM autenticato:

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

`identityMap` genera una risposta di errore da Edge Network perché manca l&#39;indicatore `primary` per l&#39;FPID. Almeno uno degli ID presenti in `identityMap` deve essere contrassegnato come `primary`.

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
        "id": "user@example.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

## Migrazione a FPID {#migrating-to-fpid}

Se esegui la migrazione agli ID dispositivo di prime parti da un’implementazione precedente, può essere difficile visualizzare l’aspetto della transizione a un livello basso. Per illustrare questo processo, considera uno scenario che coinvolge un cliente che ha già visitato il tuo sito e quale impatto avrebbe una migrazione FPID su come quel cliente viene identificato nelle soluzioni Adobe.

![Diagramma che mostra come i valori ID di un cliente vengono aggiornati tra le visite dopo la migrazione a FPID](/help/collection/js/assets/identity/tracking/visits.png)

| Visita | Descrizione |
| --- | --- |
| Prima visita | Supponiamo che non abbiate ancora iniziato a impostare il cookie FPID. L&#39;ECID contenuto nel cookie [AMCV](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) è l&#39;identificatore utilizzato per identificare il visitatore. |
| Seconda visita | Rollout della soluzione FPID avviato. L’ECID esistente è ancora presente e rimane l’identificatore primario per l’identificazione dei visitatori. |
| Terza visita | Tra la seconda e la terza visita, è trascorso abbastanza tempo da consentire l’eliminazione dell’ECID a causa dei criteri del browser. Tuttavia, poiché l&#39;FPID è stato impostato utilizzando un record DNS `A`, l&#39;FPID persiste. L’FPID è ora considerato l’ID primario e viene utilizzato per seed l’ECID, che viene scritto sul dispositivo dell’utente finale. L’utente viene ora considerato un nuovo visitatore nelle soluzioni Adobe Experience Platform e Experience Cloud. |
| Quarta visita | Tra la terza e la quarta visita, è trascorso abbastanza tempo da consentire l’eliminazione dell’ECID a causa dei criteri del browser. Come la visita precedente, l’FPID rimane dovuto al modo in cui è stato impostato. Questa volta viene generato lo stesso ECID della visita precedente. L’utente viene visualizzato nelle soluzioni Adobe Experience Platform e Experience Cloud come lo stesso utente della visita precedente. |
| Quinta visita | Tra la quarta e la quinta visita, l’utente finale ha cancellato tutti i cookie nel browser. Viene generato un nuovo FPID e utilizzato per la creazione di un nuovo ECID. L’utente viene ora considerato un nuovo visitatore nelle soluzioni Adobe Experience Platform e Experience Cloud. |
