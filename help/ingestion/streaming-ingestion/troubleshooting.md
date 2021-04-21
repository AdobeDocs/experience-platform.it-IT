---
keywords: Experience Platform;home;argomenti popolari;streaming;streaming ingestion;risoluzione dei problemi;streaming ingestion risoluzione dei problemi;streaming ingestion faq;faq;
solution: Experience Platform
title: Guida alla risoluzione dei problemi di acquisizione in streaming
topic-legacy: troubleshooting
description: Questo documento fornisce le risposte alle domande più frequenti sull’acquisizione in streaming su Adobe Experience Platform.
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi di acquisizione in streaming

Questo documento fornisce le risposte alle domande più frequenti sull’acquisizione in streaming su Adobe Experience Platform. Per domande e risoluzione dei problemi relativi ad altri servizi [!DNL Platform], inclusi quelli riscontrati in tutte le API [!DNL Platform], consulta la [guida alla risoluzione dei problemi di Experience Platform](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] fornisce API RESTful che puoi utilizzare per acquisire dati in [!DNL Experience Platform]. I dati acquisiti vengono utilizzati per aggiornare i profili dei singoli clienti in tempo quasi reale, consentendoti di fornire esperienze personalizzate e rilevanti su più canali. Per ulteriori informazioni sul servizio e sui diversi metodi di acquisizione, consulta la [Panoramica sull’acquisizione dei dati](../home.md) . Per i passaggi su come utilizzare le API Streaming Ingestion, leggi la [panoramica Streaming Ingestion](../streaming-ingestion/overview.md).

## Domande frequenti

Di seguito è riportato un elenco di risposte alle domande frequenti sull’acquisizione in streaming.

### Come posso sapere che il payload che sto inviando è formattato correttamente?

[!DNL Data Ingestion] sfrutta gli schemi  [!DNL Experience Data Model] (XDM) per convalidare il formato dei dati in arrivo. L’invio di dati non conformi alla struttura di uno schema XDM predefinito causerà errori di inserimento. Per ulteriori informazioni su XDM e sul suo utilizzo in [!DNL Experience Platform], consulta la [Panoramica del sistema XDM](../../xdm/home.md).

L’acquisizione in streaming supporta due modalità di convalida: sincrono e asincrono. Ogni metodo di convalida gestisce i dati non riusciti in modo diverso.

**La** convalida sincrona deve essere utilizzata durante il processo di sviluppo. I record per i quali non è stata eseguita la convalida vengono ignorati e restituiscono un messaggio di errore relativo al motivo dell&#39;errore (ad esempio: &quot;Formato del messaggio XDM non valido&quot;).

**La** convalida asincrona deve essere utilizzata in produzione. Eventuali dati non validi che non passano la convalida vengono inviati a [!DNL Data Lake] come file batch non riuscito, dove possono essere recuperati in un secondo momento per ulteriori analisi.

Per ulteriori informazioni sulla convalida sincrona e asincrona, consulta la [panoramica sulla convalida in streaming](../quality/streaming-validation.md). Per i passaggi su come visualizzare i batch con errore di convalida, fare riferimento alla guida sul [recupero dei batch con errore](../quality/retrieve-failed-batches.md).

### Posso convalidare un payload di richiesta prima di inviarlo a [!DNL Platform]?

I payload della richiesta possono essere valutati solo dopo l’invio a [!DNL Platform]. Quando si esegue la convalida sincrona, i payload validi restituiscono oggetti JSON compilati mentre i payload non validi restituiscono messaggi di errore. Durante la convalida asincrona, il servizio rileva e invia tutti i dati in formato non corretto al percorso [!DNL Data Lake] in cui può essere successivamente recuperato per l&#39;analisi. Per ulteriori informazioni, consulta la [panoramica sulla convalida in streaming](../quality/streaming-validation.md) .

### Cosa succede quando viene richiesta la convalida sincrona su un server Edge che non la supporta?

Quando la convalida sincrona non è supportata per la posizione richiesta, viene restituita una risposta di errore 501. Per ulteriori informazioni sulla convalida sincrona, consulta la [panoramica sulla convalida in streaming](../quality/streaming-validation.md) .

### Come posso garantire che i dati vengano raccolti solo da fonti attendibili?

[!DNL Experience Platform] supporta la raccolta dati protetta. Quando la raccolta dati autenticata è abilitata, i client devono inviare un JSON Web Token (JWT) e il loro ID organizzazione IMS come intestazioni della richiesta. Per ulteriori informazioni su come inviare dati autenticati a [!DNL Platform], consulta la guida sulla [raccolta dati autenticati](../tutorials/create-authenticated-streaming-connection.md).

### Qual è la latenza per i dati in streaming a [!DNL Real-time Customer Profile]?

