---
title: Tipo di dati carrello
description: Scopri il tipo di dati Cart Experience Data Model (XDM).
source-git-commit: c3590dc2cfe47eb634136eeb88578f965598760d
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 5%

---

# [!UICONTROL Carrello] tipo di dati

[!UICONTROL Carrello] è un tipo di dati Experience Data Model (XDM) standard che fornisce proprietà relative a un carrello. Utilizza questo tipo di dati per acquisire l&#39;identificatore univoco assegnato dal venditore (`Cart ID`) e la sorgente (`Cart Source`) quando uno o più prodotti sono stati aggiunti al carrello.

![Un diagramma del [!UICONTROL Carrello] tipo di dati.](../images/data-types/cart.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL ID carrello] | `cartID` | string | Identificatore univoco assegnato dal venditore al carrello. |
| [!UICONTROL Origine carrello] | `cartSource` | string | Da dove sono stati aggiunti uno o più prodotti al carrello. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)
