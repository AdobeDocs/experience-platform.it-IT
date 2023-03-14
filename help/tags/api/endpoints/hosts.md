---
title: Endpoint “hosts”
description: Scopri come effettuare chiamate all’endpoint /hosts nell’API di Reactor.
exl-id: 9d0d2a65-49e9-429c-a665-754b59a11cf1
source-git-commit: 905384b3190cd55e7caa9c4560d6b2774280eee7
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 92%

---

# Endpoint “hosts”

>[!NOTE]
>
>Questo documento illustra come gestire gli host nell’API di Reactor. Per informazioni generali sugli host per i tag, consulta la [panoramica sugli host](../../ui/publishing/hosts/hosts-overview.md) nella documentazione relativa alla pubblicazione.

Nell’API di Reactor, un host definisce una destinazione in cui è possibile distribuire una [build](./builds.md).

Quando una build viene richiesta da un utente di tag in Adobe Experience Platform, il sistema controlla la libreria per determinare per quale [ambiente](./environments.md) deve essere generata la libreria. Ogni ambiente ha una relazione con un host, che indica dove distribuire la build.

Un host appartiene esattamente a una [proprietà](./properties.md), mentre una proprietà può avere diversi host. Una proprietà deve avere almeno un host prima che sia possibilie pubblicare.

Un host può essere utilizzato da più ambienti all’interno di una proprietà. In genere viene usato un singolo host per una proprietà e tutti gli ambienti di tale proprietà utilizzano lo stesso host.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’[API di Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Prima di continuare, consulta la [guida introduttiva](../getting-started.md) per informazioni importanti su come eseguire l’autenticazione nell’API.

## Recuperare un elenco di host {#list}

Per recuperare un elenco di host per una proprietà, devi includere l’ID della proprietà nel percorso di una richiesta GET.

**Formato API**

```http
GET /properties/{PROPERTY_ID}/hosts
```

| Parametro | Descrizione |
| --- | --- |
| `PROPERTY_ID` | `id` della proprietà a cui appartengono gli host. |

{style="table-layout:auto"}

>[!NOTE]
>
>Utilizzando i parametri di query, gli host elencati possono essere filtrati in base ai seguenti attributi:<ul><li>`created_at`</li><li>`name`</li><li>`type_of`</li><li>`updated_at`</li></ul>Per ulteriori informazioni, consulta la guida su come [filtrare le risposte](../guides/filtering.md).

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di host per la proprietà specificata.

```json
{
  "data": [
    {
      "id": "HT405b8d9306004eb38106e66c8a4afc09",
      "type": "hosts",
      "attributes": {
        "created_at": "2020-12-14T17:42:35.239Z",
        "server": null,
        "name": "Example Akamai Host",
        "path": null,
        "port": null,
        "status": "succeeded",
        "type_of": "akamai",
        "updated_at": "2020-12-14T17:42:35.239Z",
        "username": null
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09/property"
          },
          "data": {
            "id": "PRd428c2a25caa4b32af61495f5809b737",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737",
        "self": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09"
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

## Cercare un host {#lookup}

Per cercare un host, devi fornire il suo ID nel percorso di una richiesta GET.

**Formato API**

```http
GET /hosts/{HOST_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `HOST_ID` | `id` dell’host che desideri cercare. |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli dell’host.

```json
{
  "data": {
    "id": "HT5d90148e72224224aac9bc0b01498b84",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:25.353Z",
      "server": "https://server.example.com",
      "name": "Example Akamai Host",
      "path": "/akamai",
      "port": 8000,
      "status": "succeeded",
      "type_of": "akamai",
      "updated_at": "2020-12-14T17:42:25.353Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property"
        },
        "data": {
          "id": "PRd7cf174259f34057b5c435ef873a79bf",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRd7cf174259f34057b5c435ef873a79bf",
      "self": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84"
    }
  }
}
```

## Creare un host {#create}

Per creare un nuovo host, effettua una richiesta POST.

**Formato API**

```http
POST /properties/{PROPERTY_ID}/hosts
```

| Parametro | Descrizione |
| --- | --- |
| `PROPERTY_ID` | `id` della [proprietà](./properties.md) in cui si sta definendo l’host. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente crea un nuovo host per la proprietà specificata. La chiamata associa inoltre l’host a un’estensione esistente tramite la proprietà `relationships`. Per ulteriori informazioni, consulta la guida delle [relazioni](../guides/relationships.md).

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example SFTP Host",
            "type_of": "sftp",
            "username": "John Doe",
            "encrypted_private_key": "{PRIVATE_KEY}",
            "server": "https://example.com",
            "skip_symlinks": true,
            "path": "assets",
            "port": 22
          },
          "type": "hosts"
        }
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `attributes.name` | **(Obbligatorio)** Nome leggibile per l’host. |
| `attributes.type_of` | **(Obbligatorio)** Tipo di host. Può essere una delle due opzioni seguenti: <ul><li>`akamai` per gli [host gestiti da Adobe](../../ui/publishing/hosts/managed-by-adobe-host.md)</li><li>`sftp` per gli [host SFTP](../../ui/publishing/hosts/sftp-host.md)</li></ul> |
| `attributes.encrypted_private_key` | Chiave privata opzionale da utilizzare per l’autenticazione host. |
| `attributes.path` | Percorso da aggiungere all’URL `server`. |
| `attributes.port` | Numero intero che indica la porta server specifica da utilizzare. |
| `attributes.server` | URL host per il server. |
| `attributes.skip_symlinks`<br><br>(Solo per host SFTP) | Per impostazione predefinita, tutti gli host SFTP utilizzano collegamenti simbolici (symlink) per fare riferimento alle build della libreria salvate sul server. Tuttavia, non tutti i server supportano l&#39;utilizzo di symlink. Quando questo attributo è incluso e impostato su `true`, l’host utilizza un’operazione di copia per aggiornare direttamente le risorse della build invece di utilizzare i symlink. |
| `attributes.username` | Nome utente facoltativo per l’autenticazione. |
| `type` | Tipo di risorsa da aggiornare. Per questo endpoint, il valore deve essere `hosts`. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del nuovo host creato.