Gli eventi in streaming si riflettono generalmente in [!DNL Real-time Customer Profile] in meno di 60 secondi. Le latenze effettive possono variare a causa del volume di dati, della dimensione del messaggio e delle limitazioni di larghezza di banda.

### Posso includere più messaggi nella stessa richiesta API?

Puoi raggruppare più messaggi all’interno di un singolo payload di richiesta e inviarli in streaming a [!DNL Platform]. Se utilizzato correttamente, il raggruppamento di più messaggi all’interno di una singola richiesta è un modo eccellente per ottimizzare le operazioni sui dati. Per ulteriori informazioni, leggi l’esercitazione sull’ [invio di più messaggi in una richiesta](../tutorials/streaming-multiple-messages.md) .

### Come posso sapere se i dati che sto inviando vengono ricevuti?

Tutti i dati inviati a [!DNL Platform] (con successo o in altro modo) vengono memorizzati come file batch prima di essere memorizzati nei set di dati. Lo stato di elaborazione dei batch viene visualizzato all’interno del set di dati a cui sono stati inviati.

Puoi verificare se i dati sono stati acquisiti correttamente controllando l’attività del set di dati utilizzando l’ [interfaccia utente Experience Platform](https://platform.adobe.com). Fai clic su **[!UICONTROL Datasets]** nel menu di navigazione a sinistra per visualizzare un elenco di set di dati. Seleziona il set di dati a cui stai eseguendo lo streaming dall’elenco visualizzato per aprire la relativa pagina **[!UICONTROL Dataset activity]**, mostrando tutti i batch inviati durante un periodo di tempo selezionato. Per ulteriori informazioni sull&#39;utilizzo di [!DNL Experience Platform] per monitorare i flussi di dati, consulta la guida sul [monitoraggio dei flussi di dati in streaming](../quality/monitor-data-ingestion.md).

Se non è stato possibile acquisire i dati e si desidera ripristinarli da [!DNL Platform], è possibile recuperare i batch con errori inviando i relativi ID a [!DNL Data Access API]. Per ulteriori informazioni, consulta la guida sul [recupero dei batch non riusciti](../quality/retrieve-failed-batches.md) .

### Perché i miei dati in streaming non sono disponibili nel Data Lake?

Ci sono diversi motivi per cui l&#39;acquisizione batch potrebbe non riuscire a raggiungere il [!DNL Data Lake], ad esempio formattazione non valida, dati mancanti o errori di sistema. Per determinare il motivo per cui il batch non è riuscito, è necessario recuperare il batch utilizzando [!DNL Data Ingestion Service API] e visualizzarne i dettagli. Per i passaggi dettagliati sul recupero di un batch non riuscito, vedere la guida sul [recupero dei batch non riusciti](../quality/retrieve-failed-batches.md).

### Come posso analizzare la risposta restituita per la richiesta API?

Puoi analizzare una risposta controllando prima il codice di risposta del server per determinare se la richiesta è stata accettata. Se viene restituito un codice di risposta corretto, è quindi possibile esaminare l’oggetto array `responses` per determinare lo stato dell’attività di acquisizione.

Una richiesta API con messaggio singolo riuscita restituisce il codice di stato 200. Una richiesta API di messaggio in batch riuscita (o parzialmente riuscita) restituisce il codice di stato 207.

Il seguente JSON è un oggetto di risposta di esempio per una richiesta API con due messaggi: un successo e uno fallito. I messaggi che vengono inviati correttamente restituiscono una proprietà `xactionId` . I messaggi che non riescono a eseguire lo streaming restituiscono una proprietà `statusCode` e una risposta `message` con ulteriori informazioni.

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

Se [!DNL Real-time Customer Profile] rifiuta un messaggio, è molto probabile che sia dovuto a informazioni di identità errate. Questo può essere il risultato della fornitura di un valore o di uno spazio dei nomi non valido per un&#39;identità.

Esistono due tipi di spazi dei nomi di identità: predefinito e personalizzato. Quando utilizzi spazi dei nomi personalizzati, accertati che lo spazio dei nomi sia stato registrato in [!DNL Identity Service]. Per ulteriori informazioni sull’utilizzo degli spazi dei nomi predefiniti e personalizzati, consulta la [panoramica dello spazio dei nomi di identità](../../identity-service/namespaces.md) .

Puoi utilizzare [[!DNL Experience Platform UI]](https://platform.adobe.com) per visualizzare ulteriori informazioni sul motivo per cui un messaggio non è stato inserito. Fai clic su **[!UICONTROL Monitoring]** nel menu di navigazione a sinistra, quindi visualizza la scheda **[!UICONTROL Streaming end-to-end]** per visualizzare i batch di messaggi in streaming durante un periodo di tempo selezionato.
