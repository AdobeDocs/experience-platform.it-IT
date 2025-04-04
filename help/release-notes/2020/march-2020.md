---
title: Note sulla versione di Adobe Experience Platform - Marzo 2020
description: Note sulla versione di Adobe Experience Platform di marzo 2020.
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: note sulla versione;
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 20%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 11 marzo 2020**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

* [Governance dei dati](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## Governance dei dati {#governance}

[!DNL Experience Platform] consente alle aziende di unire dati provenienti da più sistemi aziendali per consentire agli addetti al marketing di identificare, comprendere e coinvolgere i clienti. [!DNL Experience Platform] include un&#39;infrastruttura di governance dei dati end-to-end per garantire l&#39;utilizzo corretto dei dati all&#39;interno di [!DNL Experience Platform] e durante la condivisione tra i sistemi.

La governance dei dati di Adobe Experience Platform è una serie di strategie e tecnologie utilizzate per gestire i dati della clientela e garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. Svolge un ruolo chiave all’interno di [!DNL Experience Platform] a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di accesso ai dati e controllo degli accessi ai dati per le azioni di marketing.

**Nuove funzioni**

>[!NOTE]
>
>Alcune delle seguenti nuove funzioni sono attualmente in versione beta e non sono disponibili per tutti gli utenti. Le funzioni di Beta sono soggette a modifiche.

| Funzione | Descrizione |
| ------- | ----------- |
| Applicazione automatica dei criteri di utilizzo dei dati per [!DNL Real-Time Customer Data Platform] | I criteri di utilizzo dei dati vengono ora applicati nel flusso di lavoro di attivazione dei dati nelle destinazioni. La governance dei dati è inoltre incorporata e applicata quando si apportano modifiche che influiscono sulle attivazioni esistenti (come modifiche alle etichette dei set di dati, ai criteri di unione, alle definizioni dei segmenti e altro). |
| Derivazione dei dati per l’applicazione | Quando un criterio di utilizzo dei dati viene violato in Real-Time CDP, l’interfaccia utente visualizza una notifica che contiene informazioni sulla derivazione dei dati per aiutare l’utente a capire perché i criteri sono stati violati e cosa può fare per risolvere la violazione. |


**Problemi noti**

* Nessuna

Per ulteriori informazioni sulla governance dei dati, vedere [Panoramica sulla governance dei dati](../../data-governance/home.md).

## Acquisizione dei dati {#ingestion}

Adobe Experience Platform offre un set completo di funzioni per acquisire qualsiasi tipo e latenza di dati. Adobe Experience Platform [!DNL Data Ingestion] offre diverse alternative per l&#39;acquisizione dei dati, tra cui API Batch, API Streaming, connettori Adobe nativi, partner di integrazione dati o interfaccia utente di Adobe Experience Platform.

**Nuove funzioni**

| Funzione | Descrizione |
|------- | -----------|
| Acquisizione batch parziale | L’acquisizione in batch parziale consente di acquisire dati contenenti errori, fino a una determinata soglia. Grazie a questa funzionalità, gli utenti possono inserire correttamente in Adobe Experience Platform tutti i dati corretti, mentre tutti i dati errati vengono raggruppati in batch separatamente. I dettagli vengono aggiunti ai batch non riusciti per spiegare perché non hanno superato la convalida. Ulteriori informazioni sull&#39;acquisizione in blocco parziale sono disponibili nella [documentazione sull&#39;acquisizione in blocco parziale](../../ingestion/batch-ingestion/partial.md). |

**Problemi noti**

* Nessuna

Per ulteriori informazioni sull&#39;acquisizione di dati in Experience Platform, consulta la [documentazione sull&#39;acquisizione dei dati](../../ingestion/home.md).


## Destinazioni {#destinations}

In [Real-Time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni predefinite con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

**Nuove destinazioni**

Sono disponibili nuove destinazioni in cui puoi attivare i dati Adobe Experience Platform. Per ulteriori informazioni, consulta:

| Destinazione | Descrizione |
|--- | ---|
| Destinazioni di archiviazione cloud | Real-Time CDP ora può distribuire i segmenti come file di dati nei percorsi di archiviazione cloud [!DNL Amazon S3] o SFTP. Questo consente di inviare i tipi di pubblico e i relativi attributi di profilo ai sistemi interni, tramite file CSV o delimitati da tabulazioni. |
| Destinazioni di Advertising | La scheda di destinazione [!DNL Google] è ora divisa in tre schede di destinazione, per le tre diverse piattaforme [!DNL Google] attualmente supportate in Real-Time CDP: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Display e Video 360. |

Per ulteriori informazioni, visita la [panoramica delle destinazioni](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Questo è reso più difficile quando i dati del cliente sono frammentati tra sistemi diversi, facendo apparire ogni singolo cliente con più &quot;identità&quot;.

Adobe Experience Platform [!DNL Identity Service] consente di ottenere una migliore visualizzazione dei clienti e del loro comportamento collegando le identità tra dispositivi e sistemi, consentendo di fornire esperienze digitali personali e di impatto in tempo reale.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Grafico privato avanzato | La funzionalità Private Graph è stata migliorata per ridurre la latenza di generazione del grafico da un processo batch settimanale a un grafico aggiornato ogni giorno, consentendo ai clienti [!DNL Identity Service] di accedere a grafici di identità e collegamenti più aggiornati. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni su [!DNL Identity Service], consulta la [Panoramica del servizio Identity](../../identity-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo consentire di strutturare, etichettare e migliorare tali dati utilizzando i servizi [!DNL Experience Platform]. Puoi acquisire dati da diverse origini, ad esempio da applicazioni Adobe, dall’archiviazione basata su cloud, da software di terze parti e dal sistema CRM.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di configurare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Segnali obsoleti per il connettore Adobe Audience Manager | I dati a livello di segnale da Audience Manager non verranno più inviati. Tieni presente che l’iscrizione al segmento per Caratteristiche e Segmenti continuerà a essere inclusa. In seguito a questa modifica, i set di dati in entrata non verranno più generati. |
| Set di dati rinominati | I set di dati generati dal connettore Audience Manager avranno nomi e descrizioni aggiornati. |
| Attiva/disattiva [!DNL Profile] in Audience Manager | È possibile abilitare o disabilitare l&#39;attivazione di [!DNL Profile] per promuovere il set di dati in [!DNL Real-Time Customer Profile]. L’opzione Attiva/Disattiva sarà attivata per impostazione predefinita. |
| Supporto dell’interfaccia utente per i sistemi di archiviazione cloud | Nuovo connettore di origine per [!DNL Azure Data Lake Storage Gen2] nell&#39;interfaccia utente. |
| Supporto dell’interfaccia utente per i sistemi CRM | Nuovo connettore di origine per [!DNL HubSpot], [!DNL Salesforce Service Cloud] e [!DNL ServiceNow] nell&#39;interfaccia utente. |
| Supporto dell’interfaccia utente per i sistemi di database | Nuovo connettore di origine per [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server] e [!DNL MySQL] nell&#39;interfaccia utente. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni sulle origini, vedere [panoramica delle origini](../../sources/home.md).
