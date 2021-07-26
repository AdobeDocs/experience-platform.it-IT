---
title: Utilizzo di Adobe Target con Platform Web SDK
description: Scopri come eseguire il rendering di contenuti personalizzati con Experience Platform Web SDK tramite Adobe Target
keywords: target;adobe target;activity.id;experience.id;renderdecisions;decisionScopes;pre-hiding snippet;vec;Compositore esperienza basato su moduli;xdm;tipi di pubblico;decisioni;ambito;schema;
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: c83b6ea336cfe5d6d340a2dbbfb663b6bec84312
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 4%

---

# Utilizzo di [!DNL Adobe Target] con [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] può fornire ed eseguire il rendering di esperienze personalizzate gestite in  [!DNL Adobe Target] sul canale web. Puoi utilizzare un editor WYSIWYG, denominato [Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC), o un&#39;interfaccia non visiva, il [Compositore esperienza basato su moduli](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), per creare, attivare e distribuire le tue attività e esperienze di personalizzazione.

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

Il diagramma seguente ti aiuta a comprendere il flusso di lavoro delle [!DNL Target] e [!DNL Platform Web SDK] decisioni edge.

![Diagramma delle decisioni edge di Adobe Target con Platform Web SDK](./assets/target-platform-web-sdk.png)

| Chiamata | Dettagli |
| --- | --- |
| 1 | Il dispositivo carica il [!DNL Platform Web SDK]. Il [!DNL Platform Web SDK] invia una richiesta alla rete perimetrale con dati XDM, l’ID ambiente Datastreams, i parametri passati e l’ID cliente (facoltativo). La pagina (o i contenitori) è prenascosta. |
| 2 | La rete perimetrale invia la richiesta ai servizi perimetrali per arricchirla con l’ID visitatore, il consenso e altre informazioni contestuali, come la geolocalizzazione e i nomi descrittivi dei dispositivi. |
| 3 | La rete perimetrale invia la richiesta di personalizzazione arricchita al server Edge [!DNL Target] con l’ID visitatore e i parametri passati. |
| 4 | Gli script di profilo vengono eseguiti e quindi inseriti nell’archivio dei profili [!DNL Target]. L’archiviazione dei profili recupera i segmenti dalla [!UICONTROL Libreria tipi di pubblico] (ad esempio, i segmenti condivisi da [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], [!DNL Adobe Experience Platform]). |
| 5 | In base ai parametri di richiesta URL e ai dati di profilo, [!DNL Target] determina quali attività ed esperienze visualizzare per il visitatore per la visualizzazione della pagina corrente e per le visualizzazioni preacquisite future. [!DNL Target] quindi invia nuovamente questo messaggio alla rete perimetrale. |
| 6 | a) La rete perimetrale invia nuovamente la risposta di personalizzazione alla pagina, includendo facoltativamente i valori di profilo per ulteriore personalizzazione. Il contenuto personalizzato sulla pagina corrente viene mostrato il più rapidamente possibile senza che venga visualizzato momentaneamente il contenuto predefinito.<br>b) Il contenuto personalizzato per le visualizzazioni mostrate come risultato delle azioni dell’utente in un’applicazione a pagina singola (SPA) viene memorizzato nella cache in modo che possa essere applicato immediatamente senza una chiamata al server aggiuntiva quando vengono attivate le visualizzazioni &#x200B;.<br>c. La rete perimetrale invia l’ID visitatore e altri valori nei cookie, come il consenso, l’ID sessione, l’identità, il controllo dei cookie, la personalizzazione e così via. |
| 7 | La rete Edge inoltra i dettagli [!UICONTROL Analytics for Target] (A4T) (attività, esperienza e metadati di conversione) al &#x200B; Edge [!DNL Analytics]. |

## Abilitazione di [!DNL Adobe Target]

Per abilitare [!DNL Target], procedi come segue:

1. Abilita [!DNL Target] nel tuo [datastream](../../fundamentals/datastreams.md) con il codice client appropriato.
1. Aggiungi l’opzione `renderDecisions` agli eventi.

Quindi, facoltativamente, puoi anche aggiungere le seguenti opzioni:

* **`decisionScopes`**: Recupera attività specifiche (utile per le attività create con il compositore basato su moduli) aggiungendo questa opzione agli eventi.
* **[Anteprima del frammento](../manage-flicker.md)**: Nasconde solo alcune parti della pagina.

## Utilizzo del Compositore esperienza visivo di Adobe Target

Per utilizzare il Compositore esperienza visivo con un’implementazione [!DNL Platform Web SDK], installa e attiva l’ [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) o [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) estensione VEC Helper.

Per ulteriori informazioni, consulta [Estensione helper del Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) nella *guida Adobe Target*.

## Rendering automatico delle attività del Compositore esperienza visivo

Il [!DNL Adobe Experience Platform Web SDK] ha il potere di eseguire automaticamente sul Web il rendering delle esperienze definite tramite il Compositore esperienza visivo di [!DNL Adobe Target] per i tuoi utenti. Per indicare a [!DNL Experience Platform Web SDK] di eseguire il rendering automatico delle attività del Compositore esperienza visivo, invia un evento con `renderDecisions = true`:

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

