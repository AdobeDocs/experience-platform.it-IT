---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica sull'inserimento dello streaming  Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 3f1c3c77a0755a3e305da0fb8a234be0f0ee1863
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 3%

---


# Panoramica sull’assimilazione dello streaming

L&#39;assimilazione dello streaming per  Adobe Experience Platform fornisce agli utenti un metodo per inviare in tempo reale i dati da dispositivi client e server a  Experience Platform.

## Cosa puoi fare con l&#39;assimilazione in streaming?

 Adobe Experience Platform consente di creare esperienze coordinate, coerenti e pertinenti generando un profilo cliente in tempo reale per ogni singolo cliente. L&#39;assimilazione dello streaming svolge un ruolo chiave nella creazione di questi profili consentendo di fornire dati di profilo nel Data Lake con una latenza il più possibile ridotta.

Il seguente video è stato progettato per aiutarti a comprendere meglio l’assimilazione dello streaming e illustra i concetti riportati sopra.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Record del profilo di flusso e ExperienceEvents

Con l’assimilazione in streaming, gli utenti possono trasmettere in streaming ad Platform record di profilo ed ExperienceEvents per facilitarne la personalizzazione in tempo reale. Tutti i dati inviati alle API di assimilazione in streaming vengono automaticamente memorizzati nel Data Lake.

Per ulteriori informazioni, consulta [la guida](../tutorials/create-streaming-connection.md) alla connessione in streaming.

### Flusso a set di dati

Una volta certi che i dati sono puliti, puoi abilitare i set di dati per il profilo cliente e il servizio identità in tempo reale.

Per ulteriori informazioni sull&#39;abilitazione di un set di dati per il servizio Profilo e identità, consulta la guida alla [configurazione di una guida](../../profile/tutorials/dataset-configuration.md)per i set di dati.

## Qual è la latenza prevista per l’assimilazione in streaming su Platform?

| Destinazione | Latenza prevista |
| --------- | ---------------- |
| Profilo del cliente in tempo reale | &lt; 1 minuto |
| Data Lake | &lt; 60 minuti |

## Estensione Adobe Experience Platform

Potete utilizzare l&#39;estensione dell&#39;Adobe Experience Platform  per creare una nuova connessione di streaming. L’estensione Experience Platform  fornisce azioni per inviare beacon formattati in Experience Data Model (XDM) per l’assimilazione in tempo reale  Experience Platform. Per ulteriori informazioni, consulta la [documentazione di Experience Platform Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) .