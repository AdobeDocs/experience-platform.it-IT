---
title: Tipo di dati interruzione annuncio
description: Scopri il tipo di dati Experience Data Model (XDM) dell’interruzione pubblicitaria.
exl-id: dfe0c386-8459-440d-95b5-b2139fac0fc3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 6%

---

# [!UICONTROL Interruzione pubblicitaria] tipo di dati

[!UICONTROL Interruzione pubblicitaria] è un tipo di dati Experience Data Model (XDM) standard che descrive come un annuncio a tempo viene inserito in un elemento multimediale a tempo.

![Struttura del tipo di dati](../images/data-types/ad-break.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_dc.title` | Stringa | Un nome descrittivo per l’interruzione pubblicitaria. |
| `_id` | Stringa | Identificatore univoco dell’interruzione pubblicitaria. |
| `offset` | Intero | Lo scostamento, in secondi, dell’interruzione pubblicitaria dall’inizio del contenuto principale. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
