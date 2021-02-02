---
keywords: Experience Platform ;home;IAB;IAB 2.0;consenso;consenso
solution: Experience Platform
title: 'Supporto IAB TCF 2.0 nel Experience Platform '
topic: privacy events
description: Scopri come configurare le operazioni e gli schemi di dati per trasmettere le scelte di consenso degli utenti quando si attivano segmenti per destinazioni in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: b2d3e4608dc0640472966edccd3fb5a612d7583c
workflow-type: tm+mt
source-wordcount: '2447'
ht-degree: 0%

---


# Supporto IAB TCF 2.0 nel Experience Platform 

Il [!DNL Transparency & Consent Framework] (TCF), come indicato dall&#39; [!DNL Interactive Advertising Bureau] (IAB), è un quadro tecnico aperto destinato a consentire alle organizzazioni di ottenere, registrare e aggiornare il consenso dei consumatori per il trattamento dei loro dati personali, in conformità al [!DNL General Data Protection Regulation] (GDPR) dell&#39;Unione europea. La seconda iterazione del quadro, TCF 2.0, offre maggiore flessibilità per quanto riguarda il modo in cui i consumatori possono fornire o rifiutare il consenso, incluso se e come i venditori possono utilizzare determinate caratteristiche dell&#39;elaborazione dei dati, come una precisa geolocalizzazione.

