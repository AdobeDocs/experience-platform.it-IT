---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Risoluzione dei problemi di caricamento in streaming
topic: troubleshooting
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---


# Guida alla risoluzione dei problemi di caricamento in streaming

Questo documento contiene le risposte alle domande frequenti sull’assimilazione in streaming  Adobe Experience Platform. Per domande e risoluzione dei problemi relativi ad altri [!DNL Platform] servizi, inclusi quelli che si verificano tra tutte le [!DNL Platform] API, consultare la guida [alla risoluzione dei problemi del](../../landing/troubleshooting.md)Experience Platform.

 Adobe Experience Platform [!DNL Data Ingestion] fornisce API RESTful che potete utilizzare per assimilare i dati in [!DNL Experience Platform]. I dati acquisiti vengono utilizzati per aggiornare i profili dei singoli clienti in tempo quasi reale, consentendoti di fornire esperienze personalizzate e pertinenti su più canali. Per ulteriori informazioni sul servizio e sui diversi metodi di assimilazione, consulta la panoramica [sull’inserimento dei](../home.md) dati. Per informazioni sull’utilizzo delle API di assimilazione in streaming, consultate la panoramica [sull’assimilazione in](../streaming-ingestion/overview.md)streaming.

## Domande frequenti

Segue un elenco di risposte alle domande frequenti sull’assimilazione in streaming.

### Come posso sapere che il payload che sto inviando è formattato correttamente?

[!DNL Data Ingestion] sfrutta gli schemi [!DNL Experience Data Model] (XDM) per convalidare il formato dei dati in arrivo. L&#39;invio di dati non conformi alla struttura di uno schema XDM predefinito causerà errori di assimilazione. Per ulteriori informazioni su XDM e sul suo utilizzo in [!DNL Experience Platform], consultate la panoramica [di sistema](../../xdm/home.md)XDM.

L&#39;assimilazione dello streaming supporta due modalità di convalida: sincrono e asincrono. Ogni metodo di convalida gestisce i dati non riusciti in modo diverso.

**La convalida** sincrona deve essere utilizzata durante il processo di sviluppo. I record per i quali la convalida non riesce vengono ignorati e restituiscono un messaggio di errore relativo al motivo dell&#39;errore (ad esempio: &quot;Formato messaggio XDM non valido&quot;).

**La convalida** asincrona deve essere utilizzata nella produzione. Eventuali dati non validi che non superano la convalida vengono inviati al file batch [!DNL Data Lake] come file batch non riuscito, dove possono essere recuperati in seguito per ulteriori analisi.

Per ulteriori informazioni sulla convalida sincrona e asincrona, vedere la panoramica [sulla convalida](../quality/streaming-validation.md)dello streaming. Per informazioni sulla visualizzazione dei batch con errore di convalida, consultare la guida per il [recupero dei batch](../quality/retrieve-failed-batches.md)non riusciti.

### Posso convalidare un payload di richiesta prima di inviarlo a [!DNL Platform]?

I payload di richieste possono essere valutati solo dopo che sono stati inviati a [!DNL Platform]. Durante l&#39;esecuzione della convalida sincrona, i payload validi restituiscono oggetti JSON popolati mentre i payload non validi restituiscono messaggi di errore. Durante la convalida asincrona, il servizio rileva e invia tutti i dati non corretti al [!DNL Data Lake] punto in cui può essere successivamente recuperato per l&#39;analisi. Per ulteriori informazioni, consulta la panoramica [sulla convalida](../quality/streaming-validation.md) dello streaming.

### Cosa accade quando viene richiesta la convalida sincrona su un bordo che non la supporta?

Se la convalida sincrona non è supportata per la posizione richiesta, viene restituita una risposta di errore 501. Per ulteriori informazioni sulla convalida sincrona, vedere la panoramica [sulla convalida](../quality/streaming-validation.md) in streaming.

### Come posso garantire che i dati vengano raccolti solo da fonti attendibili?

[!DNL Experience Platform] supporta la raccolta dati protetta. Quando la raccolta di dati autenticati è abilitata, i client devono inviare un token Web JSON (JWT) e il relativo ID organizzazione IMS come intestazioni della richiesta. Per ulteriori informazioni su come inviare dati autenticati a [!DNL Platform], consulta la guida sulla raccolta [di dati](../tutorials/create-authenticated-streaming-connection.md)autenticati.

### Qual è la latenza per lo streaming dei dati in [!DNL Real-time Customer Profile]?

Gli eventi in streaming vengono generalmente riportati [!DNL Real-time Customer Profile] in meno di 60 secondi. Le latenze effettive possono variare a causa del volume dei dati, della dimensione del messaggio e delle limitazioni di larghezza di banda.

### Posso includere più messaggi nella stessa richiesta API?

