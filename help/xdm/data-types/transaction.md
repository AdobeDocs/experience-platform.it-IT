---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;transazione;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
title: Tipo di dati transazione
description: Questo documento fornisce una panoramica del tipo di dati XDM (Transaction Experience Data Model).
source-git-commit: bbe5456ddba1db9044b8a7f94a7ba8e450f89f0f
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 8%

---

#  Tipo di dati transazione

 Transazione è un tipo di dati XDM (Experience Data Model) standard che descrive i dettagli di una transazione monetaria.

![Struttura delle transazioni](../images/data-types/transaction.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL Valuta]](./currency.md) | Descrive l&#39;ammontare di valuta scambiata come parte della transazione. |
| `transactionDate` | [!UICONTROL DateTime] | Una marca temporale di quando si è verificata la transazione. |
| `transactionId` | [!UICONTROL Stringa] | Identificatore univoco per la transazione. |
| `transactionType` | [!UICONTROL Stringa] | Il tipo di transazione utilizzato dal visitatore. |

{style=&quot;table-layout:auto&quot;}
