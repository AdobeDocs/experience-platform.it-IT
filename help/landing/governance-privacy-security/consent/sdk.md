---
title: Elaborare dati di consenso dei clienti utilizzando Adobe Experience Platform Web SDK
description: Scopri come integrare Adobe Experience Platform Web SDK per elaborare i dati sul consenso dei clienti in Adobe Experience Platform.
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 1%

---

# Integrare Platform Web SDK per elaborare i dati sul consenso dei clienti

Adobe Experience Platform Web SDK consente di recuperare i segnali di consenso del cliente generati dalle piattaforme di gestione del consenso (CMP, Consent Management Platforms) e di inviarli a Adobe Experience Platform ogni volta che si verifica un evento di modifica del consenso.

**L&#39;SDK non si interfaccia con CMP predefiniti**. Sta a te determinare come integrare l’SDK nel tuo sito web, ascoltare le modifiche del consenso nella CMP e chiamare il comando appropriato. Questo documento fornisce indicazioni generali su come integrare la CMP con Platform Web SDK.

## Prerequisiti {#prerequisites}

Questa esercitazione presuppone che tu abbia già determinato come generare i dati sul consenso all’interno della tua CMP e che sia stato creato un set di dati contenente campi di consenso conformi allo standard Adobe o allo standard IAB Transparency and Consent Framework (TCF) 2.0. Se non hai ancora creato questo set di dati, consulta le seguenti esercitazioni prima di tornare a questa guida:

* [Creare un set di dati utilizzando lo standard Adobe](./adobe/dataset.md)
* [Creare un set di dati utilizzando lo standard TCF 2.0](./iab/dataset.md)

Questa guida segue il flusso di lavoro per la configurazione dell’SDK utilizzando l’estensione tag nell’interfaccia utente. Se non desideri utilizzare l&#39;estensione e preferisci incorporare direttamente la versione autonoma dell&#39;SDK sul tuo sito, consulta i seguenti documenti invece di questa guida:

* [Configurare uno stream di dati](/help/datastreams/overview.md)
* [Installare l’SDK](/help/web-sdk/install/overview.md)
* [Configurare l’SDK per i comandi di consenso](/help/web-sdk/commands/configure/defaultconsent.md)

I passaggi di installazione descritti in questa guida richiedono una buona conoscenza delle estensioni tag e del modo in cui vengono installate nelle applicazioni web. Per ulteriori informazioni, consulta la seguente documentazione:

* [Panoramica sui tag](/help/tags/home.md)
* [Guida rapida](/help/tags/quick-start/quick-start.md)
* [Panoramica sulla pubblicazione](/help/tags/ui/publishing/overview.md)

## Configurare un flusso di dati

Affinché l’SDK possa inviare dati ad Experience Platform, devi prima configurare uno stream di dati. Nell&#39;interfaccia utente di Data Collection o Experience Platform, seleziona **[!UICONTROL Datastreams]** nell&#39;area di navigazione a sinistra.

