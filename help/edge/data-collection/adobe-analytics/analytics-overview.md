---
title: Invio di dati ad Adobe Analytics tramite Adobe Experience Platform Web SDK
description: Scopri come inviare dati ad Adobe Analytics con Adobe Experience Platform Web SDK.
keywords: adobe analytics;analytics;dati mappati;variabili mappate;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 3a1d08a4ea87ee3db7a2a8b048d5721fa679c372
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 0%

---

# Invio di dati ad Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] può inviare dati ad Adobe Analytics. Questo funziona traducendo `xdm` in un formato utilizzabile da Adobe Analytics.

## Configurazione

Se hai una suite di rapporti mappata nell&#39;interfaccia utente di configurazione cliente, Adobe Analytics raccoglie automaticamente i dati che stai inviando. Qui puoi mappare uno o più rapporti su una determinata configurazione. Una volta mappata una suite di rapporti, i dati inizieranno automaticamente a scorrere.

## Dati mappati automaticamente

Adobe Experience Platform [!DNL Edge Network] mappa automaticamente molte variabili XDM. L&#39;elenco completo di queste variabili è elencato [qui](automatically-mapped-vars.md).

## Dati mappati manualmente

Tutti i dati raccolti dalla rete perimetrale sono accessibili tramite regole di elaborazione. I dati vengono appiattiti utilizzando la notazione del punto e sono disponibili come contextData.

Se avevi uno schema simile a questo.

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

Queste sarebbero le chiavi dei dati contestuali a tua disposizione.

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

Ecco un esempio di regola di elaborazione che utilizzerebbe questi dati.

![Interfaccia delle regole di elaborazione](./assets/edge_analytics_processing_rules.png)
