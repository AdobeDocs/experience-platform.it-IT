---
title: Tipo di dati restituito
description: Scopri il tipo di dati Return Experience Data Model (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 6%

---

# [!UICONTROL Ritorno] tipo di dati

[!UICONTROL Ritorno] è un tipo di dati standard Experience Data Model (XDM) che acquisisce le informazioni essenziali relative a un’autorizzazione di restituzione del materiale promozionale (Return Merchandise Authorization, RMA).

![Diagramma del tipo di dati Return.](../images/data-types/return.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|----------------------------------|----------------------|-----------|--------------------------------------------------|
| [!UICONTROL ID restituito] | `returnID` | string | Identificatore univoco di questa RMA. |
| [!UICONTROL Stato di ritorno] | `returnStatus` | string | Lo stato corrente della RMA (ad esempio In sospeso o Chiuso). |
| [!UICONTROL ID acquisto ordine] | `purchaseID` | string | L’identificatore univoco dell’ordine/acquisto a cui si riferisce RMA. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/return.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/return.schema.json)

