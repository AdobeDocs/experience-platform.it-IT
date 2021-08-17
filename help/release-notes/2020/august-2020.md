---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di Experience Platform 10 agosto 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: a619227de30513bb06a22ce7b4f2fc13847c1ab6
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

[!DNL Data Science Workspace] utilizza l’apprendimento automatico e l’intelligenza artificiale per trarre informazioni dai tuoi dati. Integrato in Adobe Experience Platform, [!DNL Data Science Workspace] consente di fare previsioni utilizzando i contenuti e le risorse dati nelle soluzioni Adobe.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti delle VM in [!DNL JupyterLab] | È stata migliorata la stabilità delle macchine virtuali [!DNL JupyterLab notebook] a lungo termine. |

Per ulteriori informazioni su [!DNL JupyterLab], consulta la [[!DNL JupyterLab] guida utente](../../data-science-workspace/jupyterlab/overview.md).

## Destinazioni {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni predefinite con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

**Nuove destinazioni**

Sono disponibili nuove destinazioni per l’attivazione dei dati Adobe Experience Platform. Vedi sotto per i dettagli:

| Destinazione | Descrizione |
|--- | ---|
| [!DNL Google Customer Match] | Google Customer Match consente di utilizzare i dati online e offline per raggiungere e coinvolgere nuovamente i clienti sulle proprietà possedute e gestite di Google, ad esempio: [!DNL Search], [!DNL Shopping], Gmail e YouTube. <br><br> Per ulteriori informazioni sulla destinazione e su come configurarla in Real-time CDP, visita la  [!DNL Google Customer Match] [](../../destinations/catalog/advertising/google-customer-match.md) pagina nel catalogo delle destinazioni . |

**Nuove funzionalità**

| Funzione | Descrizione |
|------- | -----------|
| Editor nome file personalizzato | Aggiornamento al flusso di lavoro di attivazione dei dati per le destinazioni di marketing e-mail e di archiviazione cloud che consente di modificare il nome dei file esportati. Per ulteriori informazioni, consulta il [ Configurare il passaggio](../../destinations/ui/activate-batch-profile-destinations.md) nel flusso di lavoro di attivazione. |
| Attributi consigliati | Aggiornamento al flusso di lavoro di attivazione dei dati per le destinazioni di marketing e-mail e di archiviazione cloud, che visualizza gli attributi consigliati da aggiungere ai file esportati. Per ulteriori informazioni, fai riferimento al [passaggio Seleziona attributi](../../destinations/ui/activate-batch-profile-destinations.md) nel flusso di lavoro di attivazione. |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Basata sull’Experience Platform, Real-time Customer Data Platform ([!DNL Real-time CDP]) consente alle aziende di unire dati noti e sconosciuti per attivare i profili dei clienti con decisioni intelligenti in tutto il percorso di clienti. [!DNL Real-time CDP] combina più origini dati aziendali per creare profili cliente in tempo reale. I segmenti generati da questi profili possono quindi essere inviati a destinazioni downstream per fornire esperienze cliente personalizzate uno-a-uno su tutti i canali e dispositivi.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto IAB TCF 2.0 | [!DNL Real-time CDP] è ora un fornitore registrato per la versione 2.0 di  [!DNL Transparency & Consent Framework] (TCF), come descritto da  [!DNL Interactive Advertising Bureau] (IAB). Puoi configurare le operazioni sui dati e gli schemi di profilo per accettare i dati di consenso dei clienti generati da una CMP e applicare le preferenze di consenso dei clienti quando attivi i segmenti sulle destinazioni a valle. |

Per ulteriori informazioni su [!DNL Real-time CDP], consulta la [[!DNL Real-time CDP] panoramica](../../rtcdp/overview.md).

## Fonti {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi [!DNL Platform] . È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Monitoraggio dell’esecuzione del flusso | Gli utenti possono monitorare tutte le esecuzioni del flusso e visualizzare una visualizzazione dettagliata di ciascuna esecuzione, tra cui lo stato di completamento, la durata dell’esecuzione, l’elenco dei file elaborati, gli errori e le metriche. Per ulteriori informazioni, consulta il documento [monitoraggio dei flussi di dati](../../sources/tutorials/ui/monitor.md) . |
| Notifiche di esecuzione del flusso | Gli utenti possono iscriversi agli eventi e registrare i webhook per ricevere notifiche in tempo reale sullo stato, le metriche e gli errori relativi alle esecuzioni dei flussi. |
| Miglioramenti al catalogo dell’interfaccia utente | Aggiornamenti alla schermata del catalogo sorgente per consentire un accesso più semplice alle azioni principali degli oggetti selezionati. |

Per ulteriori informazioni sulle origini, consulta la [panoramica origini](../../sources/home.md).
