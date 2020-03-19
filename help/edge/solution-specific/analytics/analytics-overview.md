---
title: Invio di dati ad Adobe Analytics
seo-title: Invio di dati ad Adobe Analytics con Adobe Experience Platform Web SDK
description: Scopri come inviare dati ad Adobe Analytics con l’SDK Web della piattaforma Experience
seo-description: Scopri come inviare dati ad Adobe Analytics con l’SDK Web della piattaforma Experience
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Invio di dati ad Adobe Analytics

>[!IMPORTANT]
>
>L’SDK Web per Adobe Experience Platform è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e la funzionalità sono soggette a modifiche.

L’SDK Web di Adobe Experience Platform può inviare dati ad Adobe Analytics. Questo funziona traducendo `xdm` in un formato utilizzabile da Adobe Analytics.

## Configurazione

Adobe Analytics raccoglie automaticamente i dati che stai inviando se hai una suite di rapporti mappata nell&#39;interfaccia utente di configurazione del cliente. Qui puoi mappare uno o più rapporti su una determinata configurazione. Una volta mappata una suite di rapporti, i dati inizieranno automaticamente a scorrere.

## Dati mappati automaticamente

Adobe Experience Platform Edge Network mappa automaticamente molte variabili XDM. L&#39;elenco completo delle variabili mappate automaticamente è elencato [qui](../analytics/automatically-mapped-vars.md).

## Dati mappati manualmente

Tutti i dati raccolti dalla rete Edge sono accessibili tramite regole di elaborazione. I dati vengono appiattiti utilizzando la notazione del punto e sono disponibili come contextData.

Se si aveva uno schema simile a questo.

```javascript
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    v1,
    v2,
    v3
  ],
  arrayofobjects:[
    {
      obj1key:objval1
    },
    {
      obj2key:objval2
    }
  ]
}
```

Queste sono quindi le chiavi dei dati contestuali a tua disposizione.

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array[0] //v1
a.x.array[1] //v2
a.x.array[3] //v3
a.x.arrayofobjects[1].obj1key //objval1
a.x.arrayofobjects[2].obj2key //objval2
```

Esempio di una regola di elaborazione che utilizzerebbe questi dati.

![Interfaccia delle regole di elaborazione](../../../assets/edge_analytics_processing_rules.png)
