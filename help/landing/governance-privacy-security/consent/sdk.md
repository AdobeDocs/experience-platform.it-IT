---
title: Elaborare dati di consenso dei clienti utilizzando Adobe Experience Platform Web SDK
description: Scopri come integrare Adobe Experience Platform Web SDK per elaborare i dati sul consenso dei clienti in Adobe Experience Platform.
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 1%

---

# Integrare Platform Web SDK per elaborare i dati sul consenso dei clienti

Adobe Experience Platform Web SDK consente di recuperare i segnali di consenso del cliente generati dalle piattaforme di gestione del consenso (CMP, Consent Management Platforms) e di inviarli a Adobe Experience Platform ogni volta che si verifica un evento di modifica del consenso.

**L’SDK non si interfaccia con alcuna CMP predefinita**. Sta a te determinare come integrare l’SDK nel tuo sito web, ascoltare le modifiche del consenso nella CMP e chiamare il comando appropriato. Questo documento fornisce indicazioni generali su come integrare la CMP con Platform Web SDK.

## Prerequisiti {#prerequisites}

Questa esercitazione presuppone che tu abbia già determinato come generare i dati sul consenso all’interno della tua CMP e che sia stato creato un set di dati contenente campi di consenso conformi allo standard Adobe o allo standard IAB Transparency and Consent Framework (TCF) 2.0. Se non hai ancora creato questo set di dati, consulta le seguenti esercitazioni prima di tornare a questa guida:

* [Creare un set di dati utilizzando lo standard Adobe](./adobe/dataset.md)
* [Creare un set di dati utilizzando lo standard TCF 2.0](./iab/dataset.md)

Questa guida segue il flusso di lavoro per la configurazione dell’SDK utilizzando l’estensione tag nell’interfaccia utente. Se non desideri utilizzare l&#39;estensione e preferisci incorporare direttamente la versione autonoma dell&#39;SDK sul tuo sito, consulta i seguenti documenti invece di questa guida:

* [Configurare uno stream di dati](../../../edge/datastreams/overview.md)
* [Installare l’SDK](../../../edge/fundamentals/installing-the-sdk.md)
* [Configurare l’SDK per i comandi di consenso](../../../edge/consent/supporting-consent.md)

I passaggi di installazione descritti in questa guida richiedono una buona conoscenza delle estensioni tag e del modo in cui vengono installate nelle applicazioni web. Per ulteriori informazioni, consulta la seguente documentazione:

* [Panoramica sui tag](../../../tags/home.md)
* [Guida rapida](../../../tags/quick-start/quick-start.md)
* [Panoramica sulla pubblicazione](../../../tags/ui/publishing/overview.md)

## Configurare un flusso di dati

Affinché l’SDK possa inviare dati ad Experience Platform, devi prima configurare uno stream di dati. Nell’interfaccia di Data Collection o nell’interfaccia di Experience Platform, seleziona **[!UICONTROL Flussi di dati]** nel menu di navigazione a sinistra.

