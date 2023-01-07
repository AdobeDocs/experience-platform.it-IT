---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;query
solution: Experience Platform
title: Panoramica di Query Service
description: Questo documento fornisce una panoramica del ruolo del servizio query all’interno di Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---

# Panoramica di [!DNL Query Service]

Adobe Experience Platform acquisisce dati da un’ampia varietà di sorgenti. Una grande sfida per gli addetti al marketing è dare un senso a questi dati per ottenere informazioni sui loro clienti. Adobe Experience Platform [!DNL Query Service] facilita questo grazie all&#39;utilizzo di SQL standard per eseguire query sui dati in [!DNL Platform]. Utilizzo [!DNL Query Service], puoi unire qualsiasi set di dati nel [!DNL Data Lake] e acquisisce i risultati della query come nuovo set di dati da utilizzare nel reporting, nell’apprendimento automatico o per l’acquisizione in [!DNL Real-Time Customer Profile]. Questo documento fornisce una panoramica del ruolo di [!DNL Query Service] entro [!DNL Experience Platform].

[!DNL Query Service] consente ai brand di collegare il percorso di clienti online-to-offline e comprendere l’attribuzione omni-channel. Il video seguente mostra come un&#39;azienda di esperienze può sfruttare [!DNL Query Service] per risolvere i casi d’uso chiave e come [!DNL Query Service] funziona.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Utilizzo [!DNL Query Service]

[!DNL Query Service] fornisce un&#39;interfaccia utente e un&#39;API RESTful da cui è possibile creare query SQL per analizzare meglio i dati. Con l’interfaccia utente è possibile scrivere ed eseguire query, visualizzare query eseguite in precedenza e accedere alle query salvate dagli utenti all’interno dell’organizzazione IMS. L’interfaccia utente è destinata a essere utilizzata come sandbox per testare le query prima di eseguirle sul set di dati più ampio. Ulteriori informazioni sull&#39;utilizzo del servizio interattivo in [!DNL Platform] si trova nella [Guida all’interfaccia utente del servizio query](ui/overview.md). L’API RESTful offre un’esperienza simile, che consente di scrivere ed eseguire a livello di programmazione query, pianificare query per utilizzi e ripetizioni futuri e creare modelli per le query che si desidera scrivere. Ulteriori informazioni sull’utilizzo di [!DNL Query Service] L’API si trova in [Guida per gli sviluppatori di Query Service](api/getting-started.md).

## Servizi [!DNL Query Service] e [!DNL Experience Platform]

[!DNL Query Service] interagisce e può essere utilizzato insieme a più [!DNL Experience Platform] servizi. Per sfruttare al massimo [!DNL Query Service's] si consiglia di acquisire familiarità con questi servizi e con il modo in cui interagiscono con [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] utilizza l’apprendimento automatico e l’intelligenza artificiale per ottenere informazioni dai dati memorizzati in [!DNL Experience Platform]. [!DNL Data Science Workspace] consente agli scienziati dei dati di creare ricette basate su dati di record e serie temporali sui clienti e le loro attività, facilitando previsioni come l&#39;acquisto di propensione e offerte raccomandate che l&#39;individuo è probabile apprezzare e utilizzare. È possibile utilizzare SQL in [!DNL Data Science Workspace] mediante integrazione [!DNL Query Service] in [!DNL JupyterLab], che consente di esplorare, trasformare e analizzare i dati di Adobe Analytics. Per piacere, leggi le [!DNL Data Science Workspace] panoramica per ulteriori informazioni [!DNL Data Science Workspace]e [!DNL Query Service] guida all’integrazione per ulteriori informazioni su come [!DNL Data Science Workspace] interagisce con [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] consente agli utenti di suddividere i propri clienti in gruppi più piccoli che condividono caratteristiche simili. Questi segmenti possono essere successivamente valutati per fornire una migliore analisi dei tuoi [!DNL Real-Time Customer Profile] dati. [!DNL Query Service] può essere utilizzato per fornire questa analisi eseguendo query su questi dati del segmento all’interno di [!DNL Data Lake]. Per piacere, leggi le [!DNL Segmentation Service] panoramica per ulteriori informazioni sulla segmentazione, e [!DNL Profile Query Language] (PQL) guida per ulteriori informazioni su come analizzare i segmenti.

## Casi d’uso

[!DNL Query Service] fornisce un approccio flessibile al trattamento dei dati che svolge molti scopi. Tra gli altri, può alleggerire il peso della segmentazione da parte degli addetti al marketing e contribuire a generare tipi di pubblico utilizzabili e informazioni aziendali significative. I seguenti casi d’uso offrono esempi più approfonditi della potenza di [!DNL Query Service].

### Abbandono della navigazione Adobe Analytics

Questo [l’esempio di abbandono navigazione si concentra sull’utilizzo di Adobe [!DNL Analytics]](./use-cases/abandoned-browse.md) per creare un pubblico actionable specifico. [!DNL Query Service] gestisce una logica complessa per la segmentazione per calcolare vari attributi personalizzati da utilizzare a valle o per semplificare notevolmente la creazione dei segmenti.

### Dashboard di Looker BI

Con Adobe Experience Platform puoi acquisire, archiviare, strutturare ed estrarre tutti i set di dati memorizzati, inclusi i dati comportamentali, CRM e dei punti vendita. Utilizzo [!DNL Experience Platform's Query Service], puoi eseguire query su questi set di dati e rispondere a domande specifiche sul business e quindi iniziare a generare informazioni di impatto. Il video seguente illustra il valore della creazione di dashboard negli strumenti di business intelligence (BI) tramite [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Passaggi successivi e risorse aggiuntive

Leggendo questo documento, ti è stato presentato [!DNL Query Service] e come funziona all&#39;interno dell&#39;ambito di applicazione più ampio di [!DNL Experience Platform]. Per ulteriori informazioni sull’interazione con vari endpoint all’interno di [!DNL Query Service] API, leggi [Guida per gli sviluppatori di Query Service](api/getting-started.md). Per ulteriori informazioni sull&#39;utilizzo del servizio interattivo in [!DNL Platform], leggi la [Guida all’interfaccia utente del servizio query](ui/overview.md). Per un elenco completo sulla connessione di client esterni con [!DNL Query Service], leggi la [Panoramica dei client del servizio query](clients/overview.md).

Per prepararti meglio ad eseguire le query, guarda il video seguente. Questo video condivide suggerimenti e best practice per l’esecuzione di query nell’interfaccia dell’editor di query, client PSQL, soluzioni di business intelligence (BI) e API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
