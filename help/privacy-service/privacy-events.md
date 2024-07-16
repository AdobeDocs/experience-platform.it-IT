---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Iscriviti agli eventi di Privacy Service
description: Scopri come abbonarti agli eventi di Privacy Service utilizzando un webhook preconfigurato.
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 2%

---

# Iscriviti a [!DNL Privacy Service Events]

[!DNL Privacy Service Events] sono messaggi forniti da Adobe Experience Platform [!DNL Privacy Service], che sfruttano gli eventi Adobe I/O inviati a un webhook configurato per facilitare l&#39;automazione efficiente delle richieste di processo. Riducono o eliminano la necessità di eseguire il polling dell&#39;API [!DNL Privacy Service] per verificare se un processo è stato completato o se è stata raggiunta una determinata fase cardine all&#39;interno di un flusso di lavoro.

Al momento esistono quattro tipi di notifiche relative al ciclo di vita delle richieste di processi per la privacy:

| Tipo | Descrizione |
| --- | --- |
| Processo completato | Tutte le applicazioni [!DNL Experience Cloud] hanno eseguito il report e lo stato complessivo o globale del processo è stato contrassegnato come completato. |
| Errore processo | Una o più applicazioni hanno segnalato un errore durante l’elaborazione della richiesta. |
| Prodotto completato | Una delle applicazioni associate a questo processo ha completato il lavoro. |
| Errore di prodotto | Una delle applicazioni ha segnalato un errore durante l’elaborazione della richiesta. |

In questo documento vengono descritti i passaggi necessari per impostare la registrazione di un evento per le notifiche [!DNL Privacy Service] e per interpretare i payload di notifica.

## Introduzione

Prima di iniziare questo tutorial, consulta la seguente documentazione di Privacy Service:

* [Panoramica di Privacy Service](./home.md)
* [Guida all’API di Privacy Service](./api/overview.md)

## Registra un webhook in [!DNL Privacy Service Events]

Per ricevere [!DNL Privacy Service Events], è necessario utilizzare Adobe Developer Console per registrare un webhook nell&#39;integrazione di [!DNL Privacy Service].

Segui l&#39;esercitazione su [abbonarti alle notifiche [!DNL I/O Event]](../observability/alerts/subscribe.md) per i passaggi dettagliati su come eseguire questa operazione. Accertati di scegliere **[!UICONTROL Eventi Privacy Service]** come provider di eventi per accedere agli eventi elencati sopra.

## Ricevi [!DNL Privacy Service Event] notifiche

Dopo aver registrato correttamente il webhook e aver eseguito i processi relativi alla privacy, puoi iniziare a ricevere le notifiche degli eventi. Questi eventi possono essere visualizzati utilizzando il webhook stesso oppure selezionando la scheda **[!UICONTROL Traccia debug]** nella panoramica della registrazione degli eventi del progetto in Adobe Developer Console.

![](images/privacy-events/debug-tracing.png)

Il seguente codice JSON è un esempio di payload di notifica [!DNL Privacy Service Event] che verrebbe inviato al tuo webhook quando una delle applicazioni associate a un processo di privacy ha completato il proprio lavoro:

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
| `id` | ID univoco generato dal sistema per la notifica. |
| `type` | Tipo di notifica da inviare, che fornisce contesto alle informazioni fornite in `data`. I valori potenziali includono: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Timestamp del momento in cui si è verificato l’evento. |
| `data.value` | Contiene informazioni aggiuntive relative all’attivazione della notifica: <ul><li>`jobId`: ID del processo di privacy che ha attivato la notifica.</li><li>`message`: messaggio relativo allo stato specifico del processo. Per le notifiche `productcomplete` o `producterror`, questo campo indica l&#39;applicazione di Experience Cloud in questione.</li></ul> |

## Passaggi successivi

Questo documento illustra come registrare gli eventi Privacy Service in un webhook configurato e come interpretare i payload di notifica. Per informazioni su come tenere traccia dei processi relativi alla privacy tramite l&#39;interfaccia utente, consulta la [guida utente di Privacy Service](./ui/user-guide.md).
