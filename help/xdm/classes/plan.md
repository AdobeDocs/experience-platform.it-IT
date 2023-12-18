---
title: Classe piano
description: Scopri la classe Plan in Experience Data Model (XDM).
exl-id: ccff962d-3104-482c-8d65-d2bd2602a9be
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%

---

# [!UICONTROL Piano] classe

In Experience Data Model (XDM), la [!UICONTROL Piano] classe acquisisce la serie minima di proprietà che definiscono un piano, ad esempio un piano sanitario o un piano assicurativo.

![Struttura delle classi](../images/classes/plan.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_id` | [!UICONTROL Stringa] | Identificatore di stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell’univocità di un singolo record, evitare la duplicazione dei dati e cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, durante l’inserimento dei dati non viene fornito un valore esplicito. Tuttavia, se lo desideri, puoi comunque fornire valori ID univoci. |
| `planId` | [!UICONTROL Stringa] | Identificatore univoco del piano. |
| `planName` | [!UICONTROL Stringa] | Nome del piano. |

{style="table-layout:auto"}

La classe può essere estesa con [[!UICONTROL Dettagli piano sanitario] gruppo di campi](../field-groups/plan/healthcare-plan-details.md) descrivere ulteriori dettagli su un piano di assicurazione sanitaria.
