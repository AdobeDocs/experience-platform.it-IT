---
description: Questa pagina descrive tutte le operazioni API che è possibile eseguire utilizzando l’endpoint API "/authoring/audience-templates".
title: Operazioni API per endpoint metadati pubblico
exl-id: 3444da8c-b2be-4254-980a-8cce7560134d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 5%

---

# Operazioni API per endpoint metadati pubblico

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Questa pagina elenca e descrive tutte le operazioni API che è possibile eseguire utilizzando `/authoring/audience-templates` Endpoint API Per una descrizione di quando utilizzare questo endpoint, leggi [gestione dei metadati del pubblico](./audience-metadata-management.md).

## Guida introduttiva alle operazioni API per i modelli di pubblico {#get-started}

Prima di continuare, controlla [guida introduttiva](./getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate all’API, tra cui come ottenere l’autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Creare un nuovo modello di pubblico {#create}

Per creare un nuovo modello di pubblico, devi effettuare una richiesta POST al `/authoring/audience-templates` endpoint.

**Formato API**

```http
POST /authoring/audience-templates
```

**Richiesta**

La richiesta seguente crea un nuovo modello di metadati di pubblico, configurato dai parametri forniti nel payload. Il payload riportato di seguito include tutti i parametri accettati dal `/authoring/audience-templates` endpoint. Tieni presente che non è necessario aggiungere tutti i parametri alla chiamata e che il modello è personalizzabile, in base ai requisiti API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | Stringa | Il nome del modello di metadati del pubblico per la destinazione. Questo nome verrà visualizzato in qualsiasi messaggio di errore specifico del partner nell’interfaccia utente di Experience Platform, seguito dal messaggio di errore analizzato da `metadataTemplate.create.errorSchemaMap`. |
| `url` | Stringa | L’URL e l’endpoint dell’API, utilizzati per creare, aggiornare, eliminare o convalidare tipi di pubblico/segmenti nella piattaforma. Due esempi di settore: `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` e `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | Stringa | Il metodo utilizzato sull’endpoint per creare, aggiornare, eliminare o convalidare in modo programmatico il segmento o il pubblico nella destinazione. Ad esempio: `POST`, `PUT`, `DELETE` |
| `headers.header` | Stringa | Specifica eventuali intestazioni HTTP da aggiungere alla chiamata all’API. Ad esempio, `"Content-Type"` |
| `headers.value` | Stringa | Specifica il valore delle intestazioni HTTP da aggiungere alla chiamata all’API. Ad esempio, `"application/x-www-form-urlencoded"` |
| `requestBody` | Stringa | Specifica il contenuto del corpo del messaggio da inviare all’API. I parametri da aggiungere al `requestBody` L’oggetto dipende dai campi accettati dall’API. Ad esempio, consulta [primo esempio di modello](./audience-metadata-management.md#example-1) nel documento relativo alla funzionalità Metadati del pubblico. |
| `responseFields.name` | Stringa | Specifica eventuali campi di risposta restituiti dall’API quando vengono chiamati. Ad esempio, consulta [esempi di modelli](./audience-metadata-management.md#examples) nel documento relativo alla funzionalità Metadati del pubblico. |
| `responseFields.value` | Stringa | Specifica il valore di tutti i campi di risposta restituiti dall’API quando vengono chiamati. |
| `responseErrorFields.name` | Stringa | Specifica eventuali campi di risposta restituiti dall’API quando vengono chiamati. Ad esempio, consulta [ esempi di modelli](./audience-metadata-management.md#examples) nel documento relativo alla funzionalità Metadati del pubblico. |
| `responseErrorFields.value` | Stringa | Analizza eventuali messaggi di errore restituiti nelle risposte alle chiamate API dalla destinazione. Questi messaggi di errore verranno visualizzati dagli utenti nell’interfaccia utente di Experience Platform. |
| `validations.field` | Stringa | Indica se è necessario eseguire le convalide per qualsiasi campo prima di effettuare chiamate API alla destinazione. Ad esempio, puoi utilizzare `{{validations.accountId}}` per convalidare l’ID account dell’utente. |
| `validations.regex` | Stringa | Indica come deve essere strutturato il campo affinché la convalida possa passare. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli del modello di pubblico appena creato.

## Aggiorna modello di pubblico {#update}

Per aggiornare un modello di pubblico esistente, devi effettuare una richiesta PUT al `/authoring/audience-templates` e fornendo l’ID istanza del modello di pubblico da aggiornare. Fornisci il modello aggiornato nel corpo della chiamata.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

## Recuperare un elenco di modelli di pubblico {#retrieve-list}

Per recuperare un elenco di tutti i modelli di pubblico per la tua organizzazione IMS, devi effettuare una richiesta GET al `/authoring/audience-templates` endpoint.

**Formato API**


```http
GET /authoring/audience-templates
```

**Richiesta**

La seguente richiesta recupererà l’elenco dei modelli di pubblico a cui hai accesso, in base alla configurazione di sandbox e organizzazione IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La seguente risposta restituisce lo stato HTTP 200 con un elenco di modelli di metadati di pubblico a cui hai accesso, in base all’ID organizzazione IMS e al nome della sandbox utilizzati. Uno `instanceId` corrisponde al modello per una destinazione. La risposta viene troncata per brevità.

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

## Recuperare un modello di pubblico specifico {#get}

Per recuperare informazioni dettagliate su un modello di pubblico specifico, effettua una richiesta GET al `/authoring/audience-templates` e fornendo l’ID istanza del modello di pubblico da recuperare.

**Formato API**

```http
GET /authoring/audience-templates/{INSTANCE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID del modello di metadati del pubblico che desideri recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni dettagliate sul modello di pubblico specificato.

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

Per eliminare il modello di pubblico specificato, devi effettuare una richiesta DELETE al `/authoring/audience-templates` e fornendo l’ID del modello di pubblico da eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{INSTANCE_ID}` | Il `id` del modello di pubblico da eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 insieme a una risposta HTTP vuota.

## Gestione degli errori API

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai quando utilizzare i modelli di metadati del pubblico e come configurare un modello di metadati del pubblico utilizzando `/authoring/audience-templates` Endpoint API Letto [come utilizzare Destination SDK per configurare la destinazione](./configure-destination-instructions.md) per capire in che modo questo passaggio si inserisce nel processo di configurazione della destinazione.
