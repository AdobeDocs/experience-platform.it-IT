---
title: Configurare gli override dello stream di dati
description: Scopri come configurare le sostituzioni dello stream di dati nell’interfaccia utente dello stream di dati e attivarle tramite Web SDK o Mobile SDK.
exl-id: 3f17a83a-dbea-467b-ac67-5462c07c884c
source-git-commit: 79d724eec4903b8a3eee6f717d94fcd70a4ffcb7
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 38%

---

# Configurare gli override dello stream di dati

Utilizza le sostituzioni dello stream di dati per definire configurazioni aggiuntive per gli stream di dati, che vengono passati a [!DNL Edge Network] tramite Web SDK o Mobile SDK.

Attiva diversi comportamenti dello stream di dati senza creare un nuovo stream di dati o modificare le impostazioni esistenti.

La sostituzione della configurazione dello stream di dati è un processo in due fasi:

1. Innanzitutto, devi definire la sostituzione della configurazione dello stream di dati nella [pagina di configurazione dello stream di dati](/help/datastreams/configure.md).
2. Quindi, è necessario inviare le sostituzioni a [!DNL Edge Network] in uno dei seguenti modi:
   * Tramite i comandi `sendEvent` o `configure` [Web SDK](#send-overrides).
   * Tramite l&#39;estensione tag [Web SDK](/help/tags/extensions/client/web-sdk/configure/configuration-overrides.md).
   * Tramite l&#39;API [sendEvent](#send-overrides) di Mobile SDK o utilizzando [Regole](#send-overrides).

Questo articolo spiega il processo di override della configurazione dello stream di dati end-to-end per ogni tipo di override supportato.

>[!IMPORTANT]
>
>Le integrazioni API [!DNL Edge Network] non supportano attualmente le sostituzioni dello stream di dati.
>
>Gli override dello stream di dati devono essere utilizzati quando è necessario inviare dati diversi a stream di dati diversi. Non utilizzare le sostituzioni dello stream di dati per i casi d’uso di personalizzazione o i dati di consenso.

## Casi d’uso {#use-cases}

I seguenti casi d’uso mostrano come e quando utilizzare le sostituzioni dello stream di dati.

### Raccolta di dati per più aree geografiche {#multi-region}

Un’azienda dispone di siti web o sottodomini diversi per diversi Paesi in cui opera. Hanno [configurato](/help/datastreams/configure.md) flussi di dati separati con suite di rapporti specifiche per analytics corrispondenti, token di proprietà [!DNL Adobe Target] specifici per paese, schemi specifici per paese, set di dati, configurazioni [!DNL Journey Optimizer] e così via. L’azienda dispone anche di un set globale di configurazioni in cui vengono aggregati tutti i dati specifici per Paese.

Utilizzando gli override dello stream di dati, l’azienda può cambiare dinamicamente il flusso di dati in flussi di dati diversi, invece del comportamento predefinito di invio dei dati a uno stream di dati.

Un caso d’uso comune è l’invio di dati a un flusso di dati specifico per paese e anche a un flusso di dati globale quando i clienti eseguono un’azione importante, ad esempio l’ordine o l’aggiornamento del profilo utente.

### Differenziazione di profili e identità per diverse unità aziendali {#multiple-business-units}

Un’azienda con più business unit desidera utilizzare più sandbox di Experience Platform per memorizzare dati specifici per ogni business unit.

Invece di inviare dati a uno stream di dati predefinito, l’azienda può utilizzare gli override dello stream di dati per assicurarsi che ogni unità di business abbia il proprio stream di dati tramite cui ricevere i dati.

## Configurare gli override dello stream di dati nell’interfaccia utente dello stream di dati {#configure-overrides}

Le sostituzioni della configurazione dello stream di dati consentono di modificare le seguenti configurazioni dello stream di dati:

* Set di dati evento di Experience Platform
* [!DNL Adobe Target] token di proprietà
* Contenitori di sincronizzazione ID di Audience Manager
* [!DNL Adobe Analytics] suite di rapporti

### Override dello stream di dati per Adobe Target {#target-overrides}

Per configurare le sostituzioni dello stream di dati per uno stream di dati [!DNL Adobe Target], è innanzitutto necessario creare uno stream di dati [!DNL Adobe Target]. Segui le istruzioni per [configurare uno stream di dati](/help/datastreams/configure.md) con il servizio [Adobe Target](/help/datastreams/configure.md#target).

Dopo aver creato lo stream di dati, modifica il servizio [Adobe Target](/help/datastreams/configure.md#target) aggiunto e utilizza la sezione **[!UICONTROL Property Token Overrides]** per aggiungere le sostituzioni dello stream di dati desiderate. Aggiungi un token di proprietà per riga.

![Schermata dell’interfaccia utente degli stream di dati che mostra le impostazioni del servizio Adobe Target, con gli override del token di proprietà evidenziati.](assets/overrides/override-target.png)

Dopo aver aggiunto le sostituzioni desiderate, salva le impostazioni dello stream di dati.

Le sostituzioni dello stream di dati [!DNL Adobe Target] sono ora configurate. Ora puoi [inviare le sostituzioni a  [!DNL Edge Network] tramite Web SDK o Mobile SDK](#send-overrides).

### Override dello stream di dati per Adobe Analytics {#analytics-overrides}

Per configurare le sostituzioni dello stream di dati per uno stream di dati [!DNL Adobe Analytics], è necessario innanzitutto creare uno stream di dati [Adobe Analytics](/help/datastreams/configure.md#analytics). Segui le istruzioni per [configurare uno stream di dati](/help/datastreams/configure.md) con il servizio [Adobe Analytics](/help/datastreams/configure.md#analytics).

Dopo aver creato lo stream di dati, modifica il servizio [Adobe Analytics](/help/datastreams/configure.md#analytics) aggiunto e utilizza la sezione **[!UICONTROL Report Suite Overrides]** per aggiungere le sostituzioni dello stream di dati desiderate.

Selezionare **[!UICONTROL Show Batch Mode]** per abilitare la modifica in batch delle sostituzioni della suite di rapporti. Puoi copiare e incollare un elenco di override delle suite di rapporti inserendo una suite di rapporti per riga.

![Schermata dell’interfaccia utente Stream di dati che mostra le impostazioni del servizio Adobe Analytics, con gli override delle suite di rapporti evidenziati.](assets/overrides/override-analytics.png)

Dopo aver aggiunto le sostituzioni desiderate, salva le impostazioni dello stream di dati.

Le sostituzioni dello stream di dati [!DNL Adobe Analytics] sono ora configurate. Ora puoi [inviare le sostituzioni a  [!DNL Edge Network] tramite Web SDK o Mobile SDK](#send-overrides).

### Override di stream di dati per i set di dati evento di Experience Platform {#event-dataset-overrides}

Per configurare gli override dello stream di dati per i set di dati evento di Experience Platform, accertati di aver prima creato uno stream di dati di [Adobe Experience Platform](/help/datastreams/configure.md#aep). Segui le istruzioni per [configurare uno stream di dati](/help/datastreams/configure.md) con il servizio [Adobe Experience Platform](/help/datastreams/configure.md#aep).

Dopo aver creato lo stream di dati, modifica il servizio [Adobe Experience Platform](/help/datastreams/configure.md#aep) aggiunto e seleziona l&#39;opzione **[!UICONTROL Add Event Dataset]** per aggiungere uno o più set di dati evento di sostituzione.

![Schermata dell’interfaccia utente degli stream di dati che mostra le impostazioni del servizio Adobe Experience Platform, con gli override del set di dati dell’evento evidenziati.](assets/overrides/override-aep.png)

Dopo aver aggiunto le sostituzioni desiderate, salva le impostazioni dello stream di dati.

Le sostituzioni dello stream di dati [!DNL Adobe Experience Platform] sono ora configurate. Ora puoi [inviare le sostituzioni a  [!DNL Edge Network] tramite Web SDK o Mobile SDK](#send-overrides).

### Override dello stream di dati per i contenitori di sincronizzazione ID di terze parti {#container-overrides}

Per configurare gli override degli stream di dati per i contenitori di sincronizzazione ID di terze parti, devi prima aver creato uno stream di dati. Segui le istruzioni per [configurare uno stream di dati](/help/datastreams/configure.md) per crearne uno.

Dopo aver creato lo stream di dati, passa a **[!UICONTROL Advanced Options]** e abilita l&#39;opzione **[!UICONTROL Third Party ID Sync]**.

Quindi, utilizzare la sezione **[!UICONTROL Container ID Overrides]** per aggiungere gli ID contenitore che si desidera sostituire con l&#39;impostazione predefinita.

>[!IMPORTANT]
>
>Gli ID contenitore devono essere valori numerici, come `1234567`, e non stringhe, come `"1234567"`. Se invii un valore stringa tramite Web SDK come override dell’ID contenitore, ti verrà restituito un errore.

![Schermata dell’interfaccia utente per gli stream di dati che mostra le impostazioni dello stream di dati, con gli override del contenitore di sincronizzazione ID di terze parti evidenziati.](assets/overrides/override-container.png)

Dopo aver aggiunto le sostituzioni desiderate, salva le impostazioni dello stream di dati.

Le sostituzioni del contenitore di sincronizzazione ID sono ora configurate. Ora puoi [inviare le sostituzioni a  [!DNL Edge Network] tramite Web SDK o Mobile SDK](#send-overrides).

## Inviare le sostituzioni ad Edge Network {#send-overrides}

Dopo aver configurato le sostituzioni dello stream di dati nell&#39;interfaccia utente di Data Collection, puoi inviare le sostituzioni a [!DNL Edge Network] tramite Web SDK o Mobile SDK.

* **Web SDK**: vedere [sostituzioni della configurazione dello stream di dati](/help/collection/js/commands/configure/edgeconfigoverrides.md) per esempi di codice della libreria JavaScript.
* **Mobile SDK**: è possibile inviare le sostituzioni degli ID dello stream di dati utilizzando [sendEvent API](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-sendevent/) o utilizzando [Rules](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-rules/).

## Esempio di payload {#payload-example}

Gli esempi precedenti generano un payload [!DNL Edge Network] simile a quello seguente.

```json
{
  "meta": {
    "configOverrides": {
      "com_adobe_experience_platform": {
        "datasets": {
          "event": {
            "datasetId": "SampleProfileDatasetIdOverride"
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
  "events": [  ]
}
```
