---
keywords: Experience Platform;query;servizio query;risoluzione dei problemi;protezioni;linee guida;limite;
title: Guardrail per il servizio query
description: Questo documento fornisce informazioni sui limiti di utilizzo dei dati del servizio query per facilitare l’ottimizzazione dell’utilizzo della query.
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: 5ceb261dbf1cac58d0cfe620875b8fa7c761abf2
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 2%

---

# Guardrail per il servizio query

Le guardrail sono soglie che guidano i dati e l&#39;utilizzo del sistema, l&#39;ottimizzazione delle prestazioni e la prevenzione di errori o risultati imprevisti in Adobe Experience Platform.

Questo documento fornisce limiti di utilizzo predefiniti per i dati del servizio query per ottimizzare le prestazioni del sistema durante l’esecuzione di query sui dati in relazione alle adesioni alle licenze.

## Prerequisiti

Prima di continuare con questo documento, è necessario avere una buona conoscenza delle definizioni e delle funzionalità chiave del servizio query. Sono descritti di seguito:

* **Query ad hoc**: Per l&#39;esecuzione `SELECT` query per esplorare, sperimentare e convalidare i dati in cui i risultati delle query **non sono memorizzati** sul lago dati.

* **Query batch**: Per l&#39;esecuzione `INSERT TABLE AS SELECT` e `CREATE TABLE AS SELECT` query per pulire, modellare, manipolare e arricchire i dati. I risultati di queste query **sono memorizzati** sul lago dati. La metrica per la misurazione del consumo di questa funzionalità è ore di calcolo.

* **Utenti del servizio query**: Gli utenti di Query Service forniti nella licenza corrente per Customer Journey Analytics, Adobe Real-time Customer Data Platform e/o Adobe Journey Optimizer possono essere utilizzati anche con Data Distiller. Gli utenti del servizio query sono condivisi tra le funzioni.

* **Utenti ad hoc**: Gli utenti ad hoc sono quelli che eseguono query ad hoc.

* **Utenti in batch**: Gli utenti batch sono quelli che eseguono query batch.

* **API di reporting**: Un’API per effettuare chiamate di recupero dati (internamente o esternamente). I modelli di dati per rapporti estesi sono derivati dai modelli di dati per rapporti nativi in Adobe Experience Platform, come il modello dati delle dashboard di Real-Time CDP.

L’illustrazione seguente riepiloga il modo in cui le funzionalità di Query Service vengono attualmente imballate e concesse in licenza:

## Tipi di limite

Questo documento contiene due tipi di limiti predefiniti:

* **Limite morbido**: È tuttavia possibile superare un limite soft, ma i limiti soft forniscono una linea guida consigliata per le prestazioni del sistema.

* **Limite rigido**: Un limite rigido fornisce un massimo assoluto.

>[!NOTE]
>
>I limiti predefiniti descritti in questo documento vengono costantemente migliorati. Controlla regolarmente la disponibilità di aggiornamenti.

## Garanzie sulle prestazioni dell&#39;entità principale

Le tabelle riportate di seguito forniscono i limiti e le descrizioni consigliati per l’esecuzione delle query quando si utilizza un particolare pattern di query.

**Query ad hoc**

