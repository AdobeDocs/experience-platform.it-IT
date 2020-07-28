---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Ricetta di vendita al dettaglio
topic: overview
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 2%

---


# Ricetta di vendita al dettaglio

La ricetta Vendite al dettaglio consente di prevedere le previsioni di vendita per tutti i negozi preimpostati per un determinato periodo di tempo. Grazie a un modello di previsione accurato, il rivenditore sarà in grado di individuare la relazione tra le politiche di domanda e di prezzo e di prendere decisioni di prezzo ottimizzate per massimizzare le vendite e i ricavi.

Il seguente documento risponde a domande quali:
* Per chi è costruita questa ricetta?
* Cosa fa questa ricetta?
* Come si inizia?

## Per chi è costruita questa ricetta?

Un rivenditore deve affrontare molte sfide per rimanere competitivo nel mercato attuale. Il tuo marchio cerca di incrementare le vendite annuali per il tuo marchio retail, ma ci sono molte decisioni da prendere per ridurre al minimo i costi operativi. Un eccesso di offerta aumenta i costi di magazzino, mentre un eccesso di offerta aumenta il rischio di perdere clienti ad altri marchi. È necessario ordinare più forniture per i prossimi mesi? Come si decide il prezzo ottimale per i prodotti per mantenere gli obiettivi di vendita settimanali?

## Cosa fa questa ricetta?

La ricetta Retail Sales Forecasting utilizza l&#39;apprendimento automatico per prevedere le tendenze di vendita. La ricetta lo fa sfruttando la ricchezza di dati storici per il retail e l&#39;algoritmo di apprendimento automatico basato sul gradiente personalizzato che incrementa la regressione per prevedere le vendite con un anticipo di una settimana. Il modello utilizza la cronologia degli acquisti passati e utilizza per impostazione predefinita i parametri di configurazione predeterminati determinati dai nostri Data Scientist per migliorare la precisione predittiva.

## Come si inizia?

Per iniziare, segui questa [esercitazione](../jupyterlab/create-a-recipe.md).

Questa esercitazione passerà alla creazione della ricetta Vendite al dettaglio in un blocco appunti Jupyter e all&#39;utilizzo del blocco appunti per creare la ricetta in  Adobe Experience Platform.

## Schema dati

Questa ricetta utilizza gli schemi [](../../xdm/schema/field-dictionary.md) XDM per modellare i dati. Lo schema utilizzato per questa ricetta è riportato di seguito:

| Nome campo | Tipo |
--- | ---
| date | Stringa |
| store | Intero |
| storeType | Stringa |
| weekSales | Numero |
| storeSize | Intero |
| temperatura | Numero |
| RegionalFuelPrice | Numero |
| riduzione | Numero |
| cpi | Numero |
| disoccupazione | Numero |
| isHoliday | Booleano |


## Algoritmo

Innanzitutto, viene caricato il dataset di formazione nello schema *DSWRetailSales* . Da qui, il modello viene addestrato utilizzando un algoritmo [di regressione con](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html)gradiente. Il miglioramento della sfumatura utilizza l&#39;idea che gli utenti in formazione deboli (almeno leggermente migliori delle possibilità casuali) possano formare una serie di studenti focalizzati sul miglioramento delle debolezze degli studenti precedenti. Insieme, possono essere utilizzati per creare un potente modello predittivo.

Il processo comprende tre elementi: una funzione di perdita, uno studente debole e un modello additivo.

La funzione di perdita si riferisce a una misura di come un modello di previsione fa bene in termini di essere in grado di prevedere il risultato previsto - la regressione dei minimi quadrati è utilizzata in questa ricetta.

Nel potenziamento della sfumatura, una struttura decisionale viene utilizzata come studente debole. In genere, gli alberi con un numero limitato di livelli, nodi e divisioni vengono utilizzati per assicurare che lo studente rimanga debole.

Infine, viene utilizzato un modello additivo. Dopo aver calcolato la perdita con la funzione di perdita, l&#39;albero che riduce la perdita è scelto e ponderato per migliorare la modellazione delle osservazioni più difficili. L&#39;output dell&#39;albero ponderato viene quindi aggiunto alla sequenza esistente di alberi per migliorare la produzione finale del modello - quantità di vendite future.