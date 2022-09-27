---
title: Note sulla versione di Adobe Experience Platform - Settembre 2022
description: Note sulla versione di settembre 2022 per Adobe Experience Platform.
source-git-commit: 1890bd9dbce6a217951c28fc2fb3fec2634e714d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 7%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 28 settembre 2022**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Servizio Identity](#identity-service)
- [Origini](#sources)

## Servizio Identity {#identity-service}

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Ciò è reso più difficile quando i dati dei clienti sono frammentati in diversi sistemi, il che fa sì che ogni cliente sembri avere più &quot;identità&quot;.

Il servizio Adobe Experience Platform Identity consente di acquisire una visione migliore del cliente e del suo comportamento collegando le identità tra dispositivi e sistemi, consentendoti di fornire in tempo reale esperienze digitali personali di impatto.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per l’eliminazione dei set di dati | Il servizio Identity supporta ora l’eliminazione dei set di dati durante la richiesta tramite [API del servizio catalogo](https://developer.adobe.com/experience-platform-apis/references/catalog/), l’interfaccia utente o l’igiene dei dati. Leggi la guida su [eliminazione di set di dati nell’interfaccia utente](../../catalog/datasets/user-guide.md#delete-a-dataset) per ulteriori informazioni. |

Per ulteriori informazioni sul servizio Identity, consulta la sezione [Panoramica del servizio Identity](../../identity-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Audience Manager dell’impatto sulla popolazione del segmento sul profilo cliente in tempo reale | L’acquisizione di popolazioni di segmenti di Audience Manager di grandi dimensioni ha un impatto diretto sul conteggio totale dei profili quando invii per la prima volta un segmento di Audience Manager a Platform utilizzando l’origine di Audience Manager. Ciò significa che la selezione di tutti i segmenti può potenzialmente portare a un conteggio di profili superiore all’adesione all’utilizzo della licenza. Per ulteriori informazioni, consulta la sezione [Panoramica di Audience Manager Source](../../sources/connectors/adobe-applications/audience-manager.md). Per informazioni sull&#39;utilizzo della licenza, consulta la documentazione su [utilizzo del dashboard di utilizzo della licenza](../../dashboards/guides/license-usage.md). |

Per ulteriori informazioni sulle origini, consulta la sezione [panoramica di origini](../../sources/home.md).