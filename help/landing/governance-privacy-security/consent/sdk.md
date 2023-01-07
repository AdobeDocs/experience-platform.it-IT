---
title: Elaborazione dei dati di consenso dei clienti tramite Adobe Experience Platform Web SDK
description: Scopri come integrare Adobe Experience Platform Web SDK per elaborare i dati sul consenso dei clienti in Adobe Experience Platform.
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 1%

---

# Integrare Platform Web SDK per elaborare i dati sul consenso dei clienti

Adobe Experience Platform Web SDK consente di recuperare i segnali di consenso generati dalle piattaforme di gestione del consenso (CMP, Consent Management Platforms) e inviarli a Adobe Experience Platform ogni volta che si verifica un evento di modifica del consenso.

**L’SDK non si interfaccia con alcuna CMP preconfigurata**. Sta a te determinare come integrare l’SDK nel tuo sito web, ascoltare le modifiche al consenso nella CMP e chiamare il comando appropriato. Questo documento fornisce indicazioni generali su come integrare CMP con Platform Web SDK.

## Prerequisiti {#prerequisites}

Questa esercitazione presuppone che tu abbia già determinato come generare i dati di consenso all’interno di CMP e che tu abbia creato un set di dati contenente i campi di consenso conformi allo standard Adobe o allo standard IAB Transparency and Consent Framework (TCF) 2.0 . Se non hai ancora creato questo set di dati, consulta le seguenti esercitazioni prima di tornare a questa guida:

* [Creare un set di dati utilizzando lo standard Adobe](./adobe/dataset.md)
* [Creare un set di dati utilizzando lo standard TCF 2.0](./iab/dataset.md)

Questa guida segue il flusso di lavoro per configurare l&#39;SDK utilizzando l&#39;estensione tag nell&#39;interfaccia utente. Se non desideri utilizzare l&#39;estensione e preferisci incorporare direttamente sul tuo sito la versione autonoma dell&#39;SDK, consulta i seguenti documenti invece di questa guida:

