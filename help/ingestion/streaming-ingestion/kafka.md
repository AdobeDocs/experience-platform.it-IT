---
keywords: ' Experience Platform;home;argomenti popolari;kafka;kafka connettore;Kafka;'
solution: Experience Platform
title: Connettore Kafka
topic: overview
description: Il connettore del flusso per Adobe Experience Platform si basa su Apache Kafka Connect. Questa libreria può essere utilizzata per lo streaming di eventi JSON da argomenti Kafka nel tuo centro dati direttamente  Experience Platform in tempo reale.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# [!DNL Kafka] connettore per Adobe Experience Platform

Il connettore di flusso per Adobe Experience Platform è basato su [!DNL Apache Kafka Connect]. Questa libreria può essere utilizzata per lo streaming in tempo reale di eventi JSON da [!DNL Kafka] argomenti nel datacenter direttamente a [!DNL Experience Platform].

Il connettore di flusso è un connettore di tipo &quot;lavandino&quot; (unidirezionale) che fornisce i dati da [!DNL Kafka] argomenti a un endpoint registrato su [!DNL Experience Platform]. Per utilizzare questo connettore, è necessario scaricare la libreria, aggiungerla alla distribuzione [!DNL Kafka] esistente e configurare gli argomenti [!DNL Kafka] nell&#39;URL HTTP  Adobe Streaming. Il codice aggiuntivo è **not** obbligatorio. Il connettore supporta le seguenti caratteristiche:

- Raccolta di dati autenticata
- Batch di messaggi per ridurre le chiamate di rete e aumentare il throughput

Per ulteriori informazioni sul [!DNL Kafka] connettore, comprese le istruzioni sulla configurazione del connettore, consultare la [guida introduttiva](https://github.com/adobe/experience-platform-streaming-connect). Per un flusso di lavoro più dettagliato, leggete la [guida per gli sviluppatori](https://www.adobe.com/go/kafka-connector-developer-guide).