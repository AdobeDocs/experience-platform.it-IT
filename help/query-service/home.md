---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;query;home;popular topic;query service;Query service;query service;query service;query
solution: Experience Platform
title: Panoramica di Query Service
description: Scopri il ruolo di Query Service in Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# Panoramica di Query Service

Adobe Experience Platform acquisisce dati da un’ampia varietà di origini. Una delle principali sfide per gli esperti di marketing è quella di dare un senso a questi dati per ottenere informazioni approfondite sui loro clienti. Per eseguire query sui dati in Platform, puoi utilizzare SQL e Adobe Experience Platform Query Service standard. È possibile utilizzare Query Service per unire qualsiasi set di dati nel data lake e acquisire i risultati della query come nuovo set di dati da utilizzare nel reporting, nell&#39;apprendimento automatico o per l&#39;acquisizione in [!DNL Real-Time Customer Profile]. Questo documento fornisce una panoramica del ruolo di Query Service in Experience Platform.

Puoi utilizzare Query Service per collegare il percorso di clienti online-offline e comprendere l’attribuzione omni-channel per il brand. Il video seguente mostra come un’azienda che si occupa di esperienze può utilizzare Query Service per risolvere casi d’uso chiave e come funziona Query Service.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Utilizzo di Query Service {#usage}

Per analizzare i dati, crea ed esegui query SQL con l’interfaccia utente di Query Service o l’API RESTful.
Con l’interfaccia utente di Query Service puoi scrivere, eseguire e pianificare le query, visualizzare le query eseguite in precedenza e accedere a quelle salvate dagli utenti della tua organizzazione. Puoi anche verificare le query prima di eseguirle sul set di dati più ampio con l’Editor query. Per una panoramica delle funzionalità dell&#39;interfaccia utente, consultare la [Guida dell&#39;interfaccia utente di Query Service](ui/overview.md).

L’API RESTful offre un’esperienza simile. È possibile utilizzare l’API Query Service per scrivere ed eseguire query a livello di programmazione, creare e salvare modelli per le query che si desidera adattare o pianificare le query per l’esecuzione automatica. Per ulteriori informazioni sull&#39;utilizzo dell&#39;API di Query Service, consultare la [Guida per gli sviluppatori di Query Service](api/getting-started.md).

Per iniziare rapidamente a utilizzare le funzioni di Query Service, si consiglia di leggere i seguenti documenti:

- [Linee guida generali per l’esecuzione delle query](./best-practices/writing-queries.md)
- [Sintassi SQL in Query Service](./sql/syntax.md)
- [Creare set di dati derivati con SQL](./data-distiller/derived-datasets/create-derived-datasets-with-sql.md)

## Servizi Query Service e Experience Platform {#experience-platform-services}

Query Service interagisce e può essere utilizzato con più servizi Experience Platform. Per trarre il massimo dalle funzionalità di Query Service, è necessario acquisire familiarità con questi servizi e con il modo in cui interagiscono con Query Service. La pagina di destinazione della documentazione di Experience Platform [](https://experienceleague.adobe.com/docs/experience-platform.html) fornisce riepiloghi e collegamenti alle funzionalità della piattaforma.

### [!DNL Data Science Workspace] {#data-science-workspace}

Adobe Experience Platform [!DNL Data Science Workspace] utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per ottenere informazioni dai dati archiviati in Experience Platform. I data scientist possono utilizzare [!DNL Data Science Workspace] per creare ricette basate su dati di record e serie temporali relativi ai clienti e alle loro attività. Queste ricette facilitano le previsioni come la propensione all&#39;acquisto e le offerte consigliate che l&#39;individuo è in grado di apprezzare e utilizzare. È possibile utilizzare SQL in [!DNL Data Science Workspace] integrando Query Service in [!DNL JupyterLab] per esplorare, trasformare e analizzare i dati di Adobe Analytics. Per ulteriori informazioni sull&#39;interazione di [!DNL Data Science Workspace] con Query Service, leggere la [[!DNL Data Science Workspace] panoramica](../data-science-workspace/home.md) e la [guida alla connessione di Jupyter Notebook](./clients/jupyter-notebook.md).

### [!DNL Segmentation Service] {#segmentation}

Utilizza il servizio di segmentazione di Adobe Experience Platform per suddividere i clienti in gruppi più piccoli che condividono caratteristiche simili. Questi tipi di pubblico possono quindi essere valutati per fornire una migliore analisi dei dati del profilo cliente in tempo reale. Puoi utilizzare Query Service per eseguire query su questi dati di pubblico all’interno del data lake e fornire l’analisi. Leggi la [Panoramica del servizio di segmentazione](../segmentation/home.md) e la guida [[!DNL Profile Query Language] (PQL)](../segmentation/pql/overview.md) per ulteriori informazioni su come analizzare i tipi di pubblico.

## Casi d’uso {#use-cases}

Query Service offre un approccio flessibile all’elaborazione dei dati, utile per diversi scopi. Può, tra l’altro, alleggerire il carico di segmentazione da parte degli esperti marketing e contribuire a generare tipi di pubblico utilizzabili e informazioni aziendali significative. I seguenti casi d’uso offrono esempi più approfonditi della potenza di Query Service.

### Abbandono navigazione Adobe Analytics {#abandon-browse}

Questo [esempio di abbandono navigazione è incentrato sull&#39;utilizzo dei dati Adobe [!DNL Analytics]](./use-cases/abandoned-browse.md) per creare un pubblico specifico utilizzabile. Query Service soddisfa una logica complessa per la segmentazione per calcolare vari attributi personalizzati da utilizzare a valle o per semplificare notevolmente la modalità di creazione dei tipi di pubblico.

## Generare informazioni approfondite con dashboard personalizzati {#custom-dashboards}

Con Adobe Experience Platform puoi acquisire, archiviare, strutturare e richiamare tutti i set di dati memorizzati, inclusi i dati comportamentali, di gestione delle relazioni con i clienti e i dati dei punti vendita. Utilizzando [!DNL Experience Platform's Query Service], puoi eseguire query su questi set di dati e rispondere a domande specifiche sull&#39;azienda, per poi iniziare a generare informazioni di impatto. Scopri come creare e gestire dashboard personalizzate in cui creare, aggiungere e modificare widget personalizzati per visualizzare le metriche chiave con [dashboard definiti dall&#39;utente](../dashboards/standard-dashboards.md). Puoi anche [personalizzare i tuoi report Real-Time CDP](../dashboards/data-models/cdp-insights-data-model-b2c.md) per i tuoi casi d&#39;uso di marketing e KPI utilizzando query SQL con i modelli dati di Real-time Customer Data Platform Insights.

## Passaggi successivi e risorse aggiuntive

Dopo aver letto questo documento, hai imparato a utilizzare Query Service e a come funziona all’interno dell’ambito di applicazione più ampio di Experience Platform. Per continuare a conoscere le funzioni di Query Service, ti consigliamo di leggere i seguenti documenti:

- [Guida per gli sviluppatori di Query Service](api/getting-started.md): per ulteriori informazioni sull&#39;interazione con vari endpoint nell&#39;API di Query Service.
- [Guida all&#39;interfaccia utente di Query Service](ui/overview.md): per ulteriori informazioni sull&#39;utilizzo di Query Editor e dell&#39;interfaccia utente.
- [Panoramica sui client di Query Service](clients/overview.md): per un elenco completo dei client esterni da connettere a Query Service.

Per prepararti meglio all’esecuzione delle query, guarda il video seguente. Questo video offre suggerimenti e best practice per l’esecuzione di query nell’interfaccia dell’editor delle query, nei client PSQL, nelle soluzioni di business intelligence (BI) e nell’API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
