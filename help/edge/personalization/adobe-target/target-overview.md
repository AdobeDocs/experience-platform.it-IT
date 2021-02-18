---
title: Utilizzo di  Adobe Target con Platform Web SDK
description: Scopri come eseguire il rendering del contenuto personalizzato con l’SDK Web per Experienci Platform  utilizzando  Adobe Target
keywords: target;adobe target;activity.id;experience.id;renderingDecisions;DecisionScopes;prehide snippet;vec;Form-Based Experience Composer;xdm;audiences;decisions;scope;schema;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 3%

---


# Utilizzo di  Adobe Target con Platform Web SDK

Adobe Experience Platform [!DNL Web SDK] è in grado di distribuire e rappresentare esperienze personalizzate gestite in Adobe Target  canale Web. Potete utilizzare un editor WYSIWYG, denominato [Visual Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) (VEC), o un&#39;interfaccia non visiva, il [Composer esperienza basato su moduli](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html), per creare, attivare e distribuire le attività e le esperienze di personalizzazione.

## Abilitazione  Adobe Target

Per abilitare [!DNL Target], è necessario effettuare le seguenti operazioni:

1. Abilitare la destinazione nella [configurazione periferica](../../fundamentals/edge-configuration.md) con il codice client appropriato.
1. Aggiungete l&#39;opzione `renderDecisions` agli eventi.

Quindi, facoltativamente, puoi anche:

* Aggiungete `decisionScopes` agli eventi per recuperare attività specifiche (utile per le attività create con il compositore basato su modulo).
* Aggiungete il [snippet di anteprima](../manage-flicker.md) per nascondere solo alcune porzioni della pagina.

## Utilizzo di  Adobe Target VEC

Per utilizzare VEC con un&#39;implementazione SDK Web della piattaforma, è necessario installare e attivare l&#39;estensione [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) o [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper Extension.

## Rendering automatico delle attività VEC

L’SDK Web di Adobe Experience Platform consente di eseguire automaticamente il rendering delle esperienze definite tramite  VEC di Adobe Target sul Web per gli utenti. Per indicare ad Adobe Experience Platform Web SDK di eseguire il rendering automatico delle attività VEC, inviate un evento con `renderDecisions = true`:

```javascript
alloy
("sendEvent", 
  { 
  "renderDecisions": true, 
  "xdm": {
    "commerce": { 
      "order": {
        "purchaseID": "a8g784hjq1mnp3", 
         "purchaseOrderNumber": "VAU3123", 
         "currencyCode": "USD", 
         "priceTotal": 999.98 
         } 
      } 
    }
  }
);
```

## Utilizzo di Composer basato su modulo

Experience Composer basato su modulo è un&#39;interfaccia non visiva utile per configurare test A/B, [!DNL Experience Targeting],  attività Automated Personalization e Recommendations con diversi tipi di risposta, come JSON, HTML, Image, ecc. A seconda del tipo di risposta o della decisione restituita da  Adobe Target, è possibile eseguire la logica aziendale principale. Per recuperare le decisioni per le attività di Composer basate su modulo, inviate un evento con tutti gli ‘ambiti decisionali’ per i quali desiderate ottenere una decisione.

```javascript
alloy
  ("sendEvent", { 
    decisionScopes: [
      "foo", "bar"], 
      "xdm": {
        "commerce": { 
          "order": { 
            "purchaseID": "a8g784hjq1mnp3", 
            "purchaseOrderNumber": "VAU3123", 
            "currencyCode": "USD", 
            "priceTotal": 999.98 
          } 
        } 
      } 
    }
  );
```

## Ambiti decisionali

`decisionScopes` definisce sezioni, posizioni o parti delle pagine in cui eseguire il rendering di un&#39;esperienza personalizzata. Questi `decisionScopes` sono personalizzabili e definiti dall&#39;utente. Per i clienti [!DNL Target] correnti, `decisionScopes` sono noti anche come &quot;mbox&quot;. Nell&#39;interfaccia [!DNL Target], `decisionScopes` viene visualizzato come &quot;locations&quot;.

## L&#39;ambito `__view__`

Adobe Experience Platform Web SDK fornisce funzionalità che consentono di recuperare azioni VEC senza affidarsi all&#39;SDK per eseguire il rendering delle azioni VEC. Inviare un evento con `__view__` definito come `decisionScopes`.

```javascript
alloy("sendEvent", {
      "decisionScopes": ["__view__", "foo", "bar"], 
      "xdm": { 
        "web": { 
          "webPageDetails": { 
            "name": "Home Page"
          }
        } 
      }
    }
  ).then(function(results) {
    for (decision of results.decisions) {
      if (decision.decisionScope === "__view__") {
        console.log(decision.content)
      }
    }
  });
```

## Tipi di pubblico in XDM

Quando definisci Audiences per le attività Target che verranno distribuite tramite Adobe Experience Platform Web SDK, [XDM](https://docs.adobe.com/content/help/it-IT/experience-platform/xdm/home.html) deve essere definito e utilizzato. Dopo aver definito schemi, classi e mixin XDM, potete creare una regola di pubblico Target definita dai dati XDM per il targeting. In Target, i dati XDM vengono visualizzati in Audience Builder come parametro personalizzato. L&#39;XDM viene serializzato utilizzando la notazione del punto (ad esempio, `web.webPageDetails.name`).

Se hai attività Target con audience predefinite che utilizzano parametri personalizzati o un profilo utente, accertati che non verranno distribuite correttamente tramite l’SDK. Invece di utilizzare parametri personalizzati o il profilo utente, è necessario utilizzare XDM. Tuttavia, esistono campi di targeting del pubblico out-of-the-box supportati tramite Adobe Experience Platform Web SDK che non richiedono XDM. Questi sono i campi disponibili nell&#39;interfaccia di Target che non richiedono XDM:

* Libreria di Target
* Geo
* Rete 
* Operating System
* Pagine del sito
* Browser
* Origini del traffico
* Intervallo temporale

## Terminologia

__Decisioni:__ In  [!DNL Target], queste sono correlate all&#39;esperienza selezionata da un&#39;attività.

__Schema:__ Lo schema di una decisione è il tipo di offerta in  [!DNL Target].

__Campo di applicazione:__ Ambito di applicazione della decisione. In [!DNL Target], questo è l&#39;mBox. L&#39;mBox globale è l&#39;ambito `__view__`.

__XDM:__ l&#39;XDM viene serializzato nella notazione del punto e quindi inserito  [!DNL Target] come parametri mBox.
