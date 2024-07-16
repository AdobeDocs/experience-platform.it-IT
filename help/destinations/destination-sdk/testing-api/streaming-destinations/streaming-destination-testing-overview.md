---
description: Scopri come utilizzare l’API di test di destinazione per testare la configurazione della destinazione di streaming prima di pubblicarla.
title: Panoramica dell’API di test della destinazione di streaming
exl-id: 21e4d647-1168-4cb4-a2f8-22d201e39bba
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# Panoramica dell’API di test della destinazione di streaming

Come parte di Destination SDK, Adobe fornisce strumenti per sviluppatori per aiutarti a configurare e testare la destinazione. Questa pagina descrive come verificare la configurazione di destinazione. Per informazioni su come creare un modello di trasformazione dei messaggi, leggere [Creare e verificare un modello di trasformazione dei messaggi](../../testing-api/streaming-destinations/create-template.md).

Per **verificare se la destinazione è configurata correttamente e per verificare l&#39;integrità dei flussi di dati nella destinazione configurata**, utilizzare lo *strumento di test della destinazione*. Con questo strumento, puoi verificare la configurazione di destinazione inviando messaggi all’endpoint API REST.

Di seguito è illustrato il modo in cui il test della destinazione si inserisce nel [flusso di lavoro di configurazione della destinazione](../../guides/configure-destination-instructions.md) in Destination SDK:

![Immagine di dove il passaggio di test di destinazione si inserisce nel flusso di lavoro di configurazione di destinazione](../../assets/testing-api/test-destination-step.png)

## Strumento di test della destinazione: scopo e prerequisiti {#destination-testing-tool}

Utilizza lo strumento di test di destinazione per verificare la configurazione di destinazione inviando messaggi all&#39;endpoint partner fornito nella [configurazione del server](../../authoring-api/destination-server/create-destination-server.md).

Prima di utilizzare lo strumento, accertati di:
* Configura la destinazione seguendo i passaggi descritti nel [flusso di lavoro di configurazione della destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md) e
* Stabilisci una connessione alla destinazione, come descritto in [Come ottenere l&#39;ID istanza di destinazione](../../testing-api/streaming-destinations/destination-testing-api.md#get-destination-instance-id).

Con questo strumento, dopo aver configurato la destinazione, puoi:
* Verifica se la destinazione è configurata correttamente;
* Verifica l’integrità dei flussi di dati verso la destinazione configurata.

### Come usare {#how-to-use}

>[!NOTE]
>
>Per la documentazione completa sulle API, leggere [Operazioni API per test di destinazione](../../testing-api/streaming-destinations/destination-testing-api.md).

Puoi effettuare chiamate all’endpoint API di test di destinazione con o senza l’aggiunta di profili nella richiesta.

Se non aggiungi profili alla richiesta, Adobe li genera internamente e li aggiunge alla richiesta. Se desideri generare profili da utilizzare in questa richiesta, consulta il [Riferimento API per la generazione di profili di esempio](../../testing-api/streaming-destinations/sample-profile-generation-api.md). Devi generare profili basati sullo schema XDM di origine, come mostrato nel [riferimento API](../../testing-api/streaming-destinations/sample-profile-generation-api.md#generate-sample-profiles-source-schema). Lo schema di origine è lo [schema di unione](../../../../profile/ui/union-schema.md) della sandbox in uso.

La risposta contiene il risultato dell’elaborazione della richiesta di destinazione. La richiesta include tre sezioni principali:
* La richiesta generata da Adobe per la destinazione.
* La risposta ricevuta dalla destinazione.
* L&#39;elenco dei profili inviati nella richiesta, sia che i profili siano stati [aggiunti dall&#39;utente nella richiesta](../../testing-api/streaming-destinations/destination-testing-api.md#test-with-added-profiles), sia che siano stati generati da Adobe se [il corpo della richiesta di test della destinazione era vuoto](../../testing-api/streaming-destinations/destination-testing-api.md#test-without-adding-profiles).

>[!NOTE]
>
>L’Adobe può generare più coppie di richieste e risposte. Ad esempio, se invii 10 profili a una destinazione con un valore `maxUsersPerRequest` di 7, ci sarà una richiesta con 7 profili e un&#39;altra richiesta con 3 profili.

**Richiesta di esempio con parametro profiles nel corpo**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
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
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "attributes":{
            "key":{
               "value":"string"
            }
         }
      }
   ]
}'
```

**Richiesta di esempio senza il parametro dei profili nel corpo**


```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw ''
```

**Risposta di esempio**

Il contenuto del parametro `results.httpCalls` è specifico per l&#39;API REST.

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
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
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

Per le descrizioni dei parametri di richiesta e risposta, fare riferimento a [Operazioni API di test della destinazione](../../testing-api/streaming-destinations/destination-testing-api.md).

## Passaggi successivi

Dopo aver testato la destinazione e aver confermato che è configurata correttamente, utilizza l&#39;[API di pubblicazione della destinazione](../../publishing-api/create-publishing-request.md) per inviare la configurazione all&#39;Adobe per la revisione.
