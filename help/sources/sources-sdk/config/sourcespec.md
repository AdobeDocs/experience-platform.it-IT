---
keywords: Experience Platform;home;argomenti popolari;sorgenti;connettori;connettori sorgente;origini sdk;sdk;SDK
title: Configurare le specifiche di origine per le origini self-service (SDK batch)
topic-legacy: overview
description: Questo documento fornisce una panoramica delle configurazioni da preparare per utilizzare Origini self-service (SDK batch).
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '1690'
ht-degree: 1%

---

# Configurare le specifiche di origine per le origini self-service (SDK batch)

Le specifiche di origine contengono informazioni specifiche per un&#39;origine, inclusi gli attributi relativi alla categoria, allo stato beta e all&#39;icona del catalogo di un&#39;origine. Contengono inoltre utili informazioni quali parametri URL, contenuto, intestazione e pianificazione. Le specifiche di origine descrivono anche lo schema dei parametri necessari per creare una connessione di origine da una connessione di base. Lo schema è necessario per creare una connessione di origine.

Consulta la sezione [appendice](#source-spec) per un esempio di specifica di origine compilata completamente.


```json
"sourceSpec": {
  "attributes": {
    "uiAttributes": {
      "isSource": true,
      "isPreview": true,
      "isBeta": true,
      "category": {
        "key": "protocols"
      },
      "icon": {
        "key": "genericRestIcon"
      },
      "description": {
        "key": "genericRestDescription"
      },
      "label": {
        "key": "genericRestLabel"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Defines static and user input parameters to fetch resource values.",
      "properties": {
        "urlParams": {
          "type": "object",
          "properties": {
            "host": {
              "type": "string",
              "description": "Enter resource url host path."
            },
            "path": {
              "type": "string",
              "description": "Enter resource path",
              "example": "/3.0/reports/campaignId/email-activity"
            },
            "method": {
              "type": "string",
              "description": "HTTP method type.",
              "enum": [
                "GET",
                "POST"
              ]
            },
            "queryParams": {
              "type": "object",
              "description": "The query parameters in json format",
            }
          },
          "required": [
            "path",
            "method"
          ]
        },
        "headerParams": {
          "type": "object",
          "description": "The header parameters in json format",
        },
        "contentPath": {
          "type": "object",
          "description": "The parameters required for main collection content.",
          "properties": {
            "path": {
              "description": "The path to the main content.",
              "type": "string",
              "example": "$.emails"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the root content path node.",
              "example": "email"
            }
          },
          "required": [
            "path"
          ]
        },
        "explodeEntityPath": {
          "type": "object",
          "description": "The parameters required for the sub-array content.",
          "properties": {
            "path": {
              "description": "The path to the sub-array content.",
              "type": "string",
              "example": "$.email.activity"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the  root content path node.",
              "example": "activity"
            }
          },
          "required": [
            "path"
          ]
        },
        "paginationParams": {
          "type": "object",
          "description": "The parameters required to fetch data using pagination.",
          "properties": {
            "type": {
              "description": "The pagination fetch type.",
              "type": "string",
              "enum": [
                "OFFSET",
                "POINTER"
              ]
            },
            "limitName": {
              "type": "string",
              "description": "The limit property name",
              "example": "limit or count"
            },
            "limitValue": {
              "type": "integer",
              "description": "The number of records to fetch per page.",
              "example": "limit=10 or count=10"
            },
            "offsetName": {
              "type": "string",
              "description": "The offset property name",
              "example": "offset"
            },
            "pointerPath": {
              "type": "string",
              "description": "The path to pointer property",
              "example": "$.paging.next"
            }
          },
          "required": [
            "type",
            "limitName",
            "limitValue"
          ]
        },
        "scheduleParams": {
          "type": "object",
          "description": "The parameters required to fetch data for batch schedule.",
          "properties": {
            "scheduleStartParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleEndParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleStartParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            },
            "scheduleEndParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            }
          },
          "required": [
            "scheduleStartParamName",
            "scheduleEndParamName"
          ]
        }
      },
      "required": [
        "urlParams",
        "contentPath",
        "paginationParams",
        "scheduleParams"
      ]
    }
  },
}
```

| Proprietà | Descrizione | Esempio |
| --- | --- | --- |
| `sourceSpec.attributes` | Contiene informazioni sull’origine specifica dell’interfaccia utente o dell’API. |
| `sourceSpec.attributes.uiAttributes` | Visualizza informazioni sull’origine specifica dell’interfaccia utente. |
| `sourceSpec.attributes.uiAttributes.isBeta` | Attributo booleano che indica se la sorgente richiede più feedback dai clienti per aggiungerla alla sua funzionalità. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Definisce la categoria dell&#39;origine. | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Definisce l’icona utilizzata per il rendering dell’origine nell’interfaccia utente di Platform. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Visualizza una breve descrizione dell’origine. |
| `sourceSpec.attributes.uiAttributes.label` | Visualizza l’etichetta da utilizzare per il rendering dell’origine nell’interfaccia utente di Platform. |
| `sourceSpec.attributes.spec.properties.urlParams` | Contiene informazioni sul percorso della risorsa URL, sul metodo e sui parametri di query supportati. |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | Definisce il percorso della risorsa da cui recuperare i dati. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | Definisce il metodo HTTP da utilizzare per effettuare la richiesta alla risorsa di recuperare i dati. | `GET`, `POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | Definisce i parametri di query supportati che possono essere utilizzati per aggiungere l’URL di origine quando si effettua una richiesta di recupero dati. **Nota**: Qualsiasi valore di parametro fornito dall&#39;utente deve essere formattato come segnaposto. Ad esempio: `${USER_PARAMETER}`. | `"queryParams" : {"key" : "value", "key1" : "value1"}` verrà aggiunto all’URL sorgente come: `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | Definisce le intestazioni che devono essere fornite nella richiesta HTTP all’URL di origine durante il recupero dei dati. | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.bodyParams` | Questo attributo può essere configurato per inviare il corpo HTTP tramite una richiesta POST. |
| `sourceSpec.attributes.spec.properties.contentPath` | Definisce il nodo che contiene l’elenco degli elementi necessari per l’acquisizione in Platform. Questo attributo deve seguire una sintassi di percorso JSON valida e puntare a un particolare array. | Visualizza la [sezione risorse aggiuntive](#content-path) per un esempio della risorsa contenuta in un percorso di contenuto. |
| `sourceSpec.attributes.spec.properties.contentPath.path` | Percorso che punta ai record di raccolta da acquisire in Platform. | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | Questa proprietà ti consente di identificare elementi specifici della risorsa identificata nel percorso del contenuto che devono essere esclusi dall’acquisizione. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | Questa proprietà consente di specificare in modo esplicito i singoli attributi che si desidera mantenere. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | Questa proprietà consente di ignorare il valore del nome dell&#39;attributo specificato in `contentPath`. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | Questa proprietà consente di appiattire due array e trasformare i dati delle risorse in una risorsa Platform. |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | Percorso che punta ai record della raccolta che desideri appiattire. | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | Questa proprietà ti consente di identificare elementi specifici della risorsa identificata nel percorso dell’entità che devono essere esclusi dall’acquisizione. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | Questa proprietà consente di specificare in modo esplicito i singoli attributi che si desidera mantenere. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | Questa proprietà consente di ignorare il valore del nome dell&#39;attributo specificato in `explodeEntityPath`. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | Definisce i parametri o i campi che devono essere forniti per ottenere un collegamento alla pagina successiva dalla risposta della pagina corrente dell&#39;utente o durante la creazione di un URL della pagina successiva. |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | Visualizza il tipo di impaginazione supportato per l’origine. | <ul><li>`OFFSET`: Questo tipo di impaginazione consente di analizzare i risultati specificando un indice dal punto in cui avviare la matrice risultante e un limite al numero di risultati restituiti.</li><li>`POINTER`: Questo tipo di impaginazione consente di utilizzare un `pointer` per puntare a un particolare elemento che deve essere inviato con una richiesta. L&#39;impaginazione del tipo di puntatore richiede il percorso nel payload che punta alla pagina successiva.</li><li>`CONTINUATION_TOKEN`: Questo tipo di impaginazione ti consente di aggiungere i parametri di query o intestazione con un token di continuazione per recuperare i dati di ritorno rimanenti dall’origine, che non sono stati restituiti inizialmente a causa di un valore massimo predeterminato.</li><li>`PAGE`: Questo tipo di impaginazione ti consente di aggiungere il parametro di query con un parametro di paging per scorrere i dati restituiti in base alle pagine, a partire dalla pagina zero.</li><li>`NONE`: Questo tipo di impaginazione può essere utilizzato per le origini che non supportano nessuno dei tipi di impaginazione disponibili. Tipo di impaginazione `NONE` restituisce l&#39;intero dato di risposta dopo una richiesta.</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | Nome del limite attraverso il quale l’API può specificare il numero di record da recuperare in una pagina. | `limit` oppure `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | Il numero di record da recuperare in una pagina. | `limit=10` oppure `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | Nome dell&#39;attributo di offset. Questa opzione è necessaria se il tipo di impaginazione è impostato su `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | Nome dell&#39;attributo del puntatore. Questo richiede il percorso json dell’attributo che indicherà la pagina successiva. Questa opzione è necessaria se il tipo di impaginazione è impostato su `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | Contiene parametri che definiscono i formati di pianificazione supportati per la sorgente. I parametri di pianificazione includono `startTime` e `endTime`, che consente di impostare intervalli di tempo specifici per le esecuzioni batch, in modo che i record recuperati in una precedente esecuzione batch non vengano recuperati di nuovo. |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | Definisce il nome del parametro dell&#39;ora di inizio | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | Definisce il nome del parametro del tempo di fine | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | Definisce il formato supportato per il `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | Definisce il formato supportato per il `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Definisce i parametri forniti dall’utente per recuperare i valori delle risorse. | Consulta la sezione [risorse aggiuntive](#user-input) per un esempio di parametri immessi dall’utente per `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## Risorse aggiuntive {#appendix}

Le sezioni seguenti forniscono informazioni sulle configurazioni aggiuntive che puoi effettuare per il tuo `sourceSpec`, inclusi schemi di programmazione avanzati e schemi personalizzati.

### Esempio di percorso del contenuto {#content-path}

Di seguito è riportato un esempio del contenuto del `contentPath` in una proprietà [!DNL MailChimp Members] specifica di connessione.

```json
"contentPath": {
  "path": "$.members",
  "skipAttributes": [
    "_links",
    "total_items",
    "list_id"
  ],
  "overrideWrapperAttribute": "member"
}
```

### `spec.properties` esempio di input dell&#39;utente {#user-input}

Esempio di un `spec.properties` utilizzando [!DNL MailChimp Members] specifica di connessione.

In questo esempio, `listId` è fornito come parte `urlParams.path`. Se hai bisogno di recuperare `listId` da un cliente, devi anche definirlo come parte di `spec.properties`.


```json
"urlParams": {
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      }
"spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
```

### Esempio di specifica origine {#source-spec}

Di seguito è riportata una specifica di origine completata utilizzando [!DNL MailChimp Members]:

```json
  "sourceSpec": {
    "attributes": {
      "uiAttributes": {
        "isSource": true,
        "isPreview": true,
        "isBeta": true,
        "category": {
          "key": "marketingAutomation"
        },
        "icon": {
          "key": "mailchimpMembersIcon"
        },
        "description": {
          "key": "mailchimpMembersDescription"
        },
        "label": {
          "key": "mailchimpMembersLabel"
        }
      },
      "urlParams": {
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      },
      "contentPath": {
        "path": "$.members",
        "skipAttributes": [
          "_links",
          "total_items",
          "list_id"
        ],
        "overrideWrapperAttribute": "member"
      },
      "paginationParams": {
        "type": "OFFSET",
        "limitName": "count",
        "limitValue": "100",
        "offSetName": "offset"
      },
      "scheduleParams": {
        "scheduleStartParamName": "since_last_changed",
        "scheduleEndParamName": "before_last_changed",
        "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
        "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
  }
```

### Configurare diversi tipi di impaginazione per l&#39;origine {#pagination}

Di seguito sono riportati alcuni esempi di altri tipi di impaginazione supportati da Origini self-service (SDK batch):

#### `CONTINUATION_TOKEN`

Un tipo di token di continuazione dell&#39;impaginazione restituisce un token stringa che indica l&#39;esistenza di più elementi che non è stato possibile restituire, a causa di un numero massimo predefinito di elementi che possono essere restituiti in un&#39;unica risposta.

Un&#39;origine che supporta il tipo di token di continuazione dell&#39;impaginazione può avere un parametro di impaginazione simile a:

```json
"paginationParams": {
  "type": "CONTINUATION_TOKEN",
  "continuationTokenPath": "$.meta.after_cursor",
  "parameterType": "QUERYPARAM",
  "parameterName": "page[after]",
  "delayRequestMillis": "850"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `type` | Tipo di impaginazione utilizzato per restituire i dati. |
| `continuationTokenPath` | Il valore che deve essere aggiunto ai parametri di query per passare alla pagina successiva dei risultati restituiti. |
| `parameterType` | La `parameterType` definisce dove `parameterName` devono essere aggiunti. La `QUERYPARAM` type ti consente di aggiungere la query con `parameterName`. La `HEADERPARAM` consente di aggiungere `parameterName` alla richiesta di intestazione. |
| `parameterName` | Nome del parametro utilizzato per incorporare il token di continuazione. Il formato è il seguente: `{PARAMETER_NAME}={CONTINUATION_TOKEN}`. |
| `delayRequestMillis` | La `delayRequestMillis` in impaginazione consente di controllare il tasso di richieste effettuate all&#39;origine. Alcune sorgenti possono avere un limite al numero di richieste che puoi fare al minuto. Ad esempio: [!DNL Zendesk] ha un limite di 100 richieste al minuto e definisce  `delayRequestMillis` a `850` consente di configurare l’origine per effettuare chiamate a circa 80 richieste al minuto, molto al di sotto della soglia di 100 richieste al minuto. |

Di seguito è riportato un esempio di risposta restituita utilizzando il tipo di token di continuazione dell’impaginazione:

```json
{
  "results": [
    {
      "id": 5624716025745,
      "url": "https://dev.zendesk.com/api/v2/users/5624716025745.json",
      "name": "newinctest@zenaep.com",
      "email": "newinctest@zenaep.com",
      "created_at": "2022-04-22T10:27:30Z",
      
    }
  ],
  "facets": null,
  "meta": {
    "has_more": false,
    "after_cursor": "eyJmaWVsZCI6ImNyZWF0ZWRfYXQiLCJk",
    "before_cursor": null
  },
  "links": {
    "prev": null,
    "next": "https://dev.zendesk.com/api/v2/search/export.json?filter%5Btype%5D=user&page%5Bafter%5D=eyJmaWVsZCI6"
  }
}
```

#### `PAGE`

La `PAGE` il tipo di impaginazione consente di scorrere i dati restituiti in base al numero di pagine che iniziano da zero. Quando utilizzi `PAGE` digitare impaginazione, è necessario specificare il numero di record forniti in una singola pagina.

```json
"paginationParams": {
  "type": "PAGE",
  "limitName": "records",
  "limitValue": "100",
  "pageParamName": "pageIndex",
  "maximumRequest": 10000
}
```

| Proprietà | Descrizione |
| --- | --- |
| `type` | Tipo di impaginazione utilizzato per restituire i dati. |
| `limitName` | Nome del limite attraverso il quale l’API può specificare il numero di record da recuperare in una pagina. |
| `limitValue` | Il numero di record da recuperare in una pagina. |
| `pageParamName` | Il nome del parametro che è necessario aggiungere ai parametri di query per attraversare diverse pagine dei dati restituiti. Ad esempio: `https://abc.com?pageIndex=1` restituisce la seconda pagina del payload di ritorno di un’API. |
| `maximumRequest` | Il numero massimo di richieste che un&#39;origine può effettuare per una determinata esecuzione incrementale. Il limite predefinito corrente è 10000. |

#### `NONE`

La `NONE` il tipo di impaginazione può essere utilizzato per le origini che non supportano nessuno dei tipi di impaginazione disponibili. Origini che utilizzano il tipo di impaginazione di `NONE` è sufficiente restituire tutti i record recuperabili quando viene effettuata una richiesta GET.

```json
"paginationParams": {
  "type": "NONE"
}
```

### Pianificazione avanzata per le origini self-service (SDK batch)

Configura la pianificazione incrementale e di backfill della tua sorgente utilizzando la pianificazione avanzata. La `incremental` consente di configurare una pianificazione in cui l&#39;origine acquisirà solo record nuovi o modificati, mentre il `backfill` consente di creare una pianificazione per l&#39;acquisizione di dati storici.

Con la programmazione avanzata, puoi utilizzare espressioni e funzioni specifiche della tua origine per configurare pianificazioni incrementali e di backfill. Nell’esempio seguente, la [!DNL Zendesk] l&#39;origine richiede che la pianificazione incrementale sia formattata come `type:user updated > {START_TIME} updated < {END_TIME}` e la retrocompilazione come `type:user updated < {END_TIME}`.

```json
"scheduleParams": {
        "type": "ADVANCE",
        "paramFormat": "yyyy-MM-ddTHH:mm:ssK",
        "incremental": "type:user updated > {START_TIME} updated < {END_TIME}",
        "backfill": "type:user updated < {END_TIME}"
      }
```

| Proprietà | Descrizione |
| --- | --- |
| `scheduleParams.type` | Tipo di pianificazione che verrà utilizzato dalla sorgente. Imposta questo valore su `ADVANCE` per utilizzare il tipo di programmazione avanzata. |
| `scheduleParams.paramFormat` | Il formato definito del parametro di pianificazione. Questo valore può essere lo stesso dell&#39;origine `scheduleStartParamFormat` e `scheduleEndParamFormat` valori. |
| `scheduleParams.incremental` | Query incrementale dell&#39;origine. Incremental si riferisce a un metodo di acquisizione in cui vengono acquisiti solo dati nuovi o modificati. |
| `scheduleParams.backfill` | Query di backfill dell’origine. Il backfill si riferisce a un metodo di acquisizione in cui vengono acquisiti dati storici. |

Una volta configurata la pianificazione avanzata, devi quindi fare riferimento alla `scheduleParams` nella sezione URL, body o header params , a seconda di ciò che la tua sorgente supporta. Nell’esempio seguente: `{SCHEDULE_QUERY}` è un segnaposto utilizzato per specificare dove verranno utilizzate le espressioni di programmazione incrementale e di backfill. Nel caso di un [!DNL Zendesk] sorgente, `query` viene utilizzato nella `queryParams` per specificare la pianificazione avanzata.

```json
"urlParams": {
        "path": "/api/v2/search/export@{if(empty(coalesce(pipeline()?.parameters?.ingestionStart,'')),'?query=type:user&filter[type]=user&','')}",
        "method": "GET",
        "queryParams": {
          "query": "{SCHEDULE_QUERY}",
          "filter[type]": "user"
        }
      }
```

### Aggiungi uno schema personalizzato per definire gli attributi dinamici della sorgente

È possibile includere uno schema personalizzato nel `sourceSpec` per definire tutti gli attributi richiesti per l’origine, compresi eventuali attributi dinamici necessari. È possibile aggiornare la specifica di connessione corrispondente della sorgente effettuando una richiesta di PUT al `/connectionSpecs` punto finale [!DNL Flow Service] , fornendo al contempo lo schema personalizzato nel `sourceSpec` sezione delle specifiche di connessione.

Di seguito è riportato un esempio di schema personalizzato che è possibile aggiungere alle specifiche di connessione della propria origine:

```json
      "schema": {
        "type": "object",
        "properties": {
          "results": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "organization_id": {
                  "type": "integer",
                  "minimum": -9007199254740992,
                  "maximum": 9007199254740991
                }
                "active": {
                  "type": "boolean"
                },
                "created_at": {
                  "type": "string"
                },
                "email": {
                  "type": "string"
                },
                "iana_time_zone": {
                  "type": "string"
                },
                "id": {
                  "type": "integer"
                },
                "locale": {
                  "type": "string"
                },
                "locale_id": {
                  "type": "integer"
                },
                "moderator": {
                  "type": "boolean"
                },
                "name": {
                  "type": "string"
                },
                "only_private_comments": {
                  "type": "boolean"
                },
                "report_csv": {
                  "type": "boolean"
                },
                "restricted_agent": {
                  "type": "boolean"
                },
                "result_type": {
                  "type": "string"
                },
                "role": {
                  "type": "integer"
                },
                "shared": {
                  "type": "boolean"
                },
                "shared_agent": {
                  "type": "boolean"
                },
                "suspended": {
                  "type": "boolean"
                },
                "ticket_restriction": {
                  "type": "string"
                },
                "time_zone": {
                  "type": "string"
                },
                "two_factor_auth_enabled": {
                  "type": "boolean"
                },
                "updated_at": {
                  "type": "string"
                },
                "url": {
                  "type": "string"
                },
                "verified": {
                  "type": "boolean"
                },
                "tags": {
                  "type": "array",
                  "items": {
                    "type": "string"
                  }
                }
              }
            }
          }
        }
      }
```


## Passaggi successivi

Con le specifiche di origine compilate, puoi procedere alla configurazione delle specifiche di esplorazione per la sorgente che desideri integrare in Platform. Visualizza il documento su [configurazione delle specifiche](./explorespec.md) per ulteriori informazioni.