| Guardrail | Limite | Tipo di limite | Descrizione |
|---|---|---|---|
| Tempo massimo di esecuzione | 10 minuti | Duro | Definisce il tempo massimo di output per una query SQL ad hoc. Superando il limite di tempo per restituire un risultato, viene generato il codice di errore 53400. |
| Utenti del servizio query simultanei | <ul><li>Come specificato nella descrizione del prodotto dell’applicazione.</li><li>+5 (con ogni pacchetto aggiuntivo aggiuntivo per utenti di query ad hoc acquistato)</li></ul> | Duro | Questo definisce quanti utenti possono creare simultaneamente sessioni per una particolare organizzazione. Se viene superato il limite di concorrenza, l&#39;utente riceve un `Session Limit Reached` errore. |
| Condivisa query | <ul><li>Come specificato nella descrizione del prodotto dell’applicazione.</li><li>+1 (con ogni ulteriore pacchetto SKU aggiuntivo dell&#39;utente di query ad hoc acquistato)</li></ul> | Duro | Questo definisce quante query possono essere eseguite contemporaneamente per una particolare organizzazione. Se viene superato il limite di concorrenza, le query vengono messe in coda. |
| Limite di uscita del connettore client e dei risultati | Connettore client<ul><li>Interfaccia utente della query (100 righe)</li><li>Client di terze parti (50.000)</li><li>[!DNL PostgresSQL] client (50.000)</li></ul> | Duro | Il risultato di una query può essere ricevuto tramite i seguenti mezzi:<ul><li>Interfaccia utente del servizio query</li><li>Client di terze parti</li><li>[!DNL PostgresSQL] client</li></ul>Nota: L&#39;aggiunta di una limitazione al conteggio dei risultati potrebbe restituire i risultati più rapidamente. Ad esempio, `LIMIT 5`, `LIMIT 10` e così via. |
| Risultati restituiti tramite | Interfaccia utente client | N/D | Definisce come i risultati vengono resi disponibili agli utenti. |

{style="table-layout:auto"}

**Query batch**

| **Guardrail** | **Limite** | **Tipo di limite** | **Descrizione** |
|---|---|---|---|
| Tempo massimo di esecuzione | 24 ore | Duro | Definisce il tempo massimo di esecuzione per una query SQL batch.<br>Il tempo di elaborazione di una query dipende dal volume di dati da elaborare e dalla complessità della query. |
| Utenti del servizio query simultanei per batch non pianificato | <ul><li>Come specificato nella descrizione del prodotto dell’applicazione.</li><li>+5 (con ogni pacchetto aggiuntivo aggiuntivo per utenti di query ad hoc acquistato)</li></ul> | Duro | Per le query batch non pianificate (ad esempio le query CTAS/ITAS in modalità interattiva), questo definisce quanti utenti possono creare simultaneamente sessioni per una particolare organizzazione. Se viene superato il limite di concorrenza, l&#39;utente riceve un `Session Limit Reached` errore. |
| Utenti del servizio query simultanei per batch pianificato | Nessun limite utente | N/D | Le query batch pianificate sono processi asincroni, quindi non vi sono limitazioni utente. |
| Ore computazionali per l&#39;elaborazione di dati batch | Come specificato nell&#39;ordine di vendita SKU personalizzati SKU di Adobe Experience Platform Intelligence Query del cliente | Morbido | In questo modo viene definita la quantità di tempo di calcolo per anno consentita a un cliente l’esecuzione di query batch per la scansione, il processo e la riscrittura dei dati nel data lake. |
| Condivisa query | Supportati | N/D | Le query batch pianificate sono processi asincroni, pertanto le query simultanee sono supportate. |
| Limite di uscita del connettore client e risultato | Connettore client<ul><li>Interfaccia utente della query (nessun limite massimo per le righe)</li><li>Client di terze parti (nessun limite massimo alle righe)</li><li>[!DNL PostgresSQL] client (nessun limite massimo alle righe)</li><li>API REST (nessun limite massimo alle righe)</li></ul> | Duro | Il risultato di una query può essere reso disponibile utilizzando i seguenti metodi:<ul><li>Può essere memorizzato come set di dati derivati</li><li>Può essere inserito nei set di dati derivati esistenti</li></ul>Nota: Non esiste un limite superiore al numero del conteggio dei record dal risultato della query. |
| Risultati restituiti tramite | Set di dati | N/D | Definisce come i risultati vengono resi disponibili agli utenti. |

{style="table-layout:auto"}

## Archivio accelerato query {#query-accelerated-store}

La tabella seguente fornisce i limiti e la descrizione consigliati per l’archivio con accelerazione query.

| Guardrail | Limite | Tipo di limite | Descrizione |
|---|---|---|---|
| Condivisa query | 4 | Duro | Per garantire che le query sui dati aggregati tramite l’API di reporting (incluse le query che ottimizzano i modelli di dati come i modelli di dati di Real-Time CDP) dispongano delle risorse da eseguire in modo efficiente, l’API di reporting tiene traccia dell’utilizzo delle risorse assegnando gli slot di concorrenza a ciascuna query. Il sistema mette le query in una coda e attende fino a quando gli slot di concorrenza diventano disponibili o possono essere servite dalla cache. Sono disponibili al massimo quattro slot di query simultanee in un dato momento.<br>Se si accede all’API di reporting tramite uno strumento BI e si desidera una maggiore concorrenza, è necessario un server BI. |

{style="table-layout:auto"}

## Passaggi successivi

Dopo aver letto questo documento, è necessario comprendere meglio i limiti predefiniti per l’esecuzione delle query con i pattern di query disponibili.

Per ulteriori informazioni sul servizio Query, consulta la seguente documentazione:

* [API del servizio query](./api/getting-started.md)
* [Interfaccia utente del servizio query](./ui/overview.md)
