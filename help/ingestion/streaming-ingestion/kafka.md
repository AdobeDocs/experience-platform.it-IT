---
keywords: Experience Platform;home;argomenti popolari;kafka;connettore kafka;Kafka;
solution: Experience Platform
title: Connettore Kafka
description: Il connettore di flusso per Adobe Experience Platform è basato su Apache Kafka Connect. Questa libreria può essere utilizzata per inviare in streaming gli eventi JSON dagli argomenti Kafka nel centro dati direttamente agli Experienci Platform in tempo reale.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# Connettore [!DNL Kafka] per Adobe Experience Platform

Il connettore di flusso per Adobe Experience Platform è basato su [!DNL Apache Kafka Connect]. Questa libreria può essere utilizzata per inviare eventi JSON da [!DNL Kafka] argomenti nel centro dati direttamente a [!DNL Experience Platform] in tempo reale.

Il connettore di flusso è un connettore sink (unidirezionale) che fornisce dati da [!DNL Kafka] argomenti a un endpoint registrato su [!DNL Experience Platform]. Per utilizzare questo connettore, è necessario scaricare la libreria, aggiungerla alla distribuzione [!DNL Kafka] esistente e configurare gli argomenti [!DNL Kafka] nell&#39;URL HTTP di streaming Adobe. Il codice aggiuntivo è **non** richiesto. Il connettore supporta le seguenti funzionalità:

- Raccolta autenticata dei dati
- Creazione di batch di messaggi per ridurre le chiamate di rete e aumentare la velocità effettiva

Per ulteriori informazioni sul connettore [!DNL Kafka], incluse le istruzioni sulla configurazione del connettore, leggere la [guida introduttiva](https://github.com/adobe/experience-platform-streaming-connect). Per un flusso di lavoro più dettagliato, leggere la [guida per gli sviluppatori](https://www.adobe.com/go/kafka-connector-developer-guide).
