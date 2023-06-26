---
title: Configurare le sostituzioni dello stream di dati
description: Scopri come configurare le sostituzioni dello stream di dati nell’interfaccia utente dello stream di dati e attivarle tramite l’SDK per web.
exl-id: 7829f411-acdc-49a1-a8fe-69834bcdb014
source-git-commit: 621dd1dbf99720604f797b97a5e31e090456cdf3
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---

# Configurare le sostituzioni dello stream di dati

Le sostituzioni dello stream di dati consentono di definire configurazioni aggiuntive per gli stream di dati, che vengono passati alla rete Edge tramite l’SDK per web.

Questo consente di attivare comportamenti diversi dello stream di dati rispetto a quelli predefiniti, senza creare un nuovo stream di dati o modificare le impostazioni esistenti.

La sostituzione della configurazione dello stream di dati è un processo in due fasi:

1. Innanzitutto, devi definire le sostituzioni della configurazione dello stream di dati in [pagina di configurazione dello stream di dati](configure.md).
2. Quindi, devi inviare le sostituzioni alla rete Edge tramite un comando Web SDK o utilizzando Web SDK [estensione tag](../extension/web-sdk-extension-configuration.md).

Questo articolo spiega il processo di sostituzione della configurazione dello stream di dati end-to-end per ogni tipo di sostituzione supportata.

## Configurare le sostituzioni dello stream di dati nell’interfaccia utente dello stream di dati {#configure-overrides}

Le sostituzioni della configurazione dello stream di dati consentono di modificare le seguenti configurazioni dello stream di dati:

* Set di dati evento Experience Platform
* Token di proprietà di Adobe Target
* Contenitori di sincronizzazione ID Audience Manager
* Suite di rapporti di Adobe Analytics

### Override dello stream di dati per Adobe Target {#target-overrides}

