---
title: personalizzazione
description: Esegui il rendering di contenuti diversi a utenti diversi, creando un’esperienza personalizzata per loro.
exl-id: 4bd370c8-8d8d-469e-9666-b5b6d0e3a660
source-git-commit: 54cd49bc1e6f23e3fb6d539274ea16d36ea21386
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---

# `personalization`

L&#39;oggetto `personalization` configura le decisioni di personalizzazione (offerte o proposte) richieste e il modo in cui vengono gestite nella richiesta e nella risposta. È particolarmente utile nelle implementazioni di Adobe Target o Adobe Journey Optimizer, in quanto è la forza motrice che consente di personalizzare il contenuto visualizzato per utente.

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["hero-banner"],
    surfaces: ["web://example.com"],
    schemas: ["https://ns.adobe.com/personalization/dom-action"],
    sendDisplayEvent: true,
    sendDisplayNotifications: true,
    includePendingDisplayNotifications: true,
    defaultPersonalizationEnabled: false
  },
  renderDecisions: true,
  xdm: adobeDataLayer.getState(reference)
});
```

L&#39;oggetto `personalization` contiene le proprietà seguenti:

## `personalization.decisionScopes`

La proprietà `decisionScopes` è un array di stringhe che indica al Web SDK di recuperare e restituire le decisioni di personalizzazione. Ogni elemento dell’array identifica una posizione, un contesto o un posizionamento logico in cui desideri contenuti personalizzati.

Questa proprietà è utile quando desideri recuperare in modo esplicito contenuti personalizzati per aree o componenti specifici di una pagina. È particolarmente utile nelle applicazioni a pagina singola che potrebbero richiedere set diversi di offerte quando l’utente cambia la navigazione o la visualizzazione. Puoi inoltre utilizzare questa proprietà per ottimizzare le prestazioni recuperando solo le offerte per gli elementi dell’interfaccia utente rilevanti per l’utente.

```js
personalization: {
  decisionScopes: ["hero-banner", "cart-offer"]
}
```

In Adobe Target, ogni ambito decisionale è associato a una mbox o a un’attività. In Adobe Journey Optimizer, ogni ambito decisionale è associato a posizionamenti o campagne di contenuti web basati su decisioni. In Offer Decisioning, gli ambiti decisionali corrispondono a quali offerte o proposte deve ricevere il visitatore.

>[!TIP]
>
>Se si desidera richiedere o bloccare l&#39;ambito globale, utilizzare [`defaultPersonalizationEnabled`](#personalizationdefaultpersonalizationenabled) anziché specificarlo qui in `decisionScopes`.

## `personalization.surfaces`

La proprietà `surfaces` è una matrice di [stringhe URI di superficie](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/channels/code-based-experience/configure-code-based-channel/code-based-surface#surface-uri) che definiscono manualmente il canale, il dispositivo o il contesto da cui è richiesta la personalizzazione. Consentono di distinguere tra diverse esperienze digitali, come domini, app o piattaforme di dispositivi all’interno dell’ecosistema cross-channel. Per impostazione predefinita, la libreria deduce la superficie predefinita dalla pagina corrente. È possibile utilizzare questa proprietà per sostituire la superficie derivata automaticamente per la pagina corrente.

Questa proprietà è utile quando desideri utilizzare la personalizzazione tra canali e deve distinguere il funzionamento della personalizzazione tra canali separati. Consente di creare offerte distinte per siti diversi nella stessa organizzazione Adobe Experience Platform.

```js
personalization: {
  surfaces: ["web://example.com", "web://support.example.com/contact"]
}
```

Questa proprietà è utilizzata in modo fondamentale con Adobe Journey Optimizer, in quanto corrisponde alle superfici impostate nelle campagne Journey Optimizer e nella gestione delle superfici.

## `personalization.schemas`

La proprietà `schemas` è un array di stringhe URI di schema che filtrano i tipi di contenuto di personalizzazione richiesti da Edge Network. L’impostazione di questa proprietà limita la risposta ricevuta da Adobe all’inclusione di offerte che corrispondono alle definizioni dei tipi di contenuto specificate. Se omesso, la libreria richiede offerte di tutti gli schemi disponibili per gli ambiti o le superfici corrispondenti.

Questa proprietà consente di ottimizzare la dimensione della risposta e assicura che il sito web o l’applicazione ricevano solo i tipi di offerta che possono essere gestiti. È utile anche con applicazioni a pagina singola che eseguono il rendering del contenuto personalizzato in un modo specifico, ad esempio utilizzando solo azioni DOM o solo oggetti JSON.

```js
personalization: {
  schemas: [
    "https://ns.adobe.com/personalization/dom-action",
    "https://ns.adobe.com/personalization/html-content-item"
  ]
}
```

Sono supportati i seguenti URI di schema:

* **`https://ns.adobe.com/personalization/dom-action`**: offerte che sono azioni DOM dirette, in genere generate dal Compositore esperienza visivo in Adobe Target. Contengono istruzioni per manipolare automaticamente gli elementi sulla pagina senza codice aggiuntivo. È lo standard per la personalizzazione web con rendering automatico.
* **`https://ns.adobe.com/personalization/html-content-item`**: offerte che contengono HTML non elaborati consegnate come stringa. L’implementazione in genere inserisce questo contenuto nella posizione desiderata sulla pagina, fornendo un maggiore controllo rispetto alle azioni DOM. Generalmente utilizzato per banner, snippet o contenuti modali.
* **`https://ns.adobe.com/personalization/json-content-item`**: offerte formattate come oggetto JSON. Più comunemente utilizzato nelle implementazioni basate su API o nei front-end che prevedono dati strutturati invece di modifiche HTML o DOM.
* **`https://ns.adobe.com/personalization/redirect-item`**: offerte che reindirizzano a un URL diverso. Utilizzato per portare l’utente a una nuova pagina basata su targeting o logica decisionale, ad esempio pagine di destinazione o flussi di onboarding.
* **`https://ns.adobe.com/personalization/ruleset-item`**: fornisce un blocco di logica di business per alimentare un motore di regole lato client. Contiene un set di regole con controllo delle versioni che definisce condizioni logiche e conseguenze (logica di personalizzazione if/then).
* **`https://ns.adobe.com/personalization/message/in-app`**: offerte formattate in modo specifico per i messaggi in-app di Adobe Journey Optimizer, in genere riprodotte come modali, banner, popup o sovrapposizioni.
* **`https://ns.adobe.com/personalization/message/content-card`**: offerte formattate in modo specifico per le schede di contenuto Adobe Journey Optimizer, progettate per feed persistenti o in stile casella in entrata nelle app Web o mobili.
* **`https://ns.adobe.com/personalization/message/native-alert`**: offerte formattate specificamente per gli avvisi nativi di Adobe Journey Optimizer, che attivano le finestre di dialogo delle notifiche native per la piattaforma.
* **`https://ns.adobe.com/personalization/measurement`**: utilizzato per tenere traccia di clic e interazioni su offerte personalizzate. Non contiene contenuto di cui è possibile eseguire il rendering.
* **`https://ns.adobe.com/personalization/eventHistoryOperation`**: schema per la modifica della cronologia degli eventi di un visitatore nell&#39;archivio locale. Utilizzato internamente dagli SDK per tenere traccia delle esperienze consegnate o bloccate. Non contiene contenuto di cui è possibile eseguire il rendering.
* **`https://ns.adobe.com/personalization/default-content-item`**: fallback o contenuto predefinito, in genere quando non è idonea alcuna offerta personalizzata. In questo modo, gli utenti non qualificati possono continuare a ricevere contenuti, mantenendo l’esperienza coerente.

