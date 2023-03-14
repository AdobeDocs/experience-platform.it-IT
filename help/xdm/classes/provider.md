---
title: Classe provider
description: Questo documento fornisce una panoramica della classe Provider in Experience Data Model (XDM).
exl-id: acb9b8a3-f911-49c5-9d2a-3a0d6aeebef9
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 4%

---

# [!UICONTROL Provider] classe

In Experience Data Model (XDM), la [!UICONTROL Provider] la classe acquisisce l&#39;insieme minimo di proprietà che definiscono un&#39;entità aziendale fornitore (ad esempio un fornitore di assistenza sanitaria o un fornitore di assicurazione).

![Struttura delle classi](../images/classes/provider.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `providerName` | [[!UICONTROL Nome della persona]](../data-types/person-name.md) | Nome del provider. |
| `_id` | [!UICONTROL Stringa] | Identificatore di stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell’univocità di un singolo record, evitare la duplicazione dei dati e cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, durante l’inserimento dei dati non viene fornito un valore esplicito. Tuttavia, se lo desideri, puoi comunque fornire valori ID univoci. |
| `providerId` | [!UICONTROL Stringa] | Identificatore univoco del provider. |

{style="table-layout:auto"}

La classe può essere estesa con [[!UICONTROL Fornitore di servizi sanitari] gruppo di campi](../field-groups/provider/healthcare-provider.md) per descrivere ulteriori dettagli su un operatore sanitario.
