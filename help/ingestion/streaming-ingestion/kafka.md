---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connettore Kafka
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# [!DNL Kafka] connettore per  Adobe Experience Platform

Il connettore del flusso per  Adobe Experience Platform è basato su [!DNL Apache Kafka Connect]. Questa libreria può essere utilizzata per lo streaming di eventi JSON da [!DNL Kafka] argomenti nel centro dati direttamente a [!DNL Experience Platform] in tempo reale.

Il connettore di flusso è un connettore di tipo &quot;lavello&quot; (unidirezionale) che fornisce dati da [!DNL Kafka] topic a un endpoint registrato su [!DNL Experience Platform]. Per utilizzare questo connettore, è necessario scaricare la libreria, aggiungerla alla [!DNL Kafka] distribuzione esistente e configurare gli [!DNL Kafka] argomenti nell&#39;URL Adobe Streaming HTTP. Il codice aggiuntivo **non** è richiesto. Il connettore supporta le seguenti caratteristiche:

- Raccolta di dati autenticata
- Batch di messaggi per ridurre le chiamate di rete e aumentare il throughput

Per ulteriori informazioni sul [!DNL Kafka] connettore, comprese le istruzioni su come impostare il connettore, consultare la guida [](https://github.com/adobe/experience-platform-streaming-connect)introduttiva. Per un flusso di lavoro più dettagliato, consultate la guida [](https://github.com/adobe/experience-platform-streaming-connect/blob/master/DEVELOPER_GUIDE.md)per gli sviluppatori.