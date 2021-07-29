---
title: Endpoint dei pacchetti di estensione
description: Scopri come effettuare chiamate all’endpoint /extension_packages nell’API Reactor.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 6%

---

# Endpoint dei pacchetti di estensione

>[!WARNING]
>
>L’implementazione dell’endpoint `/extension_packages` è in continuo cambiamento in seguito all’aggiunta, alla rimozione e alla rielaborazione delle funzioni.

Un pacchetto di estensione rappresenta un [estensione](./extensions.md) creato da uno sviluppatore di estensioni. Un pacchetto di estensione definisce funzionalità aggiuntive che possono essere rese disponibili agli utenti di tag. Nella maggior parte dei casi queste funzionalità si presentano sotto forma di [componenti regola](./rule-components.md) (eventi, condizioni e azioni) e di [elementi dati](./data-elements.md), ma possono anche includere moduli principali e moduli condivisi.

I pacchetti di estensione vengono visualizzati nel catalogo delle estensioni nell’interfaccia utente di raccolta dati per consentire agli utenti di eseguire l’installazione. L&#39;aggiunta di un pacchetto di estensione a una proprietà viene eseguita creando un&#39;estensione con un collegamento al pacchetto di estensione.

Un pacchetto di estensione appartiene alla [azienda](./companies.md) dello sviluppatore che lo ha creato.

## Introduzione

L&#39;endpoint utilizzato in questa guida fa parte dell&#39; [API del reattore](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Prima di continuare, controlla la [guida introduttiva](../getting-started.md) per informazioni importanti su come eseguire l&#39;autenticazione nell&#39;API.

## Recupera un elenco di pacchetti di estensione {#list}

Puoi recuperare un elenco di pacchetti di estensione effettuando una richiesta GET a `/extension_packages`.

**Formato API**

```http
GET /extension_packages
```

>[!NOTE]
>
>Utilizzando i parametri di query, i pacchetti di estensione elencati possono essere filtrati in base ai seguenti attributi:<ul><li>`archive`</li><li>`created_at`</li><li>`name`</li><li>`stage`</li><li>`token`</li><li>`updated_at`</li></ul>Per ulteriori informazioni, consulta la guida sulle [risposte relative al filtro](../guides/filtering.md) .

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

Una risposta corretta restituisce un elenco di pacchetti di estensione.

```json
{
  "data": [
    {
      "id": "EP6860e2485de2413ea9b295d6f5321ad3",
      "type": "extension_packages",
      "attributes": {
        "actions": [

        ],
        "author": {
          "url": "http://adobe.com",
          "name": "Adobe Systems",
          "email": "reactor@adobe.com"
        },
        "availability": "development",
        "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP6860e2485de2413ea9b295d6f5321ad3",
        "conditions": [

        ],
        "configuration": null,
        "created_at": "2020-11-09T17:58:32.694Z",
        "data_elements": [

        ],
        "description": "Provides nothing.",
        "discontinued": false,
        "display_name": "Kessel Template Test",
        "events": [

        ],
        "exchange_url": null,
        "hosted_lib_files": null,
        "icon_path": "resources/icons/core.svg",
        "main": null,
        "name": "test-1604944710",
        "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
        "resources": null,
        "shared_modules": null,
        "status": "succeeded",
        "platform": "web",
        "updated_at": "2020-11-09T17:58:35.754Z",
        "version": "1.0.0",
        "view_base_path": "dist/"
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_packages/EP6860e2485de2413ea9b295d6f5321ad3"
      }
    },
    {
      "id": "EP1b173c8316954e0986e5a405b4e715e3",
      "type": "extension_packages",
      "attributes": {
        "actions": [

        ],
        "author": {
          "url": "http://adobe.com",
          "name": "Adobe Systems",
          "email": "reactor@adobe.com"
        },
        "availability": "development",
        "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP1b173c8316954e0986e5a405b4e715e3",
        "conditions": [

        ],
        "configuration": null,
        "created_at": "2020-11-09T17:58:34.632Z",
        "data_elements": [

        ],
        "description": "Provides nothing.",
        "discontinued": false,
        "display_name": "Kessel Template Test",
        "events": [

        ],
        "exchange_url": null,
        "hosted_lib_files": null,
        "icon_path": "resources/icons/core.svg",
        "main": null,
        "name": "test-1604944712",
        "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
        "resources": null,
        "shared_modules": null,
        "status": "succeeded",
        "platform": "web",
        "updated_at": "2020-11-09T17:58:36.655Z",
        "version": "1.0.0",
        "view_base_path": "dist/"
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_packages/EP1b173c8316954e0986e5a405b4e715e3"
      }
    },
    {
      "id": "EPb8eca81769a64af3892af5202a57ce15",
      "type": "extension_packages",
      "attributes": {
        "actions": [

        ],
        "author": {
          "url": "http://adobe.com",
          "name": "Adobe Systems",
          "email": "reactor@adobe.com"
        },
        "availability": "development",
        "cdn_path": "https://assets.adobedtm.com/staging/extensions/EPb8eca81769a64af3892af5202a57ce15",
        "conditions": [

        ],
        "configuration": null,
        "created_at": "2020-11-09T18:32:29.271Z",
        "data_elements": [

        ],
        "description": "Provides nothing.",
        "discontinued": false,
        "display_name": "Kessel Template Test",
        "events": [

        ],
        "exchange_url": null,
        "hosted_lib_files": null,
        "icon_path": "resources/icons/core.svg",
        "main": null,
        "name": "test-1604946740",
        "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
        "resources": null,
        "shared_modules": null,
        "status": "succeeded",
        "platform": "web",
        "updated_at": "2020-11-09T18:32:43.710Z",
        "version": "1.0.0",
        "view_base_path": "dist/"
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_packages/EPb8eca81769a64af3892af5202a57ce15"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 3
    }
  }
}
```

