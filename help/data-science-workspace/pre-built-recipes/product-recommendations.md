---
keywords: ' Experience Platform;raccomandazione prodotto;Data Science Workspace;argomenti popolari;ricette;pre-costruire ricetta'
solution: Experience Platform
title: Ricetta raccomandazione prodotto
topic: overview
description: La ricetta Recommendations per i prodotti consente di fornire raccomandazioni sui prodotti personalizzate in base alle esigenze e agli interessi dei clienti. Con un modello di previsione accurato, la cronologia degli acquisti di un cliente può fornire informazioni su quali prodotti potrebbero essere interessati.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 2%

---


# Ricetta raccomandazione prodotto

La ricetta Recommendations per i prodotti consente di fornire raccomandazioni sui prodotti personalizzate in base alle esigenze e agli interessi dei clienti. Con un modello di previsione accurato, la cronologia degli acquisti di un cliente può fornire informazioni su quali prodotti potrebbero essere interessati.

## Per chi è costruita questa ricetta?

Al giorno d&#39;oggi, un rivenditore può offrire una moltitudine di prodotti, offrendo ai propri clienti molte scelte che possono anche ostacolare la ricerca dei propri clienti. A causa di vincoli di tempo e fatica, i clienti potrebbero non trovare il prodotto che desiderano, dando luogo ad acquisti con un alto livello di dissonanza cognitiva o nessun acquisto.

## Cosa fa questa ricetta?

La ricetta Recommendations per i prodotti utilizza l&#39;apprendimento automatico per analizzare le interazioni tra un cliente e i prodotti del passato e generare un elenco personalizzato di raccomandazioni sui prodotti in modo rapido e semplice. Questo ottimizza il processo di scoperta del prodotto ed elimina le lunghe, improduttive ricerche irrilevanti per i clienti. Di conseguenza, la ricetta Recommendations prodotto può migliorare l&#39;esperienza di acquisto complessiva di un cliente, aumentando il coinvolgimento e rafforzando la fedeltà al marchio.

## Come si inizia?

Per iniziare, segui l&#39;esercitazione Adobe Experience Platform Lab (vedi collegamento Lab qui sotto). Questa esercitazione illustra come creare la ricetta Recommendations prodotto in un blocco appunti Jupyter seguendo il flusso di lavoro [notebook per la ricetta](../jupyterlab/create-a-recipe.md) e implementando la ricetta in [!DNL Experience Platform] [!DNL Data Science Workspace].

* [Lab: Predicare il futuro con Data Science Workspace](https://expleague.azureedge.net/labs/L777/index.html)
* [Risorse Lab](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Schema dati

Questa ricetta utilizza schemi [XDM ](../../xdm/schema/field-dictionary.md) personalizzati per modellare i dati di input e output:

### Schema dati di input

| Nome campo | Tipo |
--- | ---
| itemId | Stringa |
| actionType | Stringa |
| timestamp | Stringa |
| userId | Stringa |

### Schema dati di output

| Nome campo | Tipo |
--- | ---
| Recommendations | Stringa |
| userId | Intero |

## Algoritmo

La ricetta Product Recommendations utilizza il filtraggio collaborativo per generare un elenco personalizzato di raccomandazioni sui prodotti per i clienti. I filtri collaborativi, a differenza di un approccio basato sui contenuti, non richiedono informazioni su un prodotto specifico ma utilizzano le preferenze storiche di un cliente su un set di prodotti. Questa potente tecnica di raccomandazione utilizza due semplici presupposti:
* Ci sono clienti con interessi simili, e possono essere raggruppati confrontando i loro comportamenti di acquisto e navigazione.
* È più probabile che un cliente sia interessato a una raccomandazione basata su clienti simili in termini di comportamento di acquisto e navigazione.

Questo processo è suddiviso in due fasi principali. Innanzitutto, definite un sottoinsieme di clienti simili. Quindi, all&#39;interno di tale insieme, identificate funzioni simili tra i clienti al fine di restituire una raccomandazione per il cliente target.