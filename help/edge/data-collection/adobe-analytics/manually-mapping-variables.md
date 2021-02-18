---
title: Mappatura manuale  variabili Adobe Analytics nell’SDK per Adobe Experience Platform Web
description: Scoprite come mappare manualmente le variabili in  Adobe Analytics utilizzando le regole di elaborazione nell’SDK Web del Experience Platform .
seo-description: Mappatura manuale delle variabili in  Adobe Analytics tramite regole di elaborazione con Web SDK
keywords: adobe analytics;analytics;variables;mapping variables;map variables;contextData;context Data;Processing rules;rules;xdm;schema;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# Mappatura manuale delle variabili in  Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] può mappare automaticamente determinate variabili, ma queste devono essere mappate manualmente.

Per i dati XDM non mappati automaticamente su [!DNL Analytics], è possibile utilizzare [dati contestuali](https://docs.adobe.com/content/help/en/analytics/implementation/vars/page-vars/contextdata.html) per corrispondere allo [schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html). Quindi può essere mappato in [!DNL Analytics] utilizzando [regole di elaborazione](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) per compilare le variabili [!DNL Analytics].

È inoltre possibile utilizzare un set predefinito di azioni ed elenchi di prodotti per inviare o recuperare dati con Adobe Experience Platform Web SDK. A tale scopo, vedere [Products](https://docs.adobe.com/content/help/en/experience-platform/edge/implement/commerce.html).

## Dati contestuali

Per essere utilizzati da [!DNL Analytics], i dati XDM vengono appiattiti utilizzando la notazione del punto e resi disponibili come `contextData`. Il seguente elenco di coppie di valori mostra un esempio di `context data`:

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

Tutti i dati raccolti dalla rete Edge sono accessibili tramite [regole di elaborazione](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). In [!DNL Analytics], puoi utilizzare le regole di elaborazione per incorporare dati contestuali nelle variabili [!DNL Analytics].

Ad esempio, nella regola seguente,  Adobe Analytics è impostato per compilare i termini di ricerca interna ( eVar2)**con i dati associati a** a.x._atag.search.term(Context Data)**.**

![](assets/examplerule.png)


## schema XDM

Adobe Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i diversi sistemi, diventa più semplice mantenere il significato e, di conseguenza, ottenere valore dai dati. [!DNL Analytics] i dati contestuali funzionano con la struttura definita dallo schema.

L&#39;esempio seguente mostra come il comando [`event`](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html) possa essere utilizzato con l&#39;opzione `xdm` per inviare e recuperare dati con Adobe Experience Platform Web SDK. In questo esempio, il comando `event` corrisponde allo schema [ExperienceEvent Commerce Details](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) in modo che i valori productListItems `name` e `SKU` siano tracciati:


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

Per ulteriori informazioni sul tracciamento degli eventi con Adobe Experience Platform [!DNL Web SDK], vedere [Eventi di tracciamento](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html).
