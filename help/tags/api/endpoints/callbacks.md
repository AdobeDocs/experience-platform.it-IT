---
title: Endpoint “callbacks”
description: Scopri come effettuare chiamate all’endpoint /callbacks nell’API di Reactor.
exl-id: dd980f91-89e3-4ba0-a6fc-64d66b288a22
source-git-commit: 7f3b9ef9270b7748bc3366c8c39f503e1aee2100
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 96%

---

# Endpoint “callbacks”

Un callback (o richiamata) è un messaggio che l’API di Reactor invia a un URL specifico (di solito quello ospitato dalla tua organizzazione).

I callback devono essere utilizzati insieme a [eventi di audit](./audit-events.md) per monitorare le attività nell’API di Reactor. Ogni volta che viene generato un evento di audit di un determinato tipo, un callback può inviare un messaggio corrispondente all’URL specificato.

Il servizio dietro l’URL specificato nel callback deve rispondere con il codice di stato HTTP 200 (OK) o 201 (Creato). Se il servizio non risponde con uno di questi codici di stato, la consegna del messaggio viene ritentata agli intervalli seguenti:

* 1 minuto
* 5 minuti
* 30 minuti
* 1 ora
* 12 ore
* 1 giorno
* 3 giorni

>[!NOTE]
>
>Gli intervalli dei tentativi sono relativi all’intervallo precedente. Ad esempio, se il nuovo tentativo eseguito dopo un minuto non riesce, il tentativo successivo avverrà cinque minuti dall’errore del tentativo a un minuto (quindi sei minuti dopo la generazione del messaggio).

Se nessuno dei tentativi di consegna ha esito positivo, il messaggio viene eliminato.

Un callback appartiene esattamente a una [proprietà](./properties.md). Una proprietà può avere molti callback.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’[API di Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Prima di continuare, consulta la [guida introduttiva](../getting-started.md) per informazioni importanti su come eseguire l’autenticazione nell’API.

## Elencare i callback {#list}

Per elencare tutti i callback di una proprietà, devi eseguire una richiesta GET.

**Formato API**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| Parametro | Descrizione |
| --- | --- |
| `{PROPERTY_ID}` | `id` della proprietà di cui desideri elencare i callback. |

{style="table-layout:auto"}

>[!NOTE]
>
>Utilizzando i parametri di query, i callback elencati possono essere filtrati in base ai seguenti attributi:<ul><li>`created_at`</li><li>`updated_at`</li></ul>Per ulteriori informazioni, consulta la guida su come [filtrare le risposte](../guides/filtering.md).

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di callback per la proprietà specificata.

```json
{
  "data": [
    {
      "id": "CB26edef8d709243579589107bcda034da",
      "type": "callbacks",
      "attributes": {
        "created_at": "2020-12-14T17:34:47.082Z",
        "subscriptions": [
          "rule.created"
        ],
        "updated_at": "2020-12-14T17:34:47.082Z",
        "url": "https://www.example.com"
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da/property"
          },
          "data": {
            "id": "PR66a3356c73fc4aabb67ee22caae53d70",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70",
        "self": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## Cercare un callback {#lookup}

Per cercare un callback occorre specificare il relativo ID nel percorso di una richiesta GET.

**Formato API**

```http
GET /callbacks/{CALLBACK_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `CALLBACK_ID` | `id` del callback che si desidera cercare. |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del callback.

```json
{
  "data": {
    "id": "CBeef389cee8d84e69acef8665e4dcbef6",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:36.872Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:36.872Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6/property"
        },
        "data": {
          "id": "PRb513bbab52114573ac87f9848eea6ead",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb513bbab52114573ac87f9848eea6ead",
      "self": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6"
    }
  }
}
```

## Creare un callback {#create}

Per creare un nuovo callback, devi eseguire una richiesta POST.

**Formato API**

```http
POST /properties/{PROPERTY_ID}/callbacks
```

| Parametro | Descrizione |
| --- | --- |
| `PROPERTY_ID` | `id` della [proprietà](./properties.md) in cui si sta definendo il callback. |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "url": "https://www.example.com",
            "subscriptions": [
              "rule.created"
            ]
          }
        }
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `url` | Destinazione URL del messaggio di callback. L’URL deve utilizzare l’estensione del protocollo HTTPS. |
| `subscriptions` | Matrice di stringhe che indica i tipi di evento di audit che attiveranno il callback. Per un elenco dei possibili tipi di eventi, consulta la [guida dell’endpoint “audit_events”](./audit-events.md). |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del nuovo callback creato.

```json
{
  "data": {
    "id": "CB32d8f23d5ee548278d32076af4c442a0",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:27.059Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:27.059Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0/property"
        },
        "data": {
          "id": "PR5e22de986a7c4070965e7546b2bb108d",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d",
      "self": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0"
    }
  }
}
```

## Aggiornare un callback

Per aggiornare un callback, devi includere il relativo ID nel percorso di una richiesta PATCH.

**Formato API**

```http
PATCH /callbacks/{CALLBACK_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `CALLBACK_ID` | `id` del callback che si desidera aggiornare. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente aggiorna la matrice `subscriptions` per un callback esistente.

```shell
curl -X PATCH \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "url": "https://www.example.net",
            "subscriptions": [
              "rule.created",
              "build.created"
            ]
          },
          "type": "callbacks",
          "id": "CB4310904d415549888cc9e31ebe1e1e45"
        }
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `attributes` | Oggetto le cui proprietà rappresentano gli attributi da aggiornare per il callback. Ogni chiave rappresenta il particolare attributo di callback da aggiornare, insieme al valore corrispondente a cui deve essere aggiornato.<br><br>I seguenti attributi possono essere aggiornati per i callback:<ul><li>`subscriptions`</li><li>`url`</li></ul> |
| `id` | `id` del callback che desideri aggiornare. Questo deve corrispondere al valore `{CALLBACK_ID}` fornito nel percorso della richiesta. |
| `type` | Tipo di risorsa da aggiornare. Per questo endpoint, il valore deve essere `callbacks`. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del callback aggiornato.

```json
{
  "data": {
    "id": "CB4310904d415549888cc9e31ebe1e1e45",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:56.884Z",
      "subscriptions": [
        "rule.created",
        "build.created"
      ],
      "updated_at": "2020-12-14T17:34:57.614Z",
      "url": "https://www.example.net"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45/property"
        },
        "data": {
          "id": "PR0a8ef3ca31dc456a8566e9288960bd79",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR0a8ef3ca31dc456a8566e9288960bd79",
      "self": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45"
    }
  }
}
```

## Eliminare un callback

Puoi eliminare un callback includendo il relativo ID nel percorso di una richiesta DELETE.

**Formato API**

```http
DELETE /callbacks/{CALLBACK_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `CALLBACK_ID` | `id` del callback che desideri eliminare. |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X DELETE \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto) senza corpo di risposta, a indicare che il callback è stato eliminato.
