---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;indirizzo;xdm:address;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo di dati elemento elenco prodotti
description: Scopri il tipo di dati XDM per l’elemento dell’elenco dei prodotti.
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 3%

---

# [!UICONTROL Elemento dell’elenco prodotti] tipo di dati

[!UICONTROL Elemento dell’elenco prodotti] è un tipo di dati XDM standard che descrive un prodotto selezionato da un cliente con opzioni, prezzi e contesto di utilizzo specifici per un momento specifico.

I valori acquisiti in questo tipo di dati possono differire dal record del prodotto. Ad esempio, il record del prodotto contiene dettagli del sistema di informazioni sul prodotto coerenti per tutti i clienti, in cui l’elemento dell’elenco prodotti presenta il prezzo effettivo offerto al cliente al momento dell’acquisto, che può variare a causa di campagne di vendita o prezzi stagionali.

![](../images/data-types/product-list-item.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `selectedOptions` | Array di oggetti | Contiene le opzioni personalizzate scelte per un prodotto configurabile. Ogni voce di elenco è un oggetto con le seguenti proprietà:<ul><li>`attribute`: nome per l’attributo configurabile.</li><li>`value`: valore dell’attributo.</li></ul> |
| `SKU` | [!UICONTROL Stringa] | Stock Keeping Unit (SKU), l’identificatore univoco di un prodotto definito dal fornitore. |
| `_id` | [!UICONTROL Stringa] | L’identificatore di riga per questa voce di prodotto. Il prodotto stesso è identificato tramite `product`. |
| `currencyCode` | [!UICONTROL Stringa] | Il [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) codice valuta alfabetico utilizzato per la determinazione del prezzo del prodotto. |
| `discountAmount` | [!UICONTROL Doppio] | Se il prodotto è scontato, ciò rappresenta la differenza tra il prezzo regolare e il prezzo speciale del prodotto. |
| `name` | [!UICONTROL Stringa] | Il nome visualizzato del prodotto presentato all’utente per questa visualizzazione prodotto. |
| `priceTotal` | [!UICONTROL Doppio] | Il prezzo totale per la voce di prodotto. |
| `product` | [!UICONTROL Stringa] (URI) | URI `$id` dello schema XDM che acquisisce il prodotto stesso. |
| `productAddMethod` | [!UICONTROL Stringa] | Il metodo utilizzato dal visitatore per aggiungere un elemento di prodotto all’elenco. |
| `productImageUrl` | [!UICONTROL Stringa] | Un URL per l’immagine principale del prodotto. |
| `quantity` | [!UICONTROL Intero] | Il numero di unità del prodotto che il cliente ha indicato di richiedere. |
| `unitOfMeasureCode` | [!UICONTROL Stringa] | Lo standard [codice dell’unità di misura](https://ucum.org/ucum) per il prodotto in relazione al `quantity` proprietà. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati dell’indirizzo postale, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
