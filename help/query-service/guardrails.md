---
keywords: Experience Platform;query;servizio query;risoluzione dei problemi;guardrail;linee guida;limite;
title: Guardrail per Query Service
description: In questo documento vengono fornite informazioni sui limiti di utilizzo per i dati di Query Service, utili per ottimizzare l’utilizzo delle query.
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: 23c7a4590b365a49edb066567b6ebe2ac08c67e8
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 2%

---

# Guardrail per Query Service

I guardrail sono soglie che guidano l’utilizzo dei dati e del sistema, l’ottimizzazione delle prestazioni e la prevenzione di errori o risultati imprevisti in Adobe Experience Platform.
In questo documento vengono indicati i limiti di utilizzo predefiniti per i dati di Query Service, che consentono di ottimizzare le prestazioni del sistema durante l’esecuzione di query sui dati in relazione ai diritti di licenza.

>[!IMPORTANT]
>
>Controlla i diritti di licenza nell&#39;ordine di vendita e la corrispondente [descrizione del prodotto](https://helpx.adobe.com/it/legal/product-descriptions.html) sui limiti di utilizzo effettivi, oltre a questa pagina di guardrail.

## Prerequisiti

Prima di continuare con questo documento, è necessario avere una buona conoscenza delle definizioni e delle funzionalità chiave di Query Service. Sono descritti di seguito:

* **Query ad hoc**: per l&#39;esecuzione di `SELECT` query per esplorare, sperimentare e convalidare dati in cui i risultati delle query **non sono archiviati** nel data lake.

* **Query batch**: per l&#39;esecuzione di `INSERT TABLE AS SELECT` e `CREATE TABLE AS SELECT` query per pulire, modellare, manipolare e arricchire dati. I risultati di queste query **sono archiviati** nel data lake. La metrica per misurare il consumo di questa funzionalità è costituita dalle ore di calcolo.

* **Utenti Query Service**: gli utenti Query Service forniti nella licenza corrente per Customer Journey Analytics, Adobe Real-Time Customer Data Platform e/o Adobe Journey Optimizer possono essere utilizzati anche con Data Distiller. Gli utenti di Query Service sono condivisi tra le varie funzionalità.

* **Utenti ad hoc**: gli utenti ad hoc eseguono query ad hoc.

* **Utenti batch**: gli utenti batch eseguono query batch.

* **API di reporting**: API per l&#39;esecuzione di chiamate di recupero dati (internamente o esternamente). I modelli dati per rapporti estesi sono derivati dai modelli dati nativi per rapporti in Adobe Experience Platform, ad esempio il modello dati delle dashboard di Real-Time CDP.

## Tipi di guardrail

In questo documento sono disponibili due tipi di limiti predefiniti:

| Tipo di guardrail | Descrizione |
|----------|---------|
| **Guardrail delle prestazioni (limite software)** | I guardrail di prestazioni sono limiti di utilizzo relativi all’ambito dei tuoi casi d’uso. Quando si superano i guardrail delle prestazioni, è possibile che si verifichi un peggioramento delle prestazioni e della latenza. Adobe non è responsabile di tale degrado delle prestazioni. I clienti che superano costantemente il limite di prestazioni possono scegliere di concedere licenze aggiuntive per evitare il degrado delle prestazioni. |
| **Guardrail applicati dal sistema (limite rigido)** | I guardrail applicati dal sistema vengono applicati dall’interfaccia utente o dall’API di Real-Time CDP. Questi sono i limiti che non puoi superare, poiché l’interfaccia utente e l’API ti impediranno di farlo o restituiranno un errore. |

{style="table-layout:auto"}

>[!NOTE]
>
>I limiti predefiniti descritti in questo documento vengono costantemente migliorati. Controlla regolarmente se ci sono aggiornamenti.

## Guardrail delle prestazioni dell’entità primaria

Le tabelle seguenti forniscono i limiti di guardrail e le descrizioni consigliati per l’esecuzione di query quando si utilizza un particolare modello di query.

**Query ad hoc**

| Guardrail | Limite | Tipo di limite | Descrizione |
|---|---|---|---|
| Tempo massimo di esecuzione | 10 minuti | Guarddrail imposto dal sistema | Definisce il tempo massimo di output per una query SQL ad hoc. Il superamento del limite di tempo per restituire un risultato genera il codice di errore 53400. |
| Utenti di Concurrent Query Service | <ul><li>Come specificato nella descrizione del prodotto dell’applicazione.</li><li>+5 (con ogni pacchetto aggiuntivo ad hoc per utenti di query acquistato)</li></ul> | Guarddrail imposto dal sistema | Questo definisce quanti utenti possono creare sessioni simultaneamente per una particolare organizzazione. Se il limite di concorrenza viene superato, l&#39;utente riceve un errore `Session Limit Reached`. |
| Concorrenza query | <ul><li>Come specificato nella descrizione del prodotto dell’applicazione.</li><li>+1 (con ogni pacchetto SKU aggiuntivo utente per query ad hoc acquistato)</li></ul> | Guarddrail imposto dal sistema | Definisce quante query possono essere eseguite contemporaneamente per una particolare organizzazione. Se viene superato il limite di concorrenza, le query vengono messe in coda. |
| Connettore client e limite di output dei risultati | Connettore client<ul><li>Interfaccia query (100 righe)</li><li>Cliente di terze parti (50.000)</li><li>[!DNL PostgresSQL] client (50.000)</li></ul> | Guarddrail imposto dal sistema | Il risultato di una query può essere ricevuto nei modi seguenti:<ul><li>Interfaccia utente di Query Service</li><li>Client di terze parti</li><li>[!DNL PostgresSQL] client</li></ul>Nota: l’aggiunta di un limite al conteggio degli output potrebbe restituire risultati più rapidamente. Ad esempio, `LIMIT 5`, `LIMIT 10` e così via. |
| Risultati restituiti tramite | Interfaccia utente client | N/D | Definisce il modo in cui i risultati vengono resi disponibili agli utenti. |

