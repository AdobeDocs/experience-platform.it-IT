---
title: Classe fornitore
description: Questo documento fornisce una panoramica della classe Provider in Experience Data Model (XDM).
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 4%

---

# [!UICONTROL Provider] Classe

In Experience Data Model (XDM), l’ [!UICONTROL Provider] la classe acquisisce l&#39;insieme minimo di proprietà che definiscono un&#39;entità aziendale fornitore (ad esempio un fornitore di assistenza sanitaria o un fornitore di assicurazioni).

![Struttura della classe](../images/classes/provider.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `providerName` | [[!UICONTROL Nome della persona]](../data-types/person-name.md) | Nome del provider. |
| `_id` | [!UICONTROL Stringa] | Identificatore stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell&#39;univocità di un singolo record, evitare la duplicazione dei dati e per cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, non viene fornito un valore esplicito durante l’inserimento dei dati. Tuttavia, se lo desideri, puoi comunque scegliere di fornire i tuoi valori ID univoci. |
| `providerId` | [!UICONTROL Stringa] | Identificatore univoco per il provider. |

{style=&quot;table-layout:auto&quot;}

La classe può essere estesa con [[!UICONTROL Fornitore sanitario] gruppo di campi](../field-groups/provider/healthcare-provider.md) descrivere ulteriori dettagli su un fornitore di assistenza sanitaria.
