---
title: Best practice per la gestione avanzata del ciclo di vita dei dati
description: Scopri come gestire in modo efficiente le richieste di igiene dei dati in Adobe Experience Platform utilizzando l’interfaccia utente di Advanced Data Lifecycle Management e l’API di igiene dei dati. Questa guida descrive le best practice per massimizzare le identità per richiesta, specificare singoli set di dati e prestare attenzione alla limitazione delle API per evitare rallentamenti. Il documento include le linee guida per l’impostazione della pulizia automatica dei set di dati, le modalità di monitoraggio degli stati degli ordini di lavoro e i metodi dettagliati di recupero delle risposte. Segui queste procedure per semplificare l’elaborazione delle richieste e ottimizzare i tempi di risposta.
source-git-commit: 92667fd4da093e56dcf06ae1696484671d9fdd38
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---

# Best practice per la gestione avanzata del ciclo di vita dei dati

Utilizza l’interfaccia utente di Advanced Data Lifecycle Management e l’API di igiene dei dati per gestire in modo efficiente le richieste di pulizia e rimuovere i dati dai servizi Adobe Experience Platform. Segui queste best practice per semplificare l’elaborazione delle richieste e ottimizzare i tempi di risposta per il completamento.

## Prerequisiti {#prerequisites}

Questa guida richiede una buona conoscenza dell’area di lavoro del ciclo di vita dei dati e del [API di igiene dei dati](./api/overview.md). Prima di continuare con questo documento, acquisisci familiarità con le guide [Advanced Data Lifecycle Management](./home.md) e [creazione di richieste di eliminazione record](./ui/record-delete.md) o [Scadenze dei set di dati nell’interfaccia utente](./ui/dataset-expiration.md)o tramite l’API.

## Linee guida per la creazione di ordini di lavoro {#work-order-creation-guidelines}

È possibile utilizzare `/workorder` endpoint nell’API di igiene dei dati per gestire in modo programmatico le richieste di eliminazione dei record in Experienci Platform. Con questo endpoint, puoi creare una richiesta di eliminazione, controllarne lo stato o aggiornare una richiesta esistente. Consulta la [Documento endpoint ordine di lavoro](./api/workorder.md) per scoprire come eseguire queste azioni utilizzando l’API.

>[!TIP]
>
>Un ordine di lavoro è una richiesta strutturata che esegue operazioni specifiche di gestione dei dati, come la pulizia o la trasformazione dei dati, per garantire un’elaborazione efficiente e sistematica.

Segui queste linee guida per ottimizzare gli invii delle richieste di pulizia:

1. **Massimizzare le identità per richiesta:** Per aumentare l’efficienza, includi fino a 100.000 identità per richiesta di pulizia. Il raggruppamento di più identità in un’unica richiesta consente di ridurre la frequenza delle chiamate API e riduce il rischio di problemi di prestazioni a causa di richieste di singole identità eccessive.
2. **Specifica singoli set di dati:** Per la massima efficienza, specifica il singolo set di dati da elaborare.
3. **Inviare più richieste:** Inviare più richieste con il numero massimo di identità per ottenere un&#39;elaborazione più rapida, in quanto gli ordini di lavorazione vengono raggruppati in batch per garantire l&#39;efficienza.
4. **Considerazioni sulla limitazione API:** Presta attenzione alla limitazione delle API per evitare rallentamenti. Richieste più piccole (&lt; 100 ID) con frequenze più alte possono dare luogo a 429 risposte e richiedere una nuova presentazione a tassi accettabili.

### Gestisci errori 429 {#manage-429-errors}

Se viene visualizzato un errore 429, significa che è stato superato il numero consentito di richieste in un determinato periodo di tempo. Segui queste best practice per gestire in modo efficace gli errori 429:

- **Leggi l’intestazione &quot;Riprova dopo&quot;**: quando viene restituito un errore 429, controlla l’intestazione di risposta &quot;Riprova dopo&quot;. Questa intestazione specifica il tempo di attesa prima di riprovare la richiesta.
- **Implementare la logica dei tentativi**: utilizza il valore &quot;Retry-After&quot; per implementare la logica dei nuovi tentativi nell’applicazione, garantendo che i nuovi tentativi vengano tentati dopo il tempo specificato per evitare errori 429 successivi.
- **Creare batch con le richieste**: evita di inviare numerose piccole richieste in rapida successione. Al contrario, raggruppa più identità in un’unica richiesta per ridurre la frequenza delle chiamate e minimizzare il rischio di raggiungere i limiti di frequenza.

## Scadenza set di dati {#dataset-expiration}

Imposta la pulizia automatica dei set di dati per dati di breve durata. Utilizza il `/ttl` endpoint sull’API di igiene dei dati per pianificare le date di scadenza dei set di dati. Utilizza il `/ttl` endpoint per attivare la pulizia di un set di dati in base a un’ora o a una data specificata. Per informazioni su come utilizzare questa funzione, consulta la guida dell’endpoint &quot;Dataset expiration&quot;. [creare una scadenza del set di dati](./api/dataset-expiration.md) e [parametri di query accettati](./api/dataset-expiration.md#query-params).

## Monitorare lo stato di scadenza dell’ordine di lavoro e del set di dati {#monitor}

È possibile monitorare in modo efficiente l&#39;avanzamento della gestione del ciclo di vita dei dati tramite l&#39;utilizzo di **Eventi I/O**. Un evento di I/O è un meccanismo che consente di ricevere notifiche in tempo reale su modifiche o aggiornamenti apportati a vari servizi all’interno di Platform.

Gli avvisi di eventi di I/O possono essere inviati a un webhook configurato per consentire l’automazione del monitoraggio delle attività. Per ricevere avvisi tramite webhook, devi registrarlo per gli avvisi di Platform nella console Adobe Developer. Consulta la guida su [abbonamento a notifiche Adobe I/O Event](../observability/alerts/subscribe.md) per istruzioni dettagliate.

Per recuperare e monitorare in modo efficace gli stati dei processi, utilizzare i metodi e le linee guida del ciclo di vita dei dati seguenti:

### Eventi I/O {#io-events}

Per monitorare in modo efficiente l&#39;avanzamento delle attività del ciclo di vita dei dati, impostare e utilizzare gli eventi di I/O seguendo la procedura riportata di seguito.

- Imposta i webhook per ricevere notifiche push per le modifiche di stato.
- Utilizza le notifiche per monitorare l’avanzamento e ricevere aggiornamenti al completamento.
- Evita di implementare meccanismi di polling per ridurre al minimo il traffico API.

### Recuperare risposte dettagliate per un singolo ordine di lavoro {#retrieve-detailed-work-order-response}

Per informazioni approfondite sui singoli ordini di lavorazione, utilizzare il seguente approccio:

- Effettuare una richiesta di GET al `/workorder{work_order_id}` endpoint per dati di risposta dettagliati.
- Recuperare risposte specifiche per il prodotto e messaggi di successo.
- Evita di utilizzare questo metodo per le normali attività di polling.

Attenendosi a queste best practice, è possibile gestire in modo efficace le richieste di pulizia e ottimizzare i tempi di risposta nell&#39;ambito di Advanced Data Lifecycle Management.