Il [Compositore esperienza basato su moduli](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) è un&#39;interfaccia non visiva utile per configurare [!UICONTROL Test A/B], [!UICONTROL Targeting esperienza], [!UICONTROL Automated Personalization] e [!UICONTROL Recommendations] con diversi tipi di risposta, come JSON, HTML, immagine, ecc. A seconda del tipo di risposta o della decisione restituita da [!DNL Target], è possibile eseguire la logica di business di base. Per recuperare le decisioni per le attività del Compositore basato su moduli, invia un evento con tutti gli &quot;ambiti decisionali&quot; per i quali desideri recuperare una decisione.

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

`decisionScopes` definisci sezioni, posizioni o parti delle pagine in cui desideri eseguire il rendering di un’esperienza personalizzata. Questi `decisionScopes` sono personalizzabili e definiti dall&#39;utente. Per i clienti [!DNL Target] correnti, `decisionScopes` sono noti anche come &quot;mbox&quot;. Nell’interfaccia utente [!DNL Target], `decisionScopes` viene visualizzato come &quot;posizioni&quot;.

## Ambito `__view__`

Il [!DNL Experience Platform Web SDK] fornisce funzionalità per recuperare le azioni del Compositore esperienza visivo senza affidarsi all’SDK per eseguire il rendering delle azioni del Compositore esperienza visivo. Invia un evento con `__view__` definito come `decisionScopes`.

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

Quando definisci i tipi di pubblico per le attività [!DNL Target] fornite tramite [!DNL Platform Web SDK], devi definire e utilizzare [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=it). Dopo aver definito schemi, classi e gruppi di campi di schema XDM, puoi creare una regola di pubblico [!DNL Target] definita dai dati XDM per il targeting. All&#39;interno di [!DNL Target], i dati XDM vengono visualizzati in [!UICONTROL Audience Builder] come parametro personalizzato. L’XDM viene serializzato utilizzando la notazione del punto (ad esempio, `web.webPageDetails.name`).

Se disponi di attività [!DNL Target] con tipi di pubblico predefiniti che utilizzano parametri personalizzati o un profilo utente, queste non vengono consegnate correttamente tramite l’SDK. Invece di utilizzare parametri personalizzati o il profilo utente, devi invece utilizzare XDM. Tuttavia, esistono campi di targeting del pubblico preconfigurati supportati tramite [!DNL Platform Web SDK] che non richiedono XDM. Questi campi sono disponibili nell’ interfaccia utente [!DNL Target] che non richiede XDM:

* Libreria di Target
* Geo
* Rete 
* Operating System
* Pagine del sito
* Browser
* Origini del traffico
* Intervallo temporale

Per ulteriori informazioni, consulta [Categorie di pubblico](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en) nella *guida Adobe Target*.

### Aggiornamento di un singolo profilo

Il [!DNL Platform Web SDK] ti consente di aggiornare il profilo al profilo [!DNL Target] e al [!DNL Platform Web SDK] come evento di esperienza.

Per aggiornare un profilo [!DNL Target], accertati che i dati del profilo vengano passati con quanto segue:

* Sotto `“data {“`
* Sotto `“__adobe.target”`
* Prefisso `“profile.”` ad esempio come segue

| Chiave | Tipo | Descrizione |
| --- | --- | --- |
| `renderDecisions` | Booleano | Indica al componente di personalizzazione se deve interpretare le azioni DOM |
| `decisionScopes` | Array `<String>` | Elenco di ambiti per i quali recuperare le decisioni |
| `xdm` | Oggetto | Dati formattati in XDM che arrivano nell’SDK per web di Platform come evento di esperienza |
| `data` | Oggetto | Coppie arbitrarie chiave/valore inviate alle soluzioni [!DNL Target] sotto la classe target. |

Il codice [!DNL Platform Web SDK] tipico che utilizza questo comando è simile al seguente:

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

Nella tabella seguente sono elencati gli attributi [!DNL Recommendations] e se ciascuno di essi è supportato tramite [!DNL Platform Web SDK]:

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
        "entity.id" : "123",
        "entity.genre" : "Drama"
      }
    }
  }
});
```

## Eseguire il debug di

mboxTrace e mboxDebug sono stati dichiarati obsoleti. Utilizzare [[!DNL Platform Web SDK] debugging](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html).

## Terminologia

__Decisioni:__ in  [!DNL Target], le decisioni sono correlate all’esperienza selezionata da un’attività.

__Schema:__ lo schema di una decisione è il tipo di offerta in  [!DNL Target].

__Ambito di applicazione:__ ambito di applicazione della decisione. In [!DNL Target], l&#39;ambito è mBox. L&#39;mBox globale è l&#39;ambito `__view__`.

__XDM:__ XDM viene serializzato nella notazione del punto e quindi inserito  [!DNL Target] come parametri mBox.
