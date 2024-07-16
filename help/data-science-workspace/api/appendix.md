---
keywords: Experience Platform;guida per sviluppatori;endpoint;Data Science Workspace;argomenti popolari;
solution: Experience Platform
title: Appendice alla guida API di apprendimento automatico di Sensei
description: Le sezioni seguenti forniscono informazioni di riferimento per varie funzioni dell’API di apprendimento automatico di Sensei.
role: Developer
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 1%

---

# Appendice alla guida API [!DNL Sensei Machine Learning]

Le sezioni seguenti forniscono informazioni di riferimento per varie funzionalità dell&#39;API [!DNL Sensei Machine Learning].

## Parametri di query per il recupero delle risorse {#query}

L&#39;API [!DNL Sensei Machine Learning] fornisce il supporto per i parametri di query con il recupero delle risorse. Nella tabella seguente sono descritti i parametri di query disponibili e i relativi utilizzi:

| Parametro query | Descrizione | Valore predefinito |
| --------------- | ----------- | ------- |
| `start` | Indica l&#39;indice iniziale per la paginazione. | `start=0` |
| `limit` | Indica il numero massimo di risultati da restituire. | `limit=25` |
| `orderby` | Indica le proprietà da utilizzare per l&#39;ordinamento in ordine di priorità. Includere un trattino (**-**) prima del nome di una proprietà per l&#39;ordinamento decrescente. In caso contrario, i risultati verranno ordinati in ordine crescente. | `orderby=created` |
| `property` | Indica l&#39;espressione di confronto che un oggetto deve soddisfare per essere restituito. | `property=deleted==false` |

>[!NOTE]
>
>Quando si combinano più parametri di query, questi devono essere separati da un simbolo di E commerciale (**&amp;**).

## Configurazioni CPU e GPU Python {#cpu-gpu-config}

I motori Python hanno la possibilità di scegliere tra una CPU o una GPU per i loro scopi di formazione o punteggio ed è definito su una [MLInstance](./mlinstances.md) come specifica di attività (`tasks.specification`).

Di seguito è riportata una configurazione di esempio che specifica l’utilizzo di una CPU per l’apprendimento e di una GPU per il punteggio:

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

I motori Spark hanno la capacità di modificare le risorse computazionali a scopo di formazione e punteggio. Queste risorse sono descritte nella tabella seguente:

| Risorsa | Descrizione | Tipo |
| -------- | ----------- | ---- |
| driverMemory | Memoria per il driver in megabyte | int |
| driverCore | Numero di core utilizzati dal driver | int |
| EXECUTORMEMORY | Memoria per l&#39;esecutore in megabyte | int |
| executorCores | Numero di core utilizzati dall&#39;esecutore | int |
| numExecutors | Numero di esecutori | int |

Le risorse possono essere specificate in un [MLInstance](./mlinstances.md) come (A) singoli parametri di formazione o punteggio oppure (B) all&#39;interno di un oggetto specifiche aggiuntivo (`specification`). Ad esempio, le seguenti configurazioni di risorse sono le stesse sia per l’apprendimento che per il punteggio:

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
