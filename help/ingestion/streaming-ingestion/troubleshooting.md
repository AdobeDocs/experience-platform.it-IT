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

Questo documento fornisce le risposte alle domande più frequenti sull’acquisizione in streaming su Adobe Experience Platform. Per domande e risoluzione dei problemi relativi ad altri [!DNL Platform] servizi, inclusi quelli incontrati in tutti [!DNL Platform] API, consulta la sezione [Guida alla risoluzione dei problemi di Experience Platform](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] fornisce API RESTful che puoi utilizzare per acquisire dati in [!DNL Experience Platform]. I dati acquisiti vengono utilizzati per aggiornare i profili dei singoli clienti in tempo reale, consentendoti di fornire esperienze personalizzate e rilevanti su più canali. Leggi le [Panoramica sull’acquisizione dei dati](../home.md) per ulteriori informazioni sul servizio e sui diversi metodi di acquisizione. Per i passaggi su come utilizzare le API Streaming Ingestion, leggi [panoramica sull’acquisizione in streaming](../streaming-ingestion/overview.md).

## Domande frequenti

Di seguito è riportato un elenco di risposte alle domande più frequenti sull’acquisizione in streaming.

### Come posso sapere se il payload che invio è formattato correttamente?

[!DNL Data Ingestion] sfrutta [!DNL Experience Data Model] Schemi (XDM) per convalidare il formato dei dati in arrivo. L’invio di dati non conformi alla struttura di uno schema XDM predefinito causerà un errore di acquisizione. Per ulteriori informazioni su XDM e sul suo utilizzo in [!DNL Experience Platform], vedere [Panoramica del sistema XDM](../../xdm/home.md).

L’acquisizione in streaming supporta due modalità di convalida: sincrona e asincrona. Ogni metodo di convalida gestisce i dati non riusciti in modo diverso.

**Convalida sincrona** deve essere utilizzato durante il processo di sviluppo. I record che non superano la convalida vengono eliminati e restituiscono un messaggio di errore indicante il motivo per cui non sono riusciti (ad esempio: &quot;Formato messaggio XDM non valido&quot;).

**Convalida asincrona** deve essere utilizzato in produzione. I dati non validi che non superano la convalida vengono inviati al [!DNL Data Lake] come file batch non riuscito, dove può essere recuperato in un secondo momento per ulteriori analisi.

Per ulteriori informazioni sulla convalida sincrona e asincrona, vedere [panoramica sulla convalida in streaming](../quality/streaming-validation.md). Per i passaggi su come visualizzare i batch che non superano la convalida, consulta la guida su [recupero batch non riusciti](../quality/retrieve-failed-batches.md).

### Posso convalidare un payload di richiesta prima di inviarlo a [!DNL Platform]?

I payload delle richieste possono essere valutati solo dopo l’invio [!DNL Platform]. Quando si esegue la convalida sincrona, i payload validi restituiscono oggetti JSON compilati, mentre i payload non validi restituiscono messaggi di errore. Durante la convalida asincrona, il servizio rileva e invia eventuali dati non validi al [!DNL Data Lake] dove può essere successivamente recuperato per l’analisi. Consulta la [panoramica sulla convalida in streaming](../quality/streaming-validation.md) per ulteriori informazioni.

### Cosa succede quando viene richiesta la convalida sincrona su un perimetro che non la supporta?

Quando la convalida sincrona non è supportata per la posizione richiesta, viene restituita una risposta di errore 501. Consulta la sezione [panoramica sulla convalida in streaming](../quality/streaming-validation.md) per ulteriori informazioni sulla convalida sincrona.

### Come posso garantire che i dati vengano raccolti solo da fonti attendibili?

[!DNL Experience Platform] supporta la raccolta di dati protetti. Quando la raccolta dati autenticati è abilitata, i client devono inviare un token web JSON (JWT) e il relativo ID organizzazione come intestazioni di richiesta. Per ulteriori informazioni su come inviare dati autenticati a [!DNL Platform], consulta la guida su [raccolta dati autenticati](../tutorials/create-authenticated-streaming-connection.md).

### Qual è la latenza per lo streaming dei dati in [!DNL Real-Time Customer Profile]?

Gli eventi in streaming si riflettono generalmente in [!DNL Real-Time Customer Profile] in meno di 60 secondi. Le latenze effettive possono variare a causa del volume dei dati, delle dimensioni dei messaggi e delle limitazioni della larghezza di banda.

