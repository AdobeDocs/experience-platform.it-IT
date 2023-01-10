---
keywords: Experience Platform;ricetta di acquisto del prodotto;Data Science Workspace;argomenti popolari;ricette;precostruire ricetta
solution: Experience Platform
title: Ricetta previsione acquisto prodotti
description: La ricetta Predizione di acquisto del prodotto ti consente di prevedere la probabilità di un certo tipo di evento di acquisto del cliente, ad esempio un acquisto di prodotto.
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 6%

---

# Ricetta di previsione per l&#39;acquisto di prodotti

La ricetta Predizione di acquisto del prodotto ti consente di prevedere la probabilità di un certo tipo di evento di acquisto del cliente, ad esempio un acquisto di prodotto.

![](../images/pre-built-recipes/ppp_bigpicture.png)

Il seguente documento risponderà a domande quali:
* Per chi è costruita questa ricetta?
* Cosa fa questa ricetta?

## Per chi è costruita questa ricetta?

Il tuo marchio cerca di incrementare le vendite trimestrali per la tua linea di prodotti attraverso promozioni efficaci e mirate per i tuoi clienti. Tuttavia, non tutti i clienti sono uguali e si desidera che il vostro denaro vale. Chi target? Quale dei vostri clienti è più propenso a rispondere senza trovare intrusiva la vostra promozione? Come personalizzare le promozioni per ogni cliente? Su quali canali si deve fare affidamento e quando si devono inviare le promozioni?

## Cosa fa questa ricetta?

La ricetta Predizione di acquisto del prodotto utilizza l&#39;apprendimento automatico per prevedere il comportamento di acquisto del cliente. A tal fine, applica un classificatore di foresta casuale personalizzato e un modello di dati di esperienza a due livelli (XDM) per prevedere la probabilità di un evento di acquisto. Il modello utilizza i dati di input che incorporano le informazioni sul profilo del cliente e la cronologia degli acquisti passati e utilizza per impostazione predefinita parametri di configurazione predefiniti determinati dai nostri data scientist per migliorare la precisione predittiva.

## Schema dati

Questa ricetta utilizza [Schemi XDM](../../xdm/home.md) per modellare i dati. Lo schema utilizzato per questa ricetta è mostrato di seguito:

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
| tax1 | Numero |
| orderDate2 | Numero |
| shippingDate2 | Numero |
| totalPrice2 | Numero |


## Algoritmo

In primo luogo, il set di dati sulla formazione nel *Predizione prodotto* schema caricato. Da qui, il modello viene addestrato utilizzando un [classificatore di foresta casuale](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). Classificatore di foresta casuale è un tipo di algoritmo di raggruppamento che fa riferimento a un algoritmo che combina più algoritmi per ottenere prestazioni predittive migliorate. L&#39;idea alla base dell&#39;algoritmo è che il classificatore Foresta casuale costruisce più alberi decisionali e li unisce per creare una previsione più accurata e stabile.

Questo processo inizia con la creazione di un insieme di alberi decisionali che selezionano casualmente sottoinsiemi di dati di formazione. In seguito, i risultati di ogni albero decisionale sono in media.
