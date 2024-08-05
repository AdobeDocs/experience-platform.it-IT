---
keywords: Experience Platform;ricetta di acquisto prodotto;Data Science Workspace;argomenti popolari;ricette;ricetta pre-build
solution: Experience Platform
title: Ricetta previsione acquisto prodotto
description: La ricetta di previsione dell’acquisto del prodotto consente di prevedere la probabilità di un determinato tipo di evento di acquisto del cliente, ad esempio un acquisto di prodotto.
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 5%

---

# Ricetta di previsione dell’acquisto del prodotto

>[!NOTE]
>
>Data Science Area di lavoro non è più disponibile per l&#39;acquisto.
>
>Questa documentazione è destinata ai clienti esistenti con precedenti diritti a Data Science Area di lavoro.

La ricetta di previsione dell&#39;acquisto del prodotto consente di prevedere la probabilità di un determinato tipo di evento di acquisto del cliente, ad esempio un acquisto di un prodotto, ad istanza.

![](../images/pre-built-recipes/ppp_bigpicture.png)

Il seguente documento risponderà a domande quali:
* Per chi è costruita questa ricetta?
* Cosa fa questa ricetta?

## Per chi è costruita questa ricetta?

Il tuo marchio cerca di incrementare le vendite trimestrali per la tua linea di prodotti attraverso promozioni efficaci e mirate per i tuoi clienti. Tuttavia, non tutti i clienti sono simili e si desidera il valore dei vostri soldi. A chi si rivolge? Quale dei vostri clienti risponderà più probabilmente senza che la vostra promozione sia intrusiva? Come personalizzare le promozioni per ogni cliente? Su quali canali fare affidamento e quando è necessario inviare promozioni?

## Cosa fa questa ricetta?

La ricetta di previsione dell&#39;acquisto del prodotto utilizza l&#39;apprendimento automatico per prevedere il comportamento di acquisto dei clienti. A tale scopo, applica un classificatore di foreste casuali personalizzato e un Experience Data Model (XDM) a due livelli per prevedere la probabilità di un evento di acquisto. Il modello utilizza dati di input che incorporano informazioni sul profilo del cliente e cronologia degli acquisti passati e impostazioni predefinite su parametri di configurazione predeterminati determinati dai nostri Data Scientist per migliorare l&#39;accuratezza predittiva.

## Schema dati

Questa ricetta utilizza [schemi](../../xdm/home.md) XDM per modellare i dati. Lo schema utilizzato per questa ricetta è mostrato di seguito:

| Nome campo | Tipo |
| --- | --- |
| userId | Stringa |
| genderRatio | Numero |
| etàY | Numero |
| ageM | Numero |
| optinEmail | Booleano |
| optinMobile | Booleano |
| optinAddress | Booleano |
| creato | Intero |
| Ordini totali | Numero |
| Elementi totali | Numero |
| orderDate1 | Numero |
| shippingDate1 | Numero |
| totalPrice1 | Numero |
| Tasse1 | Numero |
| orderDate2 | Numero |
| shippingDate2 | Numero |
| Prezzo totale2 | Numero |


## Algoritmo

Innanzitutto, viene caricato il set di dati training nello *schema ProductPrediction* . Da qui, il modello viene addestrato utilizzando un [classificatore di foresta casuale](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). Il classificatore di foreste casuali è un tipo di algoritmo insieme che si riferisce a un algoritmo che combina più algoritmi per ottenere prestazioni predittive migliorate. L&#39;idea alla base dell&#39;algoritmo è che il classificatore di foreste casuali costruisce più alberi decisionali e li unisce per creare una previsione più accurata e stabile.

Questo processo inizia con la creazione di un set di alberi decisionali che seleziona in modo casuale sottoinsiemi di dati di addestramento. Successivamente, viene calcolata la media dei risultati di ciascun albero decisionale.
