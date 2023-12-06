---
title: Mappatura manuale delle variabili di Adobe Analytics in Adobe Experience Platform Web SDK
description: Scopri come mappare manualmente le variabili in Adobe Analytics utilizzando le regole di elaborazione in Experienci Platform Web SDK.
seo-description: Manually map variables into Adobe Analytics using processing rules with Web SDK
keywords: adobe analytics;analisi;variabili;mappatura variabili;mappatura variabili;contextData;context Data;Processing rules;rules;xdm;schema;
exl-id: 395050c1-8d39-4da8-acea-6e618ed662dd
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 1%

---

# Mappatura manuale delle variabili in Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] può mappare automaticamente alcune variabili, ma le variabili personalizzate devono essere mappate manualmente.

Per i dati XDM che non vengono mappati automaticamente su [!DNL Analytics], è possibile utilizzare [dati contestuali](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=it) per corrispondere al tuo [schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=it). Quindi può essere mappato in [!DNL Analytics] utilizzo [regole di elaborazione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) per compilare [!DNL Analytics] variabili.

Inoltre, puoi utilizzare un set predefinito di azioni ed elenchi di prodotti per inviare o recuperare dati con Adobe Experience Platform Web SDK. Per farlo, consulta [Raccogliere informazioni su prodotti e commercio](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html).

## Dati contestuali

Da utilizzare per [!DNL Analytics], i dati XDM vengono appiattiti utilizzando la notazione del punto e resi disponibili come `contextData`. Il seguente elenco di coppie di valori mostra un esempio di ciò che `context data` si presenta come quando viene appiattito:

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

Tutti i dati raccolti dalla rete Edge sono accessibili tramite [regole di elaborazione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). In entrata [!DNL Analytics], è possibile utilizzare le regole di elaborazione per incorporare i dati contestuali in [!DNL Analytics] variabili.

Ad esempio, nella regola seguente, Adobe Analytics è impostato per compilare **Termini di ricerca interni (eVar2)** con i dati associati a **a.x._atag.search.term(Context Data)**.

![Immagine dell’interfaccia utente di Analytics che mostra un esempio di regola.](assets/examplerule.png)

## Schema XDM

Adobe Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i sistemi, diventa più semplice mantenere un significato e, quindi, ottenere valore dai dati. [!DNL Analytics] i dati contestuali funzionano con la struttura definita dallo schema.

Nell&#39;esempio seguente viene illustrato come [`event` comando](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html) può essere utilizzato con `xdm` per inviare e recuperare dati con Adobe Experience Platform Web SDK. In questo esempio, la proprietà `event` il comando corrisponde al [Schema dei dettagli di ExperienceEvent Commerce](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) affinché productListItems `name` e `SKU` i valori vengono tracciati:


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

Per ulteriori informazioni sul tracciamento degli eventi con Adobe Experience Platform [!DNL Web SDK], vedi [Tracciamento degli eventi](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html).
