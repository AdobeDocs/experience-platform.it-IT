---
title: Tipo di dati di ricerca del sito interno
description: Questo documento fornisce una panoramica del tipo di dati XDM di Internal Site Search.
source-git-commit: eaea904ddda6b7ffee6f52cd4af897c2a8885714
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---

# [!UICONTROL Ricerca sito interna] tipo di dati

[!UICONTROL Ricerca sito interna] è un tipo di dati XDM standard che descrive una ricerca interna del sito, inclusi tutti i relativi comportamenti e dettagli di ricerca.

![](../images/data-types/internal-site-search.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `autoCompleteClicked` | [!UICONTROL Booleano] | Indica se un visitatore ha utilizzato un valore di ricerca suggerito o completato automaticamente per eseguire la ricerca. |
| `autoCompleteTypedValue` | [!UICONTROL Stringa] | Per gli scenari di completamento automatico, a volte gli utenti abbandonano la ricerca e selezionano un termine specifico dal menu a discesa. Questo valore tiene traccia di ciò che l’utente ha iniziato a digitare per generare il set specifico di termini di ricerca suggeriti. |
| `autoCompleteValue` | [!UICONTROL Stringa] | Per gli scenari di completamento automatico, a volte gli utenti abbandonano la ricerca e selezionano un termine specifico dal menu a discesa. Questo valore viene utilizzato per tenere traccia dei termini specifici selezionati. |
| `instances` | [!UICONTROL Intero] | Il numero di volte in cui si è verificata la ricerca interna del sito. |
| `locationInPage` | [!UICONTROL Stringa] | Quando sulla pagina sono presenti più caselle di ricerca, questo valore deve essere utilizzato per identificare la posizione specifica utilizzata dall’utente per la ricerca. |
| `nullInstances` | [!UICONTROL Intero] | Numero di volte in cui si è verificata la ricerca interna del sito che ha fornito risultati pari a zero. |
| `numberOfResults` | [!UICONTROL Intero] | Numero totale di risultati di ricerca restituiti. |
| `postalCode` | [!UICONTROL Stringa] | Il codice postale utilizzato per la ricerca, se applicabile. |
| `productFindingMethods` | [!UICONTROL Stringa] | Valore interno del termine di ricerca del sito con binding di merchandising. Questo valore indica il termine ricercato immediatamente prima di visualizzare un prodotto. |
| `radiusDistance` | [!UICONTROL Intero] | Combinato con `radiusType`, indica la distanza selezionata del raggio di ricerca. |
| `radiusType` | [!UICONTROL Intero] | Il tipo di distanza selezionato di `radiusDistance`, chilometri o chilometri. |
| `refinementInstances` | [!UICONTROL Intero] | Il numero di volte in cui la ricerca interna del sito è stata perfezionata. |
| `refinementType` | Matrice di stringhe | Elenca i tipi di perfezionamento applicati ai risultati della ricerca. Gli esempi includono reparto, marchio, prezzo, negozio, valutazione della revisione, colore, materiale e così via. |
| `refinementValue` | [!UICONTROL Stringa] | Il valore in cui è stata perfezionata la ricerca. |
| `resultsPageNumber` | [!UICONTROL Intero] | Per i risultati di ricerca impaginati, questo valore tiene traccia della pagina dei risultati che il visitatore sta visualizzando. |
| `resultsPerPage` | [!UICONTROL Intero] | Per i risultati di ricerca impaginati, questo valore tiene traccia del numero di risultati di ricerca visualizzati per pagina. |
| `searchType` | [!UICONTROL Stringa] | Acquisisce il metodo di ricerca da eseguire, se applicabile. Gli esempi possono includere una ricerca tipo-avanti, una ricerca digitata direttamente o qualsiasi altro tipo di funzionalità di ricerca personalizzata di un sito. |
| `sortOrder` | [!UICONTROL Stringa] | Combinato con `sortType`, indica l’ordinamento dei risultati della ricerca, crescente o decrescente. |
| `term` | [!UICONTROL Stringa] | Il termine interno di ricerca del sito immesso dal visitatore. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta la [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/internal-site-search.schema.json).
