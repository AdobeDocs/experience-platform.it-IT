---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Esercitazioni sull’inserimento dei dati
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---


# Assegna dati a [!DNL Experience Platform]

 Adobe Experience Platform riunisce i dati provenienti da più origini per aiutare gli addetti al marketing a comprendere meglio il comportamento dei loro clienti. Adobe [!DNL Experience Platform Data Ingestion] rappresenta i diversi metodi mediante i quali [!DNL Platform] vengono acquisiti i dati da tali origini, nonché il modo in cui tali dati vengono memorizzati all&#39;interno del Data Lake per l&#39;utilizzo da parte di Data Lake [!DNL Platform services]. [!DNL Data Ingestion] include l’assimilazione batch, l’assimilazione in streaming e l’assimilazione mediante connettori sorgente. Per saperne di più, leggi la panoramica [sull&#39;inserimento dei](../ingestion/home.md) dati o procedi direttamente alla documentazione [](../sources/home.md)Origini.

## Creare un connettore sorgente nell’interfaccia utente e nell’API

I connettori di origine consentono di acquisire dati da più sorgenti, dove possono essere etichettati, strutturati e ottimizzati utilizzando [!DNL Platform services]. Per iniziare a creare un connettore di origine, vedere la panoramica [delle](../sources/home.md)origini.

## Assegna dati batch

 Adobe Experience Platform consente di importare facilmente i dati in [!DNL Platform] file batch. Esempi di dati da assimilare possono includere dati di profilo da un file semplice in un sistema CRM (ad esempio un file parquet) o dati conformi a uno schema [!DNL Experience Data Model] (XDM) noto nel Registro di sistema dello schema. Per iniziare, visita l’esercitazione [Platform dedicata ai dati](../ingestion/tutorials/ingest-batch-data.md)di assimilazione.

## Mappare un file CSV su uno schema XDM

Per assimilare i dati CSV in  Adobe Experience Platform, i dati devono essere mappati su uno schema [!DNL Experience Data Model] (XDM). Per i passaggi che mostrano come mappare un file CSV su uno schema XDM utilizzando l&#39;interfaccia [!DNL Experience Platform] utente, seguite l&#39;esercitazione [di](../ingestion/tutorials/map-a-csv-file.md)mappatura di un file CSV su uno schema XDM.

## Creare una connessione in streaming

Per avviare lo streaming dei dati su [!DNL Experience Platform], è innanzitutto necessario richiedere un endpoint HTTP. Puoi configurare questo endpoint per applicare il comportamento autenticato. Questo può essere fatto utilizzando l&#39;interfaccia [!DNL Platform] utente o [!DNL Experience Platform] le API. Per saperne di più, seguite le esercitazioni per [creare una connessione in streaming utilizzando l&#39;interfaccia utente](../ingestion/tutorials/create-streaming-connection-ui.md) o [creando una connessione in streaming mediante le API](../ingestion/tutorials/create-streaming-connection.md).

## Creare una connessione in streaming autenticata

La raccolta dati autenticata consente  servizi di Adobe Experience Platform, come [!DNL Real-time Customer Profile] e [!DNL Identity], di distinguere tra record provenienti da fonti attendibili e fonti non attendibili. Per iniziare, segui l’esercitazione per [creare una connessione](../ingestion/tutorials/create-authenticated-streaming-connection.md)in streaming autenticata.

## Dati del record del flusso e delle serie temporali

Con un set di dati e connessioni a vapore in posizione, è possibile trasmettere in streaming dati di record o serie temporali in [!DNL Platform]. Per iniziare lo streaming dei dati del record, segui i dati del record del [flusso nell&#39;esercitazione](../ingestion/tutorials/streaming-record-data.md)Platform. Per iniziare i dati delle serie temporali in streaming, segui i dati delle serie temporali in [streaming in Platform](../ingestion/tutorials/streaming-time-series-data.md).

## Trasmissione di più messaggi in una singola richiesta HTTP

Durante lo streaming dei dati  Adobe Experience Platform, effettuare numerose chiamate HTTP può essere costoso. Ad esempio, invece di creare 200 richieste HTTP con payload da 1 KB, è molto più efficiente creare 1 richiesta HTTP con 200 messaggi da 1 KB ciascuno, con un singolo payload di 200 KB. Se utilizzati correttamente, il raggruppamento di più messaggi all’interno di una singola richiesta è un metodo eccellente per ottimizzare i dati a cui si sta inviando [!DNL Experience Platform]. Per informazioni su come inviare più messaggi all’ [!DNL Experience Platform] interno di una singola richiesta HTTP utilizzando l’assimilazione in streaming, segui l’esercitazione [sull’](../ingestion/tutorials/streaming-multiple-messages.md)invio di più messaggi.



