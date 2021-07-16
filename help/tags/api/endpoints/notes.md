---
title: Endpoint note
description: Scopri come effettuare chiamate all’endpoint /notes nell’API del reattore.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 7%

---

# Endpoint note

Nell’API di Reactor, le note sono annotazioni testuali che possono essere aggiunte ad alcune risorse. Le note sono essenzialmente commenti sulle rispettive risorse. Il contenuto delle note non ha alcun impatto sul comportamento delle risorse e può essere utilizzato per diversi casi d’uso, tra cui:

* Informazioni di base
* Funzionamento degli elenchi
* Passaggio lungo i consigli sull’utilizzo delle risorse
* Istruzioni ad altri membri del team
* Contesto storico della registrazione

L’endpoint `/notes` nell’API di Reactor consente di gestire queste note a livello di programmazione.

Le note possono essere applicate alle seguenti risorse:

* [Elementi dati](./data-elements.md)
* [Estensioni](./extensions.md)
* [Librerie](./libraries.md)
* [Proprietà](./properties.md)
* [Componenti della regola](./rule-components.md)
* [Regole](./rules.md)

Questi sei tipi sono noti collettivamente come risorse &quot;notevoli&quot;. Quando una risorsa notevole viene eliminata, vengono eliminate anche le relative note associate.

>[!NOTE]
>
>Per le risorse che possono avere più revisioni, tutte le note devono essere create nella revisione corrente (head). Non possono essere collegate ad altre revisioni.
>
>Tuttavia, le note possono ancora essere lette da revisioni. In questi casi, l’API restituisce solo le note esistenti prima della creazione della revisione. Offrono un’istantanea delle annotazioni così come erano quando la revisione è stata tagliata. Al contrario, la lettura delle note della revisione corrente (head) restituisce tutte le note.

## Introduzione

L&#39;endpoint utilizzato in questa guida fa parte dell&#39; [API del reattore](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Prima di continuare, controlla la [guida introduttiva](../getting-started.md) per informazioni importanti su come eseguire l&#39;autenticazione nell&#39;API.

## Recupera un elenco di note {#list}

Puoi recuperare un elenco di note per una risorsa aggiungendo `/notes` al percorso di una richiesta di GET per la risorsa in questione.

**Formato API**

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Parametro | Descrizione |
| --- | --- |
| `RESOURCE_TYPE` | Il tipo di risorsa per cui vengono recuperate le note. Deve essere uno dei seguenti valori: <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | La `id` della risorsa specifica di cui si desidera elencare le note. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

Nella richiesta seguente sono elencate le note collegate a una libreria.

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

Una risposta corretta restituisce un elenco di note associate alla risorsa specificata.

```json
{
  "data": [
    {
      "id": "NTa40de8d76bfd4e40835830900ce83b7b",
      "type": "notes",
      "attributes": {
        "author_display_name": "John Smith",
        "author_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:51:00.411Z",
        "text": "this is a note on a library"
      },
      "relationships": {
        "resource": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d"
          },
          "data": {
            "id": "LBcffea1a38c52408cae2398868625a12d",
            "type": "libraries"
          }
        }
      },
      "links": {
        "resource": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d",
        "self": "https://reactor.adobe.io/notes/NTa40de8d76bfd4e40835830900ce83b7b"
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

## Cerca una nota {#lookup}

Puoi cercare una nota inserendone l’ID nel percorso di una richiesta GET.

**Formato API**

```http
GET /notes/{NOTE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `NOTE_ID` | La `id` della nota che si desidera cercare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

Una risposta corretta restituisce i dettagli della nota.

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "this is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```

## Creare una nota {#create}

>[!WARNING]
>
>Prima di creare una nuova nota, tenere presente che le note non sono modificabili e che l’unico modo per eliminarle consiste nell’eliminare la risorsa corrispondente.

Puoi creare una nuova nota aggiungendo `/notes` al percorso di una richiesta POST per la risorsa in questione.

**Formato API**

```http
POST /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Parametro | Descrizione |
| --- | --- |
| `RESOURCE_TYPE` | Il tipo di risorsa per cui si sta creando una nota. Deve essere uno dei seguenti valori: <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | La `id` della risorsa specifica per la quale desideri creare una nota. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

Nella richiesta seguente viene creata una nuova nota per una proprietà.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "type": "notes",
          "attributes": {
            "text": "this is a note on a property"
          }
        }
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `type` | **(Obbligatorio)** Il tipo di risorsa da aggiornare. Per questo endpoint, il valore deve essere `notes`. |
| `attributes.text` | **(Obbligatorio)** Testo che comprende la nota. Ogni nota è limitata a 512 caratteri Unicode. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli della nota appena creata.

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "This is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```
