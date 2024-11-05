---
title: Override della configurazione dello stream di dati
description: Scopri come configurare le sostituzioni dello stream di dati tramite Web SDK.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: 2b8ca4bc1d5cf896820a5de95dcdfcd15edc2392
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 10%

---

# Configurare gli override dello stream di dati

L&#39;oggetto `edgeConfigOverrides` consente di ignorare le impostazioni di configurazione per i comandi eseguiti nella pagina corrente. Questo oggetto override non è un comando, ma un oggetto che è possibile includere nella maggior parte dei comandi dell&#39;SDK Web.

Questo oggetto è utile quando si dispone di siti web o sottodomini diversi per paesi diversi o se si dispone di più sandbox di Experience Platform per memorizzare dati specifici per diverse business unit.

>[!IMPORTANT]
>
>Per istruzioni di configurazione end-to-end dettagliate per le sostituzioni dello stream di dati, consulta la documentazione sulle [sostituzioni della configurazione dello stream di dati](../../datastreams/overrides.md#configure-overrides).

La sostituzione della configurazione dello stream di dati è un processo in due fasi:

1. Innanzitutto, devi definire la sostituzione della configurazione dello stream di dati nella [pagina di configurazione dello stream di dati](../../datastreams/configure.md), nell&#39;interfaccia utente dello stream di dati. Per istruzioni su come configurare le sostituzioni, consulta la documentazione sulle [sostituzioni della configurazione dello stream di dati](../../datastreams/overrides.md#configure-overrides).
2. Dopo aver configurato la sostituzione dello stream di dati nell’interfaccia utente, è necessario inviare le sostituzioni all’Edge Network in uno dei seguenti modi:
   * Tramite l&#39;estensione tag [Web SDK](#tag-extension).
   * Tramite i comandi Web SDK di [`sendEvent`](../commands/sendevent/overview.md) o [`configure`](../commands/configure/overview.md).
   * Tramite il comando Mobile SDK [`sendEvent`](https://developer.adobe.com/client-sdks/home/getting-started/track-events/#send-events-to-edge-network).

Se imposti le sostituzioni sia nella configurazione dell&#39;SDK Web che in un comando specifico (ad esempio [`sendEvent`](sendevent/overview.md)), le sostituzioni nel comando specifico hanno la priorità.

>[!NOTE]
>
>Se desideri che la configurazione sostituisca *disable* un servizio Experience Cloud, assicurati che il servizio sia il primo *enabled* nella configurazione dello stream di dati. Per informazioni dettagliate su come aggiungere servizi a un flusso di dati, consulta la documentazione su come [configurare i flussi di dati](../../datastreams/configure.md#add-services).

## Inviare le sostituzioni dello stream di dati all’Edge Network tramite l’estensione tag Web SDK {#tag-extension}

Per istruzioni di configurazione dettagliate, consulta la documentazione su [configurazione delle sostituzioni dello stream di dati](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#datastrea-overrides) dall&#39;estensione tag Web SDK.

Se desideri configurare le sostituzioni dello stream di dati dall&#39;estensione tag Web SDK, imposta ogni campo desiderato in **[!UICONTROL Sostituzioni della configurazione dello stream di dati]** durante [la configurazione dell&#39;estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione **[!UICONTROL Override della configurazione dello stream di dati]**. Imposta ogni valore di sostituzione desiderato.
1. Fai clic su **[!UICONTROL Salva]**, quindi pubblica le modifiche.

Se desideri impostare le sostituzioni solo per un comando specifico, imposta ogni campo desiderato all’interno delle azioni di una regola di tag.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il campo a discesa [!UICONTROL Estensione] su **[!UICONTROL Adobe Experience Platform Web SDK]** e imposta [!UICONTROL Tipo azione] su **[!UICONTROL Invia evento]**.
1. Scorri verso il basso fino alla sezione con etichetta **[!UICONTROL Override della configurazione dello stream di dati]**.
1. Imposta ogni campo in questa sezione sul valore di sostituzione desiderato.
1. Fai clic su **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

Sono stati forniti campi separati per gli ambienti [!UICONTROL Sviluppo], [!UICONTROL Gestione temporanea] e [!UICONTROL Produzione]. Assicurati di compilare ogni campo desiderato per ogni ambiente.

## Inviare le sostituzioni all’Edge Network tramite la libreria JavaScript dell’SDK web {#library}

Dopo [aver configurato le sostituzioni dello stream di dati](../../datastreams/overrides.md) nell&#39;interfaccia utente di Data Collection, ora puoi inviare le sostituzioni all&#39;Edge Network tramite la libreria JavaScript dell&#39;SDK Web.

Se utilizzi Web SDK, l&#39;invio delle sostituzioni all&#39;Edge Network tramite il comando `edgeConfigOverrides` è il secondo e ultimo passaggio dell&#39;attivazione delle sostituzioni della configurazione dello stream di dati.

Gli override della configurazione dello stream di dati vengono inviati alla rete Edge tramite il comando `edgeConfigOverrides` di Web SDK. Questo comando crea le sostituzioni dello stream di dati passate a [!DNL Edge Network] nel comando successivo. Se si utilizza il comando `configure`, le sostituzioni vengono passate per ogni richiesta.

Il comando `edgeConfigOverrides` crea le sostituzioni dello stream di dati che vengono passate a [!DNL Edge Network] nel comando successivo.

Quando viene inviato un override di configurazione con il comando `configure`, viene incluso nei seguenti comandi di Web SDK.

* [sendEvent](../commands/sendevent/overview.md)
* [setConsent](../commands/setconsent.md)
* [getIdentity](../commands/getidentity.md)
* [appendIdentityToUrl](../commands/appendidentitytourl.md)
* [configure](../commands/configure/overview.md)

Le opzioni specificate a livello globale possono essere ignorate dall’opzione di configurazione relativa ai singoli comandi.

### Invia sostituzioni di configurazione tramite il comando Web SDK `sendEvent` {#send-event}

L&#39;esempio seguente mostra tutte le opzioni di configurazione dello stream di dati dinamici supportate in una chiamata `sendEvent`.

Se nella configurazione dello stream di dati sono abilitati tutti i servizi supportati, l&#39;esempio seguente sovrascriverà questa impostazione e disabiliterà tutti i servizi (vedi l&#39;impostazione `enabled: false` su ciascun servizio).

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
      reportSuites: ["ujslconfigoverrides3"],
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

| Parametro | Descrizione |
|---|---|
| `renderDecisions` |  |
| `edgeConfigOverrides.datastreamId` | Utilizza questo parametro per consentire a una singola richiesta di passare a uno stream di dati diverso da quello definito dal comando `configure`. |
| `edgeConfigOverrides.com_adobe_experience_platform` | Definisce la configurazione dello stream di dati dinamico per il servizio Experience Platform. |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | Definisce se l’evento verrà inviato o meno al servizio Experience Platform. |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | Definisce i set di dati utilizzati per l’evento. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | Definisce se l’evento viene inviato o meno al servizio Offer Decisioning. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | Definisce se l’evento viene inviato o meno al servizio di segmentazione Edge. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | Definisce se i dati dell’evento vengono inviati o meno alle destinazioni edge. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | Definisce se i dati dell’evento vengono inviati o meno al servizio Adobe Journey Optimizer. |
| `com_adobe_analytics.enabled` | Definisce se i dati dell’evento vengono inviati o meno ad Adobe Analytics. |
| `com_adobe_analytics.reportSuites[]` | Array di stringhe che determina a quali suite di rapporti desideri inviare dati di Analytics. |
| `com_adobe_identity.idSyncContainerId` | Il contenitore di sincronizzazione ID di terze parti che desideri utilizzare in Audience Manager. Affinché questo contenitore di sincronizzazione ID funzioni, è necessario impostare `com_adobe_audience_manager.enabled` su `true`. In caso contrario, il servizio Audience Manager è disabilitato. |
| `com_adobe_target.enabled` | Definisce se i dati dell’evento vengono inviati ad Adobe Target. |
| `com_adobe_target.propertyToken` | Token per la proprietà di destinazione Adobe Target. |
| `com_adobe_audience_manager.enabled` | Definisce se i dati dell’evento vengono inviati al servizio Audience Manager. |
| `com_adobe_launch_ssf` | Definisce se i dati dell&#39;evento vengono inviati all&#39;inoltro lato server. |

### Invia sostituzioni di configurazione tramite il comando Web SDK `configure` {#send-configure}

L’esempio seguente mostra l’aspetto di un override della configurazione con un comando `configure`.

Se nella configurazione dello stream di dati sono abilitati tutti i servizi supportati, l&#39;esempio seguente sovrascriverà questa impostazione e disabiliterà tutti i servizi (vedi l&#39;impostazione `enabled: false` su ciascun servizio).

```js
alloy("configure", {
  orgId: "97D1F3F459CE0AD80A495CBE@AdobeOrg",
  datastreamId: "db9c70a1-6f11-4563-b0e9-b5964ab3a858",
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f930753dd41ca8d4fd77",
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
      reportSuites: ["ujslconfigoverrides2"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34373,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "01dbc634-07c1-d8f9-ca69-b489a5ac5e94",
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

| Parametro | Descrizione |
|---|---|
| `orgId` | L’ID dell’organizzazione IMS corrispondente al tuo account Adobe. |
| `edgeConfigOverrides.datastreamId` | Utilizza questo parametro per consentire a una singola richiesta di passare a uno stream di dati diverso da quello definito dal comando `configure`. |
| `edgeConfigOverrides.com_adobe_experience_platform` | Definisce la configurazione dello stream di dati dinamico per il servizio Experience Platform. |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | Definisce se l’evento verrà inviato o meno al servizio Experience Platform. |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | Definisce i set di dati utilizzati per l’evento. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | Definisce se l’evento viene inviato o meno al servizio Offer Decisioning. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | Definisce se l’evento viene inviato o meno al servizio di segmentazione Edge. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | Definisce se i dati dell’evento vengono inviati o meno alle destinazioni edge. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | Definisce se i dati dell’evento vengono inviati o meno al servizio Adobe Journey Optimizer. |
| `com_adobe_analytics.enabled` | Definisce se i dati dell’evento vengono inviati o meno ad Adobe Analytics. |
| `com_adobe_analytics.reportSuites[]` | Array di stringhe che determina a quali suite di rapporti desideri inviare dati di Analytics. |
| `com_adobe_identity.idSyncContainerId` | Il contenitore di sincronizzazione ID di terze parti che desideri utilizzare in Audience Manager. Affinché questo contenitore di sincronizzazione ID funzioni, è necessario impostare `com_adobe_audience_manager.enabled` su `true`. In caso contrario, il servizio Audience Manager è disabilitato. |
| `com_adobe_target.enabled` | Definisce se i dati dell’evento vengono inviati ad Adobe Target. |
| `com_adobe_target.propertyToken` | Token per la proprietà di destinazione Adobe Target. |
| `com_adobe_audience_manager.enabled` | Definisce se i dati dell’evento vengono inviati al servizio Audience Manager. |
| `com_adobe_launch_ssf` | Definisce se i dati dell&#39;evento vengono inviati all&#39;inoltro lato server. |

