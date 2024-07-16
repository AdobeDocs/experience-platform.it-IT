---
title: Classe piano
description: Scopri la classe Plan in Experience Data Model (XDM).
exl-id: ccff962d-3104-482c-8d65-d2bd2602a9be
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%

---

# [!UICONTROL Pianifica] classe

In Experience Data Model (XDM), la classe [!UICONTROL Plan] acquisisce il set minimo di proprietà che definiscono un piano, ad esempio un piano sanitario o un piano assicurativo.

![Struttura di classe](../images/classes/plan.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_id` | [!UICONTROL Stringa] | Identificatore di stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell’univocità di un singolo record, evitare la duplicazione dei dati e cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, durante l&#39;inserimento dei dati non verrà fornito un valore esplicito. Tuttavia, se lo desideri, puoi comunque fornire valori ID univoci. |
| `planId` | [!UICONTROL Stringa] | Identificatore univoco del piano. |
| `planName` | [!UICONTROL Stringa] | Nome del piano. |

{style="table-layout:auto"}

La classe può essere estesa con il gruppo di campi [[!UICONTROL Dettagli piano sanitario]](../field-groups/plan/healthcare-plan-details.md) per descrivere ulteriori dettagli su un piano di assicurazione sanitaria.
