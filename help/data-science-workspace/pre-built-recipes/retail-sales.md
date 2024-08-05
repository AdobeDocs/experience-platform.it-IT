---
keywords: Experience Platform; ricetta di vendita al dettaglio; Data Science Area di lavoro; argomenti popolari; Ricette; pre versione ricetta
solution: Experience Platform
title: Ricetta di vendita al dettaglio
description: La ricetta delle vendite al dettaglio consente di prevedere i previsione di vendita per tutti i negozi seminati per un determinato periodo di tempo. Con un modello di previsione accurato, il rivenditore sarebbe in grado di trovare la relazione tra domanda e politiche dei prezzi e prendere decisioni sui prezzi ottimizzate per massimizzare le vendite e le entrate.
exl-id: ff01fcd1-fca6-4957-8470-a974fd1520aa
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 2%

---

# Ricetta di vendita al dettaglio

>[!NOTE]
>
>Data Science Area di lavoro non è più disponibile per l&#39;acquisto.
>
>Questa documentazione è destinata ai clienti esistenti con precedenti diritti a Data Science Area di lavoro.

La ricetta delle vendite al dettaglio consente di prevedere i previsione di vendita per tutti i negozi seminati per un determinato periodo di tempo. Con un modello di previsione accurato, il rivenditore sarebbe in grado di trovare la relazione tra domanda e politiche dei prezzi e prendere decisioni sui prezzi ottimizzate per massimizzare le vendite e le entrate.

Il seguente documento risponderà a domande quali:
* Per chi è costruita questa ricetta?
* Che cosa fa questa ricetta?
* Come si inizia?

## Per chi è costruita questa ricetta?

Un retailer deve affrontare molte sfide per rimanere competitivo nel mercato attuale. Il tuo marchio cerca di aumentare le vendite annuali per i tuoi marchio di vendita al dettaglio, ma ci sono molte decisioni da prendere per ridurre al minimo i costi operativi. Un&#39;offerta eccessiva aumenta i costi di inventario, mentre un&#39;offerta insufficiente aumenta il rischio di perdere clienti verso altre marche. Hai bisogno di ordinare più forniture per i prossimi mesi? Come decidi il prezzo ottimale per i tuoi prodotti per mantenere gli obiettivi di vendita settimanali?

## Che cosa fa questa ricetta?

La ricetta Retail Sales Forecasting utilizza l’apprendimento automatico per prevedere le tendenze di vendita. La ricetta fa questo sfruttando la ricchezza di dati storici al dettaglio e il gradiente personalizzato aumentando l&#39;algoritmo di apprendimento automatico del regressore per prevedere le vendite una settimana in anticipo. Il modello utilizza la cronologia degli acquisti passati e utilizza i parametri di configurazione predefiniti determinati dai nostri data scientist per migliorare l’accuratezza predittiva.

## Come si inizia?

Puoi iniziare seguendo questo [esercitazione](../jupyterlab/create-a-model.md).

Questo esercitazione esaminerà la creazione della ricetta di vendita al dettaglio in un Jupyter Notebook e l&#39;utilizzo del blocco appunti per workflow per creare la ricetta in Adobe Experience Platform.

## Schema dati

Questa ricetta utilizza [schemi](../../xdm/schema/field-dictionary.md) XDM per modellare i dati. Lo schema utilizzato per questa ricetta è mostrato di seguito:

| Nome campo | Tipo |
| --- | --- |
| dattero | Stringa |
| negozio | Intero |
| storeType | Stringa |
| weeklySales | Numero |
| storeSize | Intero |
| temperatura | Numero |
| regionalFuelPrice | Numero |
| markdown | Numero |
| Cpi | Numero |
| disoccupazione | Numero |
| isHoliday | Booleano |


## Algoritmo

Innanzitutto, viene caricato il set di dati di formazione nello schema *DSWRetailSales*. Da qui, il modello viene addestrato utilizzando un algoritmo regressore [gradiente potenziato](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html). Il potenziamento con gradiente utilizza l’idea che gli Allievi deboli (almeno leggermente migliori del caso casuale) possano formare una successione di Allievi focalizzati sul miglioramento delle debolezze dell’Allievo precedente. Insieme, possono essere utilizzati per creare un potente modello predittivo.

Il processo prevede tre elementi: una funzione di perdita, un allievo debole e un modello additivo.

La funzione di perdita si riferisce a un misurare di quanto bene fa un modello di previsione in termini di essere in grado di prevedere il risultato atteso - la regressione dei minimi quadrati viene utilizzata in questa ricetta.

Nel potenziamento del gradiente, come allievo debole viene utilizzato un albero decisionale. In genere, gli alberi con un numero limitato di livelli, nodi e divisioni vengono utilizzati per garantire che l’allievo rimanga debole.

Infine, viene utilizzato un modello additivo. Dopo aver calcolato la perdita con la funzione di perdita, l&#39;albero che riduce la perdita viene scelto e ponderato per migliorare la modellazione delle osservazioni più difficili. L&#39;output dell&#39;albero ponderato viene quindi aggiunto alla sequenza esistente di alberi per migliorare la produzione finale del modello - quantità di vendite future .
