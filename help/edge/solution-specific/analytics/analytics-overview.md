---
title: Invio di dati a  Adobe Analytics
seo-title: Invio di dati a  Adobe Analytics con Adobe Experience Platform Web SDK
description: Scopri come inviare dati a  Adobe Analytics con  Experience Platform Web SDK
seo-description: Scopri come inviare dati a  Adobe Analytics con  Experience Platform Web SDK
keywords: adobe analytics;analytics;mapped data;mapped vars;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Invio di dati a  Adobe Analytics

L&#39;Adobe Experience Platform [!DNL Web SDK] può inviare dati a  Adobe Analytics. Questo funziona traducendo `xdm` in un formato che l&#39;Adobe Analytics  può usare.

## Configurazione

 Adobe Analytics recupera automaticamente i dati che stai inviando se hai una suite di rapporti mappata nell&#39;interfaccia utente di configurazione del cliente. Qui puoi mappare uno o più rapporti su una determinata configurazione. Una volta mappata una suite di rapporti, i dati inizieranno automaticamente a scorrere.

## Dati mappati automaticamente

Adobe Experience Platform mappa [!DNL Edge Network] automaticamente molte variabili XDM. L&#39;elenco completo delle variabili mappate automaticamente è elencato [qui](../analytics/automatically-mapped-vars.md).

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

Queste sono quindi le chiavi dei dati contestuali a tua disposizione.

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

Esempio di una regola di elaborazione che utilizzerebbe questi dati.

![Interfaccia delle regole di elaborazione](../../../assets/edge_analytics_processing_rules.png)
