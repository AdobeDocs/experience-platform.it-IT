---
keywords: Experience Platform;home;argomenti popolari;kafka;connettore kafka;Kafka;
solution: Experience Platform
title: Connettore Kafka
description: Il connettore di flusso per Adobe Experience Platform è basato su Apache Kafka Connect. Questa libreria può essere utilizzata per inviare in streaming gli eventi JSON dagli argomenti Kafka nel centro dati direttamente agli Experienci Platform in tempo reale.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# [!DNL Kafka] connettore per Adobe Experience Platform

Il connettore di flusso per Adobe Experience Platform si basa su [!DNL Apache Kafka Connect]. Questa libreria può essere utilizzata per inviare in streaming eventi JSON da [!DNL Kafka] argomenti nel centro dati direttamente in [!DNL Experience Platform] in tempo reale.

Il connettore di flusso è un connettore sink (unidirezionale) che fornisce dati da [!DNL Kafka] argomenti di un endpoint registrato su [!DNL Experience Platform]. Per utilizzare questo connettore, devi scaricare la libreria e aggiungerla al tuo [!DNL Kafka] e configurare [!DNL Kafka] argomenti dell&#39;URL HTTP di streaming Adobe. Il codice aggiuntivo è **non** obbligatorio. Il connettore supporta le seguenti funzionalità:

- Raccolta autenticata dei dati
- Creazione di batch di messaggi per ridurre le chiamate di rete e aumentare la velocità effettiva

Per ulteriori informazioni su [!DNL Kafka] , incluse le istruzioni per la configurazione del connettore, leggere [guida introduttiva](https://github.com/adobe/experience-platform-streaming-connect). Per informazioni più dettagliate, leggere [guida per sviluppatori](https://www.adobe.com/go/kafka-connector-developer-guide).
