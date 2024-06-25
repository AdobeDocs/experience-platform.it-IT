---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;ordine;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati ordine
description: Scopri il tipo di dati Order Experience Data Model (XDM).
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 09ca510da0819ab38687edadbcc632ccbbe8ef83
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 13%

---

# [!UICONTROL Ordine] tipo di dati

[!UICONTROL Ordine] è un tipo di dati Experience Data Model (XDM) standard che descrive l’ordine effettuato per un elenco di prodotti.

![Un diagramma del [!UICONTROL Ordine] tipo di dati.](../images/data-types/order.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|-------------------------|-------------------------|-----------|------------------------------------------------------------------------------------------------------------------|
| ID acquisto | `purchaseID` | Stringa | Un identificatore univoco assegnato dal venditore per questo acquisto o contratto. Non c&#39;è garanzia che l&#39;ID sia univoco perché l&#39;ID è definito dal venditore. |
| Numero dell’ordine d’acquisto | `purchaseOrderNumber` | Stringa | Identificatore univoco assegnato dall’acquirente a questo acquisto o contratto. |
| Elenco dei pagamenti | `payments` | Array di [[!UICONTROL Voci di pagamento]](./payment-item.md) | Elenco dei pagamenti per questo ordine. I pagamenti sono descritti in dettaglio nella [!UICONTROL Voci di pagamento] specifica. |
| Elenco rimborsi | `refunds` | Array di [[!UICONTROL Voci di rimborso]](./refund-item.md) | Elenco dei rimborsi per questo ordine. Le restituzioni sono indicate nel dettaglio [!UICONTROL Voci di rimborso] specifica. |
| Informazioni di ritorno | `returns` | [[!UICONTROL Informazioni di ritorno]](./return.md) | RMA (Return Merchandise Authorization) rilasciato. Le restituzioni sono descritte in dettaglio [!UICONTROL Informazioni di ritorno] specifica. |
| Valuta | `currencyCode` | Stringa | Il codice valuta ISO 4217 utilizzato per i totali dell’ordine. Alcuni esempi includono `USD` e `EUR`. Tutte le varianti devono corrispondere al pattern `^[A-Z]{3}$`. |
| Importo imposta | `taxAmount` | Numero | Importo dell&#39;imposta pagato dall&#39;acquirente come parte del pagamento finale. |
| Importo sconto | `discountAmount` | Numero | Differenza tra il prezzo regolare e il prezzo speciale applicato all’intero ordine, anziché ai singoli prodotti. |
| Totale prezzo | `priceTotal` | Numero | Il prezzo totale di questo ordine dopo l’applicazione di tutti gli sconti e le tasse. |
| Tipo di ordine | `orderType` | Stringa | Tipo di ordine che è stato effettuato. I valori possibili sono `checkout` e `instant_purchase`. |
| Data ultimo aggiornamento | `lastUpdatedDate` | Stringa | L’ora dell’ultimo aggiornamento di un determinato record dell’ordine nel sistema commerciale. Formato: data-ora. |
| Data di creazione | `createdDate` | Stringa | L’ora/data in cui viene creato un nuovo ordine nel sistema commerce. Formato: data-ora. |
| Annulla data | `cancelDate` | Stringa | La data/ora in cui l’acquirente avvia un annullamento dell’ordine. Formato: data-ora. |
| Importo totale rimborsato | `refundTotal` | Numero | L&#39;importo totale previsto in questo rimborso sull&#39;ordine, combinando tutti gli elementi rimborsati e dopo eventuali sconti ecc. sono state applicate. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
