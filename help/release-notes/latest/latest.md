---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di maggio 2023 per Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: fc886dc0d7abb1df76c12edc423bc788b443a788
workflow-type: tm+mt
source-wordcount: '1361'
ht-degree: 4%

---

# Note sulla versione di Adobe Experience Platform

>[!IMPORTANT]
>
>In preparazione alla disponibilità generale della funzione Audience Portal, Adobe Experience Platform sta aggiornando l’utilizzo di &quot;tipi di pubblico&quot; e &quot;segmenti&quot; all’interno del sistema e della documentazione.
>
>- **Pubblico**: un insieme di persone, conti, famiglie o altre entità che condividono caratteristiche e comportamenti comuni.
>
>- **Definizione del segmento**: in Adobe Experience Platform, le regole utilizzate per descrivere le caratteristiche o il comportamento chiave di un pubblico target. Questo termine era precedentemente noto come &quot;segmento&quot;.
>
>- **Segmento**: atto di separazione dei profili in tipi di pubblico. Il termine &quot;segmento&quot; è ora utilizzato esclusivamente come verbo.
>
>- **Segmentazione**: atto di identificazione e articolazione delle caratteristiche dei profili che verranno raggruppati per produrre una serie di risultati, ad esempio un pubblico.
>
>Di conseguenza, nell’interfaccia di Adobe Experience Platform, i &quot;Segmenti&quot; vengono sostituiti da &quot;Tipi di pubblico&quot; per riflettere questo nuovo percorso di creazione e gestione del pubblico.

