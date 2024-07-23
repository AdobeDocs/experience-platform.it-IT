---
title: Endpoint autorizzazioni utilizzo pacchetto estensione
description: Scopri come effettuare chiamate all’endpoint per le autorizzazioni /extension_package_usage nell’API di Reactor.
exl-id: ad3fb704-7d2f-45ec-b80b-ea4d327f2205
source-git-commit: 9cdd349e0eccb4498d88f24a84b0f1c116b0adfe
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 16%

---

# Endpoint di autorizzazioni di utilizzo del pacchetto di estensione

Un pacchetto di estensione rappresenta un’[estensione](./extensions.md) creata da uno sviluppatore di estensioni. Ulteriori funzionalità che possono essere rese disponibili agli utenti di tag sono definite da un pacchetto di estensione. Queste funzionalità possono includere moduli principali e moduli condivisi, anche se vengono spesso fornite come [componenti regola](./rule-components.md) (eventi, condizioni e azioni) e [elementi dati](./data-elements.md).

Un pacchetto di estensione appartiene alla [società](./companies.md) dello sviluppatore. I proprietari dei pacchetti di estensione possono autorizzare altre aziende a utilizzare le loro versioni private dei pacchetti. A ogni azienda autorizzata viene concessa un’autorizzazione di utilizzo per un singolo pacchetto di estensione, valida per tutte le versioni private future e correnti del pacchetto.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’[API di Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Prima di continuare, consulta la [guida introduttiva](../getting-started.md) per informazioni importanti su come eseguire l’autenticazione nell’API.

## Recuperare le autorizzazioni di utilizzo del pacchetto di estensione per un pacchetto di estensione {#list}

Per recuperare un elenco di autorizzazioni di utilizzo per un pacchetto di estensione, effettua una richiesta GET all’endpoint seguente.

**Formato API**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parametro | Descrizione |
| --- | --- |
| `{PROPERTY_ID}` | `ID` della proprietà di cui desideri elencare l’autorizzazione per l’utilizzo del pacchetto di estensione. |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di pacchetti di estensione.

```json
{
  "data": [
    {
      "id": "EA722482c30fe44b54aa6a7317890b3bdb",
      "type": "extension_package_usage_authorizations",
      "attributes": {
        "created_at": "2024-06-05T23:17:35.776Z",
        "updated_at": "2024-06-05T23:17:35.776Z",
        "name": "Acme",
        "platform": "web",
        "owner_org_id": "{ORG_ID}",
        "owner_org_name": "Reactor QE",
        "authorized_org_id": "{ORG_ID}",
        "authorized_org_name": "Acme Inc'",
        "state": "pending_approval",
        "created_by_email": "example@adobe.com",
        "created_by_display_name": "john snow",
        "updated_by_email": "Restricted",
        "updated_by_display_name": "Restricted"
      },
      "relationships": {
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA722482c30fe44b54aa6a7317890b3bdb/extension_package"
          },
          "data": {
            "id": "EPecefc8291ae346c3b3887d5b2da533b8",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA722482c30fe44b54aa6a7317890b3bdb"
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

## Creare un’autorizzazione per l’utilizzo del pacchetto di estensione {#create}

Creare un&#39;autorizzazione per l&#39;utilizzo del pacchetto di estensione per ogni [pacchetto di estensione](./extension-packages.md) e `{ORG_ID}` dell&#39;organizzazione che si desidera autorizzare. Per creare una nuova autorizzazione per l’utilizzo del pacchetto di estensione, effettua una richiesta POST all’endpoint seguente.

**Formato API**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parametro | Descrizione |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | `ID` del pacchetto di estensione per il quale si desidera creare un&#39;autorizzazione.&quot; |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "authorized_org_id": "{ORG_ID}"
          },
          "type": "extension_package_usage_authorizations"
        }
      } 
```

| Proprietà | Descrizione |
| --- | --- |
| `attributes.authorized_org_id` | `ID` dell&#39;organizzazione che si desidera autorizzare. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della nuova autorizzazione per l’utilizzo del pacchetto di estensione.

```json
{
  "data": {
    "id": "EA35d0e731f73645e6972df9fcac101434",
    "type": "extension_package_usage_authorizations",
    "attributes": {
      "created_at": "2024-06-05T23:17:30.308Z",
      "updated_at": "2024-06-05T23:17:30.308Z",
      "name": "Acme",
      "platform": "web",
      "owner_org_id": "{ORG_ID}",
      "owner_org_name": "Reactor QE",
      "authorized_org_id": "{ORG_ID}",
      "authorized_org_name": "Acme Inc'",
      "state": "pending_approval",
      "created_by_email": "example@adobe.com",
      "created_by_display_name": "john snow",
      "updated_by_email": "Restricted",
      "updated_by_display_name": "Restricted"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434/extension_package"
        },
        "data": {
          "id": "EP43649cc8856d4f09a7c2a21a4b1e449d",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434"
    }
  }
}
```

>[!NOTE]
>
>Nell&#39;esempio di risposta precedente, l&#39;autorizzazione si trova attualmente nella fase `pending_approval`. Prima di utilizzare il pacchetto di estensione, l’organizzazione deve approvare l’autorizzazione. Gli utenti dell’organizzazione possono sfogliare il pacchetto di estensione privato mentre l’autorizzazione è in attesa di approvazione, ma non sono in grado di installarlo e non possono trovarlo nel catalogo delle estensioni.

## Recuperare un elenco di autorizzazioni di utilizzo del pacchetto di estensione {#list-authorizations}

Per recuperare un elenco di autorizzazioni di utilizzo del pacchetto di estensione, effettua una richiesta GET.

**Formato API**

```http
GET /extension_package_usage_authorizations
```

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di pacchetti di estensione.

```json
{
  "data": [
    {
      "id": "EA35d0e731f73645e6972df9fcac101434",
      "type": "extension_package_usage_authorizations",
      "attributes": {
        "created_at": "2024-06-05T23:17:30.308Z",
        "updated_at": "2024-06-05T23:17:30.308Z",
        "name": "Acme",
        "platform": "web",
        "owner_org_id": "{ORG_ID}",
        "owner_org_name": "Reactor QE",
        "authorized_org_id": "{ORG_ID}",
        "authorized_org_name": "Acme Inc'",
        "state": "pending_approval",
        "created_by_email": "Restricted",
        "created_by_display_name": "Restricted",
        "updated_by_email": "example@adobe.com",
        "updated_by_display_name": "john snow"
      },
      "relationships": {
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434/extension_package"
          },
          "data": null
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434"
      }
    }
  ],
  "links": {
    "self": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=1&page%5Bsize%5D=25",
    "next": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=2&page%5Bsize%5D=25",
    "last": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=3&page%5Bsize%5D=25"
  },
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": 2,
      "prev_page": null,
      "total_pages": 3,
      "total_count": 57
    }
  }
}
```

## Eliminare l’autorizzazione per l’utilizzo di un pacchetto di estensione {#delete}

Per eliminare l&#39;autorizzazione di utilizzo di un pacchetto di estensione, includi `ID` nel percorso di una richiesta DELETE. Questo impedisce all’organizzazione autorizzata di visualizzare le versioni private del pacchetto di estensione nel catalogo e di installarlo nelle relative proprietà.

>[!NOTE]
>
>Qualsiasi versione privata installata in precedenza continuerà a funzionare come previsto.

**Formato API**

```http
DELETE /extension_package_usage_authorizations/{ID}
```

| Parametro | Descrizione |
| --- | --- |
| `ID` | `ID` dell&#39;autorizzazione di utilizzo del pacchetto di estensione che si desidera eliminare. |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto) senza corpo di risposta. Indica che l&#39;estensione è stata eliminata.

## Aggiornare l’autorizzazione per l’utilizzo di un pacchetto di estensione {#update}

Per approvare o rifiutare l&#39;autorizzazione per l&#39;utilizzo di un pacchetto di estensione, includi `ID` nel percorso di una richiesta PATCH.

>[!NOTE]
>
>Per approvare o rifiutare l&#39;autorizzazione per l&#39;utilizzo di un pacchetto di estensione per la società, è necessario disporre di `manage_properties` diritti.

**Formato API**

```http
PATCH /extension_package_usage_authorizations/{ID}
```

| Parametro | Descrizione |
| --- | --- |
| `ID` | `ID` dell&#39;autorizzazione di utilizzo del pacchetto di estensione che si desidera eliminare. |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "state": "approved"
          },
          "type": "extension_package_usage_authorizations",
          "id": "EA86f54b48dd7042a68686508e03be8ba9"
        }
      } 
