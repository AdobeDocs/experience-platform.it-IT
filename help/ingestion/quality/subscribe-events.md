---
keywords: Experience Platform;home;argomenti popolari;notifiche di inserimento dati;notifiche;eventi di sottoscrizione;eventi di stato di inserimento dati;eventi di stato;sottoscrizione;notifiche di stato;
solution: Experience Platform
title: Notifiche di acquisizione dei dati
description: Per facilitare il monitoraggio del processo di acquisizione, Adobe Experience Platform consente di abbonarsi a un set di eventi pubblicati in ogni fase del processo, notificandovi lo stato dei dati acquisiti ed eventuali errori.
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 2%

---

# Notifiche di acquisizione dei dati

Il processo di acquisizione dei dati in Adobe Experience Platform è composto da più passaggi. Una volta identificati i file di dati che devono essere acquisiti in [!DNL Platform], il processo di acquisizione inizia e ogni passaggio avviene consecutivamente fino a quando i dati non vengono acquisiti correttamente o non riescono. Il processo di acquisizione può essere avviato utilizzando [API di acquisizione in batch di Adobe Experience Platform](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) o utilizzando [!DNL Experience Platform] interfaccia utente.

Dati caricati in [!DNL Platform] devono passare attraverso più passaggi per raggiungere la relativa destinazione, [!DNL Data Lake] o [!DNL Real-Time Customer Profile] archivio dati. Ogni passaggio comporta l’elaborazione dei dati, la convalida dei dati e quindi la memorizzazione dei dati prima di passare al passaggio successivo. A seconda della quantità di dati che vengono acquisiti, questo può diventare un processo che richiede molto tempo e c&#39;è sempre la possibilità che il processo non riesca a causa di errori di convalida, semantica o elaborazione. In caso di errore, i problemi di dati devono essere risolti e l’intero processo di acquisizione deve essere riavviato utilizzando i file di dati corretti.

assistere nel monitoraggio del processo di acquisizione, [!DNL Experience Platform] consente di effettuare la sottoscrizione a un set di eventi pubblicati in ogni fase del processo, con notifica dello stato dei dati acquisiti e di eventuali errori.

## Registra un webhook per le notifiche di inserimento dati

Per ricevere le notifiche di inserimento dei dati, devi utilizzare [Console Adobe Developer](https://www.adobe.com/go/devs_console_ui) per registrare un webhook nella tua integrazione di Experience Platform.

Segui l’esercitazione su [abbonamento a [!DNL Adobe I/O Event] Notifiche](../../observability/alerts/subscribe.md) per passaggi dettagliati su come eseguire questa operazione.

>[!IMPORTANT]
>
>Durante il processo di abbonamento, assicurati di selezionare **[!UICONTROL Notifiche di Platform]** come provider di eventi e seleziona il **[!UICONTROL Notifica di inserimento dati]** abbonamento a un evento quando richiesto.

## Ricevere notifiche di acquisizione dati

Dopo aver registrato correttamente il webhook e l’acquisizione dei nuovi dati, puoi iniziare a ricevere le notifiche relative agli eventi. Questi eventi possono essere visualizzati utilizzando il webhook stesso o selezionando **[!UICONTROL Debug Tracing]** nella panoramica sulla registrazione degli eventi del progetto in Adobe Developer Console.

Il seguente JSON è un esempio di payload di notifica che verrebbe inviato al tuo webhook nel caso di un evento di acquisizione batch non riuscito:

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
| `event_id` | Un ID univoco generato dal sistema per la notifica. |
| `event` | Un oggetto che contiene i dettagli dell&#39;evento che ha attivato la notifica. |
| `event.xdm:datasetId` | ID del set di dati a cui si applica l’evento di acquisizione. |
| `event.xdm:eventCode` | Un codice di stato che indica il tipo di evento attivato per il set di dati. Consulta la sezione [appendice](#event-codes) per valori specifici e relative definizioni. |

Per visualizzare lo schema completo delle notifiche degli eventi, consulta [archivio GitHub pubblico](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## Passaggi successivi

Una volta registrato [!DNL Platform] notifiche al progetto, puoi visualizzare gli eventi ricevuti dalla [!UICONTROL Panoramica del progetto]. Consulta la guida su [tracciamento degli eventi di Adobe I/O](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) per istruzioni dettagliate su come tracciare gli eventi.

## Appendice

La sezione seguente contiene informazioni aggiuntive sull’interpretazione dei payload di notifiche di inserimento dati.

### Eventi di notifica dello stato disponibili {#event-codes}

Nella tabella seguente sono elencate le notifiche sullo stato di acquisizione dei dati disponibili per le quali puoi effettuare l’abbonamento.

| Codice evento | Servizio Platform | Stato | Descrizione di un evento |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | Un batch è stato acquisito correttamente in un set di dati all’interno di [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | guasto | Impossibile acquisire un batch in un set di dati all’interno di [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-Time Customer Profile] | success | Acquisizione di un batch riuscita nel [!DNL Profile] archivio dati. |
| `ps_load_failure` | [!DNL Real-Time Customer Profile] | guasto | Impossibile acquisire un batch nel [!DNL Profile] archivio dati. |
| `ig_load_success` | [!DNL Identity Service] | success | Caricamento dei dati nel grafico delle identità completato. |
| `ig_load_failure` | [!DNL Identity Service] | guasto | Impossibile caricare i dati nel grafico delle identità. |

>[!NOTE]
>
>È disponibile un solo argomento evento per tutte le notifiche di inserimento dei dati. Per distinguere tra stati diversi, è possibile utilizzare il codice evento.
