---
title: Endpoint delle librerie
description: Scopri come effettuare chiamate all’endpoint /librerie nell’API di Reactor.
source-git-commit: 53612919dc040a8a3ad35a3c5c0991554ffbea7c
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 8%

---

# Endpoint delle librerie

Una libreria è una raccolta di risorse tag ([estensioni](./extensions.md), [regole](./rules.md) e [elementi dati](./data-elements.md)) che rappresentano il comportamento desiderato di una [proprietà](./properties.md). L’endpoint `/libraries` nell’API di Reactor consente di gestire in modo programmatico le librerie all’interno delle proprietà dei tag.

Una libreria appartiene esattamente a una proprietà. Una proprietà può avere molte librerie.

## Introduzione

L&#39;endpoint utilizzato in questa guida fa parte dell&#39; [API del reattore](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Prima di continuare, controlla la [guida introduttiva](../getting-started.md) per informazioni importanti su come eseguire l&#39;autenticazione nell&#39;API.

Prima di lavorare con le librerie nell&#39;API di Reactor, è importante comprendere i ruoli che lo stato e gli ambienti della libreria svolgono per determinare quali azioni puoi eseguire su una particolare libreria. Per ulteriori informazioni, consulta la guida sul [flusso di pubblicazione della libreria](../../ui/publishing/publishing-flow.md) .

## Recupera un elenco di librerie {#list}

Puoi recuperare un elenco di librerie per una proprietà includendo l’ID della proprietà nel percorso di una richiesta GET.

**Formato API**

```http
GET /properties/{PROPERTY_ID}/libraries
```

| Parametro | Descrizione |
| --- | --- |
| `PROPERTY_ID` | Il `id` della proprietà proprietaria delle librerie. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Utilizzando i parametri di query, le librerie elencate possono essere filtrate in base ai seguenti attributi:<ul><li>`created_at`</li><li>`name`</li><li>`published_at`</li><li>`stale`</li><li>`state`</li><li>`updated_at`</li></ul>Per ulteriori informazioni, consulta la guida sulle [risposte relative al filtro](../guides/filtering.md) .

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR4bc17fb09ed845b1acfb0f6600a1f3c0/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

Una risposta corretta restituisce un elenco di librerie per la proprietà specificata.

```json
{
  "data": [
    {
      "id": "LBb174d60bdbd34f87a2e9466fadaacae0",
      "type": "libraries",
      "attributes": {
        "created_at": "2020-12-14T17:44:10.776Z",
        "name": "My Library",
        "published_at": null,
        "state": "development",
        "updated_at": "2020-12-14T17:44:10.776Z",
        "build_required": true
      },
      "relationships": {
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/builds"
          }
        },
        "environment": {
          "links": {
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/environment"
          },
          "data": null
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/data_elements",
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/extensions",
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/extensions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/notes"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/rules",
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/rules"
          }
        },
        "upstream_library": {
          "data": null
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/property"
          },
          "data": {
            "id": "PR4bc17fb09ed845b1acfb0f6600a1f3c0",
            "type": "properties"
          }
        },
        "last_build": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/last_build"
          },
          "data": null
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR4bc17fb09ed845b1acfb0f6600a1f3c0",
        "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0"
      },
      "meta": {
        "build_status": null,
        "build_required_detail": "No build found since last state change"
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

## Cerca una libreria {#lookup}

Puoi cercare una libreria fornendo il relativo ID nel percorso di una richiesta GET.

**Formato API**

```http
GET /libraries/{LIBRARY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `LIBRARY_ID` | Il `id` della libreria che desideri cercare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

Una risposta corretta restituisce i dettagli della libreria.

```json
{
  "data": {
    "id": "LB5862ee2dc21b4646a5536c8d6edb0c84",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:44:00.476Z",
      "name": "My Library",
      "published_at": null,
      "state": "development",
      "updated_at": "2020-12-14T17:44:00.476Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/builds"
        }
      },
      "environment": {
        "links": {
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/environment"
        },
        "data": null
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/extensions",
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/rules",
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/property"
        },
        "data": {
          "id": "PRc90084c615844db58201d4e70d47b8bf",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/last_build"
        },
        "data": null
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRc90084c615844db58201d4e70d47b8bf",
      "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```

## Creare una libreria {#create}

Puoi creare una nuova libreria effettuando una richiesta POST.

**Formato API**

```http
POST /properties/{PROPERTY_ID}/libraries
```

| Parametro | Descrizione |
| --- | --- |
| `PROPERTY_ID` | La `id` della [proprietà](./properties.md) in cui si sta definendo la libreria. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

Nella richiesta seguente viene creata una nuova libreria per la proprietà specificata. Quando crei una libreria, puoi configurare solo il relativo attributo `name` . Per aggiungere elementi dati, estensioni e regole alla libreria, è necessario creare relazioni. Per ulteriori informazioni, consulta la sezione sulla [gestione delle risorse della libreria](#resources) .

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "My Library"
          },
          "type": "libraries"
        }
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `attributes.name` | **(Obbligatorio)** Un nome leggibile dall&#39;utente per la libreria. |
| `type` | Tipo di risorsa da aggiornare. Per questo endpoint, il valore deve essere `libraries`. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli della libreria appena creata.

