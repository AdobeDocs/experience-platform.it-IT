---
keywords: Experience Platform;home;argomenti popolari;api;API;sandbox;sandbox;sandbox;sandbox;sandbox
solution: Experience Platform
title: Appendice guida API per sandbox
description: Questo documento fornisce informazioni supplementari relative all’utilizzo dell’API Sandbox.
exl-id: 48ffea01-f1b4-48c6-a6f5-c321074023d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---

# Appendice alla guida delle API sandbox

Questo documento fornisce informazioni supplementari relative all&#39;utilizzo di [!DNL Sandbox] API.

## Utilizzo dei parametri di query {#query}

Il [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) supporta l’utilizzo di parametri di query per visualizzare e filtrare i risultati quando si elencano le sandbox.

>[!NOTE]
>
>Il `limit` e `offset` i parametri di query devono essere specificati insieme. Se ne specifichi solo uno, l’API restituirà un errore. Se non specificate alcun valore, il limite predefinito è 50 e l&#39;offset è 0.

| Parametro | Descrizione |
| --- | --- |
| `limit` | Numero massimo di record da restituire nella risposta. |
| `offset` | Numero di entità dal primo record da cui avviare (eseguire l&#39;offset) l&#39;elenco di risposte. |
