---
title: Note sulla versione di Adobe Experience Platform - Ottobre 2022
description: Note sulla versione di Adobe Experience Platform di ottobre 2022.
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
source-git-commit: 0970fd8fbea86115d92dc78cdba753da69cc2ee6
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 30%

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

Per informazioni dettagliate sulla funzione, consulta la panoramica sulle [chiavi gestite dal cliente](../../landing/governance-privacy-security/customer-managed-keys/overview.md).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Gestione dei dati sensibili per gli stream di dati | I flussi di dati ora sfruttano diverse tecnologie Platform per gestire in modo appropriato i dati sensibili in base a normative quali l’Health Insurance Portability and Accountability Act (HIPAA). Per ulteriori informazioni, consulta la sezione sulla gestione di [dati sensibili nei flussi di dati](../../datastreams/overview.md#sensitive). |
| Estensione [!DNL Splunk] per l&#39;inoltro degli eventi | È ora possibile inviare dati a [!DNL Splunk] utilizzando un&#39;estensione [inoltro eventi](../../tags/ui/event-forwarding/overview.md). Per ulteriori informazioni, vedere [[!DNL Splunk] panoramica dell&#39;estensione](../../tags/extensions/server/splunk/overview.md). |
| Estensione [!DNL Zendesk] per l&#39;inoltro degli eventi | È ora possibile inviare dati a [!DNL Zendesk] utilizzando un&#39;estensione [inoltro eventi](../../tags/ui/event-forwarding/overview.md). Per ulteriori informazioni, vedere [[!DNL Zendesk] panoramica dell&#39;estensione](../../tags/extensions/server/zendesk/overview.md). |

{style="table-layout:auto"}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Esportazioni di set di dati (Beta) | Il [Set di dati esporta la funzionalità Beta](/help/destinations/ui/export-datasets.md) consente di esportare i dati di prima generazione (come definito nella [descrizione del prodotto Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)) da Adobe Experience Platform ai sistemi dei clienti esterni tramite l&#39;interfaccia utente delle destinazioni. Questo consente di ottenere dati da Experience Platform con un flusso di lavoro senza codice/a basso codice per sei destinazioni di archiviazione cloud (elencate nella tabella seguente) per casi di utilizzo di analisi e conformità. |
| (Beta) Funzionalità avanzate di esportazione dei file | È ora possibile beneficiare della funzionalità di personalizzazione avanzata durante l&#39;esportazione di file dall&#39;Experience Platform: <br><ul><li>Nuove [opzioni di denominazione file](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).</li><li>Possibilità di impostare intestazioni di file personalizzate nei file esportati tramite il [passaggio di mappatura migliorato](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Possibilità di personalizzare la formattazione dei file CSV esportati](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> <br> Questa funzionalità è supportata dalle sei nuove schede di archiviazione cloud beta elencate nella tabella seguente. |

{style="table-layout:auto"}

**Destinazioni nuove o aggiornate** {#new-or-updated-destinations}

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line è una piattaforma di comunicazione popolare che collega persone, servizi e informazioni ed è cresciuta da un’app di chat a un hub per l’intrattenimento, il social e le attività quotidiane. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365 è una piattaforma di applicazioni aziendali basata su cloud che combina la pianificazione delle risorse aziendali (ERP) e la gestione delle relazioni con i clienti (CRM) insieme alle applicazioni di produttività e agli strumenti di intelligenza artificiale, per offrire operazioni end-to-end più fluide e controllate, un migliore potenziale di crescita e costi ridotti. |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | Il connettore di destinazione [!DNL (Beta) Adobe Commerce] consente di selezionare uno o più segmenti Real-Time CDP da attivare nel tuo account [!DNL Adobe Commerce] per fornire un&#39;esperienza dinamica personalizzata per gli acquirenti. All&#39;interno di [!DNL Adobe Commerce], puoi quindi selezionare i segmenti di Real-Time CDP per personalizzare offerte univoche nel carrello, ad esempio &#39;compra 2 ottieni 1 gratis,&#39;. Puoi anche visualizzare hero banner e modificare il prezzo dei prodotti attraverso offerte promozionali, tutte personalizzate per i segmenti Adobe Real-Time CDP. |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Crea una connessione in uscita a [!DNL Azure Data Lake Storage Gen2] per esportare periodicamente file di dati da Adobe Experience Platform al tuo spazio di archiviazione. Questa nuova destinazione beta fornisce funzionalità avanzate di esportazione dei file e supporta le esportazioni dei set di dati. |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] è un’interfaccia di archiviazione [!DNL Azure Blob] fornita da Adobe Experience Platform che consente di accedere a una struttura di archiviazione dei file sicura e basata su cloud per esportare i file da Platform. Questa nuova destinazione beta fornisce funzionalità avanzate di esportazione dei file e supporta le esportazioni dei set di dati. |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Crea una connessione in uscita a [!DNL Google Cloud Storage] per esportare periodicamente file di dati da Adobe Experience Platform ai tuoi bucket. Questa nuova destinazione beta fornisce funzionalità avanzate di esportazione dei file e supporta le esportazioni dei set di dati. |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | I partecipanti a Beta visualizzano ora due schede di destinazione [!DNL Amazon S3] affiancate nel catalogo delle destinazioni. La nuova destinazione beta fornisce funzionalità avanzate di esportazione dei file e supporta le esportazioni dei set di dati. |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | I partecipanti a Beta visualizzano ora due schede di destinazione [!DNL Azure Blob] affiancate nel catalogo delle destinazioni. La nuova destinazione beta fornisce funzionalità avanzate di esportazione dei file e supporta le esportazioni dei set di dati. |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | I partecipanti a Beta visualizzano ora due schede di destinazione [!DNL SFTP] affiancate nel catalogo delle destinazioni. La nuova destinazione beta fornisce funzionalità avanzate di esportazione dei file e supporta le esportazioni dei set di dati. |

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
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli della sessione]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Il campo `authorized` è stato aggiornato da tipo booleano a stringa. `season` e `episode` sono stati modificati da interi a stringhe. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli della pubblicità]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` è stato rinominato in `friendlyName` e `ID` in `name`. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli dell’errore]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` è stato rinominato in `name`. |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta la [Panoramica sul sistema XDM](../../xdm/home.md).