```json
{
  "data": {
    "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:33:21.774Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "My library 2020-12-14 17:33:21 +0000",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:33:21.774Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementSelector\":\".target-element\",\"elementProperty\":\"html\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/property"
        },
        "data": {
          "id": "PR05ad70a8078f44c1a229ecf0da2802f2",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/origin"
        },
        "data": {
          "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
          "type": "libraries"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/extension"
        },
        "data": {
          "id": "EX28788723a8e24a2f927fce1b55eb7ffc",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension"
        },
        "data": {
          "id": "EXd6bf04b143e64fe0ae7efe55a6655fa9",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR05ad70a8078f44c1a229ecf0da2802f2",
      "origin": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "self": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "extension": "https://reactor.adobe.io/extensions/EX28788723a8e24a2f927fce1b55eb7ffc"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Gestione delle risorse di una libreria {#resources}

Gli elementi dati, le estensioni, le regole e l&#39;ambiente associati a una libreria vengono stabiliti tramite relazioni. Le sezioni seguenti spiegano come gestire queste relazioni tramite chiamate API.

### Aggiungere risorse a una libreria {#add-resources}

Puoi aggiungere risorse a una libreria aggiungendo `/relationships` al percorso di una richiesta POST, seguito dal tipo di risorsa .

**Formato API**

```http
POST /libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Parametro | Descrizione |
| --- | --- |
| `{LIBRARY_ID}` | ID della libreria a cui desideri aggiungere risorse. |
| `{RESOURCE_TYPE}` | Il tipo di risorsa che si sta aggiungendo alla libreria. Sono accettati i seguenti valori: <ul><li>`data_elements`</li><li>`extensions`</li><li>`rules`</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta seguente aggiunge due elementi dati a una libreria.

```shell
curl -X POST \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": [
          {
            "id": "DEce7fdee2afe44efeb4d974247d1e8dbe",
            "type": "data_elements"
          },
          {
            "id": "DE8097636264104451ac3a18c95d5ff833",
            "type": "data_elements"
          }
        ]
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID della risorsa che stai aggiungendo alla libreria. |
| `type` | Il tipo di risorsa che si sta aggiungendo alla libreria. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli delle relazioni aggiunte. L&#39;esecuzione di una [richiesta di ricerca](#lookup) per la libreria mostra le relazioni aggiunte sotto la proprietà `relationships` .

```json
{
  "data": [
    {
      "type": "data_elements",
      "id": "DEce7fdee2afe44efeb4d974247d1e8dbe"
    },
    {
      "id": "DE8097636264104451ac3a18c95d5ff833",
      "type": "data_elements"
    }
  ],
  "links": {
    "related": "https://reactor.adobe.io/libraries/LB09eca17e012842b49466506f419283a7/data_elements",
    "self": "https://reactor.adobe.io/libraries/LB09eca17e012842b49466506f419283a7/relationships/data_elements"
  }
}
```

### Sostituire le risorse di una libreria {#replace-resources}

Puoi sostituire tutte le risorse esistenti di un certo tipo per una libreria aggiungendo `/relationships` al percorso di una richiesta PATCH, seguito dal tipo di risorsa che stai sostituendo.

**Formato API**

```http
PATCH /libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Parametro | Descrizione |
| --- | --- |
| `{LIBRARY_ID}` | ID della libreria di cui si desidera sostituire le relazioni. |
| `{RESOURCE_TYPE}` | Il tipo di risorsa da sostituire. Sono accettati i seguenti valori: <ul><li>`data_elements`</li><li>`extensions`</li><li>`rules`</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La seguente richiesta sostituisce le estensioni di una libreria con quelle fornite nell&#39;array `data` .