>[!NOTE]
>
>Ulteriori informazioni su TCF 2.0 sono disponibili sul sito Web [IAB Europe](https://iabeurope.eu/tcf-2-0/), compresi materiali di supporto e specifiche tecniche.

Adobe Experience Platform fa parte dell&#39;elenco di fornitori [IAB TCF 2.0 registrato](https://iabeurope.eu/vendor-list-tcf-v2-0/), all&#39;interno dell&#39;ID **565**. In conformità ai requisiti di TCF 2.0, la piattaforma consente di raccogliere i dati di consenso dei clienti e integrarli nei profili dei clienti memorizzati. Questi dati di consenso possono quindi essere presi in considerazione per stabilire se i profili sono inclusi nei segmenti di pubblico esportati, a seconda del loro caso di utilizzo.

>[!IMPORTANT]
>
>La piattaforma è in grado di soddisfare solo la versione 2.0 del TCF (o successiva). Le versioni precedenti di TCF non sono supportate.

Questo documento fornisce una panoramica su come configurare le operazioni sui dati e gli schemi di profilo per accettare i dati di consenso dei clienti generati dal CMP e su come Piattaforma trasmette le scelte di consenso degli utenti durante l&#39;esportazione dei segmenti.

## Prerequisiti

Per seguire questa guida, è necessario utilizzare una piattaforma di gestione del consenso (CMP), commerciale o propria, integrata e conforme allo IAB TCF. Per ulteriori informazioni, vedere l&#39; [elenco di CMP ](https://iabeurope.eu/cmp-list/) conformi.

>[!IMPORTANT]
>
>Se l’ID del CMP non è valido, la piattaforma continuerà a elaborare i dati così come sono. Per applicare TCF 2.0, è necessario verificare che il CMP disponga di un ID valido registrato con IAB TCF 2.0 prima di inviare i dati a Platform.

Questa guida richiede anche una buona conoscenza dei seguenti servizi della piattaforma:

* [Experience Data Model (XDM)](../../../../xdm/home.md): Il framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
* [Servizio](../../../../identity-service/home.md) identità Adobe Experience Platform: Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati relativi all&#39;esperienza dei clienti attraverso il collegamento di identità tra dispositivi e sistemi.
* [Profilo](../../../../profile/home.md) cliente in tempo reale: Consente  [!DNL Identity Service] di creare profili cliente dettagliati in tempo reale dai set di dati. [!DNL Real-time Customer Profile] estrae i dati dal Data Lake e persiste nei profili dei clienti nel proprio archivio dati separato.
* [Adobe Experience Platform Web SDK](../../../../edge/home.md): Libreria JavaScript lato client che consente di integrare vari servizi della piattaforma nel sito Web rivolto ai clienti.
   * [Comandi](../../../../edge/consent/supporting-consent.md) di consenso SDK: Una panoramica del caso d’uso dei comandi SDK relativi al consenso visualizzati in questa guida.
* [Servizio](../../../../segmentation/home.md) di segmentazione Adobe Experience Platform: Consente di suddividere  [!DNL Real-time Customer Profile] i dati in gruppi di individui che condividono caratteristiche simili e risponderanno in modo simile alle strategie di marketing.

Oltre ai servizi della piattaforma elencati sopra, è necessario avere familiarità con [le destinazioni](../../../../data-governance/home.md) e il loro ruolo nell&#39;ecosistema della piattaforma.

## Riepilogo flusso di consenso cliente {#summary}

Le sezioni seguenti descrivono il modo in cui i dati del consenso vengono raccolti e applicati dopo che il sistema è stato configurato correttamente.

### Raccolta dei dati di consenso

La piattaforma consente di raccogliere i dati sul consenso dei clienti attraverso la procedura seguente:

1. Un cliente fornisce le proprie preferenze di consenso per la raccolta dei dati tramite una finestra di dialogo sul sito Web.
1. Il CMP rileva la modifica delle preferenze di consenso e genera di conseguenza i dati di consenso TCF.
1. Con l’SDK per piattaforma Web, i dati di consenso generati (restituiti dal CMP) vengono inviati ad Adobe Experience Platform.
1. I dati di consenso raccolti vengono trasferiti in un dataset abilitato [!DNL Profile] il cui schema contiene campi di consenso TCF.

Oltre ai comandi SDK attivati dai ganci di modifica del consenso CMP, i dati di consenso possono fluire  Experience Platform attraverso qualsiasi dato XDM generato dal cliente che viene caricato direttamente in un set di dati [!DNL Profile] abilitato.

Tutti i segmenti condivisi con Platform da Adobe Audience Manager (tramite il [!DNL Audience Manager] connettore di origine o in altro modo) possono anche contenere dati di consenso, a condizione che i campi appropriati siano stati applicati a tali segmenti attraverso [!DNL Experience Cloud Identity Service]. Per ulteriori informazioni sulla raccolta dei dati di consenso in [!DNL Audience Manager], consultare il documento sul [plug-in Adobe Audience Manager per IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### Esecuzione del consenso a valle

Una volta che i dati di autorizzazione TCF sono stati correttamente assimilati, i seguenti processi si svolgono nei servizi della piattaforma a valle:

1. [!DNL Real-time Customer Profile] aggiorna i dati del consenso memorizzati per il profilo del cliente.
1. Platform elabora gli ID cliente solo se l&#39;autorizzazione fornitore per Platform (565) è fornita per ogni ID in un cluster.
1. Quando si esportano segmenti in destinazioni appartenenti a membri dell&#39;elenco dei fornitori di TCF 2.0, la piattaforma include profili solo se le autorizzazioni del fornitore per entrambe le piattaforme (565) *e* vengono fornite per ogni ID in un cluster.

Le altre sezioni di questo documento forniscono indicazioni su come configurare la piattaforma e le operazioni sui dati per soddisfare i requisiti di raccolta e applicazione descritti in precedenza.

## Come generare i dati di consenso dei clienti all&#39;interno del CMP {#consent-data}

Poiché ogni sistema CMP è univoco, è necessario determinare il modo migliore per consentire ai clienti di fornire il consenso durante l&#39;interazione con il servizio. Un modo comune per ottenere questo risultato è tramite l&#39;utilizzo di una finestra di dialogo di consenso dei cookie, simile al seguente esempio:

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

Questa finestra di dialogo deve consentire al cliente di:

| Opzione Consenso | Descrizione |
| --- | --- |
| **Finalità** | Gli scopi definiscono a quali scopi di tecnologia dell&#39;annuncio un marchio può utilizzare i dati di un cliente. Affinché Platform possa elaborare gli ID cliente, è necessario optare per i seguenti scopi: <ul><li>**Finalità 1**: Archiviare e/o accedere alle informazioni su un dispositivo</li><li>**Finalità 10**: Sviluppare e migliorare i prodotti</li></ul> |
| **Autorizzazioni fornitore** | Oltre agli scopi di supporto tecnico, la finestra di dialogo deve anche consentire al cliente di scegliere se utilizzare o meno i propri dati da fornitori specifici, incluso Adobe Experience Platform (565). |

### Stringhe di consenso {#consent-strings}

Indipendentemente dal metodo utilizzato per raccogliere i dati, l&#39;obiettivo è quello di generare un valore stringa basato sulle opzioni di consenso scelte dal cliente, denominate stringa di consenso.

Nella specifica TCF, le stringhe di consenso vengono utilizzate per codificare i dettagli rilevanti sulle impostazioni di consenso di un cliente, in termini di scopi di marketing specifici, come definiti da policy e fornitori. La piattaforma utilizza queste stringhe per memorizzare le impostazioni del consenso per ciascun cliente, pertanto ogni volta che tali impostazioni cambiano è necessario generare una nuova stringa di consenso.

Le stringhe di consenso possono essere create solo da un CMP registrato con lo IAB TCF. Per ulteriori informazioni su come generare le stringhe di consenso utilizzando il CMP specifico, fare riferimento alla [guida per la formattazione delle stringhe di consenso](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) nel repo GitHub IAB TCF.

## Creazione di set di dati con campi di consenso TCF {#datasets}

I dati di consenso dei clienti devono essere inviati a insiemi di dati i cui schemi contengono campi di consenso TCF. Per informazioni su come creare i due set di dati richiesti prima di continuare con questa guida, fare riferimento all&#39;esercitazione [creazione di set di dati per l&#39;acquisizione del consenso TCF 2.0](./dataset.md).

## Aggiornare i criteri di unione [!DNL Profile] per includere i dati di consenso {#merge-policies}

Dopo aver creato un set di dati [!DNL Profile] abilitato per la raccolta dei dati di consenso, è necessario assicurarsi che i criteri di unione siano stati configurati in modo da includere sempre i campi di consenso TCF nei profili cliente. Ciò comporta l&#39;impostazione della precedenza del set di dati in modo che l&#39;insieme di dati del consenso abbia priorità rispetto ad altri set di dati potenzialmente in conflitto.

Per ulteriori informazioni sull&#39;utilizzo dei criteri di unione, fare riferimento alla [guida utente dei criteri di unione](../../../../profile/ui/merge-policies.md). Quando imposti i criteri di unione, devi assicurarti che i tuoi segmenti includano tutti gli attributi di consenso richiesti dal [mixin privacy XDM](./dataset.md#privacy-mixin), come indicato nella guida sulla preparazione dei set di dati.

## Integrare l&#39;SDK Web del Experience Platform  per raccogliere i dati di consenso dei clienti {#sdk}

>[!NOTE]
>
>L’uso dell’SDK Web per Experienci Platform  è necessario per elaborare i dati di consenso direttamente in Adobe Experience Platform. [!DNL Experience Cloud Identity Service] al momento non è supportato.
>
>[!DNL Experience Cloud Identity Service] è ancora supportato per l&#39;elaborazione del consenso in Adobe Audience Manager, tuttavia, e la conformità con TCF 2.0 richiede solo che la libreria venga aggiornata alla  [versione 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Una volta configurato il CMP per generare le stringhe di consenso, è necessario integrare l’SDK Web del Experience Platform  per raccogliere tali stringhe e inviarle alla piattaforma. L’SDK della piattaforma fornisce due comandi che possono essere utilizzati per inviare i dati di consenso TCF a Platform (descritti nelle sottosezioni seguenti) e che devono essere utilizzati quando un cliente fornisce le informazioni di consenso per la prima volta, e in qualsiasi momento in cui il consenso viene modificato in seguito.

**L’SDK non interagisce con CMP**. Sta a voi determinare come integrare l’SDK nel vostro sito Web, ascoltare le modifiche del consenso nel CMP e chiamare il comando appropriato.

### Creare una nuova configurazione Edge

Affinché l&#39;SDK invii dati a  Experience Platform, devi prima creare una nuova configurazione edge per Platform in [!DNL Adobe Experience Platform Launch]. I passaggi specifici per la creazione di una nuova configurazione sono disponibili nella [documentazione SDK](../../../../edge/fundamentals/edge-configuration.md).

Dopo aver fornito un nome univoco per la configurazione, fate clic sul pulsante di attivazione accanto a **[!UICONTROL Adobe Experience Platform]**. Quindi, utilizzare i seguenti valori per completare il resto del modulo:

| Campo di configurazione Edge | Valore |
| --- | --- |
| [!UICONTROL Sandbox] | Il nome della piattaforma [sandbox](../../../../sandboxes/home.md) che contiene la connessione di streaming e i set di dati richiesti per impostare la configurazione del edge. |
| [!UICONTROL Streaming Inlet] | Una connessione di streaming valida per  Experience Platform. Se non disponete di un&#39;entrata in streaming, vedete l&#39;esercitazione su [creazione di una connessione in streaming](../../../../ingestion/tutorials/create-streaming-connection-ui.md). |
| [!UICONTROL Event Dataset] | Selezionare il set di dati [!DNL XDM ExperienceEvent] creato nel [passaggio precedente](#datasets). |
| [!UICONTROL Profile Dataset] | Selezionare il set di dati [!DNL XDM Individual Profile] creato nel [passaggio precedente](#datasets). |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Al termine, selezionate **[!UICONTROL Save]** nella parte inferiore dello schermo e continuate a seguire eventuali altri prompt per completare la configurazione.

### Esecuzione di comandi di modifica del consenso

Dopo aver creato la configurazione edge descritta nella sezione precedente, puoi iniziare a utilizzare i comandi SDK per inviare i dati di consenso a Piattaforma. Le sezioni seguenti forniscono esempi di come ciascun comando SDK può essere utilizzato in scenari diversi.

>[!NOTE]
>
>Per un&#39;introduzione alla sintassi comune per tutti i comandi SDK della piattaforma, vedete il documento in [esecuzione di comandi](../../../../edge/fundamentals/executing-commands.md).

#### Utilizzo dei ganci di consenso CMP

Molti CMP forniscono ganci out-of-the-box che ascoltano gli eventi di consenso-cambiamento. Quando si verificano tali eventi, è possibile utilizzare il comando `setConsent` per aggiornare i dati di consenso del cliente.

Il comando `setConsent` prevede due argomenti: (1) una stringa che indica il tipo di comando (in questo caso, &quot;setConsent&quot;) e (2) un payload che contiene una matrice `consent`, che deve contenere almeno un oggetto che fornisce i campi di consenso richiesti, come mostrato di seguito:

```js
alloy("setConsent", {
  consent: [{
    standard: "IAB TCF",
    version: "2.0",
    value: "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
    gdprApplies: "true"
  }]
});
```

| Payload, proprietà | Descrizione |
| --- | --- |
| `standard` | Standard di consenso utilizzato. Questo valore deve essere impostato su `IAB` per l&#39;elaborazione del consenso TCF 2.0. |
| `version` | Il numero di versione dello standard di consenso indicato in `standard`. Questo valore deve essere impostato su `2.0` per l&#39;elaborazione del consenso TCF 2.0. |
| `value` | Stringa di consenso con codifica base 64 generata dal CMP. |
| `gdprApplies` | Un valore booleano che indica se il GDPR si applica al cliente attualmente connesso. Affinché TCF 2.0 sia applicato a questo cliente, il valore deve essere impostato su `true`. |

Il comando `setConsent` deve essere utilizzato come parte di un gancio CMP che rileva le modifiche nelle impostazioni del consenso. Il seguente codice JavaScript fornisce un esempio di come il comando `setConsent` può essere utilizzato per il gancio di OneTrust `OnConsentChanged`:

```js
OneTrust.OnConsentChanged(function () {
  // Retrieve the TCF 2.0 consent data generated by the CMP, and pass it to Alloy. 
  __tcfapi("getTCData", 2, function (data, success) {
    if (success) {
      var tcString = data.tcString;
      var gdpr = data.gdprApplies;

      alloy("setConsent", {
        consent: [{
          standard: "IAB TCF",
          version: "2.0",
          value: tcString,
          gdprApplies: gdpr
        }]
      });
    }
  });
});
```

#### Utilizzo degli eventi

È inoltre possibile raccogliere i dati di consenso di TCF 2.0 su ogni evento attivato in Piattaforma utilizzando il comando `sendEvent`.

>[!NOTE]
>
>Per utilizzare questo metodo, è necessario aver aggiunto [!DNL Experience Event Privacy mixin] allo schema [!DNL Profile] abilitato [!DNL XDM ExperienceEvent]. Per informazioni su come configurare questa funzione, vedere la sezione relativa all&#39; [aggiornamento dello schema ExperienceEvent](./dataset.md#event-schema) nella guida alla preparazione dei set di dati.

Il comando `sendEvent` deve essere utilizzato come callback nei listener di eventi appropriati sul sito Web. Il comando prevede due argomenti: (1) una stringa che indica il tipo di comando (in questo caso, `sendEvent`) e (2) un payload contenente un oggetto `xdm` che fornisce i campi di consenso richiesti come JSON:

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
| `consentStandard` | Standard di consenso utilizzato. Questo valore deve essere impostato su `IAB` per l&#39;elaborazione del consenso TCF 2.0. |
| `consentStandardVersion` | Il numero di versione dello standard di consenso indicato in `standard`. Questo valore deve essere impostato su `2.0` per l&#39;elaborazione del consenso TCF 2.0. |
| `consentStringValue` | Stringa di consenso con codifica base 64 generata dal CMP. |
| `gdprApplies` | Un valore booleano che indica se il GDPR si applica al cliente attualmente connesso. Affinché TCF 2.0 sia applicato a questo cliente, il valore deve essere impostato su `true`. |

### Gestione delle risposte SDK

Tutti i comandi [!DNL Platform SDK] restituiscono promesse che indicano se la chiamata è riuscita o meno. Potete quindi utilizzare queste risposte per logica aggiuntiva, ad esempio per visualizzare messaggi di conferma al cliente. Per esempi specifici, consulta la sezione relativa alla gestione di operazioni riuscite o non riuscite ](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) nella guida sull&#39;esecuzione dei comandi SDK.[

## Esportare segmenti {#export}

>[!NOTE]
>
>Prima di iniziare ad esportare i segmenti, devi accertarti che i tuoi segmenti includano tutti i campi di consenso richiesti. Per ulteriori informazioni, vedere la sezione relativa alla [configurazione dei criteri di unione](#merge-policies).

Dopo aver raccolto i dati di consenso dei clienti e aver creato segmenti di pubblico contenenti gli attributi di consenso richiesti, puoi applicare la conformità TCF 2.0 al momento dell’esportazione di tali segmenti nelle destinazioni a valle.

A condizione che l&#39;impostazione di consenso `gdprApplies` sia impostata su `true` per un insieme di profili cliente, tutti i dati provenienti da tali profili esportati verso destinazioni a valle vengono filtrati in base alle preferenze di consenso per ciascun profilo. I profili che non soddisfano le preferenze di consenso richieste vengono ignorati durante il processo di esportazione.

I clienti devono acconsentire ai seguenti scopi (come indicato da [TCF 2.0 Policies](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) per includere i loro profili nei segmenti esportati verso le destinazioni:

* **Finalità 1**: Archiviare e/o accedere alle informazioni su un dispositivo
* **Finalità 10**: Sviluppare e migliorare i prodotti

TCF 2.0 richiede inoltre che l&#39;origine dei dati verifichi l&#39;autorizzazione del fornitore della destinazione prima di inviare i dati a tale destinazione. Di conseguenza, Platform verifica se l&#39;autorizzazione fornitore della destinazione viene scelta per tutti gli ID nel cluster prima di includere i dati associati a tale destinazione.

>[!NOTE]
>
>Tutti i segmenti condivisi con Adobe Audience Manager conterranno gli stessi valori di consenso di TCF 2.0 delle controparti della piattaforma. Poiché [!DNL Audience Manager] condivide lo stesso ID fornitore della piattaforma (565), sono necessari gli stessi scopi e le stesse autorizzazioni del fornitore. Per ulteriori informazioni, consultare il documento sul [plug-in Adobe Audience Manager per IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

## Verificare l&#39;implementazione {#test-implementation}

Dopo aver configurato l’implementazione TCF 2.0 e aver esportato segmenti nelle destinazioni, i dati che non soddisfano i requisiti di consenso non verranno esportati. Tuttavia, per verificare se i profili cliente corretti sono stati filtrati durante l&#39;esportazione, è necessario controllare manualmente i data store nelle destinazioni per verificare se il consenso è stato applicato correttamente.

È importante notare che se più ID costituiscono un cluster e si applica TCF 2.0, l&#39;intero cluster sarà escluso se anche un singolo ID non contiene le finalità e le autorizzazioni del fornitore corrette.

## Passaggi successivi

In questo documento è stato illustrato il processo di configurazione delle operazioni sui dati della piattaforma per soddisfare gli obblighi aziendali, come indicato da TCF 2.0. Per ulteriori informazioni, consulta la panoramica su [governance, privacy e sicurezza](../../overview.md) della piattaforma per la privacy.