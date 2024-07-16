---
title: Note sulla versione di Adobe Experience Platform - Gennaio 2021
description: Note sulla versione di Adobe Experience Platform di gennaio 2021.
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 27%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 27 gennaio 2021**

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
| Funzioni espressione regolare | [!DNL Data Prep] Mapper ora supporta la corrispondenza e l&#39;estrazione di parte del campo di input in base alle espressioni regolari. |

Per ulteriori informazioni, vedere la [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] è la soluzione di archiviazione oggetti di Microsoft per il cloud. |

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Corrispondenza ID avanzata | Sono state migliorate le funzionalità di frequenza di corrispondenza del pubblico in [!DNL Facebook Custom Audiences] e [!DNL Google Customer Match], aggiungendo il supporto per la corrispondenza di identità aggiuntiva, ad esempio ID esterni, numeri di telefono e ID di dispositivi mobili. Per ulteriori informazioni, consulta la seguente documentazione: <ul><li>[Destinazione Facebook](../../destinations/catalog/social/facebook.md)</li><li>[Destinazione Customer Match Google](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[Attiva i dati del pubblico nelle destinazioni di esportazione dei segmenti di streaming](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

Per ulteriori informazioni, visita la [panoramica delle destinazioni](../../destinations/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e pertinenti per la tua clientela, indipendentemente da dove e quando interagisce con il tuo marchio. Con il Profilo cliente in tempo reale puoi avere una visione completa di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. [!DNL Profile] consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Elimina set di dati dall’archivio profili | Quando elimini un set di dati dal Data Lake di Experience Platform, questo viene eliminato automaticamente anche dall’archivio Profili. Non è più necessario utilizzare l’endpoint API dei processi del sistema di profili per effettuare una richiesta di eliminazione al fine di eliminare esplicitamente il set di dati dall’archivio profili. Per ulteriori informazioni, consulta la [guida dell&#39;endpoint API dei processi di sistema ](../../profile/api/profile-system-jobs.md). |
| Conteggio stimato dello spazio dei nomi ID per un dato segmento | Per i conteggi dei profili stimati, l’API di anteprima ora riporta:<ul><li>Numero totale di profili stimati in un segmento per un dato spazio dei nomi.</li><li>Numero totale di profili stimati nello schema di unione profili per un dato spazio dei nomi.</li></ul>Per ulteriori informazioni, consulta la [guida dell&#39;endpoint API di anteprima del profilo](../../profile/api/preview-sample-status.md). |

Per ulteriori informazioni su Real-Time Customer Profile, inclusi tutorial e best practice per l&#39;utilizzo dei dati di [!DNL Profile], leggere la [Panoramica sul profilo cliente in tempo reale](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti al connettore di origine Adobe Audience Manager | Ora puoi filtrare e selezionare singoli segmenti di prime parti dall’Audience Manager per acquisirli in Platform, nonché filtrare le caratteristiche di prime parti. Per ulteriori informazioni, vedere l&#39;esercitazione sulla [creazione di un connettore di origine Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). |
| Miglioramenti al connettore di origine [!DNL Google BigQuery] | È ora possibile acquisire file di dimensioni superiori a 10 GB in un&#39;unica esecuzione del flusso utilizzando il connettore di origine [!DNL BigQuery]. Per ulteriori informazioni, vedere [[!DNL BigQuery] panoramica del connettore di origine](../../sources/connectors/databases/bigquery.md). |
| Supporto per tipi di dati complessi per gli archivi cloud | Ora è possibile acquisire tipi di dati complessi, ad esempio array in file JSON, quando si utilizza un connettore di origine dell’archiviazione cloud. Per ulteriori informazioni, consulta i tutorial sulla creazione di un flusso di dati nell&#39;archiviazione cloud [ nell&#39;interfaccia utente](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) o [utilizzando l&#39; [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md). |
| Supporto per l&#39;autenticazione basata su chiave dell&#39;entità servizio per l&#39;origine [!DNL Microsoft Dynamics] | È ora possibile eseguire l&#39;autenticazione nell&#39;account [!DNL Dynamics] utilizzando una chiave dell&#39;entità servizio in alternativa all&#39;autenticazione basata su password. Per ulteriori informazioni, vedere [[!DNL Dynamics] panoramica del connettore di origine](../../sources/connectors/crm/ms-dynamics.md). |
| Supporto dell’interfaccia utente per i separatori personalizzati nelle origini di archiviazione cloud | È ora possibile impostare un delimitatore di colonna personalizzato, ad esempio una virgola (`,`), una tabulazione (`\t`) o una barra verticale (`|`), per raccogliere i file delimitati nell&#39;interfaccia utente. Per ulteriori informazioni, consulta il tutorial su [creazione di un flusso di dati con un connettore di origine dell&#39;archiviazione cloud](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) |

Per ulteriori informazioni sulle origini, vedere [panoramica delle origini](../../sources/home.md).
