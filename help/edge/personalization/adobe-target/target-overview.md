---
title: Utilizzare Adobe Target con Web SDK per la personalizzazione
description: Scopri come eseguire il rendering di contenuti personalizzati con Experienci Platform Web SDK utilizzando Adobe Target
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 5%

---


# Utilizzare [!DNL Adobe Target] e [!DNL Web SDK] per la personalizzazione

[!DNL Adobe Experience Platform] [!DNL Web SDK] può distribuire ed eseguire il rendering di esperienze personalizzate gestite in [!DNL Adobe Target] al canale web. È possibile utilizzare un editor WYSIWYG, denominato [Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) o un&#39;interfaccia non visiva, il [Compositore esperienza basato su moduli](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), per creare, attivare e distribuire le attività e le esperienze di personalizzazione.

>[!IMPORTANT]
>
>Scopri come migrare l’implementazione di Target a Platform Web SDK con [Migrare Target da at.js 2.x a Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=it) esercitazione.
>
>Scopri come implementare Target per la prima volta con [Implementare Adobe Experience Cloud con Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=it) esercitazione. Per informazioni specifiche su Target, consulta la sezione del tutorial intitolata [Configurare Target con Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).


Le seguenti funzioni sono state testate e sono attualmente supportate in [!DNL Target]:

* [Test A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [Generazione di rapporti su impressioni e conversione per A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=it)
* [Attività di Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Attività Targeting esperienza](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Test multivariati (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Attività Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [Generazione di rapporti sulle impression e le conversioni del Target nativo](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [Supporto VEC](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Web SDK] schema di sistema

Il diagramma seguente consente di comprendere il flusso di lavoro di [!DNL Target] e [!DNL Web SDK] decisioni edge.

![Diagramma di Adobe Target Edge Decisioning con Platform Web SDK](./assets/target-platform-web-sdk.png)

| Chiamata | Dettagli |
| --- | --- |
| 1 | Il dispositivo carica [!DNL Web SDK]. Il [!DNL Web SDK] invia una richiesta alla rete Edge con dati XDM, l’ID ambiente Datastreams, i parametri immessi e l’ID cliente (facoltativo). La pagina (o i contenitori) è pre-nascosta. |
| 2 | La rete Edge invia la richiesta ai servizi Edge di per arricchirla con l’ID visitatore, il consenso e altre informazioni contestuali sul visitatore, come la geolocalizzazione e i nomi descrittivi dei dispositivi. |
| 3 | La rete Edge invia la richiesta di personalizzazione arricchita al [!DNL Target] Edge con l&#39;ID visitatore e i parametri immessi. |
| 4 | Gli script di profilo vengono eseguiti e quindi inseriti in [!DNL Target] archiviazione profilo. L’archiviazione del profilo recupera i segmenti da [!UICONTROL Libreria tipi di pubblico] (ad esempio, segmenti condivisi da [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], il [!DNL Adobe Experience Platform]). |
| 5 | In base ai parametri di richiesta dell’URL e ai dati di profilo, [!DNL Target] determina le attività ed esperienze da visualizzare per il visitatore per la visualizzazione della pagina corrente e per le visualizzazioni preacquisite future. [!DNL Target] quindi lo invia nuovamente alla rete edge. |
| 6 | a. La rete Edge invia nuovamente la risposta di personalizzazione alla pagina, includendo facoltativamente i valori di profilo per ulteriore personalizzazione. Il contenuto personalizzato nella pagina corrente viene mostrato il più rapidamente possibile senza che venga visualizzato momentaneamente il contenuto predefinito.<br>b. Il contenuto personalizzato per le viste mostrate come risultato delle azioni dell’utente in un’applicazione a pagina singola (SPA) viene memorizzato nella cache in modo da applicarlo immediatamente senza una chiamata al server aggiuntiva quando si attivano le viste. <br>. Edge Network invia l’ID visitatore e altri valori nei cookie, come consenso, ID sessione, identità, controllo cookie, personalizzazione. |
| 7 | La rete Edge avanza [!UICONTROL Analytics for Target] (A4T) dettagli (attività, esperienza e metadati di conversione) su [!DNL Analytics] Edge. |

## Abilitazione [!DNL Adobe Target]

Per abilitare [!DNL Target], eseguire le operazioni seguenti:

1. Abilita [!DNL Target] nel tuo [flusso di dati](../../../datastreams/overview.md) con il codice cliente appropriato.
1. Aggiungi il `renderDecisions` agli eventi.

Quindi, facoltativamente, puoi anche aggiungere le seguenti opzioni:

* **`decisionScopes`**: recupera attività specifiche (utili per le attività create con il compositore basato su moduli) aggiungendo questa opzione agli eventi.
* **[Frammento pre-hiding](../manage-flicker.md)**: nasconde solo alcune parti della pagina.

## Utilizzo di Adobe Target VEC

Per utilizzare il Compositore esperienza visivo con [!DNL Web SDK] implementazione, installazione e attivazione di [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) o [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) Estensione VEC Helper.

Per ulteriori informazioni, consulta [Estensione Helper per Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) nel *Guida di Adobe Target*.

## Rendering di contenuti personalizzati

Consulta [Rendering del contenuto di personalizzazione](../rendering-personalization-content.md) per ulteriori informazioni.

## Pubblico in XDM

Quando definisci i tipi di pubblico per [!DNL Target] attività consegnate tramite [!DNL Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=it) devono essere definiti e utilizzati. Dopo aver definito schemi, classi e gruppi di campi schema XDM, puoi creare un’ [!DNL Target] regola di pubblico definita dai dati XDM per il targeting. Entro [!DNL Target], i dati XDM vengono visualizzati nel [!UICONTROL Audience Builder] come parametro personalizzato. XDM viene serializzato utilizzando la notazione del punto (ad esempio, `web.webPageDetails.name`).

Se è stato [!DNL Target] Le attività con tipi di pubblico predefiniti che utilizzano parametri personalizzati o un profilo utente non vengono consegnate correttamente tramite l’SDK. Invece di utilizzare parametri personalizzati o il profilo utente, devi utilizzare XDM. Tuttavia, sono presenti campi di targeting del pubblico predefiniti supportati tramite [!DNL Web SDK] che non richiedono XDM. Questi campi sono disponibili nel [!DNL Target] Interfaccia utente che non richiede XDM:

* Libreria di Target
* Geo
* Rete
* Sistema operativo
* Pagine del sito
* Browser
* Origini di traffico
* Arco temporale

Per ulteriori informazioni, consulta [Categorie di pubblico](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html) nel *Guida di Adobe Target*.

### Token di risposta

I token di risposta vengono utilizzati per inviare metadati a terze parti come Google o Facebook. I token di risposta vengono restituiti nel `meta` campo entro `propositions` -> `items`. Ecco un esempio:

```json
{
  "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI2NzM2IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
  "scope": "__view__",
  "scopeDetails": ...,
  "renderAttempted": true,
  "items": [
    {
      "id": "0",
      "schema": "https://ns.adobe.com/personalization/dom-action",
      "meta": {
        "experience.id": "0",
        "activity.id": "126736",
        "offer.name": "Default Content",
        "offer.id": "0"
      }
    }
  ]
}
```

Per raccogliere i token di risposta, devi abbonarti a `alloy.sendEvent` prometti, ripeti `propositions`ed estrarre i dettagli da `items` -> `meta`.

Ogni `proposition` ha un `renderAttempted` campo booleano che indica se `proposition` è stato sottoposto o meno a rendering. Vedi l’esempio seguente:

```js
alloy("sendEvent",
  {
    renderDecisions: true,
    decisionScopes: [
      "hero-container"
    ]
  }).then(result => {
    const { propositions } = result;

    // filter rendered propositions
    const renderedPropositions = propositions.filter(proposition => proposition.renderAttempted === true);

    // collect the item metadata that represents the response tokens
    const collectMetaData = (items) => {
      return items.filter(item => item.meta !== undefined).map(item => item.meta);
    }

    const pageLoadResponseTokens = renderedPropositions
      .map(proposition => collectMetaData(proposition.items))
      .filter(e => e.length > 0)
      .flatMap(e => e);
  });
  
```

Quando è abilitato il rendering automatico, l’array delle proposte contiene:

#### Al caricamento della pagina:

* Basato su Compositore basato su modulo `propositions` con `renderAttempted` flag impostato su `false`
* Proposte basate sul Compositore esperienza visivo con `renderAttempted` flag impostato su `true`
* Proposte basate sul Compositore esperienza visivo per una visualizzazione di applicazioni a pagina singola con `renderAttempted` flag impostato su `true`

#### Alla visualizzazione - modifica (per le viste memorizzate nella cache):

* Proposte basate sul Compositore esperienza visivo per una visualizzazione di applicazioni a pagina singola con `renderAttempted` flag impostato su `true`

Quando il rendering automatico è disattivato, l’array delle proposte contiene:

#### Al caricamento della pagina:

* [!DNL Form-based Composer]basato su `propositions` con `renderAttempted` flag impostato su `false`
* [!DNL Visual Experience Composer]proposte basate su `renderAttempted` flag impostato su `false`
* [!DNL Visual Experience Composer]Proposte basate su per una visualizzazione Applicazione a pagina singola con `renderAttempted` flag impostato su `false`

#### Alla visualizzazione - modifica (per le viste memorizzate nella cache):

* Proposte basate sul Compositore esperienza visivo per una visualizzazione di applicazioni a pagina singola con `renderAttempted` flag impostato su `false`

### Aggiornamento di profilo singolo

Il [!DNL Web SDK] consente di aggiornare il profilo a [!DNL Target] profilo e al [!DNL Web SDK] come evento esperienza.

Per aggiornare un [!DNL Target] profilo, assicurati che i dati del profilo vengano passati con quanto segue:

* Sotto `"data {"`
* Sotto `"__adobe.target"`
* Prefisso `"profile."`

| Chiave | Tipo | Descrizione |
| --- | --- | --- |
| `renderDecisions` | Booleano | Indica al componente di personalizzazione se deve interpretare le azioni DOM |
| `decisionScopes` | Array `<String>` | Un elenco di ambiti per cui recuperare le decisioni |
| `xdm` | Oggetto | Dati formattati in XDM che arrivano in Web SDK come evento esperienza |
| `data` | Oggetto | Coppie chiave/valore arbitrarie inviate a [!DNL Target] soluzioni della classe target. |

Tipico [!DNL Web SDK] il codice che utilizza questo comando si presenta come segue:

**`sendEvent`con dati profilo**

```js
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**Come inviare attributi di profilo ad Adobe Target:**

```js
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Richiedi consigli

Nella tabella seguente sono elencati [!DNL Recommendations] e se ciascuno di essi è supportato tramite [!DNL Web SDK]:

| Categoria | Attributo | Stato del supporto |
| --- | --- | --- |
| Recommendations - Attributi di entità predefiniti | entity.id | Supportati |
|  | entity.name | Supportati |
|  | entity.categoryId | Supportati |
|  | entity.pageUrl | Supportati |
|  | entity.thumbnailUrl | Supportati |
|  | entity.message | Supportati |
|  | entity.value | Supportati |
|  | entity.inventory | Supportati |
|  | entity.brand | Supportati |
|  | entity.margin | Supportati |
|  | entity.event.detailsOnly | Supportati |
| Recommendations - Attributi di entità personalizzati | entity.yourCustomAttributeName | Supportati |
| Recommendations - Parametri mbox/pagina riservati | excludedIds | Supportati |
|  | cartIds | Supportati |
|  | productPurchasedId | Supportati |
| Pagina o categoria di elementi per affinità tra categorie | user.categoryId | Supportati |

**Come inviare attributi Recommendations ad Adobe Target:**

```js
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## Debugging

mboxTrace e mboxDebug sono stati dichiarati obsoleti. Utilizzare [[!DNL Web SDK] debug](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html).

## Terminologia

__Proposte:__ In entrata [!DNL Adobe Target], le proposte sono correlate all’esperienza selezionata da un’attività.

__Schema:__ Lo schema di una decisione è il tipo di offerta in [!DNL Adobe Target].

__Ambito:__ Il campo di applicazione della decisione. In entrata [!DNL Adobe Target], l&#39;ambito è il mBox. Il mBox globale è il `__view__` ambito.

__XDM:__ XDM viene serializzato in notazione con punto e quindi inserito in [!DNL Adobe Target] come parametri mBox.
