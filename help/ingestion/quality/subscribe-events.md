---
keywords: Experience Platform;home;argomenti popolari;notifiche di acquisizione dati;notifiche;sottoscrivere eventi;acquisizione dati eventi di stato;eventi di stato;sottoscrivere;notifiche di stato;
solution: Experience Platform
title: Notifiche di acquisizione dati
description: Per facilitare il monitoraggio del processo di acquisizione, Adobe Experience Platform consente di abbonarsi a un set di eventi pubblicati in ogni fase del processo, inviando all’utente una notifica sullo stato dei dati acquisiti e su eventuali errori.
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 1%

---

# Notifiche di acquisizione dei dati

Il processo di acquisizione dei dati in Adobe Experience Platform è costituito da più passaggi. Una volta identificati i file di dati che devono essere acquisiti in [!DNL Platform], il processo di acquisizione inizia e ogni passaggio si verifica in sequenza fino a quando i dati non vengono acquisiti correttamente o non hanno esito positivo. Il processo di acquisizione può essere avviato utilizzando [Adobe Experience Platform Batch Ingestion API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) o l&#39;interfaccia utente [!DNL Experience Platform].

I dati caricati in [!DNL Platform] devono seguire più passaggi per raggiungere la destinazione, l&#39;archivio dati [!DNL Data Lake] o [!DNL Real-Time Customer Profile]. Ogni passaggio comporta l’elaborazione dei dati, la loro convalida e quindi la loro memorizzazione prima di trasmetterli al passaggio successivo. A seconda della quantità di dati acquisiti, questo può diventare un processo che richiede tempo ed è sempre possibile che il processo non riesca a causa di errori di convalida, semantica o elaborazione. In caso di errore, è necessario risolvere i problemi relativi ai dati e quindi riavviare l’intero processo di acquisizione utilizzando i file di dati corretti.

Per facilitare il monitoraggio del processo di acquisizione, [!DNL Experience Platform] consente di sottoscrivere un set di eventi pubblicati in ogni fase del processo, notificando lo stato dei dati acquisiti e qualsiasi possibile errore.

## Registra un webhook per le notifiche di acquisizione dei dati

Per ricevere le notifiche di acquisizione dei dati, devi utilizzare [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) per registrare un webhook nell&#39;integrazione Experience Platform.

Segui l&#39;esercitazione su [abbonamento a [!DNL Adobe I/O Event] notifiche](../../observability/alerts/subscribe.md) per i passaggi dettagliati su come eseguire questa operazione.

>[!IMPORTANT]
>
>Durante il processo di abbonamento, accertati di selezionare **[!UICONTROL Notifiche Platform]** come provider di eventi e, quando richiesto, seleziona la **[!UICONTROL Notifica di acquisizione dati]** sottoscrizione di eventi.

## Ricevere notifiche di acquisizione dati

Dopo aver registrato correttamente il webhook e aver acquisito i nuovi dati, puoi iniziare a ricevere le notifiche dell’evento. Questi eventi possono essere visualizzati utilizzando il webhook stesso oppure selezionando la scheda **[!UICONTROL Traccia debug]** nella panoramica della registrazione degli eventi del progetto in Adobe Developer Console.

Il seguente JSON è un esempio di payload di notifica che verrebbe inviato al webhook in caso di un evento di acquisizione batch non riuscito:

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{ORG_ID}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{ORG_ID}",
        "providerMetadata": "aep_observability_catalog_events",
        "eventCode": "platform_event"
      }
    }
  }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `event_id` | ID univoco generato dal sistema per la notifica. |
| `event` | Oggetto contenente i dettagli dell’evento che ha attivato la notifica. |
| `event.xdm:datasetId` | ID del set di dati a cui si applica l’evento di acquisizione. |
| `event.xdm:eventCode` | Codice di stato che indica il tipo di evento attivato per il set di dati. Consulta l&#39;[appendice](#event-codes) per i valori specifici e le relative definizioni. |

Per visualizzare lo schema completo per le notifiche degli eventi, consulta l&#39;[archivio GitHub pubblico](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## Passaggi successivi

Dopo aver registrato [!DNL Platform] notifiche per il progetto, puoi visualizzare gli eventi ricevuti dalla [!UICONTROL Panoramica del progetto]. Per istruzioni dettagliate su come tracciare i tuoi eventi, consulta la guida su [eventi di Adobe I/O di tracciamento](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md).

## Appendice

La sezione seguente contiene informazioni aggiuntive sull’interpretazione dei payload di notifica di acquisizione dati.

### Eventi di notifica dello stato disponibili {#event-codes}

Nella tabella seguente sono elencate le notifiche di stato di acquisizione dei dati disponibili a cui puoi iscriverti.

| Codice evento | Servizio Platform | Stato | Descrizione di un evento |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | Un batch è stato acquisito correttamente in un set di dati all&#39;interno di [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | errore | Impossibile acquisire un batch in un set di dati in [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-Time Customer Profile] | success | Un batch è stato acquisito correttamente nell&#39;archivio dati [!DNL Profile]. |
| `ps_load_failure` | [!DNL Real-Time Customer Profile] | errore | Impossibile acquisire un batch nell&#39;archivio dati [!DNL Profile]. |
| `ig_load_success` | [!DNL Identity Service] | success | I dati sono stati caricati correttamente nel grafico delle identità. |
| `ig_load_failure` | [!DNL Identity Service] | errore | Caricamento dei dati nel grafo delle identità non riuscito. |

>[!NOTE]
>
>È disponibile un solo argomento evento fornito per tutte le notifiche di acquisizione dei dati. Per distinguere tra diversi stati, è possibile utilizzare il codice evento.
