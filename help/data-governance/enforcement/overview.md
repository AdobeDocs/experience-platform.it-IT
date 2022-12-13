---
keywords: Experience Platform;home;argomenti popolari;applicazione dei criteri;applicazione automatica;applicazione basata su API;governance dei dati
solution: Experience Platform
title: Panoramica sull’applicazione dei criteri
topic-legacy: guide
description: Scopri come vengono applicati i criteri di utilizzo dei dati in Adobe Experience Platform.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 6f79b1a03a75558d1a25f0375e8393ad56756d80
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Panoramica sull&#39;applicazione dei criteri

Una volta [etichette di utilizzo dei dati](../labels/overview.md) sono stati applicati e [criteri di utilizzo dei dati](../policies/overview.md) sono stati definiti, è possibile applicare tali criteri per impedire operazioni di dati che costituiscono violazioni delle politiche.

>[!NOTE]
>
>Questo documento si concentra sull&#39;applicazione dei criteri di utilizzo dei dati. Per informazioni sulle politiche di controllo degli accessi, consulta la guida su [controllo dell&#39;accesso basato sugli attributi](../../access-control/abac/overview.md).

Su Adobe Experience Platform sono disponibili due metodi di applicazione delle policy: implementazione automatica e applicazione basata su API.

## Applicazione automatica

Experience Platform sfrutta la derivazione dei dati, la classificazione dei dati e le funzionalità di gestione dei criteri per valutare automaticamente e individuare le violazioni dei criteri. Vedi la panoramica su [applicazione automatica delle politiche](./auto-enforcement.md) per ulteriori informazioni.

## Implementazione basata su API

La [!DNL Policy Service] L’API fornisce endpoint che consentono di testare le azioni di marketing rispetto ai set di dati o a combinazioni arbitrarie di etichette di utilizzo dei dati per verificare se si verificano violazioni dei criteri. In base alla risposta API, puoi quindi impostare i protocolli all’interno dell’applicazione di esperienza per applicare in modo appropriato la conformità ai criteri di governance dei dati.

Guarda l’esercitazione su [Implementazione basata su API](./api-enforcement.md) per informazioni su come valutare i criteri utilizzando l’API .
