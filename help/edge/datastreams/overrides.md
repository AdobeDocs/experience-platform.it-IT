---
title: Configurare le sostituzioni di datastream
description: Scopri come configurare le sostituzioni del datastream nell’interfaccia utente di Datastreams e attivarle tramite l’SDK per web.
source-git-commit: ce2e80a7ea7385be98bbcda6a0704cd0814c62b2
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---


# Configurare le sostituzioni di datastream

Le sostituzioni di Datastream consentono di definire configurazioni aggiuntive per i datastreams, che vengono passate alla rete Edge tramite l’SDK per web.

Questo consente di attivare comportamenti diversi del datastream rispetto a quelli predefiniti, senza creare un nuovo datastream o modificare le impostazioni esistenti.

L&#39;override della configurazione di Datastream è un processo in due fasi:

1. Innanzitutto, devi definire le sostituzioni della configurazione del datastream nel [pagina di configurazione di datastream](configure.md).
2. Quindi, devi inviare le sostituzioni alla rete Edge tramite un comando SDK per web o utilizzando l’SDK per web [estensione tag](../extension/web-sdk-extension-configuration.md).

Questo articolo spiega il processo di sostituzione della configurazione del datastream end-to-end per ogni tipo di override supportato.

## Configurare le sostituzioni del datastream nell’interfaccia utente di Datastreams {#configure-overrides}

Le sostituzioni della configurazione Datastream consentono di modificare le seguenti configurazioni del datastream:

* Experience Platform di set di dati evento
* Token di proprietà di Adobe Target
* Contenitori di sincronizzazione ID di Audience Manager
* Suite di rapporti Adobe Analytics

### Ignorare le impostazioni locali di Datastream per Adobe Target {#target-overrides}

