---
title: Tipo di dati Impression
description: Questo documento fornisce una panoramica del tipo di dati XDM Impression.
source-git-commit: 7fc16546176d196582a3cdfcee51f799eeef9788
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 6%

---

#  Impressionsdata

 Impression è un tipo di dati XDM standard che descrive un’impression di marketing, ovvero una metrica utilizzata per quantificare il numero di visualizzazioni digitali o di coinvolgimenti per un contenuto, ad esempio un annuncio, un post digitale o una pagina web.

![](../images/data-types/impressions.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `ID` | Stringa | Un ID univoco per l&#39;impression. |
| `displays` | Intero | Il numero di volte in cui l’elemento impression è stato visualizzato a un cliente. |
| `selected` | Intero | Il numero di volte in cui l’elemento di impression è stato selezionato o su cui è stato fatto clic. |
| `type` | Stringa | Tipo di impression. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
