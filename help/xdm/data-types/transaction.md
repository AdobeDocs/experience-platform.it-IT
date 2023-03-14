---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;transazione;tipo di dati;tipo di dati;tipo di dati;
title: Tipo di dati transazione
description: Questo documento fornisce una panoramica del tipo di dati Transaction Experience Data Model (XDM).
exl-id: 47b7152f-a853-44f0-8962-e902631ad8a4
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 7%

---

# [!UICONTROL Transazione] tipo di dati

[!UICONTROL Transazione] è un tipo di dati standard Experience Data Model (XDM) che descrive i dettagli di una transazione monetaria.

![Struttura delle transazioni](../images/data-types/transaction.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL Valuta]](./currency.md) | Descrive l&#39;importo della valuta scambiata nell&#39;ambito della transazione. |
| `transactionDate` | [!UICONTROL DateTime] | Timestamp del momento in cui si è verificata la transazione. |
| `transactionId` | [!UICONTROL Stringa] | Identificatore univoco della transazione. |
| `transactionType` | [!UICONTROL Stringa] | Tipo di transazione utilizzato dal visitatore. |

{style="table-layout:auto"}
