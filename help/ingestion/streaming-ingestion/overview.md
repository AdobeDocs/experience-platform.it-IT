---
keywords: ' Experience Platform;home;popolari argomenti;assimilazione dei dati;assimilazione dei dati;streaming;panoramica;assimilazione in streaming;latenza;latenza in streaming;'
solution: Experience Platform
title: Panoramica di Adobe Experience Platform Streaming Ingestion
topic: overview
description: L'assimilazione dello streaming per Adobe Experience Platform fornisce agli utenti un metodo per inviare in tempo reale i dati dai dispositivi client e server al Experience Platform .
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 3%

---


# Panoramica sull’assimilazione dello streaming

L&#39;assimilazione dello streaming per Adobe Experience Platform fornisce agli utenti un metodo per inviare in tempo reale dati da dispositivi client e server a [!DNL Experience Platform].

## Cosa puoi fare con l&#39;assimilazione in streaming?

Adobe Experience Platform consente di creare esperienze coordinate, coerenti e pertinenti generando un [!DNL Real-time Customer Profile] per ogni singolo cliente. L&#39;assimilazione dello streaming svolge un ruolo chiave nella creazione di questi profili, consentendo di fornire [!DNL Profile] dati in [!DNL Data Lake] con la massima latenza possibile.

Il seguente video è stato progettato per aiutarti a comprendere meglio l’assimilazione dello streaming e illustra i concetti riportati sopra.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Record del profilo di flusso e [!DNL ExperienceEvents]

Con l&#39;assimilazione in streaming, gli utenti possono trasmettere in streaming i record dei profili e da [!DNL ExperienceEvents] a [!DNL Platform] in secondi per contribuire alla personalizzazione in tempo reale. Tutti i dati inviati alle API di assimilazione in streaming vengono automaticamente memorizzati in [!DNL Data Lake].

Per ulteriori informazioni, leggere la [creazione di una guida alla connessione in streaming](../tutorials/create-streaming-connection.md).

### Flusso a set di dati

Una volta certi che i dati sono puliti, è possibile abilitare i set di dati per [!DNL Real-time Customer Profile] e [!DNL Identity Service].

Per ulteriori informazioni sull&#39;abilitazione di un dataset per [!DNL Profile] e [!DNL Identity Service], leggere la [configurazione di una guida per i dataset](../../profile/tutorials/dataset-configuration.md).

## Qual è la latenza prevista per l&#39;assimilazione in streaming su [!DNL Platform]?

| Destinazione | Latenza prevista |
| --------- | ---------------- |
| Profilo cliente in tempo reale | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| Data Lake | &lt; 60 minuti |

## Estensione Adobe Experience Platform

Potete utilizzare l&#39;estensione Adobe Experience Platform per creare una nuova connessione di streaming. L&#39;estensione [!DNL Experience Platform] fornisce azioni per inviare beacon formattati in [!DNL Experience Data Model] (XDM) per l&#39;inserimento in tempo reale in [!DNL Experience Platform]. Per ulteriori informazioni, visitare la documentazione relativa all&#39;estensione del Experience Platform [](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html).