---
title: Invio di dati ad Adobe Analytics tramite Web SDK
description: Scopri come inviare dati ad Adobe Analytics con Adobe Experience Platform Web SDK.
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# Inviare dati ad Adobe Analytics tramite Web SDK

Experienci Platform Web SDK può inviare dati ad Adobe Analytics tramite l’Edge Network di Experience Platform. L’Adobe fornisce diverse opzioni per inviare dati ad Adobe Analytics tramite Web SDK:

* Aggiungi il [**[!UICONTROL Gruppo di campi Adobe Analytics ExperienceEvent]**](../../xdm/field-groups/event/analytics-full-extension.md) nello schema, quindi utilizza [`XDM` oggetto](../commands/sendevent/xdm.md).
* Utilizza il [`data` oggetto](../commands/sendevent/data.md) per inviare dati ad Adobe Analytics senza uno schema XDM.
* Usa generato automaticamente [variabili di dati di contesto](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/contextdata) e [regole di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about).

## Utilizza il `XDM` oggetto {#use-xdm-object}

Se desideri utilizzare uno schema predefinito specifico per Adobe Analytics, puoi aggiungere [Gruppo di campi schema Adobe Analytics ExperienceEvent](../../xdm/field-groups/event/analytics-full-extension.md) allo schema. Una volta aggiunto, puoi popolare questo schema utilizzando `xdm` nell&#39;SDK per web per inviare dati a una suite di rapporti. Quando i dati arrivano all’Edge Network, traducono l’oggetto XDM in un formato comprensibile da Adobe Analytics.

Esistono due modi per inviare dati ad Adobe Analytics tramite Web SDK:

* [Inviare dati ad Adobe Analytics tramite l’estensione tag Web SDK](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-tag-extension)
* [Inviare dati ad Adobe Analytics utilizzando la libreria JavaScript dell’SDK per web](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-javascript-library)

Consulta [Mappatura della variabile oggetto XDM su Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/xdm-var-mapping) nella guida all’implementazione di Adobe Analytics per un riferimento completo ai campi XDM e alla loro mappatura sulle variabili di Analytics.

## Utilizza il `data` oggetto {#use-data-object}

In alternativa all’utilizzo dell’oggetto XDM, puoi utilizzare l’oggetto dati. L’oggetto dati è orientato alle implementazioni che al momento utilizzano AppMeasurement, rendendo molto più semplice l’aggiornamento all’SDK per web.

A seconda che si utilizzi AppMeasurement o l’estensione tag Analytics, consulta le seguenti guide per informazioni dettagliate su come migrare a Web SDK:

* [Migrare dall’estensione tag Adobe Analytics all’estensione tag Web SDK](https://experienceleague.adobe.com/it/docs/analytics/implementation/aep-edge/web-sdk/analytics-extension-to-web-sdk)
* [Migrare da AppMeasurement a Web SDK](https://experienceleague.adobe.com/it/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk)

Consulta la documentazione su [mappatura variabile oggetto dati su Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) nella guida all’implementazione di Adobe Analytics, per un riferimento completo ai campi degli oggetti dati e alla loro mappatura sulle variabili di Analytics.

## Utilizzare le variabili di dati di contesto {#use-context-data-variables}

Tutte le variabili che non vengono mappate automaticamente sono disponibili come [variabili di dati di contesto](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/contextdata). A questo punto puoi utilizzare [regole di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about) per mappare le variabili di dati di contesto alle variabili di Analytics. Ad esempio, se lo schema XDM era personalizzato come il seguente:

```json
{
  "xdm": {
    "key":"value",
    "animal": {
      "species": "Raven",
      "size": "13 inches"
    },
    "array": [
      "v0",
      "v1",
      "v2"
    ],
    "objectArray":[{
      "ad1": "300x200",
      "ad2": "60x240",
      "ad3": "600x50"
    }]
  }
}
```

Questi campi sarebbero quindi le chiavi di dati contestuali disponibili nell’interfaccia Regole di elaborazione:

```javascript
a.x.key //value
a.x.animal.species //Raven
a.x.animal.size //13 inches
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.objectarray.0.ad1 //300x200
a.x.objectarray.1.ad2 //60x240
a.x.objectarray.2.ad3 //600x50
```

## Domande frequenti

+++Come posso distinguere le chiamate di visualizzazione pagina dalle chiamate di tracciamento dei collegamenti nell’SDK per web?

AppMeasurement in Adobe Analytics utilizza chiamate di metodo separate per le visualizzazioni di pagina ([`t()` metodo](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/t-method)) e le chiamate di tracciamento dei collegamenti ([`tl()` metodo](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/tl-method)). L’SDK per web fornisce invece solo [`sendEvent`](../commands/sendevent/overview.md) comando per inviare sia le visualizzazioni di pagina che il tracciamento dei collegamenti. I dati inclusi in un evento determinano se si tratta di [visualizzazione pagina](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/page-views) o un [evento pagina](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/page-events) in Adobe Analytics.

Per impostazione predefinita, tutti gli eventi sono considerati visualizzazioni di pagina in Adobe Analytics. Se desideri impostare un evento Web SDK su una chiamata di tracciamento dei collegamenti di Adobe Analytics, imposta i campi seguenti:

* **Oggetto XDM**: `xdm.web.webInteraction.name`, `web.webInteraction.type`, e `web.webInteraction.URL`
* **Oggetto dati**: `data.__adobe.analytics.linkName`, `data.__adobe.analytics.linkType`, e `data.__adobe.analytics.linkURL`
* **Dati contestuali**: non supportato

Consulta la [`tl()` metodo](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/tl-method) nella guida all’implementazione di Adobe Analytics per ulteriori informazioni.

Se si abilita [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) nel `configure` , questi campi vengono compilati automaticamente.

+++

+++In che modo un flusso di dati differenzia i dati da altri servizi con i dati destinati ad Adobe Analytics?

Tutti gli eventi inviati a un flusso di dati vengono passati a tutti i servizi configurati. Ad esempio, se effettui chiamate separate per la personalizzazione e Analytics, entrambi gli eventi vengono inviati ad Analytics e Target. Questi eventi vengono registrati nei rapporti di Analytics e possono influenzare metriche quali il tasso di mancato recapito.

Se utilizzi l’SDK per web, in genere queste chiamate vengono combinate in [`sendEvent`](../commands/sendevent/overview.md) comando.

+++