Dopo aver creato un nuovo stream di dati o averne selezionato uno esistente da modificare, seleziona il pulsante di attivazione/disattivazione accanto a **[!UICONTROL Adobe Experience Platform]**. Quindi, utilizzare i valori elencati di seguito per completare il modulo.

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Campo stream di dati | Valore |
| --- | --- |
| [!UICONTROL Sandbox] | Nome della piattaforma [sandbox](../../../sandboxes/home.md) che contiene la connessione in streaming e i set di dati necessari per impostare lo stream di dati. |
| [!UICONTROL Ingresso streaming] | Ad Experience Platform, una connessione in streaming valida. Guarda il tutorial su [creazione di una connessione in streaming](../../../ingestion/tutorials/create-streaming-connection-ui.md) se non disponi di una presa di streaming esistente. |
| [!UICONTROL Set di dati evento] | Un [!DNL XDM ExperienceEvent] set di dati pianificato per l’invio di dati evento a utilizzando l’SDK. Anche se devi fornire un set di dati evento per creare un flusso di dati di Platform, tieni presente che i dati del consenso inviati tramite eventi non vengono rispettati nei flussi di lavoro di applicazione a valle. |
| [!UICONTROL Set di dati profilo] | Il [!DNL Profile]Set di dati abilitato con campi di consenso cliente creati dall’utente [precedente](#prerequisites). |

Al termine, seleziona **[!UICONTROL Salva]** nella parte inferiore della schermata e continuare a seguire eventuali altre richieste per completare la configurazione.

## Installare e configurare Platform Web SDK

Dopo aver creato un flusso di dati come descritto nella sezione precedente, devi configurare l’estensione Platform Web SDK che infine distribuirai sul sito. Se nella proprietà del tag non è installata l’estensione SDK, seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra, seguito da **[!UICONTROL Catalogo]** scheda. Quindi, seleziona **[!UICONTROL Installa]** nell’estensione Platform SDK all’interno dell’elenco delle estensioni disponibili.

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

Durante la configurazione dell’SDK, in **[!UICONTROL Configurazioni Edge]**, seleziona lo stream di dati creato nel passaggio precedente.

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Seleziona **[!UICONTROL Salva]** per installare l’estensione.

### Creare un elemento dati per impostare il consenso predefinito

Con l’estensione SDK installata, puoi creare un elemento dati che rappresenti il valore di consenso predefinito per la raccolta dati (`collect.val`) per i tuoi utenti. Questa funzione può essere utile se desideri avere valori predefiniti diversi a seconda dell’utente, ad esempio `pending` per gli utenti dell&#39;Unione europea e `in` per gli utenti nordamericani.

In questo caso d’uso, puoi implementare quanto segue per impostare il consenso predefinito in base all’area geografica dell’utente:

1. Determina l’area geografica dell’utente sul server web.
1. Prima di `script` (codice di incorporamento) nella pagina web, esegui il rendering di un `script` tag che imposta un `adobeDefaultConsent` in base all’area geografica dell’utente.
1. Imposta un elemento dati che utilizza `adobeDefaultConsent` JavaScript e utilizza questo elemento dati come valore di consenso predefinito per l’utente.

Se l’area geografica dell’utente è determinata da una CMP, puoi utilizzare i seguenti passaggi:

1. Gestisci l’evento &quot;CMP caricato&quot; sulla pagina.
1. Nel gestore eventi, imposta un `adobeDefaultConsent` in base all’area geografica dell’utente, quindi carica lo script della libreria di tag utilizzando JavaScript.
1. Imposta un elemento dati che utilizza `adobeDefaultConsent` JavaScript e utilizza questo elemento dati come valore di consenso predefinito per l’utente.

Per creare un elemento dati nell’interfaccia utente, seleziona **[!UICONTROL Elementi dati]** nel menu di navigazione a sinistra, seleziona quindi **[!UICONTROL Aggiungi elemento dati]** per passare alla finestra di dialogo di creazione dell’elemento dati.

Da qui, devi creare una [!UICONTROL Variabile JavaScript] elemento dati basato su `adobeDefaultConsent`. Al termine, seleziona **[!UICONTROL Salva]**.

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

Una volta creato l’elemento dati, torna alla pagina di configurazione dell’estensione Web SDK. Sotto [!UICONTROL Privacy] sezione, seleziona **[!UICONTROL Fornito dall’elemento dati]**, e utilizza la finestra di dialogo fornita per selezionare l’elemento dati di consenso predefinito creato in precedenza.

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Distribuire l’estensione sul sito web

Una volta completata la configurazione dell&#39;estensione, puoi integrarla nel sito web. Consulta la sezione [guida alla pubblicazione](../../../tags/ui/publishing/overview.md) nella documentazione sui tag, trovi informazioni dettagliate su come distribuire la build della libreria aggiornata.

## Esecuzione di comandi per la modifica del consenso {#commands}

Dopo aver integrato l’estensione SDK nel sito web, puoi iniziare a utilizzare Platform Web SDK `setConsent` comando per inviare i dati del consenso a Platform.

Il `setConsent` Il comando esegue due azioni:

1. Aggiorna gli attributi del profilo dell&#39;utente direttamente nell&#39;archivio Profili. Questo non invia alcun dato al data lake.
1. Crea un [Evento esperienza](../../../xdm/classes/experienceevent.md) che registra un account con marca temporale dell’evento di modifica del consenso. Questi dati vengono inviati direttamente al data lake e possono essere utilizzati per tenere traccia delle modifiche delle preferenze di consenso nel tempo.

### Quando chiamare `setConsent`

Esistono due scenari in cui `setConsent` deve essere chiamato sul sito:

1. Quando il consenso viene caricato sulla pagina (in altre parole, a ogni caricamento di pagina)
1. Come parte di un hook CMP o di un listener di eventi che rileva le modifiche nelle impostazioni di consenso

### `setConsent` sintassi

>[!NOTE]
>
>Per un’introduzione alla sintassi comune per i comandi SDK di Platform, consulta il documento su [esecuzione di comandi](../../../edge/fundamentals/executing-commands.md).

Il `setConsent` Il comando prevede due argomenti:

1. Una stringa che indica il tipo di comando (in questo caso, `"setConsent"`)
1. Oggetto payload contenente una singola proprietà di tipo array: `consent`. Il `consent` l’array deve contenere almeno un oggetto che fornisca i campi di consenso richiesti per lo standard Adobe.

I campi di consenso richiesti per lo standard Adobe sono mostrati nell’esempio seguente `setConsent` chiama:

```js
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: {
        val: "y"
      },
      share: {
        val: "y"
      },
      personalize: {
        content: {
          val: "y"
        }
      },
      metadata: {
        time: "2020-10-12T15:52:25+00:00"
      }
    }
  }]
});
```

| Payload, proprietà | Descrizione |
| --- | --- |
| `standard` | Lo standard di consenso utilizzato. Per lo standard Adobe, questo valore deve essere impostato su `Adobe`. |
| `version` | Il numero di versione dello standard di consenso indicato in `standard`. Questo valore deve essere impostato su `2.0` ad Adobe l’elaborazione del consenso standard. |
| `value` | Le informazioni di consenso aggiornate del cliente, fornite come oggetto XDM conforme alla struttura dei campi di consenso del set di dati abilitati per il profilo. |

>[!NOTE]
>
>Se utilizzi altri standard di consenso in combinazione con `Adobe` (ad esempio `IAB TCF`), è possibile aggiungere altri oggetti al `consent` per ogni standard. Ogni oggetto deve contenere valori appropriati per `standard`, `version`, e `value` per lo standard di consenso che rappresentano.

Il seguente JavaScript fornisce un esempio di funzione che gestisce le modifiche delle preferenze di consenso su un sito web, che può essere utilizzato come callback in un listener di eventi o in un hook CMP:

```js
var setConsent = function () {

  // Retrieve the current consent data.
  var categories = getConsentData();

  // If the script is running on a consent change, generate a new timestamp.
  // If the script is running on page load, set the timestamp to when the consent values last changed.
  var now = new Date();
  var collectedAt = consentChanged ? now.toISOString() : categories.collectedAt;

  //  Map the consent values and timestamp to XDM
  var consentXDM = {
    collect: {
      val: categories.collect !== -1 ? "y" : "n"
    },
    personalize: {
      content: {
        val: categories.personalizeContent !== -1 ? "y" : "n"
      }
    },
    share: {
      val: categories.share !== -1 ? "y" : "n"
    },
    metadata: {
      time: collectedAt
    }
  };

  // Pass the XDM object to the Platform Web SDK
  alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: consentXDM
    }]
  });
});
```

## Gestione delle risposte SDK

Tutti [!DNL Platform SDK] i comandi restituiscono promesse che indicano se la chiamata è riuscita o meno. Puoi quindi utilizzare queste risposte per una logica aggiuntiva, ad esempio per visualizzare i messaggi di conferma al cliente. Consulta la sezione su [gestione di operazioni riuscite o non riuscite](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) nella guida all’esecuzione dei comandi SDK per esempi specifici.

Dopo aver completato correttamente `setConsent` chiamate con l’SDK, puoi utilizzare il visualizzatore di profili nell’interfaccia utente di Platform per verificare se i dati vengono inviati nell’archivio profili. Consulta la sezione su [esplorazione dei profili per identità](../../../profile/ui/user-guide.md#browse-identity) per ulteriori informazioni.

## Passaggi successivi

Seguendo questa guida, hai configurato l’estensione Platform Web SDK per inviare i dati sul consenso ad Experience Platform. Per informazioni su come testare l’implementazione, consulta la documentazione dello standard di consenso che stai implementando:

* [Standard Adobe](./adobe/overview.md#test)
* [Standard TCF 2.0](./iab/overview.md#test)
