---
title: Note sulla versione di Adobe Experience Platform di settembre 2020
description: Note sulla versione di settembre 2020 per Adobe Experience Platform.
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 20%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 9 settembre 2020**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Governance dei dati](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## Governance dei dati {#governance}

La governance dei dati di Adobe Experience Platform è una serie di strategie e tecnologie utilizzate per gestire i dati della clientela e garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. Svolge un ruolo chiave all&#39;interno di [!DNL Experience Platform] a vari livelli, tra cui catalogazione, derivazione dati, etichettatura di utilizzo dati, criteri di accesso ai dati e controllo degli accessi ai dati per le azioni di marketing.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti dell’interfaccia utente di etichettatura del set di dati | Nell’interfaccia utente per l’etichettatura dei set di dati sono stati aggiunti diversi nuovi controlli di ordinamento e filtro per semplificare l’utilizzo di schemi di grandi dimensioni: <ul><li>Ordina i campi in ordine alfabetico in base al percorso completo dello schema.</li><li>Eseguire ricerche parziali sui nomi dei percorsi dei campi.</li><li>Filtra i campi senza etichette, con un’etichetta selezionata o con una categoria di etichette.</li></ul> |

Per ulteriori informazioni sul servizio, vedere [Panoramica sulla governance dei dati](../../data-governance/home.md).

## Destinazioni {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni predefinite con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti UX | Gli utenti possono accedere alle azioni della tabella in linea per accedere più facilmente alle azioni principali, ad esempio l’aggiunta di dati, la modifica della pianificazione e l’aggiunta di segmenti. Per ulteriori informazioni, vedi il documento [area di lavoro destinazioni](../../destinations/ui/destinations-workspace.md). |

Per ulteriori informazioni, visita la [panoramica delle destinazioni](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] consente di monitorare le attività in Adobe Experience Platform tramite l&#39;utilizzo di metriche statistiche e notifiche di eventi.

**Nuove funzionalità**

| Funzione | Descrizione |
| --- | --- |
| Adobe I/O di notifiche di eventi | [!DNL Observability Insights] sfrutta gli eventi Adobe I/O per creare notifiche di eventi per diversi servizi Experience Platform. I payload di notifica vengono inviati a un webhook configurato che può essere utilizzato per automatizzare ulteriori processi a valle. |

Per ulteriori informazioni sul servizio, vedere [[!DNL Observability Insights] panoramica](../../observability/home.md).

## [!DNL Privacy Service] {#privacy}

Diverse normative legali e organizzative danno agli utenti il diritto di accedere ai propri dati personali o di cancellarli dagli archivi di dati su richiesta. Adobe Experience Platform [!DNL Privacy Service] fornisce un&#39;API RESTful e un&#39;interfaccia utente che consentono di gestire queste richieste di dati dei clienti. Con [!DNL Privacy Service] è possibile inviare richieste di accesso ed eliminazione di dati personali o privati dei clienti dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative legali e organizzative sulla privacy.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Sostegno alla LGPD (Brasile) | I lavori sulla privacy possono ora essere creati in base al regolamento [!DNL Lei Geral de Proteção de Dados] (LGPD) del Brasile. Questi processi vengono tracciati con il codice di regolamento `lgpd_bra`. |

Per ulteriori informazioni sul servizio, consulta la [panoramica di Privacy Service](../../privacy-service/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e pertinenti per la tua clientela, indipendentemente da dove e quando interagisce con il tuo marchio. Con [!DNL Real-Time Customer Profile] è possibile visualizzare una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, del sistema CRM e di terze parti. [!DNL Profile] consente di consolidare i dati disparati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

| Funzione | Descrizione |
| ------- | ----------- |
| Visualizzatore profili | Il visualizzatore profili, nell’interfaccia utente di Platform, è stato aggiornato per essere un dashboard con personalizzazione completa. L’utente ora può effettuare le seguenti operazioni: <ul><li>Aggiornare gli attributi standard e personalizzati selezionati nel widget delle informazioni di base.</li><li>Creare, modificare e rimuovere widget personalizzati</li><li>Ridimensionare e ridisporre i widget</li></ul> |

Per ulteriori informazioni su [!DNL Real-Time Customer Profile], inclusi tutorial e best practice per l&#39;utilizzo dei dati di [!DNL Profile], leggere la [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

## Servizio di segmentazione {#segmentation}

Il servizio di segmentazione di Adobe Experience Platform fornisce un&#39;interfaccia utente e un&#39;API RESTful che consentono di creare segmenti e generare tipi di pubblico dai dati di [!DNL Real-Time Customer Profile]. Questi segmenti vengono configurati e gestiti centralmente in [!DNL Platform], rendendoli facilmente accessibili da qualsiasi applicazione Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Processi di esportazione | È stato aggiunto un flag per consentire la valutazione dei segmenti come parte di un processo di esportazione. Di conseguenza, gli utenti possono eseguire sia la segmentazione che le esportazioni in un unico processo. |
| Criteri di unione | È possibile includere più criteri di unione in un singolo processo di segmentazione batch. |

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md)

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo consentire di strutturare, etichettare e migliorare tali dati utilizzando i servizi [!DNL Platform]. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di configurare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Mappatura automatica | [!DNL Platform] fornisce consigli intelligenti per la mappatura automatica durante il flusso di lavoro di acquisizione dati, in base a uno schema o a un set di dati di destinazione selezionato dall&#39;utente. Puoi regolare manualmente le regole di mappatura automatica flessibili in base ai tuoi casi d’uso. |
| Miglioramenti UX | Gli utenti possono accedere alle azioni della tabella in linea per accedere più facilmente alle azioni principali, come l’aggiunta di dati, la modifica della pianificazione e l’aggiunta di segmenti. Per ulteriori informazioni, consulta il documento [flussi di dati di monitoraggio](../../sources/tutorials/ui/monitor.md). |

Per ulteriori informazioni sulle origini, vedere [panoramica delle origini](../../sources/home.md).
