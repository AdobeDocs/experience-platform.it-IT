---
title: Registrazione lato server per i dati A4T in Platform Web SDK
description: Scopri come abilitare la registrazione lato server per Adobe Analytics for Target (A4T) utilizzando l’SDK web di Experience Platform.
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;platform;logging;
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 1%

---

# Registrazione lato server per i dati A4T in Platform Web SDK

Adobe Experience Platform Web SDK consente di implementare la funzionalità Adobe Analytics for Target (A4T) sull’Edge Network della piattaforma. Quando la registrazione lato server è abilitata, tutti gli hit di Analytics inviati tramite l’Edge Network vengono potenziati con i dettagli di Target sul lato server, senza dover passare attraverso la procedura di unione degli hit.

La registrazione lato server per Analytics è abilitata quando Analytics è abilitato nella configurazione dello stream di dati:

![Configurazione dello stream di dati di Analytics abilitata](../assets/enable-analytics-datastream.png)

Il diagramma seguente mostra il flusso dei dati nel sistema quando è abilitata la registrazione Analytics lato server:

![Flusso di registrazione lato server](../assets/analytics-server-side-logging.png)

## Passaggi successivi

Questa guida tratta la registrazione lato server per i dati A4T nell’SDK per web. Per ulteriori informazioni su come gestire i dati A4T sul lato client, consulta la guida alla [registrazione lato client](./client-side.md).
