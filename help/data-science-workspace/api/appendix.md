---
keywords: Experience Platform;guida per sviluppatori;endpoint;Data Science Workspace;argomenti comuni;
solution: Experience Platform
title: Appendice della guida all’API di apprendimento automatico di Sensei
description: Le sezioni seguenti forniscono informazioni di riferimento per varie funzioni dell’API di apprendimento automatico di Sensei.
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# [!DNL Sensei Machine Learning] Appendice della guida API

Le sezioni seguenti forniscono informazioni di riferimento per le varie caratteristiche del [!DNL Sensei Machine Learning] API.

## Parametri di query per il recupero delle risorse {#query}

La [!DNL Sensei Machine Learning] L’API fornisce il supporto per i parametri di query con il recupero delle risorse. I parametri di query disponibili e i relativi utilizzi sono descritti nella tabella seguente:

| Parametro query | Descrizione | Valore predefinito |
| --------------- | ----------- | ------- |
| `start` | Indica l&#39;indice iniziale per l&#39;impaginazione. | `start=0` |
| `limit` | Indica il numero massimo di risultati da restituire. | `limit=25` |
| `orderby` | Indica le proprietà da utilizzare per l&#39;ordinamento in ordine di priorità. Includi un trattino (**-**) prima del nome di una proprietà da ordinare in ordine decrescente, altrimenti i risultati vengono ordinati in ordine crescente. | `orderby=created` |
| `property` | Indica l&#39;espressione di confronto che un oggetto deve soddisfare per poter essere restituito. | `property=deleted==false` |

>[!NOTE]
>
>Quando si combinano più parametri di query, questi devono essere separati da e commerciale (**&amp;**).

## Configurazioni CPU e GPU Python {#cpu-gpu-config}

I Python Engines hanno la possibilità di scegliere tra una CPU o una GPU per i suoi scopi di formazione o punteggio, ed è definito su un [MLInance](./mlinstances.md) come specifica di un&#39;attività (`tasks.specification`).

Di seguito è riportato un esempio di configurazione che specifica l’utilizzo di una CPU per la formazione e di una GPU per il punteggio:

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
>I valori di `cpus` e `gpus` non indica il numero di CPU o GPU, ma piuttosto il numero di macchine fisiche. Questi valori sono consentiti `"1"` e altrimenti lancerà un&#39;eccezione.

## Configurazioni delle risorse PySpark e Spark {#resource-config}

I motori Spark possono modificare le risorse computazionali a scopo di formazione e valutazione. Queste risorse sono descritte nella tabella seguente:

| Risorsa | Descrizione | Tipo |
| -------- | ----------- | ---- |
| driverMemory | Memoria del driver in megabyte | Intero |
| driverCores | Numero di core utilizzati dal conducente | Intero |
| exutorMemory | Memoria per esecutore in megabyte | Intero |
| esecutoreCores | Numero di core utilizzati dall&#39;esecutore | Intero |
| numExecutors | Numero di esecutori | Intero |

Le risorse possono essere specificate in un [MLInance](./mlinstances.md) come (A) parametri individuali di addestramento o punteggio, o (B) all&#39;interno di un oggetto specifico aggiuntivo (`specification`). Ad esempio, le seguenti configurazioni di risorse sono le stesse sia per la formazione che per il punteggio:

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
