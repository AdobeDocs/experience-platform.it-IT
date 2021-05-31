---
title: Mappatura manuale delle variabili Adobe Analytics nell’SDK web di Adobe Experience Platform
description: Scopri come mappare manualmente le variabili in Adobe Analytics utilizzando le regole di elaborazione nell’SDK per web di Experience Platform.
seo-description: Mappare manualmente le variabili in Adobe Analytics utilizzando le regole di elaborazione con SDK per web
keywords: adobe analytics;analytics;variabili;variabili di mappatura;variabili di mappatura;dati contestuali;dati contestuali;regole di elaborazione;regole;xdm;schema;
exl-id: 395050c1-8d39-4da8-acea-6e618ed662dd
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# Mappatura manuale delle variabili in Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] può mappare automaticamente determinate variabili, ma le variabili personalizzate devono essere mappate manualmente.

Per i dati XDM non mappati automaticamente su [!DNL Analytics], puoi utilizzare [dati contestuali](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html) per corrispondere al tuo [schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html). Quindi può essere mappato in [!DNL Analytics] utilizzando [regole di elaborazione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) per popolare le variabili [!DNL Analytics].

Inoltre, puoi utilizzare un set predefinito di azioni ed elenchi di prodotti per inviare o recuperare dati con Adobe Experience Platform Web SDK. A questo scopo, consulta [Prodotti](https://experienceleague.adobe.com/docs/experience-platform/edge/implement/commerce.html).

## Dati contestuali

I dati XDM vengono appiattiti utilizzando la notazione del punto e resi disponibili come `contextData`. [!DNL Analytics] Il seguente elenco di coppie di valori mostra un esempio di `context data`:

```json
{
  "bh": "900",
  "bw": "1680",
  "c": "24",
  "c.a.d.key.[0]": "value1",
  "c.a.d.key.[1]": "value2",
  "c.a.d.object.key1": "value1",
  "c.a.d.object.key2.[0]": "value2",
  "c.a.x.environment.browserdetails.javascriptenabled": "true",
  "c.a.x.environment.type": "browser",
  "cust_hit_time_gmt": "1579781427",
  "g": "http://example.com/home",
  "gn": "home",
  "j": "1.8.5",
  "k": "Y",
  "s": "1680x1050",
  "tnta": "218287:1:0|0,218287:1:0|2,218287:1:0|1,218287:1:0|32767,218287:1:0|1,218287:1:0|0,218287:1:0|1,218287:1:0|0,218287:1:0|1",
  "user_agent": "Mozilla/5.0 AppleWebKit/537.36 Safari/537.36",
  "v": "Y"
}
```

## Regole di elaborazione

Tutti i dati raccolti dalla rete Edge sono accessibili tramite [regole di elaborazione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). In [!DNL Analytics] puoi utilizzare le regole di elaborazione per incorporare i dati contestuali nelle variabili [!DNL Analytics].

Ad esempio, nella regola seguente, Adobe Analytics è impostato per compilare **Termini di ricerca interna (eVar2)** con i dati associati a **a.x._atag.search.term(Dati contestuali)**.

![](assets/examplerule.png)


## Schema XDM

Adobe Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i diversi sistemi, diventa più facile mantenere il significato e, quindi, ottenere valore dai dati. [!DNL Analytics] i dati contestuali funzionano con la struttura definita dallo schema.

L&#39;esempio seguente mostra come il comando [`event`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html) può essere utilizzato con l&#39;opzione `xdm` per inviare e recuperare dati con Adobe Experience Platform Web SDK. In questo esempio, il comando `event` corrisponde allo schema [Dettagli Commerce di ExperienceEvent](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) in modo che i valori productListItems `name` e `SKU` siano tracciati:


```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large Field Hat",
      },
      {
        "SKU":"HT104",
        "name":"Small Field Hat",
      }
    ]
  }
});
```

Per ulteriori informazioni sul tracciamento degli eventi con Adobe Experience Platform [!DNL Web SDK], consulta [Tracciamento degli eventi](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html).
