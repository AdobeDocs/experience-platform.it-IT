---
keywords: Experience Platform;casa;argomenti popolari;kafka;connettore kafka;Kafka;
solution: Experience Platform
title: Connettore Kafka
description: Il connettore di flusso per Adobe Experience Platform si basa su Apache Kafka Connect. Questa libreria può essere utilizzata per lo streaming in tempo reale di eventi JSON da argomenti Kafka nel tuo centro dati direttamente ad Experience Platform.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# [!DNL Kafka] connettore per Adobe Experience Platform

Il connettore di flusso per Adobe Experience Platform è basato su [!DNL Apache Kafka Connect]. Questa libreria può essere utilizzata per lo streaming di eventi JSON da [!DNL Kafka] argomenti nel centro dati direttamente in [!DNL Experience Platform] in tempo reale.

Il connettore di flusso è un connettore di lavello (unidirezionale), che fornisce i dati da [!DNL Kafka] argomenti relativi a un endpoint registrato su [!DNL Experience Platform]. Per utilizzare questo connettore, devi scaricare la libreria e aggiungerla al tuo esistente [!DNL Kafka] distribuzione e configurazione [!DNL Kafka] argomento relativo all’URL HTTP Adobe Streaming. Il codice aggiuntivo è **not** obbligatorio. Il connettore supporta le seguenti funzioni:

- Raccolta di dati autenticata
- Gestione in batch dei messaggi per ridurre le chiamate di rete e aumentare il throughput

Per ulteriori informazioni sulla [!DNL Kafka] il connettore, comprese le istruzioni su come impostare il connettore, leggere il [guida introduttiva](https://github.com/adobe/experience-platform-streaming-connect). Per un flusso di lavoro più dettagliato, leggi la sezione [guida per sviluppatori](https://www.adobe.com/go/kafka-connector-developer-guide).
