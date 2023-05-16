---
description: Utilizza i modelli di metadati del pubblico per creare, aggiornare o eliminare in modo programmatico i tipi di pubblico nella tua destinazione. Adobe fornisce un modello di metadati estensibili per il pubblico, che puoi configurare in base alle specifiche dell’API di marketing. Dopo aver definito, testato e inviato il modello, questo verrà utilizzato per Adobe per strutturare le chiamate API alla destinazione.
title: Gestione dei metadati del pubblico
source-git-commit: e69bd819fb8ef6c2384a2b843542d1ddcea0661f
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 0%

---


# Gestione dei metadati del pubblico

Utilizza i modelli di metadati del pubblico per creare, aggiornare o eliminare in modo programmatico i tipi di pubblico nella tua destinazione. Adobe fornisce un modello di metadati estensibili per il pubblico, che puoi configurare in base alle specifiche dell’API di marketing. Dopo aver definito, testato e inviato la configurazione, questa verrà utilizzata per Adobe per strutturare le chiamate API alla destinazione.

Puoi configurare la funzionalità descritta in questo documento utilizzando `/authoring/audience-templates` Endpoint API. Leggi [creare un modello di metadati](../metadata-api/create-audience-template.md) per un elenco completo delle operazioni eseguibili sull&#39;endpoint.

## Quando utilizzare l’endpoint per la gestione dei metadati del pubblico {#when-to-use}

A seconda della configurazione dell’API, potrebbe essere necessario o meno utilizzare l’endpoint per la gestione dei metadati del pubblico durante la configurazione della destinazione in Experience Platform. Utilizza il diagramma della struttura decisionale seguente per capire quando utilizzare l&#39;endpoint per i metadati del pubblico e come configurare un modello per i metadati del pubblico per la destinazione.

![Diagramma ad albero decisionale](../assets/functionality/audience-metadata-decision-tree.png)

## Casi di utilizzo supportati dalla gestione dei metadati del pubblico {#use-cases}

Con il supporto dei metadati del pubblico in Destination SDK, quando configuri la destinazione di Experience Platform, puoi dare agli utenti di Platform una delle diverse opzioni quando mappano e attivano i segmenti sulla tua destinazione. Puoi controllare le opzioni disponibili per l’utente tramite i parametri nel [Configurazione dei metadati del pubblico](../functionality/destination-configuration/audience-metadata-configuration.md) della configurazione di destinazione.

### Caso d’uso 1: disponi di un’API di terze parti e gli utenti non devono inserire ID di mappatura

Se disponi di un endpoint API per creare/aggiornare/eliminare segmenti o tipi di pubblico, puoi utilizzare i modelli di metadati del pubblico per configurare la Destination SDK in modo che corrisponda alle specifiche dell’endpoint di creazione/aggiornamento/eliminazione del segmento. Experience Platform può creare/aggiornare/eliminare programmaticamente segmenti e sincronizzare i metadati di nuovo ad Experience Platform.

Quando attivi i segmenti sulla destinazione nell’interfaccia utente di Experience Platform, gli utenti non devono compilare manualmente un campo ID mappatura segmento nel flusso di lavoro di attivazione.

### Caso d’uso 2: prima gli utenti devono creare un segmento nella destinazione e devono immettere manualmente l’ID di mappatura dell’input

Se i segmenti e gli altri metadati devono essere creati manualmente dai partner o dagli utenti nella destinazione, gli utenti devono compilare manualmente il campo ID mappatura segmento nel flusso di lavoro di attivazione per sincronizzare i metadati del segmento tra la destinazione e l’Experience Platform.

![ID mappatura input](../assets/functionality/input-mapping-id.png)

### Caso d’uso 3: la tua destinazione accetta l’ID del segmento di Experience Platform, gli utenti non devono inserire manualmente l’ID di mappatura dell’input

Se il sistema di destinazione accetta l’ID del segmento di Experience Platform, puoi configurarlo nel modello di metadati del pubblico. Gli utenti non devono compilare un ID di mappatura del segmento quando attivano un segmento.

## Modello di pubblico generico ed estensibile {#generic-and-extensible}

Per supportare i casi d’uso elencati sopra, l’Adobe fornisce un modello generico che può essere personalizzato per adattarsi alle specifiche API.

È possibile utilizzare il modello generico per [creare un nuovo modello di pubblico](../metadata-api/create-audience-template.md) se l&#39;API supporta:

