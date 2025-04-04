---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;source connectors;sources sdk;sdk;SDK
title: Configurare le specifiche di origine per le origini self-service (Batch SDK)
description: Questo documento fornisce una panoramica delle configurazioni da preparare per utilizzare le origini self-service (Batch SDK).
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2090'
ht-degree: 1%

---

# Configurare la specifica di origine per le origini self-service (Batch SDK)

Le specifiche Source contengono informazioni specifiche per un&#39;origine, inclusi gli attributi relativi alla categoria, allo stato beta e all&#39;icona del catalogo di un&#39;origine. Contengono anche informazioni utili come parametri URL, contenuto, intestazione e pianificazione. Le specifiche Source descrivono anche lo schema dei parametri necessari per creare una connessione sorgente da una connessione di base. Lo schema è necessario per creare una connessione di origine.

Per un esempio di specifica di origine completa, vedere l&#39;[appendice](#source-spec).


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
| `sourceSpec.attributes.uiAttributes.icon` | Definisce l’icona utilizzata per il rendering dell’origine nell’interfaccia utente di Experience Platform. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Visualizza una breve descrizione dell&#39;origine. |
| `sourceSpec.attributes.uiAttributes.label` | Visualizza l’etichetta da utilizzare per il rendering dell’origine nell’interfaccia utente di Experience Platform. |
| `sourceSpec.attributes.spec.properties.urlParams` | Contiene informazioni sul percorso della risorsa URL, sul metodo e sui parametri di query supportati. |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | Definisce il percorso della risorsa da cui recuperare i dati. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | Definisce il metodo HTTP da utilizzare per effettuare la richiesta alla risorsa di recupero dei dati. | `GET`, `POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | Definisce i parametri di query supportati che possono essere utilizzati per aggiungere l’URL di origine quando si effettua una richiesta di recupero dei dati. **Nota**: qualsiasi valore di parametro fornito dall&#39;utente deve essere formattato come segnaposto. Esempio: `${USER_PARAMETER}`. | `"queryParams" : {"key" : "value", "key1" : "value1"}` verrà aggiunto all&#39;URL di origine come: `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | Definisce le intestazioni che devono essere fornite nella richiesta HTTP all’URL di origine durante il recupero dei dati. | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.bodyParams` | Questo attributo può essere configurato per inviare il corpo HTTP tramite una richiesta POST. |
| `sourceSpec.attributes.spec.properties.contentPath` | Definisce il nodo che contiene l’elenco degli elementi da acquisire in Experience Platform. Questo attributo deve seguire una sintassi di percorso JSON valida e deve puntare a un array specifico. | Visualizzare la [sezione risorse aggiuntive](#content-path) per un esempio della risorsa contenuta in un percorso di contenuto. |
| `sourceSpec.attributes.spec.properties.contentPath.path` | Percorso che punta ai record della raccolta da acquisire in Experience Platform. | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | Questa proprietà ti consente di identificare elementi specifici dalla risorsa identificata nel percorso del contenuto che devono essere esclusi dall’acquisizione. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | Questa proprietà consente di specificare in modo esplicito i singoli attributi che si desidera mantenere. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | Questa proprietà consente di ignorare il valore del nome dell&#39;attributo specificato in `contentPath`. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | Questa proprietà consente di &quot;appiattire&quot; due array e trasformare i dati delle risorse in risorse Experience Platform. |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | Percorso che punta ai record della raccolta che si desidera appiattire. | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | Questa proprietà ti consente di identificare elementi specifici dalla risorsa identificata nel percorso dell’entità che devono essere esclusi dall’acquisizione. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | Questa proprietà consente di specificare in modo esplicito i singoli attributi che si desidera mantenere. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | Questa proprietà consente di ignorare il valore del nome dell&#39;attributo specificato in `explodeEntityPath`. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | Definisce i parametri o i campi da fornire per ottenere un collegamento alla pagina successiva dalla risposta della pagina corrente dell&#39;utente o durante la creazione di un URL della pagina successiva. |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | Visualizza il tipo di impaginazione supportato per l&#39;origine. | <ul><li>`OFFSET`: questo tipo di impaginazione consente di analizzare i risultati specificando un indice da cui avviare l&#39;array risultante e un limite al numero di risultati restituiti.</li><li>`POINTER`: questo tipo di impaginazione consente di utilizzare una variabile `pointer` per puntare a un elemento particolare che deve essere inviato con una richiesta. L&#39;impaginazione del tipo di puntatore richiede il percorso nel payload che punta alla pagina successiva.</li><li>`CONTINUATION_TOKEN`: questo tipo di impaginazione ti consente di aggiungere alla query o ai parametri di intestazione un token di continuazione per recuperare i dati restituiti rimanenti dall&#39;origine che non sono stati inizialmente restituiti a causa di un massimo predeterminato.</li><li>`PAGE`: questo tipo di impaginazione ti consente di aggiungere al parametro di query un parametro di paging per scorrere i dati restituiti per pagine, a partire dalla pagina zero.</li><li>`NONE`: questo tipo di impaginazione può essere utilizzato per le origini che non supportano nessuno dei tipi di impaginazione disponibili. Il tipo di impaginazione `NONE` restituisce tutti i dati di risposta dopo una richiesta.</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | Il nome del limite attraverso il quale l’API può specificare il numero di record da recuperare in una pagina. | `limit` o `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | Il numero di record da recuperare in una pagina. | `limit=10` o `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | Nome dell&#39;attributo di offset. Questa opzione è necessaria se il tipo di paginazione è impostato su `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | Nome dell&#39;attributo del puntatore. Questo richiede il percorso json dell’attributo che punterà alla pagina successiva. Questa opzione è necessaria se il tipo di paginazione è impostato su `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | Contiene parametri che definiscono i formati di pianificazione supportati per l&#39;origine. I parametri di pianificazione includono `startTime` e `endTime`, che consentono di impostare intervalli di tempo specifici per le esecuzioni batch, in modo da garantire che i record recuperati in una precedente esecuzione batch non vengano recuperati. |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | Definisce il nome del parametro dell&#39;ora di inizio | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | Definisce il nome del parametro dell&#39;ora di fine | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | Definisce il formato supportato per `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | Definisce il formato supportato per `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Definisce i parametri forniti dall&#39;utente per recuperare i valori delle risorse. | Consulta le [risorse aggiuntive](#user-input) per un esempio dei parametri immessi dall&#39;utente per `spec.properties`. |

