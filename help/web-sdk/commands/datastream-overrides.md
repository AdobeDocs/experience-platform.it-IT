---
title: Override della configurazione dello stream di dati
description: Scopri come configurare le sostituzioni dello stream di dati tramite Web SDK.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 14%

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
   * Tramite i comandi Web SDK di `sendEvent` o `configure`.
   * Tramite il comando Mobile SDK `sendEvent`.

Se imposti le sostituzioni sia nella configurazione dell&#39;SDK Web che in un comando specifico (ad esempio [`sendEvent`](sendevent/overview.md)), le sostituzioni nel comando specifico hanno la priorità.

## Proprietà oggetto

In questo oggetto sono disponibili le seguenti proprietà:

* **Override dello stream di dati**: invia chiamate a uno stream di dati diverso. Se imposti questo valore, altre sostituzioni che richiedono la configurazione dello stream di dati devono essere configurate qui nello stream di dati impostato.
* **Contenitore di sincronizzazione ID di terze parti**: l&#39;ID del contenitore di sincronizzazione ID di terze parti di destinazione in Adobe Audience Manager. Prima di utilizzare questo campo, è necessario configurare una sostituzione del contenitore ID di terze parti nelle impostazioni del flusso di dati.
* **Token di proprietà di destinazione**: il token per la proprietà di destinazione in Adobe Target. Prima di utilizzare questo campo, è necessario configurare una sostituzione del token di proprietà Target nelle impostazioni del flusso di dati.
* **Suite di rapporti**: ID suite di rapporti da escludere in Adobe Analytics. Prima di utilizzare questo campo, è necessario configurare le sostituzioni della suite di rapporti nelle impostazioni del flusso di dati.

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
| `com_adobe_identity.idSyncContainerId` | Il contenitore di sincronizzazione ID di terze parti che desideri utilizzare in Audience Manager. |
| `com_adobe_target.propertyToken` | Token per la proprietà di destinazione Adobe Target. |

### Invia sostituzioni di configurazione tramite il comando Web SDK `configure` {#send-configure}

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
| `com_adobe_identity.idSyncContainerId` | Il contenitore di sincronizzazione ID di terze parti che desideri utilizzare in Audience Manager. |
| `com_adobe_target.propertyToken` | Token per la proprietà di destinazione Adobe Target. |
