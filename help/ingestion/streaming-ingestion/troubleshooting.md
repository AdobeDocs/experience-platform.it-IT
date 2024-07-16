---
keywords: Experience Platform;home;argomenti popolari;streaming;streaming ingestion;risoluzione dei problemi;risoluzione dei problemi di streaming ingestion;streaming ingestion faq;faq;
solution: Experience Platform
title: Guida alla risoluzione dei problemi di acquisizione in streaming
description: Questo documento fornisce le risposte alle domande più frequenti sull’acquisizione in streaming su Adobe Experience Platform.
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi di acquisizione in streaming

Questo documento fornisce le risposte alle domande più frequenti sull’acquisizione in streaming su Adobe Experience Platform. Per domande e risoluzione dei problemi relativi ad altri servizi [!DNL Platform], inclusi quelli incontrati in tutte le API [!DNL Platform], fare riferimento alla [guida alla risoluzione dei problemi di Experience Platform](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] fornisce API RESTful utilizzabili per acquisire dati in [!DNL Experience Platform]. I dati acquisiti vengono utilizzati per aggiornare i profili dei singoli clienti in tempo reale, consentendoti di fornire esperienze personalizzate e rilevanti su più canali. Per ulteriori informazioni sul servizio e sui diversi metodi di acquisizione, consulta la [panoramica sull&#39;acquisizione dei dati](../home.md). Per i passaggi su come utilizzare le API Streaming Ingestion, leggi la [panoramica sull&#39;acquisizione in streaming](../streaming-ingestion/overview.md).

## Domande frequenti

Di seguito è riportato un elenco di risposte alle domande più frequenti sull’acquisizione in streaming.

### Come posso sapere se il payload che invio è formattato correttamente?

[!DNL Data Ingestion] sfrutta gli schemi [!DNL Experience Data Model] (XDM) per convalidare il formato dei dati in arrivo. L’invio di dati non conformi alla struttura di uno schema XDM predefinito causerà un errore di acquisizione. Per ulteriori informazioni su XDM e sul relativo utilizzo in [!DNL Experience Platform], vedere [Panoramica del sistema XDM](../../xdm/home.md).

L’acquisizione in streaming supporta due modalità di convalida: sincrona e asincrona. Ogni metodo di convalida gestisce i dati non riusciti in modo diverso.

**Durante il processo di sviluppo deve essere utilizzata la convalida sincrona**. I record che non superano la convalida vengono eliminati e restituiscono un messaggio di errore indicante il motivo per cui non sono riusciti (ad esempio: &quot;Formato messaggio XDM non valido&quot;).

**La convalida asincrona** deve essere utilizzata in produzione. Eventuali dati non validi che non superano la convalida vengono inviati a [!DNL Data Lake] come file batch non riuscito, dove possono essere recuperati in un secondo momento per ulteriori analisi.

Per ulteriori informazioni sulla convalida sincrona e asincrona, vedere la [panoramica sulla convalida in streaming](../quality/streaming-validation.md). Per i passaggi su come visualizzare i batch che non superano la convalida, consulta la guida su [recupero dei batch non riusciti](../quality/retrieve-failed-batches.md).

### Posso convalidare un payload di richiesta prima di inviarlo a [!DNL Platform]?

I payload delle richieste possono essere valutati solo dopo essere stati inviati a [!DNL Platform]. Quando si esegue la convalida sincrona, i payload validi restituiscono oggetti JSON compilati, mentre i payload non validi restituiscono messaggi di errore. Durante la convalida asincrona, il servizio rileva e invia eventuali dati non validi a [!DNL Data Lake], dove possono essere successivamente recuperati per l&#39;analisi. Per ulteriori informazioni, consulta la [panoramica sulla convalida in streaming](../quality/streaming-validation.md).

### Cosa succede quando viene richiesta la convalida sincrona su un perimetro che non la supporta?

Quando la convalida sincrona non è supportata per la posizione richiesta, viene restituita una risposta di errore 501. Per ulteriori informazioni sulla convalida sincrona, consulta la [panoramica sulla convalida in streaming](../quality/streaming-validation.md).

### Come posso garantire che i dati vengano raccolti solo da fonti attendibili?

[!DNL Experience Platform] supporta la raccolta di dati protetti. Quando la raccolta dati autenticati è abilitata, i client devono inviare un token web JSON (JWT) e il relativo ID organizzazione come intestazioni di richiesta. Per ulteriori informazioni su come inviare dati autenticati a [!DNL Platform], vedere la guida sulla [raccolta dati autenticati](../tutorials/create-authenticated-streaming-connection.md).

### Qual è la latenza per lo streaming dei dati in [!DNL Real-Time Customer Profile]?

Gli eventi in streaming vengono generalmente rispecchiati in [!DNL Real-Time Customer Profile] in meno di 60 secondi. Le latenze effettive possono variare a causa del volume dei dati, delle dimensioni dei messaggi e delle limitazioni della larghezza di banda.

### Posso includere più messaggi nella stessa richiesta API?

È possibile raggruppare più messaggi all&#39;interno di un singolo payload di richiesta e inviarli in streaming a [!DNL Platform]. Se utilizzato correttamente, raggruppare più messaggi all’interno di una singola richiesta è un modo eccellente per ottimizzare le operazioni sui dati. Per ulteriori informazioni, consulta il tutorial su [invio di più messaggi in una richiesta](../tutorials/streaming-multiple-messages.md).

### Come posso sapere se i dati che sto inviando vengono ricevuti?

Tutti i dati inviati a [!DNL Platform] (correttamente o altrimenti) vengono memorizzati come file batch prima di essere memorizzati in modo permanente nei set di dati. Lo stato di elaborazione dei batch viene visualizzato all’interno del set di dati a cui sono stati inviati.

Puoi verificare se i dati sono stati acquisiti correttamente controllando l&#39;attività del set di dati utilizzando l&#39;[interfaccia utente di Experience Platform](https://platform.adobe.com). Fai clic su **[!UICONTROL Set di dati]** nell&#39;area di navigazione a sinistra per visualizzare un elenco di set di dati. Selezionare il set di dati a cui si sta eseguendo il flusso dall&#39;elenco visualizzato per aprire la relativa pagina **[!UICONTROL Attività set di dati]**, in cui sono visualizzati tutti i batch inviati durante un periodo di tempo selezionato. Per ulteriori informazioni sull&#39;utilizzo di [!DNL Experience Platform] per monitorare i flussi di dati, vedere la guida al [monitoraggio dei flussi di dati di streaming](../quality/monitor-data-ingestion.md).

Se i dati non vengono acquisiti e desideri recuperarli da [!DNL Platform], puoi recuperare i batch non riusciti inviando i relativi ID a [!DNL Data Access API]. Per ulteriori informazioni, vedere la guida al [recupero dei batch non riusciti](../quality/retrieve-failed-batches.md).

### Perché i miei dati in streaming non sono disponibili nel Data Lake?

Esistono diversi motivi per cui l&#39;acquisizione batch potrebbe non riuscire a raggiungere [!DNL Data Lake], ad esempio formattazione non valida, dati mancanti o errori di sistema. Per determinare il motivo dell&#39;errore del batch, è necessario recuperare il batch utilizzando [!DNL Data Ingestion Service API] e visualizzarne i dettagli. Per i passaggi dettagliati sul recupero di un batch non riuscito, vedere la guida in [recupero di batch non riusciti](../quality/retrieve-failed-batches.md).

### Come si analizza la risposta restituita per la richiesta API?

Puoi analizzare una risposta controllando innanzitutto il codice di risposta del server per determinare se la richiesta è stata accettata. Se viene restituito un codice di risposta corretto, è possibile rivedere l&#39;oggetto array `responses` per determinare lo stato dell&#39;attività di acquisizione.

Una richiesta API a messaggio singolo riuscita restituisce il codice di stato 200. Una richiesta di API per messaggi in batch completata o parzialmente completata restituisce il codice di stato 207.

Il seguente JSON è un oggetto di risposta di esempio per una richiesta API con due messaggi: uno riuscito e uno non riuscito. I messaggi inviati correttamente restituiscono una proprietà `xactionId`. I messaggi che non riescono a trasmettere restituiscono una proprietà `statusCode` e una risposta `message` con ulteriori informazioni.

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
                imsOrgId: [{ORG_ID}] 
                Message has unknown xdm format"
        }
    ]
}
```

### Perché i miei messaggi inviati non vengono ricevuti da [!DNL Real-Time Customer Profile]?

Se [!DNL Real-Time Customer Profile] rifiuta un messaggio, è probabile che le informazioni di identità non siano corrette. Questo può essere il risultato della fornitura di un valore o uno spazio dei nomi non valido per un’identità.

Esistono due tipi di spazi dei nomi di identità: predefinito e personalizzato. Quando si utilizzano spazi dei nomi personalizzati, assicurarsi che lo spazio dei nomi sia stato registrato in [!DNL Identity Service]. Per ulteriori informazioni sull&#39;utilizzo degli spazi dei nomi predefiniti e personalizzati, consulta la [panoramica dello spazio dei nomi delle identità](../../identity-service/features/namespaces.md).

È possibile utilizzare [[!DNL Experience Platform UI]](https://platform.adobe.com) per visualizzare ulteriori informazioni sul motivo per cui l&#39;acquisizione di un messaggio non è riuscita. Fai clic su **[!UICONTROL Monitoraggio]** nell&#39;area di navigazione a sinistra, quindi visualizza la scheda **[!UICONTROL Streaming end-to-end]** per visualizzare i batch di messaggi inviati in streaming durante un periodo di tempo selezionato.