## Servizio query {#query-service}

Il Servizio query consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform.[!DNL Data Lake] È possibile unire qualsiasi set di dati da [!DNL Data Lake] e acquisire i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o per l&#39;acquisizione in Real-Time Customer Profile.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Monitorare le query tramite l’interfaccia utente di Platform | La scheda Query Service [!UICONTROL Scheduled Queries] fornisce una migliore visibilità dello stato di tutti i processi di query tramite l&#39;interfaccia utente. Dalla scheda [!UICONTROL Query pianificate] è ora possibile trovare informazioni importanti sullo stato delle esecuzioni delle query, inclusi messaggi di errore e codici in caso di esito negativo. Puoi anche abbonarti agli avvisi tramite l’interfaccia utente per ciascuna di queste query in base al loro stato. Per ulteriori informazioni su questa funzione, consulta il [documento sulle query di monitoraggio](../../query-service/ui/monitor-queries.md). |
| Query del modello dati per informazioni di reporting accelerate | Come parte dello SKU di Data Distiller, lo store con query accelerata consente di ridurre il tempo e la potenza di elaborazione necessari per ottenere informazioni critiche dai dati. Con l’archivio con query accelerata puoi creare un modello di dati personalizzato e/o estendere modelli di dati Adobe Real-time Customer Data Platform esistenti per migliorare le informazioni sul reporting e le relative visualizzazioni. Per ulteriori informazioni su questa funzione, consulta il documento [approfondimenti sul reporting accelerato degli archivi](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md). |

{style="table-layout:auto"}

Per ulteriori informazioni su Query Services, consulta [Panoramica di Query Service](../../query-service/home.md).
Nuove funzioni di Adobe Experience Platform:

