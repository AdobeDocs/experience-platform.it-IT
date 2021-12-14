---
title: Utilizzo di Adobe Target con Platform Web SDK
description: Scopri come eseguire il rendering di contenuti personalizzati con Experience Platform Web SDK tramite Adobe Target
keywords: target;adobe target;activity.id;experience.id;renderdecisions;decisionScopes;pre-hiding snippet;vec;Compositore esperienza basato su moduli;xdm;tipi di pubblico;decisioni;ambito;schema;diagramma di sistema;diagramma
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 4%

---

# Utilizzo [!DNL Adobe Target] con [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] può fornire ed eseguire il rendering di esperienze personalizzate gestite in [!DNL Adobe Target] al canale web. È possibile utilizzare un editor WYSIWYG, denominato [Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (Compositore esperienza visivo), o un’interfaccia non visiva, la [Compositore esperienza basato su moduli](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), per creare, attivare e distribuire le tue attività e esperienze di personalizzazione.

>[!IMPORTANT]
>
>La [Documentazione di Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/aep-implementation/aep-web-sdk.html?lang=en) include argomenti contenenti informazioni specifiche sull’SDK per web di Platform in relazione alle funzioni e alle funzionalità di Target.

Le seguenti funzioni sono state testate e sono attualmente supportate in [!DNL Target]:

