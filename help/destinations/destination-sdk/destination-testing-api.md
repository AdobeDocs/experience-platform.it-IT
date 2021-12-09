---
description: Questa pagina elenca e descrive tutte le operazioni API che è possibile eseguire utilizzando l'endpoint API `/authoring/testing/destinationInstance/`, per verificare se la destinazione è configurata correttamente e per verificare l'integrità dei dati che fluiscono nella destinazione configurata.
title: Operazioni API per il test di destinazione
exl-id: 2b54250d-ec30-4ad7-a8be-b86b14e4f074
source-git-commit: 52ce788f6947300b607dfc2efa09d028f9c2ddd7
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 2%

---

# Operazioni API per il test di destinazione {#template-api-operations}

>[!IMPORTANT]
>
>**Endpoint API**: `https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/`

Questa pagina elenca e descrive tutte le operazioni API che puoi eseguire utilizzando `/authoring/testing/destinationInstance/` endpoint API per verificare se la destinazione è configurata correttamente e l’integrità dei dati scorre nella destinazione configurata. Per una descrizione delle funzionalità supportate da questo endpoint, leggere [Verifica la configurazione di destinazione](./test-destination.md).

Esegui richieste all’endpoint di test con o senza aggiungere profili alla chiamata . Se non invii profili alla richiesta, Adobe li genererà internamente per te e li aggiungerà alla richiesta.

È possibile utilizzare [API di generazione di profili di esempio](./sample-profile-generation-api.md) per creare profili da utilizzare nelle richieste per l’API di test di destinazione.

## Come ottenere l&#39;ID dell&#39;istanza di destinazione {#get-destination-instance-id}

>[!IMPORTANT]
>
>* Per utilizzare questa API, è necessario disporre di una connessione esistente alla destinazione nell’interfaccia utente di Experience Platform. Leggi [connessione a destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) e [attivare profili e segmenti in una destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) per ulteriori informazioni. Dopo aver stabilito la connessione alla destinazione, ottieni l’ID dell’istanza di destinazione da utilizzare nelle chiamate API a questo endpoint dall’URL quando [esplorazione di una connessione con la destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html?lang=en).
   >![Immagine dell&#39;interfaccia utente come ottenere l&#39;ID dell&#39;istanza di destinazione](./assets/get-destination-instance-id.png)


## Guida introduttiva al test della destinazione delle operazioni API {#get-started}

Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, tra cui come ottenere l’autorizzazione di authoring di destinazione richiesta e le intestazioni richieste.

## Verifica la configurazione di destinazione senza aggiungere profili alla chiamata . {#test-without-adding-profiles}

Puoi verificare la configurazione di destinazione effettuando una richiesta di POST al `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` e fornisce l&#39;ID dell&#39;istanza di destinazione della destinazione che stai testando.

**Formato API**


```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Parametro query | Descrizione |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | L&#39;ID dell&#39;istanza di destinazione della destinazione che stai testando. |

**Richiesta**

La richiesta seguente chiama l’endpoint API REST della destinazione. La richiesta è configurata dalla `{DESTINATION_INSTANCE_ID}` parametro query.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 insieme alla risposta API dall’endpoint REST API della destinazione.

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
| `aggregationKey` | Include informazioni sul criterio di aggregazione configurato per la destinazione. Per ulteriori informazioni, consulta la sezione [Criteri di aggregazione](./destination-configuration.md#aggregation) nel documento di configurazione della destinazione. |
| `traceId` | Identificatore univoco per l&#39;operazione. Quando si verificano degli errori, puoi condividere questo ID con il team di Adobe per scopi di risoluzione dei problemi. |
| `results.httpCalls.request` | Include la richiesta inviata da Adobe alla destinazione. |
| `results.httpCalls.response` | Include la risposta ricevuta dall’Adobe dalla destinazione. |
| `inputProfiles` | Include i profili esportati nella chiamata alla destinazione. I profili corrispondono allo schema di origine. |

{style=&quot;table-layout:auto&quot;}

## Verifica la configurazione di destinazione con i profili aggiunti alla chiamata . {#test-with-added-profiles}

Puoi verificare la configurazione di destinazione effettuando una richiesta di POST al `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` e fornisce l&#39;ID dell&#39;istanza di destinazione della destinazione che stai testando.

**Formato API**

```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Parametro query | Descrizione |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | L&#39;ID dell&#39;istanza di destinazione della destinazione che stai testando. |

**Richiesta**

La richiesta seguente chiama l’endpoint API REST della destinazione. La richiesta è configurata dai parametri forniti nel payload e dalla `{DESTINATION_INSTANCE_ID}` parametro query.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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

Una risposta corretta restituisce lo stato HTTP 200 insieme alla risposta API dall’endpoint REST API della destinazione.

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

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) e [errori di intestazione della richiesta](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come verificare la destinazione. Ora puoi utilizzare l’Adobe [processo di documentazione self-service](./docs-framework/documentation-instructions.md) per creare una pagina della documentazione per la destinazione.
