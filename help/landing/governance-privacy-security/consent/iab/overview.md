---
keywords: Experience Platform;home;IAB;IAB 2.0;consenso;consenso
solution: Experience Platform
title: Supporto IAB TCF 2.0 in Experience Platform
topic-legacy: privacy events
description: Scopri come configurare le operazioni e gli schemi di dati per trasmettere le scelte di consenso dei clienti quando si attivano i segmenti nelle destinazioni in Adobe Experience Platform.
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: a3468d55d95b89c075abf91391bd7dfaa974742c
workflow-type: tm+mt
source-wordcount: '2564'
ht-degree: 1%

---

# Supporto IAB TCF 2.0 in Experience Platform

Il [!DNL Transparency & Consent Framework] (TCF), come indicato da [!DNL Interactive Advertising Bureau] (IAB), è un framework tecnico open-standard inteso a consentire alle organizzazioni di ottenere, registrare e aggiornare il consenso dei consumatori per il trattamento dei loro dati personali, in conformità con il [!DNL General Data Protection Regulation] (RGPD) dell&#39;Unione europea. La seconda iterazione del framework, TCF 2.0, offre maggiore flessibilità per quanto riguarda il modo in cui i consumatori possono fornire o rifiutare il consenso, tra cui se e come i fornitori possono utilizzare determinate caratteristiche del trattamento dei dati, come ad esempio una geolocalizzazione precisa.

