---
description: Questa pagina fornisce tutte le informazioni necessarie per inviare per la revisione di una destinazione creata utilizzando Destination SDK.
title: Invia per la revisione di una destinazione creata in Destination SDK
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: 111da9ce3e38096d11a1910929ee892e5661722c
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# Invia per la revisione di una destinazione creata in Destination SDK

## Panoramica {#overview}

Prima che la destinazione possa essere pubblicata nel [Catalogo delle destinazioni di Experience Platform](/help/destinations/catalog/overview.md), devi fornire ad Adobe alcune informazioni sulla destinazione e sui test eseguiti, per garantire agli utenti la migliore esperienza possibile durante l’attivazione dei dati sulla piattaforma.

In questa pagina sono elencate tutte le informazioni da fornire durante l’invio o l’aggiornamento di una destinazione creata con Adobe Experience Platform Destination SDK. Per inviare correttamente una destinazione in Adobe Experience Platform, invia un messaggio e-mail a <aepdestsdk@adobe.com> che include:

* Una descrizione dei casi di utilizzo risolti dalla destinazione. Questo non è necessario se aggiorni una configurazione di destinazione esistente.
* Verifica i risultati dopo aver utilizzato l’endpoint API di destinazione del test per eseguire una chiamata HTTP alla destinazione. Condividi con Adobe:
   * Chiamata API effettuata all&#39;endpoint di destinazione.
   * Risposta API ricevuta dall’endpoint di destinazione.
* Prova di aver inviato una richiesta di pubblicazione di destinazione per la destinazione utilizzando [API di pubblicazione della destinazione](./destination-publish-api.md).
* (Solo per integrazioni prodotte) una documentazione PR (richiesta di pull), seguendo le istruzioni descritte nel [processo di documentazione self-service](./docs-framework/documentation-instructions.md).
* Un file di immagine che verrà visualizzato come logo per la scheda di destinazione nel catalogo delle destinazioni Experience Platform.

Puoi trovare informazioni dettagliate su ogni elemento nelle sezioni seguenti:

## Descrizione del caso d’uso

Fornisci una descrizione dei casi d’uso che la tua destinazione risolve per i clienti di Experience Platform. Le descrizioni possono essere simili ai casi d&#39;uso dei partner esistenti:

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md): Crea tipi di pubblico dagli elenchi dei clienti, dalle persone che hanno visitato il tuo sito o da persone che hanno già interagito con i tuoi contenuti in Pinterest.
* [Dati Yahoo X](/help/destinations/catalog/advertising/datax.md#use-cases): Le API DataX sono disponibili per gli inserzionisti che desiderano eseguire il targeting di un gruppo di pubblico specifico tenuto fuori dagli indirizzi e-mail in Verizon Media (VMG) possono creare rapidamente un nuovo segmento e inviare il gruppo di pubblico desiderato utilizzando l’API in tempo quasi reale di VMG.

## Risultati del test dopo l’utilizzo dell’API di destinazione del test

Fornire i risultati dei test dopo l&#39;utilizzo del [API di destinazione del test](./test-destination.md) per eseguire una chiamata HTTP alla destinazione. Ciò include:

* La richiesta API completa (intestazioni e corpo) effettuata sull&#39;endpoint di destinazione, utilizzando l&#39;API di test.
* Risposta API ricevuta dall’endpoint di destinazione.

Ad esempio, la richiesta e la risposta potrebbero essere simili agli esempi seguenti:

**Richiesta**

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

**Risposta**

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

## Prova dell&#39;invio di una richiesta di pubblicazione di destinazione

Dopo aver verificato con successo la destinazione, devi utilizzare il [API di pubblicazione della destinazione](./destination-publish-api.md) per inviare la destinazione ad Adobe per la revisione e la pubblicazione.

Fornisci l&#39;ID della richiesta di pubblicazione per la tua destinazione. Per informazioni su come recuperare l’ID richiesta di pubblicazione, leggi [Elenca richieste di pubblicazione di destinazione](./destination-publish-api.md#retrieve-list).

## Documentazione di destinazione PR (richiesta pull) per le integrazioni prodotte

Se sei un fornitore di software indipendente (ISV) o un integratore di sistema (SI) che crea un [integrazione di prodotti](./overview.md#productized-custom-integrations), utilizza [processo di documentazione self-service](./docs-framework/documentation-instructions.md) per creare una pagina di documentazione del prodotto per la destinazione. Come parte del processo di invio, fornisci la richiesta di pull (PR) per la documentazione di destinazione.

## Logo per la destinazione

Il catalogo delle destinazioni include un logo per ogni scheda di destinazione. Nel messaggio e-mail di invio, includi un’immagine con il logo della destinazione.

I requisiti delle immagini sono:
* **Formato**: `SVG`
* **Dimensione**: inferiore a 2 MB

## Scarica e-mail di esempio

[Scarica](./assets/sample-email-submit-destination.rtf) un’e-mail di esempio con tutte le informazioni necessarie da fornire ad Adobe.
