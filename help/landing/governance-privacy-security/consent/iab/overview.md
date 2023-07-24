---
keywords: Experience Platform;home;IAB;IAB 2.0;consenso;Consenso;Consenso
solution: Experience Platform
title: Supporto IAB TCF 2.0 in Experience Platform
description: Scopri come configurare le operazioni sui dati e gli schemi per trasmettere le scelte di consenso dei clienti quando si attivano i segmenti nelle destinazioni in Adobe Experience Platform.
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 1%

---

# Supporto IAB TCF 2.0 in Experience Platform

Il [!DNL Transparency & Consent Framework] (TCF), come indicato dalla [!DNL Interactive Advertising Bureau] (IAB), è un quadro tecnico basato su standard aperti destinato a consentire alle organizzazioni di ottenere, registrare e aggiornare il consenso dei consumatori per il trattamento dei loro dati personali, in conformità con il [!DNL General Data Protection Regulation] (RGPD). La seconda iterazione del framework, TCF 2.0, offre maggiore flessibilità su come i consumatori possono fornire o negare il consenso, compreso se e come i fornitori possono utilizzare determinate caratteristiche del trattamento dei dati, come una precisa geolocalizzazione.

>[!NOTE]
>
>Ulteriori informazioni su TCF 2.0 sono disponibili sul sito [Sito web di IAB Europe](https://iabeurope.eu/tcf-2-0/), compresi i materiali di supporto e le specifiche tecniche.

Adobe Experience Platform fa parte del [Elenco fornitori IAB TCF 2.0](https://iabeurope.eu/vendor-list-tcf-v2-0/), sotto l&#39;ID **565**. In conformità ai requisiti TCF 2.0, Platform consente di raccogliere i dati sul consenso dei clienti e di integrarli nei profili dei clienti memorizzati. Questi dati sul consenso possono quindi essere presi in considerazione per stabilire se i profili sono inclusi nei segmenti di pubblico esportati, a seconda del loro caso d’uso.

>[!IMPORTANT]
>
>Platform è in grado di rispettare solo la versione 2.0 del TCF (o successiva). Le versioni precedenti di TCF non sono supportate.

Questo documento fornisce una panoramica su come configurare le operazioni sui dati e gli schemi di profilo per accettare i dati di consenso del cliente generati dalla CMP e su come Platform trasmette le scelte di consenso degli utenti durante l’esportazione di segmenti.

## Prerequisiti

Per seguire questa guida, devi utilizzare una piattaforma di gestione del consenso (CMP), commerciale o tua, integrata e conforme a IAB TCF. Consulta la [elenco di CMP conformi](https://iabeurope.eu/cmp-list/) per ulteriori informazioni.

>[!IMPORTANT]
>
>Se l’ID della tua CMP non è valido, Platform continuerà a elaborare i tuoi dati così come sono. Per applicare il TCF 2.0, è necessario confermare che la CMP dispone di un ID valido registrato con IAB TCF 2.0 prima di inviare i dati a Platform.

Questa guida richiede anche una buona conoscenza dei seguenti servizi di Platform:

* [Experience Data Model (XDM)](../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull’esperienza del cliente.
* [Servizio Adobe Experience Platform Identity](../../../../identity-service/home.md): risolve la sfida fondamentale posta dalla frammentazione dei dati sull’esperienza del cliente, collegando le identità tra dispositivi e sistemi.
* [Profilo cliente in tempo reale](../../../../profile/home.md): utilizza [!DNL Identity Service] per creare in tempo reale profili cliente dettagliati dai set di dati. [!DNL Real-Time Customer Profile] estrae dati dal Data Lake e mantiene i profili dei clienti nel proprio archivio dati separato.
* [Adobe Experience Platform Web SDK](../../../../edge/home.md): libreria JavaScript lato client che consente di integrare vari servizi Platform nel sito web rivolto al cliente.
   * [Comandi di consenso SDK](../../../../edge/consent/supporting-consent.md): panoramica del caso d’uso dei comandi SDK relativi al consenso mostrati in questa guida.
* [Servizio di segmentazione di Adobe Experience Platform](../../../../segmentation/home.md): consente di dividere [!DNL Real-Time Customer Profile] dati in gruppi di individui che condividono caratteristiche simili e risponderanno in modo simile alle strategie di marketing.

Oltre ai servizi di Platform elencati sopra, dovresti avere familiarità con [destinazioni](../../../../data-governance/home.md) e il loro ruolo nell&#39;ecosistema della piattaforma.

## Riepilogo del flusso di consenso del cliente {#summary}

Le sezioni seguenti descrivono come i dati sul consenso vengono raccolti e applicati dopo che il sistema è stato configurato correttamente.

### Raccolta dati di consenso

Platform consente di raccogliere i dati sul consenso del cliente tramite il seguente processo:

1. Un cliente fornisce le proprie preferenze di consenso per la raccolta dei dati tramite una finestra di dialogo sul sito web.
1. La tua CMP rileva la modifica della preferenza di consenso e genera di conseguenza i dati sul consenso TCF.
1. Utilizzando Platform Web SDK, i dati del consenso generati (restituiti dalla CMP) vengono inviati a Adobe Experience Platform.
1. I dati sul consenso raccolti vengono acquisiti in una [!DNL Profile]Set di dati abilitato con schema contenente campi di consenso TCF.

Oltre ai comandi SDK attivati dagli hook di modifica del consenso CMP, i dati del consenso possono anche fluire in Experience Platform tramite qualsiasi dato XDM generato dal cliente e caricato direttamente in un [!DNL Profile]Set di dati abilitato da.

Qualsiasi segmento condiviso con Platform da Adobe Audience Manager (tramite [!DNL Audience Manager] (connettore di origine o altro) possono contenere anche dati sul consenso, purché i campi appropriati siano stati applicati a tali segmenti tramite [!DNL Experience Cloud Identity Service]. Per ulteriori informazioni sulla raccolta dei dati sul consenso in [!DNL Audience Manager], consulta il documento sulla [Plug-in Adobe Audience Manager per IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=it).

### Applicazione del consenso a valle

Una volta acquisiti correttamente i dati di consenso TCF, i seguenti processi hanno luogo nei servizi Platform a valle:

1. [!DNL Real-Time Customer Profile] aggiorna i dati di consenso memorizzati per il profilo di quel cliente.
1. Platform elabora gli ID cliente solo se per ogni ID in un cluster viene fornita l’autorizzazione del fornitore per Platform (565).
1. Durante l’esportazione di segmenti in destinazioni appartenenti a membri dell’elenco di fornitori TCF 2.0, Platform include profili solo se i permessi fornitore per entrambe le piattaforme (565) *e* per ogni ID in un cluster vengono fornite le singole destinazioni.

Le altre sezioni di questo documento forniscono indicazioni su come configurare Platform e le operazioni sui dati per soddisfare i requisiti di raccolta e applicazione descritti in precedenza.

## Determinare come generare i dati sul consenso dei clienti all’interno della CMP {#consent-data}

Poiché ogni sistema CMP è univoco, devi determinare il modo migliore per consentire ai clienti di fornire il consenso durante l’interazione con il servizio. Un modo comune per ottenere questo risultato è tramite l’utilizzo di una finestra di dialogo di consenso dei cookie, simile all’esempio seguente:

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

Questa finestra di dialogo deve consentire al cliente di effettuare o meno il consenso:

| Opzione di consenso | Descrizione |
| --- | --- |
| **Finalità** | Le finalità definiscono per quali finalità di tecnologia pubblicitaria un brand può utilizzare i dati di un cliente. Affinché Platform possa elaborare gli ID cliente, è necessario accettare le seguenti finalità: <ul><li>**Scopo 1**: archivia e/o accede alle informazioni su un dispositivo</li><li>**Finalità 10**: sviluppare e migliorare i prodotti</li></ul> |
| **Autorizzazioni fornitore** | Oltre a scopi di tecnologia per annunci, la finestra di dialogo deve anche consentire al cliente di acconsentire o rinunciare all’utilizzo dei propri dati da parte di fornitori specifici, tra cui Adobe Experience Platform (565). |

### Stringhe di consenso {#consent-strings}

Indipendentemente dal metodo utilizzato per raccogliere i dati, l’obiettivo è generare un valore stringa in base alle opzioni di consenso scelte dal cliente, denominato stringa di consenso.

Nella specifica TCF, le stringhe di consenso vengono utilizzate per codificare dettagli rilevanti sulle impostazioni di consenso di un cliente, in termini di finalità di marketing specifiche, come definite dalle politiche e dai fornitori. Platform utilizza queste stringhe per memorizzare le impostazioni di consenso per ciascun cliente, pertanto ogni volta che tali impostazioni cambiano deve essere generata una nuova stringa di consenso.

Le stringhe di consenso possono essere create solo da una CMP registrata con IAB TCF. Per ulteriori informazioni su come generare stringhe di consenso utilizzando una specifica CMP, consulta [guida alla formattazione della stringa di consenso](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) nell’archivio GitHub IAB TCF.

## Creare set di dati con campi di consenso TCF {#datasets}

I dati sul consenso del cliente devono essere inviati a set di dati i cui schemi contengono campi di consenso TCF. Fai riferimento al tutorial su [creazione di set di dati per l’acquisizione del consenso TCF 2.0](./dataset.md) come creare il set di dati di profilo richiesto (e un set di dati Experience Event facoltativo) prima di continuare con questa guida.

## Aggiorna [!DNL Profile] criteri di unione per includere i dati sul consenso {#merge-policies}

Dopo aver creato un’ [!DNL Profile]: set di dati abilitato per la raccolta dei dati sul consenso, devi assicurarti che i criteri di unione siano stati configurati per includere sempre i campi di consenso TCF nei profili cliente. Ciò comporta l’impostazione della precedenza dei set di dati in modo che il set di dati di consenso abbia priorità rispetto ad altri set di dati potenzialmente in conflitto.

Per ulteriori informazioni su come utilizzare i criteri di unione, consulta [panoramica dei criteri di unione](../../../../profile/merge-policies/overview.md). Quando configuri i criteri di unione, devi assicurarti che i segmenti includano tutti gli attributi di consenso richiesti forniti da [Gruppo di campi dello schema di privacy XDM](./dataset.md#privacy-field-group), come descritto nella guida sulla preparazione dei set di dati.

## Integrare Experience Platform Web SDK per raccogliere i dati sul consenso del cliente {#sdk}

>[!NOTE]
>
>Per elaborare i dati del consenso direttamente in Adobe Experience Platform è necessario utilizzare l’SDK per web di Experience Platform. [!DNL Experience Cloud Identity Service] non è attualmente supportato.
>
>[!DNL Experience Cloud Identity Service] è ancora supportato per l’elaborazione del consenso in Adobe Audience Manager, tuttavia, e la conformità a TCF 2.0 richiede solo che la libreria sia aggiornata a [versione 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Dopo aver configurato la CMP per generare le stringhe di consenso, è necessario integrare l’SDK per web di Experience Platform per raccogliere tali stringhe e inviarle a Platform. Platform SDK fornisce due comandi che possono essere utilizzati per inviare i dati di consenso TCF a Platform (descritti nelle sottosezioni seguenti) e che devono essere utilizzati quando un cliente fornisce informazioni sul consenso per la prima volta e in qualsiasi momento successivo.

**L’SDK non si interfaccia con alcuna CMP predefinita**. Sta a te determinare come integrare l’SDK nel tuo sito web, ascoltare le modifiche del consenso nella CMP e chiamare il comando appropriato.

### Creare un nuovo flusso di dati

Affinché l’SDK possa inviare dati all’Experience Platform, devi prima creare un nuovo flusso di dati per Platform. I passaggi specifici per la creazione di un nuovo flusso di dati sono descritti in [Documentazione SDK](../../../../datastreams/overview.md).

Dopo aver fornito un nome univoco per lo stream di dati, seleziona il pulsante accanto a **[!UICONTROL Adobe Experience Platform]**. Quindi, utilizzare i valori seguenti per completare il resto del modulo:

| Campo stream di dati | Valore |
| --- | --- |
| [!UICONTROL Sandbox] | Nome della piattaforma [sandbox](../../../../sandboxes/home.md) che contiene la connessione in streaming e i set di dati necessari per impostare lo stream di dati. |
| [!UICONTROL Ingresso streaming] | Ad Experience Platform, una connessione in streaming valida. Guarda il tutorial su [creazione di una connessione in streaming](../../../../ingestion/tutorials/create-streaming-connection-ui.md) se non disponi di una presa di streaming esistente. |
| [!UICONTROL Set di dati evento] | Seleziona la [!DNL XDM ExperienceEvent] set di dati creato in [passaggio precedente](#datasets). Se hai incluso il [[!UICONTROL Consenso IAB TCF 2.0] gruppo di campi](../../../../xdm/field-groups/event/iab.md) nello schema di questo set di dati, puoi tenere traccia degli eventi di modifica del consenso nel tempo utilizzando [`sendEvent`](#sendEvent) , archiviando tali dati in questo set di dati. I valori di consenso memorizzati in questo set di dati sono **non** utilizzato nei flussi di lavoro di applicazione automatica. |
| [!UICONTROL Set di dati profilo] | Seleziona la [!DNL XDM Individual Profile] set di dati creato in [passaggio precedente](#datasets). Quando si risponde agli hook di modifica del consenso CMP utilizzando [`setConsent`](#setConsent) , i dati raccolti verranno memorizzati in questo set di dati. Poiché questo set di dati è abilitato per il profilo, i valori del consenso memorizzati in questo set di dati vengono rispettati durante i flussi di lavoro di applicazione automatica. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Al termine, seleziona **[!UICONTROL Salva]** nella parte inferiore della schermata e continuare a seguire eventuali altre richieste per completare la configurazione.

### Esecuzione di comandi per la modifica del consenso

Dopo aver creato lo stream di dati descritto nella sezione precedente, puoi iniziare a utilizzare i comandi SDK per inviare i dati del consenso a Platform. Le sezioni seguenti forniscono esempi di come ogni comando SDK può essere utilizzato in scenari diversi.

>[!NOTE]
>
>Per un’introduzione alla sintassi comune per tutti i comandi dell’SDK di Platform, consulta il documento su [esecuzione di comandi](../../../../edge/fundamentals/executing-commands.md).

#### Utilizzo degli hook per la modifica del consenso di CMP {#setConsent}

Molte CMP forniscono hook pronti all’uso in grado di ascoltare gli eventi di modifica del consenso. Quando si verificano questi eventi, puoi utilizzare `setConsent` per aggiornare i dati di consenso del cliente.

Il `setConsent` Il comando prevede due argomenti: (1) una stringa che indica il tipo di comando (in questo caso, &quot;setConsent&quot;) e (2) un payload che contiene un `consent` array, che deve contenere almeno un oggetto che fornisca i campi di consenso richiesti, come mostrato di seguito:

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
| `standard` | Lo standard di consenso utilizzato. Questo valore deve essere impostato su `IAB` per l’elaborazione del consenso TCF 2.0. |
| `version` | Il numero di versione dello standard di consenso indicato in `standard`. Questo valore deve essere impostato su `2.0` per l’elaborazione del consenso TCF 2.0. |
| `value` | Stringa di consenso con codifica base 64 generata dalla CMP. |
| `gdprApplies` | Valore booleano che indica se il RGPD si applica al cliente attualmente connesso. Affinché TCF 2.0 possa essere applicato a questo cliente, il valore deve essere impostato su `true`. Impostazione predefinita `true` se non è definita. |

Il `setConsent` Questo comando deve essere utilizzato come parte di un hook CMP che rileva le modifiche nelle impostazioni di consenso. Il seguente codice JavaScript fornisce un esempio di come `setConsent` Il comando può essere utilizzato per il `OnConsentChanged` gancio:

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

#### Utilizzo degli eventi {#sendEvent}

Puoi anche raccogliere i dati sul consenso TCF 2.0 su ogni evento attivato in Platform utilizzando `sendEvent` comando.

>[!NOTE]
>
>Per utilizzare questo metodo, devi aver aggiunto il gruppo di campi Privacy evento esperienza al tuo [!DNL Profile]-abilitato [!DNL XDM ExperienceEvent] schema. Consulta la sezione su [aggiornamento dello schema ExperienceEvent](./dataset.md#event-schema) nella guida alla preparazione dei set di dati per i passaggi su come configurarlo.

Il `sendEvent` Il comando deve essere utilizzato come callback nei listener di eventi appropriati sul sito Web. Il comando prevede due argomenti: (1) una stringa che indica il tipo di comando (in questo caso, `sendEvent`) e (2) un payload contenente un `xdm` oggetto che fornisce i campi di consenso richiesti come JSON:

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
| `xdm.consentStrings` | Array che deve contenere almeno un oggetto che fornisca i campi di consenso richiesti. |
| `consentStandard` | Lo standard di consenso utilizzato. Questo valore deve essere impostato su `IAB` per l’elaborazione del consenso TCF 2.0. |
| `consentStandardVersion` | Il numero di versione dello standard di consenso indicato in `standard`. Questo valore deve essere impostato su `2.0` per l’elaborazione del consenso TCF 2.0. |
| `consentStringValue` | Stringa di consenso con codifica base 64 generata dalla CMP. |
| `gdprApplies` | Valore booleano che indica se il RGPD si applica al cliente attualmente connesso. Affinché TCF 2.0 possa essere applicato a questo cliente, il valore deve essere impostato su `true`. Impostazione predefinita `true` se non è definita. |

### Gestione delle risposte SDK

Tutti [!DNL Platform SDK] i comandi restituiscono promesse che indicano se la chiamata è riuscita o meno. Puoi quindi utilizzare queste risposte per una logica aggiuntiva, ad esempio per visualizzare i messaggi di conferma al cliente. Consulta la sezione su [gestione di operazioni riuscite o non riuscite](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) nella guida all’esecuzione dei comandi SDK per esempi specifici.

## Esportare segmenti {#export}

>[!NOTE]
>
>Prima di iniziare l’esportazione dei segmenti, è necessario assicurarsi che i segmenti includano tutti i campi di consenso richiesti. Consulta la sezione su [configurazione dei criteri di unione](#merge-policies) per ulteriori informazioni.

Dopo aver raccolto i dati sul consenso dei clienti e aver creato segmenti di pubblico contenenti gli attributi di consenso richiesti, puoi applicare la conformità TCF 2.0 durante l’esportazione di tali segmenti in destinazioni a valle.

Purché l’impostazione del consenso `gdprApplies` è impostato su `true` per un set di profili cliente, tutti i dati di tali profili esportati verso destinazioni a valle vengono filtrati in base alle preferenze di consenso TCF per ciascun profilo. Qualsiasi profilo che non soddisfi le preferenze di consenso richieste viene saltato durante il processo di esportazione.

I clienti devono acconsentire ai seguenti scopi (come indicato da [Criteri TCF 2.0](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) per includere i loro profili nei segmenti esportati nelle destinazioni:

* **Scopo 1**: archivia e/o accede alle informazioni su un dispositivo
* **Finalità 10**: sviluppare e migliorare i prodotti

TCF 2.0 richiede inoltre che l’origine dei dati verifichi l’autorizzazione del fornitore della destinazione prima di inviare i dati a tale destinazione. Platform controlla quindi se l’autorizzazione del fornitore della destinazione ha acconsentito a tutti gli ID nel cluster prima di includere i dati associati a tale destinazione.

>[!NOTE]
>
>Tutti i segmenti condivisi con Adobe Audience Manager conterranno gli stessi valori di consenso TCF 2.0 delle controparti di Platform. Da [!DNL Audience Manager] condivide lo stesso ID fornitore di Platform (565), sono necessari gli stessi scopi e le stesse autorizzazioni del fornitore. Consulta il documento sulla [Plug-in Adobe Audience Manager per IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=it) per ulteriori informazioni.

## Testare l’implementazione {#test-implementation}

Dopo aver configurato l’implementazione di TCF 2.0 e aver esportato i segmenti nelle destinazioni, tutti i dati che non soddisfano i requisiti di consenso non verranno esportati. Tuttavia, per verificare se i profili cliente corretti sono stati filtrati durante l’esportazione, devi controllare manualmente gli archivi di dati sulle destinazioni per verificare se il consenso è stato applicato correttamente.

È importante notare che se più ID compongono un cluster e viene applicato TCF 2.0, l’intero cluster verrà escluso se anche un singolo ID non contiene le finalità e le autorizzazioni del fornitore corrette.

## Passaggi successivi

In questo documento viene descritto il processo di configurazione delle operazioni relative ai dati di Platform per soddisfare gli obblighi aziendali descritti dal TCF 2.0. Consulta la panoramica su [governance, privacy e sicurezza](../../overview.md) per ulteriori informazioni sulle funzionalità relative alla privacy di Platform.
