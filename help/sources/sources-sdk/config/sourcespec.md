---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;sorgente connettori;sorgenti sdk;sdk;SDK
title: Configurare le specifiche di origine per le origini self-service (SDK batch)
description: Questo documento fornisce una panoramica delle configurazioni da preparare per utilizzare Self-Service Sources (SDK batch).
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: b1173adb0e0c3a6460b2cb15cba9218ddad7abcb
workflow-type: tm+mt
source-wordcount: '1847'
ht-degree: 0%

---

# Configurare le specifiche di origine per le origini self-service (SDK batch)

Le specifiche dell&#39;origine contengono informazioni specifiche per un&#39;origine, inclusi gli attributi relativi alla categoria, allo stato beta e all&#39;icona del catalogo di un&#39;origine. Contengono anche informazioni utili come parametri URL, contenuto, intestazione e pianificazione. Le specifiche di origine descrivono anche lo schema dei parametri necessari per creare una connessione di origine da una connessione di base. Lo schema è necessario per creare una connessione di origine.

Consulta la [appendice](#source-spec) ad esempio una specifica di origine completamente popolata.


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
              "description": "Enter resource url host path.",
              "example": "https://{domain}.api.mailchimp.com"
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
            "host",
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
| `sourceSpec.attributes` | Contiene informazioni sull’origine specifiche per l’interfaccia utente o l’API. |
| `sourceSpec.attributes.uiAttributes` | Visualizza informazioni sull&#39;origine specifica dell&#39;interfaccia utente. |
| `sourceSpec.attributes.uiAttributes.isBeta` | Attributo booleano che indica se l’origine richiede più feedback dai clienti per aggiungere alle sue funzionalità. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Definisce la categoria dell’origine. | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Definisce l’icona utilizzata per il rendering dell’origine nell’interfaccia utente di Platform. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Visualizza una breve descrizione dell&#39;origine. |
| `sourceSpec.attributes.uiAttributes.label` | Visualizza l’etichetta da utilizzare per il rendering dell’origine nell’interfaccia utente di Platform. |
| `sourceSpec.attributes.spec.properties.urlParams` | Contiene informazioni sul percorso della risorsa URL, sul metodo e sui parametri di query supportati. |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | Definisce il percorso della risorsa da cui recuperare i dati. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | Definisce il metodo HTTP da utilizzare per effettuare la richiesta alla risorsa di recupero dei dati. | `GET`, `POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | Definisce i parametri di query supportati che possono essere utilizzati per aggiungere l’URL di origine quando si effettua una richiesta di recupero dei dati. **Nota**: qualsiasi valore di parametro fornito dall’utente deve essere formattato come segnaposto. Ad esempio: `${USER_PARAMETER}`. | `"queryParams" : {"key" : "value", "key1" : "value1"}` verrà aggiunto all’URL di origine come: `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | Definisce le intestazioni che devono essere fornite nella richiesta HTTP all’URL di origine durante il recupero dei dati. | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.bodyParams` | Questo attributo può essere configurato per inviare il corpo HTTP tramite una richiesta POST. |
| `sourceSpec.attributes.spec.properties.contentPath` | Definisce il nodo che contiene l’elenco degli elementi da acquisire in Platform. Questo attributo deve seguire una sintassi di percorso JSON valida e deve puntare a un array specifico. | Visualizza [sezione risorse aggiuntive](#content-path) per un esempio della risorsa contenuta in un percorso di contenuto. |
| `sourceSpec.attributes.spec.properties.contentPath.path` | Percorso che punta ai record della raccolta da acquisire in Platform. | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | Questa proprietà ti consente di identificare elementi specifici dalla risorsa identificata nel percorso del contenuto che devono essere esclusi dall’acquisizione. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | Questa proprietà consente di specificare in modo esplicito i singoli attributi che si desidera mantenere. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | Questa proprietà consente di ignorare il valore del nome attributo specificato in `contentPath`. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | Questa proprietà consente di &quot;appiattire&quot; due array e trasformare i dati delle risorse in risorse Platform. |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | Percorso che punta ai record della raccolta che si desidera appiattire. | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | Questa proprietà ti consente di identificare elementi specifici dalla risorsa identificata nel percorso dell’entità che devono essere esclusi dall’acquisizione. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | Questa proprietà consente di specificare in modo esplicito i singoli attributi che si desidera mantenere. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | Questa proprietà consente di ignorare il valore del nome attributo specificato in `explodeEntityPath`. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | Definisce i parametri o i campi da fornire per ottenere un collegamento alla pagina successiva dalla risposta della pagina corrente dell&#39;utente o durante la creazione di un URL della pagina successiva. |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | Visualizza il tipo di impaginazione supportato per l&#39;origine. | <ul><li>`OFFSET`: questo tipo di impaginazione ti consente di analizzare i risultati specificando un indice da cui avviare la matrice risultante e un limite sul numero di risultati restituiti.</li><li>`POINTER`: questo tipo di impaginazione ti consente di utilizzare una `pointer` variabile per puntare a un particolare elemento che deve essere inviato con una richiesta. L&#39;impaginazione del tipo di puntatore richiede il percorso nel payload che punta alla pagina successiva.</li><li>`CONTINUATION_TOKEN`: questo tipo di impaginazione ti consente di aggiungere alla query o ai parametri di intestazione un token di continuazione per recuperare i dati restituiti rimanenti dall’origine che non sono stati inizialmente restituiti a causa di un massimo predeterminato.</li><li>`PAGE`: questo tipo di impaginazione ti consente di aggiungere al parametro di query un parametro di paging per scorrere i dati restituiti per pagina, a partire dalla pagina zero.</li><li>`NONE`: questo tipo di impaginazione può essere utilizzato per origini che non supportano nessuno dei tipi di impaginazione disponibili. Tipo di impaginazione `NONE` restituisce tutti i dati di risposta dopo una richiesta.</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | Il nome del limite attraverso il quale l’API può specificare il numero di record da recuperare in una pagina. | `limit` o `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | Il numero di record da recuperare in una pagina. | `limit=10` o `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | Nome dell&#39;attributo di offset. Questa opzione è necessaria se il tipo di paginazione è impostato su `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | Nome dell&#39;attributo del puntatore. Questo richiede il percorso json dell’attributo che punterà alla pagina successiva. Questa opzione è necessaria se il tipo di paginazione è impostato su `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | Contiene parametri che definiscono i formati di pianificazione supportati per l&#39;origine. I parametri di pianificazione includono `startTime` e `endTime`, entrambi che consentono di impostare intervalli di tempo specifici per le esecuzioni batch, in modo da garantire che i record recuperati in una precedente esecuzione batch non vengano recuperati nuovamente. |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | Definisce il nome del parametro dell&#39;ora di inizio | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | Definisce il nome del parametro dell&#39;ora di fine | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | Definisce il formato supportato per `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | Definisce il formato supportato per `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Definisce i parametri forniti dall&#39;utente per recuperare i valori delle risorse. | Consulta la [risorse aggiuntive](#user-input) ad esempio, parametri immessi dall&#39;utente per `spec.properties`. |

{style="table-layout:auto"}

## Risorse aggiuntive {#appendix}

Le sezioni seguenti forniscono informazioni sulle configurazioni aggiuntive che è possibile apportare al `sourceSpec`, inclusi la pianificazione avanzata e gli schemi personalizzati.

### Esempio di percorso del contenuto {#content-path}

Di seguito è riportato un esempio del contenuto di `contentPath` proprietà in una [!DNL MailChimp Members] specifica di connessione.

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

### `spec.properties` esempio di input utente {#user-input}

Di seguito è riportato un esempio di `spec.properties` utilizzando un [!DNL MailChimp Members] specifica di connessione.

In questo esempio, `listId` viene fornito come parte di `urlParams.path`. Se è necessario recuperare `listId` da un cliente, devi anche definirlo come parte di `spec.properties`.


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

### Esempio di specifica di origine {#source-spec}

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
        "host": "https://{domain}.api.mailchimp.com",
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

### Configurare diversi tipi di impaginazione per l’origine {#pagination}

Di seguito sono riportati alcuni esempi di altri tipi di impaginazione supportati da Self-Service Sources (Batch SDK):

#### `CONTINUATION_TOKEN`

Un tipo di impaginazione del token di continuazione restituisce un token stringa che indica l’esistenza di più elementi che non possono essere restituiti, a causa di un numero massimo predeterminato di elementi che possono essere restituiti in una singola risposta.

Un’origine che supporta il tipo di token di continuazione dell’impaginazione può avere un parametro di impaginazione simile a:

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
| `continuationTokenPath` | Il valore che deve essere aggiunto ai parametri della query per passare alla pagina successiva dei risultati restituiti. |
| `parameterType` | Il `parameterType` definisce dove `parameterName` deve essere aggiunto. Il `QUERYPARAM` tipo ti consente di aggiungere la query con il `parameterName`. Il `HEADERPARAM` consente di aggiungere `parameterName` nella richiesta di intestazione. |
| `parameterName` | Nome del parametro utilizzato per incorporare il token di continuazione. Il formato è il seguente: `{PARAMETER_NAME}={CONTINUATION_TOKEN}`. |
| `delayRequestMillis` | Il `delayRequestMillis` nell’impaginazione consente di controllare la frequenza delle richieste effettuate all’origine. Alcune origini possono avere un limite al numero di richieste che è possibile effettuare al minuto. Ad esempio: [!DNL Zendesk] ha un limite di 100 richieste al minuto e definisce  `delayRequestMillis` a `850` consente di configurare l’origine per effettuare chiamate a circa 80 richieste al minuto, ben al di sotto della soglia di 100 richieste al minuto. |

Di seguito è riportato un esempio di risposta restituita utilizzando il tipo di token di continuazione impaginazione:

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

Il `PAGE` tipo di impaginazione consente di scorrere i dati restituiti per numero di pagine a partire da zero. Quando si utilizza `PAGE` tipo di impaginazione, devi fornire il numero di record dato in una singola pagina.

```json
"paginationParams": {
  "type": "PAGE",
  "limitName": "pageSize",
  "limitValue": 100,
  "initialPageIndex": 1,
  "endPageIndex": "headers.x-pagecount",
  "pageParamName": "pageNumber",
  "maximumRequest": 10000
}
```

| Proprietà | Descrizione |
| --- | --- |
| `type` | Tipo di impaginazione utilizzato per restituire i dati. |
| `limitName` | Il nome del limite attraverso il quale l’API può specificare il numero di record da recuperare in una pagina. |
| `limitValue` | Il numero di record da recuperare in una pagina. |
| `initialPageIndex` | (Facoltativo) L’indice della pagina iniziale definisce il numero di pagina da cui inizierà l’impaginazione. Questo campo può essere utilizzato per le origini in cui l’impaginazione non inizia da 0. Se non specificato, l’indice della pagina iniziale sarà 0 per impostazione predefinita. Questo campo richiede un numero intero. |
| `endPageIndex` | (Facoltativo) L’indice della pagina finale ti consente di stabilire una condizione di fine e di interrompere l’impaginazione. Questo campo può essere utilizzato quando le condizioni di fine predefinite per interrompere l’impaginazione non sono disponibili. Questo campo può essere utilizzato anche se il numero di pagine da acquisire o l’ultimo numero di pagina viene fornito tramite l’intestazione di risposta, che è comune quando si utilizza `PAGE` impaginazione di tipo. Il valore per l’indice della pagina finale può essere l’ultimo numero di pagina o un valore di espressione di tipo stringa dall’intestazione di risposta. Ad esempio, puoi utilizzare `headers.x-pagecount` per assegnare l&#39;indice della pagina finale a `x-pagecount` valore dalle intestazioni di risposta. **Nota**: `x-pagecount` è un’intestazione di risposta obbligatoria per alcune origini e contiene il valore numero di pagine da acquisire. |
| `pageParamName` | Il nome del parametro che è necessario accodare ai parametri di query per poter attraversare pagine diverse dei dati restituiti. Ad esempio: `https://abc.com?pageIndex=1` restituisce la seconda pagina del payload di ritorno di un’API. |
| `maximumRequest` | Il numero massimo di richieste che un’origine può effettuare per una determinata esecuzione incrementale. Il limite predefinito corrente è 10000. |

{style="table-layout:auto"}


#### `NONE`

Il `NONE` il tipo di impaginazione può essere utilizzato per origini che non supportano nessuno dei tipi di impaginazione disponibili. Origini che utilizzano il tipo di impaginazione `NONE` è sufficiente restituire tutti i record recuperabili quando viene effettuata una richiesta GET.

```json
"paginationParams": {
  "type": "NONE"
}
```

### Pianificazione avanzata per origini self-service (SDK batch)

Configura la pianificazione incrementale e di backfill dell’origine utilizzando la pianificazione avanzata. Il `incremental` consente di configurare una pianificazione in cui l&#39;origine acquisirà solo record nuovi o modificati, mentre `backfill` consente di creare una pianificazione per acquisire i dati storici.

Con la pianificazione avanzata, puoi utilizzare espressioni e funzioni specifiche della tua origine per configurare pianificazioni incrementali e di backfill. Nell’esempio seguente, il [!DNL Zendesk] origine richiede che la pianificazione incrementale sia formattata come `type:user updated > {START_TIME} updated < {END_TIME}` e backfill come `type:user updated < {END_TIME}`.

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
| `scheduleParams.type` | Tipo di pianificazione che verrà utilizzato dall&#39;origine. Imposta questo valore su `ADVANCE` per utilizzare il tipo di pianificazione avanzata. |
| `scheduleParams.paramFormat` | Il formato definito del parametro di pianificazione. Questo valore può essere lo stesso del `scheduleStartParamFormat` e `scheduleEndParamFormat` valori. |
| `scheduleParams.incremental` | La query incrementale dell’origine. Incrementale si riferisce a un metodo di acquisizione in cui vengono acquisiti solo dati nuovi o modificati. |
| `scheduleParams.backfill` | La query di retrocompilazione dell’origine. Il backfill si riferisce a un metodo di acquisizione in cui vengono acquisiti dati storici. |

Dopo aver configurato la pianificazione avanzata, è necessario fare riferimento a `scheduleParams` nella sezione URL, body o header params (Parametri URL, corpo o intestazione), a seconda di ciò che supporta la tua specifica origine. Nell’esempio seguente, `{SCHEDULE_QUERY}` è un segnaposto utilizzato per specificare dove verranno utilizzate le espressioni di pianificazione incrementale e di retrocompilazione. Nel caso di un [!DNL Zendesk] origine, `query` viene utilizzato in `queryParams` per specificare la programmazione avanzata.

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

### Aggiungi uno schema personalizzato per definire gli attributi dinamici della tua origine

Puoi includere uno schema personalizzato nel tuo `sourceSpec` per definire tutti gli attributi necessari per l&#39;origine, inclusi quelli dinamici. È possibile aggiornare la specifica di connessione corrispondente dell’origine effettuando una richiesta PUT al `/connectionSpecs` endpoint del [!DNL Flow Service] , fornendo al tempo stesso lo schema personalizzato nel `sourceSpec` sezione della specifica di connessione.

Di seguito è riportato un esempio di schema personalizzato che è possibile aggiungere alla specifica di connessione dell&#39;origine:

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

Con le specifiche sorgente compilate, puoi procedere alla configurazione delle specifiche di esplorazione per l’origine che desideri integrare in Platform. Consulta il documento su [configurazione delle specifiche di esplorazione](./explorespec.md) per ulteriori informazioni.
