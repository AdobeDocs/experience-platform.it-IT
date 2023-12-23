---
title: Best practice per Privacy Service
description: Scopri come ridurre i tempi di elaborazione e i costi sostenuti dall’organizzazione durante il completamento delle richieste di accesso a dati personali seguendo queste linee guida sull’uso ottimale.
source-git-commit: c6507a39ba5ae5ca6aa2bf02cf8844a4592152ac
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 0%

---

# Best practice per Privacy Service

Utilizza Privacy Service per automatizzare la conformità alle normative sulla privacy dei dati quando i clienti desiderano accedere ai propri dati personali o eliminarli dagli archivi dei dati. Per soddisfare queste esigenze aziendali in continua evoluzione, Privacy Service offre un’API e un’interfaccia utente RESTful per inviare richieste di accesso e cancellazione dei dati dei clienti nelle applicazioni Adobe Experience Cloud.

Questa guida illustra le best practice per elaborare in modo efficiente le richieste di accesso a dati personali e ottimizzare i tempi di risposta per il completamento delle operazioni durante la gestione delle richieste di dati dei clienti.

## Introduzione {#getting-started}

Questa guida richiede una buona conoscenza di [Privacy Service](./home.md) e come consente di gestire le richieste di accesso ed eliminazione da parte degli interessati (clienti) in tutte le applicazioni Adobe Experience Cloud. Si consiglia inoltre di leggere la guida [creazione di una richiesta di processo per la privacy nell’interfaccia utente](./ui/user-guide.md#create-a-new-privacy-job-request) o [l’API](./api/overview.md)e capire come eseguire queste operazioni a livello di programmazione.

## Prerequisiti {#prerequisites}

L’accesso a Adobe Experience Platform Privacy Service è controllato tramite autorizzazioni granulari basate sui ruoli in Adobe Admin Console. Per utilizzare funzioni specifiche nell’interfaccia utente e nell’API Privacy Service è necessario disporre delle autorizzazioni appropriate in un profilo di prodotto. Se hai bisogno di autorizzazioni aggiuntive, contatta l’amministratore di sistema.

Gli amministratori possono consultare la guida su [gestione delle autorizzazioni per Privacy Service](./permissions.md) per ulteriori informazioni.

## Linee guida per la creazione di posti di lavoro sulla privacy {#creation-guidelines}

Per semplificare l’elaborazione delle richieste e migliorare i tempi di risposta, considera le seguenti linee guida durante la creazione di processi per la privacy. Questo vale sia per i metodi API che per quelli dell’interfaccia utente.

1. **Massimizzare gli interessati per richiesta:** Includi il maggior numero possibile di persone interessate, fino a 1000 per richiesta.
2. **ID gruppo per efficienza:** Raggruppa più ID per un singolo interessato (fino a nove) in ogni richiesta. Il **Gli ID possono provenire da diversi servizi Adobe nella stessa richiesta**.
3. **Combinare processi di accesso ed eliminazione:** Includere entrambi i tipi di processo &quot;accesso&quot; ed &quot;eliminazione&quot; in un’unica richiesta, se richiesto dall’interessato.
4. **Solo i prodotti necessari:** Includi solo i prodotti richiesti o concessi in licenza. Prodotti aggiuntivi possono allungare i tempi di elaborazione e aumentare i costi.

## Monitorare lo stato dei processi relativi alla privacy {#monitor-status}

Per monitorare in modo efficace i processi relativi alla privacy e verificarne lo stato, Privacy Service fornisce tre metodi. I metodi disponibili sono elencati di seguito in ordine di monitoraggio dell&#39;efficienza e della produttività. Ogni metodo include linee guida sulle best practice per migliorare l’esperienza, seguite da uno scenario ideale che combina tutti gli approcci.

### Ricevi notifiche in tempo reale {#real-time-notifications}

**Eventi I/O** monitoraggio dello stato quasi in tempo reale attraverso eventi di stato. Questo è il metodo più efficiente in quanto evita la necessità di implementare meccanismi di polling e di sostenere un traffico API aggiuntivo.

**Recommendations:**

- **Configurazione webhook:** Imposta i webhook per ricevere notifiche push quando si verificano modifiche di stato per i processi inviati. Questo facilita il monitoraggio in tempo reale.
- **Notifiche:** Utilizza le notifiche a livello di processo e di prodotto per monitorare l’avanzamento delle richieste.

Consulta la documentazione su [abbonamento a eventi di Privacy Service](./privacy-events.md) per istruzioni su come impostare la registrazione di un evento per le notifiche Privacy Service e come interpretare i payload di notifica.

### Recupera tutti i processi in base ai filtri {#retrieve-filtered-responses-for-all-jobs}

Per recuperare tutti i dati del processo di privacy in base a filtri specificati, **eseguire una richiesta di GET al `/jobs` endpoint**. Questa chiamata API è utile per fornire una visualizzazione di alto livello dello stato corrente del processo per grandi set di ID processo con una sola richiesta. Non dispone di risposte dettagliate sul prodotto, ma è possibile trovarle utilizzando [`/jobs/{jobID}` endpoint](#retrieve-detailed-responses-for-specific-jobs).

Una richiesta di GET al `/jobs` l’endpoint viene utilizzato in modo migliore per raccogliere o confrontare i dati di stato di un lungo insieme di ID processo, ma **non** destinato alle normali attività di tipo polling.

**Recommendations:**

- **Parametri query:** Utilizza filtri specifici per limitare i risultati, ad esempio: intervalli di dati, tipi di regolamento e stato (elaborazione, completamento e così via).

Puoi visualizzare un elenco di tutti i processi di privacy correnti nell’organizzazione tramite l’interfaccia utente di Privacy Service. Consulta la [gestione dei processi relativi alla privacy nella documentazione dell’interfaccia utente](./ui/user-guide.md#job-requests) per informazioni su come filtrare l&#39;elenco delle richieste di processo. In alternativa, consulta la documentazione sul [utilizzo dell’endpoint /job nell’API Privacy Service](./api/privacy-jobs.md).

La documentazione API di Privacy Service contiene informazioni dettagliate su [filtri dei parametri di query disponibili](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#tag/Privacy-jobs/operation/listPrivacyJobs).

### Recuperare risposte dettagliate per un singolo processo {#retrieve-detailed-responses-for-specific-jobs}

Per recuperare risposte dettagliate per un singolo processo, **eseguire una richiesta di GET a /jobs/{jobID} endpoint**. Questo metodo è destinato a una raccolta di informazioni più approfondita, ad esempio risposte specifiche per prodotto e messaggi di successo. Una chiamata a questo endpoint è il modo migliore per vedere quali prodotti hanno risposto e quali sono ancora in sospeso, anche se è **non** destinato all’attività di polling regolare.

Consulta la `/jobs/{JOB_ID}` documentazione dell’endpoint per dettagli su [come controllare lo stato di un processo specifico](./api/privacy-jobs.md#check-status).

### Esempio di scenario ideale {#ideal-scenario}

Utilizza un webhook in modo che il sistema possa aggiornare automaticamente i record e fornire rapporti o avvisi quando i gruppi degli ID di una richiesta sono completi. Se i processi sono ancora in sospeso, il sistema recupera questi stati di processo con una richiesta GET all’API Privacy Service `/jobs` e fornisce un aggiornamento di alto livello dell&#39;elenco.

Se un particolare processo è ancora in sospeso o ha restituito un errore, puoi recuperare la risposta dettagliata con una richiesta di GET al `/job/{jobId}` endpoint.

## Dati della richiesta di accesso {#access-request-data}

Quando vengono richieste informazioni sull’interessato, ogni servizio restituisce i dati in un formato coerente con il modo in cui memorizzano e utilizzano tali dati. Una volta che tutti i servizi hanno completato la richiesta, nei dettagli del processo viene fornito un URL del file di archivio .ZIP per consentire il download di questi dati. Consulta la guida alla risoluzione dei problemi per informazioni su [come scaricare i risultati del processo di privacy](https://experienceleague.adobe.com/docs/experience-platform/privacy/troubleshooting-guide.html?lang=en#how-do-i-download-the-results-of-my-completed-privacy-jobs%3F).

Di seguito sono riportati gli elementi principali della nota relativi alla gestione dell&#39;archivio dati:

- Tutti i file di archivio vengono eliminati dai server Experienci Platform dopo 30 giorni. Non è possibile eseguire query sui dati dei clienti che hanno più di 30 giorni.
- La struttura del file di archivio include le cartelle per ogni prodotto incluso nella richiesta e i file di dati in essa contenuti. I file o le cartelle di archivio possono essere vuoti se non sono stati trovati dati per l&#39;ID specificato.
- I dati per i processi creati in precedenza sono accessibili solo per 30 giorni dopo la data di completamento. Trascorso questo periodo, i dati vengono rimossi dal sistema ed è necessario effettuare una nuova richiesta.

**Recommendations:**

- **Archivi dati Protect:** Sia il file URL che il file .ZIP devono essere protetti, in quanto possono contenere informazioni personali (PII) per l’interessato.

## Considerazioni tecniche {#technical-considerations}

Quando si completano le richieste Privacy Service è necessario tenere presenti alcune considerazioni tecniche:

- **Periodo di conservazione dei dati:** Il periodo di look-back massimo è di 60 giorni per qualsiasi gruppo di processi e il periodo di tempo massimo per una query è di 30 giorni (le date di inizio/fine).
- **Timeout gateway:** Tieni presente che la richiesta potrebbe essere eliminata dal gateway se supera i 60 secondi.
- **Gestione degli errori:** Rivedi completamente i messaggi di errore e invia nuovamente le richieste, se necessario. Privacy Service non rielabora automaticamente i processi in seguito a un errore.
- **Informazioni sugli errori HTTP 429:** Acquisisci familiarità con i messaggi di errore HTTP 429 e con i passaggi necessari per mitigare i problemi. Gli errori HTTP 429 sono il risultato di &quot;Troppe richieste&quot;. Consulta la [Messaggi di errore comuni](./troubleshooting-guide.md#common-error-messages) sezione della guida alla risoluzione dei problemi per ulteriori informazioni su come risolvere il problema.

## Passaggi successivi

Leggendo questo documento, avrete le conoscenze e le pratiche necessarie per un uso efficiente ed efficace del Privacy Service. Quindi, vedere [guida alla risoluzione dei problemi](./troubleshooting-guide.md) risposte alle domande frequenti su Privacy Service e informazioni sugli errori più comuni riscontrati nell’API.
