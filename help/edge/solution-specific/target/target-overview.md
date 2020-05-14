---
title: 'Adobe Target e l''SDK Web per Adobe Experience Platform. '
seo-title: SDK Web per Adobe Experience Platform e utilizzo di Adobe Target
description: Scopri come eseguire il rendering del contenuto personalizzato con l’SDK Web della piattaforma Experience tramite Adobe Target
seo-description: Scopri come eseguire il rendering del contenuto personalizzato con l’SDK Web della piattaforma Experience tramite Adobe Target
translation-type: tm+mt
source-git-commit: 4bff4b20ccc1913151aa1783d5123ffbb141a7d0
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 2%

---


# Panoramica di Target

L’SDK Web per Adobe Experience Platform può distribuire e rappresentare esperienze personalizzate gestite in Adobe Target per il canale Web. Potete utilizzare un editor WYSIWYG, denominato [Visual Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) (VEC), o un&#39;interfaccia non visiva, Experience Composer (Compositore [esperienza basato su](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html)modulo), per creare, attivare e distribuire le attività e le esperienze di personalizzazione.

## Abilitazione di Adobe Target

Per abilitare Target, devi effettuare le seguenti operazioni:

1. Attivate i token di risposta activity.id ed experience.id nell&#39;interfaccia di Target.

![target_reponse_token](../../solution-specific/target/assets/target_response_token.png)

1. Attivate la destinazione nella configurazione [](../../fundamentals/edge-configuration.md) edge con il codice client appropriato.
1. Aggiungete l&#39; `renderDecisions` opzione agli eventi.

Quindi, facoltativamente, puoi anche:

* Aggiungete `decisionScopes` agli eventi per recuperare attività specifiche (utile per le attività create con il compositore basato su modulo).
* Aggiungete lo snippet di [anteprima](../../solution-specific/target/flicker-management.md) per nascondere solo alcune parti della pagina.

## Utilizzo di Adobe Target VEC

Con l’SDK, puoi usare normalmente il VEC con una sola eccezione: è necessario installare e attivare l&#39;estensione [helper VEC](https://docs.adobe.com/content/help/en/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) di destinazione.

## Rendering automatico delle attività VEC

L’SDK Web AEP può rappresentare automaticamente sul Web le esperienze definite tramite il VEC di Adobe Target per gli utenti. Per indicare all’SDK Web AEP di eseguire il rendering automatico delle attività VEC, inviate un evento con `renderDecisions = true`:

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

Experience Composer basato su modulo è un&#39;interfaccia non visiva utile per configurare test A/B, targeting delle esperienze, Automated Personalization (Personalizzazione automatizzata) e attività di Recommendations con diversi tipi di risposta, come JSON, HTML, Image, ecc. A seconda del tipo di risposta o della decisione restituita da Adobe Target, è possibile eseguire la logica aziendale principale. Per recuperare le decisioni per le attività di Composer basate su modulo, inviate un evento con tutti gli ‘ambiti decisionali’ per i quali desiderate ottenere una decisione.

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

`decisionScopes` definisce sezioni, posizioni o parti delle pagine in cui eseguire il rendering di un&#39;esperienza personalizzata. Sono `decisionScopes` personalizzabili e definiti dall’utente. Per i clienti Target correnti, `decisionScopes` sono noti anche come &quot;mbox&quot;. Nell&#39;interfaccia di Target, `decisionScopes` compare come &quot;posizioni&quot;.

## __visualizza__ ambito

L’SDK Web AEP fornisce una funzionalità che consente di recuperare le azioni VEC senza affidarsi all’SDK Web AEP per eseguire il rendering delle azioni VEC. Invia un evento con `__view__` definito come `decisionScopes`.

```javascript
alloy("sendEvent", {
  decisionScopes: [“__view__”,"foo", "bar"], 
  "xdm": { 
    "web": { 
      "webPageDetails": { 
        "name": "Home Page"
       }
      } 
     }
    }
   ).then(results){
  for (decision of results.decisions){
     if(decision.decisionScope == "__view__")
       console.log(decision.content)
}
};
```

## Tipi di pubblico in XDM

Quando definite Audiences per le attività Target che verranno distribuite tramite AEP Web SDK, [XDM](https://docs.adobe.com/content/help/en/experience-platform/xdm/home.html) deve essere definito e utilizzato. Dopo aver definito schemi, classi e mixin XDM, potete creare una regola di pubblico Target definita dai dati XDM per il targeting. In Target, i dati XDM vengono visualizzati in Audience Builder come parametro personalizzato. L&#39;XDM viene serializzato utilizzando la notazione del punto (ad esempio, `web.webPageDetails.name`).

Se hai attività Target con audience predefinite che utilizzano parametri personalizzati o un profilo utente, accertati che non verranno distribuite correttamente tramite AEP Web SDK. Invece di utilizzare parametri personalizzati o il profilo utente, è necessario utilizzare XDM. Tuttavia, esistono campi di targeting del pubblico out-of-the-box supportati tramite AEP Web SDK che non richiedono XDM. Questi sono i campi disponibili nell&#39;interfaccia di Target che non richiedono XDM:

* Libreria di Target
* Geo
* Rete 
* Sistema operativo
* Pagine del sito
* Browser
* Origini del traffico
* Intervallo temporale

## Terminologia

__Decisioni__ - In Target, queste sono correlate all&#39;esperienza selezionata da un&#39;attività.

__Ambito__ - Ambito di applicazione della decisione. In Target, questo è l&#39;mBox. L&#39;mBox globale è l&#39; `__view__` ambito.

__Schema__ - Lo schema di una decisione è il tipo di offerta in Target.

__XDM__ - L&#39;XDM viene serializzato nella notazione del punto e quindi immesso in Target come parametri mBox.
