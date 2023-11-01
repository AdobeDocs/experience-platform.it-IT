---
description: Scopri come utilizzare l’API di test di destinazione per verificare se la destinazione di streaming è configurata correttamente e per verificare l’integrità dei flussi di dati alla destinazione configurata.
title: Test della destinazione di streaming con profili di esempio
exl-id: 2b54250d-ec30-4ad7-a8be-b86b14e4f074
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 2%

---


# Test della destinazione di streaming con profili di esempio {#template-api-operations}

>[!IMPORTANT]
>
>**Endpoint API**: `https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/`

Questa pagina elenca e descrive tutte le operazioni API che è possibile eseguire utilizzando `/authoring/testing/destinationInstance/` Endpoint API, per verificare se la destinazione è configurata correttamente e per verificare l’integrità dei flussi di dati alla destinazione configurata. Per una descrizione delle funzionalità supportate da questo endpoint, leggere [Verifica la configurazione di destinazione](streaming-destination-testing-overview.md).

Effettuare richieste all’endpoint di test con o senza l’aggiunta di profili alla chiamata. Se non invii profili alla richiesta, Adobe li genera internamente e li aggiunge alla richiesta.

È possibile utilizzare [API di generazione del profilo di esempio](sample-profile-generation-api.md) per creare profili da utilizzare nelle richieste all’API di test di destinazione.

## Ottenere l’ID dell’istanza di destinazione {#get-destination-instance-id}

>[!IMPORTANT]
>
>* Per utilizzare questa API, è necessario disporre di una connessione esistente alla destinazione nell’interfaccia utente di Experienci Platform. Letto [connetti alla destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) e [attivare profili e pubblico in una destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html) per ulteriori informazioni.
> * Dopo aver stabilito la connessione alla destinazione, ottieni l’ID istanza di destinazione da utilizzare nelle chiamate API a questo endpoint quando [esplorazione di una connessione con la destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html).
>![Immagine dell’interfaccia utente per ottenere l’ID dell’istanza di destinazione](../../assets/testing-api/get-destination-instance-id.png)

## Guida introduttiva alle operazioni API di test della destinazione {#get-started}

Prima di continuare, controlla [guida introduttiva](../../getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate all’API, tra cui come ottenere l’autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Verifica la configurazione di destinazione senza aggiungere profili alla chiamata {#test-without-adding-profiles}

Puoi verificare la configurazione di destinazione effettuando una richiesta POST al `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` e fornendo l’ID dell’istanza di destinazione della destinazione da testare.

**Formato API**


```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Parametro query | Descrizione |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | ID dell’istanza di destinazione della destinazione da testare. |

**Richiesta**

La richiesta seguente chiama l’endpoint API REST della destinazione. La richiesta è configurata da `{DESTINATION_INSTANCE_ID}` parametro di query.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 insieme alla risposta API dall’endpoint REST API della destinazione.

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "03fb9938-8537-4b4c-87f9-9c4d413a0ee5":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872039Z",
                  "status":"realized"
               },
               "27e05542-d6a3-46c7-9c8e-d59d50229530":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872042Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-vlnt6"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string"
            }
         }
      }
   ]
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `aggregationKey` | Include informazioni sui criteri di aggregazione configurati per la destinazione. Per ulteriori informazioni, leggere [Criterio di aggregazione](../../functionality/destination-configuration/aggregation-policy.md) documentazione. |
| `traceId` | Identificatore univoco dell&#39;operazione. Quando incontri degli errori, puoi condividere questo ID con il team di Adobi a scopo di risoluzione dei problemi. |
| `results.httpCalls.request` | Include la richiesta inviata da Adobe alla destinazione. |
| `results.httpCalls.response` | Include la risposta ricevuta da Adobe dalla destinazione. |
| `inputProfiles` | Include i profili esportati nella chiamata alla destinazione. I profili corrispondono allo schema di origine. |

{style="table-layout:auto"}

## Verifica la configurazione di destinazione con i profili aggiunti alla chiamata {#test-with-added-profiles}

Puoi verificare la configurazione di destinazione effettuando una richiesta POST al `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` e fornendo l’ID dell’istanza di destinazione della destinazione da testare.

**Formato API**

```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Parametro query | Descrizione |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | ID dell’istanza di destinazione della destinazione da testare. |

**Richiesta**

La richiesta seguente chiama l’endpoint API REST della destinazione. La richiesta è configurata dai parametri forniti nel payload e dal `{DESTINATION_INSTANCE_ID}` parametro di query.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 insieme alla risposta API dall’endpoint REST API della destinazione.

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}
```

## Gestione degli errori API {#api-error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, sai come verificare la destinazione. Ora puoi utilizzare l’Adobe [processo di documentazione self-service](../../docs-framework/documentation-instructions.md) per creare una pagina di documentazione per la destinazione.
