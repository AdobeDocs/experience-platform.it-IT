---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Iscriviti agli eventi Privacy Service
topic: privacy events
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 1%

---


# Iscriviti a [!DNL Privacy Service Events]

[!DNL Privacy Service Events] sono messaggi forniti da Adobe Experience Platform [!DNL Privacy Service], che sfruttano  eventi Adobe I/O inviati a un webhook configurato per facilitare l’automazione efficiente della richiesta di processo. Essi riducono o eliminano la necessità di eseguire il polling dell&#39; [!DNL Privacy Service] API per verificare se un processo è completo o se è stata raggiunta una determinata fase cardine all&#39;interno di un flusso di lavoro.

Al momento sono disponibili quattro tipi di notifiche relative al ciclo di vita della richiesta di lavoro per la privacy:

| Tipo | Descrizione |
| --- | --- |
| Processo completato | Tutte [!DNL Experience Cloud] le applicazioni hanno riportato un rapporto e lo stato globale o globale del processo è stato contrassegnato come completo. |
| Errore processo | Una o più applicazioni hanno segnalato un errore durante l&#39;elaborazione della richiesta. |
| Prodotto completo | Una delle applicazioni associate a questo processo ha completato il lavoro. |
| Errore del prodotto | Una delle applicazioni ha segnalato un errore durante l&#39;elaborazione della richiesta. |

Questo documento contiene i passaggi necessari per impostare una registrazione dell&#39;evento per [!DNL Privacy Service] le notifiche e per interpretare i payload di notifica.

## Introduzione

Prima di iniziare questa esercitazione, consulta la seguente documentazione Privacy Service:

* [Panoramica Privacy Service](./home.md)
* [Guida per gli sviluppatori API Privacy Service](./api/getting-started.md)

## Registrazione di un webhook [!DNL Privacy Service Events]

Per ricevere [!DNL Privacy Service Events], è necessario utilizzare  Console Sviluppatori di Adobe per registrare un webhook nell&#39; [!DNL Privacy Service] integrazione.

Seguite l’esercitazione sulle [notifiche [!DNL I/O Event] di iscrizione](../observability/notifications/subscribe.md) per i passaggi dettagliati su come ottenere questo risultato. Assicuratevi di scegliere **[!UICONTROL Privacy Service Events]** come fornitore dell&#39;evento per accedere agli eventi elencati sopra.

## Ricevere [!DNL Privacy Service Event] notifiche

Dopo aver registrato correttamente i processi webhook e privacy, potete iniziare a ricevere le notifiche sull&#39;evento. Questi eventi possono essere visualizzati utilizzando il webhook stesso, oppure selezionando la **[!UICONTROL Debug Tracing]** scheda nella panoramica di registrazione dell&#39;evento del progetto in  Adobe Developer Console.

![](images/privacy-events/debug-tracing.png)

Il seguente JSON è un esempio di payload di [!DNL Privacy Service Event] notifica che verrà inviato al tuo webhook quando una delle applicazioni associate a un processo di privacy ha completato il suo lavoro:

```json
{
  "id":"b472e249-368b-4706-90f3-1d774713f827",
  "event_id":"b116f797-e50b-432e-9c65-189106a34820",
  "specversion":"0.2",
  "type":"com.adobe.platform.gdpr.productcomplete",
  "source":"https://ns.adobe.com/platform/gdpr",
  "time":"Wed Oct 23 18:52:32 GMT 2019",
  "data":{
    "imsOrg":"{IMS_ORG}",
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
| `type` | Tipo di notifica inviata, con contesto delle informazioni fornite in `data`. I valori potenziali includono: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Una marca temporale del momento in cui si è verificato l’evento. |
| `data.value` | Contiene informazioni aggiuntive su cosa ha attivato la notifica: <ul><li>`jobId`: ID del processo di privacy che ha attivato la notifica.</li><li>`message`: Un messaggio relativo allo stato specifico del processo. Per `productcomplete` le `producterror` notifiche, questo campo indica l&#39;applicazione del Experience Cloud  in questione.</li></ul> |

## Passaggi successivi

In questo documento è stato illustrato come registrare eventi Privacy Service in un webhook configurato e come interpretare i payload di notifica. Per informazioni su come tenere traccia dei processi relativi alla privacy mediante l’interfaccia utente, consultate la guida [utente relativa ai](./ui/user-guide.md)Privacy Service.