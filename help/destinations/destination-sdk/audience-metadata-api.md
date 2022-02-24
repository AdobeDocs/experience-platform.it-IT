---
description: Questa pagina descrive tutte le operazioni API che puoi eseguire utilizzando l'endpoint API `/authoring/audience-templates`.
title: Operazioni API per l’endpoint dei metadati del pubblico
exl-id: 3444da8c-b2be-4254-980a-8cce7560134d
source-git-commit: afdabdebe9b82d828cb1941edb99ca2518a941a2
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 5%

---

# Operazioni API per l’endpoint dei metadati del pubblico

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Questa pagina elenca e descrive tutte le operazioni API che puoi eseguire utilizzando `/authoring/audience-templates` Endpoint API. Per una descrizione di quando utilizzare questo endpoint, leggere [gestione dei metadati del pubblico](./audience-metadata-management.md).

## Guida introduttiva alle operazioni API con i modelli di pubblico {#get-started}

Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, tra cui come ottenere l’autorizzazione di authoring di destinazione richiesta e le intestazioni richieste.

## Creare un nuovo modello di pubblico {#create}

Puoi creare un nuovo modello di pubblico effettuando una richiesta di POST al `/authoring/audience-templates` punto finale.

**Formato API**

```http
POST /authoring/audience-templates
```

**Richiesta**

La seguente richiesta crea un nuovo modello di metadati del pubblico, configurato dai parametri forniti nel payload. Il payload seguente include tutti i parametri accettati dal `/authoring/audience-templates` punto finale. Non è necessario aggiungere tutti i parametri alla chiamata e il modello è personalizzabile, in base ai requisiti API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "name":"string",
      "create":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "update":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "delete":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "validate":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "notify":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      }
   },
   "validations":[
      {
         "field":"string",
         "regex":"string"
      }
   ]
}'
```

| Proprietà | Tipo | Descrizione |
| -------- | ----------- | ----------- |
| `name` | Stringa | Nome del modello di metadati del pubblico per la destinazione. Questo nome verrà visualizzato in qualsiasi messaggio di errore specifico del partner nell’interfaccia utente di Experience Platform, seguito dal messaggio di errore analizzato da `metadataTemplate.create.errorSchemaMap`. |
| `url` | Stringa | L’URL e l’endpoint dell’API, utilizzati per creare, aggiornare, eliminare o convalidare i tipi di pubblico/segmenti nella piattaforma. Due esempi di settore sono: `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` e `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | Stringa | Il metodo utilizzato sull’endpoint per creare, aggiornare, eliminare o convalidare programmaticamente il segmento o il pubblico nella destinazione. Esempio: `POST`, `PUT`, `DELETE` |
| `headers.header` | Stringa | Specifica le intestazioni HTTP da aggiungere alla chiamata all&#39;API. Ad esempio, `"Content-Type"` |
| `headers.value` | Stringa | Specifica il valore delle intestazioni HTTP da aggiungere alla chiamata all&#39;API. Ad esempio, `"application/x-www-form-urlencoded"` |
| `requestBody` | Stringa | Specifica il contenuto del corpo del messaggio da inviare all&#39;API. I parametri da aggiungere al `requestBody` a seconda dei campi accettati dall’API. Ad esempio, consulta [primo esempio di modello](./audience-metadata-management.md#example-1) nel documento sulla funzionalità metadati pubblico . |
| `responseFields.name` | Stringa | Specifica tutti i campi di risposta che l&#39;API restituisce quando viene chiamata. Ad esempio, consulta [esempi di modelli](./audience-metadata-management.md#examples) nel documento sulla funzionalità metadati pubblico . |
| `responseFields.value` | Stringa | Specifica il valore di tutti i campi di risposta che l&#39;API restituisce quando viene chiamata. |
| `responseErrorFields.name` | Stringa | Specifica tutti i campi di risposta che l&#39;API restituisce quando viene chiamata. Ad esempio, consulta [ esempi di modelli](./audience-metadata-management.md#examples) nel documento sulla funzionalità metadati pubblico . |
| `responseErrorFields.value` | Stringa | Analizza eventuali messaggi di errore restituiti nelle risposte alle chiamate API dalla destinazione. Questi messaggi di errore verranno visualizzati agli utenti nell’interfaccia utente di Experience Platform. |
| `validations.field` | Stringa | Indica se è necessario eseguire le convalide per qualsiasi campo prima che le chiamate API vengano effettuate alla destinazione. Ad esempio, puoi utilizzare `{{validations.accountId}}` per convalidare l’ID account dell’utente. |
| `validations.regex` | Stringa | Indica la struttura del campo per il superamento della convalida. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli del modello di pubblico appena creato.

