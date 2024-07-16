---
keywords: Experience Platform;home;argomenti popolari;acquisizione dati;dati acquisiti;streaming;panoramica;acquisizione streaming;latenza;latenza streaming;
solution: Experience Platform
title: Panoramica sull’acquisizione in streaming
description: L’acquisizione in streaming per Adobe Experience Platform offre agli utenti un metodo per inviare in tempo reale dati da dispositivi lato client e lato server a Experience Platform.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: d6424e2a9afc046f4bff329797954fd43939a819
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 2%

---

# Panoramica sull’acquisizione in streaming

L&#39;acquisizione in streaming per Adobe Experience Platform offre agli utenti un metodo per inviare in tempo reale dati da dispositivi lato client e lato server a [!DNL Experience Platform].

## Cosa puoi fare con l’acquisizione in streaming?

Adobe Experience Platform ti consente di creare esperienze coordinate, coerenti e rilevanti generando un [!DNL Real-Time Customer Profile] per ogni singolo cliente. L&#39;acquisizione in streaming svolge un ruolo chiave nella creazione di questi profili consentendo di inviare dati [!DNL Profile] a [!DNL Data Lake] con la minor latenza possibile.

Il video seguente è stato progettato per comprendere meglio l’acquisizione in streaming e illustra i concetti descritti in precedenza.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Trasmetti record profilo e [!DNL ExperienceEvents]

Con l’acquisizione in streaming, gli utenti possono eseguire lo streaming dei record del profilo e da [!DNL ExperienceEvents] a [!DNL Platform] in secondi per favorire la personalizzazione in tempo reale. Tutti i dati inviati alle API Streaming Ingestion vengono automaticamente memorizzati in [!DNL Data Lake].

Per ulteriori informazioni, leggere la [guida alla creazione di una connessione in streaming](../tutorials/create-streaming-connection.md).

### Trasmetti a set di dati

Dopo aver verificato che i dati sono puliti, puoi abilitare i set di dati per [!DNL Real-Time Customer Profile] e [!DNL Identity Service].

Per ulteriori informazioni sull&#39;abilitazione di un set di dati per [!DNL Profile] e [!DNL Identity Service], leggere la [guida alla configurazione di un set di dati](../../profile/tutorials/dataset-configuration.md).

## Qual è la latenza prevista per l’acquisizione in streaming su Experience Platform?

>[!IMPORTANT]
>
>I guardrail per l’acquisizione in streaming vengono calcolati a livello di organizzazione e non a livello di sandbox. Ciò significa che l’utilizzo dei dati per sandbox è associato al diritto totale all’utilizzo della licenza che corrisponde all’intera organizzazione. Inoltre, l’utilizzo dei dati nelle sandbox di sviluppo è limitato al 10% del totale dei profili. Per ulteriori informazioni sui diritti di utilizzo della licenza, leggere la [guida alle best practice per la gestione dei dati](../../landing/license-usage-and-guardrails/data-management-best-practices.md).

| Destinazione | Latenza prevista |
| --------- | ---------------- |
| Profilo cliente in tempo reale | &lt; 15 minuti al 95° percentile |
| Data lake | &lt; 60 minuti |

## Linee guida RPS (Request per seconds) per l’acquisizione in streaming

La tabella seguente mostra le linee guida sui limiti di richiesta al secondo per l’acquisizione in streaming.

| Limite RPS | Note |
| --- | --- |
| 1000 richieste al secondo | Questi possono contenere più messaggi quando si utilizza l&#39;endpoint `/collection/batch`. |
| 10000 singoli messaggi al secondo | I messaggi possono essere raggruppati in un numero inferiore di richieste effettive quando si utilizza l&#39;endpoint `/collection/batch`. |

>[!IMPORTANT]
>
>Il limite imposto diventa **60 richieste al minuto** quando si utilizza la convalida sincrona, in quanto destinata a scopi di debug.

## Estensione Adobe Experience Platform

Puoi utilizzare l’estensione Adobe Experience Platform per creare una nuova connessione in streaming. L&#39;estensione [!DNL Experience Platform] fornisce azioni per inviare beacon formattati in [!DNL Experience Data Model] (XDM) per l&#39;acquisizione in tempo reale in [!DNL Experience Platform]. Per ulteriori informazioni, consulta la documentazione dell&#39;estensione [Experience Platform](../../tags/extensions/client/web-sdk/overview.md).
