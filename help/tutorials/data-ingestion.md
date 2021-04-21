---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Tutorial sull’acquisizione dei dati
topic-legacy: tutorial
type: Tutorial
description: L’acquisizione dei dati include l’acquisizione batch, l’acquisizione in streaming e l’acquisizione tramite i connettori sorgente.
exl-id: 51627acf-e90b-4911-aa54-4a59f3b6a8f9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# Inserire dati in [!DNL Experience Platform]

Adobe Experience Platform riunisce dati provenienti da più sorgenti per aiutare gli esperti di marketing a comprendere meglio il comportamento dei loro clienti. L&#39;Adobe [!DNL Experience Platform Data Ingestion] rappresenta i diversi metodi con cui [!DNL Platform] acquisisce i dati da queste sorgenti, nonché il modo in cui tali dati vengono mantenuti all&#39;interno del Data Lake per l&#39;utilizzo da parte di [!DNL Platform services] a valle. [!DNL Data Ingestion] include l’acquisizione batch, l’acquisizione in streaming e l’acquisizione tramite connettori sorgente. Per ulteriori informazioni, consulta la [Panoramica sull’acquisizione dei dati](../ingestion/home.md) o passa direttamente alla [documentazione sulle sorgenti](../sources/home.md).

## Creare una connessione sorgente nell’interfaccia utente e nell’API

I connettori sorgente consentono di acquisire dati da più sorgenti, dove possono quindi essere etichettati, strutturati e migliorati utilizzando [!DNL Platform services]. Per iniziare a creare un connettore sorgente, consulta la [panoramica origini](../sources/home.md).

## Inserire dati batch

Adobe Experience Platform consente di importare facilmente i dati in [!DNL Platform] come file batch. Esempi di dati da acquisire possono includere dati di profilo provenienti da un file flat in un sistema CRM (ad esempio un file Parquet) o dati conformi a uno schema [!DNL Experience Data Model] (XDM) noto nel Registro di sistema dello schema. Per iniziare, visita l’ [acquisizione di dati nell’esercitazione su Platform](../ingestion/tutorials/ingest-batch-data.md).

## Mappare un file CSV in uno schema XDM

Per acquisire dati CSV in Adobe Experience Platform, è necessario mappare i dati su uno schema [!DNL Experience Data Model] (XDM). Per i passaggi che mostrano come mappare un file CSV su uno schema XDM utilizzando l’ interfaccia utente [!DNL Experience Platform], segui l’ [esercitazione su come mappare un file CSV su uno schema XDM](../ingestion/tutorials/map-a-csv-file.md).

## Creare una connessione in streaming

Per avviare i dati di streaming su [!DNL Experience Platform], è necessario prima richiedere un endpoint HTTP. Puoi configurare questo endpoint per applicare il comportamento autenticato. Questa operazione può essere eseguita utilizzando l’ [!DNL Platform] interfaccia utente o le API [!DNL Experience Platform] . Per ulteriori informazioni, segui le esercitazioni per [creare una connessione in streaming utilizzando l&#39;interfaccia utente](../ingestion/tutorials/create-streaming-connection-ui.md) o [creare una connessione in streaming utilizzando le API](../ingestion/tutorials/create-streaming-connection.md).

## Creare una connessione in streaming autenticata

La raccolta dati autenticata consente ai servizi Adobe Experience Platform, ad esempio [!DNL Real-time Customer Profile] e [!DNL Identity], di distinguere tra record provenienti da fonti attendibili e da fonti non attendibili. Per iniziare, segui l&#39;esercitazione per [creare una connessione in streaming autenticata](../ingestion/tutorials/create-authenticated-streaming-connection.md).

## Dati di registrazione e serie temporali in streaming

Con un set di dati e connessioni a vapore in posizione, è possibile inviare in streaming dati di record o serie temporali in [!DNL Platform]. Per iniziare lo streaming dei dati dei record, segui i [dati dei record di streaming nell’esercitazione Platform](../ingestion/tutorials/streaming-record-data.md). Per iniziare lo streaming dei dati delle serie temporali, seguire i dati delle [serie temporali in Platform](../ingestion/tutorials/streaming-time-series-data.md).

## Trasmetti più messaggi in una singola richiesta HTTP

Quando si inviano dati in streaming a Adobe Experience Platform, effettuare numerose chiamate HTTP può essere costoso. Ad esempio, invece di creare 200 richieste HTTP con payload da 1 KB, è molto più efficiente creare 1 richiesta HTTP con 200 messaggi da 1 KB ciascuno, con un singolo payload di 200 KB. Se utilizzato correttamente, il raggruppamento di più messaggi all’interno di una singola richiesta è un modo eccellente per ottimizzare i dati inviati a [!DNL Experience Platform]. Per informazioni su come inviare più messaggi a [!DNL Experience Platform] all&#39;interno di una singola richiesta HTTP utilizzando l&#39;acquisizione in streaming, segui l&#39; [tutorial sull&#39;invio di più messaggi](../ingestion/tutorials/streaming-multiple-messages.md).
