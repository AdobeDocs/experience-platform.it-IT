---
keywords: Experience Platform;home;argomenti popolari;inserimento dati;dati acquisiti;streaming;panoramica;acquisizione streaming;latenza;latenza streaming;
solution: Experience Platform
title: Panoramica dell’acquisizione in streaming
topic-legacy: overview
description: L’acquisizione in streaming per Adobe Experience Platform fornisce agli utenti un metodo per inviare in tempo reale dati da dispositivi lato client e lato server ad Experience Platform.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 3%

---

# Panoramica sull’acquisizione in streaming

L’acquisizione in streaming per Adobe Experience Platform fornisce agli utenti un metodo per inviare dati da dispositivi lato client e lato server a [!DNL Experience Platform] in tempo reale.

## Cosa puoi fare con l’acquisizione in streaming?

Adobe Experience Platform consente di gestire esperienze coordinate, coerenti e rilevanti generando un [!DNL Real-Time Customer Profile] per ogni singolo cliente. L’acquisizione in streaming svolge un ruolo chiave nella creazione di questi profili e consente di [!DNL Profile] i dati [!DNL Data Lake] con una latenza minima possibile.

Il video seguente è stato progettato per aiutarti a comprendere lo streaming ingestion e illustra i concetti illustrati sopra.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Registri del profilo di flusso e [!DNL ExperienceEvents]

Con l’acquisizione in streaming, gli utenti possono inviare in streaming record di profilo e [!DNL ExperienceEvents] a [!DNL Platform] in pochi secondi per favorire la personalizzazione in tempo reale. Tutti i dati inviati alle API di acquisizione in streaming vengono automaticamente memorizzati nella variabile [!DNL Data Lake].

Per piacere, leggi le [creare una guida alla connessione in streaming](../tutorials/create-streaming-connection.md) per ulteriori informazioni.

### Trasmetti ai set di dati

Una volta certi che i dati sono puliti, puoi abilitare i set di dati per [!DNL Real-Time Customer Profile] e [!DNL Identity Service].

Per ulteriori informazioni sull’abilitazione di un set di dati per [!DNL Profile] e [!DNL Identity Service], leggi la [configurare una guida ai set di dati](../../profile/tutorials/dataset-configuration.md).

## Qual è la latenza prevista per l’acquisizione in streaming su [!DNL Platform]?

| Destinazione | Latenza prevista |
| --------- | ---------------- |
| Profilo cliente in tempo reale | &lt; 1 minuto |
| Lago dati | &lt; 60 minuti |

## Richiesta per secondi (RPS) guida sull’acquisizione in streaming

La tabella seguente mostra le indicazioni sui limiti della richiesta per secondi per l’acquisizione in streaming.

| Limite RPS | Note |
| --- | --- |
| 1000 richieste al secondo | Possono contenere più messaggi durante l&#39;utilizzo `/collection/batch` punto finale. |
| 10000 messaggi al secondo | I messaggi possono essere raggruppati in un numero inferiore di richieste effettive quando si utilizza il `/collection/batch` punto finale. |

>[!IMPORTANT]
>
>Il limite imposto diventa **60 richieste al minuto** quando si utilizza la convalida sincrona come concepita a scopo di debug.

## Estensione Adobe Experience Platform

Puoi utilizzare l’estensione Adobe Experience Platform per creare una nuova connessione in streaming. La [!DNL Experience Platform] l&#39;estensione fornisce azioni per inviare beacon formattati in [!DNL Experience Data Model] (XDM) per l’inserimento in tempo reale in [!DNL Experience Platform]. Visita il [Estensione Experience Platform](../../tags/extensions/client/sdk/overview.md) documentazione per ulteriori informazioni.