{style="table-layout:auto"}

**Query batch**

| **Guardrail** | **Limite** | **Tipo limite** | **Descrizione** |
|---|---|---|---|
| Tempo massimo di esecuzione | 24 ore | Guarddrail imposto dal sistema | Definisce il tempo massimo di esecuzione per una query SQL batch.<br>Il tempo di elaborazione di una query dipende dal volume di dati da elaborare e dalla complessità della query. |
| Utenti del servizio di query simultanee per batch non pianificato | <ul><li>Come specificato nella descrizione del prodotto dell’applicazione.</li><li>+5 (con ogni pacchetto aggiuntivo ad hoc per utenti di query acquistato)</li></ul> | Guarddrail imposto dal sistema | Per le query batch non pianificate (ad esempio le query CTAS/ITAS in modalità interattiva), questo definisce quanti utenti possono creare sessioni simultaneamente per una particolare organizzazione. Se il limite di concorrenza viene superato, l&#39;utente riceve un errore `Session Limit Reached`. |
| Utenti di Query Service simultanei per batch pianificato | Nessun limite utente | N/D | Le query batch pianificate sono processi asincroni, quindi non esistono limitazioni per gli utenti. |
| Ore di calcolo per l’elaborazione dei dati in batch | Come specificato nell&#39;ordine cliente SKU personalizzato di Adobe Experience Platform Intelligence Query del cliente | Guardrail delle prestazioni | Questo definisce la quantità di tempo computazionale nell’ambito per anno consentita a un cliente per l’esecuzione di query batch al fine di analizzare, elaborare e riscrivere i dati nel data lake. |
| Concorrenza query | Supportato | N/D | Le query batch pianificate sono processi asincroni, pertanto sono supportate le query simultanee. |
| Connettore client e limite di output dei risultati | Connettore client<ul><li>Interfaccia utente Query (nessun limite superiore alle righe)</li><li>Client di terze parti (nessun limite superiore alle righe)</li><li>[!DNL PostgresSQL] client (nessun limite superiore alle righe)</li><li>API REST (nessun limite superiore alle righe)</li></ul> | Guarddrail imposto dal sistema | Il risultato di una query può essere reso disponibile utilizzando i metodi seguenti:<ul><li>Può essere memorizzato come set di dati derivati</li><li>Può essere inserito nei set di dati derivati esistenti</li></ul>Nota: non esiste alcun limite superiore al numero di conteggio dei record risultante dal risultato della query. |
| Risultati restituiti tramite | Set di dati | N/D | Definisce il modo in cui i risultati vengono resi disponibili agli utenti. |

{style="table-layout:auto"}

## Archivio accelerato query {#query-accelerated-store}

La tabella seguente fornisce i limiti di guardrail e la descrizione consigliati per l’archivio query accelerato.

| Guardrail | Limite | Tipo di limite | Descrizione |
|---|---|---|---|
| Concorrenza query | 4 | Guarddrail imposto dal sistema | Per garantire che le query sui dati aggregati tramite l’API di reporting (incluse le query che migliorano i modelli di dati come i modelli di dati di Real-Time CDP) dispongano delle risorse per essere eseguite in modo efficiente, l’API di reporting tiene traccia dell’utilizzo delle risorse assegnando slot di concorrenza a ogni query. Il sistema mette le query in coda e attende che gli slot di concorrenza siano disponibili o che possano essere serviti dalla cache. Sono disponibili al massimo quattro slot di query simultanei in un determinato momento.<br>Se si accede all&#39;API di reporting tramite uno strumento BI e si necessita di maggiore concorrenza, è necessario un server BI. |

{style="table-layout:auto"}

## Passaggi successivi

Dopo aver letto questo documento, sarai in grado di comprendere meglio i limiti predefiniti per l’esecuzione delle query con i modelli di query disponibili.

Per ulteriori informazioni su Query Service, consulta la seguente documentazione:

* [API servizio query](./api/getting-started.md)
* [Interfaccia utente di Query Service](./ui/overview.md)

Consulta la seguente documentazione per ulteriori informazioni su altri guardrail dei servizi Experience Platform, sulla latenza end-to-end e sulle licenze dai documenti di descrizione del prodotto Real-Time CDP:

* [Guardrail Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagrammi di latenza end-to-end](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) per vari servizi Experience Platform.
* [Real-Time Customer Data Platform (Edizione B2C - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)