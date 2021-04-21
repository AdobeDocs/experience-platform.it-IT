---
keywords: Experience Platform;guida per sviluppatori;endpoint;Data Science Workspace;argomenti comuni;
solution: Experience Platform
title: Appendice della guida all’API di apprendimento automatico di Sensei
topic-legacy: Developer guide
description: Le sezioni seguenti forniscono informazioni di riferimento per varie funzioni dell’API di apprendimento automatico di Sensei.
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 1%

---

# [!DNL Sensei Machine Learning] Appendice della guida API

Le sezioni seguenti forniscono informazioni di riferimento per le varie funzioni dell’ API [!DNL Sensei Machine Learning] .

## Parametri di query per il recupero delle risorse {#query}

L’ API [!DNL Sensei Machine Learning] fornisce il supporto per i parametri di query per il recupero delle risorse. I parametri di query disponibili e i relativi utilizzi sono descritti nella tabella seguente:

| Parametro query | Descrizione | Valore predefinito |
| --------------- | ----------- | ------- |
| `start` | Indica l&#39;indice iniziale per l&#39;impaginazione. | `start=0` |
| `limit` | Indica il numero massimo di risultati da restituire. | `limit=25` |
| `orderby` | Indica le proprietà da utilizzare per l&#39;ordinamento in ordine di priorità. Includi un trattino (**-**) prima che un nome di proprietà venga ordinato in ordine decrescente, altrimenti i risultati vengono ordinati in ordine crescente. | `orderby=created` |
| `property` | Indica l&#39;espressione di confronto che un oggetto deve soddisfare per poter essere restituito. | `property=deleted==false` |

>[!NOTE]
>
>Quando si combinano più parametri di query, devono essere separati da e commerciale (**&amp;**).

## Configurazioni CPU e GPU Python {#cpu-gpu-config}

I motori Python possono scegliere tra una CPU o una GPU a scopo di formazione o punteggio ed è definito su una [MLInance](./mlinstances.md) come specifica di attività (`tasks.specification`).

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
>I valori di `cpus` e `gpus` non indicano il numero di CPU o GPU, ma il numero di macchine fisiche. Questi valori sono consentiti `"1"` e in caso contrario genereranno un&#39;eccezione.

## Configurazioni delle risorse PySpark e Spark {#resource-config}

I motori Spark possono modificare le risorse computazionali a scopo di formazione e valutazione. Queste risorse sono descritte nella tabella seguente:

| Risorsa | Descrizione | Tipo |
| -------- | ----------- | ---- |
| driverMemory | Memoria del driver in megabyte | int |
| driverCores | Numero di core utilizzati dal conducente | int |
| exutorMemory | Memoria per esecutore in megabyte | int |
| esecutoreCores | Numero di core utilizzati dall&#39;esecutore | int |
| numExecutors | Numero di esecutori | int |

Le risorse possono essere specificate su un [ISTANZA MLI](./mlinstances.md) come (A) parametri di formazione o valutazione individuali o (B) all&#39;interno di un oggetto di specifiche aggiuntivo (`specification`). Ad esempio, le seguenti configurazioni di risorse sono le stesse sia per la formazione che per il punteggio:

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
