---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' Adobe Experience Platform Query Service'
topic: overview
translation-type: tm+mt
source-git-commit: cfd767a05ad4c1dd43ac2bdde1966f9c89f5d219
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---


# Panoramica di Servizio query

 Adobe Experience Platform acquisisce i dati da un&#39;ampia varietà di fonti. Una sfida importante per gli esperti di marketing è dare un senso a questi dati per acquisire informazioni sui loro clienti.  Adobe Experience Platform Query Service facilita questa operazione consentendo di utilizzare SQL standard per eseguire query sui dati in Platform. Utilizzando Query Service, puoi unire qualsiasi dataset nel Data Lake e acquisire i risultati della query come nuovo dataset da utilizzare nei report, nell&#39;apprendimento automatico o per l&#39;inserimento nel profilo cliente in tempo reale. Questo documento fornisce una panoramica del ruolo di Query Service all&#39;interno  Experience Platform.

Servizio query consente ai marchi di collegare il percorso online-offline del cliente e di comprendere l&#39;attribuzione omnicanale. Il seguente video mostra come un&#39;azienda di esperienze può sfruttare il servizio Query per risolvere i casi di utilizzo chiave e come funziona il servizio Query.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Utilizzo di Query Service

Servizio query fornisce un&#39;interfaccia utente e un&#39;API RESTful da cui è possibile creare query SQL per analizzare meglio i dati. L&#39;interfaccia utente consente di scrivere ed eseguire query, visualizzare query eseguite in precedenza e accedere alle query salvate dagli utenti all&#39;interno dell&#39;organizzazione IMS. L&#39;interfaccia utente è destinata a essere utilizzata come sandbox per testare le query prima di eseguirle sul set di dati più ampio. Ulteriori informazioni sull&#39;utilizzo del servizio interattivo in Platform sono disponibili nella guida [all&#39;interfaccia utente del servizio](ui/overview.md)Query. L&#39;API RESTful offre un&#39;esperienza simile, consentendo di scrivere ed eseguire query in modo programmatico, pianificare query per uso futuro e ripetizioni, nonché creare modelli per le query da scrivere. Ulteriori informazioni sull&#39;utilizzo di Query Service API sono disponibili nella guida [per gli sviluppatori di](api/getting-started.md)Query Service.

## Servizio query e servizi Experience Platform 

Servizio query interagisce e può essere utilizzato insieme a più servizi Experience Platform . Per sfruttare al massimo le funzionalità di Query Service, si consiglia di acquisire familiarità con questi servizi e con come interagiscono con Query Service.

### Area di lavoro Data Science

 Adobe Experience Platform Data Science Workspace utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per acquisire informazioni dai dati memorizzati in  Experience Platform. Data Science Workspace consente agli esperti di analisi dei dati di creare ricette basate su dati di record e serie temporali relativi ai clienti e alle loro attività, facilitando previsioni quali l&#39;acquisto di propensione e le offerte consigliate che l&#39;individuo probabilmente apprezzerà e utilizzerà. È possibile utilizzare SQL in Data Science Workspace integrando Query Service in JupyterLab, per esplorare, trasformare e analizzare i dati di Adobe  Analytics. Per ulteriori informazioni su Data Science Workspace e sulla guida all&#39;integrazione di Query Service, consulta la panoramica di Data Science Workspace. Per ulteriori informazioni sulle modalità di interazione di Data Science Workspace con il servizio Query.

### Servizio di segmentazione

 Adobe Experience Platform Segmentation Service consente agli utenti di dividere i propri clienti in gruppi più piccoli che condividono caratteristiche simili. Questi segmenti possono essere successivamente valutati per fornire una migliore analisi dei dati del profilo cliente in tempo reale. Il servizio Query può essere utilizzato per fornire questa analisi eseguendo query su questi dati del segmento all&#39;interno del Data Lake. Per ulteriori informazioni sulla segmentazione, consulta la panoramica del servizio di segmentazione e la guida PQL (Profile Query Language) per ulteriori informazioni su come analizzare i segmenti.

### Caso di utilizzo di Looker BI

Con  Adobe Experience Platform, è possibile acquisire, memorizzare, strutturare e estrarre tutti i dataset memorizzati — inclusi i dati comportamentali, CRM e del punto vendita. Utilizzando [!DNL Experience Platform's Query Service]questo strumento, puoi eseguire query su questi set di dati e rispondere a domande specifiche sull&#39;azienda e iniziare a generare approfondimenti di impatto. Il seguente video illustra il valore della creazione di dashboard negli strumenti di business intelligence (BI) mediante [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Passaggi successivi e risorse aggiuntive

Leggendo questo documento, è stato introdotto il servizio Query e il suo funzionamento all&#39;interno dell&#39;ambito maggiore di  Experience Platform. Per ulteriori informazioni sull&#39;interazione con diversi endpoint all&#39;interno dell&#39;API di Query Service, consultate la guida [per gli sviluppatori di](api/getting-started.md)Query Service. Per ulteriori informazioni sull&#39;utilizzo del servizio interattivo in Platform, consultate la guida [all&#39;interfaccia utente del servizio](ui/overview.md)Query. Per un elenco completo sulla connessione di client esterni con Query Service, consultate la panoramica [dei client](clients/overview.md)Query Service.

Per prepararsi meglio a eseguire le query, guarda il seguente video. In questo video vengono condivisi suggerimenti e best practice per l’esecuzione di query nell’interfaccia dell’editor di query, nei client PSQL, nelle soluzioni business intelligence (BI) e nell’API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