### Posso includere più messaggi nella stessa richiesta API?

Puoi raggruppare più messaggi all’interno di un singolo payload di richiesta e inviarli in streaming a [!DNL Platform]. Se utilizzato correttamente, raggruppare più messaggi all’interno di una singola richiesta è un modo eccellente per ottimizzare le operazioni sui dati. Leggi l&#39;esercitazione su [invio di più messaggi in una richiesta](../tutorials/streaming-multiple-messages.md) per ulteriori informazioni.

### Come posso sapere se i dati che sto inviando vengono ricevuti?

Tutti i dati inviati a [!DNL Platform] (correttamente o altrimenti) viene memorizzato come file batch prima di essere mantenuto nei set di dati. Lo stato di elaborazione dei batch viene visualizzato all’interno del set di dati a cui sono stati inviati.

Puoi verificare se i dati sono stati acquisiti correttamente controllando l’attività del set di dati utilizzando [Interfaccia utente di Experienci Platform](https://platform.adobe.com). Clic **[!UICONTROL Set di dati]** nel menu di navigazione a sinistra per visualizzare un elenco di set di dati. Seleziona dall’elenco visualizzato il set di dati a cui stai eseguendo il flusso per aprirne i **[!UICONTROL Attività set di dati]** mostra tutti i batch inviati durante un periodo di tempo selezionato. Per ulteriori informazioni sull&#39;utilizzo di [!DNL Experience Platform] per monitorare i flussi di dati, consulta la guida su [monitoraggio dei flussi di dati](../quality/monitor-data-ingestion.md).

Se i dati non vengono acquisiti correttamente e desideri recuperarli da [!DNL Platform], è possibile recuperare le batch non riuscite inviando i relativi ID al [!DNL Data Access API]. Consulta la guida su [recupero batch non riusciti](../quality/retrieve-failed-batches.md) per ulteriori informazioni.

### Perché i miei dati in streaming non sono disponibili nel Data Lake?

Esistono diversi motivi per cui l’acquisizione batch potrebbe non riuscire a raggiungere [!DNL Data Lake], ad esempio formattazione non valida, dati mancanti o errori di sistema. Per determinare il motivo dell&#39;errore del batch, è necessario recuperare il batch utilizzando [!DNL Data Ingestion Service API] e visualizzarne i dettagli. Per i passaggi dettagliati sul recupero di un batch non riuscito, consulta la guida su [recupero batch non riusciti](../quality/retrieve-failed-batches.md).

### Come si analizza la risposta restituita per la richiesta API?

Puoi analizzare una risposta controllando innanzitutto il codice di risposta del server per determinare se la richiesta è stata accettata. Se viene restituito un codice di risposta corretto, puoi rivedere `responses` array per determinare lo stato dell’attività di acquisizione.

Una richiesta API a messaggio singolo riuscita restituisce il codice di stato 200. Una richiesta di API per messaggi in batch completata o parzialmente completata restituisce il codice di stato 207.

Il seguente JSON è un oggetto di risposta di esempio per una richiesta API con due messaggi: uno riuscito e uno non riuscito. I messaggi inviati correttamente restituiscono un `xactionId` proprietà. I messaggi che non riescono a trasmettere restituiscono un `statusCode` proprietà e una risposta `message` con ulteriori informazioni.

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

Se [!DNL Real-Time Customer Profile] rifiuta un messaggio, probabilmente a causa di informazioni di identità errate. Questo può essere il risultato della fornitura di un valore o uno spazio dei nomi non valido per un’identità.

Esistono due tipi di spazi dei nomi di identità: predefinito e personalizzato. Quando utilizzi spazi dei nomi personalizzati, accertati che lo spazio dei nomi sia stato registrato in [!DNL Identity Service]. Consulta la [panoramica dello spazio dei nomi delle identità](../../identity-service/features/namespaces.md) per ulteriori informazioni sull’utilizzo degli spazi dei nomi predefiniti e personalizzati.

È possibile utilizzare [[!DNL Experience Platform UI]](https://platform.adobe.com) per visualizzare ulteriori informazioni sul motivo per cui l’acquisizione di un messaggio non è riuscita. Clic **[!UICONTROL Monitorare]** nel menu di navigazione a sinistra, quindi visualizza **[!UICONTROL Streaming end-to-end]** per visualizzare i batch di messaggi inviati in streaming durante un periodo di tempo selezionato.
