---
title: Note sulla versione di Adobe Experience Platform
description: Note aggiornate sulla versione di Adobe Experience Platform.
exl-id: bcd52989-ef62-4ab9-866e-1d9e57b76a0c
source-git-commit: 5a27b725d945fcfc3908b2299f770796ce4fdbd1
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 4%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 26 gennaio 2022**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Avvisi](#alerts)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Destinations]](#destinations)
- [Servizio query](#query-service)
- [Sandbox](#sandboxes)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

## Avvisi {#alerts}

L’Experience Platform ti consente di abbonarti agli avvisi basati su eventi per varie attività di Platform. Puoi abbonarti a diverse regole di avviso tramite [!UICONTROL Avvisi] nell’interfaccia utente di Platform e può scegliere di ricevere messaggi di avviso all’interno dell’interfaccia utente stessa o tramite notifiche e-mail.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuove regole di avviso | Sono ora disponibili diverse nuove regole di avviso per i flussi di lavoro relativi all’acquisizione dei dati, alle identità, ai profili, alla segmentazione e all’attivazione. Vedi la panoramica su [regole di avviso](../../observability/alerts/rules.md) per l’elenco aggiornato dei tipi di avviso. |
| Avvisi contestuali per flussi di dati di origine | Ora puoi abbonarti per ricevere messaggi di avviso sullo stato dei flussi di dati durante il flusso di lavoro di acquisizione. Per ulteriori informazioni, consulta la guida su [iscrizione agli avvisi sorgente nell’interfaccia utente](../../sources/tutorials/ui/alerts.md). |

Per ulteriori informazioni sugli avvisi in Platform, consulta [panoramica degli avvisi](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform fornisce diverse dashboard attraverso le quali puoi visualizzare informazioni importanti sui dati dell’organizzazione, acquisiti durante le istantanee giornaliere.

| Funzione | Descrizione |
| --- | --- |
| Sottotitoli intelligenti | Un algoritmo di apprendimento automatico fornisce automaticamente informazioni sul profilo e sui dati del pubblico e illustra pattern e tendenze in un periodo di 30-90 giorni o 12 mesi. Le didascalie includono informazioni su <ul><li>Forma generale e statistiche</li><li>Tendenze e modifiche brusche</li><li>Modelli stagionali</li><li>Anomalie impreviste</li></ul> Per ulteriori informazioni, consulta [dashboard dei profili](../../dashboards/guides/profiles.md#profiles-count-trend) e [dashboard segmenti](../../dashboards/guides/segments.md#audience-size-trend) documentazione. |
| Inventario delle dashboard | Accedi ai rapporti preconfigurati di profili, segmenti e dashboard di destinazioni, comprese eventuali integrazioni installate come PowerBI, in una posizione centralizzata. Per ulteriori informazioni, consulta la sezione [[!DNL Dashboards] documentazione di inventario](../../dashboards/inventory.md). |
| Modelli di rapporto PowerBI | Crea, personalizza o estende le metriche dai modelli di dati di report di profilo, segmenti e destinazioni utilizzando nuovi grafici PowerBI. Il flusso di lavoro di installazione automatizzata ti consente di condividere le informazioni di marketing all’interno dell’organizzazione dall’ambiente PowerBI. Per ulteriori informazioni, consulta la sezione [Documentazione del modello di rapporto PowerBI](../../dashboards/integrations/power-bi.md). |

Per ulteriori informazioni su [!DNL Dashboards], vedi [[!DNL Dashboards] panoramica](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Esperienza di mappatura consolidata | La nuova interfaccia di mappatura nell’interfaccia utente di Platform offre un’esperienza di mappatura coerente per sfruttare le raccomandazioni di mappatura intelligente, configurare manualmente le regole di mappatura ed eseguire il debug degli errori che si verificano nei set di mappatura. Per ulteriori informazioni, consulta la sezione [[!DNL Data Prep] Guida all’interfaccia utente](../../data-prep/ui/mapping.md). |

Per ulteriori informazioni su [!DNL Data Prep], vedi [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ----------- | ----------- |
| Personalizzazione a pagina singola e successiva | La [funzionalità di personalizzazione pagina singola e pagina successiva](../../destinations/ui/configure-personalization-destinations.md) fornisce una visualizzazione condivisa e mirabile degli utenti per le applicazioni su Experience Edge, per garantire la coerenza tra i canali di marketing e quelli dei clienti. Questa personalizzazione è possibile tramite [Connessione Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) e [Connessione di personalizzazione personalizzata](../../destinations/catalog/personalization/custom-personalization.md). Per configurare le campagne di personalizzazione della stessa pagina o della pagina successiva, consulta [esercitazione dedicata](../../destinations/ui/configure-personalization-destinations.md). |
| Monitoraggio della destinazione in batch e metriche a livello di segmento | La funzionalità di monitoraggio della destinazione è ora espansa dalle destinazioni di streaming per includere anche destinazioni batch e metriche a livello di segmento per i flussi di dati di attivazione. Per ulteriori informazioni, leggere [dashboard delle destinazioni di monitoraggio](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard) e [visualizzazione a livello di segmento](/help/dataflows/ui/monitor-destinations.md#segment-level-view). |
| Pianifica la modifica nell’interfaccia utente per i flussi di dati di attivazione batch esistenti | Questa versione introduce l’opzione per modificare la pianificazione dei flussi di dati di attivazione esistenti per le destinazioni batch. Per ulteriori informazioni, leggere [attivare i dati di profilo in destinazioni di profilo batch](/help/destinations/ui/activate-batch-profile-destinations.md). |
| Miglioramenti alla destinazione Marketo | I clienti di Experience Platform che utilizzano il Marketo Engage possono massimizzare il proprio database Marketo con la nuova possibilità di inviare i record nuovi utenti netti in Marketo Engage da Experience Platform tramite il [Connettore di destinazione Marketo](/help/destinations/catalog/adobe/marketo-engage.md). <br> Quando invii segmenti di pubblico da Experience Platform a Marketo Engage, le persone all’interno del segmento che non esistono già nel database del Marketo Engage possono essere aggiunte automaticamente a esso. Per ulteriori informazioni, leggere [Inviare un segmento Adobe Experience Platform a un elenco statico di Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html?lang=en) (il passaggio 9 nell’esercitazione indica come inviare record nuovi utenti in Marketo). |

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [Connessione Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target è un’applicazione che fornisce personalizzazione e sperimentazione in tempo reale basate sull’intelligenza artificiale in tutte le interazioni con i clienti in entrata su siti web, app mobili e altro ancora. Adobe Target è una connessione di personalizzazione in Adobe Experience Platform. |
| [Connessione di personalizzazione personalizzata](../../destinations/catalog/personalization/custom-personalization.md) | Questa connessione di personalizzazione fornisce un modo per recuperare le informazioni sui segmenti da Adobe Experience Platform a piattaforme di personalizzazione esterne, sistemi di gestione dei contenuti, server di annunci e altre applicazioni in esecuzione sui siti web dei clienti. |

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Servizio query {#query-service}

[!DNL Query Service] consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati dal [!DNL Data Lake] e acquisisci i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o per l’inserimento in Profilo cliente in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Blocco anonimo | Il costrutto SQL a blocchi anonimi consente di suddividere i processi di preparazione dei dati su larga scala in Query Service in attività più piccole, quindi riutilizzarli ed eseguirli in sequenza per il caricamento incrementale dei dati. Per ulteriori informazioni, consulta la sezione [query di esempio per la documentazione del blocco anonimo](../../query-service/best-practices/anonymous-block.md). |
| Organizzazione del set di dati | Fornisce una struttura dati coerente e logica per organizzare le risorse dati da utilizzare con Query Service man mano che la quantità di risorse dati all’interno della sandbox cresce. Per ulteriori informazioni, consulta la sezione [organizzare la documentazione delle risorse dati](../../query-service/best-practices/organize-data-assets.md). |

Per ulteriori informazioni su [!DNL Query Service], vedi [[!DNL Query Service] panoramica](../../query-service/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono provvedere allo sviluppo, al test e alla distribuzione di queste applicazioni, garantendo al contempo la conformità operativa. Per soddisfare questa esigenza, Experience Platform fornisce sandbox che suddividono una singola istanza di Platform in ambienti virtuali separati per contribuire a sviluppare e sviluppare applicazioni di esperienza digitale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Miglioramenti dell’interfaccia utente delle sandbox | L’indicatore sandbox è ora integrato nell’intestazione di tutte le applicazioni dell’interfaccia utente di Platform. L’indicatore della sandbox visualizza il nome della sandbox, la regione e il tipo e consente inoltre di accedere a un menu a discesa per passare da una sandbox all’altra. Per ulteriori informazioni, consulta la sezione [guida all’interfaccia utente di sandbox](../../sandboxes/ui/user-guide.md). |

Per ulteriori informazioni sulle sandbox, consulta la sezione [panoramica sulle sandbox](../../sandboxes/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all’interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Corrispondenza segmento | Segment Match è un servizio di collaborazione dati che consente a due o più utenti Platform di scambiare dati, basati su identificatori comuni, in modo sicuro, gestito e rispettoso della privacy. Segment Match (Corrispondenza segmento) utilizza gli standard sulla privacy di Platform e gli identificatori personali come e-mail con hash, numeri di telefono con hash e identificatori di dispositivo come IDFA e GAID. Per ulteriori informazioni, consulta la sezione [Panoramica sulla corrispondenza dei segmenti](../../segmentation/ui/segment-match/overview.md). |

Per ulteriori informazioni su [!DNL Segmentation Service], vedi [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

| Funzione | Descrizione |
| --- | --- |
| Sorgenti beta che si spostano in GA | Le seguenti origini sono state promosse dalla versione beta a GA: <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs] miglioramenti alla sorgente | La [!DNL Event Hubs] source ora supporta il tipo di autenticazione della chiave SAS non principale per la connessione e la creazione della connessione di origine. Per ulteriori informazioni, consulta la sezione [[!DNL Event Hubs] panoramica](../../sources/connectors/cloud-storage/eventhub.md). |
| [!DNL SFTP] miglioramenti alla sorgente | La [!DNL SFTP] source ora consente di stabilire un numero impostato di un numero massimo di connessioni simultanee utilizzabili da un flusso di dati per connettersi al server SFTP. Per ulteriori informazioni, consulta la sezione [[!DNL SFTP] panoramica](../../sources/connectors/cloud-storage/sftp.md). |
