---
title: Utilizzo di Adobe Target con Platform Web SDK
description: Scopri come eseguire il rendering di contenuti personalizzati con Experience Platform Web SDK tramite Adobe Target
keywords: target;adobe target;activity.id;experience.id;renderdecisions;decisionScopes;pre-hiding snippet;vec;Compositore esperienza basato su moduli;xdm;tipi di pubblico;decisioni;ambito;schema;
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
translation-type: tm+mt
source-git-commit: e12b1337c44095ee8731f99c5829ab83bba14889
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 4%

---

# Utilizzo di Adobe Target con Platform Web SDK

Adobe Experience Platform [!DNL Web SDK] può fornire ed eseguire il rendering sul canale web di esperienze personalizzate gestite in Adobe Target. Puoi utilizzare un editor WYSIWYG, denominato [Compositore esperienza visivo](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) (VEC), o un&#39;interfaccia non visiva, il [Compositore esperienza basato su moduli](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html), per creare, attivare e distribuire le tue attività e esperienze di personalizzazione.

Le seguenti funzioni sono state testate e sono attualmente supportate in Target:

* Test A/B
* Generazione di rapporti su impression e conversione per A4T
* Automated Personalization
* Targeting esperienza
* Test multivariati
* Generazione di rapporti su impression e conversione di Target nativi
* Supporto VEC

## Abilitazione di Adobe Target

Per abilitare [!DNL Target], procedi come segue:

1. Abilita target nella [configurazione perimetrale](../../fundamentals/edge-configuration.md) con il codice client appropriato.
1. Aggiungi l’opzione `renderDecisions` agli eventi.

Quindi, facoltativamente, puoi anche aggiungere le seguenti opzioni:

* `decisionScopes`: Recupera attività specifiche (utile per le attività create con il compositore basato su moduli) aggiungendo questa opzione agli eventi.
* [Anteprima del frammento](../manage-flicker.md): Nasconde solo alcune parti della pagina.

## Utilizzo del Compositore esperienza visivo di Adobe Target

Per utilizzare il Compositore esperienza visivo con un’implementazione Platform Web SDK, installa e attiva l’ [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) o [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) estensione VEC Helper.

## Rendering automatico delle attività del Compositore esperienza visivo

Adobe Experience Platform Web SDK ha la facoltà di eseguire automaticamente sul Web il rendering delle esperienze definite tramite VEC di Adobe Target per i tuoi utenti. Per indicare a Adobe Experience Platform Web SDK di eseguire il rendering automatico delle attività del Compositore esperienza visivo, invia un evento con `renderDecisions = true`:

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

## Utilizzo del Compositore basato su moduli

Il Compositore esperienza basato su moduli è un’interfaccia non visiva utile per configurare test A/B, [!DNL Experience Targeting], Automated Personalization e attività Recommendations con diversi tipi di risposta, come JSON, HTML, immagine, ecc. A seconda del tipo di risposta o della decisione restituita da Adobe Target, è possibile eseguire la logica di business principale. Per recuperare le decisioni per le attività del Compositore basato su moduli, invia un evento con tutti gli &quot;ambiti decisionali&quot; per i quali desideri recuperare una decisione.

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

`decisionScopes` definisce sezioni, posizioni o parti delle pagine in cui desideri eseguire il rendering di un’esperienza personalizzata. Questi `decisionScopes` sono personalizzabili e definiti dall&#39;utente. Per i clienti [!DNL Target] correnti, `decisionScopes` sono noti anche come &quot;mbox&quot;. Nell’interfaccia utente [!DNL Target], `decisionScopes` viene visualizzato come &quot;posizioni&quot;.

## Ambito `__view__`

Adobe Experience Platform Web SDK fornisce funzionalità che consentono di recuperare le azioni del Compositore esperienza visivo senza affidarsi all’SDK per eseguire il rendering delle azioni del Compositore esperienza visivo. Invia un evento con `__view__` definito come `decisionScopes`.

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

Quando definisci i tipi di pubblico per le attività Target fornite tramite Adobe Experience Platform Web SDK, devi definire e utilizzare [XDM](https://docs.adobe.com/content/help/it-IT/experience-platform/xdm/home.html). Dopo aver definito schemi, classi e gruppi di campi di schema XDM, puoi creare una regola di pubblico Target definita dai dati XDM per il targeting. In Target, i dati XDM vengono visualizzati in Audience Builder come parametro personalizzato. L’XDM viene serializzato utilizzando la notazione del punto (ad esempio, `web.webPageDetails.name`).

Se disponi di attività Target con tipi di pubblico predefiniti che utilizzano parametri personalizzati o un profilo utente, queste non vengono consegnate correttamente tramite l’SDK. Invece di utilizzare parametri personalizzati o il profilo utente, devi invece utilizzare XDM. Tuttavia, esistono campi di targeting del pubblico preconfigurati supportati tramite Adobe Experience Platform Web SDK che non richiedono XDM. Questi campi sono disponibili nell’interfaccia utente di Target che non richiede XDM:

* Libreria di Target
* Geo
* Rete 
* Operating System
* Pagine del sito
* Browser
* Origini del traffico
* Intervallo temporale

## Terminologia

__Decisioni:__ in  [!DNL Target], le decisioni sono correlate all’esperienza selezionata da un’attività.

__Schema:__ lo schema di una decisione è il tipo di offerta in  [!DNL Target].

__Ambito di applicazione:__ ambito di applicazione della decisione. In [!DNL Target], l&#39;ambito è mBox. L&#39;mBox globale è l&#39;ambito `__view__`.

__XDM:__ XDM viene serializzato nella notazione del punto e quindi inserito  [!DNL Target] come parametri mBox.