* [Configurare un datastream](../../../edge/datastreams/overview.md)
* [Installare l’SDK](../../../edge/fundamentals/installing-the-sdk.md)
* [Configurare l&#39;SDK per i comandi di consenso](../../../edge/consent/supporting-consent.md)

I passaggi di installazione in questa guida richiedono una comprensione efficace delle estensioni dei tag e della loro installazione nelle applicazioni web. Per ulteriori informazioni, consulta la seguente documentazione:

* [Panoramica sui tag](../../../tags/home.md)
* [Guida rapida](../../../tags/quick-start/quick-start.md)
* [Panoramica sulla pubblicazione](../../../tags/ui/publishing/overview.md)

## Configurare un datastream

Affinché l’SDK invii dati ad Experience Platform, devi prima configurare un datastream. Nell’interfaccia utente Raccolta dati o Experience Platform, seleziona **[!UICONTROL Datastreams]** nella navigazione a sinistra.

Dopo aver creato un nuovo datastream o selezionato uno esistente da modificare, seleziona il pulsante di attivazione accanto a **[!UICONTROL Adobe Experience Platform]**. Quindi, utilizza i valori elencati di seguito per completare il modulo.

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Campo Datastream | Valore |
| --- | --- |
| [!UICONTROL Sandbox] | Nome della piattaforma [sandbox](../../../sandboxes/home.md) che contiene la connessione streaming e i set di dati richiesti per impostare il datastream. |
| [!UICONTROL Ingresso streaming] | Una connessione in streaming valida, ad Experience Platform. Guarda l’esercitazione su [creazione di una connessione in streaming](../../../ingestion/tutorials/create-streaming-connection-ui.md) se non disponi di un ingresso streaming esistente. |
| [!UICONTROL Set di dati evento] | Un [!DNL XDM ExperienceEvent] set di dati che prevedi di inviare dati evento all’SDK. Anche se devi fornire un set di dati evento per creare un archivio dati Platform, tieni presente che i dati di consenso inviati tramite eventi non sono rispettati nei flussi di lavoro di applicazione a valle. |
| [!UICONTROL Set di dati del profilo] | La [!DNL Profile]Set di dati abilitato con i campi di consenso creati dall’utente [precedente](#prerequisites). |

Al termine, seleziona **[!UICONTROL Salva]** nella parte inferiore della schermata e continuare a seguire eventuali ulteriori prompt per completare la configurazione.

## Installare e configurare l’SDK per web di Platform

Dopo aver creato un datastream come descritto nella sezione precedente, devi configurare l’estensione Platform Web SDK che distribuirai in ultima analisi sul sito. Se l&#39;estensione SDK non è installata nella proprietà tag, seleziona **[!UICONTROL Estensioni]** nella navigazione a sinistra, seguita dalla **[!UICONTROL Catalogo]** scheda . Quindi, seleziona **[!UICONTROL Installa]** nell’elenco delle estensioni disponibili, all’interno dell’estensione Platform SDK.

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

Quando configuri l&#39;SDK, in **[!UICONTROL Configurazioni perimetrali]**, seleziona il datastream creato nel passaggio precedente.

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Seleziona **[!UICONTROL Salva]** per installare l&#39;estensione .

### Creare un elemento dati per impostare il consenso predefinito

Con l&#39;estensione SDK installata, puoi creare un elemento dati per rappresentare il valore predefinito di consenso per la raccolta dati (`collect.val`) per i tuoi utenti. Può essere utile se desideri avere valori predefiniti diversi a seconda dell’utente, ad esempio `pending` per gli utenti dell&#39;Unione europea e `in` per gli utenti nordamericani.

In questo caso d’uso, puoi implementare quanto segue per impostare il consenso predefinito in base all’area geografica dell’utente:

1. Determinare la regione dell’utente sul server web.
1. Prima della `script` tag (codice di incorporamento) sulla pagina web, esegui il rendering di un `script` che imposta un `adobeDefaultConsent` in base all&#39;area geografica dell&#39;utente.
1. Imposta un elemento dati che utilizza il `adobeDefaultConsent` Variabile JavaScript e utilizza questo elemento dati come valore di consenso predefinito per l’utente.

Se l&#39;area geografica dell&#39;utente è determinata da una CMP, puoi invece utilizzare i seguenti passaggi:

1. Gestisci l’evento &quot;CMP loaded&quot; sulla pagina.
1. Nel gestore eventi, imposta un `adobeDefaultConsent` in base all&#39;area geografica dell&#39;utente, quindi carica lo script della libreria di tag utilizzando JavaScript.
1. Imposta un elemento dati che utilizza il `adobeDefaultConsent` Variabile JavaScript e utilizza questo elemento dati come valore di consenso predefinito per l’utente.

Per creare un elemento dati nell’interfaccia utente, seleziona **[!UICONTROL Elementi dati]** nel menu di navigazione a sinistra, seleziona **[!UICONTROL Aggiungi elemento dati]** per passare alla finestra di dialogo di creazione dell’elemento dati.

Da qui, devi creare un [!UICONTROL Variabile JavaScript] elemento dati basato su `adobeDefaultConsent`. Al termine, seleziona **[!UICONTROL Salva]**.

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

Una volta creato l&#39;elemento dati, torna alla pagina di configurazione dell&#39;estensione SDK per web. Sotto la [!UICONTROL Privacy] sezione , seleziona **[!UICONTROL Fornito dall’elemento dati]** e utilizza la finestra di dialogo fornita per selezionare l’elemento dati del consenso predefinito creato in precedenza.

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Distribuire l&#39;estensione sul sito web

Dopo aver configurato l&#39;estensione, questa può essere integrata nel sito web. Fai riferimento a [guida alla pubblicazione](../../../tags/ui/publishing/overview.md) nella documentazione sui tag per informazioni dettagliate su come distribuire la build della libreria aggiornata.

## Esecuzione di comandi di modifica del consenso {#commands}

Dopo aver integrato l’estensione SDK nel sito web, puoi iniziare a utilizzare l’SDK per web di Platform `setConsent` per inviare i dati di consenso a Platform.

La `setConsent` esegue due azioni:

1. Aggiorna gli attributi del profilo dell’utente direttamente nell’archivio profili. Questo non invia dati al data lake.
1. Crea un [Evento esperienza](../../../xdm/classes/experienceevent.md) registra un account con marca temporale dell’evento di modifica del consenso. Questi dati vengono inviati direttamente al data lake e possono essere utilizzati per tenere traccia delle modifiche delle preferenze di consenso nel tempo.

### Quando chiamare `setConsent`

Esistono due scenari in cui `setConsent` dovrebbe essere chiamato sul tuo sito:

1. Quando il consenso viene caricato sulla pagina (in altre parole, a ogni caricamento di pagina)
1. Come parte di un hook CMP o listener di eventi che rileva le modifiche nelle impostazioni di consenso

### `setConsent` sintassi

>[!NOTE]
>
>Per un’introduzione alla sintassi comune per i comandi SDK di Platform, consulta il documento su [esecuzione di comandi](../../../edge/fundamentals/executing-commands.md).

La `setConsent` Il comando prevede due argomenti:

1. Una stringa che indica il tipo di comando (in questo caso, `"setConsent"`)
1. Un oggetto payload contenente una singola proprietà di tipo array: `consent`. La `consent` deve contenere almeno un oggetto che fornisca i campi di consenso richiesti per lo standard Adobe.

I campi di consenso richiesti per lo standard di Adobe sono mostrati nell’esempio seguente `setConsent` chiamata:

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
| `standard` | Lo standard di consenso in uso. Per lo standard Adobe, questo valore deve essere impostato su `Adobe`. |
| `version` | Numero di versione dello standard di consenso indicato in `standard`. Questo valore deve essere impostato su `2.0` per l’elaborazione del consenso standard di Adobe. |
| `value` | Le informazioni di consenso aggiornate del cliente, fornite come oggetto XDM conforme alla struttura dei campi di consenso del set di dati abilitati per il profilo. |

>[!NOTE]
>
>Se utilizzi altri standard di consenso in combinazione con `Adobe` (quali `IAB TCF`), è possibile aggiungere ulteriori oggetti al `consent` per ogni standard. Ogni oggetto deve contenere valori appropriati per `standard`, `version`e `value` per lo standard di consenso che rappresentano.

Il seguente JavaScript fornisce un esempio di una funzione che gestisce le modifiche delle preferenze di consenso su un sito web, che può essere utilizzata come callback in un listener di eventi o un hook CMP:

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

Tutto [!DNL Platform SDK] i comandi restituiscono promesse che indicano se la chiamata è riuscita o meno. Puoi quindi utilizzare queste risposte per ottenere una logica aggiuntiva, ad esempio per visualizzare messaggi di conferma al cliente. Vedi la sezione su [gestione del successo o dell&#39;errore](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) nella guida sull’esecuzione dei comandi SDK per esempi specifici.

Una volta effettuata con successo `setConsent` con l’SDK, puoi utilizzare il visualizzatore del profilo nell’interfaccia utente di Platform per verificare se i dati sono di destinazione nell’archivio profili. Vedi la sezione su [esplorazione dei profili per identità](../../../profile/ui/user-guide.md#browse-identity) per ulteriori informazioni.

## Passaggi successivi

Seguendo questa guida, hai configurato l’estensione Platform Web SDK per inviare ad Experience Platform i dati di consenso. Per informazioni su come verificare l’implementazione, consulta la documentazione relativa allo standard di consenso che stai implementando:

* [Adobe standard](./adobe/overview.md#test)
* [Standard TCF 2.0](./iab/overview.md#test)
