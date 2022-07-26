---
title: Classe di piano
description: Questo documento fornisce una panoramica della classe Plan in Experience Data Model (XDM).
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 5%

---

# [!UICONTROL Pianificare] Classe

In Experience Data Model (XDM), l’ [!UICONTROL Pianificare] la classe acquisisce l&#39;insieme minimo di proprietà che definiscono un piano, ad esempio un piano sanitario o un piano assicurativo.

![Struttura della classe](../images/classes/plan.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_id` | [!UICONTROL Stringa] | Identificatore stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell&#39;univocità di un singolo record, evitare la duplicazione dei dati e per cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, non viene fornito un valore esplicito durante l’inserimento dei dati. Tuttavia, se lo desideri, puoi comunque scegliere di fornire i tuoi valori ID univoci. |
| `planId` | [!UICONTROL Stringa] | Identificatore univoco del piano. |
| `planName` | [!UICONTROL Stringa] | Nome del piano. |

{style=&quot;table-layout:auto&quot;}

La classe può essere estesa con [[!UICONTROL Dettagli sul piano sanitario] gruppo di campi](../field-groups/plan/healthcare-plan-details.md) descrivere ulteriori dettagli su un piano di assicurazione malattia.
