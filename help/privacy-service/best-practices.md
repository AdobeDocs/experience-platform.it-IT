---
title: Best practice per Privacy Service
description: Scopri come ridurre i tempi di elaborazione e i costi sostenuti dall’organizzazione durante il completamento delle richieste di accesso a dati personali seguendo queste linee guida sull’uso ottimale.
exl-id: 1333d6c6-5ca0-41c1-9f9e-aa2a5a8b8a9c
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 0%

---

# Best practice per Privacy Service

Utilizza Privacy Service per automatizzare la conformità alle normative sulla privacy dei dati quando i clienti desiderano accedere ai propri dati personali o eliminarli dagli archivi dei dati. Per soddisfare queste esigenze aziendali in continua evoluzione, Privacy Service offre un’API e un’interfaccia utente RESTful per inviare richieste di accesso e cancellazione dei dati dei clienti nelle applicazioni Adobe Experience Cloud.

Questa guida illustra le best practice per elaborare in modo efficiente le richieste di accesso a dati personali e ottimizzare i tempi di risposta per il completamento delle operazioni durante la gestione delle richieste di dati dei clienti.

## Introduzione {#getting-started}

Questa guida richiede una buona conoscenza di [Privacy Service](./home.md) e di come consente di gestire le richieste di accesso ed eliminazione da parte degli interessati (clienti) in tutte le applicazioni Adobe Experience Cloud. Ti consigliamo inoltre di leggere la guida in [creazione di una richiesta di processo per la privacy nell&#39;interfaccia utente](./ui/user-guide.md#create-a-new-privacy-job-request) o [nell&#39;API](./api/overview.md) e di capire come eseguire queste operazioni a livello di programmazione.

## Prerequisiti {#prerequisites}

L’accesso a Adobe Experience Platform Privacy Service è controllato tramite autorizzazioni granulari basate sui ruoli in Adobe Admin Console. Per utilizzare funzioni specifiche nell’interfaccia utente e nell’API Privacy Service è necessario disporre delle autorizzazioni appropriate in un profilo di prodotto. Se hai bisogno di autorizzazioni aggiuntive, contatta l’amministratore di sistema.

Per ulteriori informazioni, gli amministratori possono fare riferimento alla guida su [gestione delle autorizzazioni per Privacy Service](./permissions.md).

## Linee guida per la creazione di posti di lavoro sulla privacy {#creation-guidelines}

Per semplificare l’elaborazione delle richieste e migliorare i tempi di risposta, considera le seguenti linee guida durante la creazione di processi per la privacy. Questo vale sia per i metodi API che per quelli dell’interfaccia utente.

1. **Massimizzare gli interessati per richiesta:** Includere quanti più interessati possibile, fino a 1000, per richiesta.
2. **ID gruppo per efficienza:** raggruppare più ID per un singolo interessato (fino a nove) in ogni richiesta. I **ID possono provenire da diversi servizi Adobe nella stessa richiesta**.
3. **Combinare i processi di accesso ed eliminazione:** Includere entrambi i tipi di processi &quot;accesso&quot; ed &quot;eliminazione&quot; in un&#39;unica richiesta, se richiesto dall&#39;interessato.
4. **Includi solo i prodotti necessari:** Includi solo i prodotti necessari o con licenza. Prodotti aggiuntivi possono allungare i tempi di elaborazione e aumentare i costi.

## Monitorare lo stato dei processi relativi alla privacy {#monitor-status}

Per monitorare in modo efficace i processi relativi alla privacy e verificarne lo stato, Privacy Service fornisce tre metodi. I metodi disponibili sono elencati di seguito in ordine di monitoraggio dell&#39;efficienza e della produttività. Ogni metodo include linee guida sulle best practice per migliorare l’esperienza, seguite da uno scenario ideale che combina tutti gli approcci.

### Ricevi notifiche in tempo reale {#real-time-notifications}

**Eventi di I/O** offrono un monitoraggio dello stato quasi in tempo reale tramite eventi di stato. Questo è il metodo più efficiente in quanto evita la necessità di implementare meccanismi di polling e di sostenere un traffico API aggiuntivo.

**Recommendations:**

- **Configurazione webhook:** Configura i webhook per ricevere notifiche push quando si verificano modifiche di stato per i processi inviati. Questo facilita il monitoraggio in tempo reale.
- **Notifiche:** utilizza le notifiche a livello di processo e di prodotto per monitorare l&#39;avanzamento delle richieste.

Per istruzioni su come impostare la registrazione di un evento per le notifiche Privacy Service e su come interpretare i payload di notifica, consulta la documentazione su [abbonamento a eventi Privacy Service](./privacy-events.md).

### Recupera tutti i processi in base ai filtri {#retrieve-filtered-responses-for-all-jobs}

Per recuperare tutti i dati del processo di privacy in base ai filtri specificati, **esegui una richiesta di GET all&#39;endpoint `/jobs`**. Questa chiamata API è utile per fornire una visualizzazione di alto livello dello stato corrente del processo per grandi set di ID processo con una sola richiesta. Non dispone di risposte dettagliate sul prodotto, ma è possibile trovarle utilizzando l&#39;endpoint [`/jobs/{jobID}`](#retrieve-detailed-responses-for-specific-jobs).

È consigliabile utilizzare una richiesta di GET all&#39;endpoint `/jobs` per raccogliere o confrontare i dati di stato di un set elevato di ID processo, ma **non** è destinato alle normali attività di polling.

**Recommendations:**

- **Parametri query:** Utilizzare filtri specifici per limitare i risultati, ad esempio intervalli di dati, tipi di regolamento e stato (elaborazione, completamento e così via).

Puoi visualizzare un elenco di tutti i processi di privacy correnti nell’organizzazione tramite l’interfaccia utente di Privacy Service. Per informazioni su come filtrare l&#39;elenco di richieste di processo, vedere [gestione dei processi relativi alla privacy nella documentazione dell&#39;interfaccia utente](./ui/user-guide.md#job-requests). In alternativa, consulta la documentazione sull&#39;[utilizzo dell&#39;endpoint /job nell&#39;API Privacy Service](./api/privacy-jobs.md).

La documentazione API di Privacy Service contiene dettagli su [filtri dei parametri di query disponibili](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#tag/Privacy-jobs/operation/listPrivacyJobs).

### Recuperare risposte dettagliate per un singolo processo {#retrieve-detailed-responses-for-specific-jobs}

Per recuperare risposte dettagliate per un singolo processo, **eseguire una richiesta di GET all&#39;endpoint /jobs/{jobID}**. Questo metodo è destinato a una raccolta di informazioni più approfondita, ad esempio risposte specifiche per prodotto e messaggi di successo. Una chiamata a questo endpoint è il modo migliore per vedere quali prodotti hanno risposto e quali sono ancora in sospeso, anche se **non** è destinato all&#39;attività di polling regolare.

Per informazioni dettagliate su [come verificare lo stato di un processo specifico](./api/privacy-jobs.md#check-status), consulta la documentazione dell&#39;endpoint `/jobs/{JOB_ID}`.

### Esempio di scenario ideale {#ideal-scenario}

Utilizza un webhook in modo che il sistema possa aggiornare automaticamente i record e fornire rapporti o avvisi quando i gruppi degli ID di una richiesta sono completi. Se i processi sono ancora in sospeso, il sistema recupera questi stati dei processi con una richiesta GET all&#39;endpoint API Privacy Service `/jobs` e fornisce un aggiornamento di alto livello dell&#39;elenco.

Se un particolare processo è ancora in sospeso o ha restituito un errore, è possibile recuperare la risposta dettagliata con una richiesta GET all&#39;endpoint `/job/{jobId}`.

## Dati della richiesta di accesso {#access-request-data}

Quando vengono richieste informazioni sull’interessato, ogni servizio restituisce i dati in un formato coerente con il modo in cui memorizzano e utilizzano tali dati. Una volta che tutti i servizi hanno completato la richiesta, nei dettagli del processo viene fornito un URL del file di archivio .ZIP per consentire il download di questi dati. Per informazioni su [come scaricare i risultati dei processi per la privacy](https://experienceleague.adobe.com/docs/experience-platform/privacy/troubleshooting-guide.html?lang=en#how-do-i-download-the-results-of-my-completed-privacy-jobs%3F), consulta la guida alla risoluzione dei problemi.

Di seguito sono riportati gli elementi principali della nota relativi alla gestione dell&#39;archivio dati:

- Tutti i file di archivio vengono eliminati dai server Experience Platform dopo 30 giorni. Non è possibile eseguire query sui dati dei clienti che hanno più di 30 giorni.
- La struttura del file di archivio include le cartelle per ogni prodotto incluso nella richiesta e i file di dati in essa contenuti. I file o le cartelle di archivio possono essere vuoti se non sono stati trovati dati per l&#39;ID specificato.
- I dati per i processi creati in precedenza sono accessibili solo per 30 giorni dopo la data di completamento. Trascorso questo periodo, i dati vengono rimossi dal sistema ed è necessario effettuare una nuova richiesta.

**Recommendations:**

- **Archivi dati Protect:** sia l&#39;URL che il file .ZIP devono essere protetti, in quanto potrebbero contenere informazioni personali (PII) per l&#39;interessato.

## Considerazioni tecniche {#technical-considerations}

Quando si completano le richieste Privacy Service è necessario tenere presenti alcune considerazioni tecniche:

- **Periodo di conservazione dei dati:** Il periodo di look-back massimo è di 60 giorni per qualsiasi gruppo di processi e l&#39;intervallo di tempo massimo per una query è di 30 giorni (le date di inizio/fine).
- **Timeout gateway:** ricorda che la richiesta potrebbe essere eliminata dal gateway se supera i 60 secondi.
- **Gestione degli errori:** esaminare i messaggi di errore in modo approfondito e inviare nuovamente le richieste, se necessario. Privacy Service non rielabora automaticamente i processi in seguito a un errore.
- **Informazioni sugli errori HTTP 429:** Acquisisci familiarità con i messaggi di errore HTTP 429 e con i passaggi necessari per risolvere i problemi. Gli errori HTTP 429 sono il risultato di &quot;Troppe richieste&quot;. Per ulteriori informazioni su come risolvere il problema, consulta la sezione [Messaggi di errore comuni](./troubleshooting-guide.md#common-error-messages) della guida alla risoluzione dei problemi.

## Passaggi successivi

Leggendo questo documento, avrete le conoscenze e le pratiche necessarie per un uso efficiente ed efficace del Privacy Service. Quindi, consulta la [guida alla risoluzione dei problemi](./troubleshooting-guide.md) per le risposte alle domande frequenti su Privacy Service e per informazioni sugli errori più comuni riscontrati nell&#39;API.
