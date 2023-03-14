---
keywords: Experience Platform;vendita al dettaglio ricetta;Data Science Workspace;argomenti popolari;ricette;ricetta pre-build
solution: Experience Platform
title: Ricetta vendita al dettaglio
description: La ricetta Vendite al dettaglio consente di prevedere le previsioni di vendita per tutti i negozi con seeding per un determinato periodo di tempo. Grazie a un accurato modello di previsione, il retailer è in grado di individuare la relazione tra la domanda e le politiche di prezzo e di ottimizzare le decisioni di prezzo per ottimizzare le vendite e i ricavi.
exl-id: ff01fcd1-fca6-4957-8470-a974fd1520aa
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 2%

---

# Ricetta vendite al dettaglio

La ricetta Vendite al dettaglio consente di prevedere le previsioni di vendita per tutti i negozi con seeding per un determinato periodo di tempo. Grazie a un accurato modello di previsione, il retailer è in grado di individuare la relazione tra la domanda e le politiche di prezzo e di ottimizzare le decisioni di prezzo per ottimizzare le vendite e i ricavi.

Il seguente documento risponderà a domande quali:
* Per chi è costruita questa ricetta?
* Che cosa fa questa ricetta?
* Come si inizia?

## Per chi è costruita questa ricetta?

Un retailer deve affrontare molte sfide per rimanere competitivo nel mercato attuale. Il tuo marchio cerca di incrementare le vendite annuali per il tuo marchio retail, ma devi prendere diverse decisioni per ridurre al minimo i costi operativi. Un&#39;offerta eccessiva aumenta i costi di inventario, mentre un&#39;offerta insufficiente aumenta il rischio di perdere clienti verso altre marche. È necessario ordinare più forniture per i prossimi mesi? Come puoi decidere un prezzo ottimale per i tuoi prodotti per mantenere gli obiettivi di vendita settimanali?

## Che cosa fa questa ricetta?

La ricetta Retail Sales Forecasting utilizza l’apprendimento automatico per prevedere le tendenze di vendita. La ricetta fa questo sfruttando la ricchezza di dati storici al dettaglio e il gradiente personalizzato aumentando l&#39;algoritmo di apprendimento automatico del regressore per prevedere le vendite una settimana in anticipo. Il modello utilizza la cronologia degli acquisti passati e utilizza i parametri di configurazione predefiniti determinati dai nostri data scientist per migliorare l’accuratezza predittiva.

## Come si inizia?

Per iniziare, segui questa pagina [esercitazione](../jupyterlab/create-a-model.md).

Questo tutorial illustra come creare la ricetta per la vendita al dettaglio in un notebook Jupyter e come utilizzare il flusso di lavoro blocco appunti per la composizione per creare la ricetta in Adobe Experience Platform.

## Schema dati

Questa ricetta utilizza [Schemi XDM](../../xdm/schema/field-dictionary.md) per modellare i dati. Lo schema utilizzato per questa ricetta è mostrato di seguito:

| Nome campo | Tipo |
| --- | --- |
| data | Stringa |
| archiviare | Intero |
| storeType | Stringa |
| weeklySales | Numero |
| storeSize | Intero |
| temperatura | Numero |
| regionalFuelPrice | Numero |
| markdown | Numero |
| cpi | Numero |
| disoccupazione | Numero |
| isHoliday | Booleano |


## Algoritmo

In primo luogo, il set di dati di formazione nel *DSWRetailSales* schema caricato. Da qui, il modello viene addestrato utilizzando un [algoritmo di regressione con potenziamento del gradiente](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html). Il potenziamento con gradiente utilizza l’idea che gli Allievi deboli (almeno leggermente migliori del caso casuale) possano formare una successione di Allievi focalizzati sul miglioramento delle debolezze dell’Allievo precedente. Insieme, possono essere utilizzati per creare un potente modello predittivo.

Il processo prevede tre elementi: una funzione di perdita, un allievo debole e un modello additivo.

La funzione di perdita si riferisce a una misura di quanto un modello predittivo faccia in termini di capacità di prevedere il risultato atteso; in questa ricetta viene utilizzata la regressione dei minimi quadrati.

Nel potenziamento del gradiente, come allievo debole viene utilizzato un albero decisionale. In genere, gli alberi con un numero limitato di livelli, nodi e divisioni vengono utilizzati per garantire che l’allievo rimanga debole.

Infine, viene utilizzato un modello additivo. Dopo aver calcolato la perdita con la funzione di perdita, l&#39;albero che riduce la perdita viene scelto e ponderato per migliorare la modellazione delle osservazioni più difficili. L&#39;output dell&#39;albero ponderato viene quindi aggiunto alla sequenza esistente di alberi per migliorare la produzione finale del modello - quantità di vendite future .
