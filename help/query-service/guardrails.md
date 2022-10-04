---
keywords: Experience Platform;query;servizio query;risoluzione dei problemi;protezioni;linee guida;limite;
title: Guardrail per il servizio query
description: Questo documento fornisce informazioni sui limiti di utilizzo dei dati del servizio query per facilitare l’ottimizzazione dell’utilizzo della query.
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: 8e5df8b3e38197520c6e15f7c6639c62527c086e
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 3%

---

# Guardrail per il servizio query

Le guardrail sono soglie che forniscono indicazioni sull’utilizzo dei dati e del sistema, sull’ottimizzazione delle prestazioni e sull’eliminazione di errori o risultati imprevisti in Adobe Experience Platform.

Questo documento fornisce limiti di utilizzo predefiniti per i dati del servizio query per ottimizzare le prestazioni del sistema durante l’esecuzione di query sui dati in relazione alle adesioni alle licenze.

## Prerequisiti

Prima di continuare con questo documento, è necessario avere una buona conoscenza delle due funzionalità chiave del servizio Query descritte di seguito:

* **Query ad hoc**: Per l&#39;esecuzione `SELECT` query per esplorare, sperimentare e convalidare i dati in cui i risultati delle query **non sono memorizzati** sul lago dati.

* **Query batch**: Per l&#39;esecuzione `INSERT TABLE AS SELECT` e `CREATE TABLE AS SELECT` query per pulire, modellare, manipolare e arricchire i dati. I risultati di queste query **sono memorizzati** sul lago dati. La metrica per la misurazione del consumo di questa funzionalità è ore di calcolo.

L’illustrazione seguente riepiloga il modo in cui le funzionalità di Query Service vengono attualmente imballate e concesse in licenza:

![Diagramma per spiegare la distribuzione e il packaging delle funzionalità di Query Service in relazione alle licenze.](./images/guardrails/query-capabilities.png)

## Tipi di limite

Questo documento contiene due tipi di limiti predefiniti:

* **Limite morbido**: È possibile superare un limite soft, tuttavia i limiti soft forniscono una linea guida consigliata per le prestazioni del sistema.

* **Limite rigido**: Un limite rigido fornisce un massimo assoluto.

>[!NOTE]
>
>I limiti predefiniti descritti in questo documento vengono costantemente migliorati. Controlla regolarmente la disponibilità di aggiornamenti.

## Garanzie sulle prestazioni dell&#39;entità principale

Le tabelle riportate di seguito forniscono i limiti e le descrizioni consigliati per l’esecuzione delle query quando si utilizza un particolare pattern di query.

**Query ad hoc**

| **Guardrail** | **Limite** | **Tipo di limite** | **Descrizione** |
|---|---|---|---|
| Tempo massimo di esecuzione | 10 minuti | Duro | Definisce il tempo massimo di output per una query SQL ad hoc. Superando il limite di tempo per restituire un risultato, viene generato il codice di errore 53400. |
| Condivisa query | <ul><li>Come specificato nella descrizione del prodotto dell’applicazione.</li><li>+1 (con ogni ulteriore pacchetto SKU aggiuntivo dell&#39;utente di query ad hoc acquistato)</li></ul> | Duro | Questo definisce quante query possono essere eseguite contemporaneamente per una particolare organizzazione. Se viene superato il limite di concorrenza, le query vengono messe in coda. |
| Limite di uscita del connettore client e dei risultati | Connettore client<ul><li>Interfaccia utente della query (100 righe)</li><li>Client di terze parti (50.000)</li><li>[!DNL PostgresSQL] client (50.000)</li></ul> | Duro | Il risultato di una query può essere ricevuto tramite i seguenti mezzi:<ul><li>Interfaccia utente del servizio query</li><li>Client di terze parti</li><li>[!DNL PostgresSQL] client</li></ul>Nota: L&#39;aggiunta di una limitazione al conteggio dei risultati potrebbe restituire i risultati più rapidamente. Ad esempio, `LIMIT 5`, `LIMIT 10` e così via. |
| Risultati restituiti tramite | Interfaccia utente client | N/D | Definisce come i risultati vengono resi disponibili agli utenti. |

{style=&quot;table-layout:auto&quot;}

**Query batch**

| **Guardrail** | **Limite** | **Tipo di limite** | **Descrizione** |
|---|---|---|---|
| Tempo massimo di esecuzione | 24 ore | Duro | Definisce il tempo massimo di esecuzione per una query SQL batch.<br>Il tempo di elaborazione di una query dipende dal volume di dati da elaborare e dalla complessità della query. |
| Condivisa utente | Nessun limite utente | N/D | Le query batch pianificate sono processi asincroni, pertanto non vi sono limitazioni per gli utenti. |
| Ore computazionali per l&#39;elaborazione di dati batch | Come specificato nell&#39;ordine di vendita SKU personalizzati SKU di Adobe Experience Platform Intelligence Query del cliente | Morbido | In questo modo viene definita la quantità di tempo di calcolo per anno consentita a un cliente l’esecuzione di query batch per eseguire la scansione, l’elaborazione e la scrittura di dati nel data lake. |
| Condivisa query | Supportati | N/D | Le query batch pianificate sono processi asincroni, pertanto le query simultanee sono supportate. |
| Limite di uscita del connettore client e risultato | Connettore client<ul><li>Interfaccia utente della query (nessun limite massimo per le righe)</li><li>Client di terze parti (nessun limite massimo alle righe)</li><li>[!DNL PostgresSQL] client (nessun limite massimo alle righe)</li><li>API REST (nessun limite massimo alle righe)</li></ul> | Duro | Il risultato di una query può essere reso disponibile utilizzando i seguenti metodi:<ul><li>Può essere memorizzato come set di dati derivati</li><li>Può essere inserito nei set di dati derivati esistenti</li></ul>Nota: Non esiste un limite superiore al numero del conteggio dei record dal risultato della query. |
| Risultati restituiti tramite | Set di dati | N/D | Definisce come i risultati vengono resi disponibili agli utenti. |

{style=&quot;table-layout:auto&quot;}

Per garantire che ogni query per un dashboard di Real-time Customer Data Platform insights disponga di risorse sufficienti per essere eseguita in modo efficiente, l’API tiene traccia dell’utilizzo delle risorse assegnando spazi di concorrenza a ogni query. Il sistema può elaborare fino a quattro query simultanee e quindi quattro slot di query simultanee sono disponibili in un dato momento. Le query vengono inserite in una coda basata sugli slot di concorrenza, quindi attendono in coda finché non sono disponibili slot di concorrenza sufficienti.

## Passaggi successivi

Dopo aver letto questo documento, è necessario comprendere meglio i limiti predefiniti per l’esecuzione delle query con i pattern di query disponibili.

Per ulteriori informazioni sul servizio Query, consulta la seguente documentazione:

* [API del servizio query](./api/getting-started.md)
* [Interfaccia utente del servizio query](./ui/overview.md)
