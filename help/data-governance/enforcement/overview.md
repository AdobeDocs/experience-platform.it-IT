---
keywords: Experience Platform;home;argomenti popolari;Applicazione dei criteri;Applicazione automatica;Imposizione basata su API;governance dei dati
solution: Experience Platform
title: Panoramica sull'applicazione dei criteri
description: Scopri come i criteri di utilizzo dei dati vengono applicati in Adobe Experience Platform.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Panoramica sull’applicazione dei criteri

Una volta [etichette di utilizzo dei dati](../labels/overview.md) sono stati applicati e [criteri di utilizzo dati](../policies/overview.md) sono stati definiti, puoi applicare tali criteri per evitare operazioni sui dati che costituiscono violazioni dei criteri.

>[!NOTE]
>
>Questo documento si concentra sull’applicazione dei criteri di utilizzo dei dati. Per informazioni sui criteri di controllo di accesso, consulta la guida su [controllo degli accessi basato su attributi](../../access-control/abac/overview.md).

Esistono due metodi per l’applicazione dei criteri in Adobe Experience Platform: l’applicazione automatica e l’applicazione basata su API.

## Applicazione automatica

Experience Platform sfrutta la derivazione dei dati, la classificazione dei dati e le funzionalità di gestione delle policy per valutare e rendere visibili automaticamente le violazioni delle policy. Consulta la panoramica su [applicazione automatica delle policy](./auto-enforcement.md) per ulteriori informazioni.

## Imposizione basata su API

Il [!DNL Policy Service] L’API fornisce endpoint che consentono di testare azioni di marketing in base a set di dati o combinazioni arbitrarie di etichette di utilizzo dei dati per verificare se si verificano violazioni dei criteri. In base alla risposta API, puoi quindi configurare i protocolli all’interno dell’applicazione Experience per applicare in modo appropriato la conformità ai criteri di governance dei dati.

Guarda il tutorial su [Imposizione basata su API](./api-enforcement.md) per i passaggi su come valutare i criteri utilizzando l’API.
