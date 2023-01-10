---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;indirizzo;xdm:address;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati elemento dell’elenco prodotti
description: Questo documento fornisce una panoramica del tipo di dati XDM dell'elemento dell'elenco dei prodotti.
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 4%

---

# [!UICONTROL Voce dell’elenco dei prodotti] tipo di dati

[!UICONTROL Voce dell’elenco dei prodotti] è un tipo di dati XDM standard che descrive un prodotto selezionato da un cliente con opzioni, prezzi e contesto di utilizzo specifici per un determinato punto di tempo.

I valori acquisiti in questo tipo di dati possono essere diversi dal record del prodotto. Ad esempio, il record del prodotto contiene i dettagli del sistema di informazioni sul prodotto che sono coerenti per tutti i clienti, dove l&#39;articolo dell&#39;elenco di prodotti ha il prezzo effettivo offerto al cliente al momento dell&#39;acquisto, che può variare a causa di campagne di vendita o prezzi stagionali.

![](../images/data-types/product-list-item.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `selectedOptions` | Array di oggetti | Contiene opzioni personalizzate selezionate per un prodotto configurabile. Ogni voce di elenco è un oggetto con le seguenti proprietà:<ul><li>`attribute`: Un nome per l&#39;attributo configurabile.</li><li>`value`: Il valore dell&#39;attributo.</li></ul> |
| `SKU` | [!UICONTROL Stringa] | Unità di conservazione delle scorte (SKU), l&#39;identificativo univoco di un prodotto definito dal fornitore. |
| `_id` | [!UICONTROL Stringa] | Identificatore della riga per la voce di prodotto. Il prodotto stesso è identificato tramite `product`. |
| `currencyCode` | [!UICONTROL Stringa] | La [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) codice valuta alfabetico utilizzato per determinare il prezzo del prodotto. |
| `discountAmount` | [!UICONTROL Doppio] | Se il prodotto viene scontato, ciò rappresenta la differenza tra il prezzo normale e il prezzo speciale del prodotto. |
| `name` | [!UICONTROL Stringa] | Nome visualizzato del prodotto presentato all’utente per la visualizzazione del prodotto. |
| `priceTotal` | [!UICONTROL Doppio] | Prezzo totale per l&#39;articolo della linea di prodotti. |
| `product` | [!UICONTROL Stringa] (URI) | URI `$id` dello schema XDM che acquisisce il prodotto stesso. |
| `productAddMethod` | [!UICONTROL Stringa] | Il metodo utilizzato dal visitatore per aggiungere un elemento prodotto all’elenco. |
| `productImageUrl` | [!UICONTROL Stringa] | Un URL per l’immagine principale del prodotto. |
| `quantity` | [!UICONTROL Intero] | Il numero di unità che il cliente ha indicato di aver bisogno del prodotto. |
| `unitOfMeasureCode` | [!UICONTROL Stringa] | Lo standard [codice unità di misura](https://ucum.org/ucum) per il prodotto in relazione al `quantity` proprietà. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati dell’indirizzo postale, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
