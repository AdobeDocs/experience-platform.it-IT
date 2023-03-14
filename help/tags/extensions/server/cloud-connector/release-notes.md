---
title: Note sulla versione per l’estensione Adobe Experience Platform Cloud Connector
description: Note aggiornate sulla versione dell’estensione Cloud Connector in Adobe Experience Platform.
source-git-commit: e232ad7a9b581e65f7f4240bbc06155aec409eb7
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 22%

---

# Note sulla versione dell’estensione Adobe Experience Platform Cloud Connector

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

## 17 gennaio 2023

v1.0.1

* È stato risolto un problema a causa del quale un JSON valido incollato nell’area di testo Body Raw veniva salvato come stringa invece di un JSON.
* Non consentire l’impostazione del corpo nelle richieste di GET o HEAD.
* Correggi un bug a causa del quale se si salva una risposta di dimensioni superiori a 5 kb, l’esecuzione della regola non riusciva.

