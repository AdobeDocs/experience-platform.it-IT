---
keywords: Experience Platform;home;argomenti popolari;inserimento dati;dati acquisiti;streaming;panoramica;acquisizione streaming;latenza;latenza streaming;
solution: Experience Platform
title: Panoramica dell’acquisizione in streaming
topic-legacy: overview
description: L’acquisizione in streaming per Adobe Experience Platform fornisce agli utenti un metodo per inviare in tempo reale dati da dispositivi lato client e lato server ad Experience Platform.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 3%

---

# Panoramica sull’acquisizione in streaming

L’acquisizione in streaming per Adobe Experience Platform fornisce agli utenti un metodo per inviare in tempo reale dati da dispositivi lato client e lato server a [!DNL Experience Platform] .

## Cosa puoi fare con l’acquisizione in streaming?

Adobe Experience Platform consente di gestire esperienze coordinate, coerenti e rilevanti generando un [!DNL Real-time Customer Profile] per ogni singolo cliente. L’acquisizione in streaming svolge un ruolo chiave nella creazione di questi profili e consente di fornire i dati [!DNL Profile] in [!DNL Data Lake] con la minima latenza possibile.

Il video seguente è stato progettato per aiutarti a comprendere lo streaming ingestion e illustra i concetti illustrati sopra.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Registra record di profilo e [!DNL ExperienceEvents]

Con l’acquisizione in streaming, gli utenti possono inviare in streaming record di profilo e da [!DNL ExperienceEvents] a [!DNL Platform] in pochi secondi per favorire la personalizzazione in tempo reale. Tutti i dati inviati alle API di acquisizione in streaming vengono mantenuti automaticamente in [!DNL Data Lake].

Per ulteriori informazioni, leggi la [creazione di una guida alla connessione in streaming](../tutorials/create-streaming-connection.md) .

### Trasmetti ai set di dati

Una volta certi che i dati sono puliti, puoi abilitare i set di dati per [!DNL Real-time Customer Profile] e [!DNL Identity Service].

Per ulteriori informazioni sull&#39;abilitazione di un set di dati per [!DNL Profile] e [!DNL Identity Service], consulta la [configurazione di una guida ai set di dati](../../profile/tutorials/dataset-configuration.md).

## Qual è la latenza prevista per l’acquisizione in streaming su [!DNL Platform]?

| Destinazione | Latenza prevista |
| --------- | ---------------- |
| Profilo cliente in tempo reale | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| Lago dati | &lt; 60 minuti |

## Estensione Adobe Experience Platform

Puoi utilizzare l’estensione Adobe Experience Platform per creare una nuova connessione in streaming. L&#39;estensione [!DNL Experience Platform] fornisce azioni per inviare beacon formattati in [!DNL Experience Data Model] (XDM) per l&#39;acquisizione in tempo reale a [!DNL Experience Platform]. Per ulteriori informazioni, visita la documentazione [Estensione Experience Platform](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) .
