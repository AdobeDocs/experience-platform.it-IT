---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica sui connettori sorgente della piattaforma Adobe Experience
topic: overview
translation-type: tm+mt
source-git-commit: 291d669cc0f5b009b23dc2771688ee54b53d08db

---


# Panoramica sui connettori sorgente

Adobe Experience Platform consente di acquisire dati da origini esterne, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi della piattaforma. È possibile acquisire dati da origini diverse come applicazioni Adobe, archiviazione basata su cloud, database e molti altri.

Experience Platform fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di configurare con facilità le connessioni di origine a vari provider di dati. Queste connessioni di origine consentono di autenticare i sistemi di terze parti, impostare i tempi di caricamento e gestire il throughput di assimilazione dei dati.

Con Experience Platform, puoi centralizzare i dati raccolti da fonti diverse e utilizzare le informazioni acquisite per fare di più.

## Tipi di fonti

Le origini in Experience Platform sono raggruppate nelle seguenti categorie:

### Applicazioni Adobe

Experience Platform consente di acquisire dati da altre applicazioni Adobe, tra cui Adobe Analytics, Adobe Audience Manager e Experience Platform Launch. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [Panoramica del connettore Adobe Audience Manager](./ui/adobe-applications/audience-manager.md)
- [Creare un connettore sorgente Adobe Audience Manager nell’interfaccia utente](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/aam-ui-tutorial.md)
- [Panoramica del connettore dati di Adobe Analytics](./ui/adobe-applications/analytics.md)
- [Creare un connettore sorgente Adobe Analytics nell’interfaccia utente](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/adobe-analytics-ui-tutorial.md)

### Archiviazione cloud

Le origini di archiviazione cloud possono portare i tuoi dati in Platform senza bisogno di scaricare, formattare o caricare. Ogni fase del processo è integrata nel flusso di lavoro Origini tramite l&#39;interfaccia utente. Il supporto per i provider di archiviazione cloud include Amazon S3, Azure Blob, server FTP e server SFTP. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [Creare un connettore di origine Azure Blob o Amazon S3 nell&#39;interfaccia utente](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/amazon-s3-ui-tutorial.md)
- [Creare un connettore di origine Azure Data Lake Storage Gen2 nell&#39;interfaccia utente](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/adls-gen2-ui-tutorial.md)
- [Creare un connettore sorgente FTP o SFTP nell’interfaccia utente](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/ftp-sftp-ui-tutorial.md)
- [Creare un connettore di origine di archiviazione Google Cloud nell&#39;interfaccia utente](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/google-cloud-storage-ui-tutorial.md)

### Gestione delle relazioni con i clienti (CRM)

I sistemi CRM forniscono dati che possono aiutare a creare relazioni con i clienti, creando a loro volta fidelizzazione e promuovendo la fidelizzazione dei clienti. Experience Platform supporta l&#39;acquisizione di dati CRM da Microsoft Dynamics 365 e Salesforce. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [Creare un connettore sorgente Microsoft Dynamics 365 o Salesforce nell&#39;interfaccia utente](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/crm/dynamics-salesforce-ui-tutorial.md)
- [Creare un connettore di origine PayPal nell&#39;interfaccia utente](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/crm/paypal-tutorial.md)

### Successo cliente (CS)

Experience Platform supporta l’acquisizione di dati da un’applicazione di successo cliente di terze parti. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [Creare un connettore sorgente Salesforce Service Cloud nell’interfaccia utente](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/customer-success/salesforce-service-cloud-tutorial.md)
- [Creare un connettore di origine ServiceNow nell&#39;interfaccia utente](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/customer-success/servicenow-ui-tutorial.md)

### Database

Experience Platform supporta l’acquisizione di dati da un database di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consultate i seguenti documenti correlati:

- [Creare un connettore sorgente AWS Redshift nell&#39;interfaccia utente](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/amazon-redshift-ui-tutorial.md)
- [Creare un connettore di origine Azure Synapse Analytics nell&#39;interfaccia utente](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/azure-synapse-analytics-ui-tutorial.md)
- [Creare un connettore di origine Google BigQuery nell&#39;interfaccia utente](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/google-big-query-ui-tutorial.md)
- [Creare un connettore sorgente MariaDB nell&#39;interfaccia utente](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/database-nosql/mariadb-api-tutorial.md)
- [Creare un connettore di origine Microsoft SQL Server nell&#39;interfaccia utente](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/sql-server-ui-tutorial.md)
- [Creare un connettore sorgente MySQL nell’interfaccia utente](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/mysql-ui-tutorial.md)
- [Creare un connettore di origine PostgreSQL nell&#39;interfaccia utente](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/postgresql-tutorial.md)

### Marketing Automation

Experience Platform supporta l’acquisizione di dati da un sistema di automazione marketing di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consultate i seguenti documenti correlati:

- [Creare un connettore sorgente HubSpot nell’interfaccia utente](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/marketing-automation/hubspot-tutorial.md)

## Esercitazioni API

È possibile creare connettori di origine tramite l&#39;API del servizio di flusso. Per ulteriori informazioni, consulta il documento [di esercitazione sulle API](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/sources-api-tutorial.md)di origine.

## Controllo degli accessi per le origini nell&#39;assimilazione dei dati

Le autorizzazioni per le origini nell&#39;assimilazione dei dati possono essere gestite all&#39;interno di Adobe Admin Console. Potete accedere alle autorizzazioni tramite la scheda *Autorizzazioni* in un particolare profilo di prodotto. Dal pannello **Modifica autorizzazioni** , potete accedere alle autorizzazioni relative alle origini tramite la voce del menu di inserimento dei *dati* . L&#39;autorizzazione **Visualizza origini** consente l&#39;accesso in sola lettura alle origini disponibili nella scheda *Catalogo* e alle origini autenticate nella scheda *Sfoglia* , mentre l&#39;autorizzazione **Gestisci origini** consente l&#39;accesso completo alle origini di lettura, creazione, modifica e disattivazione.

La tabella seguente illustra il comportamento dell’interfaccia utente in base alle diverse combinazioni di queste autorizzazioni:

| Livello di autorizzazione | Descrizione |
| ---- | ----|
| **Visualizza origini** su | Concedere l&#39;accesso in sola lettura alle origini in ciascun tipo di origine nella scheda *Catalogo* , nonché alle schede *Sfoglia*, *Account* e *DataFlow* . |
| **Gestisci origini** su | Oltre alle funzioni incluse in **Visualizza origini**, concede l&#39;accesso all&#39;opzione Origine ** Connect in *Catalogo* e all&#39;opzione *Seleziona dati* in *Sfoglia*. **Manage Sources** (Gestisci origini) consente inoltre di abilitare o disabilitare *DataFlows* e di modificarne le pianificazioni. |
| **Visualizza origini** disattivate e **gestisci origini** disattivate | Revoca tutti gli accessi alle origini. |

Per ulteriori informazioni sulle autorizzazioni disponibili concesse tramite Admin Console, comprese quelle quattro origini, vedi la panoramica [del controllo](../access-control/home.md)degli accessi.
