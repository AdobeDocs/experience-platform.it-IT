---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di Experience Platform 27 gennaio 2021
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: 02c22453470d55236d4235c479742997e8407ef3
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 6%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 27 gennaio 2021**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Funzioni con espressione regolare | [!DNL Data Prep] Mapper ora supporta la corrispondenza e l’estrazione di una parte del campo di input in base alle espressioni regolari. |

Per ulteriori informazioni, consulta la [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] è la soluzione di archiviazione oggetti di Microsoft per il cloud. |

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Corrispondenza ID avanzata | Miglioramenti alle funzionalità di percentuali di corrispondenza del pubblico in [!DNL Facebook Custom Audiences] e [!DNL Google Customer Match], aggiungendo supporto per una corrispondenza di identità aggiuntiva, ad esempio ID esterni, numeri di telefono e ID di dispositivi mobili. Per ulteriori informazioni, consulta la seguente documentazione: <ul><li>[Destinazione facebook](../../destinations/catalog/social/facebook.md)</li><li>[Destinazione Customer Match di Google](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

Per ulteriori informazioni, visita la [panoramica delle destinazioni](../../destinations/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di fornire ai clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con Profilo cliente in tempo reale puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, CRM e di terze parti. [!DNL Profile] consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account actionable con marca temporale per ogni interazione con il cliente.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Elimina set di dati dall’archivio profili | Quando elimini un set di dati da Experience Platform Data Lake, viene eliminato automaticamente anche dall’archivio profili. Non è più necessario utilizzare l’endpoint API dei processi del sistema di profili per effettuare una richiesta di eliminazione per eliminare esplicitamente il set di dati dall’archivio profili. Per ulteriori informazioni, consulta la [guida all&#39;endpoint API dei processi di sistema del profilo](../../profile/api/profile-system-jobs.md). |
| Numero stimato dello spazio dei nomi ID per un dato segmento | Per i conteggi stimati dei profili, l&#39;API di anteprima ora riporta:<ul><li>Numero totale di profili stimati in un segmento per un determinato namespace.</li><li>Numero totale di profili stimati nello schema dell’Unione profili per un determinato spazio dei nomi.</li></ul>Per ulteriori informazioni, consulta la [guida all’endpoint API di anteprima del profilo](../../profile/api/preview-sample-status.md). |

Per ulteriori informazioni sul Profilo del cliente in tempo reale, comprese esercitazioni e best practice per l’utilizzo dei dati [!DNL Profile], si prega di iniziare leggendo la [Panoramica del profilo del cliente in tempo reale](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti al connettore sorgente Adobe Audience Manager | Ora puoi filtrare e selezionare singoli segmenti di prime parti da Audience Manager a Acquisisci in Platform, nonché filtrare le caratteristiche di prime parti. Per ulteriori informazioni, consulta l’esercitazione su [creazione di un connettore di origine Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) . |
| [!DNL Google BigQuery] miglioramenti al connettore sorgente | È ora possibile acquisire file di dimensioni superiori a 10 GB in un’esecuzione di flusso utilizzando il connettore di origine [!DNL BigQuery]. Per ulteriori informazioni, consulta la [[!DNL BigQuery] panoramica del connettore di origine](../../sources/connectors/databases/bigquery.md) . |
| Supporto per tipi di dati complessi per gli archivi cloud | È ora possibile acquisire tipi di dati complessi, ad esempio array in file JSON, quando si utilizza un connettore di origine dell’archiviazione cloud. Per ulteriori informazioni, consulta le esercitazioni sulla creazione di un flusso di dati di archiviazione cloud [nell’interfaccia utente](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) o [utilizzando l’ [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md) . |
| Supporto per l&#39;autenticazione basata su chiave dell&#39;entità servizio per l&#39;origine [!DNL Microsoft Dynamics] | Ora puoi eseguire l’autenticazione nel tuo account [!DNL Dynamics] utilizzando una chiave dell’entità del servizio come alternativa all’autenticazione basata su password. Per ulteriori informazioni, consulta la [[!DNL Dynamics] panoramica del connettore di origine](../../sources/connectors/crm/ms-dynamics.md) . |
| Supporto dell’interfaccia utente per i separatori personalizzati nelle origini di archiviazione cloud | È ora possibile impostare un delimitatore di colonna personalizzato, ad esempio una virgola (`,`), una scheda (`\t`) o una barra verticale (`|`), per raccogliere i file delimitati nell’interfaccia utente. Per ulteriori informazioni, consulta l’esercitazione su [creazione di un flusso di dati con un connettore di origine dell’archiviazione cloud](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) . |

Per ulteriori informazioni sulle origini, consulta la [panoramica origini](../../sources/home.md).
