---
keywords: Experience Platform;home;IAB;IAB 2.0;
solution: Experience Platform
title: Supporto IAB TCF 2.0 nella piattaforma dati cliente in tempo reale
topic: privacy events
translation-type: tm+mt
source-git-commit: 67c598000cec36a170e7324877d4d9f2db9453a4
workflow-type: tm+mt
source-wordcount: '2362'
ht-degree: 1%

---


# Supporto IAB TCF 2.0 in [!DNL Real-time Customer Data Platform]

Il [!DNL Transparency & Consent Framework] (TCF), come delineato dall&#39; [!DNL Interactive Advertising Bureau] (IAB), è un quadro tecnico aperto volto a consentire alle organizzazioni di ottenere, registrare e aggiornare il consenso dei consumatori per il trattamento dei loro dati personali, in conformità con il GDPR [!DNL General Data Protection Regulation] (European Union&#39;s GDPR). La seconda iterazione del quadro, TCF 2.0, offre maggiore flessibilità per quanto riguarda il modo in cui i consumatori possono fornire o rifiutare il consenso, incluso se e come i venditori possono utilizzare determinate caratteristiche dell&#39;elaborazione dei dati, come una precisa geolocalizzazione.

>[!NOTE]
>
>Ulteriori informazioni su TCF 2.0 sono disponibili sul sito web [](https://iabeurope.eu/tcf-2-0/)IAB Europe, inclusi materiali di supporto e specifiche tecniche.

[!DNL Real-time Customer Data Platform (Real-time CDP)] fa parte dell&#39;elenco [di fornitori](https://iabeurope.eu/vendor-list-tcf-v2-0/)IAB TCF 2.0 registrato, sotto l&#39;ID **565**. In conformità ai requisiti di TCF 2.0, [!DNL Real-time CDP] puoi raccogliere i dati di consenso dei clienti e integrarli nei profili dei clienti memorizzati. Questi dati di consenso possono quindi essere presi in considerazione per stabilire se i profili sono inclusi nei segmenti di pubblico esportati, a seconda del loro caso di utilizzo.

>[!IMPORTANT]
>
>[!DNL Real-time CDP] è in grado di soddisfare solo la versione 2.0 del TCF (o superiore). Le versioni precedenti di TCF non sono supportate.

Questo documento fornisce una panoramica su come configurare le operazioni sui dati e gli schemi di profilo per accettare i dati di consenso dei clienti generati dal CMP e come [!DNL Real-time CDP] veicolare le scelte di consenso degli utenti al momento dell’esportazione dei segmenti.

## Prerequisiti

Per seguire questa guida, è necessario utilizzare una piattaforma di gestione del consenso (CMP), commerciale o propria, integrata e conforme allo IAB TCF. Per ulteriori informazioni, consultate l&#39; [elenco dei CMP](https://iabeurope.eu/cmp-list/) conformi.

>[!IMPORTANT]
>
>Se l’ID del CMP non è valido, [!DNL Real-time CDP] i dati verranno elaborati così come sono. Per applicare TCF 2.0, è necessario verificare che il CMP disponga di un ID valido registrato con IAB TCF 2.0 prima di inviare i dati a [!DNL Experience Platform].

Questa guida richiede anche una buona conoscenza dei seguenti servizi Adobe Experience Platform:

* [Experience Data Model (XDM)](../../../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
* [Servizio](../../../identity-service/home.md)identità Adobe Experience Platform: Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati relativi all&#39;esperienza dei clienti attraverso il collegamento di identità tra dispositivi e sistemi.
* [Profilo](../../../profile/home.md)cliente in tempo reale: Consente [!DNL Identity Service] di creare profili cliente dettagliati dai set di dati in tempo reale. [!DNL Real-time Customer Profile] estrae i dati dal Data Lake e persiste nei profili dei clienti nel proprio archivio dati separato.
* [Adobe Experience Platform Web SDK](../../../edge/home.md): Libreria JavaScript lato client che consente di integrare vari [!DNL Platform] servizi nel sito Web rivolto ai clienti.
* [Servizio](../../../segmentation/home.md)di segmentazione Adobe Experience Platform: Consente di suddividere [!DNL Real-time Customer Profile] i dati in gruppi di persone con caratteristiche simili e risponderà in modo simile alle strategie di marketing.

Oltre ai [!DNL Platform] servizi sopra elencati, è necessario avere familiarità con [le destinazioni](../../destinations/destinations-overview.md) e il loro uso in [!DNL Real-time CDP].

## Riepilogo flusso di consenso cliente {#summary}

Le sezioni seguenti descrivono il modo in cui i dati del consenso vengono raccolti e applicati dopo che il sistema è stato configurato correttamente.

### Raccolta dei dati di consenso

[!DNL Real-time CDP] consente di raccogliere i dati sul consenso dei clienti attraverso la procedura seguente:

1. Un cliente fornisce le proprie preferenze di consenso per la raccolta dei dati tramite una finestra di dialogo sul sito Web.
1. Il CMP rileva la modifica delle preferenze di consenso e genera di conseguenza i dati di consenso IAB.
1. Utilizzando [!DNL Experience Platform Web SDK], i dati di consenso generati (restituiti dal CMP) vengono inviati ad Adobe Experience Platform.
1. I dati di consenso raccolti vengono trasferiti in un dataset [!DNL Profile]abilitato il cui schema contiene campi di consenso IAB.

Oltre ai comandi SDK attivati dai ganci di modifica del consenso CMP, i dati di consenso possono fluire anche [!DNL Experience Platform] attraverso qualsiasi dato XDM generato dal cliente che viene caricato direttamente in un dataset [!DNL Profile]abilitato.

Tutti i segmenti condivisi con [!DNL Platform] Adobe Audience Manager (tramite il connettore [!DNL Audience Manager] di origine o in altro modo) possono anche contenere dati di consenso, a condizione che i campi appropriati siano stati applicati a tali segmenti attraverso [!DNL Experience Cloud Identity Service]. Per ulteriori informazioni sulla raccolta dei dati di consenso in [!DNL Audience Manager], vedere il documento sul plug-in [Adobe Audience Manager per IAB TCF](https://docs.adobe.com/help/it-IT/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### Esecuzione del consenso a valle

Una volta che i dati di consenso IAB sono stati correttamente assimilati, i seguenti processi si svolgono nei [!DNL Real-time CDP] servizi a valle:

1. [!DNL Real-time Customer Profile] aggiorna i dati del consenso memorizzati per il profilo del cliente.
1. [!DNL Real-time CDP] elabora gli ID cliente solo se l&#39;autorizzazione del fornitore per [!DNL Real-time CDP] (565) è fornita per ogni ID in un cluster.
1. Quando si esportano segmenti in destinazioni appartenenti a membri dell&#39;elenco dei fornitori di TCF 2.0, [!DNL Real-time CDP] vengono inclusi profili solo se le autorizzazioni del fornitore per sia [!DNL Real-time CDP] (565) che per ** la destinazione sono fornite per ogni ID in un cluster.

Le altre sezioni di questo documento forniscono indicazioni su come configurare [!DNL Real-time CDP] e gestire le operazioni relative ai dati per soddisfare i requisiti di raccolta e applicazione descritti in precedenza.

## Come generare i dati sul consenso dei clienti all’interno del CMP {#consent-data}

Poiché ogni sistema CMP è univoco, è necessario determinare il modo migliore per consentire ai clienti di fornire il consenso durante l&#39;interazione con il servizio. Un modo comune per ottenere questo risultato è tramite l&#39;utilizzo di una finestra di dialogo di consenso dei cookie, simile al seguente esempio:

![](../assets/iab/cmp-dialog.png)

Questa finestra di dialogo deve consentire al cliente di:

| Opzione Consenso | Descrizione |
| --- | --- |
| **Finalità** | Gli scopi definiscono a quali scopi di tecnologia dell&#39;annuncio un marchio può utilizzare i dati di un cliente. Per [!DNL Real-time CDP] elaborare gli ID cliente è necessario optare per i seguenti scopi: <ul><li>**Finalità 1**: Archiviare e/o accedere alle informazioni su un dispositivo</li><li>**Finalità 10**: Sviluppare e migliorare i prodotti</li></ul> |
| **Autorizzazioni fornitore** | Oltre agli scopi di supporto tecnico, la finestra di dialogo deve anche consentire al cliente di scegliere se utilizzare o meno i propri dati da fornitori specifici, incluso [!DNL  Real-time CDP] (565). |

### Consenso di stringhe {#consent-strings}

Indipendentemente dal metodo utilizzato per raccogliere i dati, l&#39;obiettivo è quello di generare un valore stringa basato sulle opzioni di consenso scelte dal cliente, denominate stringa **di** consenso.

Nella specifica TCF, le stringhe di consenso vengono utilizzate per codificare i dettagli rilevanti sulle impostazioni di consenso di un cliente, in termini di scopi di marketing specifici, come definiti da policy e fornitori. [!DNL Real-time CDP] utilizza queste stringhe per memorizzare le impostazioni del consenso per ciascun cliente, pertanto ogni volta che tali impostazioni cambiano è necessario generare una nuova stringa di consenso.

Le stringhe di consenso possono essere create solo da un CMP registrato con lo IAB TCF. Per ulteriori informazioni su come generare le stringhe di consenso utilizzando il CMP specifico, fare riferimento alla guida [alla formattazione delle stringhe di](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) consenso nel repo GitHub IAB TCF.

## Creazione di set di dati con campi di consenso IAB {#datasets}

I dati di consenso del cliente devono essere inviati a un set di dati il cui schema contiene campi di consenso IAB. Fare riferimento all&#39;esercitazione sulla [creazione di set di dati per l&#39;acquisizione del consenso](./dataset-preparation.md) TCF 2.0 per la creazione dei due set di dati richiesti prima di continuare con questa guida.

## Aggiornare i criteri [!DNL Profile] di unione per includere i dati di consenso {#merge-policies}

Dopo aver creato un set di dati [!DNL Profile]abilitato per la raccolta dei dati di consenso, devi assicurarti che i criteri di unione siano stati configurati in modo da includere sempre i campi di consenso IAB nei profili cliente. Ciò comporta l&#39;impostazione della precedenza del set di dati in modo che l&#39;insieme di dati del consenso abbia priorità rispetto ad altri set di dati potenzialmente in conflitto.

Per ulteriori informazioni sull&#39;utilizzo dei criteri di unione, consultare la guida [utente relativa ai criteri di](../../../profile/ui/merge-policies.md)unione. Quando imposti i criteri di unione, devi assicurarti che i tuoi segmenti includano tutti gli attributi di consenso richiesti dal mixin [privacy](./dataset-preparation.md#privacy-mixin)XDM, come indicato nella guida sulla preparazione dei set di dati.

## Integrare l’SDK [!DNL Experience Platform] Web per raccogliere i dati sul consenso dei clienti {#sdk}

>[!NOTE]
>
>L’uso dell’SDK [!DNL Experience Platform] Web è necessario per elaborare i dati di consenso direttamente in Adobe Experience Platform. [!DNL Experience Cloud Identity Service] al momento non è supportato.
>
>[!DNL Experience Cloud Identity Service] è ancora supportato per l&#39;elaborazione del consenso in Adobe Audience Manager, tuttavia, e la conformità con TCF 2.0 richiede solo che la libreria venga aggiornata alla [versione 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Una volta configurato il CMP per generare le stringhe di consenso, è necessario integrare l’SDK [!DNL Experience Platform] Web per raccogliere tali stringhe e inviarle a [!DNL Platform]. L’ [!DNL Platform] SDK fornisce due comandi che possono essere utilizzati per inviare dati di consenso IAB a Platform (descritti nelle sottosezioni seguenti) e che devono essere utilizzati quando un cliente fornisce informazioni di consenso per la prima volta, e in qualsiasi momento in cui il consenso viene modificato successivamente.

**L’SDK non interagisce con CMP**. Sta a voi determinare come integrare l’SDK nel vostro sito Web, ascoltare le modifiche del consenso nel CMP e chiamare il comando appropriato.

### Creare una nuova configurazione Edge

Affinché l’SDK invii dati a [!DNL Experience Platform], devi prima creare una nuova configurazione edge per [!DNL Platform] in [!DNL Adobe Experience Platform Launch]. I passaggi specifici per la creazione di una nuova configurazione sono descritti nella documentazione [](../../../edge/fundamentals/edge-configuration.md)SDK.

Dopo aver fornito un nome univoco per la configurazione, fate clic sul pulsante di attivazione accanto a *[!UICONTROL Adobe Experience Platform]*. Quindi, utilizzare i seguenti valori per completare il resto del modulo:

| Campo di configurazione Edge | Valore |
| --- | --- |
| [!UICONTROL Sandbox] | Il nome della [!DNL Platform] sandbox [](../../../sandboxes/home.md) che contiene la connessione di streaming e i set di dati richiesti per configurare la configurazione edge. |
| [!UICONTROL Streaming Inlet] | Una connessione di streaming valida per [!DNL Experience Platform]. Se non disponete di un&#39;entrata in streaming, vedete l&#39;esercitazione sulla [creazione di una connessione](../../../ingestion/tutorials/create-streaming-connection-ui.md) in streaming. |
| [!UICONTROL Event Dataset] | Selezionare il [!DNL XDM ExperienceEvent] set di dati creato nel passaggio [](#datasets)precedente. |
| [!UICONTROL Profile Dataset] | Selezionare il [!DNL XDM Individual Profile] set di dati creato nel passaggio [](#datasets)precedente. |

![](../assets/iab/edge-config.png)

Al termine, fate clic **[!UICONTROL Save]** nella parte inferiore della schermata e continuate a seguire eventuali altri prompt per completare la configurazione.

### Esecuzione di comandi di modifica del consenso

Dopo aver creato la configurazione edge descritta nella sezione precedente, potete iniziare a utilizzare i comandi SDK per inviare i dati di consenso a [!DNL Platform]. Le sezioni seguenti forniscono esempi di come ciascun comando SDK può essere utilizzato in scenari diversi.

>[!NOTE]
>
>Per un&#39;introduzione alla sintassi comune per tutti i comandi [!DNL Platform] SDK, consulta il documento sull&#39; [esecuzione dei comandi](../../../edge/fundamentals/executing-commands.md).

#### Utilizzo dei ganci di consenso CMP

Molti CMP forniscono ganci out-of-the-box che ascoltano gli eventi di consenso-cambiamento. Quando si verificano tali eventi, potete utilizzare il `setConsent` comando per aggiornare i dati di consenso del cliente.

Il `setConsent` comando prevede due argomenti: (1) una stringa che indica il tipo di comando (in questo caso, &quot;setConsent&quot;) e (2) un payload che contiene una `consent` matrice, che deve contenere almeno un oggetto che fornisce i campi di consenso richiesti, come illustrato di seguito:

```js
alloy("setConsent", {
  consent: [{
    standard: "IAB",
    version: "2.0",
    value: "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
    gdprApplies: "true"
  }]
});
```

| Payload, proprietà | Descrizione |
| --- | --- |
| `standard` | Standard di consenso utilizzato. Questo valore deve essere impostato su &quot;IAB&quot; per l&#39;elaborazione del consenso TCF 2.0. |
| `version` | Numero di versione dello standard di consenso indicato in `standard`. Questo valore deve essere impostato su &quot;2.0&quot; per l&#39;elaborazione del consenso TCF 2.0. |
| `value` | Stringa di consenso con codifica base 64 generata dal CMP. |
| `gdprApplies` | Un valore booleano che indica se il GDPR si applica al cliente attualmente connesso. Affinché TCF 2.0 sia applicato a questo cliente, il valore deve essere impostato su &quot;true&quot;. |

Il `setConsent` comando deve essere utilizzato come parte di un gancio CMP che rileva le modifiche nelle impostazioni del consenso. Il seguente codice JavaScript fornisce un esempio di come il `setConsent` comando può essere utilizzato per il `OnConsentChanged` gancio di OneTrust:

```js
OneTrust.OnConsentChanged(function () {
  // Retrieve the TCF 2.0 consent data generated by the CMP, and pass it to Alloy. 
  __tcfapi("getTCData", 2, (data, success) => {
    if (success) {
      const { tcString, gdprApplies } = data;

      alloy("setConsent", {
        consent: [{
          standard: "IAB TCF",
          version: "2.0",
          value: tcString,
          gdprApplies
        }]
      });
    }
  });
});
```

#### Utilizzo degli eventi

È inoltre possibile raccogliere i dati di consenso TCF 2.0 su ogni evento attivato [!DNL Platform] utilizzando il `sendEvent` comando.

>[!NOTE]
>
>Per utilizzare questo metodo, è necessario aver aggiunto l&#39; [!DNL Experience Event Privacy mixin] allo [!DNL Profile]schema [!DNL XDM ExperienceEvent] abilitato. Consulta la sezione sull’ [aggiornamento dello schema](./dataset-preparation.md#event-schema) ExperienceEvent nella guida alla preparazione dei set di dati per i passaggi relativi alla configurazione di questo evento.

Il `sendEvent` comando deve essere utilizzato come callback nei listener di eventi appropriati sul sito Web. Il comando prevede due argomenti: (1) una stringa che indica il tipo di comando (in questo caso, &quot;sendEvent&quot;) e (2) un payload contenente un `xdm` oggetto che fornisce i campi di consenso richiesti come JSON:

```js
alloy("sendEvent", {
  xdm: {
    "consentStrings": [{
      "consentStandard": "IAB TCF",
      "consentStandardVersion": "2.0",
      "consentStringValue": "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
      "gdprApplies": true
    }]
  }
});
```

| Payload, proprietà | Descrizione |
| --- | --- |
| `xdm.consentStrings` | Un array che deve contenere almeno un oggetto che fornisce i campi di consenso richiesti. |
| `consentStandard` | Standard di consenso utilizzato. Questo valore deve essere impostato su &quot;IAB&quot; per l&#39;elaborazione del consenso TCF 2.0. |
| `consentStandardVersion` | Numero di versione dello standard di consenso indicato in `standard`. Questo valore deve essere impostato su &quot;2.0&quot; per l&#39;elaborazione del consenso TCF 2.0. |
| `consentStringValue` | Stringa di consenso con codifica base 64 generata dal CMP. |
| `gdprApplies` | Un valore booleano che indica se il GDPR si applica al cliente attualmente connesso. Affinché TCF 2.0 sia applicato a questo cliente, il valore deve essere impostato su &quot;true&quot;. |

### Gestione delle risposte SDK

Tutti [!DNL Platform SDK] i comandi restituiscono le promesse che indicano se la chiamata è riuscita o meno. Potete quindi utilizzare queste risposte per logica aggiuntiva, ad esempio per visualizzare messaggi di conferma al cliente. Per esempi specifici, consulta la sezione sulla [gestione di operazioni riuscite o non riuscite](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) nella guida all’esecuzione di comandi SDK.

## Esportare segmenti {#export}

>[!NOTE]
>
>Prima di iniziare ad esportare i segmenti, devi accertarti che i tuoi segmenti includano tutti i campi di consenso richiesti. Per ulteriori informazioni, vedere la sezione sulla [configurazione dei criteri](#merge-policies) di unione.

Dopo aver raccolto i dati di consenso dei clienti e aver creato segmenti di pubblico contenenti gli attributi di consenso richiesti, puoi applicare la conformità TCF 2.0 al momento dell’esportazione di tali segmenti nelle destinazioni a valle.

A condizione che l&#39;impostazione del consenso `gdprApplies` sia impostata su `true` per un insieme di profili cliente, tutti i dati provenienti da tali profili esportati verso destinazioni a valle vengono filtrati in base alle preferenze del consenso per ciascun profilo. I profili che non soddisfano le preferenze di consenso richieste vengono ignorati durante il processo di esportazione.

I clienti devono acconsentire ai seguenti scopi (come indicato nelle politiche [](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)TCF 2.0) per includere i loro profili nei segmenti esportati verso le destinazioni:

* **Finalità 1**: Archiviare e/o accedere alle informazioni su un dispositivo
* **Finalità 10**: Sviluppare e migliorare i prodotti

TCF 2.0 richiede inoltre che l&#39;origine dei dati verifichi l&#39;autorizzazione del fornitore della destinazione prima di inviare i dati a tale destinazione. In questo modo, [!DNL Real-time CDP] verifica se l&#39;autorizzazione fornitore della destinazione viene scelta per tutti gli ID nel cluster prima di includere i dati associati a tale destinazione.

>[!NOTE]
>
>I segmenti condivisi con Adobe Audience Manager conterranno gli stessi valori di consenso di TCF 2.0 delle [!DNL Platform] controparti. Poiché [!DNL Audience Manager] condivide lo stesso ID fornitore di [!DNL Real-time CDP] (565), sono necessari gli stessi scopi e le stesse autorizzazioni del fornitore. Per ulteriori informazioni, consulta il documento sul plug-in [Adobe Audience Manager per IAB TCF](https://docs.adobe.com/help/it-IT/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) .

## Test your implementation {#test-implementation}

Dopo aver configurato l’implementazione TCF 2.0 e aver esportato segmenti nelle destinazioni, i dati che non soddisfano i requisiti di consenso non verranno esportati. Tuttavia, per verificare se i profili cliente corretti sono stati filtrati durante l&#39;esportazione, è necessario controllare manualmente i data store nelle destinazioni per verificare se il consenso è stato applicato correttamente.

È importante notare che se più ID costituiscono un cluster e si applica TCF 2.0, l&#39;intero cluster sarà escluso se anche un singolo ID non contiene le finalità e le autorizzazioni del fornitore corrette.

## Passaggi successivi

Questo documento ha trattato il processo di configurazione delle operazioni di dati [!DNL Real-time CDP] per essere conforme a TCF 2.0. Per ulteriori informazioni sulle altre funzionalità della privacy fornite da [!DNL Real-time CDP], consulta la seguente documentazione:

* [Privacy in CDP in tempo reale](../privacy-overview.md)
* [Governance dei dati in CDP in tempo reale](../data-governance-overview.md)