```shell
curl -X PATCH \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": [
          {
            "id": "EX58312732fd0f43f98037d765ef96c4cd",
            "type": "extensions"
          }
        ]
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID della risorsa che stai aggiungendo alla libreria. |
| `type` | Il tipo di risorsa che si sta aggiungendo alla libreria. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli delle relazioni aggiornate. L&#39;esecuzione di una [richiesta di ricerca](#lookup) per la libreria mostra le relazioni sotto la proprietà `relationships` .

```json
{
  "data": [
    {
      "type": "extensions",
      "id": "EX58312732fd0f43f98037d765ef96c4cd"
    }
  ],
  "links": {
    "related": "https://reactor.adobe.io/libraries/LBdbc7c49ac8f040bc9576db26b127444d/extensions",
    "self": "https://reactor.adobe.io/libraries/LBdbc7c49ac8f040bc9576db26b127444d/relationships/extensions"
  }
}
```

### Rimuovere risorse da una libreria {#remove-resources}

Puoi rimuovere risorse esistenti da una libreria aggiungendo `/relationships` al percorso di una richiesta DELETE, seguito dal tipo di risorsa che stai rimuovendo.

**Formato API**

```http
DELETE /libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Parametro | Descrizione |
| --- | --- |
| `{LIBRARY_ID}` | ID della libreria di cui desideri rimuovere le risorse. |
| `{RESOURCE_TYPE}` | Tipo di risorsa da rimuovere. Sono accettati i seguenti valori: <ul><li>`data_elements`</li><li>`extensions`</li><li>`rules`</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La seguente richiesta rimuove una regola da una libreria. Eventuali regole esistenti non incluse nell&#39;array `data` non vengono eliminate.

