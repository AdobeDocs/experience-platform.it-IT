---
title: Note sulla versione di Adobe Experience Platform - Marzo 2021
description: Note sulla versione di Adobe Experience Platform di marzo 2021.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 38%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 31 marzo 2021**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

| Funzione | Descrizione |
| ------- | ----------- |
| Funzione `add_to_array` | È stata aggiornata la funzionalità per supportare gli array come parametro. |
| Funzione `to_array` | È stata aggiornata la funzionalità per supportare gli oggetti come parametro. |

Per ulteriori informazioni, vedere la [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## Servizio di segmentazione {#segmentation}

Il servizio di segmentazione di Adobe Experience Platform fornisce un&#39;interfaccia utente e un&#39;API RESTful che consentono di creare segmenti e generare tipi di pubblico dai dati di [!DNL Real-Time Customer Profile]. Questi segmenti vengono configurati e gestiti centralmente in [!DNL Platform], rendendoli facilmente accessibili da qualsiasi applicazione Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| (Beta) Segmentazione di Edge | La segmentazione di Edge valuta i segmenti in tempo reale, che consentono casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva. Ulteriori informazioni sulla segmentazione Edge sono disponibili nella [Panoramica dell&#39;interfaccia utente di segmentazione](../../segmentation/ui/overview.md). |
| (Beta) Segmentazione incrementale | Aumenta fino a un’ora l’aggiornamento delle definizioni dei segmenti esistenti valutate nella segmentazione batch. |

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio da applicazioni Adobe, dall’archiviazione basata su cloud, da software di terze parti e dal sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

| Funzione | Descrizione |
| ------- | ----------- |
| Sorgenti Beta che passano a GA | Le seguenti sorgenti sono state promosse dalla versione beta a GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| Supporto API per l’acquisizione di file compressi | Ora puoi visualizzare in anteprima e acquisire file JSON compressi o delimitati utilizzando le origini di archiviazione cloud. Per ulteriori informazioni, consulta l&#39;esercitazione su [raccolta di dati di archiviazione cloud tramite API](../../sources/tutorials/api/collect/cloud-storage.md). |
| Supporto dell’interfaccia utente per il caricamento di file ricorsivi | È ora possibile acquisire intere cartelle in modo ricorsivo quando si utilizza un’origine di archiviazione cloud. Quando acquisisci un’intera cartella, assicurati che il relativo contenuto condivida lo stesso schema. Per ulteriori informazioni, consulta l&#39;esercitazione su [configurazione di un flusso di dati per i connettori di archiviazione cloud nell&#39;interfaccia utente](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Per ulteriori informazioni sulle origini, vedere [panoramica delle origini](../../sources/home.md).
