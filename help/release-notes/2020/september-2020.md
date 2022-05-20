---
title: Note sulla versione di Adobe Experience Platform - Settembre 2020
description: Le note sulla versione di settembre 2020 per Adobe Experience Platform.
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 6%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 9 settembre 2020**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Governance dei dati](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## Governance dei dati {#governance}

La governance dei dati di Adobe Experience Platform è una serie di strategie e tecnologie utilizzate per gestire i dati dei clienti e garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. svolge un ruolo chiave all&#39;interno di [!DNL Experience Platform] a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di accesso ai dati e controllo dell’accesso ai dati per le azioni di marketing.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti all’interfaccia utente dell’etichettatura dei set di dati | Sono stati aggiunti diversi nuovi controlli di ordinamento e filtro all’interfaccia utente per l’etichettatura dei set di dati per facilitare l’utilizzo di schemi di grandi dimensioni: <ul><li>Ordina i campi in base all’ordine alfabetico in base al percorso completo dello schema.</li><li>Eseguire ricerche parziali sui nomi dei percorsi dei campi.</li><li>Filtrare i campi senza etichette, un’etichetta selezionata o una categoria di etichette.</li></ul> |

Consulta la sezione [Panoramica sulla governance dei dati](../../data-governance/home.md) per ulteriori informazioni sul servizio.

## Destinazioni {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni predefinite con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti UX | Gli utenti possono accedere ad azioni della tabella in linea per accedere più facilmente ad azioni principali come l’aggiunta di dati, la modifica della pianificazione e l’aggiunta di segmenti. Consulta la sezione [area di lavoro delle destinazioni](../../destinations/ui/destinations-workspace.md) per ulteriori informazioni. |

Per ulteriori informazioni, visita il [panoramica sulle destinazioni](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] consente di monitorare le attività in Adobe Experience Platform utilizzando metriche statistiche e notifiche di eventi.

**Nuove funzionalità**

| Funzione | Descrizione |
| --- | --- |
| Adobe I/O Notifiche evento | [!DNL Observability Insights] sfrutta gli eventi di Adobe I/O per creare notifiche di eventi per diversi servizi di Experience Platform. I payload di notifica vengono inviati a un webhook configurato che è quindi possibile utilizzare per automatizzare ulteriori processi downstream. |

Consulta la sezione [[!DNL Observability Insights] panoramica](../../observability/home.md) per ulteriori informazioni sul servizio.

## [!DNL Privacy Service] {#privacy}

Diverse normative legali e organizzative consentono agli utenti di accedere o cancellare i propri dati personali dagli archivi dati su richiesta. Adobe Experience Platform [!DNL Privacy Service] fornisce un’API RESTful e un’interfaccia utente per aiutarti a gestire queste richieste di dati dai clienti. Con [!DNL Privacy Service], puoi inviare richieste di accesso e cancellazione di dati di clienti privati o personali dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative legali e organizzative sulla privacy.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per LGPD (Brasile) | In Brasile è ora possibile creare posti di lavoro nel settore della privacy [!DNL Lei Geral de Proteção de Dados] Regolamento (LGPD). Questi posti di lavoro sono monitorati dal codice di regolamentazione `lgpd_bra`. |

Consulta la sezione [Panoramica di Privacy Service](../../privacy-service/home.md) per ulteriori informazioni sul servizio.

## Real-time Customer Profile {#profile}

Adobe Experience Platform ti consente di fornire ai clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con [!DNL Real-time Customer Profile], puoi visualizzare una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, CRM e di terze parti. [!DNL Profile] consente di consolidare i diversi dati dei clienti in una visualizzazione unificata che offre un account actionable e timestamp di ogni interazione con il cliente.

| Funzione | Descrizione |
| ------- | ----------- |
| Visualizzatore profili | Il visualizzatore del profilo, nell’interfaccia utente di Platform, è stato aggiornato per diventare un dashboard con personalizzazione completa. L’utente ora può effettuare le seguenti attività: <ul><li>Aggiorna gli attributi standard e personalizzati selezionati nel widget informazioni di base.</li><li>Creare, modificare e rimuovere widget personalizzati</li><li>Ridimensionamento e ridisposizione dei widget</li></ul> |

Per ulteriori informazioni su [!DNL Real-time Customer Profile], incluse esercitazioni e best practice per l’utilizzo di [!DNL Profile] dati, leggere [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

## Servizio di segmentazione {#segmentation}

Il servizio di segmentazione di Adobe Experience Platform fornisce un’interfaccia utente e un’API RESTful che consente di creare segmenti e generare tipi di pubblico dal proprio [!DNL Real-time Customer Profile] dati. Questi segmenti sono configurati e mantenuti a livello centrale su [!DNL Platform], rendendoli facilmente accessibili da qualsiasi applicazione di Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all’interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Esportare i processi | È stato aggiunto un flag per consentire la valutazione dei segmenti come parte di un processo di esportazione. Di conseguenza, gli utenti possono eseguire sia la segmentazione che le esportazioni in un unico processo. |
| Unisci criteri | È possibile includere più criteri di unione in un singolo processo di segmentazione batch. |

Per ulteriori informazioni su [!DNL Segmentation Service], vedi [Panoramica sulla segmentazione](../../segmentation/home.md)

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando [!DNL Platform] servizi. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Mappatura automatica | [!DNL Platform] fornisce consigli intelligenti per la mappatura automatica durante il flusso di lavoro di acquisizione dei dati, in base a uno schema di destinazione o a un set di dati selezionati dall’utente. Puoi regolare manualmente le regole di mappatura automatica flessibili in base ai tuoi casi d’uso. |
| Miglioramenti UX | Gli utenti possono accedere alle azioni della tabella in linea per accedere più facilmente alle azioni principali, ad esempio aggiungere dati, modificare la pianificazione e aggiungere segmenti. Consulta la sezione [monitoraggio dei flussi di dati](../../sources/tutorials/ui/monitor.md) per ulteriori informazioni. |

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
