---
title: Classe provider
description: Scopri la classe Provider in Experience Data Model (XDM).
exl-id: acb9b8a3-f911-49c5-9d2a-3a0d6aeebef9
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 4%

---

# Classe [!UICONTROL Provider]

In Experience Data Model (XDM), la classe [!UICONTROL Provider] acquisisce il set minimo di proprietà che definiscono un&#39;entità business provider (ad esempio un provider di servizi sanitari o un provider di servizi assicurativi).

![Struttura di classe](../images/classes/provider.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `providerName` | [[!UICONTROL Nome persona]](../data-types/person-name.md) | Nome del provider. |
| `_id` | [!UICONTROL Stringa] | Identificatore di stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell’univocità di un singolo record, evitare la duplicazione dei dati e cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, durante l&#39;inserimento dei dati non verrà fornito un valore esplicito. Tuttavia, se lo desideri, puoi comunque fornire valori ID univoci. |
| `providerId` | [!UICONTROL Stringa] | Identificatore univoco del provider. |

{style="table-layout:auto"}

La classe può essere estesa con il gruppo di campi [[!UICONTROL Operatore sanitario]](../field-groups/provider/healthcare-provider.md) per descrivere ulteriori dettagli su un operatore sanitario.
