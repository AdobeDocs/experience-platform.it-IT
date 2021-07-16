---
title: Endpoint aziendale
description: Scopri come effettuare chiamate all’endpoint /company nell’API Reactor.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 4%

---

# Endpoint aziendale

Un&#39;azienda rappresenta un&#39;organizzazione cliente, in genere un&#39;azienda. Nell’API di Reactor, queste società corrispondono a 1:1 con l’ID organizzazione IMS. Gli utenti API hanno solo visibilità nelle aziende a cui hanno accesso. Un&#39;azienda può contenere molte [proprietà](./properties.md). Una proprietà appartiene esattamente a una società.

L’endpoint `/companies` nell’API di Reactor ti consente di recuperare in modo programmatico le società a cui hai accesso all’interno dell’applicazione di esperienza.

## Introduzione

L&#39;endpoint utilizzato in questa guida fa parte dell&#39; [API del reattore](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Prima di continuare, controlla la [guida introduttiva](../getting-started.md) per informazioni importanti su come eseguire l&#39;autenticazione nell&#39;API.

## Recupera un elenco di aziende {#list}

Puoi elencare le aziende a cui sei autorizzato a utilizzare effettuando una richiesta di GET all’endpoint `/companies` . Nella maggior parte dei casi ce n&#39;è esattamente uno.

**Formato API**

```http
GET /companies
```

>[!NOTE]
>
>Utilizzando i parametri di query, le società elencate possono essere filtrate in base ai seguenti attributi:<ul><li>`created_at`</li><li>`name`</li><li>`org_id`</li><li>`token`</li><li>`updated_at`</li></ul>Per ulteriori informazioni, consulta la guida sulle [risposte relative al filtro](../guides/filtering.md) .

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

Una risposta corretta restituisce un elenco di aziende a cui hai accesso.

```json
{
  "data": [
    {
      "id": "COdb0cd64ad4524440be94b8496416ec7d",
      "type": "companies",
      "attributes": {
        "created_at": "2020-08-13T17:13:30.667Z",
        "name": "Example Company",
        "org_id": "{IMS_ORG}",
        "updated_at": "2020-08-13T17:13:30.667Z",
        "token": "d5a4f682bbae",
        "cjm_enabled": false,
        "edge_enabled": false,
        "edge_events_allotment": null,
        "edge_fanout_ratio": null
      },
      "relationships": {
        "properties": {
          "links": {
            "related": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d",
        "properties": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
      },
      "meta": {
        "rights": [
          "develop_extensions",
          "manage_properties"
        ],
        "platform_rights": {
          "web": [
            "develop_extensions",
            "manage_properties"
          ],
          "mobile": [
            "develop_extensions",
            "manage_properties"
          ]
        }
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

## Cerca un&#39;azienda {#lookup}

Puoi cercare una società specifica includendo il relativo ID nel percorso di una richiesta di GET.

**Formato API**

```http
GET /companies/{COMPANY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{COMPANY_ID}` | Il valore `id` della società che si desidera cercare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

Una risposta corretta restituisce i dettagli dell&#39;azienda.

```json
{
  "data": {
    "id": "COdb0cd64ad4524440be94b8496416ec7d",
    "type": "companies",
    "attributes": {
      "created_at": "2020-08-13T17:13:30.667Z",
      "name": "Example Company",
      "org_id": "{IMS_ORG}",
      "updated_at": "2020-08-13T17:13:30.667Z",
      "token": "d5a4f682bbae",
      "cjm_enabled": false,
      "edge_enabled": false,
      "edge_events_allotment": null,
      "edge_fanout_ratio": null
    },
    "relationships": {
      "properties": {
        "links": {
          "related": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d",
      "properties": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
    },
    "meta": {
      "rights": [
        "develop_extensions",
        "manage_properties"
      ],
      "platform_rights": {
        "web": [
          "develop_extensions",
          "manage_properties"
        ],
        "mobile": [
          "develop_extensions",
          "manage_properties"
        ]
      }
    }
  }
}
```
