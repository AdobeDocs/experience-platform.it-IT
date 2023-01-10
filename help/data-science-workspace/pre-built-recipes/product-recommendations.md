---
keywords: Experience Platform;ricetta di consigli di prodotto;Data Science Workspace;argomenti popolari;ricette;pregenerare ricetta
solution: Experience Platform
title: Ricetta consigli prodotti
description: La ricetta Recommendations per i prodotti ti consente di fornire consigli di prodotti personalizzati che siano personalizzati in base alle esigenze e agli interessi del cliente. Con un modello di previsione accurato, la cronologia degli acquisti di un cliente può fornire informazioni su quali prodotti potrebbe essere interessato.
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 3%

---

# Ricetta di consigli sul prodotto

La ricetta Recommendations per i prodotti ti consente di fornire consigli di prodotti personalizzati che siano personalizzati in base alle esigenze e agli interessi del cliente. Con un modello di previsione accurato, la cronologia degli acquisti di un cliente può fornire informazioni su quali prodotti potrebbe essere interessato.

## Per chi è costruita questa ricetta?

Al giorno d&#39;oggi, un rivenditore può offrire una moltitudine di prodotti, dando ai suoi clienti un sacco di scelte che possono anche ostacolare la ricerca dei loro clienti. A causa di vincoli di tempo e fatica, i clienti potrebbero non trovare il prodotto desiderato, con conseguente acquisto con un alto livello di dissonanza cognitiva o nessun acquisto affatto.

## Cosa fa questa ricetta?

La ricetta Product Recommendations utilizza l’apprendimento automatico per analizzare le interazioni di un cliente con i prodotti in passato e generare un elenco personalizzato di consigli sui prodotti in modo rapido e semplice. Questo ottimizza il processo di individuazione dei prodotti ed elimina le ricerche lunghe, improduttive e irrilevanti per i clienti. Di conseguenza, la ricetta Recommendations per i prodotti può migliorare l&#39;esperienza complessiva di acquisto di un cliente, portando a un maggiore coinvolgimento e a una maggiore fedeltà al marchio.

## Come inizio?

Per iniziare, segui l&#39;esercitazione Adobe Experience Platform Lab (vedi il link Lab qui sotto). Questa esercitazione ti mostrerà come creare la ricetta Recommendations del prodotto in un blocco appunti Jupyter seguendo la [taccuino a ricetta](../jupyterlab/create-a-model.md) e implementazione della ricetta in [!DNL Experience Platform] [!DNL Data Science Workspace].

* [Laboratorio: Prevedere il futuro con Data Science Workspace](https://expleague.azureedge.net/labs/L777/index.html)
* [Risorse Lab](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Schema dati

Questa ricetta utilizza [Schemi XDM](../../xdm/schema/field-dictionary.md) per modellare i dati di input e output:

### Schema dati di input

| Nome campo | Tipo |
| --- | --- |
| itemId | Stringa |
| actionType | Stringa |
| timestamp | Stringa |
| userId | Stringa |

### Schema dati di output

| Nome campo | Tipo |
| --- | --- |
| consigli | Stringa |
| userId | Intero |

## Algoritmo

La ricetta di Recommendations per i prodotti utilizza il filtro collaborativo per generare un elenco personalizzato di consigli di prodotti per i clienti. Il filtro collaborativo, a differenza di un approccio basato sui contenuti, non richiede informazioni su un prodotto specifico ma utilizza le preferenze storiche di un cliente su un set di prodotti. Questa potente tecnica di raccomandazione utilizza due semplici presupposti:
* Ci sono clienti con interessi simili, e possono essere raggruppati confrontando i loro comportamenti di acquisto e navigazione.
* È più probabile che un cliente sia interessato a una raccomandazione basata su clienti simili in termini di comportamento di acquisto e navigazione.

Questo processo è suddiviso in due fasi principali. Innanzitutto, definisci un sottoinsieme di clienti simili. Quindi, all’interno di tale set, identifica funzioni simili tra i clienti al fine di restituire un consiglio per il cliente target.
