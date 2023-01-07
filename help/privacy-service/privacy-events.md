---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Iscriviti agli eventi Privacy Service
description: Scopri come abbonarti agli eventi di Privacy Service utilizzando un webhook preconfigurato.
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 2%

---

# Iscriviti a [!DNL Privacy Service Events]

[!DNL Privacy Service Events] sono messaggi forniti da Adobe Experience Platform [!DNL Privacy Service], che sfruttano gli eventi di Adobe I/O inviati a un webhook configurato per facilitare l’automazione efficiente della richiesta di lavoro. Ridurre o eliminare la necessità di sondaggi [!DNL Privacy Service] API per verificare se un processo è stato completato o se è stata raggiunta una determinata fase cardine all’interno di un flusso di lavoro.

Al momento esistono quattro tipi di notifiche relative al ciclo di vita della richiesta di lavoro per la privacy:

| Tipo | Descrizione |
| --- | --- |
| Processo completato | Tutto [!DNL Experience Cloud] le applicazioni sono state segnalate e lo stato generale o globale del processo è stato contrassegnato come completo. |
| Errore di processo | Una o più applicazioni hanno segnalato un errore durante l&#39;elaborazione della richiesta. |
| Prodotto completo | Una delle applicazioni associate a questo lavoro ha completato il suo lavoro. |
| Errore di prodotto | Una delle applicazioni ha segnalato un errore durante l&#39;elaborazione della richiesta. |

Questo documento fornisce i passaggi per la configurazione di una registrazione evento per [!DNL Privacy Service] e come interpretare i payload di notifica.

## Introduzione

Prima di avviare questa esercitazione, controlla la seguente documentazione di Privacy Service:

* [Panoramica di Privacy Service](./home.md)
* [Guida all’API di Privacy Service](./api/overview.md)

## Registrare un webhook a [!DNL Privacy Service Events]

Per ricevere [!DNL Privacy Service Events], è necessario utilizzare la console Adobe Developer per registrare un webhook nel tuo [!DNL Privacy Service] integrazione.

Segui l’esercitazione su [iscrizione alle notifiche di [!DNL I/O Event]](../observability/alerts/subscribe.md) per passaggi dettagliati su come eseguire questa operazione. Assicurati di scegliere **[!UICONTROL Eventi Privacy Service]** come provider di eventi per accedere agli eventi elencati sopra.

## Ricezione [!DNL Privacy Service Event] Notifiche

Dopo aver registrato correttamente i processi webhook e privacy eseguiti, puoi iniziare a ricevere le notifiche degli eventi. Questi eventi possono essere visualizzati utilizzando il webhook stesso o selezionando **[!UICONTROL Debug Tracing]** nella panoramica sulla registrazione degli eventi del progetto in Adobe Developer Console.

![](images/privacy-events/debug-tracing.png)

Il seguente JSON è un esempio di [!DNL Privacy Service Event] payload di notifica che verrebbe inviato al tuo webhook quando una delle applicazioni associate a un processo di privacy ha completato il suo lavoro:

```json
{
  "id":"b472e249-368b-4706-90f3-1d774713f827",
  "event_id":"b116f797-e50b-432e-9c65-189106a34820",
  "specversion":"0.2",
  "type":"com.adobe.platform.gdpr.productcomplete",
  "source":"https://ns.adobe.com/platform/gdpr",
  "time":"Wed Oct 23 18:52:32 GMT 2019",
  "data":{
    "imsOrg":"{ORG_ID}",
    "value":{
      "jobId":"6f0f2b62-88a7-4515-ba05-432d9a7021c5",
      "message":"analytics.access.complete"
    }
  }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | Un ID univoco generato dal sistema per la notifica. |
| `type` | Il tipo di notifica inviata, con riferimento alle informazioni fornite in `data`. I valori potenziali includono: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Una marca temporale di quando si è verificato l’evento. |
| `data.value` | Contiene informazioni aggiuntive relative all’attivazione della notifica: <ul><li>`jobId`: ID del processo di privacy che ha attivato la notifica.</li><li>`message`: Un messaggio relativo allo stato specifico del processo. Per `productcomplete` o `producterror` notifiche, questo campo indica l’applicazione Experience Cloud in questione.</li></ul> |

## Passaggi successivi

Questo documento illustra come registrare gli eventi di Privacy Service in un webhook configurato e come interpretare i payload di notifica. Per informazioni su come tenere traccia dei processi relativi alla privacy utilizzando l’interfaccia utente, consulta la [Guida utente di Privacy Service](./ui/user-guide.md).
