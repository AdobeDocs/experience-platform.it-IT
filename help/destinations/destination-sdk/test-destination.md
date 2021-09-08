---
description: 'Nell’ambito dell’SDK di destinazione, Adobe fornisce strumenti per sviluppatori per aiutarti a configurare e testare la destinazione. Questa pagina descrive come verificare la configurazione di destinazione. '
title: Verifica la configurazione di destinazione
source-git-commit: cf6c6adf128ec867cd67af609a40b04d2c632bf9
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---

# Verifica la configurazione di destinazione {#developer-tools}

## Panoramica {#overview}

Nell’ambito dell’SDK di destinazione, Adobe fornisce strumenti per sviluppatori per aiutarti a configurare e testare la destinazione. Questa pagina descrive come verificare la configurazione di destinazione. Per informazioni su come creare un modello di trasformazione dei messaggi, leggi [Creare e testare un modello di trasformazione dei messaggi](./create-template.md).

Per **verificare se la destinazione è configurata correttamente e per verificare l&#39;integrità dei flussi di dati nella destinazione configurata**, utilizza lo *strumento di test della destinazione*. Con questo strumento, puoi testare la configurazione di destinazione inviando messaggi all’endpoint API REST.

Di seguito è illustrato come il test della destinazione si inserisce nel [flusso di lavoro di configurazione della destinazione](./configure-destination-instructions.md) nell&#39;SDK di destinazione:

![Grafico in cui il passaggio del test di destinazione si inserisce nel flusso di lavoro di configurazione della destinazione](./assets/test-destination-step.png)

## Strumento di test della destinazione {#destination-testing-tool}

Utilizza questo strumento per testare la configurazione di destinazione inviando messaggi all&#39;endpoint partner fornito nella [configurazione server](./server-and-template-configuration.md).

Con questo strumento, dopo aver configurato la destinazione, puoi:
* Verifica se la destinazione è configurata correttamente;
* Verifica l’integrità dei flussi di dati verso la destinazione configurata.

### Come utilizzare {#how-to-use}

>[!NOTE]
>
>Per la documentazione completa di riferimento API, leggi [Operazioni API di test di destinazione](./destination-testing-api.md).

Puoi effettuare chiamate all’endpoint API di test della destinazione con o senza aggiungere profili alla richiesta.

Se non aggiungi profili alla richiesta, Adobe li genererà internamente per te e li aggiungerà alla richiesta. Se desideri generare profili da utilizzare in questa richiesta, consulta il [Riferimento API per la generazione di profili di esempio](./sample-profile-generation-api.md). È necessario generare profili in base allo schema XDM di origine, come mostrato nel [riferimento API](./sample-profile-generation-api.md#generate-sample-profiles-source-schema). Lo schema di origine è lo [schema di unione](https://experienceleague.adobe.com/docs/experience-platform/profile/union-schemas/union-schema.html?lang=en) della sandbox in uso.

La risposta contiene il risultato dell’elaborazione della richiesta di destinazione. La richiesta comprende tre sezioni principali:
* La richiesta generata dall&#39;Adobe per la destinazione.
* Risposta ricevuta dalla destinazione.
* L’elenco dei profili inviati nella richiesta, siano essi [aggiunti dall’utente nella richiesta](./destination-testing-api.md/#test-with-added-profiles) o generati dall’Adobe se [il corpo della richiesta di test di destinazione era vuoto](./destination-testing-api.md#test-without-adding-profiles).

>[!NOTE]
>
>Adobe può generare più coppie di richieste e risposte. Ad esempio, se invii 10 profili a una destinazione con un valore `maxUsersPerRequest` pari a 7, sarà presente una richiesta con 7 profili e un’altra con 3 profili.

**Richiesta di esempio con il parametro profiles nel corpo**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
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

**Richiesta di esempio senza parametro dei profili nel corpo**


```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw ''
```

**Risposta di esempio**

Il contenuto del parametro `results.httpCalls` è specifico per l’API REST.

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

Per una descrizione dei parametri di richiesta e risposta, fai riferimento a [Operazioni API di test di destinazione](./destination-testing-api.md).

## Passaggi successivi

Dopo aver confermato che la destinazione è configurata correttamente, utilizza l&#39;Adobe [processo di documentazione self-service](./docs-framework/documentation-instructions.md) per creare una pagina di documentazione per la destinazione.