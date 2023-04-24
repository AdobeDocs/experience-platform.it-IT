---
title: Note sulla versione di Adobe Experience Platform - Aprile 2023
description: Le note sulla versione di aprile 2023 per Adobe Experience Platform.
source-git-commit: 9f50ca4b2a4c576af5ce8ee5c085a7603fed2560
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 6%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 26 aprile 2023**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Preparazione dei dati](#data-prep)
- [Origini](#sources)

## Preparazione dei dati {#data-prep}

Data Prep consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Aggiornamenti al periodo di backfill per Adobe Analytics nelle sandbox non di produzione. | Il periodo di backfill per Adobe Analytics nelle sandbox non di produzione è stato ridotto a tre mesi. Il backfill per le sandbox di produzione rimane invariato a 13 mesi. Questa modifica si applica solo ai nuovi flussi e non influisce sui flussi esistenti. Per ulteriori informazioni, consulta la sezione [Panoramica di Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Nuova funzione di mappatura per convertire le stringhe FPID in ECID | Utilizza la `fpid_to_ecid` funzione per convertire le stringhe FPID in ECID da utilizzare nelle applicazioni Experience Platform e Experience Cloud. Per ulteriori informazioni, consulta la sezione [Guida alle funzioni di preparazione dei dati](../../data-prep/functions.md). |

{style="table-layout:auto"}

Per ulteriori informazioni su Data Prep, consulta la sezione [Panoramica sulla preparazione dei dati](../../data-prep/home.md).

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
