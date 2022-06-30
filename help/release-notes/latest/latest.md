---
title: Note sulla versione di Adobe Experience Platform - Giugno 2022
description: Le note sulla versione di giugno 2022 per Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 3b0ae00e97eddc342e5a502f4ebf08d2fa90259f
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 5%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 22 giugno 2022**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Collection]](#data-collection)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [Servizio query](#query-service)
- [Origini](#sources)

## Raccolta dati {#data-collection}

Platform fornisce una suite di tecnologie che ti consentono di raccogliere dati sull’esperienza del cliente lato client e inviarli ad Adobe Experience Platform Edge Network, da cui arricchire, trasformare e distribuire a destinazioni Adobi o non Adobi.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| [Configurazione del tipo di accesso per i datastreams](../../edge/datastreams/overview.md#create) | Quando crei un nuovo datastream, ora puoi selezionare il tipo di richieste che desideri che la rete Edge accetti: <ul><li>**[!UICONTROL Autenticazione mista]**: Quando questa opzione è selezionata, la rete Edge accetta richieste autenticate e non autenticate. Seleziona questa opzione quando intendi usare l’SDK per web o [SDK per dispositivi mobili](https://aep-sdks.gitbook.io/docs/), insieme al [API server](../../server-api/overview.md). </li><li>**[!UICONTROL Solo autenticazione]**: Quando questa opzione è selezionata, la rete Edge accetta solo richieste autenticate. Selezionare questa opzione quando si intende utilizzare solo l&#39;API server e si desidera impedire l&#39;elaborazione di richieste non autenticate da parte del [!DNL Edge Network]. </li></ul> |
| [Proposte di rendering](../../edge/personalization/rendering-personalization-content.md#applypropositions) nelle applicazioni a pagina singola senza incrementare le metriche. | La nuova aggiunta `applyPropositions` consente di eseguire il rendering o l&#39;esecuzione di un array di proposizioni da [!DNL Target] nelle applicazioni a pagina singola, senza incrementare il [!DNL Analytics] e [!DNL Target] metriche. Questo aumenta l’accuratezza dei rapporti. |
| [Condivisione di ID da mobile a web e tra domini diversi](../../edge/identity/id-sharing.md) | L’SDK per web di Adobe Experience Platform ora supporta le funzionalità di condivisione degli ID visitatore che consentono di fornire esperienze personalizzate più accuratamente, tra app mobili e contenuti web per dispositivi mobili, e tra domini diversi. |

Per ulteriori informazioni sulla raccolta dei dati in Platform, consulta la sezione [panoramica sulla raccolta dati](../../collection/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per scatenare insights dai tuoi dati. Integrato in Adobe Experience Platform, Data Science Workspace consente di fare previsioni utilizzando i contenuti e le risorse di dati nelle soluzioni Adobe. Uno dei modi in cui Data Science Workspace ottiene questo risultato è attraverso l&#39;uso di JupyterLab. JupyterLab è un&#39;interfaccia utente basata sul Web per <a href="https://jupyter.org/" target="_blank">Jupyter del progetto</a> ed è strettamente integrato in Adobe Experience Platform. Offre agli scienziati dei dati un ambiente di sviluppo interattivo per lavorare con notebook, codice e dati Jupyter.

| Funzione | Descrizione |
| --- | --- |
| JupyterLab Launcher | JupyterLab Launcher ora include avviatori per i notebook Spark 3.2. Gli avviatori per notebook Spark 2.4 vengono ora sostituiti dai notebook Spark 3.2 e faranno parte di questa versione. |
| Spark 3.2 | Le nuove ricette Scala (Spark) e PySpark ora utilizzano Spark 3.2 |
| Kernel | I notebook Scala (Spark) vengono ora creati tramite il kernel Scala. I notebook PySpark sono ora creati tramite il Kernel Python. Il kernel Spark e PySpark sono obsoleti e sono impostati per essere rimossi in una versione successiva. |
| Ricette | Le nuove ricette PySpark e Spark ora seguono il flusso di lavoro Docker simile alle ricette Python e R. |

{style=&quot;table-layout:auto&quot;}

Per informazioni più generali su Data Science Workspace, consulta la sezione [documentazione panoramica](../../data-science-workspace/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ----------- | ----------- |
| (Beta) Supporto Destination SDK per [[!DNL Google Cloud Storage]](../../destinations/destination-sdk/server-and-file-configuration.md#gcs-example) destinazioni basate su file e [nomi di file configurabili](../../destinations/destination-sdk/file-based-destination-configuration.md#file-name-configuration). | È ora possibile utilizzare la Destination SDK per creare le destinazioni di Google Cloud Storage e definire nomi di file personalizzati per i file esportati tramite macro di nomi di file. <br><br> Il supporto per la destinazione basata su file in Adobe Experience Platform Destination SDK è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche. |
| La colonna Segmento nel flusso di dati viene eseguita su destinazioni batch | Per il flusso di dati che viene eseguito su destinazioni batch, l’interfaccia utente visualizza ora il nome del segmento associato a ogni esecuzione del flusso di dati. Ulteriori informazioni [il flusso di dati viene eseguito su destinazioni batch](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations). |

{style=&quot;table-layout:auto&quot;}

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [(Beta) Google Ad Manager 360](../../destinations/catalog/advertising/google-ad-manager-360-connection.md) | La [!DNL Google Ad Manager 360] la connessione abilita il caricamento batch per [!DNL publisher provided identifiers] (PPID) in [!DNL Google Ad Manager 360], tramite [!DNL Google Cloud Storage] <br><br>Questa destinazione è attualmente in versione beta ed è disponibile solo per un numero limitato di clienti. Per richiedere l’accesso al [!DNL Google Ad Manager 360] contatta il tuo rappresentante di Adobe e fornisci [!DNL IMS Organization ID]. |
| [[!DNL Medallia]](/help/destinations/catalog/voice/medallia-connector.md) | Attiva profili per sondaggi Medallia mirati e raccolta di feedback per comprendere meglio le esigenze e le aspettative dei clienti. |
| [[!DNL Adobe Advertising Cloud DSP]](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md) | Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) la destinazione ti consente di condividere segmenti di prime parti autenticati con inserzionisti approvati e gli utenti per l’attivazione della campagna con DSP. |

{style=&quot;table-layout:auto&quot;}

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Servizio query {#query-service}

Query Service consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati dal [!DNL Data Lake] e acquisisci i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o per l’inserimento in Profilo cliente in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Etichettatura dello schema ad hoc | Gestisci l’accesso ai dati sensibili applicando etichette ai campi di dati di schemi ad hoc generati automaticamente tramite query CTAS del servizio query. Puoi limitare l’utilizzo di determinati campi, o set di dati, di schemi ad hoc per controllare l’accesso sia a dati personali sensibili che a informazioni personali identificabili. Utilizzando la funzionalità di controllo degli accessi basata sugli attributi, puoi assegnare etichette ai campi dello schema ad hoc tramite l’interfaccia utente di Platform. |
| `FLATTEN` impostazione | Quando ci si connette a un database tramite strumenti BI di terze parti, il `FLATTEN` l’impostazione appiattisce le strutture di dati nidificate in colonne separate in cui il nome dell’attributo diventa il nome della colonna contenente i valori della riga. Questo migliora l’usabilità degli schemi ad hoc e riduce il carico di lavoro necessario per recuperare, analizzare, trasformare e creare rapporti sui dati in strumenti BI che non supportano strutture di dati nidificate. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sui servizi di query, consulta la [Panoramica del servizio query](../../query-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

| Funzione | Descrizione |
| --- | --- |
| Versione beta di [!DNL Mixpanel] source | Ora puoi utilizzare la [!DNL Mixpanel] sorgente per acquisire i dati di analisi dal [!DNL Mixpanel] conto all&#39;Experience Platform. Consulta la sezione [[!DNL Mixpanel] documentazione di origine](../../sources/connectors/analytics/mixpanel.md) per ulteriori informazioni. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
