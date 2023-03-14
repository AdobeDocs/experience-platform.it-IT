---
title: Note sulla versione di Adobe Experience Platform, marzo 2020
description: Note sulla versione di marzo 2020 per Adobe Experience Platform.
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: note sulla versione;
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 6%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 11 marzo 2020**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

* [Governance dei dati](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## Governance dei dati {#governance}

[!DNL Experience Platform] consente alle aziende di unire dati provenienti da più sistemi aziendali per consentire agli addetti al marketing di identificare, comprendere e coinvolgere meglio i clienti. [!DNL Experience Platform] include un’infrastruttura di governance dei dati end-to-end per garantire l’utilizzo corretto dei dati all’interno di [!DNL Platform] e quando vengono condivisi tra i sistemi.

La governance dei dati di Adobe Experience Platform è una serie di strategie e tecnologie utilizzate per gestire i dati dei clienti e garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. Svolge un ruolo chiave in [!DNL Experience Platform] a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di accesso ai dati e controllo degli accessi ai dati per le azioni di marketing.

**Nuove funzioni**

>[!NOTE]
>
>Alcune delle seguenti nuove funzioni sono attualmente in versione beta e non sono disponibili per tutti gli utenti. Le funzioni beta sono soggette a modifiche.

| Funzione | Descrizione |
| ------- | ----------- |
| Applicazione automatizzata dei criteri di utilizzo dei dati per [!DNL Real-Time Customer Data Platform] | I criteri di utilizzo dei dati vengono ora applicati nel flusso di lavoro di attivazione dei dati nelle destinazioni. La governance dei dati è inoltre incorporata e applicata quando si apportano modifiche che influiscono sulle attivazioni esistenti (come modifiche alle etichette dei set di dati, ai criteri di unione, alle definizioni dei segmenti e altro). |
| Derivazione dei dati per l’applicazione | Quando un criterio di utilizzo dei dati viene violato in Real-Time CDP, l’interfaccia utente visualizza una notifica che contiene informazioni sulla derivazione dei dati per aiutare l’utente a capire perché i criteri sono stati violati e cosa può fare per risolvere la violazione. |


**Problemi noti**

* Nessuna

Per ulteriori informazioni sulla governance dei dati, vedi [Panoramica sulla governance dei dati](../../data-governance/home.md).

## Acquisizione dei dati {#ingestion}

Adobe Experience Platform offre un set completo di funzioni per acquisire qualsiasi tipo e latenza di dati. Adobe Experience Platform [!DNL Data Ingestion] fornisce diverse alternative per l’acquisizione dei dati, tra cui API Batch, API Streaming, connettori Adobi nativi, partner di integrazione dei dati o interfaccia utente di Adobe Experience Platform.

**Nuove funzioni**

| Funzione | Descrizione |
|------- | -----------|
| Acquisizione batch parziale | L’acquisizione in batch parziale consente di acquisire dati contenenti errori, fino a una determinata soglia. Grazie a questa funzionalità, gli utenti possono inserire correttamente in Adobe Experience Platform tutti i dati corretti, mentre tutti i dati errati vengono raggruppati in batch separatamente. I dettagli vengono aggiunti ai batch non riusciti per spiegare perché non hanno superato la convalida. Ulteriori informazioni sull’acquisizione batch parziale sono disponibili nella sezione [documentazione parziale sull’acquisizione in blocco](../../ingestion/batch-ingestion/partial.md). |

**Problemi noti**

* Nessuna

Per ulteriori informazioni sull’acquisizione di dati in Platform, visita [Documentazione sull’acquisizione dei dati](../../ingestion/home.md).


## Destinazioni {#destinations}

In entrata [Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni predefinite con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

**Nuove destinazioni**

Sono disponibili nuove destinazioni in cui puoi attivare i dati Adobe Experience Platform. Per ulteriori informazioni, consulta:

| Destinazione | Descrizione |
|--- | ---|
| Destinazioni di archiviazione cloud | Real-Time CDP ora può distribuire i segmenti come file di dati al tuo [!DNL Amazon S3] o posizioni di archiviazione cloud SFTP. Questo consente di inviare i tipi di pubblico e i relativi attributi di profilo ai sistemi interni, tramite file CSV o delimitati da tabulazioni. |
| Destinazioni annunci | Il [!DNL Google] la scheda di destinazione è ora divisa in tre schede di destinazione, per le tre diverse [!DNL Google] piattaforme attualmente supportate in Real-Time CDP: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Display e video 360. |

Per ulteriori informazioni, visita [panoramica sulle destinazioni](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Questo è reso più difficile quando i dati del cliente sono frammentati tra sistemi diversi, facendo apparire ogni singolo cliente con più &quot;identità&quot;.

Adobe Experience Platform [!DNL Identity Service] ti consente di avere una visione migliore del cliente e del suo comportamento collegando le identità tra dispositivi e sistemi, consentendoti di fornire esperienze digitali personali e di impatto in tempo reale.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Grafico privato avanzato | La funzionalità Private Graph è stata migliorata per ridurre la latenza di generazione del grafico, da un processo batch settimanale a un grafico aggiornato ogni giorno, consentendo [!DNL Identity Service] i clienti di accedere a grafici di identità e collegamenti più aggiornati. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni su [!DNL Identity Service], vedere [Panoramica del servizio Identity](../../identity-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando [!DNL Platform] servizi. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

[!DNL Experience Platform] fornisce un’API RESTful e un’interfaccia utente interattiva che consente di configurare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Segnali obsoleti per il connettore Adobe Audience Manager | I dati a livello di segnale da Audience Manager non verranno più inviati. Tieni presente che l’iscrizione al segmento per Caratteristiche e Segmenti continuerà a essere inclusa. In seguito a questa modifica, i set di dati in entrata non verranno più generati. |
| Set di dati rinominati | I set di dati generati dal connettore Audience Manager avranno nomi e descrizioni aggiornati. |
| Abilita [!DNL Profile] attivare/disattivare in Audience Manager | [!DNL Profile] può essere abilitato o disabilitato per promuovere il set di dati in [!DNL Real-Time Customer Profile]. L’opzione Attiva/Disattiva sarà attivata per impostazione predefinita. |
| Supporto dell’interfaccia utente per i sistemi di archiviazione cloud | Nuovo connettore di origine per [!DNL Azure Data Lake Storage Gen2] nell’interfaccia utente. |
| Supporto dell’interfaccia utente per i sistemi CRM | Nuovo connettore di origine per [!DNL HubSpot], [!DNL Salesforce Service Cloud], e [!DNL ServiceNow] nell’interfaccia utente. |
| Supporto dell’interfaccia utente per i sistemi di database | Nuovo connettore di origine per [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server], e [!DNL MySQL] nell’interfaccia utente. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni sulle origini, consulta [panoramica sulle origini](../../sources/home.md).
