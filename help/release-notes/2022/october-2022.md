---
title: Note sulla versione di Adobe Experience Platform - Ottobre 2022
description: Note sulla versione di ottobre 2022 per Adobe Experience Platform.
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
source-git-commit: 260ba98f920c8006ab3ed7fb2519a8c1720916c8
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 34%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 26 ottobre 2022**

- [Chiavi gestite dal cliente](#cmk)
- [Raccolta dati](#data-collection)
- [Destinazioni](#destinations)
- [Experience Data Model](#xdm)
- [Servizio query](#query-service)

## Chiavi gestite dal cliente {#cmk}

Tutti i dati memorizzati su Adobe Experience Platform vengono crittografati a riposo utilizzando chiavi a livello di sistema. Se utilizzi un’applicazione basata su Platform, ora puoi scegliere di utilizzare le tue chiavi di crittografia, garantendo un maggiore controllo sulla sicurezza dei dati.

Consulta la panoramica su [chiavi gestite dal cliente](../../landing/governance-privacy-security/customer-managed-keys/overview.md) per i dettagli sulla funzione.

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Gestione dei dati sensibili per gli stream di dati | I flussi di dati ora sfruttano diverse tecnologie Platform per gestire in modo appropriato i dati sensibili in base a normative quali l’Health Insurance Portability and Accountability Act (HIPAA). Consulta la sezione su [gestione dei dati sensibili nei flussi di dati](../../datastreams/overview.md#sensitive) per ulteriori informazioni. |
| [!DNL Splunk] estensione per l’inoltro di eventi | Ora puoi inviare dati a [!DNL Splunk] utilizzando un [inoltro eventi](../../tags/ui/event-forwarding/overview.md) estensione. Consulta la [[!DNL Splunk] panoramica dell’estensione](../../tags/extensions/server/splunk/overview.md) per ulteriori informazioni. |
| [!DNL Zendesk] estensione per l’inoltro di eventi | Ora puoi inviare dati a [!DNL Zendesk] utilizzando un [inoltro eventi](../../tags/ui/event-forwarding/overview.md) estensione. Consulta la [[!DNL Zendesk] panoramica dell’estensione](../../tags/extensions/server/zendesk/overview.md) per ulteriori informazioni. |

{style="table-layout:auto"}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Esportazioni di set di dati (Beta) | Il [Funzionalità Beta per esportazioni set di dati](/help/destinations/ui/export-datasets.md) consente di esportare i dati di prima generazione (come definito nella [Descrizione del prodotto Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)) da Adobe Experience Platform ai sistemi dei clienti esterni, tramite l&#39;interfaccia utente delle destinazioni. Questo consente di ottenere dati da Experienci Platform con un flusso di lavoro senza codice/a basso codice per sei destinazioni di archiviazione cloud (elencate nella tabella seguente) per casi di utilizzo di analisi e conformità. |
| Funzionalità di esportazione file migliorate (Beta) | È ora possibile beneficiare di funzionalità di personalizzazione avanzate durante l’esportazione di file da Experienci Platform: <br><ul><li>Nuove [opzioni di denominazione file](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).</li><li>Possibilità di impostare intestazioni di file personalizzate nei file esportati tramite il [passaggio di mappatura migliorato](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Possibilità di personalizzare la formattazione dei file di dati CSV esportati](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> <br> Questa funzionalità è supportata dalle sei nuove schede di archiviazione cloud beta elencate nella tabella seguente. |

{style="table-layout:auto"}

**Destinazioni nuove o aggiornate** {#new-or-updated-destinations}

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line è una piattaforma di comunicazione popolare che collega persone, servizi e informazioni ed è cresciuta da un’app di chat a un hub per l’intrattenimento, il social e le attività quotidiane. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365 è una piattaforma di applicazioni aziendali basata su cloud che combina la pianificazione delle risorse aziendali (ERP) e la gestione delle relazioni con i clienti (CRM) insieme alle applicazioni di produttività e agli strumenti di intelligenza artificiale, per offrire operazioni end-to-end più fluide e controllate, un migliore potenziale di crescita e costi ridotti. |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | Il [!DNL (Beta) Adobe Commerce] il connettore di destinazione consente di selezionare uno o più segmenti Real-Time CDP da attivare nel [!DNL Adobe Commerce] per offrire agli acquirenti un&#39;esperienza dinamica e personalizzata. Entro [!DNL Adobe Commerce], puoi quindi selezionare i segmenti Real-Time CDP per personalizzare offerte univoche nel carrello, ad esempio &quot;acquista 2 ottieni 1 gratis&quot;. Puoi anche visualizzare hero banner e modificare il prezzo dei prodotti attraverso offerte promozionali, tutte personalizzate per i segmenti Adobe Real-Time CDP. |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Crea una connessione in uscita a [!DNL Azure Data Lake Storage Gen2] per esportare periodicamente file di dati da Adobe Experience Platform al tuo spazio di archiviazione. Questa nuova destinazione beta fornisce funzionalità avanzate di esportazione dei file e supporta le esportazioni dei set di dati. |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] è un’interfaccia di archiviazione [!DNL Azure Blob] fornita da Adobe Experience Platform che consente di accedere a una struttura di archiviazione dei file sicura e basata su cloud per esportare i file da Platform. Questa nuova destinazione beta fornisce funzionalità avanzate di esportazione dei file e supporta le esportazioni dei set di dati. |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Crea una connessione in uscita a [!DNL Google Cloud Storage] per esportare periodicamente file di dati da Adobe Experience Platform ai tuoi bucket. Questa nuova destinazione beta fornisce funzionalità avanzate di esportazione dei file e supporta le esportazioni dei set di dati. |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | I partecipanti beta ne visualizzano due [!DNL Amazon S3] schede di destinazione affiancate nel catalogo delle destinazioni. La nuova destinazione beta fornisce funzionalità avanzate di esportazione dei file e supporta le esportazioni dei set di dati. |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | I partecipanti beta ne visualizzano due [!DNL Azure Blob] schede di destinazione affiancate nel catalogo delle destinazioni. La nuova destinazione beta fornisce funzionalità avanzate di esportazione dei file e supporta le esportazioni dei set di dati. |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | I partecipanti beta ne visualizzano due [!DNL SFTP] schede di destinazione affiancate nel catalogo delle destinazioni. La nuova destinazione beta fornisce funzionalità avanzate di esportazione dei file e supporta le esportazioni dei set di dati. |

{style="table-layout:auto"}

**Documentazione nuova o aggiornata**

| Documentazione | Descrizione |
| ----------- | ----------- |
| [Guardrail delle destinazioni](../../destinations/guardrails.md) | Questa pagina fornisce i limiti predefiniti di utilizzo e tasso relativi al comportamento di attivazione. |

Per informazioni più generali sulle destinazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli della sessione]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | È stato aggiornato il `authorized` da tipo booleano a stringa. `season` e `episode` sono stati modificati da interi a stringhe. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli della pubblicità]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` è stato rinominato in `friendlyName`, e `ID` è stato rinominato in `name`. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli dell’errore]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` è stato rinominato come `name`. |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta la [Panoramica sul sistema XDM](../../xdm/home.md).

## Servizio query {#query-service}

Il Servizio query consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform.[!DNL Data Lake] Puoi unire qualsiasi set di dati da [!DNL Data Lake] e acquisisci i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o per l’acquisizione in Real-time Customer Profile.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Monitorare le query tramite l’interfaccia utente di Platform | Servizio query [!UICONTROL Query pianificate] fornisce una migliore visibilità dello stato di tutti i processi di query tramite l’interfaccia utente. Ora puoi trovare informazioni importanti sullo stato delle esecuzioni della query, inclusi messaggi di errore e codici in caso di esito negativo, da [!UICONTROL Query pianificate] scheda. Puoi anche abbonarti agli avvisi tramite l’interfaccia utente per ciascuna di queste query in base al loro stato. Consulta la [Monitorare il documento delle query](../../query-service/ui/monitor-queries.md) per ulteriori informazioni su questa funzione. |
| Query del modello dati per informazioni di reporting accelerate | Come parte dello SKU di Data Distiller, lo store con query accelerata consente di ridurre il tempo e la potenza di elaborazione necessari per ottenere informazioni critiche dai dati. Con l’archivio con query accelerata puoi creare un modello di dati personalizzato e/o estendere modelli di dati Adobe Real-time Customer Data Platform esistenti per migliorare le informazioni sul reporting e le relative visualizzazioni. Consulta la [documento query accelerated store reporting insights](../../query-service/data-distiller/query-accelerated-store/reporting-insights-data-model.md) per ulteriori informazioni su questa funzione. |

{style="table-layout:auto"}

Per ulteriori informazioni sul Servizio query, consulta la [Panoramica sul servizio query](../../query-service/home.md).
Nuove funzioni di Adobe Experience Platform:

