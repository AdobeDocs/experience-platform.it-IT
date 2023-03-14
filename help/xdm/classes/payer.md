---
title: Classe payer
description: Questo documento fornisce una panoramica della classe Payer in Experience Data Model (XDM).
exl-id: 8d3e0a6d-41eb-4ffe-81dd-c7b7d532a531
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 5%

---

# [!UICONTROL Pagatore] classe

In Experience Data Model (XDM), la [!UICONTROL Pagatore] la classe acquisisce l&#39;insieme minimo di proprietà che definiscono un&#39;entità business payer che raccoglie dati relativi alle società di assicurazione (ad esempio l&#39;assicurazione sanitaria).

![Struttura delle classi](../images/classes/payer.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_id` | [!UICONTROL Stringa] | Identificatore di stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell’univocità di un singolo record, evitare la duplicazione dei dati e cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, durante l’inserimento dei dati non viene fornito un valore esplicito. Tuttavia, se lo desideri, puoi comunque fornire valori ID univoci. |
| `payerId` | [!UICONTROL Stringa] | Identificatore univoco del pagatore. |
| `payerName` | [!UICONTROL Stringa] | Nome del pagatore. |

{style="table-layout:auto"}
