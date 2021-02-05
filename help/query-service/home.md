---
keywords: ' Experience Platform;home;argomenti popolari;servizio query;servizio query;query'
solution: Experience Platform
title: Panoramica del servizio Query
topic: overview
description: Questo documento fornisce una panoramica del ruolo di Query Service all'interno  Experience Platform.
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---


# [!DNL Query Service]panoramica

Adobe Experience Platform acquisisce i dati da un&#39;ampia varietà di fonti. Una sfida importante per gli esperti di marketing è dare un senso a questi dati per acquisire informazioni sui loro clienti. Adobe Experience Platform [!DNL Query Service] facilita questa operazione consentendo di utilizzare SQL standard per eseguire query sui dati in [!DNL Platform]. Utilizzando [!DNL Query Service], è possibile unire qualsiasi dataset nel [!DNL Data Lake] e acquisire i risultati della query come nuovo dataset da utilizzare nei report, nell&#39;apprendimento automatico o per l&#39;inserimento in [!DNL Real-time Customer Profile]. Questo documento fornisce una panoramica del ruolo di [!DNL Query Service] all&#39;interno di [!DNL Experience Platform].

[!DNL Query Service] consente ai marchi di collegare il percorso di clienti online e offline e di comprendere l&#39;attribuzione omnicanale. Il seguente video mostra come un&#39;azienda di esperienze può sfruttare [!DNL Query Service] per risolvere i casi d&#39;uso chiave e come funziona [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Utilizzo di [!DNL Query Service]

[!DNL Query Service] fornisce un&#39;interfaccia utente e un&#39;API RESTful dalla quale è possibile creare query SQL per analizzare meglio i dati. L&#39;interfaccia utente consente di scrivere ed eseguire query, visualizzare query eseguite in precedenza e accedere alle query salvate dagli utenti all&#39;interno dell&#39;organizzazione IMS. L&#39;interfaccia utente è destinata a essere utilizzata come sandbox per testare le query prima di eseguirle sul set di dati più ampio. Ulteriori informazioni sull&#39;utilizzo del servizio interattivo all&#39;interno di [!DNL Platform] sono disponibili nella [Guida all&#39;interfaccia utente del servizio di query](ui/overview.md). L&#39;API RESTful offre un&#39;esperienza simile, consentendo di scrivere ed eseguire query in modo programmatico, pianificare query per uso futuro e ripetizioni, nonché creare modelli per le query da scrivere. Ulteriori informazioni sull&#39;utilizzo dell&#39;API [!DNL Query Service] sono disponibili nella [Guida per gli sviluppatori di servizi di query](api/getting-started.md).

## [!DNL Query Service] e  [!DNL Experience Platform] servizi

[!DNL Query Service] interagisce e può essere utilizzato insieme a più  [!DNL Experience Platform] servizi. Per sfruttare al massimo le funzionalità di [!DNL Query Service's], è consigliabile acquisire familiarità con questi servizi e con come interagiscono con [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per acquisire informazioni dai dati memorizzati in [!DNL Experience Platform]. [!DNL Data Science Workspace] consente agli esperti informatici di creare ricette basate su dati di record e serie temporali relativi ai clienti e alle loro attività, facilitando previsioni quali l&#39;acquisto di propensione e le offerte consigliate che l&#39;individuo probabilmente apprezzerà e utilizzerà. È possibile utilizzare SQL all&#39;interno di [!DNL Data Science Workspace] integrando [!DNL Query Service] in [!DNL JupyterLab], per esplorare, trasformare e analizzare  dati Adobe Analytics. Per ulteriori informazioni su [!DNL Data Science Workspace] e sulla [!DNL Query Service] guida all&#39;integrazione, leggere la [!DNL Data Science Workspace] per ulteriori informazioni sulle modalità di interazione tra [!DNL Data Science Workspace] e [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] consente agli utenti di dividere i propri clienti in gruppi più piccoli che condividono caratteristiche simili. Questi segmenti possono quindi essere valutati per fornire una migliore analisi dei dati [!DNL Real-time Customer Profile]. [!DNL Query Service] può essere utilizzata per fornire questa analisi eseguendo query su questi dati del segmento all&#39;interno del  [!DNL Data Lake]. Per ulteriori informazioni sulla segmentazione, leggere la [!DNL Segmentation Service] panoramica e la guida [!DNL Profile Query Language] (PQL) per ulteriori informazioni su come analizzare i segmenti.

### Caso di utilizzo di Looker BI

Con Adobe Experience Platform, puoi acquisire, memorizzare, strutturare e estrarre tutti i dataset memorizzati — inclusi i dati comportamentali, CRM e del punto vendita. Utilizzando [!DNL Experience Platform's Query Service], è possibile eseguire query su questi set di dati e rispondere a domande specifiche sul business, quindi iniziare a generare approfondimenti di impatto. Il seguente video illustra il valore della creazione di dashboard negli strumenti di business intelligence (BI) utilizzando [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Passaggi successivi e risorse aggiuntive

Leggendo questo documento, è stato introdotto a [!DNL Query Service] e come funziona all&#39;interno dell&#39;ambito maggiore di [!DNL Experience Platform]. Per ulteriori informazioni sull&#39;interazione con vari endpoint all&#39;interno dell&#39;API [!DNL Query Service], consultare la [Guida per gli sviluppatori di servizi di query](api/getting-started.md). Per ulteriori informazioni sull&#39;utilizzo del servizio interattivo all&#39;interno di [!DNL Platform], leggere la [Guida all&#39;interfaccia utente del servizio di query](ui/overview.md). Per un elenco completo sulla connessione di client esterni con [!DNL Query Service], leggere la [panoramica dei client di servizi di query](clients/overview.md).

Per prepararsi meglio a eseguire le query, guarda il seguente video. In questo video vengono condivisi suggerimenti e best practice per l’esecuzione di query nell’interfaccia dell’editor di query, nei client PSQL, nelle soluzioni business intelligence (BI) e nell’API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
