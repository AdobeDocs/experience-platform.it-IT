---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;query
solution: Experience Platform
title: Panoramica del servizio query
topic-legacy: overview
description: Questo documento fornisce una panoramica del ruolo del servizio query all’interno di Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# [!DNL Query Service]panoramica

Adobe Experience Platform acquisisce dati da un’ampia varietà di sorgenti. Una grande sfida per gli addetti al marketing è dare un senso a questi dati per ottenere informazioni sui loro clienti. Adobe Experience Platform [!DNL Query Service] consente di utilizzare SQL standard per eseguire query sui dati in [!DNL Platform]. Utilizzando [!DNL Query Service], puoi unire qualsiasi set di dati nel [!DNL Data Lake] e acquisire i risultati della query come nuovo set di dati da utilizzare nel reporting, nell’apprendimento automatico o per l’acquisizione in [!DNL Real-time Customer Profile]. Questo documento fornisce una panoramica del ruolo di [!DNL Query Service] all&#39;interno di [!DNL Experience Platform].

[!DNL Query Service] consente ai brand di collegare il percorso di clienti online-to-offline e comprendere l’attribuzione omni-channel. Il video seguente mostra come un’azienda di esperienze può sfruttare [!DNL Query Service] per risolvere i casi d’uso chiave e come funziona [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Utilizzo di [!DNL Query Service]

[!DNL Query Service] fornisce un&#39;interfaccia utente e un&#39;API RESTful da cui è possibile creare query SQL per analizzare meglio i dati. Con l’interfaccia utente è possibile scrivere ed eseguire query, visualizzare query eseguite in precedenza e accedere alle query salvate dagli utenti all’interno dell’organizzazione IMS. L’interfaccia utente è destinata a essere utilizzata come sandbox per testare le query prima di eseguirle sul set di dati più ampio. Ulteriori informazioni sull&#39;utilizzo del servizio interattivo all&#39;interno di [!DNL Platform] sono disponibili nella [Guida all&#39;interfaccia utente del servizio query](ui/overview.md). L’API RESTful offre un’esperienza simile, che consente di scrivere ed eseguire a livello di programmazione query, pianificare query per utilizzi e ripetizioni futuri e creare modelli per le query che si desidera scrivere. Ulteriori informazioni sull&#39;utilizzo dell&#39;API [!DNL Query Service] sono disponibili nella [Guida per gli sviluppatori di Query Service](api/getting-started.md).

## [!DNL Query Service] e  [!DNL Experience Platform] servizi

[!DNL Query Service] interagisce e può essere utilizzato in combinazione con più  [!DNL Experience Platform] servizi. Per sfruttare al massimo le funzionalità di [!DNL Query Service's], ti consigliamo di acquisire familiarità con questi servizi e con il modo in cui interagiscono con [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per ottenere informazioni dai dati memorizzati all&#39;interno di [!DNL Experience Platform]. [!DNL Data Science Workspace] consente agli scienziati dei dati di creare ricette basate su dati di record e serie temporali sui clienti e le loro attività, facilitando previsioni come l&#39;acquisto di propensione e offerte raccomandate che l&#39;individuo è probabile apprezzare e utilizzare. È possibile utilizzare SQL all&#39;interno di [!DNL Data Science Workspace] integrando [!DNL Query Service] in [!DNL JupyterLab], per esplorare, trasformare e analizzare i dati di Adobe Analytics. Per ulteriori informazioni su [!DNL Data Science Workspace], consulta la [!DNL Data Science Workspace] panoramica e la guida all’integrazione [!DNL Query Service] per ulteriori informazioni su come [!DNL Data Science Workspace] interagisce con [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] consente agli utenti di suddividere i propri clienti in gruppi più piccoli che condividono caratteristiche simili. Questi segmenti possono essere successivamente valutati per fornire una migliore analisi dei dati [!DNL Real-time Customer Profile]. [!DNL Query Service] può essere utilizzato per fornire questa analisi eseguendo query su questi dati del segmento all’interno di  [!DNL Data Lake]. Per ulteriori informazioni sulla segmentazione, consulta la [!DNL Segmentation Service] panoramica e la guida [!DNL Profile Query Language] (PQL) per ulteriori informazioni su come analizzare i segmenti.

### Caso di utilizzo di Looker BI

Con Adobe Experience Platform puoi acquisire, archiviare, strutturare ed estrarre tutti i set di dati memorizzati, inclusi i dati comportamentali, CRM e dei punti vendita. Utilizzando [!DNL Experience Platform's Query Service], puoi eseguire query su questi set di dati e rispondere a domande specifiche sul business, quindi iniziare a generare informazioni di impatto. Il video seguente illustra il valore della creazione di dashboard negli strumenti di business intelligence (BI) utilizzando [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Passaggi successivi e risorse aggiuntive

Leggendo questo documento, ti è stato introdotto [!DNL Query Service] e come funziona all&#39;interno dell&#39;ambito maggiore di [!DNL Experience Platform]. Per ulteriori informazioni sull’interazione con vari endpoint all’interno dell’ [!DNL Query Service] API, consulta la [Guida per gli sviluppatori di Query Service](api/getting-started.md). Per ulteriori informazioni sull&#39;utilizzo del servizio interattivo all&#39;interno di [!DNL Platform], leggere la [Guida all&#39;interfaccia utente del servizio query](ui/overview.md). Per un elenco completo sulla connessione di client esterni con [!DNL Query Service], leggere la [Panoramica dei client del servizio query](clients/overview.md).

Per prepararti meglio ad eseguire le query, guarda il video seguente. Questo video condivide suggerimenti e best practice per l’esecuzione di query nell’interfaccia dell’editor di query, client PSQL, soluzioni di business intelligence (BI) e API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
