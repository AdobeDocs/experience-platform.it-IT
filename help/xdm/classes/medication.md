---
title: Classe medicinale
description: Scopri la classe Farmaco in Experience Data Model (XDM).
exl-id: e5786241-dd6e-450f-98c8-2de46affb3e2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%

---

# [!UICONTROL Medicinale] classe

In Experience Data Model (XDM), la [!UICONTROL Medicinale] La classe acquisisce il set minimo di proprietà che definiscono una sostanza utilizzata per il trattamento medico, in particolare un medicinale o un farmaco.

![Struttura delle classi](../images/classes/medication.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_id` | [!UICONTROL Stringa] | Identificatore di stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell’univocità di un singolo record, evitare la duplicazione dei dati e cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, durante l’inserimento dei dati non viene fornito un valore esplicito. Tuttavia, se lo desideri, puoi comunque fornire valori ID univoci. |
| `medicationId` | [!UICONTROL Stringa] | Identificatore univoco del medicinale. |
| `medicationName` | [!UICONTROL Stringa] | Nome del medicinale. |

{style="table-layout:auto"}

La classe può essere estesa con [[!UICONTROL Medicinale sanitario] gruppo di campi](../field-groups/medication/healthcare-medication.md) per descrivere ulteriori dettagli sul medicinale o sul medicinale.
