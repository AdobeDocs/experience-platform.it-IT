---
keywords: Experience Platform;home;popular topics;data ingestion notifications;notifications;subscribe events;data ingestion status events;status events;subscribe;status notifications;
solution: Experience Platform
title: Iscrizione agli eventi di assimilazione dei dati
topic: overview
translation-type: tm+mt
source-git-commit: 80a1694f11cd2f38347989731ab7c56c2c198090
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 1%

---


# Notifiche di assimilazione dei dati

Il processo di assimilazione dei dati in Adobe Experience Platform consiste di più passaggi. Una volta identificati i file di dati in cui è necessario eseguire l&#39;assimilazione, [!DNL Platform]il processo di assimilazione inizia e ogni passaggio si verifica consecutivamente fino a quando i dati non vengono correttamente acquisiti o non hanno esito negativo. Il processo di inserimento può essere avviato utilizzando l&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) Adobe Experience Platform Data Ingestion o l&#39;interfaccia [!DNL Experience Platform] utente.

I dati caricati in [!DNL Platform] devono passare attraverso più passaggi per raggiungere la destinazione, l&#39;archivio [!DNL Data Lake] o l&#39;archivio [!DNL Real-time Customer Profile] dati. Ogni passaggio prevede l&#39;elaborazione dei dati, la convalida dei dati e la memorizzazione dei dati prima di passare al passaggio successivo. A seconda della quantità di dati che vengono acquisiti, questo può diventare un processo che richiede molto tempo ed è sempre possibile che il processo non riesca a causa di errori di convalida, semantica o elaborazione. In caso di errore, i problemi relativi ai dati devono essere risolti e l&#39;intero processo di assimilazione deve essere riavviato utilizzando i file di dati corretti.

Per assistere nel monitoraggio del processo di assimilazione, [!DNL Experience Platform] consente di sottoscrivere un set di eventi pubblicati in ogni fase del processo, notificando all’utente lo stato dei dati acquisiti e ogni possibile errore.

## Registrazione di un webhook per le notifiche di assimilazione dei dati

Per ricevere le notifiche di assimilazione dei dati, è necessario utilizzare [console](https://www.adobe.com/go/devs_console_ui) Sviluppatore di Adobe per registrare un webhook nell&#39;integrazione del Experience Platform .

Seguite l’esercitazione sulle [notifiche [!DNL Adobe I/O Event] di iscrizione](../../observability/notifications/subscribe.md) per i passaggi dettagliati su come ottenere questo risultato.

>[!IMPORTANT]
>
>Durante il processo di iscrizione, accertatevi di selezionare **[!UICONTROL Platform notifications]** il fornitore dell&#39;evento e di selezionare la sottoscrizione dell&#39; **[!UICONTROL Data ingestion notification]** evento quando richiesto.

## Ricevere notifiche di assimilazione dei dati

Dopo aver registrato correttamente il webhook e l&#39;acquisizione di nuovi dati, potete iniziare a ricevere le notifiche sull&#39;evento. Questi eventi possono essere visualizzati utilizzando il webhook stesso, oppure selezionando la **[!UICONTROL Debug Tracing]** scheda nella panoramica di registrazione dell&#39;evento del progetto in  Adobe Developer Console.

Il seguente JSON è un esempio di payload di notifica che verrebbe inviato al webhook nel caso di un evento di caricamento batch non riuscito:

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{IMS_ORG}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{IMS_ORG}",
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
| `event.xdm:datasetId` | L&#39;ID del set di dati a cui si applica l&#39;evento di assimilazione. |
| `event.xdm:eventCode` | Un codice di stato che indica il tipo di evento attivato per il set di dati. Cfr. l&#39; [appendice](#event-codes) per i valori specifici e le relative definizioni. |

Per visualizzare lo schema completo delle notifiche degli eventi, fare riferimento all&#39;archivio [GitHub](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json)pubblico.

## Passaggi successivi

Una volta registrate [!DNL Platform] le notifiche al progetto, potete visualizzare gli eventi ricevuti dal [!UICONTROL Project overview]. Per istruzioni dettagliate su come [tracciare gli eventi, consultate  Adobe eventi](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) I/O.

## Appendice

La sezione seguente contiene informazioni aggiuntive sull&#39;interpretazione dei payload di notifica dell&#39;assimilazione dei dati.

### Eventi di notifica dello stato disponibili {#event-codes}

Nella tabella seguente sono elencate le notifiche di stato dell’assimilazione dei dati disponibili alle quali potete iscrivervi.

| Codice evento | Servizio piattaforma | Stato | Descrizione di un evento |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | È stato eseguito l&#39;assimilazione di un batch in un set di dati all&#39;interno dell&#39; [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | fallimento | Impossibile assimilare un batch in un set di dati all&#39;interno dell&#39; [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-time Customer Profile] | success | Acquisizione batch riuscita nell&#39;archivio [!DNL Profile] dati. |
| `ps_load_failure` | [!DNL Real-time Customer Profile] | fallimento | Impossibile assimilare un batch nell&#39;archivio [!DNL Profile] dati. |
| `ig_load_success` | [!DNL Identity Service] | success | Caricamento dei dati nel grafico dell&#39;identità completato. |
| `ig_load_failure` | [!DNL Identity Service] | fallimento | Impossibile caricare i dati nel grafico dell&#39;identità. |

>[!NOTE]
>
>È disponibile un solo argomento evento per tutte le notifiche di assimilazione dei dati. Per distinguere tra stati diversi, è possibile utilizzare il codice evento.