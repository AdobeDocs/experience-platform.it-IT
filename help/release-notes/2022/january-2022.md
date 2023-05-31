---
title: Note sulla versione di Adobe Experience Platform - Gennaio 2022
description: Note sulla versione di gennaio 2022 per Adobe Experience Platform.
exl-id: 734ce1b3-e270-4c37-958c-88bcc39fbf20
source-git-commit: 378f222b5c673632ce5792c52fc32410106def37
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 3%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 26 gennaio 2022**

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

Un Experience Platform consente di abbonarti agli avvisi basati su eventi per varie attività di Platform. È possibile abbonarsi a diverse regole di avviso tramite [!UICONTROL Avvisi] nell’interfaccia utente di Platform e può scegliere di ricevere messaggi di avviso all’interno dell’interfaccia utente stessa o tramite notifiche e-mail.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuove regole di avviso | Sono ora disponibili diverse nuove regole di avviso per i flussi di lavoro relativi all’acquisizione di dati, alle identità, ai profili, alla segmentazione e all’attivazione. Consulta la panoramica su [regole di avviso](../../observability/alerts/rules.md) per l’elenco aggiornato dei tipi di avviso. |
| Avvisi contestuali per flussi di dati di origine | Ora puoi abbonarti e ricevere messaggi di avviso sullo stato dei flussi di dati durante il flusso di lavoro di acquisizione. Per ulteriori informazioni, consulta la guida su [abbonamento agli avvisi sulle origini nell’interfaccia utente](../../sources/tutorials/ui/alerts.md). |

