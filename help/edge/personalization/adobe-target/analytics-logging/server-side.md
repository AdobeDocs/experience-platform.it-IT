---
title: Registrazione lato server per i dati A4T in Platform Web SDK
description: Scopri come abilitare la registrazione lato server per Adobe Analytics for Target (A4T) utilizzando l’SDK per web di Experience Platform.
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;piattaforma;registrazione;
source-git-commit: a2214465001f90d19d88c0622c154e7a4ae3bb03
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Registrazione lato server per i dati A4T in Platform Web SDK

Adobe Experience Platform Web SDK consente di implementare la funzionalità Adobe Analytics for Target (A4T) su Platform Edge Network. Quando la registrazione lato server è abilitata, tutti gli hit di Analytics inviati tramite la rete Edge vengono aumentati con i dettagli di Target sul lato server, senza dover passare attraverso il processo di unione degli hit.

La registrazione lato server per Analytics è abilitata quando Analytics è abilitato nella configurazione del datastream:

![Configurazione del datastream di Analytics abilitata](../assets/enable-analytics-datastream.png)

Il diagramma seguente mostra il flusso di dati all’interno del sistema quando la funzione di registrazione Analytics lato server è abilitata:

![Flusso di registrazione lato server](../assets/analytics-server-side-logging.png)

## Passaggi successivi

Questa guida ha trattato la registrazione lato server per i dati A4T nell’SDK per web. Consulta la guida su [registrazione lato client](./client-side.md) per ulteriori informazioni su come gestire i dati A4T sul lato client.