Per configurare le sostituzioni dello stream di dati per uno stream di dati di Adobe Target, devi prima aver creato uno stream di dati di Adobe Target. Seguire le istruzioni per [configurare uno stream di dati](configure.md) con [Adobe Target](configure.md#target) servizio.

Dopo aver creato lo stream di dati, modifica il [Adobe Target](configure.md#target) servizio aggiunto e utilizza **[!UICONTROL Override del token di proprietà]** per aggiungere le sostituzioni dello stream di dati desiderate, come illustrato nell’immagine seguente. Aggiungi un token di proprietà per riga.

![La schermata dell’interfaccia utente Datastreams mostra le impostazioni del servizio Adobe Target, con le sostituzioni del token di proprietà evidenziate.](../assets/datastreams/overrides/override-target.png)

Dopo aver aggiunto le sostituzioni desiderate, salva le impostazioni dello stream di dati.

Ora dovresti avere configurato le sostituzioni dello stream di dati di Adobe Target. Ora puoi [inviare le sostituzioni alla rete Edge tramite Web SDK](#send-overrides).

### Override dello stream di dati per Adobe Analytics {#analytics-overrides}

Per configurare le sostituzioni dello stream di dati per uno stream di dati di Adobe Analytics, devi prima disporre di un’ [Adobe Analytics](configure.md#analytics) flusso di dati creato. Seguire le istruzioni per [configurare uno stream di dati](configure.md) con [Adobe Analytics](configure.md#analytics) servizio.

Dopo aver creato lo stream di dati, modifica il [Adobe Analytics](configure.md#target) servizio aggiunto e utilizza **[!UICONTROL Sostituzioni suite di rapporti]** per aggiungere le sostituzioni dello stream di dati desiderate, come illustrato nell’immagine seguente.

Seleziona **[!UICONTROL Mostra modalità batch]** per abilitare la modifica in batch delle sostituzioni della suite di rapporti. Puoi copiare e incollare un elenco di sostituzioni della suite di rapporti, inserendo una suite di rapporti per riga.

![La schermata dell’interfaccia utente Datastreams mostra le impostazioni del servizio Adobe Analytics, con le sostituzioni della suite di rapporti evidenziate.](../assets/datastreams/overrides/override-analytics.png)

Dopo aver aggiunto le sostituzioni desiderate, salva le impostazioni dello stream di dati.

Ora dovresti avere configurato le sostituzioni dello stream di dati di Adobe Analytics. Ora puoi [inviare le sostituzioni alla rete Edge tramite Web SDK](#send-overrides).

### Override dello stream di dati per i set di dati evento di Experience Platform {#event-dataset-overrides}

Per configurare le sostituzioni dello stream di dati per i set di dati evento di Experience Platform, devi prima disporre di un’ [Adobe Experience Platform](configure.md#aep) flusso di dati creato. Seguire le istruzioni per [configurare uno stream di dati](configure.md) con [Adobe Experience Platform](configure.md#aep) servizio.

Dopo aver creato lo stream di dati, modifica il [Adobe Experience Platform](configure.md#aep) servizio aggiunto e seleziona il **[!UICONTROL Aggiungi set di dati evento]** per aggiungere uno o più set di dati evento di sostituzione, come illustrato nell’immagine seguente.

![La schermata dell’interfaccia utente dei flussi di dati mostra le impostazioni del servizio Adobe Experience Platform, con le sostituzioni del set di dati dell’evento evidenziate.](../assets/datastreams/overrides/override-aep.png)

Dopo aver aggiunto le sostituzioni desiderate, salva le impostazioni dello stream di dati.

Ora dovresti aver configurato le sostituzioni dello stream di dati di Adobe Experience Platform. Ora puoi [inviare le sostituzioni alla rete Edge tramite Web SDK](#send-overrides).

### Override dello stream di dati per contenitori di sincronizzazione ID di terze parti {#container-overrides}

Per configurare le sostituzioni dello stream di dati per i contenitori di sincronizzazione ID di terze parti, devi prima aver creato uno stream di dati. Seguire le istruzioni per [configurare uno stream di dati](configure.md) per crearne uno.

Dopo aver creato lo stream di dati, vai a **[!UICONTROL Opzioni avanzate]** e abilita **[!UICONTROL Sincronizzazione ID di terze parti]** opzione.

Quindi, utilizza **[!UICONTROL Override ID contenitore]** per aggiungere gli ID dei contenitori che dovranno sovrascrivere l’impostazione predefinita, come illustrato nell’immagine seguente.

>[!IMPORTANT]
>
>Gli ID contenitore devono essere valori numerici, come `1234567`, e non stringhe, come `"1234567"`. Se invii un valore stringa tramite Web SDK come sostituzione dell’ID contenitore, riceverai un errore.

![La schermata dell’interfaccia utente per i flussi di dati mostra le impostazioni del flusso di dati, con le sostituzioni del contenitore di sincronizzazione ID di terze parti evidenziate.](../assets/datastreams/overrides/override-container.png)

Dopo aver aggiunto le sostituzioni desiderate, salva le impostazioni dello stream di dati.

Ora dovresti aver configurato le sostituzioni del contenitore di sincronizzazione ID. Ora puoi [inviare le sostituzioni alla rete Edge tramite Web SDK](#send-overrides).

## Inviare le sostituzioni alla rete Edge tramite Web SDK {#send-overrides}

>[!NOTE]
>
>In alternativa all’invio delle sostituzioni di configurazione tramite comandi Web SDK, puoi aggiungere le sostituzioni di configurazione all’SDK per web [estensione tag](../extension/web-sdk-extension-configuration.md).

Dopo [configurazione delle sostituzioni dello stream di dati](#configure-overrides) Nell’interfaccia utente di Data Collection, ora puoi inviare le sostituzioni alla rete Edge tramite Web SDK.

L’invio delle sostituzioni alla rete Edge tramite Web SDK è il secondo e ultimo passaggio dell’attivazione delle sostituzioni della configurazione dello stream di dati.

Le sostituzioni della configurazione dello stream di dati vengono inviate alla rete Edge tramite `edgeConfigOverrides` Comando Web SDK. Questo comando crea le sostituzioni dello stream di dati che vengono passate al [!DNL Edge Network] al comando successivo o, nel caso di `configure` per ogni richiesta.

Il `edgeConfigOverrides` crea le sostituzioni dello stream di dati che vengono passate al [!DNL Edge Network] al comando successivo o, nel caso di `configure`, per ogni richiesta.

Quando viene inviata una sostituzione della configurazione con `configure` è incluso nei seguenti comandi supportati.

* [sendEvent](../fundamentals/tracking-events.md)
* [setConsent](../consent/iab-tcf/overview.md)
* [getIdentity](../identity/overview.md)
* [appendIdentityToUrl](../identity/id-sharing.md#cross-domain-sharing)
* [configura](../fundamentals/configuring-the-sdk.md)

Le opzioni specificate a livello globale possono essere ignorate dall&#39;opzione di configurazione relativa ai singoli comandi.

### Invio delle sostituzioni di configurazione tramite `sendEvent` comando {#send-event}

L’esempio seguente mostra l’aspetto di una sostituzione della configurazione su una `sendEvent` comando.

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
          datasetId: "MyOverrideDataset"
        },
        profile: {
          datasetId: "www"
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
| `edgeConfigOverrides.datastreamId` | Utilizza questo parametro per consentire a una singola richiesta di andare a un flusso di dati diverso da quello definito da `configure` comando. |

### Invio delle sostituzioni di configurazione tramite `configure` comando {#send-configure}

L’esempio seguente mostra l’aspetto di una sostituzione della configurazione su una `configure` comando.

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
          datasetId: "MyOverrideDataset"
        },
        "profile": { 
          datasetId: "www"
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

### Esempio di payload {#payload-example}

Gli esempi precedenti generano un [!DNL Edge Network] payload simile al seguente:

```json
{
  "meta": {
    "configOverrides": {
      "com_adobe_experience_platform": {
        "datasets": {
          "event": {
            "datasetId": "MyOverrideDataset"
          },
          "profile": {
            "datasetId": "www"
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
    "state": {  }
  },
  "events": [  ],
  "query": {
    "identity": {
      "fetch": [
        "ECID"
      ]
    }
  }
}
```
