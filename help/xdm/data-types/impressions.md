---
title: Tipo di dati impression
description: Scopri il tipo di dati XDM Impression.
exl-id: 1e758043-a41e-45f7-ae8b-514990d0649e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 6%

---

# Tipo di dati [!UICONTROL Impression]

[!UICONTROL Impression] è un tipo di dati XDM standard che descrive un&#39;impressione di marketing, ovvero una metrica utilizzata per quantificare il numero di visualizzazioni o progetti digitali per un contenuto, ad esempio un annuncio pubblicitario, un post digitale o una pagina Web.

![](../images/data-types/impressions.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `ID` | Stringa | Un ID univoco per l’impression. |
| `displays` | Intero | Il numero di volte in cui l&#39;elemento di impression è stato visualizzato a un cliente. |
| `selected` | Intero | Il numero di volte in cui l’elemento di impression è stato selezionato o cliccato. |
| `type` | Stringa | Il tipo di impression. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
