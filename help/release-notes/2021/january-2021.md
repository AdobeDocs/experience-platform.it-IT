---
title: Note sulla versione di Adobe Experience Platform
description: ' note sulla versione del Experience Platform 27 gennaio 2021'
doc-type: release notes
last-update: January 27, 2021
author: ens60013
translation-type: tm+mt
source-git-commit: 18712835b2408b24cd2735b19c94bf1b1fe50df1
workflow-type: tm+mt
source-wordcount: '712'
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

[!DNL Data Prep] consente agli sviluppatori di dati di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Funzioni di espressione regolari | [!DNL Data Prep] Mapper ora supporta la corrispondenza e l&#39;estrazione di parte del campo di input in base alle espressioni regolari. |

Per ulteriori informazioni, vedere la [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni preconfigurate con piattaforme di destinazione che consentono l&#39;attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing multicanale, campagne e-mail, pubblicità mirata e molti altri casi di utilizzo.

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] è la soluzione di archiviazione oggetti di Microsoft per il cloud. |

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Corrispondenza ID avanzata | Miglioramenti alle funzionalità di corrispondenza tra pubblico in [!DNL Facebook Custom Audiences] e [!DNL Google Customer Match], mediante l&#39;aggiunta del supporto per corrispondenza di identità aggiuntiva, ad esempio ID esterni, numeri di telefono e ID dispositivo mobile. Per ulteriori informazioni, consulta la seguente documentazione: <ul><li>[Destinazione Facebook](../../destinations/catalog/social/facebook.md)</li><li>[Destinazione di corrispondenza cliente Google](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[Attivare profili e segmenti su una destinazione](../../destinations/ui/activate-destinations.md)</li></ul> |

Per saperne di più, visita la [panoramica delle destinazioni](../../destinations/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform consente di creare esperienze coordinate, coerenti e pertinenti per i clienti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con il profilo cliente in tempo reale, puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati da più canali, inclusi dati online, offline, CRM e di terze parti. [!DNL Profile] consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Elimina set di dati dall&#39;archivio profili | Quando si elimina un set di dati dal  Experience Platform Data Lake, verrà eliminato automaticamente anche dallo store Profile. Non è più necessario utilizzare l&#39;endpoint API dei processi del sistema di profilo per effettuare una richiesta di eliminazione per eliminare il set di dati dallo store del profilo in modo esplicito. Per ulteriori informazioni, consultate la [guida per l&#39;endpoint API dei processi del sistema di profilo](../../profile/api/profile-system-jobs.md). |
| Conteggio stimato dello spazio dei nomi ID per un determinato segmento | Per i conteggi stimati dei profili, l&#39;API di anteprima ora segnala:<ul><li>Totale dei profili stimati in un segmento per un dato spazio nomi.</li><li>Totale dei profili stimati nello schema dell&#39;unione dei profili per un dato spazio nomi.</li></ul>Per ulteriori informazioni, fare riferimento alla [guida dell&#39;endpoint API di anteprima profilo](../../profile/api/preview-sample-status.md). |

Per ulteriori informazioni sul profilo cliente in tempo reale, comprese esercitazioni e best practice per l&#39;utilizzo dei dati [!DNL Profile], si prega di iniziare leggendo la [panoramica sul profilo cliente in tempo reale](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da origini esterne consentendo al contempo di strutturare, etichettare e migliorare tali dati tramite i servizi Piattaforma. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, software di terze parti e il sistema CRM in uso.

 Experience Platform fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti al connettore sorgente Adobe Audience Manager | Ora puoi filtrare e selezionare singoli segmenti di prime parti da  Audience Manager a caricamento in piattaforma, nonché filtrare le caratteristiche di prime parti. Per ulteriori informazioni, vedere l&#39;esercitazione su [creazione di un connettore di origine del Audience Manager ](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). |
| [!DNL Google BigQuery] miglioramenti al connettore di origine | È ora possibile acquisire file di dimensioni superiori a 10 GB in un&#39;esecuzione di flusso utilizzando il connettore sorgente [!DNL BigQuery]. Per ulteriori informazioni, vedere [[!DNL BigQuery] panoramica del connettore di origine](../../sources/connectors/databases/bigquery.md). |
| Supporto per tipi di dati complessi per gli storage cloud | Ora è possibile assimilare tipi di dati complessi, come array in file JSON, quando si utilizza un connettore origine di archiviazione cloud. Per ulteriori informazioni, vedere le esercitazioni sulla creazione di un flusso di dati di archiviazione cloud [nell&#39;interfaccia utente](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) o [tramite l&#39;API [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md). |
| Supporto per l&#39;autenticazione basata sulle chiavi dell&#39;entità del servizio per l&#39;origine [!DNL Microsoft Dynamics] | Ora puoi eseguire l&#39;autenticazione sul tuo account [!DNL Dynamics] utilizzando una chiave dell&#39;entità del servizio come alternativa all&#39;autenticazione basata su password. Per ulteriori informazioni, vedere [[!DNL Dynamics] panoramica del connettore di origine](../../sources/connectors/crm/ms-dynamics.md). |
| Supporto dell&#39;interfaccia utente per i separatori personalizzati nelle origini di archiviazione cloud | È ora possibile impostare un delimitatore di colonna personalizzato, ad esempio una virgola (`,`), una scheda (`\t`) o una pipe (`|`), per raccogliere i file delimitati nell&#39;interfaccia utente. Per ulteriori informazioni, vedere l&#39;esercitazione su [creazione di un flusso di dati con un connettore origine di archiviazione cloud](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) |

Per ulteriori informazioni sulle origini, vedere la [panoramica delle origini](../../sources/home.md).
