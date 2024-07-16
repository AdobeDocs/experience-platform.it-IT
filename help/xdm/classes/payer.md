---
title: Classe payer
description: Scopri la classe Payer in Experience Data Model (XDM).
exl-id: 8d3e0a6d-41eb-4ffe-81dd-c7b7d532a531
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 5%

---

# Classe [!UICONTROL Payer]

In Experience Data Model (XDM), la classe [!UICONTROL Payer] acquisisce il set minimo di proprietà che definiscono un&#39;entità business payer che raccoglie i dati relativi alle compagnie di assicurazione (come l&#39;assicurazione sanitaria).

![Struttura di classe](../images/classes/payer.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_id` | [!UICONTROL Stringa] | Identificatore di stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell’univocità di un singolo record, evitare la duplicazione dei dati e cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, durante l&#39;inserimento dei dati non verrà fornito un valore esplicito. Tuttavia, se lo desideri, puoi comunque fornire valori ID univoci. |
| `payerId` | [!UICONTROL Stringa] | Identificatore univoco del pagatore. |
| `payerName` | [!UICONTROL Stringa] | Nome del pagatore. |

{style="table-layout:auto"}
