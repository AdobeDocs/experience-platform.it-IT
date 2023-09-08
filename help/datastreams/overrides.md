---
title: Configurare gli override dello stream di dati
description: Scopri come configurare gli override dello stream di dati nell’interfaccia utente dello stream di dati e attivarle tramite il Web SDK.
exl-id: 7829f411-acdc-49a1-a8fe-69834bcdb014
source-git-commit: b0b53d9fcf410812eee3abdbbb6960d328fee99f
workflow-type: ht
source-wordcount: '1231'
ht-degree: 100%

---

# Configurare gli override dello stream di dati

Gli override dello stream di dati consentono di definire configurazioni aggiuntive per gli stream di dati, che vengono passate alla rete Edge tramite il Web SDK.

Questo consente di attivare comportamenti diversi dello stream di dati rispetto a quelli predefiniti, senza creare un nuovo stream di dati o modificare le impostazioni esistenti.

L’override della configurazione dello stream di dati è un processo costituito da due passaggi:

1. Innanzitutto, devi definire gli override della configurazione dello stream di dati nella [pagina di configurazione dello stream di dati](configure.md).
2. Quindi, devi inviare gli override alla rete Edge tramite un comando Web SDK o utilizzando l’[estensione tag](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) di Web SDK.

Questo articolo spiega il processo di override della configurazione dello stream di dati end-to-end per ogni tipo di override supportato.

