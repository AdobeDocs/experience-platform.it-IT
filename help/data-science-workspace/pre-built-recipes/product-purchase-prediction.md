---
keywords: Experience Platform;ricetta di acquisto prodotto;Data Science Workspace;argomenti popolari;ricette;ricetta pre-build
solution: Experience Platform
title: Ricetta previsione acquisto prodotto
description: La ricetta di previsione dell’acquisto del prodotto consente di prevedere la probabilità di un determinato tipo di evento di acquisto del cliente, ad esempio un acquisto di prodotto.
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 5%

---

# Ricetta di previsione dell’acquisto del prodotto

La ricetta di previsione dell’acquisto del prodotto consente di prevedere la probabilità di un determinato tipo di evento di acquisto del cliente, ad esempio un acquisto di prodotto.

![](../images/pre-built-recipes/ppp_bigpicture.png)

Il seguente documento risponderà a domande quali:
* Per chi è costruita questa ricetta?
* Che cosa fa questa ricetta?

## Per chi è costruita questa ricetta?

Il tuo marchio cerca di incrementare le vendite trimestrali per la tua linea di prodotti attraverso promozioni efficaci e mirate per i tuoi clienti. Tuttavia, non tutti i clienti sono simili e si desidera il valore dei vostri soldi. A chi si rivolge? Quale dei vostri clienti risponderà più probabilmente senza che la vostra promozione sia intrusiva? Come personalizzare le promozioni per ogni cliente? Su quali canali fare affidamento e quando è necessario inviare promozioni?

## Che cosa fa questa ricetta?

La ricetta di Previsione dell’acquisto del prodotto utilizza l’apprendimento automatico per prevedere il comportamento d’acquisto del cliente. A tal fine, applica un classificatore di foresta casuale personalizzato e un Experience Data Model (XDM) a due livelli per prevedere la probabilità di un evento di acquisto. Il modello utilizza i dati di input che incorporano le informazioni del profilo cliente e la cronologia degli acquisti passati; per migliorare l’accuratezza predittiva, utilizza i parametri di configurazione predefiniti determinati dai nostri data scientist.

## Schema dati

Questa ricetta utilizza [schemi XDM](../../xdm/home.md) per modellare i dati. Lo schema utilizzato per questa ricetta è mostrato di seguito:

| Nome campo | Tipo |
| --- | --- |
| userId | Stringa |
| genderRatio | Numero |
| ageY | Numero |
| ageM | Numero |
| optinEmail | Booleano |
| optinMobile | Booleano |
| optinAddress | Booleano |
| creato | Intero |
| totalOrders | Numero |
| totalItems | Numero |
| orderDate1 | Numero |
| shippingDate1 | Numero |
| totalPrice1 | Numero |
| imposta1 | Numero |
| orderDate2 | Numero |
| shippingDate2 | Numero |
| totalPrice2 | Numero |


## Algoritmo

Innanzitutto, viene caricato il set di dati di formazione nello schema *ProductPrediction*. Da qui, il modello viene addestrato utilizzando un [classificatore di foresta casuale](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). Il classificatore di foresta casuale è un tipo di algoritmo integrato che fa riferimento a un algoritmo che combina più algoritmi per ottenere prestazioni predittive migliorate. L&#39;idea alla base dell&#39;algoritmo è che il classificatore casuale di foresta costruisce più alberi decisionali e li unisce per creare una previsione più precisa e stabile.

Questo processo inizia con la creazione di un set di alberi decisionali che seleziona in modo casuale sottoinsiemi di dati di addestramento. Successivamente, viene calcolata la media dei risultati di ciascun albero decisionale.
