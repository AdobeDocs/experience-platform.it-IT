---
keywords: Experience Platform;home;IAB;IAB 2.0;consenso;Consenso;Consenso
solution: Experience Platform
title: Supporto IAB TCF 2.0 in Experience Platform
description: Scopri come configurare le operazioni sui dati e gli schemi per trasmettere le scelte di consenso dei clienti quando si attivano i segmenti nelle destinazioni in Adobe Experience Platform.
role: Developer
feature: Consent
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '2492'
ht-degree: 0%

---

# Supporto IAB TCF 2.0 in Experience Platform

Il [!DNL Transparency & Consent Framework] (TCF), come descritto da [!DNL Interactive Advertising Bureau] (IAB) è un framework tecnico basato su standard aperti che consente alle organizzazioni di ottenere, registrare e aggiornare il consenso del consumatore per il trattamento dei propri dati personali, in conformità con il [!DNL General Data Protection Regulation] (RGPD) dell&#39;Unione Europea. La seconda iterazione del framework, TCF 2.0, offre maggiore flessibilità su come i consumatori possono fornire o negare il consenso, compreso se e come i fornitori possono utilizzare determinate caratteristiche del trattamento dei dati, come una precisa geolocalizzazione.

>[!NOTE]
>
>Ulteriori informazioni su TCF 2.0 sono disponibili sul sito Web [IAB Europe](https://iabeurope.eu/), inclusi i materiali di supporto e le specifiche tecniche.

Adobe Experience Platform fa parte dell&#39;elenco fornitori [IAB TCF 2.0 registrato](https://iabeurope.eu/vendor-list-tcf/), con ID **565**. In conformità ai requisiti TCF 2.0, Platform consente di raccogliere i dati sul consenso dei clienti e di integrarli nei profili dei clienti memorizzati. Questi dati sul consenso possono quindi essere presi in considerazione per stabilire se i profili sono inclusi nei segmenti di pubblico esportati, a seconda del loro caso d’uso.

>[!IMPORTANT]
>
>Platform è in grado di rispettare solo la versione 2.0 del TCF (o successiva). Le versioni precedenti di TCF non sono supportate.

Questo documento fornisce una panoramica su come configurare le operazioni sui dati e gli schemi di profilo per accettare i dati sul consenso dei clienti generati dalla piattaforma di gestione dei consensi (CMP, Consent Management Platform). Inoltre, illustra come Platform trasmette le scelte di consenso degli utenti durante l’esportazione di segmenti.

## Prerequisiti

Per seguire insieme a questa guida, devi utilizzare una CMP, commerciale o tua, integrata e conforme con IAB TCF. Per ulteriori informazioni, vedere l&#39;[elenco di CMP conformi](https://iabeurope.eu/cmp-list/).

>[!IMPORTANT]
>
>Se l’ID della CMP non è valido, Platform continua a elaborare i dati così come sono. Per applicare il TCF 2.0, prima di inviare i dati a Platform è necessario confermare che la CMP dispone di un ID valido registrato con il TCF IAB 2.0.

Questa guida richiede anche una buona conoscenza dei seguenti servizi di Platform:

* [Experience Data Model (XDM)](/help/xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
* [Servizio Adobe Experience Platform Identity](/help/identity-service/home.md): risolve il problema fondamentale della frammentazione dei dati sull&#39;esperienza del cliente, collegando le identità tra dispositivi e sistemi.
* [Profilo cliente in tempo reale](/help/profile/home.md): utilizza [!DNL Identity Service] per creare profili cliente dettagliati dai set di dati in tempo reale. [!DNL Real-Time Customer Profile] estrae dati dal Data Lake e mantiene i profili cliente nel proprio archivio dati separato.
* [Adobe Experience Platform Web SDK](/help/web-sdk/home.md): libreria JavaScript lato client che consente di integrare vari servizi Platform nel sito Web rivolto al cliente.
   * [Comandi di consenso SDK](../../../../web-sdk/commands/setconsent.md): panoramica del caso d&#39;uso dei comandi SDK relativi al consenso mostrata in questa guida.
* [Servizio di segmentazione di Adobe Experience Platform](/help/segmentation/home.md): consente di dividere i dati di [!DNL Real-Time Customer Profile] in gruppi di individui che condividono caratteristiche simili e rispondono in modo simile alle strategie di marketing.

Oltre ai servizi di Platform elencati in precedenza, dovresti avere familiarità con [destinazioni](/help/data-governance/home.md) e con il loro ruolo nell&#39;ecosistema di Platform.

## Riepilogo del flusso di consenso del cliente {#summary}

Le sezioni seguenti descrivono come i dati sul consenso vengono raccolti e applicati dopo che il sistema è stato configurato correttamente.

### Raccolta dati di consenso

Platform consente di raccogliere i dati sul consenso del cliente tramite il seguente processo:

1. Un cliente fornisce le proprie preferenze di consenso per la raccolta dei dati tramite una finestra di dialogo sul sito web.
1. La tua CMP rileva la modifica della preferenza di consenso e genera di conseguenza i dati sul consenso TCF.
1. Utilizzando Platform Web SDK, i dati del consenso generati (restituiti dalla CMP) vengono inviati a Adobe Experience Platform.
1. I dati di consenso raccolti vengono acquisiti in un set di dati abilitato per [!DNL Profile] il cui schema contiene campi di consenso TCF.

Oltre ai comandi SDK attivati dagli hook di modifica del consenso di CMP, i dati del consenso possono anche fluire in Experience Platform tramite qualsiasi dato XDM generato dal cliente e caricato direttamente in un set di dati abilitato per [!DNL Profile].

Tutti i segmenti condivisi con Platform da Adobe Audience Manager (tramite il connettore di origine [!DNL Audience Manager] o altro) possono contenere anche dati sul consenso se i campi appropriati sono stati applicati a tali segmenti tramite [!DNL Experience Cloud Identity Service]. Per ulteriori informazioni sulla raccolta dei dati sul consenso in [!DNL Audience Manager], consulta il documento sul plug-in [Adobe Audience Manager per IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=it).

### Applicazione del consenso a valle

Una volta acquisiti correttamente i dati di consenso TCF, i seguenti processi hanno luogo nei servizi Platform a valle:

1. [!DNL Real-Time Customer Profile] aggiorna i dati di consenso archiviati per il profilo del cliente.
1. Platform elabora gli ID cliente solo se per ogni ID in un cluster viene fornita l’autorizzazione del fornitore per Platform (565).
1. Durante l’esportazione di segmenti in destinazioni appartenenti a membri dell’elenco di fornitori TCF 2.0, Platform include profili solo se le autorizzazioni del fornitore per Platform (565) *e* sono fornite per ogni ID in un cluster.

Le altre sezioni di questo documento forniscono indicazioni su come configurare Platform e le operazioni sui dati per soddisfare i requisiti di raccolta e applicazione descritti in precedenza.

## Determinare come generare i dati sul consenso dei clienti all’interno della CMP {#consent-data}

Poiché ogni sistema CMP è univoco, devi determinare il modo migliore per consentire ai clienti di fornire il consenso durante l’interazione con il servizio. Una finestra di dialogo per il consenso dei cookie è un metodo comune per ottenere il consenso del cliente. Di seguito è riportato un esempio di finestra di dialogo CMP.

![Esempio di finestra di dialogo della piattaforma di gestione dei consensi.](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

Questa finestra di dialogo deve consentire al cliente di effettuare o meno il consenso:

| Opzione di consenso | Descrizione |
| --- | --- |
| **Finalità** | Le finalità definiscono per quali finalità di tecnologia pubblicitaria un brand può utilizzare i dati di un cliente. Per consentire a Platform di elaborare gli ID cliente, è necessario accettare le seguenti finalità: <ul><li>**Scopo 1**: archiviare e/o accedere a informazioni su un dispositivo</li><li>**Scopo 10**: sviluppare e migliorare i prodotti</li></ul> |
| **Autorizzazioni fornitore** | Oltre a scopi di tecnologia per annunci, la finestra di dialogo deve anche consentire al cliente di acconsentire o rinunciare all’utilizzo dei propri dati da parte di fornitori specifici, tra cui Adobe Experience Platform (565). |

### Stringhe di consenso {#consent-strings}

Indipendentemente dal metodo utilizzato per raccogliere i dati, l’obiettivo è generare un valore stringa in base alle opzioni di consenso scelte dal cliente, denominato stringa di consenso.

Nella specifica TCF, le stringhe di consenso vengono utilizzate per codificare dettagli rilevanti sulle impostazioni di consenso di un cliente, in termini di finalità di marketing specifiche, come definite dalle politiche e dai fornitori. Platform utilizza queste stringhe per memorizzare le impostazioni di consenso per ciascun cliente, pertanto ogni volta che tali impostazioni cambiano deve essere generata una nuova stringa di consenso.

Le stringhe di consenso possono essere create solo da una CMP registrata con IAB TCF. Per ulteriori informazioni su come generare stringhe di consenso utilizzando la tua CMP specifica, consulta la [guida alla formattazione delle stringhe di consenso](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) nell&#39;archivio GitHub IAB TCF.

## Creare set di dati con campi di consenso TCF {#datasets}

I dati sul consenso del cliente devono essere inviati a set di dati i cui schemi contengono campi di consenso TCF. Prima di continuare con questa guida, consulta l&#39;esercitazione sulla [creazione di set di dati per l&#39;acquisizione del consenso TCF 2.0](./dataset.md) per informazioni su come creare il set di dati di profilo richiesto (e un set di dati Experience Event facoltativo).

## Aggiorna i criteri di unione di [!DNL Profile] per includere i dati sul consenso {#merge-policies}

Dopo aver creato un set di dati abilitato per [!DNL Profile] per la raccolta dei dati sul consenso, è necessario assicurarsi che i criteri di unione siano stati configurati in modo da includere sempre i campi di consenso TCF nei profili cliente. Ciò comporta l’impostazione della precedenza dei set di dati in modo che il set di dati di consenso abbia priorità rispetto ad altri set di dati potenzialmente in conflitto.

Per ulteriori informazioni su come utilizzare i criteri di unione, consulta la [panoramica dei criteri di unione](/help/profile/merge-policies/overview.md). Durante la configurazione dei criteri di unione, devi assicurarti che i segmenti includano tutti gli attributi di consenso richiesti forniti dal gruppo di campi dello schema di privacy [XDM](./dataset.md#privacy-field-group), come descritto nella guida sulla preparazione dei set di dati.

## Integrare Experience Platform Web SDK per raccogliere i dati sul consenso del cliente {#sdk}

>[!NOTE]
>
>L’utilizzo di Experience Platform Web SDK è necessario per elaborare i dati sul consenso direttamente in Adobe Experience Platform. [!DNL Experience Cloud Identity Service] non è supportato.
>
>[!DNL Experience Cloud Identity Service] è ancora supportato per l&#39;elaborazione del consenso in Adobe Audience Manager, tuttavia la conformità con TCF 2.0 richiede solo che la libreria sia aggiornata alla [versione 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Dopo aver configurato la CMP per generare le stringhe di consenso, è necessario integrare l’SDK per web di Experience Platform per raccogliere tali stringhe e inviarle a Platform. Platform SDK fornisce due comandi che possono essere utilizzati per inviare i dati di consenso TCF a Platform (descritti nelle sottosezioni seguenti). Questi comandi devono essere utilizzati quando un cliente fornisce informazioni sul consenso per la prima volta e in seguito ogni volta che tale consenso cambia.

**L&#39;SDK non si interfaccia con CMP predefiniti**. Sta a te determinare come integrare l’SDK nel tuo sito web, ascoltare le modifiche del consenso nella CMP e chiamare il comando appropriato.

### Creare un flusso di dati

Affinché l’SDK possa inviare dati all’Experience Platform, devi prima creare un flusso di dati per Platform. I passaggi specifici per la creazione di uno stream di dati sono forniti nella [documentazione SDK](/help/datastreams/overview.md).

Dopo aver fornito un nome univoco per lo stream di dati, seleziona il pulsante accanto a **[!UICONTROL Adobe Experience Platform]**. Quindi, utilizzare i valori seguenti per completare il resto del modulo:

| Campo stream di dati | Valore |
| --- | --- |
| [!UICONTROL Sandbox] | Il nome della piattaforma [sandbox](/help/sandboxes/home.md) che contiene la connessione streaming e i set di dati necessari per impostare lo stream di dati. |
| [!UICONTROL Ingresso streaming] | Ad Experience Platform, una connessione in streaming valida. Se non disponi di un ingresso di streaming, consulta l&#39;esercitazione sulla [creazione di una connessione di streaming](/help/ingestion/tutorials/create-streaming-connection-ui.md). |
| [!UICONTROL Set di dati di evento] | Seleziona il set di dati [!DNL XDM ExperienceEvent] creato nel [passaggio precedente](#datasets). Se hai incluso il gruppo di campi [[!UICONTROL IAB TCF 2.0 Consent]](/help/xdm/field-groups/event/iab.md) nello schema di questo set di dati, puoi tenere traccia degli eventi di modifica del consenso nel tempo utilizzando il comando [`sendEvent`](#sendEvent), memorizzando tali dati in questo set di dati. Tieni presente che i valori di consenso memorizzati in questo set di dati sono **non** utilizzati nei flussi di lavoro di applicazione automatica. |
| [!UICONTROL Set di dati di profilo] | Seleziona il set di dati [!DNL XDM Individual Profile] creato nel [passaggio precedente](#datasets). Quando si risponde agli hook di modifica del consenso di CMP tramite il comando [`setConsent`](#setConsent), i dati raccolti vengono memorizzati in questo set di dati. Poiché questo set di dati è abilitato per il profilo, i valori del consenso memorizzati in questo set di dati vengono rispettati durante i flussi di lavoro di applicazione automatica. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Al termine, seleziona **[!UICONTROL Salva]** nella parte inferiore della schermata e continua seguendo eventuali altre richieste per completare la configurazione.

### Esecuzione di comandi per la modifica del consenso

Dopo aver creato lo stream di dati descritto nella sezione precedente, puoi iniziare a utilizzare i comandi SDK per inviare i dati del consenso a Platform. Le sezioni seguenti forniscono esempi di come ogni comando SDK può essere utilizzato in scenari diversi.

#### Utilizzo degli hook per la modifica del consenso di CMP {#setConsent}

Molte CMP forniscono hook pronti all’uso in grado di ascoltare gli eventi di modifica del consenso. Quando si verificano questi eventi, è possibile utilizzare il comando [`setConsent`](/help/web-sdk/commands/setconsent.md) per aggiornare i dati del consenso del cliente.

Il comando `setConsent` prevede due argomenti:

1. Stringa che indica il tipo di comando (in questo caso, &quot;setConsent&quot;).
1. Payload contenente un array `consent`. L’array deve contenere almeno un oggetto che fornisca i campi di consenso richiesti.

Il comando `setConsent` viene visualizzato di seguito:

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
| `standard` | Lo standard di consenso utilizzato. Questo valore deve essere impostato su `IAB` per l&#39;elaborazione del consenso TCF 2.0. |
| `version` | Il numero di versione dello standard di consenso indicato in `standard`. Questo valore deve essere impostato su `2.0` per l&#39;elaborazione del consenso TCF 2.0. |
| `value` | Stringa di consenso con codifica base 64 generata dalla CMP. |
| `gdprApplies` | Valore booleano che indica se il RGPD si applica al cliente attualmente connesso. Affinché TCF 2.0 possa essere applicato a questo cliente, il valore deve essere impostato su `true`. Impostazione predefinita: `true` se non definita. |

Il comando `setConsent` deve essere utilizzato come parte di un hook CMP che rileva le modifiche nelle impostazioni di consenso. Il seguente JavaScript fornisce un esempio di come il comando `setConsent` può essere utilizzato per l&#39;hook `OnConsentChanged` di OneTrust:

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

È inoltre possibile raccogliere i dati sul consenso TCF 2.0 su ogni evento attivato in Platform utilizzando il comando `sendEvent`.

>[!NOTE]
>
>Per utilizzare questo metodo, è necessario aggiungere il gruppo di campi Privacy evento esperienza allo schema [!DNL XDM ExperienceEvent] abilitato per [!DNL Profile]. Consulta la sezione sull&#39;aggiornamento dello schema ExperienceEvent](./dataset.md#event-schema) nella guida alla preparazione del set di dati per i passaggi su come configurare questo elemento.[

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
| `xdm.consentStrings` | Array che deve contenere almeno un oggetto che fornisca i campi di consenso richiesti. |
| `consentStandard` | Lo standard di consenso utilizzato. Questo valore deve essere impostato su `IAB` per l&#39;elaborazione del consenso TCF 2.0. |
| `consentStandardVersion` | Il numero di versione dello standard di consenso indicato in `standard`. Questo valore deve essere impostato su `2.0` per l&#39;elaborazione del consenso TCF 2.0. |
| `consentStringValue` | Stringa di consenso con codifica base 64 generata dalla CMP. |
| `gdprApplies` | Valore booleano che indica se il RGPD si applica al cliente attualmente connesso. Affinché TCF 2.0 possa essere applicato a questo cliente, il valore deve essere impostato su `true`. Impostazione predefinita: `true` se non definita. |

### Gestione delle risposte SDK

Molti comandi Web SDK restituiscono promesse che indicano se la chiamata è riuscita o meno. Puoi quindi utilizzare queste risposte per una logica aggiuntiva, ad esempio per visualizzare i messaggi di conferma al cliente. Per ulteriori informazioni, vedere [Risposte ai comandi](/help/web-sdk/commands/command-responses.md).

## Esportare segmenti {#export}

>[!NOTE]
>
>Prima di iniziare l’esportazione dei segmenti, è necessario assicurarsi che i segmenti includano tutti i campi di consenso richiesti. Per ulteriori informazioni, vedere la sezione relativa alla [configurazione dei criteri di unione](#merge-policies).

Dopo aver raccolto i dati sul consenso dei clienti e aver creato segmenti di pubblico contenenti gli attributi di consenso richiesti, puoi applicare la conformità TCF 2.0 durante l’esportazione di tali segmenti in destinazioni a valle.

Se l&#39;impostazione di consenso `gdprApplies` è impostata su `true` per un set di profili cliente, tutti i dati di tali profili esportati nelle destinazioni a valle vengono filtrati in base alle preferenze di consenso TCF per ciascun profilo. Qualsiasi profilo che non soddisfi le preferenze di consenso richieste viene saltato durante il processo di esportazione.

I clienti devono acconsentire alle seguenti finalità (come indicato da [Criteri TCF 2.0](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) per includere i propri profili nei segmenti esportati nelle destinazioni:

* **Scopo 1**: archiviare e/o accedere a informazioni su un dispositivo
* **Scopo 10**: sviluppare e migliorare i prodotti

TCF 2.0 richiede inoltre che l’origine dei dati verifichi l’autorizzazione del fornitore della destinazione prima di inviare i dati a tale destinazione. Platform controlla quindi se l’autorizzazione del fornitore della destinazione ha acconsentito a tutti gli ID nel cluster prima di includere i dati associati a tale destinazione.

>[!NOTE]
>
>Tutti i segmenti condivisi con Adobe Audience Manager contengono gli stessi valori di consenso TCF 2.0 delle controparti di Platform. Poiché [!DNL Audience Manager] condivide lo stesso ID fornitore di Platform (565), sono necessari gli stessi scopi e le stesse autorizzazioni del fornitore. Per ulteriori informazioni, vedere il documento sul plug-in [Adobe Audience Manager per IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=it).

## Testare l’implementazione {#test-implementation}

Dopo aver configurato l’implementazione di TCF 2.0 e aver esportato i segmenti nelle destinazioni, tutti i dati che non soddisfano i requisiti di consenso non verranno esportati. Per verificare se i profili cliente corretti sono stati filtrati durante l’esportazione, controlla manualmente gli archivi dati sulle destinazioni per verificare se il consenso è stato applicato correttamente.

>[!IMPORTANT]
>
>Se un cluster è costituito da più ID e viene applicato TCF 2.0, l’intero cluster viene escluso se anche un singolo ID non contiene le finalità e le autorizzazioni fornitore corrette.

## Passaggi successivi

In questo documento viene descritto il processo di configurazione delle operazioni relative ai dati di Platform per soddisfare gli obblighi aziendali descritti dal TCF 2.0. Per ulteriori informazioni sulle funzionalità relative alla privacy di Platform, consulta la panoramica su [governance, privacy e sicurezza](../../overview.md).
