---
title: Note sulla versione di Adobe Experience Platform - Agosto 2020
description: Note sulla versione di agosto 2020 per Adobe Experience Platform.
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 23%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 12 agosto 2020**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per acquisire informazioni dai tuoi dati. Integrato in Adobe Experience Platform, [!DNL Data Science Workspace] consente di effettuare previsioni utilizzando i contenuti e i dati delle risorse delle soluzioni Adobe.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti VM in [!DNL JupyterLab] | È stata migliorata la stabilità delle macchine virtuali [!DNL JupyterLab notebook] con esecuzione prolungata. |

Per ulteriori informazioni su [!DNL JupyterLab], consulta la [[!DNL JupyterLab] guida utente](../../data-science-workspace/jupyterlab/overview.md).

## Destinazioni {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni predefinite con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

**Nuove destinazioni**

Sono disponibili nuove destinazioni in cui puoi attivare i dati Adobe Experience Platform. Per ulteriori informazioni, consulta:

| Destinazione | Descrizione |
|--- | ---|
| [!DNL Google Customer Match] | Google Customer Match consente di utilizzare i dati online e offline per raggiungere e coinvolgere nuovamente i clienti nelle proprietà possedute e gestite da Google, ad esempio: [!DNL Search], [!DNL Shopping], Gmail e YouTube. <br><br> Per ulteriori informazioni sulla destinazione e su come configurarla in Real-Time CDP, visita la [!DNL Google Customer Match] [pagina](../../destinations/catalog/advertising/google-customer-match.md) nel catalogo delle destinazioni. |

**Nuove funzioni**

| Funzione | Descrizione |
|------- | -----------|
| Editor nome file personalizzato | Aggiornamento del flusso di lavoro di attivazione dati per le destinazioni di e-mail marketing e di archiviazione cloud, che consente di modificare il nome dei file esportati. Per ulteriori informazioni, consulta il [passaggio di configurazione](../../destinations/ui/activate-batch-profile-destinations.md) nel flusso di lavoro di attivazione. |
| Attributi consigliati | Aggiornamento del flusso di lavoro di attivazione dati per le destinazioni di e-mail marketing e di archiviazione cloud che mostra gli attributi consigliati da aggiungere ai file esportati. Per ulteriori informazioni, fare riferimento al passaggio [Seleziona attributi](../../destinations/ui/activate-batch-profile-destinations.md) nel flusso di lavoro di attivazione. |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Basato su Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) consente alle aziende di unire dati noti e sconosciuti per attivare i profili cliente con decisioni intelligenti in tutto il percorso del cliente. [!DNL Real-Time CDP] combina più origini dati aziendali per creare profili cliente in tempo reale. I segmenti generati da questi profili possono quindi essere inviati alle destinazioni a valle per fornire esperienze cliente personalizzate individuali su tutti i canali e i dispositivi.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto IAB TCF 2.0 | [!DNL Real-Time CDP] è ora un fornitore registrato per la versione 2.0 di [!DNL Transparency & Consent Framework] (TCF), come indicato da [!DNL Interactive Advertising Bureau] (IAB). Puoi configurare le operazioni sui dati e gli schemi di profilo per accettare i dati di consenso del cliente generati da una CMP e applicare le preferenze di consenso dei clienti quando attivi i segmenti nelle destinazioni a valle. |

Per ulteriori informazioni su [!DNL Real-Time CDP], consulta la [[!DNL Real-Time CDP] panoramica](../../rtcdp/overview.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo consentire di strutturare, etichettare e migliorare tali dati utilizzando i servizi [!DNL Platform]. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di configurare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Monitoraggio dell’esecuzione del flusso | Gli utenti possono monitorare tutte le esecuzioni del flusso e visualizzare una vista dettagliata di ciascuna esecuzione, incluso lo stato di completamento, la durata dell’esecuzione, l’elenco dei file elaborati, gli errori e le metriche. Per ulteriori informazioni, consulta il documento [flussi di dati di monitoraggio](../../sources/tutorials/ui/monitor.md). |
| Notifiche di esecuzione del flusso | Gli utenti possono abbonarsi a eventi e registrare webhook per ricevere notifiche in tempo reale su stato, metriche ed errori relativi alle esecuzioni del flusso. |
| Miglioramenti al catalogo interfaccia utente | La schermata del catalogo delle origini è stata aggiornata per consentire un accesso più semplice alle azioni principali degli oggetti selezionati. |

Per ulteriori informazioni sulle origini, vedere [panoramica delle origini](../../sources/home.md).
