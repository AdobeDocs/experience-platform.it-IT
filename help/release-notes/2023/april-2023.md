---
title: Note sulla versione di Adobe Experience Platform - Aprile 2023
description: Le note sulla versione di aprile 2023 per Adobe Experience Platform.
source-git-commit: 938b4ba7affadc7ad0eca086d7cc2c9ce1a54a83
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 5%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 26 aprile 2023**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Dashboard](#dashboards)
- [Preparazione dei dati](#data-prep)
- [Experience Data Model](#xdm)
- [Profilo cliente in tempo reale](#profile)
- [Origini](#sources)

## Dashboard {#dashboards}

Adobe Experience Platform offre diverse dashboard attraverso le quali puoi visualizzare informazioni importanti sui dati dell’organizzazione, acquisiti durante le istantanee giornaliere.

**Funzioni nuove o aggiornate** {#dashboards-new-updated-features}

| Funzione | Descrizione |
| --- | --- |
| Dashboard definiti dall&#39;utente | Ora puoi **filtrare i dati storici** dalle informazioni sui widget e utilizza dati recenti o un periodo di analisi personalizzato.<br>È inoltre possibile **duplica i widget esistenti**. Personalizzando un duplicato e modificandone gli attributi, puoi evitare di riavviare dall’inizio la creazione di un nuovo widget univoco. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard, tra cui come concedere autorizzazioni di accesso e creare widget personalizzati, inizia leggendo il [panoramica delle dashboard](../../dashboards/home.md).

## Preparazione dei dati {#data-prep}

Data Prep consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Aggiornamenti al periodo di backfill per Adobe Analytics nelle sandbox non di produzione. | Il periodo di backfill per Adobe Analytics nelle sandbox non di produzione è stato ridotto a tre mesi. Il backfill per le sandbox di produzione rimane invariato a 13 mesi. Questa modifica si applica solo ai nuovi flussi e non influisce sui flussi esistenti. Per ulteriori informazioni, consulta la sezione [Panoramica di Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Nuova funzione di mappatura per convertire le stringhe FPID in ECID | Utilizza la `fpid_to_ecid` funzione per convertire le stringhe FPID in ECID da utilizzare nelle applicazioni Experience Platform e Experience Cloud. Per ulteriori informazioni, consulta la sezione [Guida alle funzioni di preparazione dei dati](../../data-prep/functions.md). |

{style="table-layout:auto"}

Per ulteriori informazioni su Data Prep, consulta la sezione [Panoramica sulla preparazione dei dati](../../data-prep/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Mostra/Nascondi nomi | L’Editor schema ora consente di alternare tra i nomi dei campi originali e i nomi visualizzati più leggibili. Questa flessibilità consente di migliorare la reperibilità dei campi e la modifica degli schemi. I nomi visualizzati per i gruppi di campi standard vengono generati dal sistema, ma possono anche essere personalizzati tramite l’interfaccia utente, se necessario. |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta la sezione [Panoramica del sistema XDM](../../xdm/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di fornire ai clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con Profilo cliente in tempo reale puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, CRM e di terze parti. Il profilo consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account con marca temporale utilizzabile per ogni interazione con il cliente.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Scadenza dati profilo pseudonimi | La scadenza dei dati del profilo pseudonimo è ora disponibile in generale! Questa versione rimuoverà continuamente dall’istanza di Experience Platform i profili pseudonimi non aggiornati una volta abilitati. Per saperne di più su questa funzione e su Profili pseudonimi, si prega di leggere [Guida alla scadenza dei dati di profilo pseudonimo](../../profile/pseudonymous-profiles.md). |

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e consente di strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto API per il filtraggio dei dati a livello di riga per Microsoft Dynamics, Salesforce CRM e il Marketing Cloud Salesforce | Utilizza gli operatori logici e di confronto per filtrare i dati a livello di riga per le origini di Marketing Cloud Microsoft Dynamics, Salesforce CRM e Salesforce. Leggi la guida su [filtraggio dei dati per una sorgente tramite API](../../sources/tutorials/api/filter.md) per ulteriori informazioni. |
| Disponibilità beta dello streaming Shopify | La [Shopify Streaming source](../../sources/connectors/ecommerce/shopify-streaming.md) è ora disponibile in versione beta. Utilizza l’origine Shopify Streaming per inviare ad Experience Platform i dati dall’account Shopify Partners. |
| Disponibilità generale dell&#39;integrazione OneTrust | La [Origine integrazione OneTrust](../../sources/connectors/consent-and-preferences/onetrust.md) è ora GA. Utilizza l&#39;origine di integrazione OneTrust per fornire ad Experience Platform i dati di consenso e preferenze dall&#39;account di integrazione OneTrust. |
| Disponibilità generale di Oracle Service Cloud | La [Origine Oracle Service Cloud](../../sources/connectors/customer-success/oracle-service-cloud.md) è ora GA. Utilizza l’origine Oracle Service Cloud per riportare ad Experience Platform i dati di Oracle Service Cloud . |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, consulta la sezione [panoramica di origini](../../sources/home.md).
