---
title: Tipo di dati elemento restituito
description: Scopri il tipo di dati Return Item Experience Data Model (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 6%

---

# [!UICONTROL Restituisci elemento] tipo di dati

[!UICONTROL Restituisci elemento] è un tipo di dati Experience Data Model (XDM) standard che acquisisce dettagli essenziali relativi al processo di restituzione di un articolo acquistato.

![Diagramma del tipo di dati Articolo restituito.](../images/data-types/return-item.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|-----------------------------|------------------------------|-----------|--------------------------------------------------------|
| [!UICONTROL Stato di ritorno] | `returnStatus` | string | Stato dell&#39;elemento restituito, ad esempio In sospeso o Approvato. |
| [!UICONTROL Motivo restituzione] | `returnReason` | string | Motivo per cui è stata richiesta la restituzione per l&#39;articolo. |
| [!UICONTROL Condizione restituzione articolo] | `returnItemCondition` | string | La condizione dell&#39;articolo per il quale viene richiesta la restituzione. |
| [!UICONTROL Risoluzione di ritorno] | `returnResolution` | string | La risoluzione o il risultato desiderato atteso dal rendimento (ad esempio, rimborso o scambio). |
| [!UICONTROL Quantità restituita richiesta] | `returnQuantityRequested` | numero intero | Quantità dell&#39;articolo che l&#39;acquirente ha richiesto di restituire. |
| [!UICONTROL Quantità di reso autorizzata] | `returnQuantityAuthorized` | numero intero | Quantità dell&#39;articolo di cui è autorizzata la restituzione. |
| [!UICONTROL Quantità restituita ricevuta] | `returnQuantityReceived` | numero intero | Quantità di articoli restituiti ricevuti. |
| [!UICONTROL Quantità di reso approvata] | `returnQuantityApproved` | numero intero | Quantità dell&#39;articolo con restituzione completa e approvata. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.schema.json)
