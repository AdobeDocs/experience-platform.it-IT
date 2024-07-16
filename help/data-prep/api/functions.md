---
keywords: Experience Platform;home;argomenti popolari;preparazione dati;guida api;schemi;
title: Endpoint API per funzioni
description: Puoi utilizzare l’endpoint "/functions" nell’API della preparazione dati per convalidare le espressioni di mappatura ed elencare le funzioni del set di mappatura disponibili.
exl-id: dc24bfb4-2d96-4757-a610-0c2ee960d41d
source-git-commit: 05e63064dc8eb3f070a383f508cc4a86d4f5e9cc
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 5%

---

# Endpoint funzioni

Le funzioni di mappatura consentono di trasformare i dati tra gli schemi di origine e di destinazione. È possibile utilizzare l&#39;endpoint `/languages/el` per convalidare le espressioni e ottenere un elenco di tutte le funzioni del set di mappatura disponibili.

## Convalidare espressioni

Per verificare se l&#39;espressione corrente è valida, eseguire una richiesta POST all&#39;endpoint `/languages/el/validate`.

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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con lo stato di convalida dell’espressione.

```json
{
    "validationStatus": "succeeded",
    "error": "none"
}
```

## Elencare le funzioni del set di mappatura

Per recuperare un elenco di tutte le funzioni del set di mappatura disponibili, eseguire una richiesta GET all&#39;endpoint `/languages/el/functions`.

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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco di tutte le funzioni del set di mappatura disponibili.

>[!NOTE]
>
>La risposta è stata troncata per motivi di spazio.

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

## Elenca gli operatori del set di mappatura

È possibile recuperare un elenco di tutti gli operatori del set di mappatura disponibili effettuando una richiesta GET all&#39;endpoint `/languages/el/operators`.

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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco di tutti gli operatori del set di mappatura disponibili.

>[!NOTE]
>
>La risposta è stata troncata per motivi di spazio.

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
