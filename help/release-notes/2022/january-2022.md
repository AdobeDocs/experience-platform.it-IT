---
title: Note sulla versione di Adobe Experience Platform - Gennaio 2022
description: Note sulla versione di Adobe Experience Platform di gennaio 2022.
exl-id: 734ce1b3-e270-4c37-958c-88bcc39fbf20
source-git-commit: 1e9d6b0c43461902c5b966aa1d0576103e872e0c
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 20%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 26 gennaio 2022**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Avvisi](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Servizio query](#query-service)
- [Sandbox](#sandboxes)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

## Avvisi {#alerts}

Un Experience Platform consente di abbonarti agli avvisi basati su eventi per varie attività di Platform. Puoi abbonarti a diverse regole di avviso tramite la scheda [!UICONTROL Avvisi] nell&#39;interfaccia utente di Platform e scegliere di ricevere messaggi di avviso all&#39;interno dell&#39;interfaccia utente stessa o tramite notifiche e-mail.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuove regole di avviso | Sono ora disponibili diverse nuove regole di avviso per i flussi di lavoro relativi all’acquisizione di dati, alle identità, ai profili, alla segmentazione e all’attivazione. Per un elenco aggiornato dei tipi di avviso, consulta la panoramica sulle [regole di avviso](../../observability/alerts/rules.md). |
| Avvisi contestuali per flussi di dati di origine | Ora puoi abbonarti e ricevere messaggi di avviso sullo stato dei flussi di dati durante il flusso di lavoro di acquisizione. Per ulteriori informazioni, consulta la guida su [abbonamento agli avvisi sulle origini nell&#39;interfaccia utente](../../sources/tutorials/ui/alerts.md). |

Per ulteriori informazioni sugli avvisi in Platform, consulta la [panoramica degli avvisi](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform fornisce più dashboard attraverso le quali è possibile visualizzare approfondimenti importanti sui dati della tua organizzazione, acquisiti durante le istantanee giornaliere.

| Funzione | Descrizione |
| --- | --- |
| Sottotitoli intelligenti | Un algoritmo di apprendimento automatico fornisce automaticamente informazioni sui dati di profilo e pubblico e illustra pattern e tendenze in un periodo di 30-90 giorni o 12 mesi. I sottotitoli includono informazioni su <ul><li>Forma generale e statistiche</li><li>Tendenze e cambiamenti repentini</li><li>Pattern stagionali</li><li>Anomalie impreviste</li></ul> Ulteriori informazioni sono disponibili nella documentazione delle [dashboard dei profili](../../dashboards/guides/profiles.md#profiles-count-trend) e delle [dashboard dei segmenti](../../dashboards/guides/audiences.md#audience-size-trend). |
| Inventario dei dashboard | Accedi ai rapporti preconfigurati delle dashboard di profili, segmenti e destinazioni, comprese le integrazioni installate come Power BI, in una posizione centralizzata. Per ulteriori informazioni, consulta la [[!DNL Dashboards] documentazione di inventario](../../dashboards/inventory.md). |
| Modelli di report Power BI | Crea, personalizza o estendi le metriche dai modelli dati di reporting di profilo, segmenti e destinazione utilizzando nuovi grafici Power BI. Il flusso di lavoro di installazione automatizzata consente di condividere le informazioni di marketing all’interno dell’organizzazione dall’ambiente Power BI. Per ulteriori informazioni, vedere la [documentazione del modello di report PowerBI](../../dashboards/integrations/power-bi.md). |

Per ulteriori informazioni su [!DNL Dashboards], vedere la [[!DNL Dashboards] panoramica](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Esperienza di mappatura consolidata | La nuova interfaccia di mappatura nell’interfaccia utente di Platform offre un’esperienza di mappatura coerente per sfruttare i consigli sulla mappatura intelligente, configurare manualmente le regole di mappatura ed eseguire il debug di eventuali errori che si verificano per i set di mappatura. Per ulteriori informazioni, vedere la [[!DNL Data Prep] Guida dell&#39;interfaccia utente](../../data-prep/ui/mapping.md). |

Per ulteriori informazioni su [!DNL Data Prep], vedere la [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ----------- | ----------- |
| Personalizzazione della stessa pagina e della pagina successiva | La funzione di personalizzazione [stessa pagina e pagina successiva](../../destinations/ui/activate-edge-personalization-destinations.md) fornisce una visualizzazione condivisa e mirata degli utenti per le applicazioni nell&#39;Edge Network, per la coerenza tra i canali di marketing e quelli dei clienti. Questa personalizzazione è possibile tramite la [connessione Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) e la [connessione di personalizzazione personalizzata](../../destinations/catalog/personalization/custom-personalization.md). Per configurare le campagne di personalizzazione della stessa pagina o della pagina successiva, consulta l&#39;[esercitazione dedicata](../../destinations/ui/activate-edge-personalization-destinations.md). |
| Monitoraggio della destinazione batch e metriche a livello di segmento | La funzionalità di monitoraggio della destinazione è ora estesa dalle destinazioni di streaming per includere anche destinazioni batch e metriche a livello di segmento per i flussi di dati di attivazione. Per ulteriori informazioni, leggere [dashboard delle destinazioni di monitoraggio](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard), [dashboard dei processi di monitoraggio dei segmenti](/help/dataflows/ui/monitor-destinations.md#monitoring-segment-jobs-dashboard) e [visualizzazione a livello di segmento](/help/dataflows/ui/monitor-destinations.md#segment-level-view). |
| Pianifica la modifica nell’interfaccia utente per i flussi di dati di attivazione batch esistenti | Questa versione introduce l’opzione per modificare la pianificazione dei flussi di dati di attivazione esistenti nelle destinazioni batch. Per ulteriori informazioni, leggere [attivare i dati profilo nelle destinazioni profilo batch](/help/destinations/ui/activate-batch-profile-destinations.md). |
| Miglioramenti alla destinazione Marketo | I clienti Experience Platform che utilizzano Marketo Engage possono massimizzare il proprio database Marketo con la nuova possibilità di inviare record persona netti al Marketo Engage da Experience Platform tramite il [connettore di destinazione Marketo](/help/destinations/catalog/adobe/marketo-engage.md). <br> Quando si inviano segmenti di pubblico da Experience Platform a Marketo Engage, è possibile aggiungere automaticamente al segmento persone che non esistono già nel database di Marketo Engage. Per ulteriori informazioni, leggere [Effettuare il push di un segmento di Adobe Experience Platform in un elenco statico di Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html) (il passaggio 9 nell&#39;esercitazione indica come eseguire il push dei record persona netti in Marketo). |

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [Connessione Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target è un’applicazione che offre personalizzazione e sperimentazione in tempo reale basata sull’intelligenza artificiale in tutte le interazioni dei clienti in entrata tramite siti web, app mobili e altro ancora. Adobe Target è una connessione di personalizzazione in Adobe Experience Platform. |
| [Connessione di personalizzazione personalizzata](../../destinations/catalog/personalization/custom-personalization.md) | Questa connessione di personalizzazione consente di recuperare informazioni sui segmenti da Adobe Experience Platform a piattaforme di personalizzazione esterne, sistemi di gestione dei contenuti, server di annunci e altre applicazioni in esecuzione sui siti web dei clienti. |

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Servizio query {#query-service}

[!DNL Query Service] consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. È possibile unire qualsiasi set di dati da [!DNL Data Lake] e acquisire i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o per l&#39;acquisizione in Real-Time Customer Profile.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Blocco anonimo | Il costrutto SQL per blocchi anonimi consente di suddividere i processi di preparazione dei dati su larga scala in Query Service in attività più piccole, quindi di riutilizzarle ed eseguirle in sequenza per il caricamento incrementale dei dati. Per ulteriori informazioni, consulta [query di esempio per la documentazione sui blocchi anonimi](../../query-service/key-concepts/anonymous-block.md). |
| Organizzazione del set di dati | Fornisce una struttura logica coerente dei dati per organizzare le risorse di dati da utilizzare con Query Service man mano che aumenta la quantità di risorse di dati all’interno della sandbox. Per ulteriori informazioni, consulta la [documentazione sulle risorse dati](../../query-service/best-practices/organize-data-assets.md). |

Per ulteriori informazioni su [!DNL Query Service], vedere la [[!DNL Query Service] panoramica](../../query-service/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa. Per soddisfare questa esigenza, Experience Platform fornisce sandbox che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Miglioramenti all’interfaccia utente delle sandbox | L’indicatore sandbox è ora integrato nell’intestazione di tutte le applicazioni dell’interfaccia utente di Platform. L’indicatore della sandbox visualizza il nome, l’area geografica e il tipo della sandbox e consente inoltre di accedere a un menu a discesa per passare da una sandbox all’altra. Per ulteriori informazioni, consulta la [guida dell&#39;interfaccia utente della sandbox](../../sandboxes/ui/user-guide.md). |

Per ulteriori informazioni sulle sandbox, consulta la [panoramica sulle sandbox](../../sandboxes/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Corrispondenza segmento | Segment Match è un servizio di collaborazione sui dati che consente a due o più utenti di Platform di scambiarsi dati, basati su identificatori comuni, in modo sicuro, gestito e rispettoso della privacy. Segment Match utilizza gli standard di privacy di Platform e gli identificatori personali come e-mail con hash, numeri di telefono con hash e identificatori di dispositivo come IDFA e GAID. Per ulteriori informazioni, consulta la [Panoramica sulla corrispondenza dei segmenti](../../segmentation/ui/segment-match/overview.md). |

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio da applicazioni Adobe, dall’archiviazione basata su cloud, da software di terze parti e dal sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

| Funzione | Descrizione |
| --- | --- |
| Sorgenti Beta che passano a GA | Le seguenti sorgenti sono state promosse dalla versione beta a GA: <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs] miglioramenti all&#39;origine | L&#39;origine [!DNL Event Hubs] ora supporta il tipo di autenticazione della chiave SAS non radice per connettersi e creare la connessione di origine. Per ulteriori informazioni, vedere la [[!DNL Event Hubs] panoramica](../../sources/connectors/cloud-storage/eventhub.md). |
| [!DNL SFTP] miglioramenti all&#39;origine | L&#39;origine [!DNL SFTP] ora consente di stabilire un numero impostato di connessioni simultanee massime che un flusso di dati può utilizzare per connettersi al server SFTP. Per ulteriori informazioni, vedere la [[!DNL SFTP] panoramica](../../sources/connectors/cloud-storage/sftp.md). |
