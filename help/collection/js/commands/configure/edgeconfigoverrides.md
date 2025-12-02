---
title: edgeConfigOverrides
description: Configurare le sostituzioni dello stream di dati per l’implementazione.
source-git-commit: f4a2778c71ad6a48621212f3ece1776d1b3ac643
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# `edgeConfigOverrides` (`configure` comando)

L&#39;oggetto `edgeConfigOverrides` consente di ignorare le impostazioni di configurazione per i comandi eseguiti nella pagina corrente. Questo oggetto è utile quando si dispone di siti web o sottodomini diversi per paesi diversi o se si dispone di più sandbox di Experience Platform per memorizzare dati specifici per diverse business unit. Se si desidera ignorare le impostazioni di configurazione per un solo comando nella pagina, provare a utilizzare l&#39;oggetto [`edgeConfigOverrides` nel comando `sendEvent`](../sendevent/edgeconfigoverrides.md).

Il processo di sostituzione della configurazione dello stream di dati è costituito da due passaggi principali:

1. Innanzitutto, devi definire la sostituzione della configurazione dello stream di dati quando [configuri uno stream di dati](/help/datastreams/configure.md) nell&#39;interfaccia utente dello stream di dati. Per istruzioni su come configurare le sostituzioni, consulta [Le sostituzioni della configurazione dello stream di dati](/help/datastreams/overrides.md) nella documentazione dello stream di dati.
1. Dopo aver configurato l&#39;override dello stream di dati nell&#39;interfaccia utente dello stream di dati, puoi configurare l&#39;oggetto `edgeConfigOverrides`.

Quando si imposta l&#39;oggetto `edgeConfigOverrides` nel comando `configure`, viene applicato a tutti i dati inviati ad Adobe. I seguenti comandi _also_ supportano l&#39;oggetto `edgeConfigOverrides`:

* [`sendEvent`](../sendevent/edgeconfigoverrides.md)
* [&quot;setConsent&quot;](../setconsent.md)
* [&quot;getIdentity&quot;](../getidentity.md)
* [&quot;appendIdentityToUrl&quot;](../appendidentitytourl.md)

L&#39;impostazione di `edgeConfigOverrides` in uno qualsiasi dei comandi precedenti ha la precedenza sull&#39;oggetto `edgeConfigOverrides` nel comando `configure` se entrambi sono impostati. Se uno di questi comandi non contiene un oggetto `edgeConfigOverrides`, verrà utilizzato l&#39;oggetto `edgeConfigOverrides` nel comando `configure`.

## Esempio

Se nella configurazione dello stream di dati sono abilitati tutti i servizi supportati, l’esempio seguente sostituisce questa impostazione e disabilita tutti i servizi.

```js
alloy("configure", {
  orgId: "97D1F3F459CE0AD80A495CBE@AdobeOrg",
  datastreamId: "db9c70a1-6f11-4563-b0e9-b5964ab3a858",
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f930753dd41ca8d4fd77"
        }
      },
      com_adobe_edge_ode: {
        enabled: false
      },
      com_adobe_edge_segmentation: {
        enabled: false
      },
      com_adobe_edge_destinations: {
        enabled: false
      },
      com_adobe_edge_ajo: {
        enabled: false
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["exampleoverridersid","exampleoverridersid2"]
    },
    com_adobe_identity: {
      idSyncContainerId: 34373
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "01dbc634-07c1-d8f9-ca69-b489a5ac5e94"
    },
    com_adobe_audience_manager: {
      enabled: false
    },
    com_adobe_launch_ssf: {
      enabled: false
    }
  }
});
```

| Parametro | Tipo | Descrizione |
| --- | --- | --- |
| **`orgId`** | `string` | ID organizzazione IMS della tua azienda. |
| **`datastreamId`** | `string` | ID dello stream di dati a cui inviare i dati. |
| **`com_adobe_experience_platform`** | `object` | Definisce la configurazione dello stream di dati dinamico per i servizi Adobe Experience Platform. |
| **`com_adobe_experience_platform.enabled`** | `boolean` | Determina se l’evento viene inviato a Adobe Experience Platform. |
| **`com_adobe_experience_platform.datasets`** | `object` | Definisce i set di dati utilizzati per l’evento. |
| **`com_adobe_experience_platform.com_adobe_edge_ode.enabled`** | `boolean` | Determina se l’evento viene inviato ad Offer Decisioning. |
| **`com_adobe_experience_platform.com_adobe_edge_segmentation.enabled`** | `boolean` | Determina se l’evento viene inviato ad Edge Segmentation. |
| **`com_adobe_experience_platform.com_adobe_edge_destinations.enabled`** | `boolean` | Determina se l’evento viene inviato alle destinazioni Edge. |
| **`com_adobe_experience_platform.com_adobe_edge_ajo.enabled`** | `boolean` | Determina se l’evento viene inviato a Adobe Journey Optimizer. |
| **`com_adobe_analytics.enabled`** | `boolean` | Determina se l’evento viene inviato ad Adobe Analytics. |
| **`com_adobe_analytics.reportSuites[]`** | `string[]` | Array di stringhe che determina le suite di rapporti a cui inviare i dati di Analytics. |
| **`com_adobe_audience_manager.enabled`** | `boolean` | Determina se l’evento viene inviato a Adobe Audience Manager. |
| **`com_adobe_identity.idSyncContainerId`** | `integer` | Contenitore di terze parti per la sincronizzazione degli ID che desideri utilizzare in Audience Manager. Richiede `com_adobe_audience_manager.enabled` impostato su `true`. In caso contrario, il servizio Audience Manager è disabilitato. |
| **`com_adobe_target.enabled`** | `boolean` | Determina se l’evento viene inviato ad Adobe Target. |
| **`com_adobe_target.propertyToken`** | `string` | Token per la proprietà di destinazione Adobe Target. |
| **`com_adobe_launch_ssf`** | `boolean` | Determina se l&#39;evento viene inviato all&#39;inoltro lato server. |

## Sostituzioni della configurazione tramite l’estensione tag Web SDK

L&#39;equivalente dell&#39;estensione tag Web SDK di questo campo si trova in [Sostituzioni configurazione](/help/tags/extensions/client/web-sdk/configure/configuration-overrides.md) durante la configurazione dell&#39;estensione tag.
