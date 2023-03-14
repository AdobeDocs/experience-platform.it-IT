---
title: Note sulla versione di Adobe Experience Platform, marzo 2021
description: Note sulla versione di marzo 2021 per Adobe Experience Platform.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 6%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 31 marzo 2021**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

| Funzione | Descrizione |
| ------- | ----------- |
| Funzione  di `add_to_array` | È stata aggiornata la funzionalità per supportare gli array come parametro. |
| Funzione  di `to_array` | È stata aggiornata la funzionalità per supportare gli oggetti come parametro. |

Per ulteriori informazioni, vedere [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## Servizio di segmentazione {#segmentation}

Il servizio di segmentazione di Adobe Experience Platform fornisce un’interfaccia utente e un’API RESTful che consente di creare segmenti e generare tipi di pubblico dal tuo [!DNL Real-Time Customer Profile] dati. Questi segmenti sono configurati e gestiti centralmente su [!DNL Platform], rendendoli facilmente accessibili da qualsiasi applicazione Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo commerciabile di persone all’interno della tua base clienti. I segmenti possono essere basati su dati record (ad esempio informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Segmentazione Edge (Beta) | La segmentazione Edge valuta i segmenti in tempo reale, che consentono casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva. Ulteriori informazioni sulla segmentazione Edge sono disponibili nella sezione [Panoramica sulla segmentazione dell’interfaccia utente](../../segmentation/ui/overview.md). |
| (Beta) Segmentazione incrementale | Aumenta fino a un’ora l’aggiornamento delle definizioni dei segmenti esistenti valutate nella segmentazione batch. |

Per ulteriori informazioni su [!DNL Segmentation Service], consultare il [Panoramica sulla segmentazione](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

| Funzione | Descrizione |
| ------- | ----------- |
| Sorgenti beta che passano a GA | Le seguenti sorgenti sono state promosse dalla versione beta a GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| Supporto API per l’acquisizione di file compressi | Ora puoi visualizzare in anteprima e acquisire file JSON compressi o delimitati utilizzando le origini di archiviazione cloud. Per ulteriori informazioni, consulta l’esercitazione su [raccolta di dati di archiviazione cloud tramite API](../../sources/tutorials/api/collect/cloud-storage.md). |
| Supporto dell’interfaccia utente per il caricamento di file ricorsivi | È ora possibile acquisire intere cartelle in modo ricorsivo quando si utilizza un’origine di archiviazione cloud. Quando acquisisci un’intera cartella, assicurati che il relativo contenuto condivida lo stesso schema. Per ulteriori informazioni, consulta l’esercitazione su [configurazione di un flusso di dati per i connettori di archiviazione cloud nell’interfaccia utente](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Per ulteriori informazioni sulle origini, consulta [panoramica sulle origini](../../sources/home.md).