```

| Proprietà | Descrizione |
| --- | --- |
| `attributes` | Attributi che desideri rivedere. Per le autorizzazioni di utilizzo del pacchetto di estensione è possibile rivedere `state`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli dell’autorizzazione di utilizzo del pacchetto di estensione rivista.

```json
{
  "data": {
    "id": "EA86f54b48dd7042a68686508e03be8ba9",
    "type": "extension_package_usage_authorizations",
    "attributes": {
      "created_at": "2024-06-05T23:17:59.480Z",
      "updated_at": "2024-06-05T23:18:00.115Z",
      "name": "Acme",
      "platform": "web",
      "owner_org_id": "{ORG_ID}",
      "owner_org_name": "Reactor QE",
      "authorized_org_id": "{ORG_ID}",
      "authorized_org_name": "Acme Inc'",
      "state": "approved",
      "created_by_email": "Restricted",
      "created_by_display_name": "Restricted",
      "updated_by_email": "example@adobe.com",
      "updated_by_display_name": "john snow"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA86f54b48dd7042a68686508e03be8ba9/extension_package"
        },
        "data": {
          "id": "EPb91d54cad9f749dba4e5566459f84c9c",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA86f54b48dd7042a68686508e03be8ba9"
    }
  }
}
```

>[!NOTE]
>
>Una volta approvata l’autorizzazione, l’organizzazione può installare il pacchetto di estensione sulle proprietà.

## Recuperare i dati per il pacchetto di estensione per l’autorizzazione di utilizzo di un pacchetto di estensione {#retrieve-data}

Per recuperare i dati del pacchetto di estensione per l’autorizzazione di utilizzo di un pacchetto di estensione, effettua una richiesta GET.

**Formato API**

```http
GET /extension_package_usage_authorizations/{ID}/extension_package
```

| Parametro | Descrizione |
| --- | --- |
| `ID` | `ID` dell&#39;autorizzazione di utilizzo del pacchetto di estensione che si desidera recuperare. |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID}/extension_package \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dati per il pacchetto di estensione per l’autorizzazione di un pacchetto di estensione.

```json
{
  "data": {
    "id": "EP45ae063fd75c4c22936d3d456c858cfa",
    "type": "extension_packages",
    "attributes": {
      "actions": [],
      "author": {
        "url": "http://adobe.com",
        "name": "Acme",
        "email": "acme@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP45ae063fd75c4c22936d3d456c858cfa",
      "conditions": [],
      "configuration": null,
      "created_at": "2024-06-05T23:17:48.607Z",
      "data_elements": [],
      "description": "Provides nothing.",
      "discontinued": false,
      "display_name": "Acme Template Test",
      "ecma_version": null,
      "events": [],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": "null",
      "name": "Acme",
      "owner_org_id": "{ORG_ID}",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2024-06-05T23:17:53.806Z",
      "version": "1.0.0",
      "view_base_path": "dist/",
      "created_by_email": "example@adobe.com",
      "created_by_display_name": "john snow",
      "updated_by_email": "example@adobe.com",
      "updated_by_display_name": "john snow"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_packages/EP45ae063fd75c4c22936d3d456c858cfa/extension_package_usage_authorizations"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP45ae063fd75c4c22936d3d456c858cfa"
    }
  }
}
```
