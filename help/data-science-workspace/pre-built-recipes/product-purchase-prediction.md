---
keywords: Experience Platform;product purchase recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Ricetta di acquisto del prodotto
topic: overview
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 6%

---


# Ricetta di acquisto del prodotto

## Panoramica

La ricetta Predizione di acquisto del prodotto consente di prevedere la probabilità di un determinato tipo di evento di acquisto del cliente, ad esempio un acquisto di prodotto.

![](../images/pre-built-recipes/ppp_bigpicture.png)

Il seguente documento risponde a domande quali:
* Per chi è costruita questa ricetta?
* Cosa fa questa ricetta?

## Per chi è costruita questa ricetta?

Il tuo marchio cerca di incrementare le vendite trimestrali per la tua linea di prodotti attraverso promozioni efficaci e mirate per i tuoi clienti. Tuttavia, non tutti i clienti sono uguali e vuoi che il tuo denaro valga. Chi è il bersaglio? Quale cliente è più propenso a rispondere senza trovare invadente la tua promozione? Come si personalizzano le promozioni per ogni cliente? Su quali canali dovreste fare affidamento e quando dovreste inviare le promozioni?

## Cosa fa questa ricetta?

La ricetta Predizione acquisto prodotto utilizza l&#39;apprendimento automatico per prevedere il comportamento di acquisto del cliente. A tal fine, applica un classificatore di foresta casuale personalizzato e un modello dati esperienza a due livelli (XDM) per prevedere la probabilità di un evento di acquisto. Il modello utilizza i dati di input che includono le informazioni sul profilo del cliente e la cronologia degli acquisti passati e i parametri di configurazione predefiniti determinati dai nostri Data Scientist per migliorare la precisione predittiva.

## Schema dati

Questa ricetta utilizza gli schemi [](../../xdm/home.md) XDM per modellare i dati. Lo schema utilizzato per questa ricetta è riportato di seguito:

| Nome campo | Tipo |
--- | ---
| userId | Stringa |
| genderRatio | Numero |
| ageY | Numero |
| ageM | Numero |
| optinEmail | Booleano |
| optinMobile | Booleano |
| optinAddress | Booleano |
| created | Intero |
| totalOrders | Numero |
| totalItems | Numero |
| orderDate1 | Numero |
| shippingDate1 | Numero |
| totalPrice1 | Numero |
| tax1 | Numero |
| orderDate2 | Numero |
| shippingDate2 | Numero |
| totalPrice2 | Numero |


## Algoritmo

Innanzitutto, viene caricato il dataset di formazione nello schema *ProductPredizione* . Da qui, il modello viene addestrato utilizzando un classificatore [Foresta](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)casuale. Il classificatore della foresta casuale è un tipo di algoritmo di ensembled che fa riferimento a un algoritmo che combina più algoritmi per ottenere prestazioni predittive migliorate. L&#39;idea alla base dell&#39;algoritmo è che il classificatore casuale della foresta crea più alberi decisionali e li unisce per creare una previsione più accurata e stabile.

Questo processo inizia con la creazione di una serie di strutture decisionali che selezionano in modo casuale sottoinsiemi di dati di formazione. In seguito, i risultati di ogni albero decisionale vengono calcolati come media.