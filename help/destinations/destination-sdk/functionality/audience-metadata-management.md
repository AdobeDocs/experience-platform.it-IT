---
description: Utilizza i modelli di metadati del pubblico per creare, aggiornare o eliminare in modo programmatico i tipi di pubblico nella tua destinazione. Adobe fornisce un modello estensibile di metadati per il pubblico, che puoi configurare in base alle specifiche della tua API di marketing. Dopo aver definito, testato e inviato il modello, questo verrà utilizzato da Adobe per strutturare le chiamate API alla destinazione.
title: Gestione dei metadati del pubblico
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 0%

---


# Gestione dei metadati del pubblico

Utilizza i modelli di metadati del pubblico per creare, aggiornare o eliminare in modo programmatico i tipi di pubblico nella tua destinazione. Adobe fornisce un modello estensibile di metadati per il pubblico, che puoi configurare in base alle specifiche della tua API di marketing. Dopo aver definito, testato e inviato la configurazione, questa verrà utilizzata da Adobe per strutturare le chiamate API alla destinazione.

È possibile configurare la funzionalità descritta in questo documento utilizzando `/authoring/audience-templates` Endpoint API Letto [creare un modello di metadati](../metadata-api/create-audience-template.md) per un elenco completo delle operazioni che è possibile eseguire sull&#39;endpoint.

## Quando utilizzare l’endpoint di gestione dei metadati dell’audience {#when-to-use}

A seconda della configurazione API, potrebbe essere necessario utilizzare o meno l’endpoint di gestione dei metadati dell’audience durante la configurazione della destinazione in Experience Platform. Utilizza il diagramma dell’albero decisionale seguente per capire quando utilizzare l’endpoint dei metadati del pubblico e come configurare un modello di metadati del pubblico per la tua destinazione.

![Diagramma dell’albero decisionale](../assets/functionality/audience-metadata-decision-tree.png)

## Casi d’uso supportati dalla gestione dei metadati dell’audience {#use-cases}

Con il supporto dei metadati del pubblico in Destination SDK, quando configuri la destinazione di Experience Platform, puoi offrire agli utenti di Platform una di più opzioni quando mappano e attivano i tipi di pubblico nella destinazione. Puoi controllare le opzioni disponibili per l’utente tramite i parametri nella sezione [Configurazione dei metadati del pubblico](../functionality/destination-configuration/audience-metadata-configuration.md) della configurazione di destinazione.

### Caso d’uso 1: disponi di un’API di terze parti e gli utenti non devono immettere ID di mappatura

Se disponi di un endpoint API per creare/aggiornare/eliminare tipi di pubblico o tipi di pubblico, puoi utilizzare i modelli di metadati del pubblico per configurare Destination SDK in modo che corrisponda alle specifiche dell’endpoint creazione/aggiornamento/eliminazione del pubblico. Experience Platform può creare, aggiornare o eliminare a livello di programmazione tipi di pubblico e sincronizzare nuovamente i metadati con Experience Platform.

Quando si attivano dei tipi di pubblico nella destinazione nell&#39;interfaccia utente di Experience Platform, gli utenti non devono compilare manualmente un campo ID di mappatura pubblico nel flusso di lavoro di attivazione.

### Caso d’uso 2: gli utenti devono prima creare un’audience nella destinazione e devono inserire manualmente l’ID della mappatura

Se i tipi di pubblico e altri metadati devono essere creati manualmente dai partner o dagli utenti nella tua destinazione, gli utenti devono compilare manualmente il campo ID mappatura pubblico nel flusso di lavoro di attivazione per sincronizzare i metadati del pubblico tra la destinazione e l’Experience Platform.

![ID mappatura input](../assets/functionality/input-mapping-id.png)

### Caso d’uso 3: la destinazione accetta l’ID del pubblico Experience Platform e gli utenti non devono inserire manualmente l’ID della mappatura

Se il sistema di destinazione accetta l&#39;ID pubblico Experience Platform, puoi configurarlo nel modello di metadati del pubblico. Gli utenti non devono compilare un ID di mappatura del pubblico quando attivano un segmento.

## Modello di pubblico generico ed estensibile {#generic-and-extensible}

Per supportare i casi d’uso elencati sopra, Adobe fornisce un modello generico che può essere personalizzato per adattarsi alle specifiche API.

È possibile utilizzare il modello generico per [creare un nuovo modello di pubblico](../metadata-api/create-audience-template.md) se l’API supporta:

* I metodi HTTP: POST, GET, PUT, DELETE, PATCH
* Tipi di autenticazione: OAuth 1, OAuth 2 con token di aggiornamento, OAuth 2 con token bearer
* Funzioni: crea un pubblico, aggiorna un pubblico, ottieni un pubblico, elimina un pubblico, convalida le credenziali.

