---
title: Mappatura manuale delle variabili in  Analytics
seo-title: Mappatura manuale delle variabili in  Analytics con SDK Web
description: Come mappare manualmente le variabili in  Analytics utilizzando le regole di elaborazione
seo-description: mappare manualmente le variabili in  Analytics utilizzando le regole di elaborazione con SDK Web
translation-type: tm+mt
source-git-commit: 71193ad346c3976f80b14ee0d6e5b12055a17473
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---


# Mappatura manuale delle variabili in  Analytics

L’SDK Web per Adobi Experience Platform  (AEP) può mappare automaticamente determinate variabili, ma queste devono essere mappate manualmente.

Per i dati XDM non mappati automaticamente a  Analytics, è possibile utilizzare i dati [](https://docs.adobe.com/content/help/en/analytics/implementation/vars/page-vars/contextdata.html) contestuali per corrispondere allo [schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html). Quindi può essere mappato in  Analytics utilizzando le regole [di](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) elaborazione per compilare  variabili Analytics.

Potete inoltre utilizzare un set predefinito di azioni ed elenchi di prodotti per inviare o recuperare dati con l’SDK Web AEP. Per eseguire questa operazione, vedi [Prodotti](https://docs.adobe.com/content/help/en/experience-platform/edge/implement/commerce.html).

## Dati contestuali

Per essere utilizzati da  Analytics, i dati XDM vengono appiattiti mediante la notazione del punto e resi disponibili come `contextData`. Il seguente elenco di coppie di valori mostra un esempio di `context data`:

```javascript
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

Tutti i dati raccolti dalla rete edge sono accessibili tramite regole [di](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html)elaborazione. In  Analytics, potete utilizzare le regole di elaborazione per incorporare i dati contestuali nelle variabili di Analytics .

Ad esempio, nella regola seguente,  Analytics è impostato per compilare i termini di ricerca **interna (eVar2)** con i dati associati a **a.x_atag.search.term(Context Data)**.

![](assets/examplerule.png)


## Schema XDM

 Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i diversi sistemi, diventa più semplice mantenere il significato e, di conseguenza, ottenere valore dai dati.  i dati contestuali di Analytics funzionano con la struttura definita dallo schema.

L’esempio seguente mostra come [`event` il comando](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html) può essere utilizzato con l’ `xdm` opzione per inviare e recuperare dati con l’SDK Web AEP. In questo esempio, il `event` comando corrisponde allo schema [Dettagli](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) ExperienceEvent Commerce in modo che i valori e gli elementi productListItems `name` `SKU` siano tracciati:


```
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

Per ulteriori informazioni sul tracciamento degli eventi con AEP Web SDK, vedi [Tracciamento degli eventi](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html).
