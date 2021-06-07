---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;indirizzo;xdm:address;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati elemento dell’elenco prodotti
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM dell'elemento dell'elenco dei prodotti.
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 4%

---

# [!UICONTROL Tipo di ] dati dell’elenco prodotti

[!UICONTROL L’] elemento dell’elenco dei prodotti è un tipo di dati XDM standard che descrive un prodotto selezionato da un cliente con opzioni, prezzi e contesto di utilizzo specifici per un determinato punto di tempo.

I valori acquisiti in questo tipo di dati possono essere diversi dal record del prodotto. Ad esempio, il record del prodotto contiene i dettagli del sistema di informazioni sul prodotto che sono coerenti per tutti i clienti, dove l&#39;articolo dell&#39;elenco di prodotti ha il prezzo effettivo offerto al cliente al momento dell&#39;acquisto, che può variare a causa di campagne di vendita o prezzi stagionali.

![](../images/data-types/product-list-item.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `SKU` | [!UICONTROL Stringa] | Unità di conservazione delle scorte (SKU), l&#39;identificativo univoco di un prodotto definito dal fornitore. |
| `_id` | [!UICONTROL Stringa] | Identificatore della riga per la voce di prodotto. Il prodotto stesso viene identificato tramite `product`. |
| `currencyCode` | [!UICONTROL Stringa] | Il codice della valuta alfabetica [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) utilizzato per determinare il prezzo del prodotto. |
| `name` | [!UICONTROL Stringa] | Nome visualizzato del prodotto presentato all’utente per la visualizzazione del prodotto. |
| `priceTotal` | [!UICONTROL Doppio] | Prezzo totale per l&#39;articolo della linea di prodotti. |
| `product` | [!UICONTROL String]  (URI) | URI `$id` dello schema XDM che acquisisce il prodotto stesso. |
| `productAddMethod` | [!UICONTROL Stringa] | Il metodo utilizzato dal visitatore per aggiungere un elemento prodotto all’elenco. |
| `quantity` | [!UICONTROL Intero] | Il numero di unità che il cliente ha indicato di aver bisogno del prodotto. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati dell’indirizzo postale, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
