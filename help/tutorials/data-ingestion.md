---
keywords: ' Experience Platform;home;argomenti popolari'
solution: Experience Platform
title: Esercitazioni sull’inserimento dei dati
topic: tutorial
type: Tutorial
description: L’inserimento dei dati include l’assimilazione batch, l’assimilazione in streaming e l’assimilazione mediante connettori sorgente.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# Assegna dati in [!DNL Experience Platform]

Adobe Experience Platform riunisce i dati provenienti da più origini per aiutare gli addetti al marketing a comprendere meglio il comportamento dei loro clienti.  Adobe [!DNL Experience Platform Data Ingestion] rappresenta i diversi metodi mediante i quali [!DNL Platform] acquisisce i dati da tali origini, nonché il modo in cui tali dati vengono memorizzati all&#39;interno del Data Lake per essere utilizzati da parte di [!DNL Platform services] a valle. [!DNL Data Ingestion] include l’assimilazione batch, l’assimilazione in streaming e l’assimilazione mediante connettori sorgente. Per saperne di più, leggere la [Panoramica sull&#39;inserimento dei dati](../ingestion/home.md) o passare direttamente alla [Documentazione di Origini](../sources/home.md).

## Creare un connettore sorgente nell’interfaccia utente e nell’API

I connettori di origine consentono di acquisire dati da più sorgenti, dove possono essere etichettati, strutturati e migliorati utilizzando [!DNL Platform services]. Per iniziare a creare un connettore di origine, vedere la [panoramica delle origini](../sources/home.md).

## Assegna dati batch

Adobe Experience Platform consente di importare facilmente i dati in [!DNL Platform] come file batch. Esempi di dati da assimilare possono includere dati di profilo da un file semplice in un sistema CRM (ad esempio un file Parquet) o dati conformi a uno schema [!DNL Experience Data Model] (XDM) noto nel Registro di sistema dello schema. Per iniziare, visita [i dati di assimilazione in Esercitazione piattaforma](../ingestion/tutorials/ingest-batch-data.md).

## Mappare un file CSV su uno schema XDM

Per trasferire i dati CSV in Adobe Experience Platform, questi devono essere mappati su uno schema [!DNL Experience Data Model] (XDM). Per i passaggi che mostrano come mappare un file CSV su uno schema XDM utilizzando l&#39;interfaccia utente [!DNL Experience Platform], seguite l&#39; [mappatura di un file CSV su un&#39;esercitazione dello schema XDM](../ingestion/tutorials/map-a-csv-file.md).

## Creare una connessione in streaming

Per avviare lo streaming dei dati su [!DNL Experience Platform], è prima necessario richiedere un endpoint HTTP. Puoi configurare questo endpoint per applicare il comportamento autenticato. Ciò può essere fatto utilizzando l&#39;interfaccia utente [!DNL Platform] o le API [!DNL Experience Platform]. Per saperne di più, segui le esercitazioni per [creare una connessione in streaming utilizzando l&#39;interfaccia utente](../ingestion/tutorials/create-streaming-connection-ui.md) o [creare una connessione in streaming utilizzando le API](../ingestion/tutorials/create-streaming-connection.md).

## Creare una connessione in streaming autenticata

La raccolta dati autenticata consente ai servizi Adobe Experience Platform, ad esempio [!DNL Real-time Customer Profile] e [!DNL Identity], di distinguere tra record provenienti da fonti attendibili e fonti non attendibili. Per iniziare, segui l&#39;esercitazione per [creare una connessione di streaming autenticata](../ingestion/tutorials/create-authenticated-streaming-connection.md).

## Dati del record del flusso e delle serie temporali

Con un set di dati e connessioni a vapore in posizione, è possibile trasmettere in streaming dati di record o serie temporali in [!DNL Platform]. Per iniziare lo streaming dei dati del record, segui i [dati del record del flusso nell&#39;esercitazione della piattaforma](../ingestion/tutorials/streaming-record-data.md). Per iniziare i dati delle serie temporali in streaming, segui i dati delle serie temporali in [streaming in Platform](../ingestion/tutorials/streaming-time-series-data.md).

## Trasmissione di più messaggi in una singola richiesta HTTP

Quando si inviano dati in streaming ad Adobe Experience Platform, effettuare numerose chiamate HTTP può essere costoso. Ad esempio, invece di creare 200 richieste HTTP con payload da 1 KB, è molto più efficiente creare 1 richiesta HTTP con 200 messaggi da 1 KB ciascuno, con un singolo payload di 200 KB. Se utilizzati correttamente, il raggruppamento di più messaggi all&#39;interno di una singola richiesta è un metodo eccellente per ottimizzare i dati inviati a [!DNL Experience Platform]. Per informazioni su come inviare più messaggi a [!DNL Experience Platform] all&#39;interno di una singola richiesta HTTP utilizzando l&#39;assimilazione in streaming, seguire l&#39;esercitazione [invio di più messaggi](../ingestion/tutorials/streaming-multiple-messages.md).



