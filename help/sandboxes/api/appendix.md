---
keywords: Experience Platform;home;argomenti popolari;api;API;sandbox;sandbox;sandbox;Sandbox
solution: Experience Platform
title: Appendice della guida API di Sandbox
description: Questo documento fornisce informazioni supplementari relative all’utilizzo dell’API Sandbox.
topic-legacy: developer guide
source-git-commit: f5ce7b7f09c624c53065757bb8a9b09f989dce0a
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---

# Appendice della guida API della sandbox

Questo documento fornisce informazioni supplementari relative all’utilizzo dell’API [!DNL Sandbox].

## Utilizzo dei parametri di query {#query}

L’ [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) supporta l’utilizzo di parametri di query per la pagina e filtrare i risultati durante l’elenco delle sandbox.

>[!NOTE]
>
>I parametri di query `limit` e `offset` devono essere specificati insieme. Se ne specifichi una sola, l’API restituirà un errore. Se non specificate nessuno, il limite predefinito è 50 e l&#39;offset è 0.

| Parametro | Descrizione |
| --- | --- |
| `limit` | Il numero massimo di record da restituire nella risposta. |
| `offset` | Il numero di entità dal primo record da cui avviare (offset) l&#39;elenco di risposte. |
