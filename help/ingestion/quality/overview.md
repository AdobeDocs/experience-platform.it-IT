---
keywords: Experience Platform;home;argomenti popolari;qualità dei dati;qualità;convalida supportata;convalida;convalida supportata;
solution: Experience Platform
title: Qualità dei dati
description: Il seguente documento fornisce un riepilogo dei controlli e dei comportamenti di convalida supportati per l’acquisizione in batch e in streaming in Adobe Experience Platform.
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 5%

---

# Qualità dei dati in Adobe Experience Platform

Adobe Experience Platform offre garanzie ben definite di completezza, accuratezza e coerenza per tutti i dati caricati tramite l’acquisizione in batch o in streaming. Il seguente documento fornisce un riepilogo dei controlli e dei comportamenti di convalida supportati per l’acquisizione in batch e in streaming in [!DNL Experience Platform].

## Controlli supportati

|   | Acquisizione in batch | Acquisizione in streaming |
| ------ | --------------- | ------------------- |
| Controllo del tipo di dati | Sì | Sì |
| Controllo enum | Sì | Sì |
| Controllo intervallo (min, max) | Sì | Sì |
| Controllo campo obbligatorio | Sì | Sì |
| Verifica pattern | No | Sì |
| Verifica formato | No | Sì |

## Comportamenti di convalida supportati

Sia l’acquisizione in batch che in streaming evitano che i dati non riusciti vengano trasferiti a valle spostando i dati danneggiati per il recupero e l’analisi in [!DNL Data Lake]. L’acquisizione dei dati fornisce le seguenti convalide per l’acquisizione in batch e in streaming.

### Acquisizione batch

Per l’acquisizione in batch vengono eseguite le seguenti convalide:

| Area di convalida | Descrizione |
| --------------- | ----------- |
| Schema | Verifica che lo schema sia **non** vuoto e contiene un riferimento allo schema di unione come segue: `"meta:immutableTags": ["union"]` |
| `identityField` | Assicura che siano definiti tutti i descrittori di identità validi. |
| `createdUser` | Assicura che l’utente che ha acquisito il batch possa acquisirlo. |

### Acquisizione in streaming

Per l’acquisizione in streaming vengono eseguite le seguenti convalide:

| Area di convalida | Descrizione |
| --------------- | ----------- |
| Schema | Verifica che lo schema sia **non** vuoto e contiene un riferimento allo schema di unione come segue: `"meta:immutableTags": ["union"]` |
| `identityField` | Assicura che siano definiti tutti i descrittori di identità validi. |
| JSON | Assicura che il JSON sia valido. |
| Organizzazione IMS | Verifica che l’organizzazione IMS indicata sia valida. |
| Nome origine | Assicura che sia specificato il nome dell&#39;origine dati. |
| Set di dati | Assicura che il set di dati sia specificato, abilitato e non sia stato rimosso. |
| Header | Verifica che l’intestazione sia specificata e valida. |

Ulteriori informazioni su come [!DNL Platform] monitora e convalida i dati sono disponibili nella sezione [monitoraggio della documentazione dei flussi di dati](./monitor-data-ingestion.md).

## Convalida del valore identità

La tabella seguente illustra le regole esistenti da seguire per garantire la corretta convalida del valore di identità.

| Namespace | Regola di convalida | Comportamento del sistema quando la regola viene violata |
| --- | --- | --- |
| ECID | <ul><li>Il valore identità di un ECID deve essere esattamente di 38 caratteri.</li><li>Il valore identità di un ECID deve essere costituito solo da numeri.</li></ul> | <ul><li>Se il valore identità di ECID non è esattamente di 38 caratteri, il record viene ignorato.</li><li>Se il valore di identità dell’ECID contiene caratteri non numerici, il record viene ignorato.</li></ul> |
| Non ECID | Il valore identità non può superare i 1024 caratteri. | Se il valore di identità supera i 1024 caratteri, il record viene ignorato. |

Per ulteriori informazioni su [!DNL Identity Service] guardrail, vedere [[!DNL Identity Service] panoramica sui guardrail](../../identity-service/guardrails.md).
