---
title: Tipo di dati carrello
description: Scopri il tipo di dati Cart Experience Data Model (XDM).
exl-id: 24ae3882-60f3-4962-b0b5-7dba48170da8
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 14%

---

# Tipo di dati [!UICONTROL Carrello]

[!UICONTROL Carrello] è un tipo di dati Experience Data Model (XDM) standard che fornisce proprietà relative a un carrello acquisti. Utilizzare questo tipo di dati per acquisire l&#39;identificatore univoco assegnato dal venditore (`Cart ID`) e l&#39;origine (`Cart Source`) in cui uno o più prodotti sono stati aggiunti al carrello.

![Diagramma del tipo di dati [!UICONTROL Carrello].](../images/data-types/cart.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL ID carrello] | `cartID` | stringa | Identificatore univoco assegnato dal venditore al carrello. |
| [!UICONTROL Source carrello] | `cartSource` | stringa | Da dove sono stati aggiunti uno o più prodotti al carrello. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)
