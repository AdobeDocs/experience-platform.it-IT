---
title: Note sulla versione dell’estensione connettore cloud di Adobe Experience Platform
description: Note aggiornate sulla versione dell’estensione connettore cloud in Adobe Experience Platform.
exl-id: 5ee85d9f-71f4-46ee-9064-4ceee1cf90e7
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '128'
ht-degree: 100%

---

# Note sulla versione dell’estensione connettore cloud di Adobe Experience Platform

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch è ora una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

## 17 gennaio 2023

v1.0.1

* È stato risolto un problema a causa del quale un codice JSON valido incollato nell’area di testo Body Raw veniva salvato come stringa anziché come JSON.
* È possibile non consentire l’impostazione di corpo testo (body) nelle richieste GET o HEAD.
* È stato corretto un bug a causa del quale se si salvava una risposta di dimensioni superiori a 5 KB, l’esecuzione della regola non riusciva.
