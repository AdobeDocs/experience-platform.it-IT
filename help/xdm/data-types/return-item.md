---
title: Tipo di dati elemento restituito
description: Scopri il tipo di dati Return Item Experience Data Model (XDM).
exl-id: e703d65b-a133-484e-96d6-6b1f50fc1e48
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 7%

---

# Tipo di dati [!UICONTROL Restituisci elemento]

[!UICONTROL Return Item] è un tipo di dati XDM (Experience Data Model) standard che acquisisce i dettagli essenziali relativi al processo di restituzione di un articolo acquistato.

![Diagramma del tipo di dati Elemento restituito.](../images/data-types/return-item.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|-----------------------------|------------------------------|-----------|--------------------------------------------------------|
| [!UICONTROL Stato restituito] | `returnStatus` | stringa | Stato dell&#39;elemento restituito, ad esempio In sospeso o Approvato. |
| [!UICONTROL Motivo restituzione] | `returnReason` | stringa | Motivo per cui è stata richiesta la restituzione per l&#39;articolo. |
| [!UICONTROL Condizione elemento restituito] | `returnItemCondition` | stringa | La condizione dell&#39;articolo per il quale viene richiesta la restituzione. |
| [!UICONTROL Risoluzione restituita] | `returnResolution` | stringa | La risoluzione o il risultato desiderato atteso dal rendimento (ad esempio, rimborso o scambio). |
| [!UICONTROL Quantità restituita richiesta] | `returnQuantityRequested` | intero | Quantità dell&#39;articolo che l&#39;acquirente ha richiesto di restituire. |
| [!UICONTROL Quantità restituita autorizzata] | `returnQuantityAuthorized` | intero | Quantità dell&#39;articolo di cui è autorizzata la restituzione. |
| [!UICONTROL Quantità restituita ricevuta] | `returnQuantityReceived` | intero | Quantità di articoli restituiti ricevuti. |
| [!UICONTROL Quantità restituita approvata] | `returnQuantityApproved` | intero | Quantità dell&#39;articolo con restituzione completa e approvata. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.schema.json)
