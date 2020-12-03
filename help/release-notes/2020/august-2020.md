---
title: Note sulla versione di Adobe Experience Platform
description: ' note sulla versione del Experience Platform 10 agosto 2020'
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: d29f7c7243ec798abe60fff895b36277996cb4a0
workflow-type: tm+mt
source-wordcount: '581'
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

[!DNL Data Science Workspace] utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per liberare informazioni dai dati. Integrato in Adobe Experience Platform, [!DNL Data Science Workspace] consente di fare previsioni utilizzando i contenuti e le risorse dati nelle soluzioni  Adobe.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti delle VM [!DNL JupyterLab] | È stata migliorata la stabilità delle [!DNL JupyterLab notebook] macchine virtuali con esecuzione prolungata. |

Per ulteriori informazioni su [!DNL JupyterLab], consulta la guida [[!DNL JupyterLab] ](../../data-science-workspace/jupyterlab/overview.md)utente.

## Destinazioni {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni pre-costruite con piattaforme di destinazione che attivano i dati a tali partner in modo semplice.

**Nuove destinazioni**

Sono disponibili nuove destinazioni in cui è possibile attivare i dati Adobe Experience Platform. Per ulteriori informazioni, vedere di seguito:

| Destinazione | Descrizione |
|--- | ---|
| [!DNL Google Customer Match] | Google Customer Match consente di utilizzare i dati online e offline per raggiungere e coinvolgere nuovamente i clienti nelle proprietà di Google possedute e gestite, ad esempio: [!DNL Search], [!DNL Shopping], Gmail e YouTube. <br><br> Per ulteriori informazioni sulla destinazione e su come configurarla in CDP in tempo reale, visita la [!DNL Google Customer Match] pagina [](../../destinations/catalog/advertising/google-customer-match.md) nel catalogo delle destinazioni. |

**Nuove funzionalità**

| Funzione | Descrizione |
|------- | -----------|
| Editor nome file personalizzato | Aggiornamento al flusso di lavoro di attivazione dei dati per le destinazioni di marketing e-mail e di archiviazione cloud che consente di modificare il nome dei file esportati. Per ulteriori informazioni, consulta il passaggio [](../../destinations/ui/activate-destinations.md#configure) Configura nel flusso di lavoro di attivazione. |
| Attributi consigliati | Aggiornamento al flusso di lavoro di attivazione dei dati per le destinazioni di marketing e-mail e di archiviazione cloud per le quali vengono visualizzati gli attributi consigliati da aggiungere ai file esportati. Per ulteriori informazioni, consulta il passaggio [](../../destinations/ui/activate-destinations.md#select-attributes) Seleziona attributi nel flusso di lavoro di attivazione. |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Basato  Experience Platform, la piattaforma dati ([!DNL Real-time CDP]) in tempo reale aiuta le aziende a mettere insieme dati noti e sconosciuti per attivare profili cliente con decisioni intelligenti per tutto il percorso del cliente. [!DNL Real-time CDP] combina più origini dati aziendali per creare profili cliente in tempo reale. I segmenti generati da questi profili possono quindi essere inviati a destinazioni a valle per fornire esperienze cliente personalizzate uno-a-uno su tutti i canali e i dispositivi.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto IAB TCF 2.0 | [!DNL Real-time CDP] è ora un fornitore registrato per la versione 2.0 del [!DNL Transparency & Consent Framework] (TCF), come indicato dallo [!DNL Interactive Advertising Bureau] (IAB). Puoi configurare le tue operazioni di dati e gli schemi di profilo per accettare i dati di consenso dei clienti generati da un CMP e applicare le preferenze di consenso dei clienti quando attivi i segmenti nelle destinazioni a valle. Per ulteriori informazioni, consulta la panoramica sul supporto [IAB TCF 2.0 in CDP](../../rtcdp/privacy/iab/overview.md) in tempo reale. |

Per ulteriori informazioni su [!DNL Real-time CDP], consultate la [[!DNL Real-time CDP] panoramica](../../rtcdp/overview.md).

## Origini {#sources}

Adobe Experience Platform è in grado di acquisire dati da origini esterne e di strutturarli, etichettarli e ottimizzarli utilizzando [!DNL Platform] i servizi. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Monitoraggio dell&#39;esecuzione dei flussi | Gli utenti possono monitorare tutte le esecuzioni del flusso e visualizzare una visualizzazione dettagliata di ciascuna esecuzione, incluso lo stato di completamento, la durata dell&#39;esecuzione, l&#39;elenco dei file elaborati, gli errori e le metriche. Per ulteriori informazioni, consulta il documento [sui flussi di dati](../../sources/tutorials/ui/monitor.md) di monitoraggio. |
| Notifiche di esecuzione del flusso | Gli utenti possono iscriversi agli eventi e registrare i webhooks per ricevere notifiche in tempo reale sullo stato, le metriche e gli errori relativi alle esecuzioni di flusso. |
| Miglioramenti al catalogo dell&#39;interfaccia utente | Aggiornamenti alla schermata del catalogo origini per consentire un accesso più semplice alle azioni principali degli oggetti selezionati. |

Per ulteriori informazioni sulle origini, consultate la panoramica sulle [origini](../../sources/home.md).