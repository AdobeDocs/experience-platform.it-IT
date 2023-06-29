---
keywords: Experience Platform;home;argomenti popolari;acquisizione dati;dati acquisiti;streaming;panoramica;acquisizione streaming;latenza;latenza streaming;
solution: Experience Platform
title: Panoramica sull’acquisizione in streaming
description: L’acquisizione in streaming per Adobe Experience Platform offre agli utenti un metodo per inviare in tempo reale dati da dispositivi lato client e lato server a Experience Platform.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 4%

---

# Panoramica sull’acquisizione in streaming

L’acquisizione in streaming per Adobe Experience Platform offre agli utenti un metodo per inviare dati da dispositivi lato client e lato server a [!DNL Experience Platform] in tempo reale.

## Cosa puoi fare con l’acquisizione in streaming?

Adobe Experience Platform ti consente di creare esperienze coordinate, coerenti e rilevanti generando un [!DNL Real-Time Customer Profile] per ogni singolo cliente. L’acquisizione in streaming svolge un ruolo chiave nella creazione di questi profili consentendoti di distribuire [!DNL Profile] dati in [!DNL Data Lake] con la minima latenza possibile.

Il video seguente è stato progettato per comprendere meglio l’acquisizione in streaming e illustra i concetti descritti in precedenza.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Flusso di record di profilo e [!DNL ExperienceEvents]

Con l’acquisizione in streaming, gli utenti possono inviare in streaming i record del profilo e [!DNL ExperienceEvents] a [!DNL Platform] in secondi per stimolare la personalizzazione in tempo reale. Tutti i dati inviati alle API Streaming Ingestion vengono automaticamente mantenuti in [!DNL Data Lake].

Leggi le [creare una guida alla connessione in streaming](../tutorials/create-streaming-connection.md) per ulteriori informazioni.

### Trasmetti a set di dati

Una volta che hai la certezza che i dati sono puliti, puoi abilitare i set di dati per [!DNL Real-Time Customer Profile] e [!DNL Identity Service].

Per ulteriori informazioni sull’abilitazione di un set di dati per [!DNL Profile] e [!DNL Identity Service], leggi le [configurare una guida al set di dati](../../profile/tutorials/dataset-configuration.md).

## Qual è la latenza prevista per l’acquisizione in streaming su [!DNL Platform]?

| Destinazione | Latenza prevista |
| --------- | ---------------- |
| Profilo cliente in tempo reale | &lt; 1 minuto |
| Data Lake | &lt; 60 minuti |

## Linee guida RPS (Request per seconds) per l’acquisizione in streaming

La tabella seguente mostra le linee guida sui limiti di richiesta al secondo per l’acquisizione in streaming.

| Limite RPS | Note |
| --- | --- |
| 1000 richieste al secondo | Questi possono contenere più messaggi quando si utilizza `/collection/batch` endpoint. |
| 10000 singoli messaggi al secondo | I messaggi possono essere raggruppati in meno richieste effettive quando si utilizza `/collection/batch` endpoint. |

>[!IMPORTANT]
>
>Il limite imposto diventa **60 richieste al minuto** quando si utilizza la convalida sincrona in quanto destinata a scopi di debug.

## Estensione Adobe Experience Platform

Puoi utilizzare l’estensione Adobe Experience Platform per creare una nuova connessione in streaming. Il [!DNL Experience Platform] L&#39;estensione fornisce azioni per inviare beacon formattati in [!DNL Experience Data Model] (XDM) per l’acquisizione in tempo reale in [!DNL Experience Platform]. Visita il [Estensione Experience Platform](../../tags/extensions/client/web-sdk/overview.md) per ulteriori informazioni.
