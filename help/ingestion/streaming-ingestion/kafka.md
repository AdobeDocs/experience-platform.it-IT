---
keywords: Experience Platform;casa;argomenti popolari;kafka;connettore kafka;Kafka;
solution: Experience Platform
title: Connettore Kafka
topic-legacy: overview
description: Il connettore di flusso per Adobe Experience Platform si basa su Apache Kafka Connect. Questa libreria può essere utilizzata per lo streaming in tempo reale di eventi JSON da argomenti Kafka nel tuo centro dati direttamente ad Experience Platform.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# [!DNL Kafka] connettore per Adobe Experience Platform

Il connettore di flusso per Adobe Experience Platform si basa su [!DNL Apache Kafka Connect]. Questa libreria può essere utilizzata per lo streaming in tempo reale di eventi JSON da [!DNL Kafka] argomenti nel datacenter direttamente a [!DNL Experience Platform].

Il connettore di flusso è un connettore lavello (unidirezionale) che fornisce dati da [!DNL Kafka] argomenti a un endpoint registrato su [!DNL Experience Platform]. Per utilizzare questo connettore, devi scaricare la libreria, aggiungerla alla distribuzione [!DNL Kafka] esistente e configurare gli argomenti [!DNL Kafka] nell’URL HTTP Adobe Streaming. Il codice aggiuntivo è **non** obbligatorio. Il connettore supporta le seguenti funzioni:

- Raccolta di dati autenticata
- Gestione in batch dei messaggi per ridurre le chiamate di rete e aumentare il throughput

Per ulteriori informazioni sul connettore [!DNL Kafka], comprese le istruzioni su come impostare il connettore, consulta la [guida introduttiva](https://github.com/adobe/experience-platform-streaming-connect). Per un flusso di lavoro più dettagliato, consulta la [guida per gli sviluppatori](https://www.adobe.com/go/kafka-connector-developer-guide).