```json
{
  "data": {
    "id": "HT69bfe634dead4a9a8c659f5d4d94cecd",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:07.033Z",
      "server": "//example.com",
      "name": "Example SFTP Host",
      "path": "assets",
      "port": 22,
      "status": "pending",
      "skip_symlinks": true,
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:07.033Z",
      "username": "John Doe"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd/property"
        },
        "data": {
          "id": "PRb25a704c0b7c4562835ccdf96d3afd31",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31",
      "self": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd"
    }
  }
}
```

## Aggiornare un host {#update}

>[!NOTE]
>
>È possibile aggiornare solo gli host SFTP.

Per aggiornare un host, devi includere il suo ID nel percorso di una richiesta PATCH.

**Formato API**

```http
PATCH /hosts/{HOST_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `HOST_ID` | `id` dell’host da aggiornare. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente aggiorna il `name` di un host esistente.

```shell
curl -X PATCH \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New host Name"
          },
          "id": "HT5d90148e72224224aac9bc0b01498b84",
          "type": "hosts"
        }
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `attributes` | Oggetto le cui proprietà rappresentano gli attributi da aggiornare per l’host. È possibile aggiornare i seguenti attributi di un host: <ul><li>`encrypted_private_key`</li><li>`name`</li><li>`path`</li><li>`port`</li><li>`server`</li><li>`type_of`</li><li>`username`</li></ul> |
| `id` | `id` dell’host da aggiornare. Deve corrispondere al valore `{HOST_ID}` fornito nel percorso della richiesta. |
| `type` | Tipo di risorsa da aggiornare. Per questo endpoint, il valore deve essere `hosts`. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli dell’host aggiornato.

```json
{
  "data": {
    "id": "HTb14e136a6fe147459b298a4645d2a6f5",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:45.087Z",
      "server": null,
      "name": "My SFTP host",
      "path": null,
      "port": null,
      "status": "succeeded",
      "skip_symlinks": true,
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:45.696Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5/property"
        },
        "data": {
          "id": "PR8f240526f7b54a4dbd46965e79519fde",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR8f240526f7b54a4dbd46965e79519fde",
      "self": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5"
    }
  }
}
```

## Eliminare un host

Per eliminare un host, devi includere il suo ID nel percorso di una richiesta DELETE.

**Formato API**

```http
DELETE /hosts/{HOST_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `HOST_ID` | `id` dell’host da eliminare. |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X DELETE \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto) senza corpo di risposta, indicando che l’host è stato eliminato.

## Recuperare le risorse correlate per un host {#related}

Le seguenti chiamate mostrano come recuperare le risorse correlate per un host. Quando si [cerca un host](#lookup), queste relazioni sono elencate nella proprietà `relationships`.

Per ulteriori informazioni sulle relazioni nell’API di Reactor, consulta la [guida delle relazioni](../guides/relationships.md).

### Cercare la proprietà correlata per un host {#property}

Per cercare la proprietà a cui appartiene un host, aggiungi `/property` al percorso di una richiesta di ricerca.

**Formato API**

```http
GET /hosts/{HOST_ID}/property
```

| Parametro | Descrizione |
| --- | --- |
| `{HOST_ID}` | `id` dell’host di cui desideri cercare la proprietà. |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della proprietà dell’host specificato.

```json
{
  "data": {
    "id": "PRbdfaffb7bf374b87be50e672f0cf9309",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:52:05.900Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:52:05.900Z",
      "platform": "web",
      "development": false,
      "token": "47d65c7c98db",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments",
      "extensions": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions",
      "rules": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules",
      "self": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309"
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
