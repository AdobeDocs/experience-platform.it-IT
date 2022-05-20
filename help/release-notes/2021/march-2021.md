---
title: Note sulla versione di Adobe Experience Platform - Marzo 2021
description: Note sulla versione di marzo 2021 per Adobe Experience Platform.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
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
| Funzione  di `add_to_array` | Funzionalità aggiornata per supportare gli array come parametro. |
| Funzione  di `to_array` | Funzionalità aggiornata per supportare gli oggetti come parametro. |

Per ulteriori informazioni, consulta la sezione [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## Servizio di segmentazione {#segmentation}

Il servizio di segmentazione di Adobe Experience Platform fornisce un’interfaccia utente e un’API RESTful che consente di creare segmenti e generare tipi di pubblico dal proprio [!DNL Real-time Customer Profile] dati. Questi segmenti sono configurati e mantenuti a livello centrale su [!DNL Platform], rendendoli facilmente accessibili da qualsiasi applicazione di Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all’interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| (Beta) Segmentazione dei bordi | La segmentazione dei bordi valuta i segmenti in tempo reale, che consentono casi d’uso per la stessa pagina e per la personalizzazione della pagina successiva. Ulteriori informazioni sulla segmentazione dei bordi sono disponibili nella sezione [Panoramica dell’interfaccia utente di segmentazione](../../segmentation/ui/overview.md). |
| (Beta) Segmentazione incrementale | Aumenta la freschezza delle definizioni di segmenti esistenti valutate nella segmentazione batch fino a un’ora. |

Per ulteriori informazioni su [!DNL Segmentation Service], vedi [Panoramica sulla segmentazione](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

| Funzione | Descrizione |
| ------- | ----------- |
| Sorgenti beta che si spostano in GA | Le seguenti origini sono state promosse dalla versione beta a GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| Supporto API per l’acquisizione di file compressi | È ora possibile visualizzare in anteprima e acquisire file JSON compressi o delimitati utilizzando origini di archiviazione cloud. Per ulteriori informazioni, consulta l’esercitazione su [raccolta di dati di archiviazione cloud tramite API](../../sources/tutorials/api/collect/cloud-storage.md). |
| Supporto dell’interfaccia utente per il caricamento ricorsivo dei file | È ora possibile acquisire in modo ricorsivo intere cartelle quando si utilizza un&#39;origine di archiviazione cloud. Quando si acquisisce un&#39;intera cartella, è necessario assicurarsi che il suo contenuto condivida lo stesso schema. Per ulteriori informazioni, consulta l’esercitazione su [configurazione di un flusso di dati per i connettori di archiviazione cloud nell’interfaccia utente](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