Se necessario, il team di progettazione Adobe può collaborare con te per espandere il modello generico con campi personalizzati.

## Esempi di configurazione {#configuration-examples}

Questa sezione include tre esempi di configurazioni di metadati di pubblico generici, come riferimento, insieme alle descrizioni delle sezioni principali della configurazione. Osserva come l’URL, le intestazioni, la richiesta e il corpo della risposta differiscono tra le tre configurazioni di esempio. Ciò è dovuto alle diverse specifiche delle tre piattaforme di esempio nell’API di marketing.

In alcuni esempi, i campi macro come `{{authData.accessToken}}` o `{{segment.name}}` sono utilizzati nell’URL e in altri esempi vengono utilizzati nelle intestazioni o nel corpo della richiesta. Dipende davvero dalle specifiche API di marketing.

| Sezione modello | Descrizione |
|--- |--- |
| `create` | Include tutti i componenti necessari (URL, metodo HTTP, intestazioni, corpo della richiesta e della risposta) per effettuare una chiamata HTTP all’API, creare in modo programmatico segmenti/tipi di pubblico nella piattaforma e sincronizzare nuovamente le informazioni con Adobe Experience Platform. |
| `update` | Include tutti i componenti necessari (URL, metodo HTTP, intestazioni, corpo della richiesta e della risposta) per effettuare una chiamata HTTP all’API, aggiornare programmaticamente segmenti/tipi di pubblico nella piattaforma e sincronizzare nuovamente le informazioni con Adobe Experience Platform. |
| `delete` | Include tutti i componenti necessari (URL, metodo HTTP, intestazioni, corpo della richiesta e della risposta) per effettuare una chiamata HTTP all’API, per eliminare in modo programmatico segmenti/tipi di pubblico nella piattaforma. |
| `validate` | Esegue le convalide per qualsiasi campo nella configurazione del modello prima di effettuare una chiamata all&#39;API partner. Ad esempio, puoi verificare che l’ID account dell’utente sia stato immesso correttamente. |
| `notify` | Si applica solo alle destinazioni basate su file. Include tutti i componenti necessari (URL, metodo HTTP, intestazioni, corpo della richiesta e della risposta) per effettuare una chiamata HTTP all’API e ricevere una notifica sulle esportazioni dei file riuscite. |

{style="table-layout:auto"}

### Esempio di streaming 1 {#example-1}

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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

### Esempio di streaming 2 {#example-2}

```json
{
   "instanceId":"12c78017-5af3-4d4e-8f9c-d330c547c482",
   "createdDate":"2021-07-20T13:27:37.029490Z",
   "lastModifiedDate":"2021-07-20T18:53:03.622306Z",
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

### Esempio di streaming 3 {#example-3}

```json
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
```


### Esempio basato su file {#example-file-based}

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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
      "notify":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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

Trova descrizioni di tutti i parametri nel modello in [Creare un modello di pubblico](../metadata-api/create-audience-template.md) Riferimento API.

## Macro utilizzate nei modelli di metadati del pubblico

Per trasmettere informazioni quali ID pubblico, token di accesso, messaggi di errore e altro ancora tra Experience Platform e l’API, i modelli di pubblico includono macro che è possibile utilizzare. Di seguito è riportata una descrizione delle macro utilizzate nei tre esempi di configurazione riportati in questa pagina:

| Macro | Descrizione |
|--- |--- |
| `{{segment.alias}}` | Consente di accedere all’alias del pubblico in Experience Platform. |
| `{{segment.name}}` | Consente di accedere al nome del pubblico in Experience Platform. |
| `{{segment.id}}` | Consente di accedere all’ID del pubblico in Experience Platform. |
| `{{customerData.accountId}}` | Ti consente di accedere al campo ID account configurato nella configurazione di destinazione. |
| `{{oauth2ServiceAccessToken}}` | Consente di generare dinamicamente un token di accesso in base alla configurazione OAuth 2. |
| `{{authData.accessToken}}` | Ti consente di passare il token di accesso all’endpoint API. Utilizzare `{{authData.accessToken}}` se in Experience Platform si desidera utilizzare token senza scadenza per la connessione alla destinazione, altrimenti utilizza `{{oauth2ServiceAccessToken}}` per generare un token di accesso. |
| `{{body.segments[0].segment.id}}` | Restituisce l’identificatore univoco del pubblico creato come valore della chiave `externalAudienceId`. |
| `{{error.message}}` | Restituisce un messaggio di errore che verrà mostrato agli utenti nell’interfaccia utente di Experience Platform. |

{style="table-layout:auto"}
