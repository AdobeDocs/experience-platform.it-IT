---
keywords: ' Experience Platform;home;popolari argomenti;streaming;streaming, assimilazione;risoluzione dei problemi;caricamento in streaming, risoluzione dei problemi;caricamento in streaming, faq;faq;'
solution: Experience Platform
title: Guida alla risoluzione dei problemi di ingestione in streaming
topic: troubleshooting
description: Questo documento contiene le risposte alle domande frequenti sull’assimilazione in streaming su Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---


# Guida alla risoluzione dei problemi di caricamento in streaming

Questo documento contiene le risposte alle domande frequenti sull’assimilazione in streaming su Adobe Experience Platform. Per le domande e la risoluzione dei problemi relativi ad altri servizi [!DNL Platform], compresi quelli che si verificano in tutte le [!DNL Platform] API, fare riferimento alla [ Guida alla risoluzione dei problemi del Experience Platform](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] fornisce RESTful API che è possibile utilizzare per assimilare i dati in [!DNL Experience Platform]. I dati acquisiti vengono utilizzati per aggiornare i profili dei singoli clienti in tempo quasi reale, consentendoti di fornire esperienze personalizzate e pertinenti su più canali. Leggere la [Panoramica sull&#39;inserimento dei dati](../home.md) per ulteriori informazioni sul servizio e sui diversi metodi di inserimento. Per informazioni sull&#39;utilizzo delle API di assimilazione in streaming, consultate la [panoramica sull&#39;assimilazione in streaming](../streaming-ingestion/overview.md).

## Domande frequenti

Segue un elenco di risposte alle domande frequenti sull’assimilazione in streaming.

### Come posso sapere che il payload che sto inviando è formattato correttamente?

[!DNL Data Ingestion] sfrutta gli schemi  [!DNL Experience Data Model] (XDM) per convalidare il formato dei dati in arrivo. L&#39;invio di dati non conformi alla struttura di uno schema XDM predefinito causerà errori di assimilazione. Per ulteriori informazioni su XDM e sul suo utilizzo in [!DNL Experience Platform], vedere la [Panoramica del sistema XDM](../../xdm/home.md).

L&#39;assimilazione dello streaming supporta due modalità di convalida: sincrono e asincrono. Ogni metodo di convalida gestisce i dati non riusciti in modo diverso.

**La** convalida sincrona deve essere utilizzata durante il processo di sviluppo. I record per i quali la convalida non riesce vengono ignorati e restituiscono un messaggio di errore relativo al motivo dell&#39;errore (ad esempio: &quot;Formato messaggio XDM non valido&quot;).

**La** convalida asincrona deve essere utilizzata nella produzione. Eventuali dati non validi che non superano la convalida vengono inviati al file batch [!DNL Data Lake] come file batch non riuscito, dove possono essere recuperati in seguito per ulteriori analisi.

Per ulteriori informazioni sulla convalida sincrona e asincrona, vedere la [panoramica sulla convalida dello streaming](../quality/streaming-validation.md). Per i passaggi su come visualizzare i batch che non superano la convalida, fare riferimento alla guida per il recupero dei batch con errore [](../quality/retrieve-failed-batches.md).

### Posso convalidare un payload di richiesta prima di inviarlo a [!DNL Platform]?

I payload di richieste possono essere valutati solo dopo che sono stati inviati a [!DNL Platform]. Durante l&#39;esecuzione della convalida sincrona, i payload validi restituiscono oggetti JSON popolati mentre i payload non validi restituiscono messaggi di errore. Durante la convalida asincrona, il servizio rileva e invia tutti i dati non corretti alla [!DNL Data Lake], dove successivamente può essere recuperato per l&#39;analisi. Per ulteriori informazioni, vedere la [panoramica sulla convalida dello streaming](../quality/streaming-validation.md).

### Cosa accade quando viene richiesta la convalida sincrona su un bordo che non la supporta?

Se la convalida sincrona non è supportata per la posizione richiesta, viene restituita una risposta di errore 501. Per ulteriori informazioni sulla convalida sincrona, vedere la [panoramica sulla convalida dello streaming](../quality/streaming-validation.md).

### Come posso garantire che i dati vengano raccolti solo da fonti attendibili?

[!DNL Experience Platform] supporta la raccolta dati protetta. Quando la raccolta di dati autenticati è abilitata, i client devono inviare un token Web JSON (JWT) e il relativo ID organizzazione IMS come intestazioni della richiesta. Per ulteriori informazioni sull&#39;invio di dati autenticati a [!DNL Platform], consultare la guida sulla [raccolta di dati autenticati](../tutorials/create-authenticated-streaming-connection.md).

### Qual è la latenza per lo streaming dei dati su [!DNL Real-time Customer Profile]?

Gli eventi in streaming si riflettono generalmente in [!DNL Real-time Customer Profile] in meno di 60 secondi. Le latenze effettive possono variare a causa del volume dei dati, della dimensione del messaggio e delle limitazioni di larghezza di banda.

### Posso includere più messaggi nella stessa richiesta API?

Puoi raggruppare più messaggi all&#39;interno di un singolo payload di richiesta e inviarli in streaming a [!DNL Platform]. Se utilizzati correttamente, il raggruppamento di più messaggi all’interno di una singola richiesta è un metodo eccellente per ottimizzare le operazioni relative ai dati. Per ulteriori informazioni, leggere l&#39;esercitazione su [invio di più messaggi in una richiesta](../tutorials/streaming-multiple-messages.md).

### Come posso sapere se i dati che sto inviando vengono ricevuti?

Tutti i dati inviati a [!DNL Platform] (o comunque correttamente) vengono memorizzati come file batch prima di essere memorizzati nei set di dati. Lo stato di elaborazione dei batch viene visualizzato all’interno del set di dati a cui sono stati inviati.

È possibile verificare se i dati sono stati acquisiti correttamente controllando l&#39;attività del dataset utilizzando l&#39;interfaccia utente del Experience Platform [](https://platform.adobe.com). Fare clic su **[!UICONTROL Datasets]** nella barra di navigazione a sinistra per visualizzare un elenco di set di dati. Selezionare il set di dati a cui si sta eseguendo lo streaming dall&#39;elenco visualizzato per aprire la relativa pagina **[!UICONTROL Dataset activity]**, mostrando tutti i batch inviati durante un periodo di tempo selezionato. Per ulteriori informazioni sull&#39;utilizzo di [!DNL Experience Platform] per monitorare i flussi di dati, consultare la guida sul [monitoraggio dei flussi di dati in streaming](../quality/monitor-data-ingestion.md).

Se il caricamento dei dati non è riuscito e si desidera ripristinarlo da [!DNL Platform], è possibile recuperare i batch non riusciti inviando i relativi ID a [!DNL Data Access API]. Per ulteriori informazioni, vedere la guida relativa al recupero dei batch non riusciti [](../quality/retrieve-failed-batches.md).

### Perché i miei dati di streaming non sono disponibili nel Data Lake?

Esistono diversi motivi per cui l&#39;inserimento batch potrebbe non riuscire a raggiungere il [!DNL Data Lake], ad esempio formattazione non valida, dati mancanti o errori di sistema. Per determinare il motivo dell&#39;errore del batch, è necessario recuperare il batch utilizzando [!DNL Data Ingestion Service API] e visualizzarne i dettagli. Per i passaggi dettagliati sul recupero di un batch non riuscito, vedere la guida in [recupero di batch non riusciti](../quality/retrieve-failed-batches.md).

### Come posso analizzare la risposta restituita per la richiesta API?

Potete analizzare una risposta controllando innanzitutto il codice di risposta del server per determinare se la richiesta è stata accettata. Se viene restituito un codice di risposta corretto, è possibile esaminare l&#39;oggetto array `responses` per determinare lo stato dell&#39;attività di assimilazione.

Una richiesta API per messaggio singolo riuscita restituisce il codice di stato 200. Una richiesta API per messaggi in batch riuscita (o parzialmente riuscita) restituisce il codice di stato 207.

Il seguente JSON è un oggetto di risposta di esempio per una richiesta API con due messaggi: un esito positivo e uno negativo. I messaggi con esito positivo dello streaming restituiscono una proprietà `xactionId`. I messaggi che non riescono a trasmettere in streaming restituiscono una proprietà `statusCode` e una risposta `message` con ulteriori informazioni.

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

Esistono due tipi di spazi dei nomi di identità: predefinito e personalizzato. Quando utilizzate spazi dei nomi personalizzati, accertatevi che lo spazio dei nomi sia stato registrato in [!DNL Identity Service]. Per ulteriori informazioni sull&#39;utilizzo degli spazi dei nomi predefiniti e personalizzati, vedere [panoramica dello spazio dei nomi identità](../../identity-service/namespaces.md).

È possibile utilizzare [[!DNL Experience Platform UI]](https://platform.adobe.com) per visualizzare ulteriori informazioni sul motivo per cui un&#39;operazione di inserimento non è riuscita. Fare clic su **[!UICONTROL Monitoring]** nella navigazione a sinistra, quindi visualizzare la scheda **[!UICONTROL Streaming end-to-end]** per visualizzare i batch di messaggi in streaming durante un periodo di tempo selezionato.
