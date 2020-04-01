---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Query Service
topic: overview
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce

---


# Panoramica di Servizio query

Adobe Experience Platform acquisisce i dati da un&#39;ampia varietà di origini. Una sfida importante per gli esperti di marketing è dare un senso a questi dati per acquisire informazioni sui loro clienti. Adobe Experience Platform Query Service facilita questa operazione consentendo di utilizzare SQL standard per eseguire query sui dati nella piattaforma. Utilizzando Query Service, puoi unire qualsiasi dataset nel Data Lake e acquisire i risultati della query come nuovo dataset da utilizzare nei report, nell&#39;apprendimento automatico o per l&#39;inserimento nel profilo cliente in tempo reale. Questo documento fornisce una panoramica del ruolo di Servizio query all&#39;interno di Experience Platform.

## Utilizzo di Query Service

Servizio query fornisce un&#39;interfaccia utente e un&#39;API RESTful da cui è possibile creare query SQL per analizzare meglio i dati. L&#39;interfaccia utente consente di scrivere ed eseguire query, visualizzare query eseguite in precedenza e accedere alle query salvate dagli utenti all&#39;interno dell&#39;organizzazione IMS. L&#39;interfaccia utente è destinata a essere utilizzata come sandbox per testare le query prima di eseguirle sul set di dati più ampio. Ulteriori informazioni sull&#39;utilizzo del servizio interattivo all&#39;interno della piattaforma sono disponibili nella guida [all&#39;interfaccia utente del servizio](ui/overview.md)query. L&#39;API RESTful offre un&#39;esperienza simile, consentendo di scrivere ed eseguire query in modo programmatico, pianificare query per uso futuro e ripetizioni, nonché creare modelli per le query da scrivere. Ulteriori informazioni sull&#39;utilizzo di Query Service API sono disponibili nella guida [per gli sviluppatori di](api/getting-started.md)Query Service.

## Servizio query e servizi della piattaforma Experience

Il servizio Query interagisce e può essere utilizzato insieme a più servizi Experience Platform. Per sfruttare al massimo le funzionalità di Query Service, si consiglia di acquisire familiarità con questi servizi e con come interagiscono con Query Service.

### Area di lavoro Data Science

Adobe Experience Platform Data Science Workspace utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per ottenere informazioni approfondite dai dati memorizzati in Experience Platform. Data Science Workspace consente agli esperti di analisi dei dati di creare ricette basate su dati di record e serie temporali relativi ai clienti e alle loro attività, facilitando previsioni quali l&#39;acquisto di propensione e le offerte consigliate che l&#39;individuo probabilmente apprezzerà e utilizzerà. È possibile utilizzare SQL in Data Science Workspace integrando Query Service in JupyterLab, per esplorare, trasformare e analizzare i dati di Adobe Analytics. Per ulteriori informazioni su Data Science Workspace e sulla guida all&#39;integrazione di Query Service, consulta la panoramica di Data Science Workspace. Per ulteriori informazioni sulle modalità di interazione di Data Science Workspace con il servizio Query.

### Servizio di segmentazione

Adobe Experience Platform Segmentation Service consente agli utenti di dividere i propri clienti in gruppi più piccoli che condividono caratteristiche simili. Questi segmenti possono essere successivamente valutati per fornire una migliore analisi dei dati del profilo cliente in tempo reale. Il servizio Query può essere utilizzato per fornire questa analisi eseguendo query su questi dati del segmento all&#39;interno del Data Lake. Per ulteriori informazioni sulla segmentazione, consulta la panoramica del servizio di segmentazione e la guida PQL (Profile Query Language) per ulteriori informazioni su come analizzare i segmenti.

## Passaggi successivi

Leggendo questo documento, è stato introdotto il servizio Query e il suo funzionamento all&#39;interno dell&#39;ambito maggiore della piattaforma Experience. Per ulteriori informazioni sull&#39;interazione con diversi endpoint all&#39;interno dell&#39;API di Query Service, consultate la guida [per gli sviluppatori di](api/getting-started.md)Query Service. Per ulteriori informazioni sull&#39;utilizzo del servizio interattivo in Piattaforma, consultate la guida [all&#39;interfaccia utente del servizio](ui/overview.md)query. Per un elenco completo sulla connessione di client esterni con Query Service, consultate la panoramica [dei client](clients/overview.md)Query Service.