Dopo aver creato un nuovo flusso di dati o averne selezionato uno esistente da modificare, seleziona il pulsante di attivazione/disattivazione accanto a **[!UICONTROL Adobe Experience Platform]**. Quindi, utilizzare i valori elencati di seguito per completare il modulo.

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Campo stream di dati | Valore |
| --- | --- |
| [!UICONTROL Sandbox] | Il nome della piattaforma [sandbox](../../../sandboxes/home.md) che contiene la connessione streaming e i set di dati necessari per impostare lo stream di dati. |
| [!UICONTROL Set di dati di evento] | Un set di dati [!DNL XDM ExperienceEvent] che intendi inviare a utilizzando l&#39;SDK. Anche se devi fornire un set di dati evento per creare un flusso di dati di Platform, tieni presente che i dati del consenso inviati tramite eventi non vengono rispettati nei flussi di lavoro di applicazione a valle. |
| [!UICONTROL Set di dati di profilo] | Il set di dati abilitato per [!DNL Profile] con campi di consenso del cliente creato [prima](#prerequisites). |

Al termine, seleziona **[!UICONTROL Salva]** nella parte inferiore della schermata e continua seguendo eventuali altre richieste per completare la configurazione.

## Installare e configurare Platform Web SDK

Dopo aver creato un flusso di dati come descritto nella sezione precedente, devi configurare l’estensione Platform Web SDK che infine distribuirai sul sito. Se l&#39;estensione SDK non è installata nella proprietà tag, seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra, seguito dalla scheda **[!UICONTROL Catalogo]**. Quindi, seleziona **[!UICONTROL Installa]** nell&#39;estensione Platform SDK all&#39;interno dell&#39;elenco delle estensioni disponibili.

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

Durante la configurazione dell&#39;SDK, in **[!UICONTROL Configurazioni Edge]**, seleziona lo stream di dati creato nel passaggio precedente.

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Seleziona **[!UICONTROL Salva]** per installare l&#39;estensione.

### Creare un elemento dati per impostare il consenso predefinito

Con l&#39;estensione SDK installata, puoi creare un elemento dati che rappresenti il valore di consenso predefinito per la raccolta dati (`collect.val`) per i tuoi utenti. Questo può essere utile se si desidera avere valori predefiniti diversi a seconda dell&#39;utente, ad esempio `pending` per gli utenti dell&#39;Unione Europea e `in` per gli utenti nordamericani.

In questo caso d’uso, puoi implementare quanto segue per impostare il consenso predefinito in base all’area geografica dell’utente:

1. Determina l’area geografica dell’utente sul server web.
1. Prima del tag `script` (codice di incorporamento) nella pagina Web, esegui il rendering di un tag `script` separato che imposta una variabile `adobeDefaultConsent` in base all&#39;area geografica dell&#39;utente.
1. Configurare un elemento dati che utilizza la variabile JavaScript `adobeDefaultConsent` e utilizzare questo elemento dati come valore di consenso predefinito per l&#39;utente.

Se l’area geografica dell’utente è determinata da una CMP, puoi utilizzare i seguenti passaggi:

1. Gestisci l’evento &quot;CMP caricato&quot; sulla pagina.
1. Nel gestore eventi impostare una variabile `adobeDefaultConsent` in base all&#39;area dell&#39;utente, quindi caricare lo script della libreria di tag utilizzando JavaScript.
1. Configurare un elemento dati che utilizza la variabile JavaScript `adobeDefaultConsent` e utilizzare questo elemento dati come valore di consenso predefinito per l&#39;utente.

Per creare un elemento dati nell&#39;interfaccia utente, seleziona **[!UICONTROL Elementi dati]** nell&#39;area di navigazione a sinistra, quindi seleziona **[!UICONTROL Aggiungi elemento dati]** per accedere alla finestra di dialogo di creazione dell&#39;elemento dati.

Da qui è necessario creare un elemento dati [!UICONTROL Variabile JavaScript] basato su `adobeDefaultConsent`. Al termine, seleziona **[!UICONTROL Salva]**.

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

Una volta creato l’elemento dati, torna alla pagina di configurazione dell’estensione Web SDK. Nella sezione [!UICONTROL Privacy], seleziona **[!UICONTROL Fornito dall&#39;elemento dati]**, quindi utilizza la finestra di dialogo fornita per selezionare l&#39;elemento dati di consenso predefinito creato in precedenza.

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Distribuire l’estensione sul sito web

Una volta completata la configurazione dell&#39;estensione, puoi integrarla nel sito web. Per informazioni dettagliate su come distribuire la build della libreria aggiornata, consulta la [guida alla pubblicazione](../../../tags/ui/publishing/overview.md) nella documentazione dei tag.

## Esecuzione di comandi per la modifica del consenso {#commands}

Dopo aver integrato l’estensione SDK nel sito web, puoi iniziare a utilizzare il comando Platform Web SDK `setConsent` per inviare i dati sul consenso a Platform.

Il comando `setConsent` esegue due azioni:

1. Aggiorna gli attributi del profilo dell&#39;utente direttamente nell&#39;archivio Profili. Questo non invia alcun dato al data lake.
1. Crea un [evento esperienza](../../../xdm/classes/experienceevent.md) che registra un account con marca temporale dell&#39;evento di modifica del consenso. Questi dati vengono inviati direttamente al data lake e possono essere utilizzati per tenere traccia delle modifiche delle preferenze di consenso nel tempo.

### Quando chiamare `setConsent`

Esistono due scenari in cui `setConsent` deve essere chiamato sul sito:

1. Quando il consenso viene caricato sulla pagina (in altre parole, a ogni caricamento di pagina)
1. Come parte di un hook CMP o di un listener di eventi che rileva le modifiche nelle impostazioni di consenso

### Sintassi `setConsent`

Il comando [`setConsent`](/help/web-sdk/commands/setconsent.md) prevede un oggetto payload contenente una singola proprietà di tipo array: `consent`. L&#39;array `consent` deve contenere almeno un oggetto che fornisca i campi di consenso richiesti per lo standard Adobe.

I campi di consenso richiesti per lo standard Adobe sono mostrati nella seguente chiamata di esempio `setConsent`:

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
        time: "YYYY-10-12T15:52:25+00:00"
      }
    }
  }]
});
```

| Payload, proprietà | Descrizione |
| --- | --- |
| `standard` | Lo standard di consenso utilizzato. Per lo standard Adobe, questo valore deve essere impostato su `Adobe`. |
| `version` | Il numero di versione dello standard di consenso indicato in `standard`. Questo valore deve essere impostato su `2.0` per l&#39;elaborazione del consenso secondo lo standard Adobe. |
| `value` | Le informazioni di consenso aggiornate del cliente, fornite come oggetto XDM conforme alla struttura dei campi di consenso del set di dati abilitati per il profilo. |

>[!NOTE]
>
>Se si utilizzano altri standard di consenso insieme a `Adobe` (ad esempio `IAB TCF`), è possibile aggiungere altri oggetti all&#39;array `consent` per ogni standard. Ogni oggetto deve contenere valori appropriati per `standard`, `version` e `value` per lo standard di consenso che rappresenta.

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

Tutti i comandi [!DNL Platform SDK] restituiscono promesse che indicano se la chiamata è riuscita o meno. Puoi quindi utilizzare queste risposte per una logica aggiuntiva, ad esempio per visualizzare i messaggi di conferma al cliente. Per ulteriori informazioni, vedere [Risposte ai comandi](/help/web-sdk/commands/command-responses.md).

Dopo aver effettuato correttamente `setConsent` chiamate con l&#39;SDK, puoi utilizzare il visualizzatore di profili nell&#39;interfaccia utente di Platform per verificare se i dati vengono inviati nell&#39;archivio profili. Per ulteriori informazioni, consulta la sezione su [esplorazione dei profili per identità](../../../profile/ui/user-guide.md#browse-identity).

## Passaggi successivi

Seguendo questa guida, hai configurato l’estensione Platform Web SDK per inviare i dati sul consenso ad Experience Platform. Per informazioni su come testare l’implementazione, consulta la documentazione dello standard di consenso che stai implementando:

* [Standard Adobe](./adobe/overview.md#test)
* [Standard TCF 2.0](./iab/overview.md#test)
