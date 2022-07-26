---
title: Tipo di dati di interruzione annuncio
description: Questo documento fornisce una panoramica del tipo di dati XDM (Ad break Experience Data Model).
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 6%

---

# [!UICONTROL Pausa annunci] tipo di dati

[!UICONTROL Pausa annunci] è un tipo di dati XDM (Experience Data Model) standard che descrive il modo in cui un annuncio temporizzato viene inserito in un elemento multimediale temporizzato.

![Struttura del tipo di dati](../images/data-types/ad-break.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_dc.title` | Stringa | Un nome descrittivo per la pausa pubblicitaria. |
| `_id` | Stringa | Identificatore univoco per l&#39;interruzione pubblicitaria. |
| `offset` | Intero | L’offset, in secondi, dell’interruzione dell’annuncio dall’inizio del contenuto principale. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