**Data di rilascio: 24 maggio 2023**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Raccolta dati](#data-collection)
- [Governance dei dati](#data-governance)
- [Acquisizione dei dati](#data-ingestion)
- [Destinazioni](#destinations)
- [Servizio Identity](#identity-service)
- [Servizio query](#query-service)
- [Origini](#sources)

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobi o non Adobi.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [!DNL Twitter] estensione API per conversioni | Il [[!DNL Twitter] API di conversione](../../tags/extensions/server/twitter/overview.md) l&#39;estensione per l&#39;inoltro degli eventi consente di inoltrare i dati evento lato server, in tempo reale, per le conversioni di eventi utilizzando [!DNL Twitter] API di conversione. |
| Assistenza nel percorso degli elementi dati | Determinazione del percorso dell’elemento dati all’interno del [Estensione core](../../tags/extensions/client/core/overview.md) ora è più facile che mai. Questo miglioramento fornisce un modulo guidato per aiutarti a selezionare e formattare il percorso corretto dell’elemento dati. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle raccolte di dati, consulta [panoramica delle raccolte dati](../../tags/home.md).

## Governance dei dati {#data-governance}

La governance dei dati di Adobe Experience Platform è una serie di strategie e tecnologie utilizzate per gestire i dati dei clienti e garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. Svolge un ruolo chiave all’interno di Experience Platform a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di accesso ai dati e controllo degli accessi ai dati per le azioni di marketing.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Obsolescenza dell’etichettatura a livello di campo del set di dati | La possibilità di applicare etichette ai singoli campi è stata spostata dai set di dati agli schemi. Questo consente di centralizzare la gestione delle etichette dei campi a monte per la governance dei dati, il consenso e il controllo degli accessi. Le etichette dei campi del set di dati applicate in precedenza saranno temporaneamente supportate tramite l’interfaccia utente di Experience Platform. Eventuali etichette per i campi del set di dati esistenti devono essere migrate manualmente alle etichette per i campi dello schema entro il 31 maggio 2024. Leggi le [guida end-to-end sulla governance dei dati](../../data-governance/e2e.md) per ulteriori informazioni sulla migrazione delle etichette. |

{style="table-layout:auto"}

Per ulteriori informazioni sulla governance dei dati, consulta [panoramica sulla governance dei dati](../../data-governance/home.md).

## Acquisizione dei dati {#data-ingestion}

Adobe Experience Platform offre un set completo di funzioni per acquisire qualsiasi tipo e latenza di dati. Puoi acquisire utilizzando API in batch o in streaming, utilizzando origini create da Adobe, partner di integrazione dei dati o l’interfaccia utente di Adobe Experience Platform.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Disponibilità beta dei modelli di acquisizione dei dati | I modelli di acquisizione dei dati forniscono agli architetti e agli ingegneri di dati modelli standard e strumenti di automazione per accelerare il processo di acquisizione dei dati, inclusa la creazione di schemi e set di dati e la configurazione delle regole di mappatura. I modelli di acquisizione dati sono attualmente disponibili per [[!DNL Marketo Engage]](../../sources/connectors/adobe-applications/marketo/marketo.md), [[!DNL Salesforce]](../../sources/connectors/crm/salesforce.md) e [[!DNL Microsoft Dynamics]](../../sources/connectors/crm/ms-dynamics.md) origini. Per ulteriori informazioni, consulta la guida su [utilizzo dei modelli nell’interfaccia utente](../../sources/tutorials/ui/templates.md). |

Per ulteriori informazioni sull’acquisizione dei dati, consulta la sezione [panoramica sull’acquisizione dei dati](../../ingestion/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni preconfigurate con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni** {#new-destinations}

| Destinazione | Descrizione |
| ----------- | ----------- |
| **[[!UICONTROL Categorie di interesse Mailchimp]](../../destinations/catalog/email-marketing/mailchimp-interest-categories.md)** | **[!UICONTROL Mailchimp]** è una popolare piattaforma di automazione del marketing e un servizio di marketing e-mail utilizzato dalle aziende per gestire e parlare con i contatti (clienti, clienti o altre parti interessate) utilizzando mailing list e campagne di marketing e-mail. Utilizza questo connettore per ordinare i contatti in base ai loro interessi e preferenze. |

{style="table-layout:auto"}

<!--

**New or updated functionality** {#destinations-new-updated-functionality}

| Functionality | Description |
| ----------- | ----------- |
| General availability of attribute-based personalization through the [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) and [Custom personalization](../../destinations/catalog/personalization/custom-personalization.md) destinations. | Leverage profile attributes in real-time to deliver one-to-one web and mobile personalization, via Adobe Target or other custom personalization destinations in Experience Platform. See the [dedicated documentation](../../destinations/ui/activate-edge-personalization-destinations.md) for more details. |
| Destination SDK support for grouping exported audiences based on merge policy. | When building a file-based destination with Destination SDK, you can now configure the grouping of exported audiences into one or multiple files, based on merge policy. <br><br> Additionally, you can now include the merge policy ID and merge policy name in the exported file names, by using the dedicated template macros. <br><br>See the [batch configuration documentation](../../destinations/destination-sdk/functionality/destination-configuration/batch-configuration.md) for more details on how to use the `segmentGroupingEnabled` parameter and the new file name template macros.|

{style="table-layout:auto"}

-->

**Correzioni di problemi e miglioramenti** {#destinations-fixes-and-enhancements}

- È stato corretto un limite nella destinazione di archiviazione cloud SFTP (Beta), a causa del quale gli utenti non potevano personalizzare il valore del parametro Port. Il valore ora è modificabile quando si imposta una connessione di destinazione SFTP (Beta) tramite il [API](/help/destinations/api/activate-segments-file-based-destinations.md) o [UI](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information).

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Servizio Identity {#identity-service}

Il servizio Adobe Experience Platform Identity offre una panoramica completa dei clienti e del loro comportamento, collegando le identità attraverso diversi dispositivi e sistemi e consentendo di offrire esperienze digitali personali e di forte impatto in tempo reale.

**Aggiornare le funzioni**

| Funzione | Descrizione |
| --- | --- |
| Supporto per gli ID partner nelle applicazioni Adobe Experience Cloud [!BADGE Beta]{type=Informative} | Gli ID partner sono ora disponibili in Identity Service. Gli ID partner sono identificatori utilizzati dai partner dati per rappresentare le persone. In Real-time Customer Data Platform, gli ID partner vengono utilizzati principalmente per l’attivazione estesa del pubblico e l’arricchimento dei dati. Gli ID partner non sono memorizzati nel grafico delle identità. Per ulteriori informazioni, consulta la documentazione su [tipi di identità](../../identity-service/namespaces.md#identity-types). |

Per ulteriori informazioni sul servizio Identity, consulta [Panoramica del servizio Identity](../../identity-service/home.md)

## Servizio query {#query-service}

Query Service consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL data lake]. Puoi unire qualsiasi set di dati dal data lake e acquisire i risultati della query sotto forma di nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o da acquisire in Real-Time Customer Profile.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Calcola le statistiche a livello di colonna per i set di dati ADLS | Il `ANALYZE TABLE` il comando è stato esteso con `COMPUTE STATISTICS` e `SHOW STATISTICS` Comandi SQL. È ora possibile calcolare le statistiche per un sottoinsieme di un set di dati ADLS o per determinate colonne all’interno di tale set di dati. Per ulteriori informazioni, leggere [guida al calcolo delle statistiche dei set di dati](../../query-service/essential-concepts/dataset-statistics.md). |

{style="table-layout:auto"}

Per ulteriori informazioni su Query Services, consulta [Panoramica di Query Service](../../query-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e consente di strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto API per lo streaming di dati da una [!DNL Snowflake] database | Ora puoi inviare dati in streaming da un [[!DNL Snowflake] sorgente](../../sources/connectors/databases/snowflake-streaming.md) utilizzando [!DNL Flow Service] API. |
| Supporto API esteso per la modalità bozza | È ora possibile mettere in pausa e salvare l’avanzamento durante il flusso di lavoro delle origini quando si utilizza [!DNL Flow Service] API in qualsiasi momento. Utilizza il `mode=draft` per salvare le connessioni di base, di origine e di destinazione come bozze. Tutte le entità 2D possono essere riesaminate per il completamento in un secondo momento. Leggi la guida su [impostazione [!DNL Flow Service] entità a stato bozza](../../sources/tutorials/api/draft.md) per ulteriori informazioni. |
| Disponibilità generale del [!DNL Salesforce Marketing Cloud] sorgente | Il [[!DNL Salesforce Marketing Cloud source] è ora in GA](../../sources/connectors/marketing-automation/salesforce-marketing-cloud.md). Utilizza questa origine per portare [!DNL Salesforce Marketing Cloud] dati di Experience Platform. |
| [!DNL Google Ads] aggiornamenti di autenticazione | Ora puoi fornire un ID cliente di accesso al momento dell’autenticazione del [!DNL Google Ads] conto di origine per recuperare i dati del rapporto da un cliente operativo specifico. Leggi le [[!DNL Google Ads] documentazione di origine](../../sources/connectors/advertising/ads.md) per ulteriori informazioni. |
| [!DNL Google PubSub] aggiornamenti di autenticazione | Ora puoi definire i privilegi di accesso per il tuo [!DNL Google PubSub] origine durante la creazione di un nuovo account. Utilizza l’autenticazione basata su progetto per consentire l’accesso a livello principale, oppure utilizza l’autenticazione basata su argomento e su sottoscrizione per limitare l’accesso a un particolare argomento e flusso di sottoscrizione. Leggi le [[!DNL Google PubSub] documentazione di origine](../../sources/connectors/cloud-storage/google-pubsub.md) per ulteriori informazioni. |
| Nuovi parametri del campo di impaginazione per `type=PAGE` nelle origini self-service (SDK batch) | Ora puoi utilizzare `initialPageIndex` e `endPageIndex` durante l’integrazione di un’origine con `type=PAGE` tramite Batch SDK. <ul><li>`initialPageIndex`: questo parametro ti consente di definire il numero di pagina da cui inizia l’impaginazione. </li><li>`endPageIndex`: questo parametro consente di stabilire una condizione finale e interrompere l’impaginazione.</li></ul> Per ulteriori informazioni su questi nuovi parametri, leggere [Documentazione dell’SDK batch di origini self-service](../../sources/sources-sdk/config/sourcespec.md#page). |
| Supporto dell’interfaccia utente per la modalità bozza | Ora tramite l’interfaccia utente di puoi mettere in pausa e salvare l’avanzamento durante il flusso di lavoro delle origini. Puoi selezionare **[!UICONTROL Salva come bozza]** durante i passaggi di dettaglio, mappatura e pianificazione del flusso di lavoro per salvarlo come bozza da completare in un secondo momento. Leggi la guida su [salvataggio dei flussi di dati come bozze nell’interfaccia utente](../../sources/tutorials/ui/draft.md) per ulteriori informazioni. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, leggere [panoramica sulle origini](../../sources/home.md).