---
title: Elaborazione dei dati di consenso dei clienti tramite Adobe Experience Platform Web SDK
topic-legacy: getting started
description: Scopri come integrare Adobe Experience Platform Web SDK per elaborare i dati sul consenso dei clienti in Adobe Experience Platform utilizzando lo standard Adobe 2.0.
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1254'
ht-degree: 1%

---

# Integra l’SDK per web di Platform per elaborare i dati sul consenso dei clienti utilizzando lo standard Adobe 2.0

Adobe Experience Platform Web SDK consente di recuperare i segnali di consenso generati dalle piattaforme di gestione del consenso (CMP, Consent Management Platforms) e inviarli a Adobe Experience Platform ogni volta che si verifica un evento di modifica del consenso.

**L’SDK non si interfaccia con alcuna CMP preconfigurata**. Sta a te determinare come integrare l’SDK nel tuo sito web, ascoltare le modifiche al consenso nella CMP e chiamare il comando appropriato. Questo documento fornisce indicazioni generali su come integrare CMP con Platform Web SDK.

>[!NOTE]
>
>Questa guida descrive i passaggi necessari per integrare l’SDK tramite un’estensione tag nell’interfaccia utente di Raccolta dati. Se invece desideri utilizzare la versione autonoma dell&#39;SDK, consulta i seguenti documenti:
>
>* [Configurare un datastream](../../../../edge/fundamentals/datastreams.md)
* [Installare l’SDK](../../../../edge/fundamentals/installing-the-sdk.md)
* [Configurare l&#39;SDK per i comandi di consenso](../../../../edge/consent/supporting-consent.md)


## Prerequisiti

Questa esercitazione presuppone che tu abbia già determinato come generare i dati di consenso all’interno di CMP e che tu abbia creato un set di dati contenente i campi di consenso che è stato abilitato per Profilo cliente in tempo reale. Per ulteriori informazioni su questi passaggi, consulta la panoramica sull’ [elaborazione del consenso in Experience Platform](./overview.md) prima di tornare a questa guida.

Inoltre, questa guida richiede una buona conoscenza delle estensioni dei tag e della relativa modalità di installazione nelle applicazioni web. Per ulteriori informazioni, consulta la seguente documentazione:

* [Panoramica sui tag](../../../../tags/home.md)
* [Guida rapida](../../../../tags/quick-start/quick-start.md)
* [Panoramica sulla pubblicazione](../../../../tags/ui/publishing/overview.md)

## Configurare un datastream

Affinché l’SDK invii dati ad Experience Platform, devi disporre di un datastream esistente per Platform configurato nell’interfaccia utente di raccolta dati. Inoltre, il [!UICONTROL Set di dati di profilo] selezionato per la configurazione deve contenere campi di consenso standardizzati.

Dopo aver creato una nuova configurazione o aver selezionato una configurazione esistente da modificare, seleziona il pulsante di attivazione accanto a **[!UICONTROL Adobe Experience Platform]**. Quindi, utilizza i valori elencati di seguito per completare il modulo.

![](../../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Campo Datastream | Valore |
| --- | --- |
| [!UICONTROL Sandbox] | Il nome della piattaforma [sandbox](../../../../sandboxes/home.md) che contiene la connessione in streaming e i set di dati richiesti per impostare il datastream. |
| [!UICONTROL Ingresso streaming] | Una connessione in streaming valida, ad Experience Platform. Se non disponi di un&#39;entrata in streaming, consulta l&#39;esercitazione su [creazione di una connessione in streaming](../../../../ingestion/tutorials/create-streaming-connection-ui.md) . |
| [!UICONTROL Set di dati evento] | Un set di dati [!DNL XDM ExperienceEvent] che prevedi di inviare dati evento all’utilizzo dell’SDK. Sebbene sia necessario fornire un set di dati dell’evento per creare un datastream Platform, al momento l’invio diretto dei dati di consenso tramite eventi non è supportato. |
| [!UICONTROL Set di dati del profilo] | Il set di dati abilitato [!DNL Profile] con i campi di consenso dei clienti creati in precedenza. |

Al termine, seleziona **[!UICONTROL Salva]** nella parte inferiore dello schermo e continua a seguire tutte le istruzioni aggiuntive per completare la configurazione.


## Installare e configurare l’SDK per web di Platform

Dopo aver creato un datastream come descritto nella sezione precedente, devi configurare l’estensione Platform Web SDK che distribuirai in ultima analisi sul sito. Se l&#39;estensione SDK non è installata nella proprietà tag, seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra, seguito dalla scheda **[!UICONTROL Catalogo]** . Quindi, seleziona **[!UICONTROL Installa]** sotto l&#39;estensione Platform SDK all&#39;interno dell&#39;elenco delle estensioni disponibili.

![](../../../images/governance-privacy-security/consent/adobe/sdk/install.png)

Durante la configurazione dell&#39;SDK, in **[!UICONTROL Configurazioni bordi]**, seleziona il datastream creato nel passaggio precedente.

![](../../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Seleziona **[!UICONTROL Salva]** per installare l&#39;estensione.

### Creare un elemento dati per impostare il consenso predefinito

Con l&#39;estensione SDK installata, puoi creare un elemento dati che rappresenti il valore predefinito di consenso per la raccolta dati (`collect.val`) per i tuoi utenti. Questo può essere utile se desideri avere valori predefiniti diversi a seconda dell’utente, ad esempio `pending` per gli utenti dell’Unione europea e `in` per gli utenti nordamericani.

In questo caso d’uso, puoi implementare quanto segue per impostare il consenso predefinito in base all’area geografica dell’utente:

1. Determinare la regione dell’utente sul server web.
1. Prima del tag `script` (codice di incorporamento) sulla pagina web, esegui il rendering di un tag `script` separato che imposta una variabile `adobeDefaultConsent` in base all’area dell’utente.
1. Imposta un elemento dati che utilizza la variabile JavaScript `adobeDefaultConsent` e utilizza questo elemento dati come valore di consenso predefinito per l’utente.

Se l&#39;area geografica dell&#39;utente è determinata da una CMP, puoi invece utilizzare i seguenti passaggi:

1. Gestisci l’evento &quot;CMP loaded&quot; sulla pagina.
1. Nel gestore eventi, imposta una variabile `adobeDefaultConsent` basata sull&#39;area dell&#39;utente, quindi carica lo script della libreria di tag utilizzando JavaScript.
1. Imposta un elemento dati che utilizza la variabile JavaScript `adobeDefaultConsent` e utilizza questo elemento dati come valore di consenso predefinito per l’utente.

Per creare un elemento dati nell’interfaccia utente Raccolta dati, seleziona **[!UICONTROL Elementi dati]** nel menu di navigazione a sinistra, quindi seleziona **[!UICONTROL Aggiungi elemento dati]** per accedere alla finestra di dialogo per la creazione dell’elemento dati.

Da qui, devi creare un elemento dati [!UICONTROL JavaScript Variable] basato su `adobeDefaultConsent`. Al termine, seleziona **[!UICONTROL Salva]**.

![](../../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

Una volta creato l&#39;elemento dati, torna alla pagina di configurazione dell&#39;estensione SDK per web. Nella sezione [!UICONTROL Privacy] , seleziona **[!UICONTROL Fornito dall&#39;elemento dati]** e utilizza la finestra di dialogo fornita per selezionare l&#39;elemento dati di consenso predefinito creato in precedenza.

![](../../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Distribuire l&#39;estensione sul sito web

Dopo aver configurato l&#39;estensione, questa può essere integrata nel sito web. Per informazioni dettagliate su come distribuire la build della libreria aggiornata, consulta la [guida alla pubblicazione](https://experienceleague.adobe.com/docs/launch/using/publish/overview.html) nella documentazione sui tag .

## Esecuzione di comandi di modifica del consenso {#commands}

Dopo aver integrato l’estensione SDK nel sito web, puoi iniziare a utilizzare il comando Platform Web SDK `setConsent` per inviare i dati di consenso a Platform.

Esistono due scenari in cui `setConsent` deve essere chiamato sul sito:

1. Quando il consenso viene caricato sulla pagina (in altre parole, a ogni caricamento di pagina)
1. Come parte di un hook CMP o listener di eventi che rileva le modifiche nelle impostazioni di consenso

>[!NOTE]
Per un’introduzione alla sintassi comune per i comandi SDK di Platform, consulta il documento relativo all’ [esecuzione di comandi](../../../../edge/fundamentals/executing-commands.md).

Il comando `setConsent` prevede due argomenti:

1. Una stringa che indica il tipo di comando (in questo caso, `"setConsent"`)
1. Un oggetto payload contenente una singola proprietà di tipo array: `consent`. La matrice `consent` deve contenere almeno un oggetto che fornisca i campi di consenso richiesti per lo standard Adobe.

I campi di consenso richiesti per lo standard di Adobe sono mostrati nella seguente chiamata di esempio `setConsent` :

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
| `standard` | Lo standard di consenso in uso. Per lo standard di Adobe, questo valore deve essere impostato su `Adobe`. |
| `version` | Il numero di versione dello standard di consenso indicato in `standard`. Questo valore deve essere impostato su `2.0` per l’elaborazione del consenso standard di Adobe. |
| `value` | Le informazioni di consenso aggiornate del cliente, fornite come oggetto XDM conforme alla struttura dei campi di consenso del set di dati abilitati per il profilo. |

>[!NOTE]
Se utilizzi altri standard di consenso insieme a `Adobe` (ad esempio `IAB TCF`), puoi aggiungere altri oggetti alla matrice `consent` per ogni standard. Ogni oggetto deve contenere i valori appropriati per `standard`, `version` e `value` per lo standard di consenso che rappresenta.

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

Tutti i comandi [!DNL Platform SDK] restituiscono promesse che indicano se la chiamata è riuscita o meno. Puoi quindi utilizzare queste risposte per ottenere una logica aggiuntiva, ad esempio per visualizzare messaggi di conferma al cliente. Consulta la sezione sulla [gestione del successo o dell&#39;errore](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) nella guida sull&#39;esecuzione dei comandi SDK per esempi specifici.

## Passaggi successivi

Seguendo questa guida, hai configurato l’estensione Platform Web SDK per inviare ad Experience Platform i dati di consenso. Ora puoi tornare alla panoramica di elaborazione del consenso per i passaggi su come [testare l&#39;implementazione](./overview.md#test-implementation).