>[!IMPORTANT]
>
>Gli override dello stream di dati sono supportati solo per le integrazioni [Web SDK](../edge/home.md). Le integrazioni [SDK Mobile](https://developer.adobe.com/client-sdks/documentation/) e [API server](../server-api/overview.md) al momento non supportano gli override dello stream di dati.
><br><br>
>Gli override dello stream di dati devono essere utilizzati quando è necessario inviare dati diversi a stream di dati diversi. Non utilizzare gli override dello stream di dati per i casi di utilizzo di personalizzazione o per i dati sul consenso.

## Casi d’uso {#use-cases}

Per aiutarti a comprendere meglio come e quando utilizzare gli override dello stream di dati, ecco alcuni casi d’uso che i clienti di Adobe Experience Platform possono risolvere utilizzando questa funzione.

**Raccolta di dati per più aree geografiche**

Un’azienda dispone di siti web o sottodomini diversi per diversi Paesi in cui opera. Ha [configurato](configure.md) stream di dati separati con le corrispondenti suite di rapporti specifiche per l’analisi, i token di proprietà di Adobe Target specifici per Paese, gli schemi specifici per Paese, i set di dati, le configurazioni di Journey Optimizer e così via. L’azienda dispone anche di un set globale di configurazioni in cui vengono aggregati tutti i dati specifici per Paese.

Utilizzando gli override dello stream di dati, l’azienda può cambiare dinamicamente il flusso di dati in flussi di dati diversi, invece del comportamento predefinito di invio dei dati a uno stream di dati.

Un caso d’uso comune potrebbe essere quello di inviare dati a uno stream di dati specifico per Paese e anche di inviare dati a uno stream di dati globale in cui i clienti eseguono un’azione importante, ad esempio l’invio di un ordine o l’aggiornamento del profilo utente.

**Differenziazione di profili e identità per diverse unità aziendali**

Un’azienda con più unità aziendali desidera utilizzare più sandbox di Experience Platform per memorizzare dati specifici di ogni unità aziendale.

Invece di inviare dati a uno stream di dati predefinito, l’azienda può utilizzare gli override dello stream di dati per assicurarsi che ogni unità aziendale abbia il proprio stream di dati tramite cui ricevere i dati.

## Configurare gli override dello stream di dati nell’interfaccia utente dello stream di dati {#configure-overrides}

Gli ovverride della configurazione dello stream di dati consentono di modificare le seguenti configurazioni dello stream di dati:

* Set di dati evento di Experience Platform
* Token di proprietà di Adobe Target
* Contenitori di sincronizzazione ID di Audience Manager
* Suite di rapporti di Adobe Analytics

### Override dello stream di dati per Adobe Target {#target-overrides}

Per configurare gli override dello stream di dati per uno stream di dati di Adobe Target, devi prima aver creato uno stream di dati di Adobe Target. Segui le istruzioni per [configurare uno stream di dati](configure.md) con il servizio [Adobe Target](configure.md#target).

Dopo aver creato lo stream di dati, modifica il servizio [Adobe Target](configure.md#target) aggiunto e utilizza la sezione **[!UICONTROL Override del token di proprietà]** per aggiungere gli override dello stream di dati desiderati, come illustrato nell’immagine seguente. Aggiungi un token di proprietà per riga.

![Schermata dell’interfaccia utente degli stream di dati che mostra le impostazioni del servizio Adobe Target, con gli override del token di proprietà evidenziati.](assets/overrides/override-target.png)

Dopo aver aggiunto gli override desiderati, salva le impostazioni dello stream di dati.

Ora dovresti avere configurato gli override dello stream di dati di Adobe Target. Ora puoi [inviare gli override alla rete Edge tramite Web SDK](#send-overrides).

### Override dello stream di dati per Adobe Analytics {#analytics-overrides}

Per configurare gli override dello stream di dati per uno stream di dati di Adobe Analytics, devi prima aver creato uno stream di dati di [Adobe Analytics](configure.md#analytics). Segui le istruzioni per [configurare uno stream di dati](configure.md) con il servizio [Adobe Analytics](configure.md#analytics).

Dopo aver creato lo stream di dati, modifica il servizio [Adobe Analytics](configure.md#target) aggiunto e utilizza la sezione **[!UICONTROL Override suite di rapporti]** per aggiungere gli override dello stream di dati desiderate, come illustrato nell’immagine seguente.

Seleziona **[!UICONTROL Mostra modalità batch]** per attivare la modifica in batch degli override delle suite di rapporti. Puoi copiare e incollare un elenco di override delle suite di rapporti inserendo una suite di rapporti per riga.

![Schermata dell’interfaccia utente Stream di dati che mostra le impostazioni del servizio Adobe Analytics, con gli override delle suite di rapporti evidenziati.](assets/overrides/override-analytics.png)

Dopo aver aggiunto gli override desiderati, salva le impostazioni dello stream di dati.

Ora gli override dello stream di dati di Adobe Analytics saranno configurati. Ora puoi [inviare gli override alla rete Edge tramite Web SDK](#send-overrides).

### Override di stream di dati per i set di dati evento di Experience Platform {#event-dataset-overrides}

Per configurare gli override dello stream di dati per i set di dati evento di Experience Platform, accertati di aver prima creato uno stream di dati di [Adobe Experience Platform](configure.md#aep). Segui le istruzioni per [configurare uno stream di dati](configure.md) con il servizio [Adobe Experience Platform](configure.md#aep).

Dopo aver creato lo stream di dati, modifica il servizio [Adobe Experience Platform](configure.md#aep) aggiunto e seleziona l’opzione **[!UICONTROL Aggiungi set di dati evento]** per aggiungere uno o più set di dati evento di override, come illustrato nell’immagine seguente.

![Schermata dell’interfaccia utente degli stream di dati che mostra le impostazioni del servizio Adobe Experience Platform, con gli override del set di dati dell’evento evidenziati.](assets/overrides/override-aep.png)

Dopo aver aggiunto gli override desiderati, salva le impostazioni dello stream di dati.

Ora dovresti aver configurato gli override dello stream di dati di Adobe Experience Platform. Ora puoi [inviare gli override alla rete Edge tramite Web SDK](#send-overrides).

### Override dello stream di dati per i contenitori di sincronizzazione ID di terze parti {#container-overrides}

Per configurare gli override degli stream di dati per i contenitori di sincronizzazione ID di terze parti, devi prima aver creato uno stream di dati. Segui le istruzioni per [configurare uno stream di dati](configure.md) per crearne uno.

Dopo aver creato lo stream di dati, passa a **[!UICONTROL Opzioni avanzate]** e abilita l’opzione **[!UICONTROL Sincronizzazione ID di terze parti]**.

Quindi, utilizza la sezione **[!UICONTROL Override ID contenitore]** per aggiungere gli ID contenitore che dovranno sovrascrivere l’impostazione predefinita, come illustrato nell’immagine seguente.

>[!IMPORTANT]
>
>Gli ID contenitore devono essere valori numerici, come `1234567`, e non stringhe, come `"1234567"`. Se invii un valore stringa tramite Web SDK come override dell’ID contenitore, ti verrà restituito un errore.

![Schermata dell’interfaccia utente per gli stream di dati che mostra le impostazioni dello stream di dati, con gli override del contenitore di sincronizzazione ID di terze parti evidenziati.](assets/overrides/override-container.png)

Dopo aver aggiunto gli override desiderati, salva le impostazioni dello stream di dati.

Ora gli override del contenitore di sincronizzazione ID saranno configurati. Ora puoi [inviare gli override alla rete Edge tramite Web SDK](#send-overrides).

## Inviare gli override alla rete Edge tramite Web SDK {#send-overrides}

>[!NOTE]
>
>In alternativa all’invio degli override di configurazione tramite i comandi di Web SDK, puoi aggiungere gli override di configurazione all’[estensione tag](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) di Web SDK.

Dopo [aver configurato gli override dello stream di dati](#configure-overrides) nell’interfaccia utente Raccolta dati, puoi inviare gli override alla rete Edge tramite Web SDK.

L’invio degli override alla rete Edge tramite Web SDK è il secondo e ultimo passaggio dell’attivazione degli override della configurazione dello stream di dati.

Gli override della configurazione dello stream di dati vengono inviati alla rete Edge tramite il comando `edgeConfigOverrides` di Web SDK. Questo comando crea gli override dello stream di dati che vengono passati alla [!DNL Edge Network] al comando successivo o, nel caso del comando `configure`, a ogni richiesta.

Il comando `edgeConfigOverrides` crea gli override dello stream di dati che vengono passati alla [!DNL Edge Network] al comando successivo o, nel caso di `configure`, a ogni richiesta.

Quando viene inviato un override di configurazione con il comando `configure`, viene incluso nei seguenti comandi di Web SDK.

* [sendEvent](../edge/fundamentals/tracking-events.md)
* [setConsent](../edge/consent/iab-tcf/overview.md)
* [getIdentity](../edge/identity/overview.md)
* [appendIdentityToUrl](../edge/identity/id-sharing.md#cross-domain-sharing)
* [configure](../edge/fundamentals/configuring-the-sdk.md)

Le opzioni specificate a livello globale possono essere ignorate dall’opzione di configurazione relativa ai singoli comandi.

### Invio degli override della configurazione tramite il comando `sendEvent` {#send-event}

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
| `edgeConfigOverrides.datastreamId` | Utilizza questo parametro per consentire a una singola richiesta di passare a uno stream di dati diverso da quello definito dal comando `configure`. |

### Invio degli override della configurazione tramite il comando `configure` {#send-configure}

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

Gli esempi precedenti generano un payload della [!DNL Edge Network] simile al seguente:

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