## Cerca un pacchetto di estensione {#lookup}

Puoi cercare un pacchetto di estensione fornendo il relativo ID nel percorso di una richiesta GET.

**Formato API**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | Il `id` del pacchetto di estensione che desideri cercare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

Una risposta corretta restituisce i dettagli del pacchetto di estensione, incluse le relative risorse delegate come `actions`, `conditions`, `data_elements` e altro ancora. La risposta di esempio seguente è stata troncata per lo spazio.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Crea o aggiorna un pacchetto di estensione {#create}

I pacchetti di estensione vengono creati utilizzando uno strumento di scaffolding Node.js e salvati sul computer locale prima di essere inviati all’API Reactor. Per ulteriori informazioni sulla configurazione di un pacchetto di estensione, consulta la guida [guida introduttiva allo sviluppo di estensioni](../../extension-dev/getting-started.md).

Dopo aver creato il file del pacchetto di estensione, puoi inviarlo all’API di Reactor tramite una richiesta di POST. Se il pacchetto di estensione esiste già nell&#39;API, questa chiamata aggiorna il pacchetto a una nuova versione.

**Formato API**

```http
POST /extension_packages
```

**Richiesta**

La seguente richiesta crea un nuovo pacchetto di estensione. Il percorso locale del file del pacchetto che viene caricato è indicato come dati del modulo (`package`) e pertanto questo endpoint richiede un&#39;intestazione `Content-Type` di `multipart/form-data`.

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: multipart/form-data' \
  -F 'package=@"/Users/temp/extension-package.zip"'
```

**Risposta**

Una risposta corretta restituisce i dettagli del pacchetto di estensione appena creato.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Aggiornare un pacchetto di estensione {#update}

Puoi aggiornare un pacchetto di estensione includendo il relativo ID nel percorso di una richiesta POST.

**Formato API**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | Il `id` del pacchetto di estensione che desideri aggiornare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

Come con [creazione di un pacchetto di estensione](#create), è necessario caricare tramite i dati del modulo una versione locale del pacchetto aggiornato.

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: multipart/form-data' \
  -F 'package=@"/Users/temp/extension-package.zip"'
```

**Risposta**

Una risposta corretta restituisce i dettagli del pacchetto di estensione aggiornato.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Rilasciare in privato un pacchetto di estensione {#private-release}

Una volta completato il test del pacchetto di estensione, puoi rilasciarlo privatamente. Questo lo rende disponibile a qualsiasi proprietà all’interno della tua azienda.

Dopo aver rilasciato privatamente, puoi iniziare il processo di rilascio pubblico compilando il [modulo di richiesta di rilascio pubblico](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=7DRB5U).

**Formato API**

```http
PATCH /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | Il `id` del pacchetto di estensione che desideri rilasciare privatamente. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

Una versione privata viene ottenuta fornendo un `action` con un valore di `release_private` nel `meta` dei dati della richiesta.

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "meta": {
            "action": "release_private"
          },
          "id": "EP27e9323eb585411fae6086fc78a3b70b",
          "type": "extension_packages"
        }
      }'
```

**Risposta**

Una risposta corretta restituisce i dettagli del pacchetto di estensione.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Interrompere un pacchetto di estensione {#discontinue}

Puoi interrompere un pacchetto di estensione impostando il relativo attributo `discontinued` su `true` tramite una richiesta PATCH.

**Formato API**

```http
PATCH /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | Il `id` del pacchetto di estensione che desideri interrompere. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

Una versione privata viene ottenuta fornendo un `action` con un valore di `release_private` nel `meta` dei dati della richiesta.

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "discontinued": true
          },
          "id": "EP5705a5d99aba406692e0ac666fcab160",
          "type": "extension_packages"
        }
      }'
```

**Risposta**

Una risposta corretta restituisce i dettagli del pacchetto di estensione.

```json
{
  "data": {
    "id": "EP5705a5d99aba406692e0ac666fcab160",
    "type": "extension_packages",
    "attributes": {
      "actions": [

      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP5705a5d99aba406692e0ac666fcab160",
      "conditions": [

      ],
      "configuration": null,
      "created_at": "2020-12-14T17:39:36.932Z",
      "data_elements": [

      ],
      "description": "Provides nothing.",
      "discontinued": true,
      "display_name": "Kessel Template Test",
      "events": [

      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "test-1607967575",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-12-14T17:39:43.883Z",
      "version": "1.0.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP5705a5d99aba406692e0ac666fcab160"
    }
  }
}
```

## Elencare le versioni di un pacchetto di estensione

Puoi elencare le versioni di un pacchetto di estensione aggiungendo `/versions` al percorso di una richiesta di ricerca.

**Formato API**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}/versions
```

| Parametro | Descrizione |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | Il `id` del pacchetto di estensione di cui desideri elencare le versioni. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172/versions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

Una risposta corretta restituisce un array delle versioni precedenti del pacchetto di estensione. Una risposta di esempio è stata omessa per lo spazio.
