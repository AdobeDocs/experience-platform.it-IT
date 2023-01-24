---
title: Note sulla versione di Adobe Experience Platform - Gennaio 2023
description: Le note sulla versione di gennaio 2023 per Adobe Experience Platform.
source-git-commit: 01c220147312108649e036d93288823df5389235
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 9%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 25 gennaio 2023**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Origini](#sources)

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e consente di strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

| Funzione | Descrizione |
| --- | --- |
| Consenti accesso utente alle sottocartelle delle origini di archiviazione cloud | È ora possibile definire l’accesso a una sottocartella specifica dell’origine di archiviazione cloud durante la creazione di un nuovo account. Una volta creati, gli utenti potranno accedere solo ai dati della sottocartella consentita. Questa funzione è disponibile per le seguenti origini di archiviazione cloud: [Archiviazione BLOB di Azure](../../sources/connectors/cloud-storage/blob.md), [Google Cloud Storage](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)e [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Disponibilità beta [!DNL SugarCRM] | [!DNL SugarCRM] le origini sono ora disponibili in versione beta. Utilizza la [!DNL SugarCRM Accounts & Contacts] e [!DNL SugarCRM Events] origini per ottenere i dati dal [!DNL SugarCRM] conto all&#39;Experience Platform. Per ulteriori informazioni, consulta la sezione [[!DNL SugarCRM] panoramica](../../sources/connectors/crm/sugarcrm.md). |