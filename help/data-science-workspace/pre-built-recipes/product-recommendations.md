---
keywords: Experience Platform;ricetta consigli prodotto;Data Science Workspace;argomenti popolari;ricette;ricetta pre-build
solution: Experience Platform
title: Ricetta consigli prodotto
description: La ricetta Product Recommendations ti consente di fornire consigli di prodotto personalizzati e personalizzati in base alle esigenze e agli interessi del cliente. Con un modello di previsione accurato, la cronologia degli acquisti di un cliente può fornire informazioni sui prodotti che potrebbe essere interessato.
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 3%

---

# Ricetta per consigli sui prodotti

La ricetta Product Recommendations ti consente di fornire consigli di prodotto personalizzati e personalizzati in base alle esigenze e agli interessi del cliente. Con un modello di previsione accurato, la cronologia degli acquisti di un cliente può fornire informazioni sui prodotti che potrebbe essere interessato.

## Per chi è costruita questa ricetta?

Nei giorni nostri, un rivenditore può offrire una moltitudine di prodotti, dando ai loro clienti un sacco di scelte che possono anche ostacolare la ricerca dei loro clienti. A causa di vincoli di tempo e fatica, i clienti potrebbero non trovare il prodotto che desiderano, con conseguente acquisto con un alto livello di dissonanza cognitiva o nessun acquisto.

## Che cosa fa questa ricetta?

La ricetta Product Recommendations utilizza l’apprendimento automatico per analizzare le interazioni di un cliente con i prodotti del passato e generare un elenco personalizzato di consigli di prodotti in modo rapido e semplice. In questo modo è possibile ottimizzare il processo di rilevamento dei prodotti ed eliminare le ricerche lunghe, improduttive e irrilevanti per i clienti. Di conseguenza, la ricetta Product Recommendations può migliorare l’esperienza di acquisto complessiva di un cliente, aumentando il coinvolgimento e la fedeltà al marchio.

## Come si inizia?

Per iniziare, segui l’esercitazione di Adobe Experience Platform Lab (consulta il collegamento Lab di seguito). Questa esercitazione ti mostrerà come creare la ricetta Product Recommendations in un notebook Jupyter seguendo [da blocco appunti a ricetta](../jupyterlab/create-a-model.md) e implementazione della ricetta in [!DNL Experience Platform] [!DNL Data Science Workspace].

* [Lab: prevedere il futuro con Data Science Workspace](https://expleague.azureedge.net/labs/L777/index.html)
* [Risorse di laboratorio](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Schema dati

Questa ricetta utilizza personalizzati [Schemi XDM](../../xdm/schema/field-dictionary.md) per modellare i dati di input e output:

### Schema dati di input

| Nome campo | Tipo |
| --- | --- |
| itemId | Stringa |
| interfaceType | Stringa |
| timestamp | Stringa |
| userId | Stringa |

### Schema dati di output

| Nome campo | Tipo |
| --- | --- |
| consigli | Stringa |
| userId | Intero |

## Algoritmo

La ricetta del Recommendations di prodotto utilizza il filtro collaborativo per generare un elenco personalizzato di consigli di prodotto per i clienti. Il filtro collaborativo, a differenza di un approccio basato sui contenuti, non richiede informazioni su un prodotto specifico, ma utilizza piuttosto le preferenze storiche di un cliente su un set di prodotti. Questa potente tecnica di raccomandazione utilizza due semplici presupposti:
* Esistono clienti con interessi simili e possono essere raggruppati confrontando i loro comportamenti di acquisto e navigazione.
* È più probabile che un cliente sia interessato a un consiglio basato su clienti simili in termini di comportamento di acquisto e navigazione.

Questo processo è suddiviso in due fasi principali. Innanzitutto, definisci un sottoinsieme di clienti simili. Quindi, all’interno di tale set, identifica funzionalità simili tra tali clienti al fine di restituire un consiglio per il cliente target.
