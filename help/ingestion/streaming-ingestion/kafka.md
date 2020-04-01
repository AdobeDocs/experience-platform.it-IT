---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connettore Kafka
topic: overview
translation-type: tm+mt
source-git-commit: f80b2e1d787d1f8d9fe8ac306422aa7744a69cd3

---


# Connettore Kafka per Adobe Experience Platform

Il connettore di flusso per Adobe Experience Platform si basa su Apache Kafka Connect. Questa libreria può essere utilizzata per lo streaming in tempo reale di eventi JSON da argomenti Kafka nel tuo centro dati direttamente a Experience Platform.

Il connettore di flusso è un connettore di tipo &quot;lavello&quot; (unidirezionale) che fornisce i dati da argomenti Kafka a un endpoint registrato su Experience Platform. Per utilizzare questo connettore, è necessario scaricare la libreria, aggiungerla alla distribuzione Kafka esistente e configurare gli argomenti Kafka all&#39;URL HTTP Adobe Streaming. Il codice aggiuntivo **non** è richiesto. Il connettore supporta le seguenti caratteristiche:

- Raccolta di dati autenticata
- Batch di messaggi per ridurre le chiamate di rete e aumentare il throughput

Per ulteriori informazioni sul connettore Kafka, comprese le istruzioni su come impostare il connettore, consultare la guida [](https://github.com/adobe/experience-platform-streaming-connect)introduttiva. Per un flusso di lavoro più dettagliato, consultate la guida [](https://github.com/adobe/experience-platform-streaming-connect/blob/master/DEVELOPER_GUIDE.md)per gli sviluppatori.