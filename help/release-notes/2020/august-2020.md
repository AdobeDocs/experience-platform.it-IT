---
title: Note sulla versione di Adobe Experience Platform - Agosto 2020
description: Note sulla versione di agosto 2020 per Adobe Experience Platform.
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 6%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 12 agosto 2020**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] utilizza l’apprendimento automatico e l’intelligenza artificiale per trarre informazioni dai tuoi dati. integrata in Adobe Experience Platform, [!DNL Data Science Workspace] consente di effettuare previsioni utilizzando il contenuto e le risorse di dati nelle soluzioni Adobe.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti delle VM in [!DNL JupyterLab] | Miglioramento della stabilità del lungo periodo [!DNL JupyterLab notebook] macchine virtuali. |

Per ulteriori informazioni su [!DNL JupyterLab], vedi [[!DNL JupyterLab] guida utente](../../data-science-workspace/jupyterlab/overview.md).

## Destinazioni {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni predefinite con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

**Nuove destinazioni**

Sono disponibili nuove destinazioni per l’attivazione dei dati Adobe Experience Platform. Vedi sotto per i dettagli:

| Destinazione | Descrizione |
|--- | ---|
| [!DNL Google Customer Match] | Customer Match di Google consente di utilizzare i dati online e offline per raggiungere e coinvolgere nuovamente i clienti su proprietà possedute e gestite da Google, ad esempio: [!DNL Search], [!DNL Shopping], Gmail e YouTube. <br><br> Visita il [!DNL Google Customer Match] [page](../../destinations/catalog/advertising/google-customer-match.md) nel catalogo delle destinazioni per ulteriori informazioni sulla destinazione e su come configurarla in Real-Time CDP. |

**Nuove funzioni**

| Funzione | Descrizione |
|------- | -----------|
| Editor nome file personalizzato | Aggiornamento al flusso di lavoro di attivazione dei dati per le destinazioni di marketing e-mail e di archiviazione cloud che consente di modificare il nome dei file esportati. Per ulteriori informazioni, consulta la [ Configura passaggio](../../destinations/ui/activate-batch-profile-destinations.md) nel flusso di lavoro di attivazione. |
| Attributi consigliati | Aggiornamento al flusso di lavoro di attivazione dei dati per le destinazioni di marketing e-mail e di archiviazione cloud, che visualizza gli attributi consigliati da aggiungere ai file esportati. Per ulteriori informazioni, consulta la [Passaggio Seleziona attributi](../../destinations/ui/activate-batch-profile-destinations.md) nel flusso di lavoro di attivazione. |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Basato su Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) consente alle aziende di unire dati noti e sconosciuti per attivare i profili dei clienti con decisioni intelligenti in tutto il percorso di clienti. [!DNL Real-Time CDP] combina più origini dati aziendali per creare profili cliente in tempo reale. I segmenti generati da questi profili possono quindi essere inviati a destinazioni downstream per fornire esperienze cliente personalizzate uno-a-uno su tutti i canali e dispositivi.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto IAB TCF 2.0 | [!DNL Real-Time CDP] è ora un fornitore registrato per la versione 2.0 di [!DNL Transparency & Consent Framework] (TCF), come indicato dal [!DNL Interactive Advertising Bureau] (IAB). Puoi configurare le operazioni sui dati e gli schemi di profilo per accettare i dati di consenso dei clienti generati da una CMP e applicare le preferenze di consenso dei clienti quando attivi i segmenti sulle destinazioni a valle. |

Per ulteriori informazioni su [!DNL Real-Time CDP], vedi [[!DNL Real-Time CDP] panoramica](../../rtcdp/overview.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando [!DNL Platform] servizi. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Monitoraggio dell’esecuzione del flusso | Gli utenti possono monitorare tutte le esecuzioni del flusso e visualizzare una visualizzazione dettagliata di ciascuna esecuzione, tra cui lo stato di completamento, la durata dell’esecuzione, l’elenco dei file elaborati, gli errori e le metriche. Consulta la sezione [monitoraggio dei flussi di dati](../../sources/tutorials/ui/monitor.md) per ulteriori informazioni. |
| Notifiche di esecuzione del flusso | Gli utenti possono iscriversi agli eventi e registrare i webhook per ricevere notifiche in tempo reale sullo stato, le metriche e gli errori relativi alle esecuzioni dei flussi. |
| Miglioramenti al catalogo dell’interfaccia utente | Aggiornamenti alla schermata del catalogo sorgente per consentire un accesso più semplice alle azioni principali degli oggetti selezionati. |

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
