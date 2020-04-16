---
title: 'Note sulla versione di Adobe Experience Platform '
description: Note sulla versione della piattaforma Experience - 11 marzo 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: 33ce1e83514d7aa3cdc5fcee66f444d2fd203097

---


# Note sulla versione di Adobe Experience Platform

## Data di rilascio: 11 marzo 2020

## Governance dei dati

Experience Platform consente alle aziende di unire i dati provenienti da più sistemi aziendali per consentire ai professionisti del marketing di identificare, capire e coinvolgere i clienti. La piattaforma Experience include un&#39;infrastruttura completa per la gestione dei dati, che include l&#39;etichettatura e l&#39;applicazione dell&#39;uso dei dati (DULE), per garantire l&#39;uso corretto dei dati all&#39;interno della piattaforma e quando vengono condivisi tra i sistemi.

Adobe Experience Platform Data Governance è una serie di strategie e tecnologie utilizzate per gestire i dati dei clienti e garantire la conformità a normative, restrizioni e criteri applicabili all&#39;utilizzo dei dati. Essa svolge un ruolo chiave all’interno di Experience Platform a vari livelli, tra cui catalogazione, line-up di dati, etichettatura dell’utilizzo dei dati, criteri di accesso ai dati e controllo dell’accesso ai dati per le azioni di marketing.

### Nuove funzionalità

>[!NOTE] Alcune delle seguenti nuove funzioni sono attualmente in versione beta e non sono disponibili a tutti gli utenti. Le funzioni Beta sono soggette a modifiche.

| Funzione | Descrizione |
| ------- | ----------- |
| Applicazione automatizzata dei criteri di utilizzo dei dati per la piattaforma dati cliente in tempo reale | I criteri di utilizzo dei dati vengono ora applicati nel flusso di lavoro per l&#39;attivazione dei dati alle destinazioni. La governance dei dati è inoltre incorporata e applicata quando si apportano modifiche che interessano le attivazioni esistenti (come modifiche alle etichette dei set di dati, criteri di unione, definizioni dei segmenti e altri). |
| Linea di dati per l&#39;applicazione | Quando un criterio di utilizzo dei dati viene violato in CDP in tempo reale, l&#39;interfaccia utente visualizza una notifica che contiene informazioni sulla linea di dati per aiutare l&#39;utente a capire perché i criteri sono stati violati e cosa possono fare per risolvere la violazione. |


### Problemi noti

* None

Per ulteriori informazioni sulla governance dei dati, consulta la panoramica [sulla governance dei](../../data-governance/home.md)dati.

## Ingestione dati

Adobe Experience Platform offre un set completo di funzioni per acquisire qualsiasi tipo e latenza di dati. L’inserimento dei dati in Adobe Experience Platform offre diverse alternative per l’assimilazione dei dati, tra cui API per batch, API per lo streaming, connettori Adobe nativi, partner per l’integrazione dei dati o l’interfaccia utente di Adobe Experience Platform.

### Nuove funzionalità

| Funzione | Descrizione |
|------- | -----------|
| Iniezione parziale del batch | L&#39;assimilazione parziale dei batch è la capacità di assimilare i dati contenenti errori, fino a una determinata soglia. Grazie a questa funzionalità, gli utenti possono trasferire con successo tutti i dati corretti in Adobe Experience Platform mentre tutti i dati errati vengono raggruppati separatamente. I dettagli vengono aggiunti ai batch non riusciti per spiegare il motivo per cui non hanno superato la convalida. Ulteriori informazioni sull’assimilazione parziale dei batch sono disponibili nella documentazione [di inserimento](../../ingestion/batch-ingestion/partial.md)parziale dei batch. |

### Problemi noti

* None

Per ulteriori informazioni sull’assimilazione dei dati in Piattaforma, consulta la documentazione [sull’inserimento](../../ingestion/home.md)dei dati.


## Destinazioni

In [Adobe Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni preconfigurate con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

### Nuove destinazioni

Sono disponibili nuove destinazioni in cui puoi attivare i dati della tua Adobe Experience Platform. Per ulteriori informazioni, vedere di seguito:

| Destinazione | Descrizione |
|--- | ---|
| Destinazioni di archiviazione cloud | Adobe Real-time CDP è ora in grado di inviare i segmenti come file di dati alle posizioni di archiviazione cloud Amazon S3 o SFTP. Questo consente di inviare audience e i relativi attributi di profilo ai sistemi interni, tramite file CSV o delimitati da tabulazioni. |
| Destinazioni pubblicitarie | La scheda di destinazione Google ora è divisa in tre schede di destinazione, per le tre diverse piattaforme Google attualmente supportate in Adobe Real-time CDP: Google Ads, Google Ad Manager, Google Display &amp; Video 360. |

Per saperne di più, visita la panoramica [delle destinazioni](../../rtcdp/destinations/destinations-overview.md)

## Servizio identità

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Ciò è reso più difficile quando i dati del cliente sono frammentati in sistemi diversi, causando l&#39;apparenza di più &quot;identità&quot; per ogni singolo cliente.

Adobe Experience Platform Identity Service ti aiuta a ottenere una visione migliore del tuo cliente e del suo comportamento attraverso il collegamento di identità tra dispositivi e sistemi, consentendoti di offrire esperienze digitali personali e di forte impatto in tempo reale.

### Nuove funzionalità

| Funzione | Descrizione |
| ------- | ----------- |
| Grafico privato avanzato | La funzionalità di Grafico privato è stata migliorata per ridurre la latenza di generazione del grafico da un processo batch settimanale a un grafico aggiornato ogni giorno, consentendo ai clienti del Servizio identità di accedere a grafici e collegamenti di identità più aggiornati. |

### Problemi noti

* None

Per ulteriori informazioni sul servizio identità, consulta la panoramica [del servizio](../../identity-service/home.md)identità.

## Origini

Adobe Experience Platform è in grado di acquisire dati da origini esterne e allo stesso tempo di strutturarli, etichettarli e ottimizzarli tramite i servizi della piattaforma. È possibile acquisire dati da origini diverse, come applicazioni Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

Experience Platform fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

### Nuove funzionalità

| Funzione | Descrizione |
| ------- | ----------- |
| Segnali obsoleti per il connettore Adobe Audience Manager | I dati a livello di segnale di Audience Manager non verranno più inviati. Si noti che l&#39;appartenenza al segmento per le caratteristiche e i segmenti sarà ancora inclusa. In seguito a questa modifica, i set di dati in entrata non saranno più generati. |
| Set di dati rinominati | I set di dati generati dal connettore Audience Manager avranno nomi e descrizioni aggiornati. |
| Attiva/disattiva profilo in Audience Manager | L&#39;attivazione o la disattivazione del profilo per promuovere il dataset nel profilo cliente in tempo reale. Per impostazione predefinita, Attiva/Disattiva è attivato. |
| Supporto dell&#39;interfaccia utente per i sistemi di storage cloud | Nuovo connettore di origine per Azure Data Lake Storage Gen2 nell&#39;interfaccia utente. |
| Supporto dell&#39;interfaccia utente per i sistemi CRM | Nuovo connettore sorgente per HubSpot, Salesforce Service Cloud e ServiceNow nell’interfaccia utente. |
| Supporto dell&#39;interfaccia utente per i sistemi di database | Nuovo connettore di origine per AWS Redshift, Google BigQuery, MariaDB, Microsoft SQL Server e MySQL nell&#39;interfaccia utente. |

### Problemi noti

* None

Per ulteriori informazioni sulle origini, consultate la panoramica sulle [origini](../../sources/home.md).