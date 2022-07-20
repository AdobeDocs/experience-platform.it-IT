---
title: Utilizzo di Adobe Analytics con Platform Web SDK
description: Scopri come inviare dati ad Adobe Analytics con Adobe Experience Platform Web SDK.
keywords: adobe analytics;analytics;dati mappati;variabili mappate;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: f627c1f6c917e74e0a366ce0611a1fa6bd0e3c3d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Utilizzo di Adobe Analytics con Platform Web SDK

Adobe Experience Platform [!DNL Web SDK] può inviare dati ad Adobe Analytics. Questo funziona traducendo `xdm` in un formato utilizzabile da Adobe Analytics.

## Configurazione

Se hai una suite di rapporti mappata nell&#39;interfaccia utente di configurazione cliente, Adobe Analytics raccoglie automaticamente i dati che stai inviando. Qui puoi mappare uno o più rapporti su una determinata configurazione. Una volta mappata una suite di rapporti, i dati inizieranno automaticamente a scorrere.

## Gruppo di campi XDM

Per facilitare l’acquisizione delle metriche Adobe Analytics più comuni, forniamo un gruppo di campi Analytics da utilizzare. Per ulteriori dettagli su questo schema, consulta la documentazione per [Gruppo di campi dello schema dell’estensione completa Adobe Analytics ExperienceEvent](../../../xdm/field-groups/event/analytics-full-extension.md)

## Dati mappati automaticamente

Adobe Experience Platform [!DNL Edge Network] mappa automaticamente molte variabili XDM. L&#39;elenco completo di queste variabili è elencato [qui](automatically-mapped-vars.md).

## Dati mappati manualmente

È possibile accedere a qualsiasi dato non mappato automaticamente dalla rete perimetrale tramite regole di elaborazione. I dati vengono appiattiti utilizzando la notazione del punto e sono disponibili come contextData.

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
