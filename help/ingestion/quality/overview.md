---
keywords: Experience Platform;home;argomenti comuni;qualità dei dati;qualità;convalida supportata;convalida;convalida supportata;
solution: Experience Platform
title: Qualità dei dati
topic-legacy: overview
description: Il seguente documento fornisce un riepilogo dei controlli e dei comportamenti di convalida supportati per l’acquisizione in batch e in streaming in Adobe Experience Platform.
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 5%

---

# Qualità dei dati in Adobe Experience Platform

Adobe Experience Platform fornisce garanzie ben definite per la completezza, l’accuratezza e la coerenza dei dati caricati tramite l’acquisizione in batch o in streaming. Il seguente documento fornisce un riepilogo dei controlli e dei comportamenti di convalida supportati per l’acquisizione in batch e in streaming in [!DNL Experience Platform].

## Controlli supportati

|   | Acquisizione batch | Acquisizione in streaming |
| ------ | --------------- | ------------------- |
| Controllo del tipo di dati | Sì | Sì |
| Controllo Enum | Sì | Sì |
| Controllo intervallo (min, max) | Sì | Sì |
| Controllo campo obbligatorio | Sì | Sì |
| Controllo pattern | No | Sì |
| Controllo formato | No | Sì |

## Comportamenti di convalida supportati

L’acquisizione in batch e in streaming impedisce che i dati non riusciti vadano a valle spostando i dati errati per il recupero e l’analisi in [!DNL Data Lake]. L’acquisizione dei dati fornisce le seguenti convalide per l’acquisizione in batch e in streaming.

### Acquisizione batch

Le seguenti convalide vengono eseguite per l’acquisizione batch:

| Area di convalida | Descrizione |
| --------------- | ----------- |
| Schema | Assicura che lo schema sia **non** vuoto e contenga un riferimento allo schema dell&#39;unione, come segue: `"meta:immutableTags": ["union"]` |
| `identityField` | Assicura che siano definiti tutti i descrittori di identità validi. |
| `createdUser` | Assicura che l&#39;utente che ha acquisito il batch possa acquisire il batch. |

### Acquisizione in streaming

Le seguenti convalide vengono eseguite per l’acquisizione in streaming:

| Area di convalida | Descrizione |
| --------------- | ----------- |
| Schema | Assicura che lo schema sia **non** vuoto e contenga un riferimento allo schema dell&#39;unione, come segue: `"meta:immutableTags": ["union"]` |
| `identityField` | Assicura che siano definiti tutti i descrittori di identità validi. |
| JSON | Assicura che il JSON sia valido. |
| Organizzazione IMS | Assicura che l’organizzazione IMS indicata sia un’organizzazione valida. |
| Nome origine | Assicura che sia specificato il nome dell’origine dati. |
| Set di dati | Assicura che il set di dati sia specificato, abilitato e non sia stato rimosso. |
| Header | Verifica che l’intestazione sia specificata ed è valida. |

Ulteriori informazioni sul modo in cui [!DNL Platform] monitora e convalida i dati sono disponibili nella [documentazione sui flussi di dati di monitoraggio](./monitor-data-ingestion.md).
