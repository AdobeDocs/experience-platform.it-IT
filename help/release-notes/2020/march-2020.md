---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di Experience Platform 11 marzo 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: note sulla versione;
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 6%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 11 marzo 2020**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

* [[!DNL Data Governance]](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## [!DNL Data Governance] {#governance}

[!DNL Experience Platform] consente alle aziende di unire i dati provenienti da più sistemi aziendali per consentire agli addetti al marketing di identificare, comprendere e coinvolgere meglio i clienti. [!DNL Experience Platform] include un&#39;infrastruttura end-to-end per la governance dei dati, al fine di garantire l&#39;uso corretto dei dati all&#39;interno  [!DNL Platform] e quando vengono condivisi tra sistemi.

Adobe Experience Platform [!DNL Data Governance] è una serie di strategie e tecnologie utilizzate per gestire i dati dei clienti e garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. svolge un ruolo chiave all’interno di [!DNL Experience Platform] a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di accesso ai dati e controllo dell’accesso ai dati per le azioni di marketing.

**Nuove funzionalità**

>[!NOTE]
>
>Alcune delle seguenti nuove funzioni sono attualmente in versione beta e non sono disponibili per tutti gli utenti. Le funzioni beta sono soggette a modifiche.

| Funzione | Descrizione |
| ------- | ----------- |
| Applicazione automatica dei criteri di utilizzo dei dati per [!DNL Real-time Customer Data Platform] | I criteri di utilizzo dei dati vengono ora applicati nel flusso di lavoro per l’attivazione dei dati alle destinazioni. [!DNL Data Governance] viene inoltre incorporato e applicato quando si apportano modifiche che influiscono sulle attivazioni esistenti (come modifiche alle etichette dei set di dati, criteri di unione, definizioni di segmenti e altre). |
| Linea di dati per l’applicazione | Quando un criterio di utilizzo dei dati viene violato in Real-time CDP, l’interfaccia utente visualizza una notifica che contiene informazioni di derivazione dei dati per aiutare l’utente a comprendere perché i criteri sono stati violati e cosa può fare per risolvere la violazione. |


**Problemi noti**

* Nessuna

Per ulteriori informazioni su [!DNL Data Governance], consulta la [Panoramica sulla governance dei dati](../../data-governance/home.md).

## Acquisizione dei dati {#ingestion}

Adobe Experience Platform offre un set completo di funzioni per acquisire qualsiasi tipo e latenza di dati. Adobe Experience Platform [!DNL Data Ingestion] offre diverse alternative per l’acquisizione dei dati, tra cui API Batch, API Streaming, connettori Adobe nativi, partner di integrazione dei dati o l’interfaccia utente di Adobe Experience Platform.

**Nuove funzionalità**

| Funzione | Descrizione |
|------- | -----------|
| Acquisizione batch parziale | L’acquisizione parziale in batch è la capacità di acquisire dati contenenti errori, fino a una determinata soglia. Grazie a questa funzionalità, gli utenti possono acquisire correttamente tutti i dati corretti in Adobe Experience Platform mentre tutti i dati errati vengono inseriti in batch separatamente. I dettagli vengono aggiunti ai batch non riusciti per spiegare perché non hanno superato la convalida. Ulteriori informazioni sull&#39;acquisizione parziale dei batch sono disponibili nella [documentazione sull&#39;acquisizione parziale dei batch](../../ingestion/batch-ingestion/partial.md). |

**Problemi noti**

* Nessuna

Per ulteriori informazioni sull’acquisizione di dati in Platform, consulta la [documentazione sull’acquisizione dei dati](../../ingestion/home.md).


## Destinazioni {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni predefinite con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

**Nuove destinazioni**

Sono disponibili nuove destinazioni per l’attivazione dei dati di Adobe Experience Platform. Vedi sotto per i dettagli:

| Destinazione | Descrizione |
|--- | ---|
| Destinazioni di archiviazione cloud | Real-time CDP può ora consegnare i segmenti come file di dati alle [!DNL Amazon S3] posizioni di archiviazione cloud SFTP. Questo consente di inviare i tipi di pubblico e i relativi attributi di profilo ai sistemi interni tramite file CSV o file delimitati da tabulazioni. |
| Destinazioni pubblicitarie | La scheda di destinazione [!DNL Google] è ora divisa in tre schede di destinazione, per le tre diverse piattaforme [!DNL Google] attualmente supportate in Real-time CDP: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Display &amp; Video 360. |

Per ulteriori informazioni, visita la [panoramica delle destinazioni](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Ciò è reso più difficile quando i dati dei clienti sono frammentati in diversi sistemi, il che fa sì che ogni singolo cliente sembri avere più &quot;identità&quot;.

Adobe Experience Platform [!DNL Identity Service] ti aiuta a ottenere una visione migliore del cliente e del suo comportamento attraverso il collegamento di identità tra dispositivi e sistemi, consentendoti di fornire esperienze digitali personali di impatto in tempo reale.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Grafico privato avanzato | La funzionalità Private Graph è stata migliorata per ridurre la latenza di generazione del grafico da un processo batch settimanale a un grafico aggiornato ogni giorno, consentendo ai [!DNL Identity Service] clienti di accedere a grafici di identità e collegamenti più aggiornati. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni su [!DNL Identity Service], consulta la [Panoramica del servizio Identity](../../identity-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi [!DNL Platform] . Puoi acquisire dati da diverse sorgenti, come applicazioni Adobe, archiviazione basata su cloud, software di terze parti e il tuo sistema CRM.

[!DNL Experience Platform] fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Segnali obsoleti per il connettore Adobe Audience Manager | I dati a livello di segnale da Audience Manager non verranno più inviati. Tieni presente che l’appartenenza al segmento per le caratteristiche e i segmenti continuerà a essere inclusa. In seguito a questa modifica, i set di dati in entrata non verranno più generati. |
| Set di dati rinominati | I set di dati generati dal connettore di Audience Manager avranno nomi e descrizioni aggiornati. |
| Attiva/disattiva [!DNL Profile] in Audience Manager | [!DNL Profile] può essere abilitata o disabilitata per promuovere il set di dati a  [!DNL Real-time Customer Profile]. L’opzione Attiva/Disattiva sarà attivata per impostazione predefinita. |
| Supporto dell’interfaccia utente per i sistemi di archiviazione cloud | Nuovo connettore sorgente per [!DNL Azure Data Lake Storage Gen2] nell’interfaccia utente. |
| Supporto dell’interfaccia utente per i sistemi CRM | Nuovo connettore sorgente per [!DNL HubSpot], [!DNL Salesforce Service Cloud] e [!DNL ServiceNow] nell’interfaccia utente. |
| Supporto dell’interfaccia utente per i sistemi di database | Nuovo connettore sorgente per [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server] e [!DNL MySQL] nell’interfaccia utente. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni sulle origini, consulta la [panoramica origini](../../sources/home.md).