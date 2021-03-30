---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di Experience Platform per il 31 marzo 2021.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
translation-type: tm+mt
source-git-commit: 8d4270d9168a570fcf92ba60d70dbc8e9af98136
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 9%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 31 marzo 2021**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Sources]](#sources)

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

I seguenti aggiornamenti alle sorgenti sono inclusi nella versione di Experience Platform di marzo 2021:

| Funzione | Descrizione |
| ------- | ----------- |
| Sorgenti beta che si spostano in GA | Le seguenti origini sono state promosse dalla versione beta a GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| Supporto API per l’acquisizione di file compressi | È ora possibile visualizzare in anteprima e acquisire file JSON compressi o delimitati utilizzando origini di archiviazione cloud. Per ulteriori informazioni, consulta l’esercitazione sulla [raccolta di dati di archiviazione cloud utilizzando le API](../../sources/tutorials/api/collect/cloud-storage.md). |
| Supporto dell’interfaccia utente per il caricamento ricorsivo dei file | È ora possibile acquisire in modo ricorsivo intere cartelle quando si utilizza un&#39;origine di archiviazione cloud. Quando si acquisisce un&#39;intera cartella, è necessario assicurarsi che il suo contenuto condivida lo stesso schema. Per ulteriori informazioni, consulta l’esercitazione su [configurazione di un flusso di dati per i connettori di archiviazione cloud nell’interfaccia utente](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Per ulteriori informazioni sulle origini, consulta la [panoramica origini](../../sources/home.md).
