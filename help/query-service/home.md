---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' Adobe Experience Platform Query Service'
topic: overview
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 0%

---


# [!DNL Query Service]panoramica

 Adobe Experience Platform acquisisce i dati da un&#39;ampia varietà di fonti. Una sfida importante per gli esperti di marketing è dare un senso a questi dati per acquisire informazioni sui loro clienti.  Adobe Experience Platform [!DNL Query Service] facilita tale operazione consentendo di utilizzare SQL standard per eseguire query sui dati in [!DNL Platform]. Utilizzando [!DNL Query Service], è possibile unire qualsiasi set di dati nel modulo [!DNL Data Lake] e acquisire i risultati della query come nuovo set di dati da utilizzare nei report, nell&#39;apprendimento automatico o per l&#39;inserimento in [!DNL Real-time Customer Profile]. Questo documento fornisce una panoramica del ruolo dell&#39; [!DNL Query Service] interno [!DNL Experience Platform].

[!DNL Query Service] consente ai marchi di collegare il percorso online-offline del cliente e comprendere l&#39;attribuzione omnicanale. Il seguente video mostra come un&#39;azienda di esperienze può sfruttare [!DNL Query Service] per risolvere i casi di utilizzo chiave e come [!DNL Query Service] funziona.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Using [!DNL Query Service]

[!DNL Query Service] fornisce un&#39;interfaccia utente e un&#39;API RESTful dalla quale è possibile creare query SQL per analizzare meglio i dati. L&#39;interfaccia utente consente di scrivere ed eseguire query, visualizzare query eseguite in precedenza e accedere alle query salvate dagli utenti all&#39;interno dell&#39;organizzazione IMS. L&#39;interfaccia utente è destinata a essere utilizzata come sandbox per testare le query prima di eseguirle sul set di dati più ampio. Ulteriori informazioni sull&#39;utilizzo del servizio interattivo all&#39;interno [!DNL Platform] sono disponibili nella guida [all&#39;interfaccia utente del servizio](ui/overview.md)query. L&#39;API RESTful offre un&#39;esperienza simile, consentendo di scrivere ed eseguire query in modo programmatico, pianificare query per uso futuro e ripetizioni, nonché creare modelli per le query da scrivere. Ulteriori informazioni sull&#39;utilizzo dell&#39; [!DNL Query Service] API sono disponibili nella guida [per gli sviluppatori di](api/getting-started.md)Query Service.

## [!DNL Query Service] e [!DNL Experience Platform] servizi

[!DNL Query Service] interagisce e può essere utilizzato insieme a più [!DNL Experience Platform] servizi. Per sfruttare al massimo [!DNL Query Service's] le funzionalità, si consiglia di acquisire familiarità con questi servizi e con come interagiscono con [!DNL Query Service].

### [!DNL Data Science Workspace]

 Adobe Experience Platform [!DNL Data Science Workspace] utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per acquisire informazioni dai dati memorizzati all&#39;interno [!DNL Experience Platform]. [!DNL Data Science Workspace] consente agli esperti informatici di creare ricette basate su dati di record e serie temporali relativi ai clienti e alle loro attività, facilitando previsioni quali l&#39;acquisto di propensione e le offerte consigliate che l&#39;individuo probabilmente apprezzerà e utilizzerà. È possibile utilizzare SQL all&#39;interno [!DNL Data Science Workspace] integrando [!DNL Query Service] in [!DNL JupyterLab], per esplorare, trasformare e analizzare i dati di Adobe  Analytics. Per ulteriori informazioni su [!DNL Data Science Workspace] e sulla guida all’ [!DNL Data Science Workspace]integrazione, consulta la [!DNL Query Service] panoramica per ulteriori informazioni sulle [!DNL Data Science Workspace] interazioni con [!DNL Query Service].

### [!DNL Segmentation Service]

 Adobe Experience Platform [!DNL Segmentation Service] consente agli utenti di dividere i propri clienti in gruppi più piccoli che condividono caratteristiche simili. Questi segmenti possono quindi essere valutati per fornire una migliore analisi dei [!DNL Real-time Customer Profile] dati. [!DNL Query Service] può essere utilizzata per fornire questa analisi eseguendo query su questi dati del segmento all&#39;interno del [!DNL Data Lake]. Per ulteriori informazioni sulla segmentazione, consulta la [!DNL Segmentation Service] panoramica e la guida [!DNL Profile Query Language] (PQL) per ulteriori informazioni su come analizzare i segmenti.

### Caso di utilizzo di Looker BI

Con  Adobe Experience Platform, è possibile acquisire, memorizzare, strutturare e estrarre tutti i dataset memorizzati — inclusi i dati comportamentali, CRM e del punto vendita. Utilizzando [!DNL Experience Platform's Query Service]questo strumento, puoi eseguire query su questi set di dati e rispondere a domande specifiche sull&#39;azienda e iniziare a generare approfondimenti di impatto. Il seguente video illustra il valore della creazione di dashboard negli strumenti di business intelligence (BI) mediante [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Passaggi successivi e risorse aggiuntive

Leggendo questo documento, è stato introdotto a [!DNL Query Service] e come funziona all&#39;interno dell&#39;ambito maggiore di [!DNL Experience Platform]. Per ulteriori informazioni sull&#39;interazione con diversi endpoint all&#39;interno dell&#39; [!DNL Query Service] API, consultate la guida [per gli sviluppatori di](api/getting-started.md)Query Service. Per ulteriori informazioni sull&#39;utilizzo del servizio interattivo all&#39;interno [!DNL Platform], consultate la guida [all&#39;interfaccia utente del servizio](ui/overview.md)query. Per un elenco completo sulla connessione di client esterni con [!DNL Query Service], consultate la panoramica [dei client](clients/overview.md)Query Service.

Per prepararsi meglio a eseguire le query, guarda il seguente video. In questo video vengono condivisi suggerimenti e best practice per l’esecuzione di query nell’interfaccia dell’editor di query, nei client PSQL, nelle soluzioni business intelligence (BI) e nell’API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