## `personalization.sendDisplayEvent`

La proprietà `sendDisplayEvent` è un valore booleano che determina se un evento di notifica della visualizzazione viene inviato automaticamente all&#39;Edge Network subito dopo il rendering del contenuto personalizzato sulla pagina. Se omesso, il valore predefinito è `true`. Imposta questa variabile su `false` se non vuoi indicare che è stato eseguito il rendering del contenuto personalizzato per il tracciamento delle impression.

Il caso d&#39;uso più comune per l&#39;impostazione di questa variabile su `false` si verifica quando si prevede di inviare un altro comando in un&#39;altra posizione nell&#39;implementazione che contrassegna un evento di visualizzazione. Alcune implementazioni hanno sia eventi impression che eventi Analytics; questa proprietà ti offre il controllo completo su quali `sendEvent` comandi incrementano le impression.

```js
personalization: {
  sendDisplayEvent: true
}
```

>[!NOTE]
>
>Le versioni precedenti di Web SDK (versioni 2.12.0 e precedenti) utilizzano invece `sendDisplayNotifications`.

## `personalization.includePendingDisplayNotifications`

La proprietà `includePendingDisplayNotifications` è un valore booleano che controlla se le notifiche di visualizzazione in sospeso sono raggruppate nella chiamata `sendEvent` corrente. Le notifiche di visualizzazione in sospeso rappresentano impression per contenuti personalizzati di cui è stato eseguito il rendering, ma che non sono ancora stati segnalati ad Edge Network come evento di visualizzazione. Questa proprietà è utile quando si utilizzano applicazioni a pagina singola, in quanto il rendering del contenuto personalizzato e le chiamate `sendEvent` potrebbero essere asincrone l&#39;una rispetto all&#39;altra.

