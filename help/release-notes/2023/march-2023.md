---
title: Note sulla versione di Adobe Experience Platform - Febbraio 2023
description: Note sulla versione di marzo 2023 per Adobe Experience Platform.
source-git-commit: 44075e38664c01c64e7d09f5856353bff64becb5
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 5%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 29 marzo 2023**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Raccolta dati](#data-collection)
- [Preparazione dei dati](#data-prep)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che ti consentono di raccogliere i dati sull’esperienza del cliente lato client e inviarli ad Adobe Experience Platform Edge Network dove possono essere arricchiti, trasformati e distribuiti su destinazioni Adobi o non Adobi.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuovo flusso di lavoro di avvio rapido per l’API Meta Conversioni (Beta) | Accedi ai nuovi flussi di lavoro di avvio rapido in &quot;Guida introduttiva&quot; dalla schermata iniziale Raccolta dati. La [flusso di lavoro di avvio rapido per l’API Meta Conversions](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) consente ai clienti di raccogliere e inoltrare rapidamente i dati evento, lato server a Meta per le conversioni di annunci in pochi semplici passaggi. |
| [!DNL Braze] estensione di inoltro eventi | La [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) l’estensione di inoltro eventi consente di sfruttare i dati acquisiti in Adobe Experience Platform Edge Network e inviarli a [!DNL Braze] sotto forma di eventi lato server che utilizzano [!DNL Braze] API di tracciamento utente. |
| [!DNL Mixpanel] estensione di inoltro eventi | La [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) L’estensione consente ai clienti di sfruttare l’inoltro eventi per acquisire informazioni sull’evento in Adobe Experience Platform Edge Network e inviarle a Mixpanel utilizzando l’API Track Events. |

{style="table-layout:auto"}

## Preparazione dei dati {#data-prep}

Data Prep consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuove funzioni per la codifica e la decodifica delle stringhe URL | <ul><li>La `get_url_encoded` prende un URL come input e sostituisce o codifica caratteri speciali con caratteri ASCII.</li><li>La `get_url_decoded` prende un URL come input e decodifica i caratteri ASCII in caratteri speciali.</li></ul> Per ulteriori informazioni, consulta la sezione [Guida alle funzioni di preparazione dei dati](../../data-prep/functions.md). Per un elenco completo dei caratteri riservati e dei corrispondenti caratteri codificati, consulta la guida in [caratteri speciali](../../data-prep/functions.md#special-characters). |

Per ulteriori informazioni su Data Prep, consulta la sezione [Panoramica sulla preparazione dei dati](../../data-prep/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all’interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Metriche del profilo | Per ottenere una rappresentazione più accurata delle metriche di profilo, la suddivisione dei membri e le metriche di abbandono vengono combinate e ora vengono calcolate in un periodo di 24 ore. Ulteriori informazioni disponibili in [Guida all’interfaccia utente di segmentazione](../../segmentation/ui/overview.md) |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Segmentation Service], vedi [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e consente di strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Disponibilità beta [!DNL Chatlio] | La [!DNL Chatlio] la sorgente è ora disponibile in versione beta. Utilizza la [!DNL Chatlio] origine per lo streaming [!DNL Chatlio] dati degli eventi ad Experience Platform. Per ulteriori informazioni, consulta la sezione [[!DNL Chatlio] panoramica](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Disponibilità beta [!DNL Customer.io] | La [!DNL Customer.io] la sorgente è ora disponibile in versione beta. Utilizza la [!DNL Customer.io] origine per lo streaming ad Experience Platform dei dati degli eventi cliente. Per ulteriori informazioni, consulta la sezione [[!DNL Customer.io] panoramica](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Disponibilità beta [!DNL Pendo] | La [!DNL Pendo] la sorgente è ora disponibile in versione beta. Utilizza la [!DNL Pendo] per lo streaming ad Experience Platform dei dati di analisi dei prodotti. Per ulteriori informazioni, consulta la sezione [[!DNL Pendo] panoramica](../../sources/connectors/analytics/pendo-webhook.md). |
| Supporto per i flussi di dati bozze | Ora puoi utilizzare l’API del servizio di flusso per impostare i flussi di dati su uno stato bozza. I flussi di dati elaborati possono essere successivamente aggiornati e pubblicati con nuove informazioni. Per ulteriori informazioni, consulta la guida su [impostazione dei flussi di dati di origine come bozze](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, consulta la sezione [panoramica di origini](../../sources/home.md).
