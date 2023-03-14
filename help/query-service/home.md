---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;query;home;popular topic;query service;Query service;query service;query service;query
solution: Experience Platform
title: Panoramica di Query Service
description: Questo documento fornisce una panoramica del ruolo di Query Service in Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---

# Panoramica di [!DNL Query Service]

Adobe Experience Platform acquisisce dati da un’ampia varietà di origini. Una delle principali sfide per gli esperti di marketing è dare un senso a questi dati per acquisire informazioni approfondite sui loro clienti. Adobe Experience Platform [!DNL Query Service] semplifica questo processo consentendo di utilizzare SQL standard per eseguire query sui dati in [!DNL Platform]. Utilizzo di [!DNL Query Service], puoi unire qualsiasi set di dati nel [!DNL Data Lake] e acquisire i risultati della query come nuovo set di dati da utilizzare nel reporting, nell’apprendimento automatico o per l’acquisizione in [!DNL Real-Time Customer Profile]. Questo documento fornisce una panoramica del ruolo di [!DNL Query Service] entro [!DNL Experience Platform].

[!DNL Query Service] consente ai brand di collegare il percorso cliente online-offline e comprendere l’attribuzione omni-channel. Il video seguente mostra come un’azienda che offre esperienze può sfruttare [!DNL Query Service] affrontare casi d’uso chiave e come [!DNL Query Service] funziona.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Utilizzo [!DNL Query Service]

[!DNL Query Service] fornisce un’interfaccia utente e un’API RESTful da cui creare query SQL per analizzare meglio i dati. Con l’interfaccia utente di puoi scrivere ed eseguire query, visualizzare le query eseguite in precedenza e accedere a quelle salvate dagli utenti della tua organizzazione IMS. L’interfaccia utente deve essere utilizzata come sandbox per testare le query prima di eseguirle su un set di dati più ampio. Ulteriori informazioni sull’utilizzo del servizio interattivo in [!DNL Platform] si trova nella sezione [Guida all’interfaccia utente di Query Service](ui/overview.md). L’API RESTful offre un’esperienza simile che consente di scrivere ed eseguire query a livello di programmazione, pianificare le query per utilizzi e ripetizioni futuri e creare modelli per le query che desideri scrivere. Ulteriori informazioni sull&#39;utilizzo di [!DNL Query Service] L’API di si trova nella sezione [Guida per gli sviluppatori di Query Service](api/getting-started.md).

## Servizi [!DNL Query Service] e [!DNL Experience Platform]

[!DNL Query Service] interagisce e può essere utilizzato insieme a più [!DNL Experience Platform] servizi. Per trarre il massimo da [!DNL Query Service's] è consigliabile acquisire familiarità con questi servizi e con il modo in cui interagiscono con [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] utilizza l’apprendimento automatico e l’intelligenza artificiale per acquisire informazioni approfondite dai dati memorizzati in [!DNL Experience Platform]. [!DNL Data Science Workspace] consente ai data scientist di creare ricette basate su dati di record e serie temporali relativi ai clienti e alle loro attività, facilitando previsioni quali la propensione all’acquisto e le offerte consigliate che l’utente probabilmente apprezzerà e utilizzerà. È possibile utilizzare SQL in [!DNL Data Science Workspace] integrando [!DNL Query Service] in [!DNL JupyterLab], per esplorare, trasformare e analizzare i dati di Adobe Analytics. Leggi le [!DNL Data Science Workspace] panoramica per ulteriori informazioni su [!DNL Data Science Workspace]e [!DNL Query Service] per ulteriori informazioni su come [!DNL Data Science Workspace] interagisce con [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] consente agli utenti di suddividere i propri clienti in gruppi più piccoli che condividono caratteristiche simili. Questi segmenti possono essere successivamente valutati per fornire un’analisi migliore sulla [!DNL Real-Time Customer Profile] dati. [!DNL Query Service] può essere utilizzato per fornire questa analisi eseguendo query su questi dati di segmento all’interno del [!DNL Data Lake]. Leggi le [!DNL Segmentation Service] panoramica per ulteriori informazioni sulla segmentazione e [!DNL Profile Query Language] (PQL) per ulteriori informazioni su come analizzare i segmenti.

## Casi d’uso

[!DNL Query Service] offre un approccio flessibile all’elaborazione dei dati, utile per diverse finalità. Può, tra l’altro, alleggerire il carico di segmentazione da parte degli esperti marketing e contribuire a generare tipi di pubblico utilizzabili e informazioni aziendali significative. I seguenti casi d’uso offrono esempi più approfonditi della potenza di [!DNL Query Service].

### Abbandono navigazione Adobe Analytics

Questo [Adobe di abbandono navigazione [!DNL Analytics]](./use-cases/abandoned-browse.md) dati per creare un pubblico specifico actionable. [!DNL Query Service] supporta una logica complessa per la segmentazione per calcolare vari attributi personalizzati da utilizzare a valle o per semplificare notevolmente la modalità di creazione dei segmenti.

### Cruscotti Looker BI

Con Adobe Experience Platform puoi acquisire, archiviare, strutturare e richiamare tutti i set di dati memorizzati, inclusi i dati comportamentali, di gestione delle relazioni con i clienti e i dati dei punti vendita. Utilizzo di [!DNL Experience Platform's Query Service], puoi eseguire query su questi set di dati e rispondere a domande specifiche sull’azienda, per poi iniziare a generare informazioni di impatto. Il video seguente illustra il valore della creazione di dashboard negli strumenti di business intelligence (BI) tramite [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Passaggi successivi e risorse aggiuntive

Dopo aver letto questo documento, sei stato introdotto a [!DNL Query Service] e come funziona all&#39;interno dell&#39;ambito di applicazione più ampio di [!DNL Experience Platform]. Per ulteriori informazioni sull’interazione con vari endpoint all’interno di [!DNL Query Service] API, leggi le [Guida per gli sviluppatori di Query Service](api/getting-started.md). Per ulteriori informazioni sull’utilizzo del servizio interattivo in [!DNL Platform], leggi le [Guida all’interfaccia utente di Query Service](ui/overview.md). Per un elenco completo sulla connessione di client esterni con [!DNL Query Service], leggi le [Panoramica sui client di Query Service](clients/overview.md).

Per prepararti meglio all’esecuzione delle query, guarda il video seguente. Questo video offre suggerimenti e best practice per l’esecuzione di query nell’interfaccia dell’editor delle query, nei client PSQL, nelle soluzioni di business intelligence (BI) e nell’API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
