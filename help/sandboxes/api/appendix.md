---
keywords: Experience Platform;home;argomenti popolari;api;API;sandbox;sandbox;sandbox;Sandbox
solution: Experience Platform
title: Appendice della guida API di Sandbox
description: Questo documento fornisce informazioni supplementari relative all’utilizzo dell’API Sandbox.
exl-id: 48ffea01-f1b4-48c6-a6f5-c321074023d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---

# Appendice della guida API della sandbox

Questo documento fornisce informazioni supplementari relative all&#39;utilizzo dei [!DNL Sandbox] API.

## Utilizzo dei parametri di query {#query}

La [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) supporta l’utilizzo di parametri di query per la pagina e filtrare i risultati quando vengono elencate le sandbox.

>[!NOTE]
>
>La `limit` e `offset` i parametri di query devono essere specificati insieme. Se ne specifichi una sola, l’API restituirà un errore. Se non specificate nessuno, il limite predefinito è 50 e l&#39;offset è 0.

| Parametro | Descrizione |
| --- | --- |
| `limit` | Il numero massimo di record da restituire nella risposta. |
| `offset` | Il numero di entità dal primo record da cui avviare (offset) l&#39;elenco di risposte. |
