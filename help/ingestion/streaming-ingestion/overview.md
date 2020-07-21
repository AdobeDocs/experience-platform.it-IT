---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica sull'inserimento dello streaming  Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 3%

---


# Panoramica sull’assimilazione dello streaming

L&#39;assimilazione dello streaming per  Adobe Experience Platform fornisce agli utenti un metodo per inviare i dati dai dispositivi client e server [!DNL Experience Platform] in tempo reale.

## Cosa puoi fare con l&#39;assimilazione in streaming?

 Adobe Experience Platform consente di creare esperienze coordinate, coerenti e pertinenti generando un [!DNL Real-time Customer Profile] rapporto per ogni singolo cliente. L’assimilazione dello streaming svolge un ruolo chiave nella creazione di questi profili consentendo di inviare [!DNL Profile] i dati al [!DNL Data Lake] pubblico con una latenza il più possibile ridotta.

Il seguente video è stato progettato per aiutarti a comprendere meglio l’assimilazione dello streaming e illustra i concetti riportati sopra.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Record del profilo di flusso e [!DNL ExperienceEvents]

Con l’assimilazione in streaming, gli utenti possono trasmettere in streaming i record dei profili e [!DNL ExperienceEvents] in [!DNL Platform] pochi secondi per promuovere la personalizzazione in tempo reale. Tutti i dati inviati alle API di assimilazione in streaming vengono automaticamente memorizzati nella cartella [!DNL Data Lake].

Per ulteriori informazioni, consulta [la guida](../tutorials/create-streaming-connection.md) alla connessione in streaming.

### Flusso a set di dati

Una volta certi che i dati sono puliti, potete abilitare i set di dati per [!DNL Real-time Customer Profile] e [!DNL Identity Service].

Per ulteriori informazioni sull&#39;abilitazione di un dataset per [!DNL Profile] e [!DNL Identity Service], leggere la guida alla [configurazione di un dataset](../../profile/tutorials/dataset-configuration.md).

## What is the expected latency for streaming ingestion on [!DNL Platform]?

| Destinazione | Latenza prevista |
| --------- | ---------------- |
| Profilo del cliente in tempo reale | &lt; 1 minuto |
| Data Lake | &lt; 60 minuti |

## Estensione Adobe Experience Platform

Potete utilizzare l&#39;estensione dell&#39;Adobe Experience Platform  per creare una nuova connessione di streaming. L&#39; [!DNL Experience Platform] estensione fornisce azioni per inviare beacon formattati in [!DNL Experience Data Model] (XDM) per l&#39;assimilazione in tempo reale a [!DNL Experience Platform]. Per ulteriori informazioni, consulta la [documentazione di Experience Platform Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) .