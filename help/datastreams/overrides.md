---
title: Configurare gli override dello stream di dati
description: Scopri come configurare le sostituzioni dello stream di dati nell’interfaccia utente dello stream di dati e attivarle tramite Web SDK o Mobile SDK.
exl-id: 3f17a83a-dbea-467b-ac67-5462c07c884c
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 53%

---

# Configurare gli override dello stream di dati

Le sostituzioni dello stream di dati consentono di definire configurazioni aggiuntive per gli stream di dati, che vengono passati ad Edge Network tramite Web SDK o Mobile SDK.

Questo consente di attivare comportamenti diversi dello stream di dati rispetto a quelli predefiniti, senza creare uno stream di dati o modificare le impostazioni esistenti.

La sostituzione della configurazione dello stream di dati è un processo in due fasi:

1. Innanzitutto, devi definire la sostituzione della configurazione dello stream di dati nella [pagina di configurazione dello stream di dati](configure.md).
2. Quindi, devi inviare le sostituzioni ad Edge Network in uno dei seguenti modi:
   * Tramite i comandi `sendEvent` o `configure` [Web SDK](#send-overrides).
   * Tramite l&#39;estensione tag [Web SDK](../tags/extensions/client/web-sdk/configure/configuration-overrides.md).
   * Tramite l&#39;API [sendEvent](#send-overrides) di Mobile SDK o utilizzando [Regole](#send-overrides).

Questo articolo spiega il processo di override della configurazione dello stream di dati end-to-end per ogni tipo di override supportato.

>[!IMPORTANT]
>
>Le integrazioni [API Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/) non supportano attualmente le sostituzioni dello stream di dati.
><br>
>Gli override dello stream di dati devono essere utilizzati quando è necessario inviare dati diversi a stream di dati diversi. Non utilizzare le sostituzioni dello stream di dati per i casi d’uso di personalizzazione o i dati di consenso.

## Casi d’uso {#use-cases}

Per aiutarti a comprendere meglio come e quando utilizzare gli override dello stream di dati, ecco alcuni casi d’uso che i clienti di Adobe Experience Platform possono risolvere utilizzando questa funzione.

**Raccolta di dati per più aree geografiche**

Un’azienda dispone di siti web o sottodomini diversi per diversi Paesi in cui opera. Ha [configurato](configure.md) stream di dati separati con le corrispondenti suite di rapporti specifiche per l’analisi, i token di proprietà di Adobe Target specifici per Paese, gli schemi specifici per Paese, i set di dati, le configurazioni di Journey Optimizer e così via. L’azienda dispone anche di un set globale di configurazioni in cui vengono aggregati tutti i dati specifici per Paese.

Utilizzando gli override dello stream di dati, l’azienda può cambiare dinamicamente il flusso di dati in flussi di dati diversi, invece del comportamento predefinito di invio dei dati a uno stream di dati.

Un caso d’uso comune potrebbe essere l’invio di dati a un flusso di dati specifico per paese e anche a un flusso di dati globale in cui i clienti eseguono un’azione importante, ad esempio l’ordine o l’aggiornamento del profilo utente.

**Differenziazione di profili e identità per diverse unità di business**

Un’azienda con più business unit desidera utilizzare più sandbox Experience Platform per memorizzare dati specifici di ogni business unit.

Invece di inviare dati a uno stream di dati predefinito, l’azienda può utilizzare gli override dello stream di dati per assicurarsi che ogni unità di business abbia il proprio stream di dati tramite cui ricevere i dati.

## Configurare gli override dello stream di dati nell’interfaccia utente dello stream di dati {#configure-overrides}

Gli ovverride della configurazione dello stream di dati consentono di modificare le seguenti configurazioni dello stream di dati:

* Set di dati evento di Experience Platform
* Token di proprietà di Adobe Target
* Contenitori di sincronizzazione ID di Audience Manager
* Suite di rapporti di Adobe Analytics

### Override dello stream di dati per Adobe Target {#target-overrides}

Per configurare gli override dello stream di dati per uno stream di dati di Adobe Target, devi prima aver creato uno stream di dati di Adobe Target. Segui le istruzioni per [configurare uno stream di dati](configure.md) con il servizio [Adobe Target](configure.md#target).

Dopo aver creato lo stream di dati, modifica il servizio [Adobe Target](configure.md#target) aggiunto e utilizza la sezione **[!UICONTROL Property Token Overrides]** per aggiungere le sostituzioni dello stream di dati desiderate, come illustrato nell&#39;immagine seguente. Aggiungi un token di proprietà per riga.

![Schermata dell’interfaccia utente degli stream di dati che mostra le impostazioni del servizio Adobe Target, con gli override del token di proprietà evidenziati.](assets/overrides/override-target.png)

Dopo aver aggiunto gli override desiderati, salva le impostazioni dello stream di dati.

Ora dovresti avere configurato gli override dello stream di dati di Adobe Target. Ora puoi [inviare le sostituzioni ad Edge Network tramite Web SDK o Mobile SDK](#send-overrides).

### Override dello stream di dati per Adobe Analytics {#analytics-overrides}

Per configurare gli override dello stream di dati per uno stream di dati di Adobe Analytics, devi prima aver creato uno stream di dati di [Adobe Analytics](configure.md#analytics). Segui le istruzioni per [configurare uno stream di dati](configure.md) con il servizio [Adobe Analytics](configure.md#analytics).

Dopo aver creato lo stream di dati, modifica il servizio [Adobe Analytics](configure.md#target) aggiunto e utilizza la sezione **[!UICONTROL Report Suite Overrides]** per aggiungere le sostituzioni dello stream di dati desiderate, come illustrato nell&#39;immagine seguente.

Selezionare **[!UICONTROL Show Batch Mode]** per abilitare la modifica in batch delle sostituzioni della suite di rapporti. Puoi copiare e incollare un elenco di override delle suite di rapporti inserendo una suite di rapporti per riga.

![Schermata dell’interfaccia utente Stream di dati che mostra le impostazioni del servizio Adobe Analytics, con gli override delle suite di rapporti evidenziati.](assets/overrides/override-analytics.png)

Dopo aver aggiunto gli override desiderati, salva le impostazioni dello stream di dati.

Ora gli override dello stream di dati di Adobe Analytics saranno configurati. Ora puoi [inviare le sostituzioni ad Edge Network tramite Web SDK o Mobile SDK](#send-overrides).

### Override di stream di dati per i set di dati evento di Experience Platform {#event-dataset-overrides}

Per configurare gli override dello stream di dati per i set di dati evento di Experience Platform, accertati di aver prima creato uno stream di dati di [Adobe Experience Platform](configure.md#aep). Segui le istruzioni per [configurare uno stream di dati](configure.md) con il servizio [Adobe Experience Platform](configure.md#aep).

Dopo aver creato lo stream di dati, modificare il servizio [Adobe Experience Platform](configure.md#aep) aggiunto e selezionare l&#39;opzione **[!UICONTROL Add Event Dataset]** per aggiungere uno o più set di dati evento di sostituzione, come illustrato nell&#39;immagine seguente.

![Schermata dell’interfaccia utente degli stream di dati che mostra le impostazioni del servizio Adobe Experience Platform, con gli override del set di dati dell’evento evidenziati.](assets/overrides/override-aep.png)

Dopo aver aggiunto gli override desiderati, salva le impostazioni dello stream di dati.

Ora dovresti aver configurato gli override dello stream di dati di Adobe Experience Platform. Ora puoi [inviare le sostituzioni ad Edge Network tramite Web SDK o Mobile SDK](#send-overrides).

### Override dello stream di dati per i contenitori di sincronizzazione ID di terze parti {#container-overrides}

Per configurare gli override degli stream di dati per i contenitori di sincronizzazione ID di terze parti, devi prima aver creato uno stream di dati. Segui le istruzioni per [configurare uno stream di dati](configure.md) per crearne uno.

Dopo aver creato lo stream di dati, passa a **[!UICONTROL Advanced Options]** e abilita l&#39;opzione **[!UICONTROL Third Party ID Sync]**.

Quindi, utilizza la sezione **[!UICONTROL Container ID Overrides]** per aggiungere gli ID contenitore che desideri escludere dall&#39;impostazione predefinita, come illustrato nell&#39;immagine seguente.

>[!IMPORTANT]
>
>Gli ID contenitore devono essere valori numerici, come `1234567`, e non stringhe, come `"1234567"`. Se invii un valore stringa tramite Web SDK come override dell’ID contenitore, ti verrà restituito un errore.

![Schermata dell’interfaccia utente per gli stream di dati che mostra le impostazioni dello stream di dati, con gli override del contenitore di sincronizzazione ID di terze parti evidenziati.](assets/overrides/override-container.png)

Dopo aver aggiunto gli override desiderati, salva le impostazioni dello stream di dati.

Ora gli override del contenitore di sincronizzazione ID saranno configurati. Ora puoi [inviare le sostituzioni ad Edge Network tramite Web SDK o Mobile SDK](#send-overrides).

## Inviare le sostituzioni ad Edge Network {#send-overrides}

Dopo aver configurato le sostituzioni dello stream di dati nell’interfaccia utente di Data Collection, puoi inviare le sostituzioni ad Edge Network tramite Web SDK o Mobile SDK.

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
