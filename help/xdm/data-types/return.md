---
title: Tipo di dati restituito
description: Scopri il tipo di dati Return Experience Data Model (XDM).
exl-id: 1fd99a25-547f-49e7-8980-dda7db2ebb8a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 8%

---

# Tipo di dati [!UICONTROL Return]

[!UICONTROL Return] è un tipo di dati XDM (Experience Data Model) standard che acquisisce le informazioni essenziali relative a un&#39;autorizzazione di restituzione del materiale promozionale (RMA).

![Diagramma del tipo di dati restituito.](../images/data-types/return.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|----------------------------------|----------------------|-----------|--------------------------------------------------|
| [!UICONTROL ID restituito] | `returnID` | stringa | Identificatore univoco di questa RMA. |
| [!UICONTROL Stato restituito] | `returnStatus` | stringa | Lo stato corrente della RMA (ad esempio In sospeso o Chiuso). |
| [!UICONTROL ID acquisto ordine] | `purchaseID` | stringa | L’identificatore univoco dell’ordine/acquisto a cui si riferisce RMA. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/return.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/return.schema.json)
