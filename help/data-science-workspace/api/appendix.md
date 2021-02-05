---
keywords: ' Experience Platform;guida sviluppatore;endpoint;Data Science Workspace;argomenti più comuni;'
solution: Experience Platform
title: Guida all'API di apprendimento di una macchina Sensei
topic: Developer guide
description: Le sezioni seguenti forniscono informazioni di riferimento per le varie funzionalità di Sensei Machine Learning API.
translation-type: tm+mt
source-git-commit: b395535cbe7e4030606ee2808eb173998f5c32e0
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 1%

---


# [!DNL Sensei Machine Learning] Appendice della guida API

Le sezioni seguenti forniscono informazioni di riferimento per le varie funzionalità dell&#39;API [!DNL Sensei Machine Learning].

## Parametri di query per il recupero delle risorse {#query}

L&#39;API [!DNL Sensei Machine Learning] fornisce il supporto per i parametri di query con il recupero delle risorse. I parametri di query disponibili e i relativi utilizzi sono descritti nella tabella seguente:

| Parametro query | Descrizione | Valore predefinito |
| --------------- | ----------- | ------- |
| `start` | Indica l&#39;indice iniziale per l&#39;impaginazione. | `start=0` |
| `limit` | Indica il numero massimo di risultati da restituire. | `limit=25` |
| `orderby` | Indica le proprietà da utilizzare per l&#39;ordinamento in ordine di priorità. Includete un trattino (**-**) prima che il nome di una proprietà venga ordinato in ordine decrescente, altrimenti i risultati vengono ordinati in ordine crescente. | `orderby=created` |
| `property` | Indica l&#39;espressione di confronto che un oggetto deve soddisfare per essere restituito. | `property=deleted==false` |

>[!NOTE]
>
>Quando si combinano più parametri di query, questi devono essere separati da e commerciale (**&amp;**).

## Configurazione CPU Python e GPU {#cpu-gpu-config}

I motori Python hanno la possibilità di scegliere tra una CPU o una GPU a scopo di formazione o punteggio, ed è definita su un [MLIninstance](./mlinstances.md) come specifica di attività (`tasks.specification`).

Esempio di configurazione che specifica l’utilizzo di una CPU per la formazione e di una GPU per il punteggio:

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "training parameter",
                "value": "parameter value"
            }    
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "cpus": "1"
        }
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value" 
            }
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "gpus": "1"
        }
    }
]
```

>[!NOTE]
>
>I valori di `cpus` e `gpus` non indicano il numero di CPU o GPU, ma il numero di computer fisici. Questi valori sono consentiti `"1"` e genereranno un&#39;eccezione in caso contrario.

## Configurazioni risorse PySpark e Spark {#resource-config}

I motori Spark sono in grado di modificare le risorse computazionali a scopo di formazione e punteggio. Queste risorse sono descritte nella tabella seguente:

| Risorsa | Descrizione | Tipo |
| -------- | ----------- | ---- |
| driverMemory | Memoria per driver in megabyte | int |
| driverCores | Numero di core utilizzati dal conducente | int |
| esecutoreMemory | Memoria per esecutore in megabyte | int |
| esecutoreCores | Numero di core utilizzati dall&#39;esecutore | int |
| numExecutor | Numero di esecutori | int |

Le risorse possono essere specificate su un [MLIninstance](./mlinstances.md) come (A) singoli parametri di formazione o punteggio oppure (B) all&#39;interno di un oggetto di specifiche aggiuntivo (`specification`). Ad esempio, le seguenti configurazioni di risorse sono le stesse sia per la formazione che per il punteggio:

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "driverMemory",
                "value": "2048"
            },
            {
                "key": "driverCores",
                "value": "1"
            },
            {
                "key": "executorMemory",
                "value": "2048"
            },
            {
                "key": "executorCores",
                "value": "2"
            },
            {
                "key": "numExecutors",
                "value": "3"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value"
            }
        ],
        "specification": {
            "type": "SparkTaskSpec",
            "name": "Spark Task name",
            "className": "Class name",
            "driverMemoryInMB": 2048,
            "driverCores": 1,
            "executorMemoryInMB": 2048,
            "executorCores": 2,
            "numExecutors": 3
        }
    }
]
```