```shell
curl -X DELETE \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": [
          {
            "id": "RLa16f7859c7404239940c2cf2ec02b03c",
            "type": "rules"
          }
        ]
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID della risorsa che stai rimuovendo dalla libreria. |
| `type` | Il tipo di risorsa che stai rimuovendo dalla libreria. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli delle relazioni aggiornate per il tipo di risorsa. Se non esistono relazioni per questo tipo di risorsa, la proprietà `data` viene restituita come matrice vuota. L&#39;esecuzione di una [richiesta di ricerca](#lookup) per la libreria mostra le relazioni sotto la proprietà `relationships` .

```json
{
  "data": [

  ],
  "links": {
    "related": "https://reactor.adobe.io/libraries/LBbde5759742844fe59458ca0c988ecd61/rules",
    "self": "https://reactor.adobe.io/libraries/LBbde5759742844fe59458ca0c988ecd61/relationships/rules"
  }
}
```

## Assegnare una libreria a un ambiente {#environment}

È possibile assegnare una libreria a un ambiente `/relationships/environment` al percorso di una richiesta POST.

**Formato API**

```http
POST /libraries/{LIBRARY_ID}/relationships/environment
```

| Parametro | Descrizione |
| --- | --- |
| `{LIBRARY_ID}` | ID della libreria da assegnare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X POST \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "id": "EN867c480dc5ea4158be3ea68e5543bd85",
          "type": "environments"
        }
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID dell&#39;ambiente a cui assegni la libreria. |
| `type` | Deve essere impostato su `environments`. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli della relazione. L&#39;esecuzione di una [richiesta di ricerca](#lookup) per la libreria mostra la relazione aggiunta sotto la proprietà `relationships` .

```json
{
  "data": {
    "id": "EN867c480dc5ea4158be3ea68e5543bd85",
    "type": "environments"
  },
  "links": {
    "related": "https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/environment",
    "self": "https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment"
  }
}
```

## Transizione di una libreria {#transition}

Puoi passare una libreria a un altro stato di pubblicazione includendo il relativo ID nel percorso di una richiesta PATCH e fornendo un valore `meta.action` appropriato nel payload.

**Formato API**

```http
PATCH /libraries/{LIBRARY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `LIBRARY_ID` | Il `id` della libreria di cui desideri eseguire la transizione. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta seguente sposta lo stato di una libreria esistente in base al valore di `meta.action` fornito nel payload. Le azioni disponibili per una libreria dipendono dal suo stato di pubblicazione corrente, come descritto in [flusso di pubblicazione](../../ui/publishing/publishing-flow.md#state).

```shell
curl -X PATCH \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "id": "LB80c337c956804738b2db2ea2f69fcdf0",
          "type": "libraries",
          "meta": {
            "action": "submit"
          }
        }
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `meta.action` | L&#39;azione di transizione specifica che desideri eseguire sulla libreria. Sono disponibili le azioni seguenti, a seconda dello stato di pubblicazione corrente della libreria: <ul><li>`develop`</li><li>`submit`</li><li>`approve`</li><li>`reject`</li></ul> |
| `id` | Il `id` della libreria da aggiornare. Questo deve corrispondere al valore `{LIBRARY_ID}` fornito nel percorso della richiesta. |
| `type` | Tipo di risorsa da aggiornare. Per questo endpoint, il valore deve essere `libraries`. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli della libreria aggiornata.

```json
{
  "data": {
    "id": "LB80c337c956804738b2db2ea2f69fcdf0",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:47:57.783Z",
      "name": "My Library",
      "published_at": null,
      "state": "submitted",
      "updated_at": "2020-12-14T17:48:06.431Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/builds"
        }
      },
      "environment": {
        "links": {
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/environment"
        },
        "data": null
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/extensions",
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/rules",
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/property"
        },
        "data": {
          "id": "PRbc84c93c1c9f48c9836ade5ea4199006",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/last_build"
        },
        "data": {
          "id": "BL8d6e931f2f6d48ea96d6730122f13bcc",
          "type": "builds"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRbc84c93c1c9f48c9836ade5ea4199006",
      "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```

## Pubblicare una libreria {#publish}

>[!NOTE]
>
>Solo le librerie approvate possono essere pubblicate in produzione.

Per pubblicare una libreria in produzione, accertati che un ambiente di produzione sia stato aggiunto alla libreria, quindi crea una build.

**Formato API**

```http
POST /libraries/{LIBRARY_ID}/builds
```

| Parametro | Descrizione |
| --- | --- |
| `LIBRARY_ID` | Il `id` della libreria che desideri pubblicare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

Questa richiesta non richiede un payload.

```shell
curl -X POST \
  https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/builds \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
```

**Risposta**

```json
{
  "data": {
    "id": "BL162b63703eb74c6bb3c12471e0062c05",
    "type": "builds",
    "attributes": {
      "created_at": "2020-12-14T17:48:18.731Z",
      "status": "pending",
      "updated_at": "2020-12-14T17:48:18.731Z",
      "token": "b223fc55df1c"
    },
    "relationships": {
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/rules"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/environment"
        },
        "data": {
          "id": "EN5428335fff304c749f06a241db137a60",
          "type": "environments"
        }
      },
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/library"
        },
        "data": {
          "id": "LBa937e62887e94d85b77cbe703f5dfc56",
          "type": "libraries"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/property"
        },
        "data": {
          "id": "PR7e2b7aaaffcb499398010ba964603415",
          "type": "properties"
        }
      }
    },
    "links": {
      "environment": "https://reactor.adobe.io/environments/EN5428335fff304c749f06a241db137a60",
      "library": "https://reactor.adobe.io/libraries/LBa937e62887e94d85b77cbe703f5dfc56",
      "self": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05"
    },
    "meta": {
      "artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/8b659dd115cf/launch-5986a1b644a4-development.min.js",
      "direct_artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/8b659dd115cf/b223fc55df1c/launch-5986a1b644a4-development.min.js",
      "archive": false,
      "host_type_of": "akamai"
    }
  }
}
```

## Gestire le note per una libreria {#notes}

Le librerie sono risorse &quot;di rilievo&quot;, il che significa che puoi creare e recuperare note basate su testo su ogni singola risorsa. Per ulteriori informazioni su come gestire le note per le librerie e altre risorse compatibili, consulta la [guida all’endpoint delle note](./notes.md) .

## Recuperare le risorse correlate per una libreria {#related}

Le seguenti chiamate mostrano come recuperare le risorse correlate per una libreria. Quando [cerca una libreria](#lookup), queste relazioni sono elencate nella proprietà `relationships` .

Per ulteriori informazioni sulle relazioni nell&#39;API del reattore, consulta la [guida alle relazioni](../guides/relationships.md) .

### Elencare gli elementi dati correlati per una libreria {#data-elements}

Puoi elencare gli elementi dati utilizzati da una libreria aggiungendo `/data_elements` al percorso di una richiesta di ricerca.

**Formato API**

```http
GET  /libraries/{LIBRARY_ID}/data_elements
```

| Parametro | Descrizione |
| --- | --- |
| `{LIBRARY_ID}` | Il `id` della libreria di cui si desidera elencare gli elementi dati. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

Una risposta corretta restituisce un elenco di elementi dati che utilizzano la libreria specificata.

```json
{
  "data": [
    {
      "id": "DE4956628e8baa4b358cc592337049b37b",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:45:11.694Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:45:10 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:45:11.694Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/property"
          },
          "data": {
            "id": "PR245ca5e560784249b2a88ef82f2851b6",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/origin"
          },
          "data": {
            "id": "DE4c027939f2004fdcb15e3b4099e70974",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/extension"
          },
          "data": {
            "id": "EX5942ffd7fac94428875bd664e397bd47",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/updated_with_extension"
          },
          "data": {
            "id": "EXbf411638b90843c486254b5ca0fe47d6",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR245ca5e560784249b2a88ef82f2851b6",
        "origin": "https://reactor.adobe.io/data_elements/DE4c027939f2004fdcb15e3b4099e70974",
        "self": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b",
        "extension": "https://reactor.adobe.io/extensions/EX5942ffd7fac94428875bd664e397bd47"
      },
      "meta": {
        "latest_revision_number": 1
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

### Elencare le estensioni correlate per una libreria {#extensions}

Puoi elencare le estensioni utilizzate da una libreria aggiungendo `/extensions` al percorso di una richiesta di ricerca.

**Formato API**

```http
GET  /libraries/{LIBRARY_ID}/extensions
```

| Parametro | Descrizione |
| --- | --- |
| `{LIBRARY_ID}` | Il `id` della libreria di cui desideri elencare le estensioni. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/extensions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

Una risposta corretta restituisce un elenco di estensioni che utilizzano la libreria specificata.

```json
{
  "data": [
    {
      "id": "EXac1e55883e5b47eb9a3589b311960677",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:45:23.759Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:45:23.759Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/property"
          },
          "data": {
            "id": "PR2d1f3ba867204dc7a4c17614d23bbab0",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/origin"
          },
          "data": {
            "id": "EX63cf3b91ec8146889759bbacb15627c3",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR2d1f3ba867204dc7a4c17614d23bbab0",
        "origin": "https://reactor.adobe.io/extensions/EX63cf3b91ec8146889759bbacb15627c3",
        "self": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677",
        "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
        "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
      },
      "meta": {
        "latest_revision_number": 1
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

### Elencare le regole correlate per una libreria {#rules}

Puoi elencare le regole utilizzate da una libreria aggiungendo `/rules` al percorso di una richiesta di ricerca.

**Formato API**

```http
GET  /libraries/{LIBRARY_ID}/rules
```

| Parametro | Descrizione |
| --- | --- |
| `{LIBRARY_ID}` | Il `id` della libreria di cui si desidera elencare le regole. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

Una risposta corretta restituisce un elenco di regole che utilizzano la libreria specificata.

```json
{
  "data": [
    {
      "id": "RL460e550125054fffb824cce56c8cb1ac",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:45:36.405Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:45:36.405Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/property"
          },
          "data": {
            "id": "PRa68d0d2c6e0a4ae380fb30f17f7c435d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/origin"
          },
          "data": {
            "id": "RL04911614524d463a9c115bea442bce72",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRa68d0d2c6e0a4ae380fb30f17f7c435d",
        "origin": "https://reactor.adobe.io/rules/RL04911614524d463a9c115bea442bce72",
        "self": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac",
        "rule_components": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/rule_components"
      },
      "meta": {
        "latest_revision_number": 1
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

### Cercare l&#39;ambiente correlato per una libreria {#related-environment}

Puoi cercare l&#39;ambiente a cui è assegnata una libreria aggiungendo `/environment` al percorso di una richiesta GET.

**Formato API**

```http
GET  /libraries/{LIBRARY_ID}/environment
```

| Parametro | Descrizione |
| --- | --- |
| `{LIBRARY_ID}` | Il `id` della libreria di cui desideri cercare l&#39;ambiente. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

Una risposta corretta restituisce i dettagli dell&#39;ambiente a cui è assegnata la libreria specificata.

```json
{
  "data": {
    "id": "ENe66122e6793641d8a8453f63c42e4270",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2020-12-14T17:39:12.484Z",
      "library_path": "f9fd106ab399/2df53b69e8a2",
      "library_name": "launch-1d2ffee7eef5-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-1d2ffee7eef5-development.min.js",
          "minified": true,
          "references": [
            "f9fd106ab399/2df53b69e8a2/launch-1d2ffee7eef5-development.min.js"
          ],
          "license_path": "f9fd106ab399/2df53b69e8a2/launch-1d2ffee7eef5-development.js"
        },
        {
          "library_name": "launch-1d2ffee7eef5-development.js",
          "minified": false,
          "references": [
            "f9fd106ab399/2df53b69e8a2/launch-1d2ffee7eef5-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": "https://assets.adobedtm.com/staging",
      "stage": "development",
      "updated_at": "2020-12-14T17:39:13.988Z",
      "status": "succeeded",
      "token": "1d2ffee7eef5"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/library"
        },
        "data": {
          "id": "LB52ccd7f1e99146999f90cb3bca4940a2",
          "type": "libraries"
        }
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/host",
          "self": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/relationships/host"
        },
        "data": {
          "id": "HT53a4ebcb177d431e8fd26929930de0af",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/property"
        },
        "data": {
          "id": "PR79de7e0885a9451786f1bf4b9136a72c",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR79de7e0885a9451786f1bf4b9136a72c",
      "self": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

### Cerca la proprietà correlata per una libreria {#property}

Puoi cercare la proprietà proprietaria di una libreria aggiungendo `/property` al percorso di una richiesta GET.

**Formato API**

```http
GET  /libraries/{LIBRARY_ID}/property
```

| Parametro | Descrizione |
| --- | --- |
| `{LIBRARY_ID}` | Il `id` della libreria di cui desideri cercare la proprietà. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

Una risposta corretta restituisce i dettagli della proprietà proprietaria della libreria specificata.

```json
{
  "data": {
    "id": "PRb18ac8f8b69d4f99af43870e91c17543",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:51:56.180Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:51:56.180Z",
      "platform": "web",
      "development": false,
      "token": "9d97006b0f9b",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/environments",
      "extensions": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/extensions",
      "rules": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/rules",
      "self": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```

### Cerca una libreria a monte {#upstream}

Puoi cercare la libreria successiva a monte da una libreria aggiungendo `/upstream_library` al percorso di una richiesta GET.

**Formato API**

```http
GET  /libraries/{LIBRARY_ID}/upstream_library
```

| Parametro | Descrizione |
| --- | --- |
| `{LIBRARY_ID}` | La `id` della libreria di cui desideri cercare la libreria a monte. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/upstream_library \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

Una risposta corretta restituisce i dettagli della libreria a monte.

```json
{
  "data": {
    "id": "LB29cc2f86b3684e00a10d196a60f4b0c0",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:49:32.459Z",
      "name": "My Library",
      "published_at": null,
      "state": "submitted",
      "updated_at": "2020-12-14T17:49:41.070Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/builds"
        }
      },
      "environment": {
        "links": {
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/environment"
        },
        "data": null
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/extensions",
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/rules",
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/property"
        },
        "data": {
          "id": "PR7c206ed399644222aef329488cee7fa7",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/last_build"
        },
        "data": {
          "id": "BL87cde018ecd44ac7a20b0271ab06d04b",
          "type": "builds"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR7c206ed399644222aef329488cee7fa7",
      "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```
