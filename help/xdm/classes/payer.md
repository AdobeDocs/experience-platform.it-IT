---
title: Classe ordinante
description: Questo documento fornisce una panoramica della classe Payer in Experience Data Model (XDM).
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 5%

---

# [!UICONTROL Pagatore] Classe

In Experience Data Model (XDM), l’ [!UICONTROL Pagatore] la classe acquisisce l&#39;insieme minimo di proprietà che definiscono un&#39;entità aziendale ordinante che raccoglie i dati relativi alle imprese di assicurazione (come l&#39;assicurazione malattia).

![Struttura della classe](../images/classes/payer.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_id` | [!UICONTROL Stringa] | Identificatore stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell&#39;univocità di un singolo record, evitare la duplicazione dei dati e per cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, non viene fornito un valore esplicito durante l’inserimento dei dati. Tuttavia, se lo desideri, puoi comunque scegliere di fornire i tuoi valori ID univoci. |
| `payerId` | [!UICONTROL Stringa] | Identificatore univoco del pagatore. |
| `payerName` | [!UICONTROL Stringa] | Nome del pagatore. |

{style=&quot;table-layout:auto&quot;}