{style="table-layout:auto"}

## Risorse aggiuntive {#appendix}

Nelle sezioni seguenti vengono fornite informazioni sulle configurazioni aggiuntive che è possibile apportare a `sourceSpec`, inclusi la pianificazione avanzata e gli schemi personalizzati.

### Esempio di percorso del contenuto {#content-path}

Di seguito è riportato un esempio del contenuto della proprietà `contentPath` in una specifica di connessione [!DNL MailChimp Members].

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

### Esempio di input utente `spec.properties` {#user-input}

Di seguito è riportato un esempio di `spec.properties` fornito dall&#39;utente che utilizza una specifica di connessione [!DNL MailChimp Members].

In questo esempio, `listId` viene fornito come parte di `urlParams.path`. Se devi recuperare `listId` da un cliente, devi definirlo anche come parte di `spec.properties`.


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

### Esempio di specifica Source {#source-spec}

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

Di seguito sono riportati alcuni esempi di altri tipi di impaginazione supportati dalle origini self-service (Batch SDK):

>[!BEGINTABS]

>[!TAB Offset]

Questo tipo di impaginazione consente di analizzare i risultati specificando un indice da cui avviare la matrice risultante e un limite sul numero di risultati restituiti. Ad esempio:

```json
"paginationParams": {
        "type": "OFFSET",
        "limitName": "limit",
        "limitValue": "4",
        "offSetName": "offset",
        "endConditionName": "$.hasMore",
        "endConditionValue": "Const:false"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `type` | Tipo di impaginazione utilizzato per restituire i dati. |
| `limitName` | Il nome del limite attraverso il quale l’API può specificare il numero di record da recuperare in una pagina. |
| `limitValue` | Il numero di record da recuperare in una pagina. |
| `offSetName` | Nome dell&#39;attributo di offset. Questa opzione è necessaria se il tipo di paginazione è impostato su `offset`. |
| `endConditionName` | Valore definito dall&#39;utente che indica la condizione che terminerà il ciclo di impaginazione nella successiva richiesta HTTP. È necessario specificare il nome dell&#39;attributo in cui inserire la condizione finale. |
| `endConditionValue` | Il valore dell’attributo sul quale vuoi inserire la condizione finale. |

>[!TAB Puntatore]

Questo tipo di impaginazione consente di utilizzare una variabile `pointer` per puntare a un elemento particolare che deve essere inviato con una richiesta. L&#39;impaginazione del tipo di puntatore richiede il percorso nel payload che punta alla pagina successiva. Ad esempio:

```json
{
 "type": "POINTER",
 "limitName": "limit",
 "limitValue": 1,
 "pointerPath": "paging.next"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `type` | Tipo di impaginazione utilizzato per restituire i dati. |
| `limitName` | Il nome del limite attraverso il quale l’API può specificare il numero di record da recuperare in una pagina. |
| `limitValue` | Il numero di record da recuperare in una pagina. |
| `pointerPath` | Nome dell&#39;attributo del puntatore. Questo richiede il percorso json dell’attributo che punterà alla pagina successiva. |

>[!TAB Token di continuazione]

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
| `parameterType` | La proprietà `parameterType` definisce dove è necessario aggiungere `parameterName`. Il tipo `QUERYPARAM` ti consente di aggiungere la query a `parameterName`. `HEADERPARAM` ti consente di aggiungere `parameterName` alla richiesta di intestazione. |
| `parameterName` | Nome del parametro utilizzato per incorporare il token di continuazione. Formato: `{PARAMETER_NAME}={CONTINUATION_TOKEN}`. |
| `delayRequestMillis` | La proprietà `delayRequestMillis` nell&#39;impaginazione consente di controllare la frequenza delle richieste effettuate all&#39;origine. Alcune origini possono avere un limite al numero di richieste che è possibile effettuare al minuto. Ad esempio, [!DNL Zendesk] ha un limite di 100 richieste al minuto e la definizione di `delayRequestMillis` in `850` consente di configurare l&#39;origine per effettuare chiamate a circa 80 richieste al minuto, ben al di sotto della soglia di 100 richieste al minuto. |

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

>[!TAB Pagina]

Il tipo di impaginazione `PAGE` consente di scorrere i dati restituiti per numero di pagine a partire da zero. Quando si utilizza l&#39;impaginazione di tipo `PAGE`, è necessario fornire il numero di record specificato in una singola pagina.

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
| `endPageIndex` | (Facoltativo) L’indice della pagina finale ti consente di stabilire una condizione di fine e di interrompere l’impaginazione. Questo campo può essere utilizzato quando le condizioni di fine predefinite per interrompere l’impaginazione non sono disponibili. Questo campo può essere utilizzato anche se il numero di pagine da acquisire o l&#39;ultimo numero di pagina viene fornito tramite l&#39;intestazione di risposta, comune quando si utilizza l&#39;impaginazione di tipo `PAGE`. Il valore per l’indice della pagina finale può essere l’ultimo numero di pagina o un valore di espressione di tipo stringa dall’intestazione di risposta. Ad esempio, è possibile utilizzare `headers.x-pagecount` per assegnare l&#39;indice della pagina finale al valore `x-pagecount` dalle intestazioni di risposta. **Nota**: `x-pagecount` è un&#39;intestazione di risposta obbligatoria per alcune origini e contiene il valore numero di pagine da acquisire. |
| `pageParamName` | Il nome del parametro che è necessario accodare ai parametri di query per poter attraversare pagine diverse dei dati restituiti. `https://abc.com?pageIndex=1`, ad esempio, restituirebbe la seconda pagina del payload di ritorno di un&#39;API. |
| `maximumRequest` | Il numero massimo di richieste che un’origine può effettuare per una determinata esecuzione incrementale. Il limite predefinito corrente è 10000. |

{style="table-layout:auto"}


>[!TAB Nessuno]

Il tipo di impaginazione `NONE` può essere utilizzato per le origini che non supportano nessuno dei tipi di impaginazione disponibili. Le origini che utilizzano il tipo di impaginazione di `NONE` restituiscono semplicemente tutti i record recuperabili quando viene effettuata una richiesta GET.

```json
"paginationParams": {
  "type": "NONE"
}
```

>[!ENDTABS]

### Pianificazione avanzata per origini self-service (Batch SDK)

Configura la pianificazione incrementale e di backfill dell’origine utilizzando la pianificazione avanzata. La proprietà `incremental` consente di configurare una pianificazione in cui l&#39;origine acquisirà solo record nuovi o modificati, mentre la proprietà `backfill` consente di creare una pianificazione per acquisire i dati storici.

Con la pianificazione avanzata, puoi utilizzare espressioni e funzioni specifiche della tua origine per configurare pianificazioni incrementali e di backfill. Nell&#39;esempio seguente, l&#39;origine [!DNL Zendesk] richiede che la pianificazione incrementale sia formattata come `type:user updated > {START_TIME} updated < {END_TIME}` e che la retrocompilazione come `type:user updated < {END_TIME}`.

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
| `scheduleParams.type` | Tipo di pianificazione che verrà utilizzato dall&#39;origine. Impostare questo valore su `ADVANCE` per utilizzare il tipo di pianificazione avanzata. |
| `scheduleParams.paramFormat` | Il formato definito del parametro di pianificazione. Questo valore può essere uguale ai valori `scheduleStartParamFormat` e `scheduleEndParamFormat` dell&#39;origine. |
| `scheduleParams.incremental` | La query incrementale dell’origine. Incrementale si riferisce a un metodo di acquisizione in cui vengono acquisiti solo dati nuovi o modificati. |
| `scheduleParams.backfill` | La query di retrocompilazione dell’origine. Il backfill si riferisce a un metodo di acquisizione in cui vengono acquisiti dati storici. |

Dopo aver configurato la pianificazione avanzata, è necessario fare riferimento a `scheduleParams` nella sezione URL, body o header params (Parametri URL, corpo o intestazione), a seconda di ciò che supporta la propria origine. Nell&#39;esempio seguente, `{SCHEDULE_QUERY}` è un segnaposto utilizzato per specificare dove verranno utilizzate le espressioni di pianificazione incrementale e di backfill. Nel caso di un&#39;origine [!DNL Zendesk], `query` viene utilizzato in `queryParams` per specificare la pianificazione avanzata.

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

È possibile includere uno schema personalizzato in `sourceSpec` per definire tutti gli attributi richiesti per l&#39;origine, inclusi gli eventuali attributi dinamici necessari. È possibile aggiornare la specifica di connessione corrispondente dell&#39;origine effettuando una richiesta PUT all&#39;endpoint `/connectionSpecs` dell&#39;API [!DNL Flow Service] e fornendo al contempo lo schema personalizzato nella sezione `sourceSpec` della specifica di connessione.

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

Con le specifiche sorgente compilate, puoi procedere alla configurazione delle specifiche di esplorazione per l’origine che desideri integrare in Experience Platform. Per ulteriori informazioni, consulta il documento sulla [configurazione delle specifiche di esplorazione](./explorespec.md).
