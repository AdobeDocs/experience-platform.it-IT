---
title: edgeConfigOverrides
description: Configurare le sostituzioni dello stream di dati solo per il comando sendEvent.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# `edgeConfigOverrides` (`sendEvent` comando)

L&#39;oggetto `edgeConfigOverrides` consente di ignorare le impostazioni di configurazione solo per il comando `sendEvent` corrente. Questo oggetto è utile quando si dispone di comandi specifici sulla stessa pagina che si desidera eseguire con impostazioni di configurazione diverse rispetto al resto dell&#39;implementazione di Web SDK. Se si desidera ignorare le impostazioni di configurazione per tutti i comandi di una determinata pagina, provare a utilizzare l&#39;oggetto [`edgeConfigOverrides` nel comando `configure`](../configure/edgeconfigoverrides.md).

Il processo di sostituzione della configurazione del flusso di dati generale è costituito da due passaggi principali:

1. Innanzitutto, devi definire la sostituzione della configurazione dello stream di dati quando [configuri uno stream di dati](/help/datastreams/configure.md) nell&#39;interfaccia utente dello stream di dati. Per istruzioni su come configurare le sostituzioni, consulta [Le sostituzioni della configurazione dello stream di dati](/help/datastreams/overrides.md) nella documentazione dello stream di dati.
1. Dopo aver configurato l&#39;override dello stream di dati nell&#39;interfaccia utente dello stream di dati, puoi configurare l&#39;oggetto `edgeConfigOverrides`.

Il comando `configure` supporta anche un oggetto `edgeConfigOverrides`. Vedere [`edgeConfigOverrides`](../configure/edgeconfigoverrides.md) nel comando `configure`. L&#39;oggetto `edgeConfigOverrides` nel comando `sendEvent` ha la precedenza sull&#39;oggetto `edgeConfigOverrides` nel comando `configure` se entrambi sono impostati.

## Esempio

Se nella configurazione dello stream di dati sono abilitati tutti i servizi supportati, l&#39;esempio seguente sostituisce questa impostazione e disabilita tutti i servizi (vedi l&#39;impostazione `enabled: false` per ciascun servizio). Questo oggetto supporta le stesse proprietà dell&#39;oggetto [`edgeConfigOverrides`](../configure/edgeconfigoverrides.md) nel comando `configure`.

```js
alloy("sendEvent", {
  renderDecisions: true,
  edgeConfigOverrides: {
    datastreamId: "bfa8fe21-6157-42d3-b47a-78310920b39d",
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f949a8a6891ca8a28911",
        },
      },
      com_adobe_edge_ode: {
        enabled: false,
      },
      com_adobe_edge_segmentation: {
        enabled: false,
      },
      com_adobe_edge_destinations: {
        enabled: false,
      },
      com_adobe_edge_ajo: {
        enabled: false,
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["examplersid3"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34374,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "f3fd55e1-a06d-8650-9aa5-c8356c6e2223",
    },
    com_adobe_audience_manager: {
      enabled: false,
    },
    com_adobe_launch_ssf: {
      enabled: false,
    },
  },
});
```

## La configurazione dello stream di dati viene ignorata utilizzando l’estensione tag Web SDK

L&#39;equivalente dell&#39;estensione tag Web SDK di questo oggetto è la sezione [Override della configurazione Datastream](/help/tags/extensions/client/web-sdk/actions/send-event.md#datastream-configuration-overrides) durante la configurazione dell&#39;azione &#39;[!UICONTROL Send event]&#39;.