* [Test A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [Generazione di rapporti su impression e conversione per A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Attività Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Attività di targeting delle esperienze](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Test multivariati (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Attività di Consigli](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [Generazione di rapporti sulle impression e sulle conversioni di Target nativi](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [Supporto VEC](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Platform Web SDK] diagramma di sistema

Il diagramma seguente illustra il flusso di lavoro di [!DNL Target] e [!DNL Platform Web SDK] decisione edge.

![Diagramma delle decisioni edge di Adobe Target con Platform Web SDK](./assets/target-platform-web-sdk.png)

| Chiamata | Dettagli |
| --- | --- |
| 1 | Il dispositivo carica il [!DNL Platform Web SDK]. La [!DNL Platform Web SDK] invia una richiesta alla rete perimetrale con dati XDM, ID ambiente Datastreams, parametri passati e ID cliente (facoltativo). La pagina (o i contenitori) è prenascosta. |
| 2 | La rete perimetrale invia la richiesta ai servizi perimetrali per arricchirla con l’ID visitatore, il consenso e altre informazioni contestuali, come la geolocalizzazione e i nomi descrittivi dei dispositivi. |
| 3 | La rete perimetrale invia la richiesta di personalizzazione arricchita al [!DNL Target] con ID visitatore e parametri passati. |
| 4 | Gli script di profilo vengono eseguiti e quindi inseriti in [!DNL Target] archiviazione dei profili. L’archiviazione dei profili recupera i segmenti dal [!UICONTROL Libreria Pubblico] (ad esempio, segmenti condivisi da [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], [!DNL Adobe Experience Platform]). |
| 5 | In base ai parametri di richiesta URL e ai dati di profilo, [!DNL Target] determina quali attività ed esperienze visualizzare per il visitatore per la visualizzazione della pagina corrente e per le visualizzazioni preacquisite future. [!DNL Target] quindi invia nuovamente questo messaggio alla rete perimetrale. |
| 6 | a) La rete perimetrale invia nuovamente la risposta di personalizzazione alla pagina, includendo facoltativamente i valori di profilo per ulteriore personalizzazione. Il contenuto personalizzato sulla pagina corrente viene mostrato il più rapidamente possibile senza che venga visualizzato momentaneamente il contenuto predefinito.<br>b) Il contenuto personalizzato per le visualizzazioni mostrate come risultato delle azioni dell’utente in un’applicazione a pagina singola (SPA) viene memorizzato nella cache in modo che possa essere applicato immediatamente senza una chiamata al server aggiuntiva quando vengono attivate le visualizzazioni. <br>c. La rete perimetrale invia l’ID visitatore e altri valori nei cookie, come il consenso, l’ID sessione, l’identità, il controllo dei cookie, la personalizzazione e così via. |
| 7 | La rete perimetrale in avanti [!UICONTROL Analytics for Target] (A4T) dettagli (attività, esperienza e metadati di conversione) in [!DNL Analytics] bordo. |

## Abilitazione [!DNL Adobe Target]

Per abilitare [!DNL Target], procedi come segue:

1. Abilita [!DNL Target] nel tuo [datastream](../../fundamentals/datastreams.md) con il codice cliente appropriato.
1. Aggiungi il `renderDecisions` agli eventi.

Quindi, facoltativamente, puoi anche aggiungere le seguenti opzioni:

* **`decisionScopes`**: Recupera attività specifiche (utile per le attività create con il compositore basato su moduli) aggiungendo questa opzione agli eventi.
* **[Anteprima del frammento](../manage-flicker.md)**: Nasconde solo alcune parti della pagina.

## Utilizzo del Compositore esperienza visivo di Adobe Target

Per utilizzare il Compositore esperienza visivo con un [!DNL Platform Web SDK] implementazione, installazione e attivazione di [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) o [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) Estensione VEC Helper.

Per ulteriori informazioni, consulta [Estensione helper del Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) in *Guida di Adobe Target*.

## Rendering di contenuti personalizzati

Vedi [Rendering del contenuto di personalizzazione](../rendering-personalization-content.md) per ulteriori informazioni.

## Tipi di pubblico in XDM

Quando definisci i tipi di pubblico per [!DNL Target] le attività fornite tramite [!DNL Platform Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=it) devono essere definiti e utilizzati. Dopo aver definito schemi, classi e gruppi di campi di schema XDM, è possibile creare un [!DNL Target] regola del pubblico definita dai dati XDM per il targeting. Within [!DNL Target], i dati XDM vengono visualizzati nella sezione [!UICONTROL Audience Builder] come parametro personalizzato. L’XDM viene serializzato utilizzando la notazione del punto (ad esempio, `web.webPageDetails.name`).

Se [!DNL Target] le attività con tipi di pubblico predefiniti che utilizzano parametri personalizzati o un profilo utente, non vengono consegnati correttamente tramite l’SDK. Invece di utilizzare parametri personalizzati o il profilo utente, devi invece utilizzare XDM. Tuttavia, esistono campi di targeting del pubblico predefiniti supportati tramite il [!DNL Platform Web SDK] che non richiedono XDM. Questi campi sono disponibili nella [!DNL Target] Interfaccia utente che non richiede XDM:

* Libreria di Target
* Geo
* Rete 
* Operating System
* Pagine del sito
* Browser
* Origini del traffico
* Intervallo temporale

Per ulteriori informazioni, consulta [Categorie di pubblico](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en) in *Guida di Adobe Target*.

### Token di risposta

I token di risposta vengono utilizzati principalmente per inviare metadati a terze parti come Google, Facebook, ecc. I token di risposta vengono restituiti nella variabile `meta` campo `propositions` -> `items`. Ecco un esempio:

```
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

Per raccogliere i token di risposta, devi abbonarti per `alloy.sendEvent` promettere, eseguire iterazioni `propositions`
ed estrarre i dettagli da `items` -> `meta`. Ogni `proposition` ha `renderAttempted` campo booleano che indica se la `proposition` è stato reso o no. Vedi il campione seguente:

```
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

Quando il rendering automatico è abilitato, la matrice delle proposizioni contiene:

#### Al caricamento della pagina:

* Basato su Compositore basato su moduli `propositions` con `renderAttempted` flag impostato su `false`
* Proposizioni basate su Compositore esperienza visivo con `renderAttempted` flag impostato su `true`
* Proposte basate su Compositore esperienza visivo per una visualizzazione di applicazione a pagina singola con `renderAttempted` flag impostato su `true`

#### On View - change (sulla visualizzazione in cache):

* Proposte basate su Compositore esperienza visivo per una visualizzazione di applicazione a pagina singola con `renderAttempted` flag impostato su `true`

Quando il rendering automatico è disabilitato, la matrice delle proposizioni contiene:

#### Al caricamento della pagina:

* Basato su Compositore basato su moduli `propositions` con `renderAttempted` flag impostato su `false`
* Proposizioni basate su Compositore esperienza visivo con `renderAttempted` flag impostato su `false`
* Proposte basate su Compositore esperienza visivo per una visualizzazione di applicazione a pagina singola con `renderAttempted` flag impostato su `false`

#### On View - change (sulla visualizzazione in cache):

* Proposte basate su Compositore esperienza visivo per una visualizzazione di applicazione a pagina singola con `renderAttempted` flag impostato su `false`

### Aggiornamento di un singolo profilo

La [!DNL Platform Web SDK] consente di aggiornare il profilo al [!DNL Target] e al [!DNL Platform Web SDK] come evento di esperienza.

Per aggiornare un [!DNL Target] , assicurati che i dati del profilo siano trasmessi con quanto segue:

* Sotto `“data {“`
* Sotto `“__adobe.target”`
* Prefisso `“profile.”` ad esempio come segue

| Chiave | Tipo | Descrizione |
| --- | --- | --- |
| `renderDecisions` | Booleano | Indica al componente di personalizzazione se deve interpretare le azioni DOM |
| `decisionScopes` | Array `<String>` | Elenco di ambiti per i quali recuperare le decisioni |
| `xdm` | Oggetto | Dati formattati in XDM che arrivano nell’SDK per web di Platform come evento di esperienza |
| `data` | Oggetto | Coppie chiave/valore arbitrarie inviate a [!DNL Target] soluzioni sotto la classe target. |

Tipico [!DNL Platform Web SDK] il codice che utilizza questo comando ha il seguente aspetto:

**`sendEvent`con dati di profilo**

```
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**Come inviare gli attributi del profilo ad Adobe Target:**

```
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

Elenco delle tabelle seguenti [!DNL Recommendations] e se ciascuno di essi è supportato tramite il [!DNL Platform Web SDK]:

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

**Come inviare gli attributi di Recommendations ad Adobe Target:**

```
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

## Eseguire il debug di

mboxTrace e mboxDebug sono stati dichiarati obsoleti. Utilizzo [[!DNL Platform Web SDK] debugging](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html).

## Terminologia

__Proposizioni:__ In [!DNL Target], le proposizioni sono correlate all’esperienza selezionata da un’attività .

__Schema:__ Lo schema di una decisione è il tipo di offerta in [!DNL Target].

__Ambito di applicazione:__ Il campo di applicazione della decisione. In [!DNL Target], l&#39;ambito è mBox. L&#39;mBox globale è il `__view__` ambito di applicazione.

__XDM:__ XDM viene serializzato nella notazione del punto e quindi inserito in [!DNL Target] come parametri mBox.
