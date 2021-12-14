---
title: Ricerca di risorse nell’API di Reactor
description: Scopri come cercare le risorse nell’API di Reactor.
exl-id: cb594e60-3e24-457e-bfb3-78ec84d3e39a
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 100%

---

# Ricerca di risorse nell’API di Reactor

L’endpoint `/search` nell’API di Reactor consente di eseguire query strutturate sulle risorse memorizzate. Questo documento fornisce esempi di diverse query di ricerca per vari casi d’uso comuni.

>[!NOTE]
>
>Prima di leggere questa guida, consulta la [guida dell’endpoint “search”](../endpoints/search.md) per informazioni sulla sintassi di query accettata e altre linee guida sull’utilizzo.

## Strategie di base per le query

Gli esempi seguenti illustrano alcuni concetti di base per l’utilizzo della funzionalità di ricerca dell’API.

### Ricerca in più campi

È possibile eseguire una ricerca in più campi utilizzando caratteri jolly nel nome del campo. Ad esempio, per eseguire ricerche in più campi attributo, utilizza `attributes.*` come nome del campo.

```json
{
  "data": {
    "query": {
      "attributes.*": {
        "value": "evar7"
      }
    }
  }
}
```

>[!IMPORTANT]
>
>Solitamente, i valori di ricerca devono corrispondere al tipo di dati oggetto della ricerca. Ad esempio, non è possibile eseguire una query con un valore `evar7` per un campo di numeri interi. Durante la ricerca in più campi, il requisito del tipo di query è meno rigoroso onde evitare errori, ma può produrre risultati indesiderati.

### Definire l’ambito delle query per tipi di risorse specifici

Puoi eseguire una ricerca per un tipo di risorsa specifico fornendo `resource_types` nella richiesta. Ad esempio, per eseguire ricerche in `data_elements` e `rule_components`:

```json
{
  "data": {
    "from": 0,
    "size": 25,
    "query": {
      "attributes.display_name": {
        "value": "Performance"
      }
    },
    "resource_types": [
      "data_elements",
      "rule_components"
    ]
  }
}
```

### Ordinare le risposte

La proprietà `sort` può essere utilizzata per ordinare le risposte. Ad esempio, per ordinare in base al valore `created_at`, a partire dal più recente:

```json
{
  "data": {
    "from": 0,
    "size": 25,
    "query": {
      "attributes.display_name": {
        "value": "Performance"
      }
    },
    "sort": [
      {
        "attributes.created_at": "desc"
      }
    ],
    "resource_types": [
      "data_elements",
      "rule_components"
    ]
  }
}
```

## Esempi comuni di ricerca

L’esempio seguente illustra altri pattern di ricerca comuni.

### Qualsiasi risorsa con un nome specifico

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "attributes.name": {
              "value": "Adobe"
            }
          }
        }
      }'
```

### Qualsiasi risorsa che fa riferimento a “evar7”

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "attributes.*": {
              "value": "evar7"
            }
          }
        }
      }'
```

### Elementi dati di tipo delegato “custom-code”

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "attributes.delegate_descriptor_id": {
              "value": "custom-code"
            }
          },
          "resource_types": ["data_elements"]
        }
      }'
```

### Componenti di regole che fanno riferimento a un elemento dati specifico

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "attributes.settings": {
              "value": "myDataElement8"
            }
          },
          "resource_types": ["rule_components"]
        }
      }'
```

### Regole in una proprietà specifica

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "relationships.property.data.id": {
              "value": "PR3cab070a9eb3423894e4a3038ef0e7b7"
            }
          },
          "resource_types": ["rules"]
        }
      }'
```

### Ricerca di una risorsa per ID

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "id": {
              "value": "PR3cab070a9eb3423894e4a3038ef0e7b7"
            }
          }
        }
      }'
```

### Eseguire una ricerca utilizzando la logica “OR”

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "attributes.display_name": {
              "value": "My Rule Holiday Sale",
              "value_operator: "OR"
            }
          }
        }
      }'
```
