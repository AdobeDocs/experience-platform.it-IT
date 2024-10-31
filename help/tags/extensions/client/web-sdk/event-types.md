---
title: Tipi di eventi nell’estensione Adobe Experience Platform Web SDK
description: Scopri come utilizzare i tipi di evento forniti dall’estensione Adobe Experience Platform Web SDK in Adobe Experience Platform Launch.
solution: Experience Platform
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: b37bf09e3ec16f29d6acee3bca71463fa2c876ce
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 0%

---

# Tipi di evento

Questa pagina descrive i tipi di evento Adobe Experience Platform forniti dall’estensione tag Adobe Experience Platform Web SDK. Sono utilizzati per [generare regole](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html?lang=it) e non devono essere confusi con il campo `eventType` nell&#39;oggetto [`xdm`](/help/web-sdk/commands/sendevent/xdm.md).

## Hook di monitoraggio attivato {#monitoring-hook-triggered}

Adobe Experience Platform Web SDK include hook di monitoraggio utilizzabili per monitorare vari eventi di sistema. Questi strumenti sono utili per sviluppare strumenti di debug personalizzati e per acquisire i registri dell’SDK web.

Per informazioni complete sui parametri contenuti da ogni evento hook di monitoraggio, consulta la [documentazione sugli hook di monitoraggio dell&#39;SDK Web](../../../../web-sdk/monitoring-hooks.md).

![Tag dell&#39;immagine dell&#39;interfaccia utente che mostra il tipo di evento hook di monitoraggio](assets/monitoring-hook-triggered.png)

L’estensione tag Web SDK supporta i seguenti hook di monitoraggio:

* **[!UICONTROL onInstanceCreated]**: questo evento hook di monitoraggio viene attivato quando si crea una nuova istanza Web SDK.
* **[!UICONTROL onInstanceConfigured]**: questo evento hook di monitoraggio viene attivato dall&#39;SDK Web quando il comando [`configure`](../../../../web-sdk/commands/configure/overview.md) è stato risolto
* **[!UICONTROL onBeforeCommand]**: questo evento hook di monitoraggio viene attivato da Web SDK prima dell&#39;esecuzione di qualsiasi altro comando. Puoi utilizzare questo hook di monitoraggio per recuperare le opzioni di configurazione di un comando specifico.
* **[!UICONTROL onCommandResolved]**: questo evento hook di monitoraggio viene attivato prima della risoluzione della promessa di comando. È possibile utilizzare questa funzione per visualizzare le opzioni e i risultati del comando.
* **[!UICONTROL onCommandRejected]**: questo evento hook di monitoraggio viene attivato quando una promessa di comando viene rifiutata e contiene informazioni sulla causa dell&#39;errore.
* **[!UICONTROL onBeforeNetworkRequest]**: questo evento hook di monitoraggio viene attivato prima dell&#39;esecuzione di una richiesta di rete.
* **[!UICONTROL onNetworkResponse]**: questo evento hook di monitoraggio viene attivato quando il browser riceve una risposta.
* **[!UICONTROL onNetworkError]**: questo evento di monitoraggio dell&#39;hook viene attivato quando la richiesta di rete non è riuscita.
* **[!UICONTROL onBeforeLog]**: questo evento hook di monitoraggio viene attivato prima che l&#39;SDK Web registri qualsiasi elemento nella console.
* **[!UICONTROL onContentRendering]**: questo evento hook di monitoraggio è attivato dal componente `personalization` e consente di eseguire il debug del rendering del contenuto di personalizzazione. Questo evento può avere stati diversi:
   * `rendering-started`: indica che Web SDK sta per eseguire il rendering delle proposte. Prima che l&#39;SDK Web inizi a eseguire il rendering di un ambito di decisione o di una visualizzazione, nell&#39;oggetto `data` è possibile visualizzare le proposte che stanno per essere sottoposte a rendering dal componente `personalization` e il nome dell&#39;ambito.
   * `no-offers`: indica che non è stato ricevuto alcun payload per i parametri richiesti.
   * `rendering-failed`: indica che Web SDK non è riuscito a eseguire il rendering di una proposta.
   * `rendering-succeeded`: indica che il rendering è stato completato per un ambito di decisione.
   * `rendering-redirect`: indica che Web SDK eseguirà una proposta di reindirizzamento.
* **[!UICONTROL onContentHiding]**: questo evento hook di monitoraggio viene attivato quando viene applicato o rimosso uno stile di pre-hiding.


## [!UICONTROL Invio evento completato]

In genere, la proprietà dispone di una o più regole che utilizzano l&#39;azione [[!UICONTROL Invia evento]](action-types.md#send-event) per inviare eventi all&#39;Edge Network di Adobe Experience Platform. Ogni volta che un evento viene inviato a Edge Network, viene restituita una risposta al browser con dati utili. Senza il tipo di evento [!UICONTROL Invia evento completato], non potrai accedere ai dati restituiti.

Per accedere ai dati restituiti, crea una regola separata, quindi aggiungi un evento [!UICONTROL Invia evento completato] alla regola. Questa regola viene attivata ogni volta che viene ricevuta una risposta dal server a seguito di un&#39;azione [!UICONTROL Invia evento].

Quando un evento [!UICONTROL Invia evento completato] attiva una regola, fornisce i dati restituiti dal server che possono essere utili per eseguire determinate attività. In genere, si aggiunge un&#39;azione [!UICONTROL Codice personalizzato] (dall&#39;estensione [!UICONTROL Core]) alla stessa regola contenente l&#39;evento [!UICONTROL Invia evento completato]. Nell&#39;azione [!UICONTROL Codice personalizzato], il codice personalizzato avrà accesso a una variabile denominata `event`. Questa variabile `event` conterrà i dati restituiti dal server.

La regola per la gestione dei dati restituiti da Edge Network potrebbe essere simile alla seguente:

![](assets/send-event-complete.png)

Di seguito sono riportati alcuni esempi di come eseguire alcune attività utilizzando l&#39;azione [!UICONTROL Codice personalizzato] in questa regola.

### Rendering manuale di contenuti personalizzati

Nell’azione Codice personalizzato, inclusa nella regola per la gestione dei dati di risposta, puoi accedere alle proposte di personalizzazione restituite dal server. A questo scopo, digita il seguente codice personalizzato:

```javascript
var propositions = event.propositions;
```

Se `event.propositions` esiste, si tratta di un array contenente oggetti di proposta di personalizzazione. Le proposte incluse nell’array sono determinate, in gran parte, dal modo in cui l’evento è stato inviato al server.

Per questo primo scenario, si supponga di non aver selezionato la casella di controllo [!UICONTROL Decisioni di rendering] e di non aver fornito alcun [!UICONTROL ambito di decisione] nell&#39;azione [!UICONTROL Invia evento] responsabile dell&#39;invio dell&#39;evento.

![img.png](assets/send-event-render-unchecked-without-scopes.png)

In questo esempio, l&#39;array `propositions` contiene solo proposte relative all&#39;evento idonee per il rendering automatico.

L&#39;array `propositions` potrebbe essere simile a questo esempio:

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  }
]
```

Durante l&#39;invio dell&#39;evento, la casella di controllo [!UICONTROL Decisioni di rendering] non è stata selezionata, pertanto l&#39;SDK non ha tentato di eseguire automaticamente il rendering di alcun contenuto. L’SDK ha comunque recuperato automaticamente i contenuti idonei per il rendering automatico e ti ha fornito come eseguire il rendering manualmente, se lo desideri. Tieni presente che la proprietà `renderAttempted` di ogni oggetto della proposta è impostata su `false`.

Se invece avessi selezionato la casella di controllo [!UICONTROL Decisioni di rendering] durante l&#39;invio dell&#39;evento, l&#39;SDK avrebbe tentato di eseguire il rendering di tutte le proposte idonee per il rendering automatico. Di conseguenza, la proprietà `renderAttempted` di ciascuno degli oggetti della proposta sarà impostata su `true`. In questo caso, non sarebbe necessario eseguire manualmente il rendering di queste proposte.

Finora hai esaminato solo i contenuti di personalizzazione idonei per il rendering automatico (ad esempio, qualsiasi contenuto creato nel Compositore esperienza visivo di Adobe Target). Per recuperare qualsiasi contenuto di personalizzazione _not_ idoneo per il rendering automatico, richiedi il contenuto fornendo ambiti decisionali utilizzando il campo [!UICONTROL Ambiti decisionali] nell&#39;azione [!UICONTROL Invia evento]. Un ambito è una stringa che identifica una particolare proposta che desideri recuperare dal server.

L&#39;azione [!UICONTROL Invia evento] sarà simile alla seguente:

![img.png](assets/send-event-render-unchecked-with-scopes.png)

In questo esempio, se le proposte vengono trovate nel server corrispondente all&#39;ambito `salutation` o `discount`, vengono restituite e incluse nell&#39;array `propositions`. Tieni presente che le proposte idonee per il rendering automatico continueranno a essere incluse nell&#39;array `propositions`, indipendentemente da come configuri i campi [!UICONTROL Decisioni di rendering] o [!UICONTROL Ambiti decisionali] nell&#39;azione [!UICONTROL Invia evento]. L&#39;array `propositions`, in questo caso, sarà simile all&#39;esempio seguente:

```json
[
  {
    "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
    "scope": "salutation",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/json-content-item",
        "data": {
          "id": "4433221",
          "content": {
            "salutation": "Welcome, esteemed visitor!"
          }
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
    "scope": "discount",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "data": {
          "id": "4433222",
          "content": "<div>50% off your order!</div>",
          "format": "text/html"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  }
]
```

A questo punto, puoi eseguire il rendering del contenuto delle proposte come lo ritieni opportuno. In questo esempio, la proposta corrispondente all&#39;ambito `discount` è una proposta HTML creata utilizzando il Compositore esperienza basato su moduli di Adobe Target. Si supponga di disporre di un elemento nella pagina con ID `daily-special` e di voler eseguire il rendering del contenuto della proposta `discount` nell&#39;elemento `daily-special`. Effettua le seguenti operazioni:

1. Estrarre le proposte dall&#39;oggetto `event`.
1. Eseguire un ciclo in ogni proposta, cercando la proposta con un ambito di `discount`.
1. Se trovi una proposta, scorri ciclicamente ogni elemento della proposta, cercando l’elemento che è il contenuto HTML. (È meglio controllare che presumere.)
1. Se trovi un elemento contenente contenuti HTML, individua l&#39;elemento `daily-special` nella pagina e sostituisci il relativo HTML con il contenuto personalizzato.

Il codice personalizzato all&#39;interno dell&#39;azione [!UICONTROL Codice personalizzato] potrebbe essere visualizzato come segue:

```javascript
var propositions = event.propositions;

var discountProposition;
if (propositions) {
  // Find the discount proposition, if it exists.
  for (var i = 0; i < propositions.length; i++) {
    var proposition = propositions[i]; 
    if (proposition.scope === "discount") {
      discountProposition = proposition;
      break;
    }
  }
}

var discountHtml;
if (discountProposition) {
  // Find the item from proposition that should be rendered.
  // Rather than assuming there a single item that has HTML
  // content, find the first item whose schema indicates
  // it contains HTML content.
  for (var j = 0; j < discountProposition.items.length; j++) {
    var discountPropositionItem = discountProposition.items[i]; 
    if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
      discountHtml = discountPropositionItem.data.content;
      break;
    }
  }
}

if (discountHtml) {
  // Discount HTML exists. Time to render it.
  var dailySpecialElement = document.getElementById("daily-special");
  dailySpecialElement.innerHTML = discountHtml;
}
```

### Accesso ai token di risposta di Adobe Target

Il contenuto Personalization restituito da Adobe Target include [token di risposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), ovvero dettagli su attività, offerta, esperienza, profilo utente, informazioni geografiche e altro ancora. Questi dettagli possono essere condivisi con strumenti di terze parti o utilizzati per il debug. I token di risposta possono essere configurati nell’interfaccia utente di Adobe Target.

Nell’azione Codice personalizzato, inclusa nella regola per la gestione dei dati di risposta, puoi accedere alle proposte di personalizzazione restituite dal server. A tale scopo, digita il seguente codice personalizzato:

```javascript
var propositions = event.propositions;
```

Se `event.propositions` esiste, si tratta di un array contenente oggetti di proposta di personalizzazione. Per ulteriori informazioni sul contenuto di `result.propositions`, vedere [Eseguire manualmente il rendering del contenuto personalizzato](#manually-render-personalized-content).

Supponiamo di voler raccogliere tutti i nomi delle attività da tutte le proposte di cui è stato eseguito il rendering automatico dall’SDK web e inviarli in un singolo array. È quindi possibile inviare il singolo array a una terza parte. In questo caso, scrivere il codice personalizzato nell&#39;azione [!UICONTROL Codice personalizzato] in:

1. Estrarre le proposte dall&#39;oggetto `event`.
1. Eseguire un ciclo tra le proposte.
1. Determina se l’SDK ha eseguito il rendering della proposta.
1. In tal caso, scorri ciclicamente ogni elemento della proposta.
1. Recuperare il nome dell&#39;attività dalla proprietà `meta`, che è un oggetto contenente token di risposta.
1. Invia il nome dell’attività a un array.
1. Invia i nomi delle attività a una terza parte.

```javascript
var propositions = event.propositions;
if (propositions) {
  var activityNames = [];
  propositions.forEach(function(proposition) {
    if (proposition.renderAttempted) {
      proposition.items.forEach(function(item) {
        if (item.meta) {
          // item.meta contains the response tokens.
          var activityName = item.meta["activity.name"];
          // Ignore duplicates
          if (activityNames.indexOf(activityName) === -1) {
            activityNames.push(activityName);  
          }
        }
      });
    }
  });
  // Now that activity names are in an array,
  // you can send them to a third party or use
  // them in some other way.
}
```

## [!UICONTROL Sottoscrivi elementi set di regole] {#subscribe-ruleset-items}

Il tipo di evento **[!UICONTROL Sottoscrivi elementi set di regole]** consente di sottoscrivere le schede di contenuto Adobe Journey Optimizer per una superficie. Ogni volta che i set di regole vengono valutati, il callback fornito a questo comando riceve un oggetto risultato con proposte che contengono i dati della scheda di contenuto.

![Immagine dell&#39;interfaccia utente dei tag di Experience Platform che mostra il tipo di evento Sottoscrivi elementi set di regole.](assets/subscribe-ruleset-items.png)

Questo tipo di evento supporta le seguenti proprietà configurabili:

* **[!UICONTROL Schemi]**: un array di schemi per i quali si desidera effettuare la sottoscrizione alle schede di contenuto. Puoi inserire gli schemi manualmente o fornendo un elemento dati.
* **[!UICONTROL Superfici]**: array di superfici per le quali si desidera sottoscrivere schede di contenuto. Potete immettere le superfici manualmente o fornendo un elemento dati.
