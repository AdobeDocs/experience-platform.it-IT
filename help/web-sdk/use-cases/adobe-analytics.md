---
title: Invio di dati ad Adobe Analytics tramite Web SDK
description: Scopri come inviare dati ad Adobe Analytics con Adobe Experience Platform Web SDK.
keywords: adobe analytics;dati mappati;variabili mappate;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 3%

---

# Inviare dati ad Adobe Analytics tramite Web SDK

Adobe Experience Platform Web SDK può inviare dati ad Adobe Analytics tramite la rete Edge di Adobe Experience Platform. Quando i dati arrivano alla rete Edge, traducono l’oggetto XDM in un formato comprensibile da Adobe Analytics.

## Gruppo di campi XDM

Per acquisire più facilmente le metriche di Adobe Analytics più comuni, Adobe fornisce un gruppo di campi orientato ad Adobe Analytics che puoi utilizzare. Per ulteriori dettagli su questo schema, consulta [Gruppo di campi schema Estensione completa Adobe Analytics ExperienceEvent](/help/xdm/field-groups/event/analytics-full-extension.md).

## Mappatura variabile

La rete Edge mappa automaticamente molte variabili XDM. Consulta [Mappatura delle variabili di Analytics nella rete Edge](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=it) nella guida all’implementazione di Adobe Analytics per un elenco completo delle variabili mappate automaticamente.

Tutte le variabili che non vengono mappate automaticamente sono disponibili come [Variabili di dati di contesto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=it). A questo punto puoi utilizzare [Regole di elaborazione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about.html) per mappare le variabili di dati di contesto alle variabili di Analytics. Ad esempio, se lo schema XDM era personalizzato come il seguente:

```js
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    "v0",
    "v1",
    "v2"
  ],
  arrayofobjects:[
    {
      obj1key:objval0
    },
    {
      obj2key:objval1
    }
  ]
}
```

Quindi sarebbero le chiavi di dati contestuali disponibili nell’interfaccia Regole di elaborazione:

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.arrayofobjects.0.obj1key //objval0
a.x.arrayofobjects.1.obj2key //objval1
```

>[!NOTE]
>
>Con la raccolta di reti Edge, tutti gli eventi vengono inviati ad Analytics e a tutti gli altri servizi configurati per lo stream di dati. Ad esempio, se hai sia Analytics che Target configurati come servizi e effettui chiamate separate per la personalizzazione e per Analytics, entrambi gli eventi vengono inviati ad Analytics e Target. Questi eventi vengono registrati nei rapporti di Analytics e possono influenzare metriche quali il tasso di mancato recapito.

## Visualizzazioni di pagina e chiamate di tracciamento dei collegamenti

AppMeasurement in Adobe Analytics utilizza chiamate di metodo separate per le visualizzazioni di pagina ([`t()` metodo](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/t-method.html)) e le chiamate di tracciamento dei collegamenti ([`tl()` metodo](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/tl-method.html)). L’SDK per web fornisce invece solo [`sendEvent`](../commands/sendevent/overview.md) comando per inviare sia le visualizzazioni di pagina che il tracciamento dei collegamenti. I dati inclusi in un evento determinano se si tratta di [visualizzazione pagina](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-views.html?lang=it) o un [evento pagina](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-events.html) in Adobe Analytics.

Per impostazione predefinita, tutti gli eventi sono considerati visualizzazioni di pagina in Adobe Analytics. Se desideri impostare un evento Web SDK su una chiamata di tracciamento dei collegamenti di Adobe Analytics, imposta i seguenti campi XDM:

* **`web.webInteraction.URL`**: URL del collegamento.
* **`web.webInteraction.name`**: nome della dimensione Collegamento personalizzato, Collegamento di download o Collegamento di uscita, a seconda del valore in `web.webInteraction.type`
* **`web.webInteraction.type`**: determina il tipo di collegamento su cui è stato fatto clic. I valori validi includono `other` (Collegamenti personalizzati), `download` (Collegamenti di download) e `exit` (Collegamenti di uscita).

Se si abilita [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) nel `configure` , questi campi XDM vengono compilati automaticamente.