Puoi raggruppare più messaggi all’interno di un singolo payload di richiesta e inviarli in streaming [!DNL Platform]. Se utilizzati correttamente, il raggruppamento di più messaggi all’interno di una singola richiesta è un metodo eccellente per ottimizzare le operazioni relative ai dati. Per ulteriori informazioni, consulta l’esercitazione sull’ [invio di più messaggi in una richiesta](../tutorials/streaming-multiple-messages.md) .

### Come posso sapere se i dati che sto inviando vengono ricevuti?

Tutti i dati inviati a [!DNL Platform] (correttamente o in altro modo) vengono memorizzati come file batch prima di essere memorizzati nei set di dati. Lo stato di elaborazione dei batch viene visualizzato all’interno del set di dati a cui sono stati inviati.

È possibile verificare se i dati sono stati acquisiti correttamente controllando l&#39;attività del dataset utilizzando l&#39;interfaccia [utente del Experience Platform](https://platform.adobe.com). Fare clic **[!UICONTROL Datasets]** nella barra di navigazione a sinistra per visualizzare un elenco di set di dati. Selezionate dall’elenco visualizzato il set di dati a cui si sta eseguendo lo streaming per aprire la *[!UICONTROL Dataset activity]* pagina, mostrando tutti i batch inviati durante un periodo di tempo selezionato. Per ulteriori informazioni sull&#39;utilizzo [!DNL Experience Platform] per monitorare i flussi di dati, consulta la guida sul [monitoraggio dei flussi](../quality/monitor-data-flows.md)di dati in streaming.

Se il caricamento dei dati non è riuscito e si desidera ripristinarlo da [!DNL Platform], è possibile recuperare i batch non riusciti inviando i relativi ID al [!DNL Data Access API]. Per ulteriori informazioni, consulta la guida sul [recupero dei batch](../quality/retrieve-failed-batches.md) con errore.

### Perché i miei dati di streaming non sono disponibili nel Data Lake?

Ci sono diversi motivi per cui l&#39;inserimento batch potrebbe non riuscire a raggiungere il [!DNL Data Lake], ad esempio formattazione non valida, dati mancanti o errori di sistema. Per determinare il motivo per cui il batch ha avuto esito negativo, è necessario recuperare il batch utilizzando il batch [!DNL Data Ingestion Service API] e visualizzarne i dettagli. Per i passaggi dettagliati relativi al recupero di un batch con errore, vedere la guida al [recupero dei batch](../quality/retrieve-failed-batches.md)con errore.

### Come posso analizzare la risposta restituita per la richiesta API?

Potete analizzare una risposta controllando innanzitutto il codice di risposta del server per determinare se la richiesta è stata accettata. Se viene restituito un codice di risposta corretto, è possibile esaminare l&#39;oggetto `responses` array per determinare lo stato dell&#39;attività di assimilazione.

Una richiesta API per messaggio singolo riuscita restituisce il codice di stato 200. Una richiesta API per messaggi in batch riuscita (o parzialmente riuscita) restituisce il codice di stato 207.

Il seguente JSON è un oggetto di risposta di esempio per una richiesta API con due messaggi: un esito positivo e uno negativo. Messaggi che restituiscono correttamente una `xactionId` proprietà. I messaggi che non riescono a trasmettere in streaming restituiscono una `statusCode` proprietà e una risposta `message` con ulteriori informazioni.

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a
                79b25e9421ea127f5] 
                imsOrgId: [{IMS_ORG}] 
                Message has unknown xdm format"
        }
    ]
}
```

### Perché i miei messaggi inviati non vengono ricevuti da [!DNL Real-time Customer Profile]?

Se [!DNL Real-time Customer Profile] rifiuta un messaggio, è probabile che sia dovuto a informazioni di identità errate. Questo può essere il risultato della fornitura di un valore o di uno spazio nomi non validi per un&#39;identità.

Esistono due tipi di spazi dei nomi di identità: predefinito e personalizzato. Quando si utilizzano spazi dei nomi personalizzati, assicurarsi che lo spazio dei nomi sia stato registrato all&#39;interno di [!DNL Identity Service]. Per ulteriori informazioni sull&#39;utilizzo degli spazi dei nomi predefiniti e personalizzati, consultate la panoramica [dello spazio dei nomi](../../identity-service/namespaces.md) identità.

Puoi utilizzare il [!DNL Experience Platform UI](https://platform.adobe.com) per visualizzare ulteriori informazioni sul motivo per cui un messaggio non è stato inviato correttamente. Fai clic **[!UICONTROL Monitoring]** nella barra di navigazione a sinistra, quindi visualizza la _[!UICONTROL Streaming end-to-end]_scheda per visualizzare i batch di messaggi in streaming durante un periodo di tempo selezionato.