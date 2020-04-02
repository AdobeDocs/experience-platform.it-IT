---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conversioni PQL
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# Conversioni PQL

introduzione

- Conversione della formattazione da pql/text e pql/json

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte dell&#39;API di segmentazione. Prima di continuare, consulta la guida [per lo sviluppatore di](./getting-started.md)segmentazione.

In particolare, la sezione [](./getting-started.md#getting-started) introduttiva della guida per gli sviluppatori di segmentazione include collegamenti a argomenti correlati, una guida alla lettura delle chiamate API di esempio nel documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente chiamate a qualsiasi API della piattaforma Experience.

## Conversione della formattazione da pql/text e pql/json

**Formato API**

```http
POST /segment/conversion
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "name": "People who ordered in the last 30 days",
  "expression": {
    "type": "PQL",
    "format": "pql/text",
    "value": "workAddress.country = \"US\""
  },
  "schema": {
    "name": "_xdm.context.profile"
  },
  "ttlInDays": 60
}
 '
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Un nome univoco per la definizione del segmento. |
| `expression.type` | Il tipo di espressione. Può essere `PQL` o `ARL`. |
| `expression.format` | Il formato dell&#39;espressione. Può essere `pql/text` o `pql/json`. |
| `expression.value` | Stringa di query dell&#39;espressione da convertire. |
| `schema.name` | L&#39;ID classe dello schema a cui si fa riferimento. |
| `ttlInDays` | Un numero intero che rappresenta il tempo di vita (TTL). |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli del segmento convertito.

```json
{
    "ttlInDays": 60,
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"country\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"workAddress\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}},{\"nodeType\":\"literal\",\"literalType\":\"String\",\"value\":\"US\"}]}"
    }
}
```

## Passaggi successivi