Per configurare le sostituzioni del datastream per un datastream Adobe Target, devi prima aver creato un datastream Adobe Target. Segui le istruzioni per [configurare un datastream](configure.md) con [Adobe Target](configure.md#target) servizio.

Dopo aver creato il datastream, modifica il [Adobe Target](configure.md#target) il servizio aggiunto e l&#39;utente utilizza **[!UICONTROL Sostituzioni dei token di proprietà]** per aggiungere le sostituzioni del datastream desiderato, come illustrato nell’immagine seguente. Aggiungi un token di proprietà per riga.

![Schermata dell’interfaccia utente dei Datastreams che mostra le impostazioni del servizio Adobe Target, evidenziando le sostituzioni dei token di proprietà.](../assets/datastreams/overrides/override-target.png)

Dopo aver aggiunto le sostituzioni desiderate, salva le impostazioni del datastream.

È ora necessario configurare le sostituzioni del datastream di Adobe Target. Ora puoi [inviare le sostituzioni alla rete Edge tramite l’SDK per web](#send-overrides).

### Ignorare le impostazioni locali di Datastream per Adobe Analytics {#analytics-overrides}

Per configurare le sostituzioni del datastream per un datastream Adobe Analytics, devi prima disporre di un [Adobe Analytics](configure.md#analytics) creazione di datastream. Segui le istruzioni per [configurare un datastream](configure.md) con [Adobe Analytics](configure.md#analytics) servizio.

Dopo aver creato il datastream, modifica il [Adobe Analytics](configure.md#target) il servizio aggiunto e l&#39;utente utilizza **[!UICONTROL Override suite di rapporti]** per aggiungere le sostituzioni del datastream desiderato, come illustrato nell’immagine seguente.

Seleziona **[!UICONTROL Mostra modalità batch]** per abilitare la modifica batch delle sostituzioni della suite di rapporti. Puoi copiare e incollare un elenco di sostituzioni delle suite di rapporti, inserendo una suite di rapporti per riga.

![Schermata dell’interfaccia utente di Datastreams che mostra le impostazioni del servizio Adobe Analytics, evidenziando le sostituzioni della suite di rapporti.](../assets/datastreams/overrides/override-analytics.png)

Dopo aver aggiunto le sostituzioni desiderate, salva le impostazioni del datastream.

È ora necessario configurare le sostituzioni del datastream di Adobe Analytics. Ora puoi [inviare le sostituzioni alla rete Edge tramite l’SDK per web](#send-overrides).

### Sostituzioni di Datastream per Experience Platform i set di dati evento {#event-dataset-overrides}

Per configurare le sostituzioni del datastream per i set di dati evento di Experience Platform, devi prima disporre di un [Adobe Experience Platform](configure.md#aep) creazione di datastream. Segui le istruzioni per [configurare un datastream](configure.md) con [Adobe Experience Platform](configure.md#aep) servizio.

Dopo aver creato il datastream, modifica il [Adobe Experience Platform](configure.md#aep) il servizio aggiunto e seleziona il **[!UICONTROL Aggiungi set di dati evento]** per aggiungere uno o più set di dati evento di sostituzione, come illustrato nell’immagine seguente.

![Schermata dell’interfaccia utente dei Datastreams che mostra le impostazioni del servizio Adobe Experience Platform, evidenziando le sostituzioni dei set di dati dell’evento.](../assets/datastreams/overrides/override-aep.png)

Dopo aver aggiunto le sostituzioni desiderate, salva le impostazioni del datastream.

È ora necessario configurare le sostituzioni del datastream Adobe Experience Platform. Ora puoi [inviare le sostituzioni alla rete Edge tramite l’SDK per web](#send-overrides).

### Ignorare il datastream per i contenitori di sincronizzazione ID di terze parti {#container-overrides}

Per configurare le sostituzioni del datastream per i contenitori di sincronizzazione ID di terze parti, devi prima aver creato un datastream. Segui le istruzioni per [configurare un datastream](configure.md) per crearne una.

Una volta creato il datastream, vai a **[!UICONTROL Opzioni avanzate]** e **[!UICONTROL Sincronizzazione ID di terze parti]** opzione .

Quindi, utilizza il **[!UICONTROL Ignorare gli ID contenitore]** per aggiungere gli ID del contenitore che desideri ignorare l’impostazione predefinita, come illustrato di seguito.

>[!IMPORTANT]
>
>Gli ID contenitore devono essere valori numerici, come `1234567`e non stringhe quali `"1234567"`. Se invii un valore stringa tramite l&#39;SDK per web come override di ID contenitore, riceverai un errore.

![Schermata dell’interfaccia utente Datastreams che mostra le impostazioni del datastream, evidenziando le sostituzioni del contenitore di sincronizzazione ID di terze parti.](../assets/datastreams/overrides/override-container.png)

Dopo aver aggiunto le sostituzioni desiderate, salva le impostazioni del datastream.

A questo punto è necessario configurare le sostituzioni del contenitore di sincronizzazione ID. Ora puoi [inviare le sostituzioni alla rete Edge tramite l’SDK per web](#send-overrides).

## Inviare le sostituzioni alla rete Edge tramite l’SDK per web {#send-overrides}

>[!NOTE]
>
>In alternativa all’invio delle sostituzioni di configurazione tramite i comandi SDK per web, puoi aggiungere le sostituzioni di configurazione all’SDK per web. [estensione tag](../extension/web-sdk-extension-configuration.md).

Dopo [configurazione delle sostituzioni di datastream](#configure-overrides) nell’interfaccia utente di raccolta dati, ora puoi inviare le sostituzioni alla rete Edge tramite l’SDK per web.

L’invio delle sostituzioni alla rete Edge tramite l’SDK per web è il secondo e ultimo passaggio dell’attivazione delle sostituzioni di configurazione del datastream.

Le sostituzioni della configurazione del datastream vengono inviate alla rete Edge tramite `edgeConfigOverrides` Comando SDK per web. Questo comando crea sostituzioni del datastream che vengono passate al [!DNL Edge Network] sul comando successivo, oppure, nel caso di `configure` per ogni richiesta.

La `edgeConfigOverrides` crea sostituzioni del datastream che vengono passate al [!DNL Edge Network] sul comando successivo, oppure, nel caso di `configure`, per ogni richiesta.

Quando viene inviata una sostituzione di configurazione con il comando `configure` è incluso nei seguenti comandi supportati.

* [sendEvent](../fundamentals/tracking-events.md)
* [setConsent](../consent/iab-tcf/overview.md)
* [getIdentity](../identity/overview.md)
* [appendIdentityToUrl](../identity/id-sharing.md#cross-domain-sharing)
* [configurare](../fundamentals/configuring-the-sdk.md)

Le opzioni specificate a livello globale possono essere sostituite dall’opzione di configurazione su singoli comandi.

### Invio di sostituzioni di configurazione tramite `sendEvent` command {#send-event}

L’esempio seguente mostra l’aspetto di una sostituzione di configurazione su un `sendEvent` comando.

```js {line-numbers="true" highlight="5-25"}
alloy("sendEvent", {
  xdm: {
    /* ... */
  },
  edgeConfigOverrides: {
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

### Invio di sostituzioni di configurazione tramite `configure` command {#send-configure}

L’esempio seguente mostra l’aspetto di una sostituzione di configurazione su un `configure` comando.

```js {line-numbers="true" highlight="8-30"}
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "etc",
  edgeBasePath: "ee",
  edgeConfigId: "etc",
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

Gli esempi di cui sopra generano un [!DNL Edge Network] payload simile al seguente:

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

