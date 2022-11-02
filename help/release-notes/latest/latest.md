---
title: Note sulla versione di Adobe Experience Platform
description: Note aggiornate sulla versione di Adobe Experience Platform.
source-git-commit: d046c17a7b376f5c2e2f25c38fac0916ed2dba73
workflow-type: tm+mt
source-wordcount: '1394'
ht-degree: 5%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 26 ottobre 2022**

Nuove funzioni in Adobe Experience Platform:

- [Chiavi gestite dal cliente](#cmk)

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Raccolta dati](#data-collection)
- [Destinazioni](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Servizio query](#query-service)
- [Origini](#sources)

## Chiavi gestite dal cliente {#cmk}

Tutti i dati archiviati in Adobe Experience Platform vengono crittografati a riposo utilizzando le chiavi a livello di sistema. Se utilizzi un’applicazione basata su Platform, ora puoi scegliere di utilizzare le tue chiavi di crittografia, offrendoti un maggiore controllo sulla sicurezza dei dati.

Vedi la panoramica su [chiavi gestite dal cliente](../../landing/governance-privacy-security/customer-managed-keys.md) per informazioni dettagliate sulla funzione.

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che ti consentono di raccogliere i dati sull’esperienza del cliente lato client e inviarli ad Adobe Experience Platform Edge Network dove possono essere arricchiti, trasformati e distribuiti su destinazioni Adobi o non Adobi.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Gestione sensibile dei dati per i datastreams | I Datastreams ora sfruttano diverse tecnologie Platform per gestire in modo appropriato i dati sensibili come imposto da regolamenti come l&#39;Health Insurance Portability and Accountability Act (HIPAA). Vedi la sezione su [gestione dei dati sensibili nei flussi di dati](../../edge/datastreams/overview.md#sensitive) per ulteriori informazioni. |
| [!DNL Splunk] estensione per l&#39;inoltro eventi | Ora puoi inviare dati a [!DNL Splunk] utilizzando [inoltro eventi](../../tags/ui/event-forwarding/overview.md) estensione. Consulta la sezione [[!DNL Splunk] panoramica dell&#39;estensione](../../tags/extensions/web/splunk/overview.md) per ulteriori informazioni. |
| [!DNL Zendesk] estensione per l&#39;inoltro eventi | Ora puoi inviare dati a [!DNL Zendesk] utilizzando [inoltro eventi](../../tags/ui/event-forwarding/overview.md) estensione. Consulta la sezione [[!DNL Zendesk] panoramica dell&#39;estensione](../../tags/extensions/web/zendesk/overview.md) per ulteriori informazioni. |

{style=&quot;table-layout:auto&quot;}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Esportazioni di set di dati (Beta) | La [Il set di dati esporta la funzionalità Beta](/help/destinations/ui/export-datasets.md) consente di esportare dati di prima generazione (come definito nella [Descrizione del prodotto Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)) da Adobe Experience Platform ai sistemi dei clienti esterni tramite l’interfaccia utente delle destinazioni. Questo ti consente di ottenere i dati da un Experience Platform con un flusso di lavoro no-code/low-code a sei destinazioni di archiviazione cloud (elencate nella tabella seguente) per casi di utilizzo analitici e di conformità. |
| (Beta) Funzionalità di esportazione file migliorate | È ora possibile sfruttare le funzionalità avanzate di personalizzazione durante l’esportazione di file da un Experience Platform: <br><ul><li>Aggiuntivo [opzioni di denominazione file](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).</li><li>Possibilità di impostare intestazioni di file personalizzate nei file esportati tramite [passaggio di mappatura migliorato](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Possibilità di personalizzare la formattazione dei file di dati CSV esportati](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> <br> Questa funzionalità è supportata dalle sei nuove schede di archiviazione cloud beta elencate nella tabella seguente. |

{style=&quot;table-layout:auto&quot;}

**Destinazioni nuove o aggiornate**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line è una piattaforma di comunicazione popolare che collega persone, servizi e informazioni ed è cresciuta da un&#39;app di chat a un hub per l&#39;intrattenimento, social e attività quotidiane. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365 è una piattaforma di applicazioni aziendali basate su cloud che combina Enterprise Resource Planning (ERP) e Customer Relationship Management (CRM) insieme alle applicazioni di produttività e agli strumenti AI, per garantire operazioni più fluide e controllate end-to-end, un migliore potenziale di crescita e costi ridotti. |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | La [!DNL (Beta) Adobe Commerce] il connettore di destinazione consente di selezionare uno o più segmenti di Real-Time CDP da attivare nel [!DNL Adobe Commerce] per offrire un’esperienza personalizzata dinamica ai tuoi acquirenti. Within [!DNL Adobe Commerce], puoi quindi selezionare i segmenti Real-Time CDP per personalizzare offerte univoche nel carrello, ad esempio &quot;acquista 2 get 1 free&quot;. Puoi anche visualizzare banner eroi e modificare il prezzo del prodotto tramite offerte promozionali, tutte personalizzate per i segmenti Adobe Real-Time CDP. |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Creare una connessione in uscita diretta con [!DNL Azure Data Lake Storage Gen2] per esportare periodicamente i file di dati da Adobe Experience Platform nel percorso di archiviazione personale. Questa nuova destinazione beta fornisce funzionalità avanzate di esportazione dei file e supporta le esportazioni dei set di dati. |
| [[!DNL (Beta) Azure Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] è un [!DNL Azure Blob] l’interfaccia di archiviazione fornita da Adobe Experience Platform consente di accedere a una struttura di archiviazione file sicura basata su cloud per esportare i file fuori da Platform. Questa nuova destinazione beta fornisce funzionalità avanzate di esportazione dei file e supporta le esportazioni dei set di dati. |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Creare una connessione in uscita diretta con [!DNL Google Cloud Storage] per esportare periodicamente i file di dati da Adobe Experience Platform nei blocchi personali. Questa nuova destinazione beta fornisce funzionalità avanzate di esportazione dei file e supporta le esportazioni dei set di dati. |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Ora i partecipanti beta vedono due [!DNL Amazon S3] schede di destinazione affiancate nel catalogo delle destinazioni. La nuova destinazione beta fornisce funzionalità avanzate di esportazione dei file e supporta le esportazioni dei set di dati. |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Ora i partecipanti beta vedono due [!DNL Azure Blob] schede di destinazione affiancate nel catalogo delle destinazioni. La nuova destinazione beta fornisce funzionalità avanzate di esportazione dei file e supporta le esportazioni dei set di dati. |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Ora i partecipanti beta vedono due [!DNL SFTP] schede di destinazione affiancate nel catalogo delle destinazioni. La nuova destinazione beta fornisce funzionalità avanzate di esportazione dei file e supporta le esportazioni dei set di dati. |

{style=&quot;table-layout:auto&quot;}

**Documentazione nuova o aggiornata**

| Documentazione | Descrizione |
| ----------- | ----------- |
| [Guardaroba](../../destinations/guardrails.md) | Questa pagina fornisce limiti di utilizzo e di frequenza predefiniti per quanto riguarda il comportamento di attivazione. |

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Tipo di dati | [[!UICONTROL Informazioni sulla sessione]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | È stato aggiornato il `authorized` da un tipo booleano a una stringa. `season` e `episode` sono stati modificati da interi a stringhe. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli pubblicitari]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` è stato rinominato in `friendlyName`e `ID` è stato rinominato in `name`. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli degli errori]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` è stato rinominato come `name`. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni su XDM in Platform, consulta la sezione [Panoramica del sistema XDM](../../xdm/home.md).

## Servizio query {#query-service}

Query Service consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati dal [!DNL Data Lake] e acquisisci i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o per l’inserimento in Profilo cliente in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Monitorare le query tramite l’interfaccia utente di Platform | Servizio query [!UICONTROL Query pianificate] La scheda fornisce una migliore visibilità dello stato di tutti i processi di query tramite l’interfaccia utente. È ora possibile trovare informazioni importanti sullo stato delle esecuzioni della query, inclusi i messaggi di errore e i codici in caso di errore, da [!UICONTROL Query pianificate] scheda . Puoi anche abbonarti agli avvisi tramite l’interfaccia utente per tutte queste query in base al loro stato. Consulta la sezione [Documento Query di monitoraggio](../../query-service/monitor-queries.md) per ulteriori informazioni su questa funzione. |
| Modello di dati per informazioni di reporting accelerate per query | Come parte dello SKU di Data Distiller, lo store con accelerazione query ti consente di ridurre il tempo e la potenza di elaborazione necessari per ottenere informazioni critiche dai tuoi dati. Con l’archivio con accelerazione query è possibile creare un modello dati personalizzato e/o estenderlo ai modelli dati Adobe Real-time Customer Data Platform esistenti per migliorare le informazioni di reporting e le relative visualizzazioni. Consulta la sezione [documento approfondimenti reportistica di archivio accelerato di query](../../query-service/query-accelerated-store/reporting-insights-data-model.md) per ulteriori informazioni su questa funzione. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sui servizi di query, consulta la [Panoramica del servizio query](../../query-service/home.md).
Nuove funzioni in Adobe Experience Platform:

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- | 
| Disponibilità beta dell’origine Adobe Workfront | Utilizza la [Origine Adobe Workfront](../../sources/connectors/adobe-applications/workfront.md) per dare Experience Platform ai dati Workfront ed eseguire casi d&#39;uso, ad esempio la combinazione dei record di lavoro con dati di terze parti, l&#39;applicazione di analisi storiche e di serie temporali sui record di lavoro e l&#39;esecuzione di query sui dati di lavoro utilizzando SQL standard. Per ulteriori informazioni, consulta la guida su [creazione di una connessione sorgente Workfront nell’interfaccia utente](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |
| Disponibilità beta dell’origine Oracle Service Cloud | Utilizza l’origine Oracle Service Cloud per acquisire i dati dall’account Oracle Service Cloud all’Experience Platform. Per ulteriori informazioni, consulta la documentazione sul [Origine Oracle Service Cloud](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Per ulteriori informazioni sulle origini, consulta la sezione [panoramica di origini](../../sources/home.md).
