---
title: Best practice per la gestione avanzata del ciclo di vita dei dati
description: Scopri come gestire in modo efficiente le richieste di igiene dei dati in Adobe Experience Platform utilizzando l’interfaccia utente di Advanced Data Lifecycle Management e l’API di igiene dei dati. Questa guida descrive le best practice per massimizzare le identità per richiesta, specificare singoli set di dati e prestare attenzione alla limitazione delle API per evitare rallentamenti. Il documento include le linee guida per l’impostazione della pulizia automatica dei set di dati, le modalità di monitoraggio degli stati degli ordini di lavoro e i metodi dettagliati di recupero delle risposte. Segui queste procedure per semplificare l’elaborazione delle richieste e ottimizzare i tempi di risposta.
exl-id: 75e2a97b-ce6c-4ebd-8fc8-597887f77037
source-git-commit: 5174529d606ac0186ff3193790ada70a46c7e274
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# Best practice per la gestione avanzata del ciclo di vita dei dati

Utilizza l’interfaccia utente di Advanced Data Lifecycle Management e l’API di igiene dei dati per gestire in modo efficiente le richieste di pulizia e rimuovere i dati dai servizi Adobe Experience Platform. Segui queste best practice per semplificare l’elaborazione delle richieste e ottimizzare i tempi di risposta per il completamento.

## Prerequisiti {#prerequisites}

Questa guida richiede una buona conoscenza dell&#39;area di lavoro del ciclo di vita dei dati e dell&#39;[API per l&#39;igiene dei dati](./api/overview.md). Prima di continuare questo documento, acquisisci familiarità con le guide di [Advanced Data Lifecycle Management](./home.md) e [creazione di richieste di eliminazione record](./ui/record-delete.md) o [scadenze di set di dati nell&#39;interfaccia utente](./ui/dataset-expiration.md) o tramite l&#39;API.

## Linee guida per la creazione di ordini di lavoro {#work-order-creation-guidelines}

È possibile utilizzare l&#39;endpoint `/workorder` nell&#39;API di igiene dei dati per gestire in modo programmatico le richieste di eliminazione dei record in Experience Platform. Con questo endpoint, puoi creare una richiesta di eliminazione, controllarne lo stato o aggiornare una richiesta esistente. Per informazioni su come eseguire queste azioni utilizzando l&#39;API, consulta il documento [Endpoint ordine di lavoro](./api/workorder.md).

>[!TIP]
>
>Un ordine di lavoro è una richiesta strutturata che esegue operazioni specifiche di gestione dei dati, come la pulizia o la trasformazione dei dati, per garantire un’elaborazione efficiente e sistematica.

Segui queste linee guida per ottimizzare gli invii delle richieste di pulizia:

1. **Massimizza identità per richiesta:** Per migliorare l&#39;efficienza, includi fino a 100.000 identità per richiesta di pulizia. Il raggruppamento di più identità in un’unica richiesta consente di ridurre la frequenza delle chiamate API e riduce il rischio di problemi di prestazioni a causa di richieste di singole identità eccessive. Inviare richieste con il numero massimo di identità per ottenere un&#39;elaborazione più rapida, in quanto gli ordini di lavorazione vengono raggruppati in batch per garantire l&#39;efficienza.
2. **Specificare singoli set di dati:** Per la massima efficienza, specificare il singolo set di dati da elaborare.
3. **Considerazioni sulla limitazione API:** Presta attenzione alla limitazione API per evitare rallentamenti. Richieste più piccole (&lt; 100 ID) con frequenze più alte possono dare luogo a 429 risposte e richiedere una nuova presentazione a tassi accettabili.

### Gestisci errori 429 {#manage-429-errors}

Se viene visualizzato un errore 429, significa che è stato superato il numero consentito di richieste in un determinato periodo di tempo. Segui queste best practice per gestire in modo efficace gli errori 429:

- **Leggi l&#39;intestazione &#39;Retry-After&#39;**: quando viene restituito un errore 429, controlla l&#39;intestazione di risposta &#39;Retry-After&#39;. Questa intestazione specifica il tempo di attesa prima di riprovare la richiesta.
- **Implementare la logica dei tentativi**: utilizzare il valore &#39;Riprova dopo&#39; per implementare la logica dei tentativi nell&#39;applicazione, assicurandosi che i tentativi vengano eseguiti dopo il tempo specificato per evitare errori 429 successivi.
- **Blocca le richieste**: evita di inviare numerose piccole richieste in rapida successione. Al contrario, raggruppa più identità in un’unica richiesta per ridurre la frequenza delle chiamate e minimizzare il rischio di raggiungere i limiti di frequenza.

## Scadenza set di dati {#dataset-expiration}

Imposta la pulizia automatica dei set di dati per dati di breve durata. Utilizza l&#39;endpoint `/ttl` nell&#39;API di igiene dei dati per pianificare le date di scadenza dei set di dati per la pulizia in base a un&#39;ora o a una data specificata. Per informazioni su come [creare una scadenza del set di dati](./api/dataset-expiration.md) e i [parametri di query accettati](./api/dataset-expiration.md#query-params), consulta la guida dell&#39;endpoint &quot;Dataset Exiration&quot;.

## Monitorare lo stato di scadenza dell’ordine di lavoro e del set di dati {#monitor}

È possibile monitorare in modo efficiente l&#39;avanzamento della gestione del ciclo di vita dei dati tramite l&#39;utilizzo di **eventi di I/O**. Un evento di I/O è un meccanismo che consente di ricevere notifiche in tempo reale su modifiche o aggiornamenti apportati a vari servizi all’interno di Platform.

Gli avvisi di eventi di I/O possono essere inviati a un webhook configurato per consentire l’automazione del monitoraggio delle attività. Per ricevere avvisi tramite webhook, devi registrarlo per gli avvisi di Platform in Adobe Developer Console. Per istruzioni dettagliate, consulta la guida su [abbonamento a notifiche evento Adobe I/O](../observability/alerts/subscribe.md).

Per recuperare e monitorare in modo efficace gli stati dei processi, utilizzare i metodi e le linee guida del ciclo di vita dei dati seguenti:

### Eventi I/O {#io-events}

Per monitorare in modo efficiente l&#39;avanzamento delle attività del ciclo di vita dei dati, impostare e utilizzare gli eventi di I/O seguendo la procedura riportata di seguito.

- Imposta i webhook per ricevere notifiche push per le modifiche di stato.
- Utilizza le notifiche per monitorare l’avanzamento e ricevere aggiornamenti al completamento.
- Evita di implementare meccanismi di polling per ridurre al minimo il traffico API.

### Recuperare risposte dettagliate per un singolo ordine di lavoro {#retrieve-detailed-work-order-response}

Per informazioni approfondite sui singoli ordini di lavorazione, utilizzare il seguente approccio:

- Effettuare una richiesta di GET all&#39;endpoint `/workorder/{work_order_id}` per dati di risposta dettagliati.
- Recuperare risposte specifiche per il prodotto e messaggi di successo.
- Evita di utilizzare questo metodo per le normali attività di polling.

Attenendosi a queste best practice, è possibile gestire in modo efficace le richieste di pulizia e ottimizzare i tempi di risposta nell&#39;ambito di Advanced Data Lifecycle Management.
