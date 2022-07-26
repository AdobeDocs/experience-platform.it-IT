---
title: Classe di farmaco
description: Questo documento fornisce una panoramica della classe Medicina in Experience Data Model (XDM).
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 5%

---

# [!UICONTROL Medicina] Classe

In Experience Data Model (XDM), l’ [!UICONTROL Medicina] la classe acquisisce il set minimo di proprietà che definiscono una sostanza utilizzata per il trattamento medico, in particolare un farmaco o.

![Struttura della classe](../images/classes/medication.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_id` | [!UICONTROL Stringa] | Identificatore stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell&#39;univocità di un singolo record, evitare la duplicazione dei dati e per cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, non viene fornito un valore esplicito durante l’inserimento dei dati. Tuttavia, se lo desideri, puoi comunque scegliere di fornire i tuoi valori ID univoci. |
| `medicationId` | [!UICONTROL Stringa] | Identificatore univoco del farmaco. |
| `medicationName` | [!UICONTROL Stringa] | Il nome del farmaco. |

{style=&quot;table-layout:auto&quot;}

La classe può essere estesa con [[!UICONTROL Medicina sanitaria] gruppo di campi](../field-groups/medication/healthcare-medication.md) per descrivere ulteriori dettagli sul farmaco o farmaco.
