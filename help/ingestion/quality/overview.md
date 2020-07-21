---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Qualità dell'assimilazione dei dati
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 6%

---


# Qualità dei dati in  Adobe Experience Platform

 Adobe Experience Platform offre garanzie ben definite per completezza, precisione e coerenza dei dati caricati tramite l’assimilazione in batch o in streaming. Il seguente documento fornisce un riepilogo dei controlli e dei comportamenti di convalida supportati per l’inserimento di batch e streaming in [!DNL Experience Platform].

## Controlli supportati

|   | Inserimento batch | Ingestione streaming |
| ------ | --------------- | ------------------- |
| Controllo del tipo di dati | Sì | Sì |
| Controllo Enum | Sì | Sì |
| Controllo intervallo (min, max) | Sì | Sì |
| Controllo campo obbligatorio | Sì | Sì |
| Controllo pattern | No | Sì |
| Controllo formato | No | Sì |

## Comportamenti di convalida supportati

Sia l’assimilazione batch che lo streaming impediscono l’accesso a valle dei dati non riusciti, spostando i dati errati per il recupero e l’analisi in [!DNL Data Lake]. L&#39;assimilazione dei dati fornisce le seguenti convalide per l&#39;assimilazione batch e lo streaming.

### Caricamento batch

Le seguenti convalide vengono eseguite per l&#39;assimilazione batch:

| Area di convalida | Descrizione |
| --------------- | ----------- |
| Schema | Assicurarsi che lo schema **non** sia vuoto e contenga un riferimento allo schema unione, come segue: `"meta:immutableTags": ["union"]` |
| `identityField` | Assicurarsi che tutti i descrittori di identità validi siano definiti. |
| `createdUser` | Assicurarsi che l&#39;utente che ha effettuato l&#39;acquisizione del batch sia autorizzato a caricare il batch. |

### Caricamento in streaming

Le seguenti convalide vengono eseguite per l&#39;assimilazione in streaming:

| Area di convalida | Descrizione |
| --------------- | ----------- |
| Schema | Assicurarsi che lo schema **non** sia vuoto e contenga un riferimento allo schema unione, come segue: `"meta:immutableTags": ["union"]` |
| `identityField` | Assicurarsi che tutti i descrittori di identità validi siano definiti. |
| JSON | Assicurarsi che il JSON sia valido. |
| Organizzazione IMS | Assicurarsi che l&#39;organizzazione IMS elencata sia un&#39;organizzazione valida. |
| Nome origine | Assicurarsi che il nome dell&#39;origine dati sia specificato. |
| Set di dati | Assicurarsi che il dataset sia specificato, attivato e non sia stato rimosso. |
| Intestazione | Assicurarsi che l&#39;intestazione sia specificata ed è valida. |

Ulteriori informazioni sulle modalità di [!DNL Platform] monitoraggio e convalida dei dati sono disponibili nella documentazione [sui flussi di dati di](./monitor-data-flows.md)monitoraggio.
