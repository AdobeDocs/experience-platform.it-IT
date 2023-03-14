---
title: Note sulla versione di Adobe Experience Platform - Gennaio 2021
description: Note sulla versione di gennaio 2021 per Adobe Experience Platform.
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 5%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 27 gennaio 2021**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Funzioni espressione regolare | [!DNL Data Prep] Mapper ora supporta la corrispondenza e l’estrazione di parte del campo di input in base alle espressioni regolari. |

Per ulteriori informazioni, vedere [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni preconfigurate con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] è la soluzione di archiviazione di oggetti di Microsoft per il cloud. |

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Corrispondenza ID avanzata | Miglioramenti alle funzionalità di audience match rate (tasso di corrispondenza del pubblico) in [!DNL Facebook Custom Audiences] e [!DNL Google Customer Match], aggiungendo il supporto per la corrispondenza di identità aggiuntiva, ad esempio ID esterni, numeri di telefono e ID del dispositivo mobile. Per ulteriori informazioni, consulta la seguente documentazione: <ul><li>[Destinazione facebook](../../destinations/catalog/social/facebook.md)</li><li>[Destinazione Customer Match di Google](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[Attiva i dati del pubblico nelle destinazioni di esportazione di segmenti di streaming](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

Per ulteriori informazioni, visita [panoramica sulle destinazioni](../../destinations/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di offrire ai tuoi clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con Real-Time Customer Profile puoi visualizzare una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, del sistema CRM e di terze parti. [!DNL Profile] consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Elimina set di dati dall’archivio profili | Quando elimini un set di dati dal Data Lake di Experience Platform, questo viene eliminato automaticamente anche dall’archivio Profili. Non è più necessario utilizzare l’endpoint API dei processi del sistema di profili per effettuare una richiesta di eliminazione al fine di eliminare esplicitamente il set di dati dall’archivio profili. Per ulteriori informazioni, vedere [guida dell’endpoint API dei processi di sistema del profilo](../../profile/api/profile-system-jobs.md). |
| Conteggio stimato dello spazio dei nomi ID per un dato segmento | Per i conteggi dei profili stimati, l’API di anteprima ora riporta:<ul><li>Numero totale di profili stimati in un segmento per un dato spazio dei nomi.</li><li>Numero totale di profili stimati nello schema di unione profili per un dato spazio dei nomi.</li></ul>Per ulteriori informazioni, consulta [guida dell’endpoint API per l’anteprima del profilo](../../profile/api/preview-sample-status.md). |

Per ulteriori informazioni su Real-Time Customer Profile, inclusi tutorial e best practice per l’utilizzo di [!DNL Profile] , per iniziare leggi il [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti al connettore di origine Adobe Audience Manager | Ora puoi filtrare e selezionare singoli segmenti di prime parti dall’Audience Manager per acquisirli in Platform, nonché filtrare le caratteristiche di prime parti. Guarda il tutorial su [creazione di un connettore di origine di Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) per ulteriori informazioni. |
| [!DNL Google BigQuery] miglioramenti al connettore di origine | È ora possibile acquisire file di dimensioni superiori a 10 GB in un’unica esecuzione del flusso utilizzando [!DNL BigQuery] connettore di origine. Consulta la [[!DNL BigQuery] panoramica del connettore di origine](../../sources/connectors/databases/bigquery.md) per ulteriori informazioni. |
| Supporto per tipi di dati complessi per gli archivi cloud | Ora è possibile acquisire tipi di dati complessi, ad esempio array in file JSON, quando si utilizza un connettore di origine dell’archiviazione cloud. Consulta i tutorial sulla creazione di un flusso di dati di archiviazione cloud [nell’interfaccia utente](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) o [utilizzando [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md) per ulteriori informazioni. |
| Supporto per l&#39;autenticazione basata su chiave dell&#39;entità servizio per [!DNL Microsoft Dynamics] sorgente | Ora puoi eseguire l’autenticazione al tuo [!DNL Dynamics] utilizzando una chiave dell&#39;entità servizio come alternativa all&#39;autenticazione basata su password. Consulta la [[!DNL Dynamics] panoramica del connettore di origine](../../sources/connectors/crm/ms-dynamics.md) per ulteriori informazioni. |
| Supporto dell’interfaccia utente per i separatori personalizzati nelle origini di archiviazione cloud | È ora possibile impostare un delimitatore di colonna personalizzato, ad esempio una virgola (`,`), scheda (`\t`) o una pipe (`|`), per raccogliere i file delimitati nell’interfaccia utente. Guarda il tutorial su [creazione di un flusso di dati con un connettore di origine dell’archiviazione cloud](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) per ulteriori informazioni |

Per ulteriori informazioni sulle origini, consulta [panoramica sulle origini](../../sources/home.md).
