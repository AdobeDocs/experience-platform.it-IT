---
title: Note sulla versione dell’estensione connettore cloud di Adobe Experience Platform
description: Note aggiornate sulla versione dell’estensione connettore cloud in Adobe Experience Platform.
exl-id: 5ee85d9f-71f4-46ee-9064-4ceee1cf90e7
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 100%

---

# Note sulla versione dell’estensione connettore cloud di Adobe Experience Platform

## 17 gennaio 2023

v1.0.1

* È stato risolto un problema a causa del quale un codice JSON valido incollato nell’area di testo Body Raw veniva salvato come stringa anziché come JSON.
* È possibile non consentire l’impostazione di corpo testo (body) nelle richieste GET o HEAD.
* È stato corretto un bug a causa del quale se si salvava una risposta di dimensioni superiori a 5 KB, l’esecuzione della regola non riusciva.
