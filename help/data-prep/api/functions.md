---
keywords: Experience Platform;home;argomenti popolari;preparazione dati;guida api;schemi;
solution: Experience Platform
title: Endpoint API per gli schemi
topic-legacy: schemas
description: Puoi utilizzare l'endpoint `/function` nell'API di Adobe Experience Platform per convalidare le espressioni di mappatura e elencare le funzioni disponibili per i set di mappatura.
exl-id: dc24bfb4-2d96-4757-a610-0c2ee960d41d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 5%

---

# Endpoint delle funzioni

Le funzioni del set di mappature consentono di trasformare i dati tra schemi di origine e di destinazione. È possibile utilizzare `/languages/el` per convalidare le espressioni e ottenere un elenco di tutte le funzioni disponibili per il set di mappature.

## Convalidare espressioni

Puoi verificare se l’espressione corrente è valida effettuando una richiesta POST al `/languages/el/validate` punto finale.

**Formato API**

```
POST /languages/el/validate
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/languages/el/validate \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "expression": "concat(\"Hi\", \",\", \"there\", \"!\")"
  }'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con lo stato di convalida dell&#39;espressione.

```json
{
    "validationStatus": "succeeded",
    "error": "none"
}
```

## Funzioni set di mappatura elenco

È possibile recuperare un elenco di tutte le funzioni del set di mappature disponibili effettuando una richiesta di GET al `/languages/el/functions` punto finale.

**Formato API**

```
GET /languages/el/functions
```

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/functions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un elenco di tutte le funzioni disponibili per il set di mappature.

>[!NOTE]
>
>Questa risposta è stata troncata per lo spazio.

```json
[
    {
        "category": "Date / Time",
        "function": "date",
        "description": "Function that converts date string into a ZonedDateTime object.",
        "syntax": "ZonedDateTime date(String, String, ZonedDateTime)",
        "returns": "Returns the date object that is formatted in given format or a default date if the expression evaluates to a null date.",
        "returnType": "java.time.ZonedDateTime",
        "example": "",
        "result": "",
        "params": [],
        "since": 1
    },
    {
        "category": "Hierarchies - Arrays",
        "function": "first",
        "description": "Function to retrieve the first element of the given array.",
        "syntax": "T first(T...)",
        "returns": "The first element or null if the array is null or empty.",
        "returnType": "java.lang.Object",
        "example": "first(\"1\", \"2\", \"3\")",
        "result": "\"1\"",
        "params": [
            {
                "name": "values",
                "description": "Zero or more arguments",
                "type": "object",
                "dataType": "[Ljava.lang.Object;",
                "position": 1
            }
        ],
        "since": 1
    }
]
```

## Elenca operatori set di mappature

Puoi recuperare un elenco di tutti gli operatori del set di mappature disponibili effettuando una richiesta di GET al `/languages/el/operators` punto finale.

**Formato API**

```
GET /languages/el/operators
```

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/operators \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un elenco di tutti gli operatori di set di mappature disponibili.

>[!NOTE]
>
>Questa risposta è stata troncata per lo spazio.

```json
[
    {
        "operatorSymbol": "+",
        "methodName": "add",
        "numberOfOperands": 2,
        "description": "Simple arithmetic addition",
        "example": "1 + 2"
    },
    {
        "operatorSymbol": "/",
        "methodName": "divide",
        "numberOfOperands": 2,
        "description": "Simple arithmetic division",
        "example": "1 / 2"
    },
    {
        "operatorSymbol": "~",
        "methodName": "complement",
        "numberOfOperands": 1,
        "description": "The usual ~ operator is used, e.g.\n~33\n, ~0010 0001 = 1101 1110 = -34.",
        "example": "~44"
    },
    {
        "operatorSymbol": "-",
        "methodName": "negate",
        "numberOfOperands": 1,
        "description": "The unary - operator is used. For example\n-12",
        "example": "-12"
    },
    {
        "operatorSymbol": "!",
        "methodName": "not",
        "numberOfOperands": 1,
        "description": "The usual ! operator can be used as well as the word not, e.g.\n!cond1\nand\nnot cond1\nare equivalent",
        "example": "!cond1"
    }
]
```
