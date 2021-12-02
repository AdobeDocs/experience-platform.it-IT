---
keywords: Experience Platform;ricetta vendite al dettaglio;Data Science Workspace;argomenti popolari;ricette;precostruire ricetta
solution: Experience Platform
title: Ricetta vendite al dettaglio
topic-legacy: overview
description: La ricetta Vendite al dettaglio consente di prevedere le previsioni di vendita per tutti i negozi predefiniti per un determinato periodo di tempo. Con un modello di previsione accurato, il rivenditore sarebbe in grado di trovare il rapporto tra le politiche di domanda e di prezzo e di prendere decisioni di prezzo ottimizzate per massimizzare le vendite e i ricavi.
exl-id: ff01fcd1-fca6-4957-8470-a974fd1520aa
source-git-commit: 38c493e6306e493f4ef5caf90509bda6f4d80023
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 2%

---

# Ricetta di vendita al dettaglio

La ricetta Vendite al dettaglio consente di prevedere le previsioni di vendita per tutti i negozi predefiniti per un determinato periodo di tempo. Con un modello di previsione accurato, il rivenditore sarebbe in grado di trovare il rapporto tra le politiche di domanda e di prezzo e di prendere decisioni di prezzo ottimizzate per massimizzare le vendite e i ricavi.

Il seguente documento risponderà a domande quali:
* Per chi è costruita questa ricetta?
* Cosa fa questa ricetta?
* Come inizio?

## Per chi è costruita questa ricetta?

Un retailer deve affrontare molte sfide per rimanere competitivo nel mercato attuale. Il tuo marchio cerca di incrementare le vendite annuali per il tuo marchio retail, ma ci sono molte decisioni da prendere per ridurre al minimo i costi operativi. L&#39;eccesso di offerta aumenta i costi di inventario, mentre l&#39;offerta insufficiente aumenta il rischio di perdere clienti ad altri marchi. È necessario ordinare più forniture per i prossimi mesi? Come si decide il prezzo ottimale per i prodotti per mantenere gli obiettivi di vendita settimanali?

## Cosa fa questa ricetta?

La ricetta Retail Sales Forecasting utilizza l&#39;apprendimento automatico per prevedere le tendenze di vendita. La ricetta lo fa sfruttando la ricchezza di dati storici al dettaglio e l&#39;algoritmo di apprendimento automatico personalizzato che incrementa la regressione delle vendite per prevedere le vendite con una settimana di anticipo. Il modello utilizza la cronologia degli acquisti passati e utilizza per impostazione predefinita parametri di configurazione predefiniti determinati dai nostri data scientist per migliorare la precisione predittiva.

## Come inizio?

Per iniziare, segui questo [tutorial](../jupyterlab/create-a-model.md).

Questa esercitazione passerà alla creazione della ricetta Vendite al dettaglio in un blocco appunti Jupyter e all&#39;utilizzo del blocco appunti per creare il flusso di lavoro della ricetta in Adobe Experience Platform.

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
| RegionalFuelPrice | Numero |
| markdown | Numero |
| cpi | Numero |
| disoccupazione | Numero |
| isHoliday | Booleano |


## Algoritmo

In primo luogo, il set di dati sulla formazione nel *DSWRetailSales* schema caricato. Da qui, il modello viene addestrato utilizzando un [algoritmo di regressione di incremento della sfumatura](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html). Il miglioramento della sfumatura utilizza l&#39;idea che gli studenti deboli (almeno leggermente meglio del caso casuale) possono formare una serie di studenti concentrati sul miglioramento delle debolezze dello studente precedente. Insieme, possono essere utilizzati per creare un potente modello predittivo.

Il processo comprende tre elementi: una funzione di perdita, uno studente debole e un modello additivo.

La funzione di perdita si riferisce a una misura di quanto un modello di previsione fa bene in termini di essere in grado di prevedere il risultato previsto - la regressione dei minimi quadrati viene utilizzata in questa ricetta.

In aumento del gradiente, un albero decisionale viene utilizzato come studente debole. In genere, gli alberi con un numero limitato di livelli, nodi e suddivisioni vengono utilizzati per garantire che lo studente rimanga debole.

Infine, viene utilizzato un modello additivo. Dopo aver calcolato la perdita con la funzione di perdita, l&#39;albero che riduce la perdita viene scelto e ponderato per migliorare la modellazione delle osservazioni più difficili. L&#39;output dell&#39;albero ponderato viene quindi aggiunto alla sequenza esistente di alberi per migliorare la produzione finale del modello - quantità di vendite future.
