---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;transazione;tipo di dati;tipo di dati;tipo di dati;
title: Tipo di dati transazione
description: Scopri il tipo di dati Transaction Experience Data Model (XDM).
exl-id: 47b7152f-a853-44f0-8962-e902631ad8a4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '92'
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
