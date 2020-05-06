---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Esercitazioni sull’inserimento dei dati
topic: tutorial
translation-type: tm+mt
source-git-commit: 0eecd802fc8d0ace3a445f3f188a7f095b97d0c8
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# Caricamento di dati in Experience Platform

Adobe Experience Platform riunisce i dati provenienti da più origini per aiutare gli esperti di marketing a comprendere meglio il comportamento dei loro clienti. L&#39;inserimento dei dati in Adobe Experience Platform rappresenta i diversi metodi mediante i quali la piattaforma acquisisce i dati da tali origini, nonché il modo in cui tali dati vengono memorizzati all&#39;interno del Data Lake per essere utilizzati dai servizi della piattaforma a valle. L’inserimento dei dati include l’assimilazione batch, l’assimilazione in streaming e l’assimilazione mediante connettori sorgente. Per saperne di più, leggi la panoramica [sull&#39;inserimento dei](../ingestion/home.md) dati o procedi direttamente alla documentazione [](../sources/home.md)Origini.

## Creare un connettore sorgente nell’interfaccia utente e nell’API

I connettori di origine consentono di acquisire dati da più origini, dove possono essere etichettati, strutturati e migliorati utilizzando i servizi della piattaforma. Per iniziare a creare un connettore di origine, vedere la panoramica [delle](../sources/home.md)origini.

## Assegna dati batch

Adobe Experience Platform consente di importare facilmente i dati in piattaforma come file batch. Esempi di dati da assimilare possono includere dati di profilo da un file semplice in un sistema CRM (ad esempio un file parquet) o dati conformi a uno schema XDM (Experience Data Model) noto nel Registro di sistema dello schema. Per iniziare, visita i dati di [inserimento nell’esercitazione](../ingestion/tutorials/ingest-batch-data.md)sulla piattaforma.

## Mappare un file CSV su uno schema XDM

Per assimilare i dati CSV in Adobe Experience Platform, questi devono essere mappati su uno schema Experience Data Model (XDM). Per i passaggi che mostrano come mappare un file CSV su uno schema XDM mediante l’interfaccia utente della piattaforma Experience, seguite l’esercitazione [sullo schema XDM](../ingestion/tutorials/map-a-csv-file.md)mappata su un file CSV.

## Creare una connessione in streaming

Per avviare lo streaming dei dati in Experience Platform, devi prima richiedere un endpoint HTTP. Puoi configurare questo endpoint per applicare il comportamento autenticato. Questo può essere fatto utilizzando l&#39;interfaccia utente della piattaforma o le API della piattaforma Experience. Per saperne di più, seguite le esercitazioni per [creare una connessione in streaming utilizzando l&#39;interfaccia utente](../ingestion/tutorials/create-streaming-connection-ui.md) o [creando una connessione in streaming mediante le API](../ingestion/tutorials/create-streaming-connection.md).

## Creare una connessione in streaming autenticata

La raccolta dei dati autenticata consente ai servizi Adobe Experience Platform, come Profilo cliente e Identità in tempo reale, di distinguere tra record provenienti da fonti attendibili e fonti non attendibili. Per iniziare, segui l’esercitazione per [creare una connessione](../ingestion/tutorials/create-authenticated-streaming-connection.md)in streaming autenticata.

## Dati del record del flusso e delle serie temporali

Con un set di dati e connessioni a vapore in posizione, è possibile trasmettere in streaming dati di record o serie temporali in Platform. Per iniziare lo streaming dei dati dei record, segui i dati dei record [di flusso nell&#39;esercitazione](../ingestion/tutorials/streaming-record-data.md)della piattaforma. Per iniziare i dati delle serie temporali in streaming, segui i dati delle serie temporali in [streaming in Piattaforma](../ingestion/tutorials/streaming-time-series-data.md).

## Trasmissione di più messaggi in una singola richiesta HTTP

Durante lo streaming dei dati in Adobe Experience Platform, effettuare numerose chiamate HTTP può essere costoso. Ad esempio, invece di creare 200 richieste HTTP con payload da 1 KB, è molto più efficiente creare 1 richiesta HTTP con 200 messaggi da 1 KB ciascuno, con un singolo payload di 200 KB. Se utilizzati correttamente, il raggruppamento di più messaggi all’interno di una singola richiesta è un metodo eccellente per ottimizzare i dati inviati a Experience Platform. Per informazioni su come inviare più messaggi a Experience Platform all’interno di una singola richiesta HTTP utilizzando l’assimilazione in streaming, segui l’esercitazione [sull’](../ingestion/tutorials/streaming-multiple-messages.md)invio di più messaggi.