* Metodi HTTP: POST, GET, PUT, DELETE, PATCH
* Tipi di autenticazione: OAuth 1, OAuth 2 con token di aggiornamento, OAuth 2 con token portatore
* Funzioni: creare un pubblico, aggiornare un pubblico, ottenere un pubblico, eliminare un pubblico, convalidare le credenziali

Il team di progettazione di Adobe può collaborare con l’utente per espandere il modello generico con campi personalizzati, se richiesto dai casi di utilizzo.

## Esempi di configurazione {#configuration-examples}

Questa sezione include tre esempi di configurazioni generiche di metadati del pubblico, per il tuo riferimento, insieme a descrizioni delle sezioni principali della configurazione. Osserva come url, intestazioni, corpo della richiesta e della risposta differiscono tra le tre configurazioni di esempio. Ciò è dovuto alle diverse specifiche dell’API marketing delle tre piattaforme di esempio.

In alcuni esempi, campi macro come `{{authData.accessToken}}` o `{{segment.name}}` sono utilizzati nell&#39;URL e in altri esempi sono utilizzati nelle intestazioni o nel corpo della richiesta. Dipende veramente dalle specifiche API di marketing.

| Sezione modello | Descrizione |
|--- |--- |
| `create` | Include tutti i componenti richiesti (URL, metodo HTTP, intestazioni, corpo della richiesta e della risposta) per effettuare una chiamata HTTP all’API, creare programmaticamente segmenti/tipi di pubblico nella piattaforma e sincronizzare le informazioni di nuovo a Adobe Experience Platform. |
| `update` | Include tutti i componenti richiesti (URL, metodo HTTP, intestazioni, corpo della richiesta e della risposta) per effettuare una chiamata HTTP all’API, aggiornare programmaticamente segmenti/tipi di pubblico nella piattaforma e sincronizzare le informazioni di nuovo a Adobe Experience Platform. |
| `delete` | Include tutti i componenti richiesti (URL, metodo HTTP, intestazioni, corpo della richiesta e della risposta) per effettuare una chiamata HTTP all’API e eliminare programmaticamente segmenti/tipi di pubblico nella piattaforma. |
| `validate` | Esegue le convalide per qualsiasi campo nella configurazione del modello prima di effettuare una chiamata all&#39;API partner. Ad esempio, puoi verificare che l’ID account dell’utente sia inserito correttamente. |
| `notify` | Si applica solo alle destinazioni basate su file. Include tutti i componenti richiesti (URL, metodo HTTP, intestazioni, corpo della richiesta e della risposta) per effettuare una chiamata HTTP all’API e per avvisarti della riuscita delle esportazioni di file. |

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

Trova descrizioni di tutti i parametri nel modello nel [Creare un modello di pubblico](../metadata-api/create-audience-template.md) Riferimento API.

## Macro utilizzate nei modelli di metadati del pubblico

Per trasmettere informazioni quali ID segmento, token di accesso, messaggi di errore e altro ancora tra Experience Platform e l’API, i modelli di pubblico includono macro utilizzabili. Di seguito è riportata una descrizione delle macro utilizzate nei tre esempi di configurazione presenti in questa pagina:

| Macro | Descrizione |
|--- |--- |
| `{{segment.alias}}` | Ti consente di accedere all’alias del segmento in Experience Platform. |
| `{{segment.name}}` | Ti consente di accedere al nome del segmento in Experience Platform. |
| `{{segment.id}}` | Ti consente di accedere all’ID del segmento in Experience Platform. |
| `{{customerData.accountId}}` | Ti consente di accedere al campo ID account configurato nella configurazione di destinazione. |
| `{{oauth2ServiceAccessToken}}` | Consente di generare in modo dinamico un token di accesso basato sulla configurazione OAuth 2. |
| `{{authData.accessToken}}` | Consente di passare il token di accesso all’endpoint API. Utilizzo `{{authData.accessToken}}` se Experience Platform deve utilizzare token non in scadenza per connettersi alla destinazione, in caso contrario utilizza `{{oauth2ServiceAccessToken}}` per generare un token di accesso. |
| `{{body.segments[0].segment.id}}` | Restituisce l&#39;identificatore univoco del pubblico creato, come valore della chiave `externalAudienceId`. |
| `{{error.message}}` | Restituisce un messaggio di errore che verrà visualizzato agli utenti nell’interfaccia utente di Experience Platform. |

{style="table-layout:auto"}