>[!NOTE]
>
>Ulteriori informazioni su TCF 2.0 sono disponibili sul sito web [IAB Europe](https://iabeurope.eu/tcf-2-0/), compresi materiali di supporto e specifiche tecniche.

Adobe Experience Platform fa parte dell&#39; [elenco fornitori IAB TCF 2.0](https://iabeurope.eu/vendor-list-tcf-v2-0/) registrato, sotto l&#39;ID **565**. In conformità ai requisiti di TCF 2.0, Platform ti consente di raccogliere i dati sul consenso del cliente e integrarli nei profili cliente memorizzati. Questi dati di consenso possono quindi essere fatti in modo da determinare se i profili sono inclusi nei segmenti di pubblico esportati, a seconda del loro caso d’uso.

>[!IMPORTANT]
>
>Platform è in grado di soddisfare solo la versione 2.0 del TCF (o superiore). Le versioni precedenti di TCF non sono supportate.

Questo documento fornisce una panoramica su come configurare le operazioni sui dati e gli schemi di profilo per accettare i dati di consenso dei clienti generati dalla CMP e su come Platform trasmette le scelte di consenso degli utenti durante l’esportazione dei segmenti.

## Prerequisiti

Per seguire questa guida, devi utilizzare una piattaforma di gestione dei consensi (CMP, Consent Management Platform), commerciale o tua, integrata e conforme con IAB TCF. Per ulteriori informazioni, consulta l’ [elenco delle CMP conformi](https://iabeurope.eu/cmp-list/) .

>[!IMPORTANT]
>
>Se l’ID della CMP non è valido, Platform manterrà l’elaborazione dei dati così come sono. Per applicare TCF 2.0, devi confermare che la tua CMP abbia un ID valido registrato con IAB TCF 2.0 prima di inviare dati a Platform.

Questa guida richiede anche una buona comprensione dei seguenti servizi Platform:

* [Experience Data Model (XDM)](../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
* [Servizio](../../../../identity-service/home.md) Adobe Experience Platform Identity: Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati sulla customer experience attraverso il collegamento di identità tra dispositivi e sistemi.
* [Profilo](../../../../profile/home.md) cliente in tempo reale: Utilizza  [!DNL Identity Service] per creare profili cliente dettagliati dai set di dati in tempo reale. [!DNL Real-time Customer Profile] richiama i dati dal Data Lake e persiste i profili dei clienti nel proprio archivio dati separato.
* [SDK](../../../../edge/home.md) web Adobe Experience Platform: Libreria JavaScript lato client che consente di integrare vari servizi Platform nel sito web rivolto ai clienti.
   * [Comandi](../../../../edge/consent/supporting-consent.md) di consenso SDK: Panoramica del caso d’uso dei comandi SDK relativi al consenso visualizzati in questa guida.
* [Servizio](../../../../segmentation/home.md) di segmentazione di Adobe Experience Platform: Consente di suddividere  [!DNL Real-time Customer Profile] i dati in gruppi di singoli utenti che condividono caratteristiche simili e risponderanno in modo simile alle strategie di marketing.

Oltre ai servizi Platform elencati sopra, devi anche conoscere [destinazioni](../../../../data-governance/home.md) e il loro ruolo nell’ecosistema della piattaforma.

## Riepilogo del flusso del consenso del cliente {#summary}

Le sezioni seguenti descrivono come i dati di consenso vengono raccolti e applicati dopo che il sistema è stato configurato correttamente.

### Raccolta dati di consenso

Platform ti consente di raccogliere i dati sul consenso dei clienti attraverso il seguente processo:

1. Un cliente fornisce le proprie preferenze di consenso per la raccolta dei dati tramite una finestra di dialogo sul sito web.
1. La CMP rileva la modifica della preferenza di consenso e genera di conseguenza i dati di consenso TCF.
1. Utilizzando l’SDK per web di Platform, i dati di consenso generati (restituiti da CMP) vengono inviati a Adobe Experience Platform.
1. I dati di consenso raccolti vengono acquisiti in un set di dati abilitato [!DNL Profile] il cui schema contiene campi di consenso TCF.

Oltre ai comandi SDK attivati dagli hook di CMP per la modifica del consenso, i dati di consenso possono fluire in Experience Platform attraverso qualsiasi dato XDM generato dal cliente e caricato direttamente in un set di dati abilitato [!DNL Profile].

Anche qualsiasi segmento condiviso con Platform da Adobe Audience Manager (tramite il connettore di origine [!DNL Audience Manager] o altro) può contenere dati di consenso, purché i campi appropriati siano stati applicati a tali segmenti tramite [!DNL Experience Cloud Identity Service]. Per ulteriori informazioni sulla raccolta dei dati di consenso in [!DNL Audience Manager], consulta il documento sul plug-in [Adobe Audience Manager per IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=it).

### Applicazione del consenso a valle

Una volta che i dati di consenso TCF sono stati correttamente acquisiti, i seguenti processi si svolgono nei servizi della piattaforma a valle:

1. [!DNL Real-time Customer Profile] aggiorna i dati di consenso memorizzati per il profilo del cliente.
1. Platform elabora gli ID cliente solo se viene fornita l’autorizzazione fornitore per Platform (565) per ogni ID in un cluster.
1. Quando si esportano segmenti in destinazioni appartenenti a membri dell’elenco dei fornitori di TCF 2.0, Platform include i profili solo se le autorizzazioni del fornitore per entrambe le piattaforme (565) *e* vengono fornite le singole destinazioni per ogni ID in un cluster.

Le altre sezioni di questo documento forniscono indicazioni su come configurare Platform e le operazioni sui dati per soddisfare i requisiti di raccolta e applicazione descritti in precedenza.

## Determinare come generare i dati di consenso dei clienti all’interno di CMP {#consent-data}

Poiché ogni sistema CMP è univoco, devi determinare il modo migliore per consentire ai tuoi clienti di fornire il consenso mentre interagiscono con il tuo servizio. Un modo comune per ottenere questo risultato è l’utilizzo di una finestra di dialogo di consenso dei cookie, simile all’esempio seguente:

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

Questa finestra di dialogo deve consentire al cliente di scegliere tra:

| Opzione di consenso | Descrizione |
| --- | --- |
| **Finalità** | Gli scopi definiscono a quali scopi ad tech un marchio può utilizzare i dati di un cliente. Affinché Platform possa elaborare gli ID cliente, è necessario effettuare le seguenti operazioni: <ul><li>**Scopo 1**: Archiviare e/o accedere alle informazioni su un dispositivo</li><li>**Finalità 10**: Sviluppare e migliorare i prodotti</li></ul> |
| **Autorizzazioni fornitore** | Oltre a scopi ad-tech, la finestra di dialogo deve anche consentire al cliente di scegliere se accettare o meno i propri dati utilizzati da fornitori specifici, incluso Adobe Experience Platform (565). |

### Stringhe di consenso {#consent-strings}

Indipendentemente dal metodo utilizzato per raccogliere i dati, l’obiettivo è quello di generare un valore stringa basato sulle opzioni di consenso scelte dal cliente, denominata stringa di consenso.

Nella specifica TCF, le stringhe di consenso vengono utilizzate per codificare i dettagli rilevanti sulle impostazioni di consenso di un cliente, in termini di finalità di marketing specifiche definite da policy e fornitori. Platform utilizza queste stringhe per memorizzare le impostazioni di consenso per ciascun cliente, pertanto ogni volta che queste impostazioni cambiano, deve essere generata una nuova stringa di consenso.

Le stringhe di consenso possono essere create solo da una CMP registrata con IAB TCF. Per ulteriori informazioni su come generare stringhe di consenso utilizzando la CMP in uso, consulta la [guida alla formattazione delle stringhe di consenso](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) nell’archivio GitHub IAB TCF.

## Creare set di dati con campi di consenso TCF {#datasets}

I dati di consenso del cliente devono essere inviati ai set di dati i cui schemi contengono campi di consenso TCF. Fai riferimento all’esercitazione su [creazione di set di dati per l’acquisizione del consenso TCF 2.0](./dataset.md) per scoprire come creare il set di dati di profilo richiesto (e un set di dati opzionale per gli eventi di esperienza) prima di continuare con questa guida.

## Aggiornare [!DNL Profile] i criteri di unione per includere i dati di consenso {#merge-policies}

Dopo aver creato un set di dati abilitato [!DNL Profile] per la raccolta dei dati di consenso, assicurati che i criteri di unione siano stati configurati in modo da includere sempre i campi di consenso TCF nei profili dei clienti. Ciò comporta l’impostazione della precedenza del set di dati in modo che il set di dati di consenso abbia priorità rispetto ad altri set di dati potenzialmente in conflitto.

Per ulteriori informazioni su come utilizzare i criteri di unione, vedere [panoramica dei criteri di unione](../../../../profile/merge-policies/overview.md). Quando imposti i criteri di unione, devi accertarti che i segmenti includano tutti gli attributi di consenso richiesti dal gruppo di campi [schema privacy XDM](./dataset.md#privacy-field-group), come descritto nella guida sulla preparazione dei set di dati.

## Integra l’SDK web per Experience Platform per raccogliere i dati sul consenso dei clienti. {#sdk}

>[!NOTE]
>
>Per elaborare i dati di consenso direttamente in Adobe Experience Platform è necessario utilizzare Experience Platform Web SDK. [!DNL Experience Cloud Identity Service] attualmente non supportato.
>
>[!DNL Experience Cloud Identity Service] è ancora supportato per l’elaborazione del consenso in Adobe Audience Manager, tuttavia, e la conformità con TCF 2.0 richiede solo che la libreria venga aggiornata alla  [versione 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Dopo aver configurato la CMP per generare le stringhe di consenso, è necessario integrare l’SDK web di Experience Platform per raccogliere tali stringhe e inviarle a Platform. L’SDK di Platform fornisce due comandi che possono essere utilizzati per inviare i dati di consenso TCF a Platform (descritti nelle sottosezioni seguenti) e devono essere utilizzati quando un cliente fornisce informazioni di consenso per la prima volta e in qualsiasi momento in cui il consenso viene modificato.

**L’SDK non si interfaccia con alcuna CMP preconfigurata**. Sta a te determinare come integrare l’SDK nel tuo sito web, ascoltare le modifiche al consenso nella CMP e chiamare il comando appropriato.

### Creare una nuova configurazione perimetrale

Affinché l’SDK invii dati ad Experience Platform, devi prima creare una nuova configurazione edge per Platform in [!DNL Adobe Experience Platform Launch]. I passaggi specifici per la creazione di una nuova configurazione sono descritti nella documentazione [SDK](../../../../edge/fundamentals/datastreams.md).

Dopo aver fornito un nome univoco per la configurazione, seleziona il pulsante di attivazione accanto a **[!UICONTROL Adobe Experience Platform]**. Quindi, utilizzare i seguenti valori per completare il resto del modulo:

| Campo di configurazione perimetrale | Valore |
| --- | --- |
| [!UICONTROL Sandbox] | Il nome della piattaforma [sandbox](../../../../sandboxes/home.md) che contiene la connessione in streaming e i set di dati richiesti per impostare la configurazione Edge. |
| [!UICONTROL Ingresso streaming] | Una connessione in streaming valida, ad Experience Platform. Se non disponi di un&#39;entrata in streaming, consulta l&#39;esercitazione su [creazione di una connessione in streaming](../../../../ingestion/tutorials/create-streaming-connection-ui.md) . |
| [!UICONTROL Set di dati evento] | Seleziona il set di dati [!DNL XDM ExperienceEvent] creato nel [passaggio precedente](#datasets). Se hai incluso il gruppo di campi [[!UICONTROL Consent] IAB TCF 2.0](../../../../xdm/field-groups/event/iab.md) nello schema di questo set di dati, puoi tenere traccia degli eventi di modifica del consenso nel tempo utilizzando il comando [`sendEvent`](#sendEvent), memorizzando tali dati in questo set di dati. Tieni presente che i valori di consenso memorizzati in questo set di dati sono **non** utilizzati nei flussi di lavoro di implementazione automatica. |
| [!UICONTROL Set di dati del profilo] | Seleziona il set di dati [!DNL XDM Individual Profile] creato nel [passaggio precedente](#datasets). Quando rispondi agli hook di modifica del consenso CMP utilizzando il comando [`setConsent`](#setConsent), i dati raccolti saranno memorizzati in questo set di dati. Poiché questo set di dati è abilitato per il profilo, i valori di consenso memorizzati in questo set di dati vengono rispettati durante i flussi di lavoro di implementazione automatica. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Al termine, seleziona **[!UICONTROL Salva]** nella parte inferiore dello schermo e continua a seguire tutte le istruzioni aggiuntive per completare la configurazione.

### Esecuzione di comandi di modifica del consenso

Dopo aver creato la configurazione perimetrale descritta nella sezione precedente, puoi iniziare a utilizzare i comandi SDK per inviare i dati di consenso a Platform. Le sezioni seguenti forniscono esempi di come ogni comando SDK può essere utilizzato in scenari diversi.

>[!NOTE]
>
>Per un’introduzione alla sintassi comune per tutti i comandi SDK di Platform, consulta il documento relativo all’ [esecuzione di comandi](../../../../edge/fundamentals/executing-commands.md).

#### Utilizzo degli hook CMP per la modifica del consenso {#setConsent}

Molte CMP forniscono hook predefiniti che ascoltano eventi di cambiamento del consenso. Quando si verificano tali eventi, puoi utilizzare il comando `setConsent` per aggiornare i dati di consenso del cliente.

Il comando `setConsent` prevede due argomenti: (1) una stringa che indica il tipo di comando (in questo caso, &quot;setConsent&quot;) e (2) un payload contenente una matrice `consent` che deve contenere almeno un oggetto che fornisce i campi di consenso richiesti, come illustrato di seguito:

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
| `standard` | Lo standard di consenso in uso. Questo valore deve essere impostato su `IAB` per l’elaborazione del consenso TCF 2.0. |
| `version` | Il numero di versione dello standard di consenso indicato in `standard`. Questo valore deve essere impostato su `2.0` per l’elaborazione del consenso TCF 2.0. |
| `value` | Stringa di consenso con codifica base 64 generata dalla CMP. |
| `gdprApplies` | Un valore booleano che indica se il RGPD è applicabile al cliente attualmente connesso. Affinché TCF 2.0 sia applicato per questo cliente, il valore deve essere impostato su `true`. Se non è definito, viene impostato il valore predefinito `true`. |

Il comando `setConsent` deve essere utilizzato come parte di un hook CMP che rileva le modifiche nelle impostazioni di consenso. Il seguente JavaScript fornisce un esempio di come il comando `setConsent` può essere utilizzato per il gancio di OneTrust `OnConsentChanged`:

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

Puoi anche raccogliere i dati di consenso TCF 2.0 su ogni evento attivato in Platform utilizzando il comando `sendEvent` .

>[!NOTE]
>
>Per utilizzare questo metodo, devi aver aggiunto il gruppo di campi Privacy dell’evento esperienza allo schema [!DNL Profile] abilitato [!DNL XDM ExperienceEvent] . Consulta la sezione sull’ [aggiornamento dello schema ExperienceEvent](./dataset.md#event-schema) nella guida alla preparazione dei set di dati per i passaggi su come configurarlo.

Il comando `sendEvent` deve essere utilizzato come callback nei listener di eventi appropriati sul sito web. Il comando prevede due argomenti: (1) una stringa che indica il tipo di comando (in questo caso, `sendEvent`) e (2) un payload contenente un oggetto `xdm` che fornisce i campi di consenso richiesti come JSON:

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
| `xdm.consentStrings` | Matrice che deve contenere almeno un oggetto che fornisca i campi di consenso richiesti. |
| `consentStandard` | Lo standard di consenso in uso. Questo valore deve essere impostato su `IAB` per l’elaborazione del consenso TCF 2.0. |
| `consentStandardVersion` | Il numero di versione dello standard di consenso indicato in `standard`. Questo valore deve essere impostato su `2.0` per l’elaborazione del consenso TCF 2.0. |
| `consentStringValue` | Stringa di consenso con codifica base 64 generata dalla CMP. |
| `gdprApplies` | Un valore booleano che indica se il RGPD è applicabile al cliente attualmente connesso. Affinché TCF 2.0 sia applicato per questo cliente, il valore deve essere impostato su `true`. Se non è definito, viene impostato il valore predefinito `true`. |

### Gestione delle risposte SDK

Tutti i comandi [!DNL Platform SDK] restituiscono promesse che indicano se la chiamata è riuscita o meno. Puoi quindi utilizzare queste risposte per ottenere una logica aggiuntiva, ad esempio per visualizzare messaggi di conferma al cliente. Consulta la sezione sulla [gestione del successo o dell&#39;errore](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) nella guida sull&#39;esecuzione dei comandi SDK per esempi specifici.

## Esportare segmenti {#export}

>[!NOTE]
>
>Prima di iniziare l’esportazione dei segmenti, devi accertarti che i segmenti includano tutti i campi di consenso richiesti. Per ulteriori informazioni, consulta la sezione su [configurazione dei criteri di unione](#merge-policies) .

Una volta raccolti i dati di consenso dei clienti e creati segmenti di pubblico contenenti gli attributi di consenso richiesti, puoi applicare la conformità TCF 2.0 durante l’esportazione di tali segmenti nelle destinazioni a valle.

A condizione che l’impostazione di consenso `gdprApplies` sia impostata su `true` per un set di profili cliente, tutti i dati provenienti da tali profili esportati verso destinazioni a valle vengono filtrati in base alle preferenze di consenso TCF per ciascun profilo. Qualsiasi profilo che non soddisfa le preferenze di consenso richieste viene ignorato durante il processo di esportazione.

I clienti devono acconsentire alle seguenti finalità (come indicato da [TCF 2.0 Policies](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) per includere i loro profili nei segmenti esportati nelle destinazioni:

* **Scopo 1**: Archiviare e/o accedere alle informazioni su un dispositivo
* **Finalità 10**: Sviluppare e migliorare i prodotti

TCF 2.0 richiede inoltre che l&#39;origine dei dati controlli l&#39;autorizzazione fornitore della destinazione prima di inviare i dati a tale destinazione. Di conseguenza, Platform controlla se l’autorizzazione fornitore della destinazione viene accettata per tutti gli ID nel cluster prima di includere i dati associati a tale destinazione.

>[!NOTE]
>
>Tutti i segmenti condivisi con Adobe Audience Manager conterranno gli stessi valori di consenso TCF 2.0 dei loro omologhi della piattaforma. Poiché [!DNL Audience Manager] condivide lo stesso ID fornitore di Platform (565), sono necessari gli stessi scopi e le stesse autorizzazioni fornitore. Per ulteriori informazioni, consulta il documento sul [plug-in Adobe Audience Manager per IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) .

## Verificare l’implementazione {#test-implementation}

Dopo aver configurato l’implementazione di TCF 2.0 e aver esportato segmenti nelle destinazioni, i dati che non soddisfano i requisiti di consenso non verranno esportati. Tuttavia, per verificare se i profili cliente corretti sono stati filtrati durante l’esportazione, è necessario controllare manualmente gli archivi di dati sulle destinazioni per verificare se il consenso è stato applicato correttamente.

È importante notare che se più ID compongono un cluster e si applica il TCF 2.0, l&#39;intero cluster verrà escluso se anche un singolo ID non contiene le finalità corrette e le autorizzazioni del fornitore.

## Passaggi successivi

Questo documento illustra il processo di configurazione delle operazioni sui dati di Platform per soddisfare gli obblighi aziendali descritti da TCF 2.0. Per ulteriori informazioni sulle funzionalità relative alla privacy di Platform, consulta la panoramica su [governance, privacy e sicurezza](../../overview.md) .
