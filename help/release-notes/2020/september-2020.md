---
title: Note sulla versione di Adobe Experience Platform
description: ' Experience Platform note sulla versione 9 settembre 2020'
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: adf8e8457c8ffef263223a38d3f9c345cf7c6ab2
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 6%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 9 settembre 2020**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Governance]](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Governance] {#governance}

Adobe Experience Platform Data Governance è una serie di strategie e tecnologie utilizzate per gestire i dati dei clienti e garantire la conformità a normative, restrizioni e criteri applicabili all&#39;utilizzo dei dati. Esso svolge un ruolo chiave a vari livelli, [!DNL Experience Platform] tra cui catalogazione, linea di dati, etichettatura dell&#39;utilizzo dei dati, criteri di accesso ai dati e controllo dell&#39;accesso ai dati per le azioni di marketing.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti all&#39;interfaccia utente per l&#39;etichettatura dei set di dati | Diversi nuovi controlli di ordinamento e filtro sono stati aggiunti all&#39;interfaccia utente per l&#39;etichettatura dei set di dati per facilitare l&#39;utilizzo di schemi di grandi dimensioni: <ul><li>Ordinare i campi in ordine alfabetico in base al percorso completo dello schema.</li><li>Eseguire ricerche parziali sui nomi dei percorsi dei campi.</li><li>Filtrare i campi senza etichette, etichetta selezionata o categoria di etichette.</li></ul> |

Per ulteriori informazioni sul servizio, consulta la panoramica [sulla governance dei](../../data-governance/home.md) dati.

## Destinazioni {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni pre-costruite con piattaforme di destinazione che attivano i dati a tali partner in modo semplice.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti UX | Gli utenti possono accedere alle azioni della tabella in linea per un accesso più semplice alle azioni principali, ad esempio l&#39;aggiunta di dati, la modifica della pianificazione e l&#39;aggiunta di segmenti. Per ulteriori informazioni, consulta il documento sull’area di lavoro [delle](../../destinations/ui/destinations-workspace.md) destinazioni. |

Per saperne di più, visita la panoramica [delle destinazioni](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] consente di monitorare le attività su Adobe Experience Platform mediante l&#39;uso di metriche statistiche e notifiche di eventi.

**Nuove funzionalità**

| Funzione | Descrizione |
| --- | --- |
|  Notifiche evento Adobe I/O | [!DNL Observability Insights] sfrutta  Adobe I/O Events per creare notifiche di eventi per diversi servizi  Experience Platform. I payload di notifica vengono inviati a un webhook configurato che puoi quindi utilizzare per automatizzare ulteriori processi a valle. Per ulteriori informazioni, consulta la panoramica [delle](../../observability/notifications/overview.md) notifiche. |

Per ulteriori informazioni sul servizio, consultate la [[!DNL Observability Insights] panoramica](../../observability/home.md) .

## [!DNL Privacy Service] {#privacy}

Diverse normative legali e organizzative danno agli utenti il diritto di accedere o cancellare i propri dati personali dall&#39;archivio dei dati su richiesta. Adobe Experience Platform [!DNL Privacy Service] fornisce un&#39;API RESTful e un&#39;interfaccia utente per aiutarti a gestire queste richieste di dati dai tuoi clienti. Con [!DNL Privacy Service]questa opzione puoi inviare richieste di accesso ed eliminazione di dati di clienti privati o personali dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative sulla privacy legali e organizzative.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per LGPD (Brasile) | I lavori per la privacy possono ora essere creati in base alla normativa brasiliana [!DNL Lei Geral de Proteção de Dados] (LGPD). Questi posti di lavoro sono tracciati secondo il codice di regolamentazione `lgpd_bra`. |

Per ulteriori informazioni sul servizio, consultate la panoramica [dei](../../privacy-service/home.md) Privacy Service.

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform consente di creare esperienze coordinate, coerenti e pertinenti per i clienti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con [!DNL Real-time Customer Profile], puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi online, offline, CRM e dati di terze parti. [!DNL Profile] consente di consolidare i diversi dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

| Funzione | Descrizione |
| ------- | ----------- |
| Visualizzatore profilo | Il visualizzatore del profilo, nell’interfaccia utente della piattaforma, è stato aggiornato per essere un dashboard con personalizzazione completa. L&#39;utente ora può effettuare le seguenti operazioni: <ul><li>Aggiorna gli attributi standard e personalizzati selezionati nel widget delle informazioni di base.</li><li>Creare, modificare e rimuovere widget personalizzati</li><li>Ridimensionare e ridisporre i widget</li></ul> |

Per ulteriori informazioni [!DNL Real-time Customer Profile], comprese esercitazioni e best practice per l’utilizzo dei [!DNL Profile] dati, consulta la panoramica [Profilo cliente](../../profile/home.md)in tempo reale.

## Servizio di segmentazione {#segmentation}

Adobe Experience Platform Segmentation Service fornisce un&#39;interfaccia utente e RESTful API che consente di creare segmenti e generare audience dai [!DNL Real-time Customer Profile] dati. Questi segmenti sono configurati e mantenuti a livello centrale [!DNL Platform], rendendoli facilmente accessibili da qualsiasi applicazione  Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all&#39;interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Esportare i processi | È stato aggiunto un flag per consentire la valutazione dei segmenti come parte di un processo di esportazione. Di conseguenza, gli utenti possono eseguire sia la segmentazione che le esportazioni in un singolo processo. |
| Unisci criteri | È possibile includere più criteri di unione in un singolo processo di segmentazione batch. |

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la panoramica sulla [segmentazione](../../segmentation/home.md)

## Origini {#sources}

Adobe Experience Platform è in grado di acquisire dati da origini esterne e di strutturarli, etichettarli e ottimizzarli utilizzando [!DNL Platform] i servizi. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Mappatura automatica | [!DNL Platform] fornisce raccomandazioni intelligenti per la mappatura automatica durante il flusso di lavoro di assimilazione dei dati, in base a uno schema di destinazione o set di dati selezionato dall&#39;utente. Potete regolare manualmente le regole di mappatura automatica flessibili in base ai casi di utilizzo. |
| Miglioramenti UX | Gli utenti possono accedere alle azioni della tabella in linea per un accesso più semplice alle azioni principali, ad esempio l&#39;aggiunta di dati, la modifica della pianificazione e l&#39;aggiunta di segmenti. Per ulteriori informazioni, consulta il documento [sui flussi di dati](../../sources/tutorials/ui/monitor.md) di monitoraggio. |

Per ulteriori informazioni sulle origini, consultate la panoramica sulle [origini](../../sources/home.md).
