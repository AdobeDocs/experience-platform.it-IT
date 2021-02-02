---
title: Note sulla versione di Adobe Experience Platform
description: ' note sulla versione del Experience Platform 10 agosto 2020'
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 49c984a60fd699706eec508ec1d786340df40b57
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 7%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 12 agosto 2020**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per liberare informazioni dai dati. Integrato in Adobe Experience Platform, [!DNL Data Science Workspace] consente di creare previsioni utilizzando i contenuti e le risorse dati nelle soluzioni  Adobe.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti della VM in [!DNL JupyterLab] | È stata migliorata la stabilità delle [!DNL JupyterLab notebook] macchine virtuali con esecuzione prolungata. |

Per ulteriori informazioni su [!DNL JupyterLab], vedere la [[!DNL JupyterLab] guida utente](../../data-science-workspace/jupyterlab/overview.md).

## Destinazioni {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni pre-costruite con piattaforme di destinazione che attivano i dati a tali partner in modo semplice.

**Nuove destinazioni**

Sono disponibili nuove destinazioni in cui è possibile attivare i dati Adobe Experience Platform. Per ulteriori informazioni, vedere di seguito:

| Destinazione | Descrizione |
|--- | ---|
| [!DNL Google Customer Match] | Google Customer Match consente di utilizzare i dati online e offline per raggiungere e coinvolgere nuovamente i clienti nelle proprietà di Google possedute e gestite, ad esempio: [!DNL Search], [!DNL Shopping], Gmail e YouTube. <br><br> Per ulteriori informazioni sulla destinazione e su come configurarla in CDP in tempo reale, visita la  [!DNL Google Customer Match] [](../../destinations/catalog/advertising/google-customer-match.md) pagina nel catalogo delle destinazioni. |

**Nuove funzionalità**

| Funzione | Descrizione |
|------- | -----------|
| Editor nome file personalizzato | Aggiornamento al flusso di lavoro di attivazione dei dati per le destinazioni di marketing e-mail e di archiviazione cloud che consente di modificare il nome dei file esportati. Per ulteriori informazioni, fare riferimento alla sezione [ Configurare il passaggio](../../destinations/ui/activate-destinations.md#configure) nel flusso di lavoro di attivazione. |
| Attributi consigliati | Aggiornamento al flusso di lavoro di attivazione dei dati per le destinazioni di marketing e-mail e di archiviazione cloud per le quali vengono visualizzati gli attributi consigliati da aggiungere ai file esportati. Per ulteriori informazioni, fare riferimento al [Selezionare gli attributi step](../../destinations/ui/activate-destinations.md#select-attributes) nel flusso di lavoro di attivazione. |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Basato  Experience Platform, la piattaforma dati cliente in tempo reale ([!DNL Real-time CDP]) consente alle aziende di mettere insieme dati noti e sconosciuti per attivare profili cliente con decisioni intelligenti in tutto il percorso cliente. [!DNL Real-time CDP] combina più origini dati aziendali per creare profili cliente in tempo reale. I segmenti generati da questi profili possono quindi essere inviati a destinazioni a valle per fornire esperienze cliente personalizzate uno-a-uno su tutti i canali e i dispositivi.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto IAB TCF 2.0 | [!DNL Real-time CDP] è ora un fornitore registrato per la versione 2.0 del  [!DNL Transparency & Consent Framework] (TCF), come indicato dallo  [!DNL Interactive Advertising Bureau] (IAB). Puoi configurare le tue operazioni di dati e gli schemi di profilo per accettare i dati di consenso dei clienti generati da un CMP e applicare le preferenze di consenso dei clienti quando attivi i segmenti nelle destinazioni a valle. |

Per ulteriori informazioni su [!DNL Real-time CDP], vedere la [[!DNL Real-time CDP] panoramica](../../rtcdp/overview.md).

## Origini {#sources}

Adobe Experience Platform è in grado di acquisire dati da origini esterne consentendo al contempo di strutturare, etichettare e migliorare tali dati utilizzando i servizi [!DNL Platform]. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Monitoraggio dell&#39;esecuzione dei flussi | Gli utenti possono monitorare tutte le esecuzioni del flusso e visualizzare una visualizzazione dettagliata di ciascuna esecuzione, incluso lo stato di completamento, la durata dell&#39;esecuzione, l&#39;elenco dei file elaborati, gli errori e le metriche. Per ulteriori informazioni, vedere il documento [Monitoring dataflows](../../sources/tutorials/ui/monitor.md). |
| Notifiche di esecuzione del flusso | Gli utenti possono iscriversi agli eventi e registrare i webhooks per ricevere notifiche in tempo reale sullo stato, le metriche e gli errori relativi alle esecuzioni di flusso. |
| Miglioramenti al catalogo dell&#39;interfaccia utente | Aggiornamenti alla schermata del catalogo origini per consentire un accesso più semplice alle azioni principali degli oggetti selezionati. |

Per ulteriori informazioni sulle origini, vedere la [panoramica delle origini](../../sources/home.md).