## Aggiornare il modello di pubblico {#update}

Puoi aggiornare un modello di pubblico esistente effettuando una richiesta di PUT al `/authoring/audience-templates` e fornisce l’ID istanza del modello di pubblico da aggiornare. Nel corpo della chiamata , fornisci il modello aggiornato.

**Formato API**

```http
PUT /authoring/audience-templates/{INSTANCE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID del modello di metadati del pubblico che desideri aggiornare. |

**Richiesta**

La richiesta seguente aggiorna un modello di metadati di pubblico esistente, configurato dai parametri forniti nel payload.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1.0/{{customerData.accountId}}/customaudiences?fields=name,description,account_id&subtype=CUSTOM&name={{segment.name}}&customer_file_source={{segment.metadata.customer_file_source}}&access_token={{authData.accessToken}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?field=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}&&name={{segment.name}}&description={{segment.description}}&customer_file_source={{segment.metadata.customer_file_source}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?fields=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "validate":{
         "url":"https://api.moviestar.com/v1.0/permissions?access_token={{authData.accessToken}}",
         "httpMethod":"GET",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.data[0].permission}}",
               "name":"Id"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      }
   }
}
```

## Recupera un elenco di modelli di pubblico {#retrieve-list}

Puoi recuperare un elenco di tutti i modelli di pubblico per la tua organizzazione IMS effettuando una richiesta di GET al `/authoring/audience-templates` punto finale.

**Formato API**


```http
GET /authoring/audience-templates
```

**Richiesta**

La seguente richiesta recupererà l’elenco di modelli di pubblico a cui hai accesso, in base alla configurazione dell’organizzazione IMS e della sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta seguente restituisce lo stato HTTP 200 con un elenco di modelli di metadati del pubblico a cui hai accesso, in base all’ID organizzazione IMS e al nome della sandbox utilizzati. Uno `instanceId` corrisponde al modello per una destinazione. La risposta viene troncata per brevità.

```json
{
   "items":[
      {
         "instanceId":"12a3238f-b509-4a40-b8fb-0a5006e7901d",
         "createdDate":"2021-07-20T13:30:30.843054Z",
         "lastModifiedDate":"2021-07-21T16:33:05.787472Z",
         "metadataTemplate":{
            "create":{
               "url":"https://api.moviestar.com/v2/dmpSegments",
               "httpMethod":"POST",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "requestBody":{
                  "json":{
                     "name":"{{segment.name}}",
                     "type":"USER",
                     "account":"{{customerData.accountId}}",
                     "accessPolicy":"PRIVATE",
                     "destinations":[
                        {
                           "destination":"MOVIESTAR"
                        }
                     ],
                     "sourcePlatform":"ADOBE"
                  }
               },
               "responseFields":[
                  {
                     "value":"{{headers.x-moviestar-id}}",
                     "name":"externalAudienceId"
                  }
               ],
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "update":{
               "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
               "httpMethod":"POST",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "requestBody":{
                  "json":{
                     "patch":{
                        "$set":{
                           "name":"{{segment.name}}"
                        }
                     }
                  }
               },
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "delete":{
               "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
               "httpMethod":"DELETE",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "name":"Moviestar audience template - Third example"
         }
      }
   ]
}
```

## Recupera un modello di pubblico specifico {#get}

Puoi recuperare informazioni dettagliate su un modello di pubblico specifico effettuando una richiesta GET al `/authoring/audience-templates` e fornisce l’ID istanza del modello di pubblico che desideri recuperare.

**Formato API**

```http
GET /authoring/audience-templates/{INSTANCE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID del modello di metadati del pubblico da recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sul modello di pubblico specificato.

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```


## Eliminare un modello di pubblico specifico {#delete}

Puoi eliminare il modello di pubblico specificato effettuando una richiesta di DELETE al `/authoring/audience-templates` e fornisce l’ID del modello di pubblico da eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{INSTANCE_ID}` | La `id` del modello di pubblico da eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 insieme a una risposta HTTP vuota.

## Gestione degli errori API

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai quando utilizzare i modelli di metadati del pubblico e come configurare un modello di metadati del pubblico utilizzando `/authoring/audience-templates` Endpoint API. Leggi [come utilizzare Destination SDK per configurare la destinazione](./configure-destination-instructions.md) per capire dove si adatta questo passaggio al processo di configurazione della destinazione.