Per ulteriori informazioni sugli avvisi in Platform, consulta [panoramica degli avvisi](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform fornisce più dashboard attraverso i quali è possibile visualizzare informazioni importanti sui dati dell’organizzazione, acquisite durante le istantanee giornaliere.

| Funzione | Descrizione |
| --- | --- |
| Didascalie intelligenti | Un algoritmo di apprendimento automatico fornisce automaticamente informazioni sui dati di profilo e pubblico e illustra pattern e tendenze in un periodo di 30-90 giorni o 12 mesi. I sottotitoli includono informazioni su <ul><li>Forma generale e statistiche</li><li>Tendenze e cambiamenti repentini</li><li>Pattern stagionali</li><li>Anomalie impreviste</li></ul> Ulteriori informazioni sono disponibili sul sito [dashboard dei profili](../../dashboards/guides/profiles.md#profiles-count-trend) e [dashboard dei segmenti](../../dashboards/guides/segments.md#audience-size-trend) documentazione. |
| Inventario dei dashboard | Accedi ai rapporti preconfigurati delle dashboard di profili, segmenti e destinazioni, comprese le integrazioni installate come Power BI, in una posizione centralizzata. Per ulteriori informazioni, vedere [[!DNL Dashboards] documentazione di inventario](../../dashboards/inventory.md). |
| Modelli di report Power BI | Crea, personalizza o estendi le metriche dai modelli dati di reporting di profilo, segmenti e destinazione utilizzando nuovi grafici Power BI. Il flusso di lavoro di installazione automatizzata consente di condividere le informazioni di marketing all’interno dell’organizzazione dall’ambiente Power BI. Per ulteriori informazioni, vedere [Documentazione del modello di report Power BI](../../dashboards/integrations/power-bi.md). |

Per ulteriori informazioni su [!DNL Dashboards], consultare il [[!DNL Dashboards] panoramica](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Esperienza di mappatura consolidata | La nuova interfaccia di mappatura nell’interfaccia utente di Platform offre un’esperienza di mappatura coerente per sfruttare i consigli sulla mappatura intelligente, configurare manualmente le regole di mappatura ed eseguire il debug di eventuali errori che si verificano per i set di mappatura. Per ulteriori informazioni, vedere [[!DNL Data Prep] Guida all’interfaccia utente](../../data-prep/ui/mapping.md). |

Per ulteriori informazioni su [!DNL Data Prep], consultare il [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni preconfigurate con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ----------- | ----------- |
| Personalizzazione della stessa pagina e della pagina successiva | Il [funzione di personalizzazione della stessa pagina e della pagina successiva](../../destinations/ui/activate-edge-personalization-destinations.md) fornisce una visualizzazione condivisa e mirata degli utenti per le applicazioni Experience Edge, per coerenza tra i canali di marketing e quelli dei clienti. Questa personalizzazione è possibile tramite [Connessione Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) e [Connessione di personalizzazione personalizzata](../../destinations/catalog/personalization/custom-personalization.md). Per configurare le campagne di personalizzazione della stessa pagina o della pagina successiva, consulta [tutorial dedicato](../../destinations/ui/activate-edge-personalization-destinations.md). |
| Monitoraggio della destinazione batch e metriche a livello di segmento | La funzionalità di monitoraggio della destinazione è ora estesa dalle destinazioni di streaming per includere anche destinazioni batch e metriche a livello di segmento per i flussi di dati di attivazione. Per ulteriori informazioni, consulta [dashboard delle destinazioni di monitoraggio](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard), [monitoraggio del dashboard processi di segmento](/help/dataflows/ui/monitor-destinations.md#monitoring-segment-jobs-dashboard), e [vista a livello di segmento](/help/dataflows/ui/monitor-destinations.md#segment-level-view). |
| Pianifica la modifica nell’interfaccia utente per i flussi di dati di attivazione batch esistenti | Questa versione introduce l’opzione per modificare la pianificazione dei flussi di dati di attivazione esistenti nelle destinazioni batch. Per ulteriori informazioni, consulta [attivare i dati profilo nelle destinazioni profilo batch](/help/destinations/ui/activate-batch-profile-destinations.md). |
| Miglioramenti alla destinazione Marketo | I clienti Experience Platform che utilizzano Marketi Engage possono massimizzare il proprio database Marketo con la nuova possibilità di inserire in Marketi Engage i record di persone nuovi tramite Experience Platform [Connettore di destinazione Marketo](/help/destinations/catalog/adobe/marketo-engage.md). <br> Quando si inviano segmenti di pubblico da un Experience Platform Marketo Engage all’altro, è possibile aggiungere automaticamente al segmento persone che non esistono già nel database del Marketo Engage. Per ulteriori informazioni, consulta [Invio di un segmento Adobe Experience Platform a un elenco statico Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html?lang=en) (il passaggio 9 nell’esercitazione indica come inserire in Marketo i record persona netti nuovi). |

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [Connessione Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target è un’applicazione che offre personalizzazione e sperimentazione in tempo reale basata sull’intelligenza artificiale in tutte le interazioni dei clienti in entrata tramite siti web, app mobili e altro ancora. Adobe Target è una connessione di personalizzazione in Adobe Experience Platform. |
| [Connessione di personalizzazione personalizzata](../../destinations/catalog/personalization/custom-personalization.md) | Questa connessione di personalizzazione consente di recuperare informazioni sui segmenti da Adobe Experience Platform a piattaforme di personalizzazione esterne, sistemi di gestione dei contenuti, server di annunci e altre applicazioni in esecuzione sui siti web dei clienti. |

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Servizio query {#query-service}

[!DNL Query Service] consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati da [!DNL Data Lake] e acquisisci i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o per l’acquisizione in Real-time Customer Profile.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Blocco anonimo | Il costrutto SQL per blocchi anonimi consente di suddividere i processi di preparazione dei dati su larga scala in Query Service in attività più piccole, quindi di riutilizzarle ed eseguirle in sequenza per il caricamento incrementale dei dati. Per ulteriori informazioni, vedere [query di esempio per la documentazione del blocco anonimo](../../query-service/essential-concepts/anonymous-block.md). |
| Organizzazione del set di dati | Fornisce una struttura logica coerente dei dati per organizzare le risorse di dati da utilizzare con Query Service man mano che aumenta la quantità di risorse di dati all’interno della sandbox. Per ulteriori informazioni, vedere [organizzare la documentazione delle risorse dati](../../query-service/best-practices/organize-data-assets.md). |

Per ulteriori informazioni su [!DNL Query Service], consultare il [[!DNL Query Service] panoramica](../../query-service/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa. Per soddisfare questa esigenza, Experience Platform fornisce sandbox che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Miglioramenti all’interfaccia utente delle sandbox | L’indicatore sandbox è ora integrato nell’intestazione di tutte le applicazioni dell’interfaccia utente di Platform. L’indicatore della sandbox visualizza il nome, l’area geografica e il tipo della sandbox e consente inoltre di accedere a un menu a discesa per passare da una sandbox all’altra. Per ulteriori informazioni, vedere [guida all’interfaccia utente di sandbox](../../sandboxes/ui/user-guide.md). |

Per ulteriori informazioni sulle sandbox, consulta [panoramica sulle sandbox](../../sandboxes/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo commerciabile di persone all’interno della tua base clienti. I segmenti possono essere basati su dati record (ad esempio informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Corrispondenza segmento | Segment Match è un servizio di collaborazione sui dati che consente a due o più utenti di Platform di scambiarsi dati, basati su identificatori comuni, in modo sicuro, gestito e rispettoso della privacy. Segment Match utilizza gli standard di privacy di Platform e gli identificatori personali come e-mail con hash, numeri di telefono con hash e identificatori di dispositivo come IDFA e GAID. Per ulteriori informazioni, vedere [Panoramica di Segment Match](../../segmentation/ui/segment-match/overview.md). |

Per ulteriori informazioni su [!DNL Segmentation Service], consultare il [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

| Funzione | Descrizione |
| --- | --- |
| Sorgenti beta che passano a GA | Le seguenti sorgenti sono state promosse dalla versione beta a GA: <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs] miglioramenti all&#39;origine | Il [!DNL Event Hubs] source ora supporta il tipo di autenticazione con chiave SAS non radice per la connessione e la creazione della connessione di origine. Per ulteriori informazioni, vedere [[!DNL Event Hubs] panoramica](../../sources/connectors/cloud-storage/eventhub.md). |
| [!DNL SFTP] miglioramenti all&#39;origine | Il [!DNL SFTP] source ora consente di stabilire un numero impostato di connessioni simultanee massime che un flusso di dati può utilizzare per connettersi al server SFTP. Per ulteriori informazioni, vedere [[!DNL SFTP] panoramica](../../sources/connectors/cloud-storage/sftp.md). |