Il valore predefinito per questa proprietà è `false`. Impostare questa proprietà su `true` se si desidera eseguire il batch e il flushing di tutte le notifiche di visualizzazione in sospeso in modo che le relative impression vengano registrate con precisione. In genere, per l’implementazione sincrona, come i siti web tradizionali, non è necessario impostare questa proprietà.

```js
personalization: {
  includePendingDisplayNotifications: true
}
```

## `personalization.defaultPersonalizationEnabled`

La proprietà `defaultPersonalizationEnabled` è un valore booleano che consente di controllare in modo esplicito il modo in cui il Web SDK richiede l&#39;ambito di personalizzazione predefinito a livello di pagina (`__view__`) e la superficie per questo comando `sendEvent`. Per impostazione predefinita, al primo comando `sendEvent` dopo il caricamento di una pagina, Web SDK richiede offerte per l&#39;ambito di personalizzazione predefinito a livello di pagina e le superfici associate. I comandi `sendEvent` successivi non richiedono la personalizzazione predefinita. È possibile utilizzare questa proprietà per ignorare tale comportamento. È utile nelle implementazioni di applicazioni a pagina singola, dove potresti voler richiedere nuovamente la personalizzazione predefinita mentre l’utente naviga nel tuo sito. È inoltre possibile utilizzare questa proprietà quando si desidera _solo_ inviare un evento di visualizzazione senza duplicare il recupero delle offerte.

```js
personalization: {
  defaultPersonalizationEnabled: false
}
```

Questa proprietà utilizza la logica seguente a seconda di come viene impostata:

* **Non impostato**: richiede la personalizzazione predefinita quando non è ancora stata richiesta. La personalizzazione predefinita viene in genere richiesta nei primi `sendEvent` dopo il caricamento di una pagina, quindi non viene più richiesta nelle chiamate `sendEvent` successive sulla stessa pagina. L&#39;impostazione di questa proprietà ha la precedenza su questo comportamento.
* **`true`**: richiede esplicitamente l&#39;ambito della pagina e la superficie predefinita, anche se questo comando `sendEvent` non è il primo dopo il caricamento di una pagina. I momenti ideali per impostare questa proprietà su `true` sono quelli in cui è necessario forzare una richiesta di personalizzazione predefinita, ad esempio in scenari di applicazioni a pagina singola.
* **`false`**: soppressione esplicita della richiesta per l&#39;ambito pagina e la superficie predefinita, anche se questo comando `sendEvent` è il primo dopo il caricamento di una pagina. I momenti ideali per impostare questa proprietà su `false` sono quelli in cui si desidera che un determinato comando `sendEvent` non richieda nuove offerte, ma invii semplicemente i dati ad Analytics o invii un evento di visualizzazione.

## Componenti Personalization tramite l’estensione tag Web SDK

L&#39;equivalente dell&#39;estensione tag Web SDK di questa proprietà è la sezione [**[!UICONTROL Personalization]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields) durante la configurazione di un&#39;azione &#39;[!UICONTROL Send event]&#39;.
