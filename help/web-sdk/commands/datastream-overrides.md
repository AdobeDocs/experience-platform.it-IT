---
title: Override della configurazione dello stream di dati
description: Scopri come configurare le sostituzioni dello stream di dati tramite Web SDK.
source-git-commit: 9cb46957a1c9755dcad6279aae5f5cc04eb6b305
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 14%

---


# Configurare gli override dello stream di dati

Il `edgeConfigOverrides` object consente di ignorare le impostazioni di configurazione per i comandi eseguiti nella pagina corrente. Questo oggetto override non è un comando, ma un oggetto che è possibile includere nella maggior parte dei comandi dell&#39;SDK Web.

Questo oggetto è utile quando si dispone di siti web o sottodomini diversi per paesi diversi o se si dispone di più sandbox di Experience Platform per memorizzare dati specifici per diverse business unit.

>[!IMPORTANT]
>
>Per istruzioni di configurazione end-to-end dettagliate per le sostituzioni dello stream di dati, consulta [sostituzioni della configurazione dello stream di dati](../../datastreams/overrides.md#configure-overrides) documentazione.

La sostituzione della configurazione dello stream di dati è un processo in due fasi:

1. Innanzitutto, devi definire la sostituzione della configurazione dello stream di dati in [pagina di configurazione dello stream di dati](../../datastreams/configure.md), nell’interfaccia utente per gli stream di dati. Consulta la [sostituzioni della configurazione dello stream di dati](../../datastreams/overrides.md#configure-overrides) documentazione per istruzioni su come configurare le sostituzioni.
2. Dopo aver configurato la sostituzione dello stream di dati nell’interfaccia utente, è necessario inviare le sostituzioni alla rete Edge in uno dei seguenti modi:
   * Tramite l’SDK web [estensione tag](#tag-extension).
   * Attraverso il `sendEvent` o `configure` Comandi dell’SDK per web.
   * Tramite Mobile SDK `sendEvent` comando.

Se imposti le sostituzioni sia nella configurazione dell’SDK web che in un comando specifico (ad esempio [`sendEvent`](sendevent/overview.md)), le sostituzioni nel comando specifico hanno la priorità.

## Proprietà oggetto

In questo oggetto sono disponibili le seguenti proprietà:

* **Sostituzione dello stream di dati**: invia chiamate a un diverso stream di dati. Se imposti questo valore, altre sostituzioni che richiedono la configurazione dello stream di dati devono essere configurate qui nello stream di dati impostato.
* **Contenitore di sincronizzazione ID di terze parti**: ID del contenitore di sincronizzazione ID di terze parti di destinazione in Adobe Audience Manager. Prima di utilizzare questo campo, è necessario configurare una sostituzione del contenitore ID di terze parti nelle impostazioni del flusso di dati.
* **Token proprietà di destinazione**: token per la proprietà di destinazione in Adobe Target. Prima di utilizzare questo campo, è necessario configurare una sostituzione del token di proprietà Target nelle impostazioni del flusso di dati.
* **Suite di rapporti**: ID suite di rapporti da escludere in Adobe Analytics. Prima di utilizzare questo campo, è necessario configurare le sostituzioni della suite di rapporti nelle impostazioni del flusso di dati.

## Inviare le sostituzioni dello stream di dati a Edge Network tramite l’estensione tag Web SDK {#tag-extension}

Consulta la documentazione su [configurazione delle sostituzioni dello stream di dati](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#datastrea-overrides) dall’estensione tag Web SDK per istruzioni di configurazione dettagliate.

Se desideri configurare le sostituzioni dello stream di dati dall’estensione tag Web SDK, imposta ogni campo desiderato in **[!UICONTROL Override della configurazione dello stream di dati]** quando [configurazione dell’estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** il [!UICONTROL Adobe Experience Platform Web SDK] Card.
1. Scorri verso il basso fino a **[!UICONTROL Override della configurazione dello stream di dati]** sezione. Imposta ogni valore di sostituzione desiderato.
1. Clic **[!UICONTROL Salva]**, quindi pubblica le modifiche.

Se desideri impostare le sostituzioni solo per un comando specifico, imposta ogni campo desiderato all’interno delle azioni di una regola di tag.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. Sotto [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il [!UICONTROL Estensione] campo a discesa per **[!UICONTROL Adobe Experience Platform Web SDK]**, e impostare [!UICONTROL Tipo di azione] a **[!UICONTROL Invia evento]**.
1. Scorri verso il basso fino alla sezione etichettata **[!UICONTROL Override della configurazione dello stream di dati]**.
1. Imposta ogni campo in questa sezione sul valore di sostituzione desiderato.
1. Clic **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

Sono forniti campi separati per [!UICONTROL Sviluppo], [!UICONTROL Staging], e [!UICONTROL Produzione] ambienti. Assicurati di compilare ogni campo desiderato per ogni ambiente.

## Inviare le sostituzioni alla rete Edge tramite la libreria JavaScript dell’SDK per web {#library}

Dopo [configurazione delle sostituzioni dello stream di dati](../../datastreams/overrides.md) Nell’interfaccia utente di Data Collection, ora puoi inviare le sostituzioni alla rete Edge, tramite la libreria JavaScript dell’SDK Web.

Se utilizzi Web SDK, inviare le sostituzioni alla rete Edge tramite `edgeConfigOverrides` Il comando è il secondo e ultimo passaggio dell’attivazione delle sostituzioni della configurazione dello stream di dati.

Gli override della configurazione dello stream di dati vengono inviati alla rete Edge tramite il comando `edgeConfigOverrides` di Web SDK. Questo comando crea le sostituzioni dello stream di dati che vengono passate al [!DNL Edge Network] al comando successivo. Se utilizzi il `configure` , le sostituzioni vengono passate per ogni richiesta.

Il `edgeConfigOverrides` crea le sostituzioni dello stream di dati che vengono passate al [!DNL Edge Network] al comando successivo.

Quando viene inviato un override di configurazione con il comando `configure`, viene incluso nei seguenti comandi di Web SDK.

* [sendEvent](../commands/sendevent/overview.md)
* [setConsent](../commands/setconsent.md)
* [getIdentity](../commands/getidentity.md)
* [appendIdentityToUrl](../commands/appendidentitytourl.md)
* [configure](../commands/configure/overview.md)

Le opzioni specificate a livello globale possono essere ignorate dall’opzione di configurazione relativa ai singoli comandi.

### Inviare sostituzioni di configurazione tramite Web SDK `sendEvent` comando {#send-event}

L’esempio seguente mostra l’aspetto di un override della configurazione con un comando `sendEvent`.

```js {line-numbers="true" highlight="5-25"}
alloy("sendEvent", {
  xdm: {
    /* ... */
  },
  edgeConfigOverrides: {
    datastreamId: "{DATASTREAM_ID}"
    com_adobe_experience_platform: {
      datasets: {
        event: {
          datasetId: "SampleEventDatasetIdOverride"
        }
      }
    },
    com_adobe_analytics: {
      reportSuites: [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
        ]
    },
    com_adobe_identity: {
      idSyncContainerId: "1234567"
    },
    com_adobe_target: {
      propertyToken: "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  }
});
```

| Parametro | Descrizione |
|---|---|
| `edgeConfigOverrides.datastreamId` | Utilizza questo parametro per consentire a una singola richiesta di passare a uno stream di dati diverso da quello definito dal comando `configure`. |
| `com_adobe_analytics.reportSuites[]` | Array di stringhe che determina a quali suite di rapporti inviare dati di Analytics. |
| `com_adobe_identity.idSyncContainerId` | Il contenitore di sincronizzazione ID di terze parti che desideri utilizzare in Audienci Manager. |
| `com_adobe_target.propertyToken` | Token per la proprietà di destinazione Adobe Target. |

### Inviare sostituzioni di configurazione tramite Web SDK `configure` comando {#send-configure}

L’esempio seguente mostra l’aspetto di un override della configurazione con un comando `configure`.

```js {line-numbers="true" highlight="8-30"}
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "etc",
  edgeBasePath: "ee",
  datastreamId: "{DATASTREAM_ID}",
  orgId: "org",
  debugEnabled: true,
  edgeConfigOverrides: {
    "com_adobe_experience_platform": {
      "datasets": {
        "event": {
          datasetId: "SampleProfileDatasetIdOverride"
        }
      }
    },
    "com_adobe_analytics": {
      "reportSuites": [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
      ]
    },
    "com_adobe_identity": {
      "idSyncContainerId": "1234567"
    },
    "com_adobe_target": {
      "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  },
  onBeforeEventSend: function() { /* … */ });
};
```

| Parametro | Descrizione |
|---|---|
| `edgeConfigOverrides.datastreamId` | Utilizza questo parametro per consentire a una singola richiesta di passare a uno stream di dati diverso da quello definito dal comando `configure`. |
| `com_adobe_analytics.reportSuites[]` | Array di stringhe che determina a quali suite di rapporti inviare dati di Analytics. |
| `com_adobe_identity.idSyncContainerId` | Il contenitore di sincronizzazione ID di terze parti che desideri utilizzare in Audienci Manager. |
| `com_adobe_target.propertyToken` | Token per la proprietà di destinazione Adobe Target. |