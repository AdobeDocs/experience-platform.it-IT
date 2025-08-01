---
description: Questa pagina fornisce tutte le informazioni necessarie per inviare una destinazione prodotta per la revisione quando viene creata con Destination SDK.
title: Inviare una destinazione prodotta per la revisione
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 0%

---

# Inviare una destinazione prodotta per la revisione

## Panoramica {#overview}

>[!IMPORTANT]
>
>* Il processo qui documentato è necessario solo per i partner che inviano destinazioni (pubbliche) prodotte. Se stai creando una destinazione privata per il tuo utilizzo personale, non è necessario produrre e condividere questi materiali con Adobe.
>
>* Il tempo di risposta standard di Adobe per esaminare le richieste di pubblicazione delle destinazioni è di cinque giorni lavorativi.
>
>* Se il team di Adobe ti chiede di apportare eventuali aggiornamenti alle configurazioni dopo l’invio iniziale, devi inviare un’altra richiesta di pubblicazione di destinazione dopo aver apportato gli aggiornamenti.
>
>* Anche dopo che la destinazione è live nel catalogo Experience Platform, se devi apportare aggiornamenti alle configurazioni, devi inviare una nuova richiesta di pubblicazione di destinazione affinché gli aggiornamenti vengano rispecchiati nelle configurazioni.
>
>* La timeline di revisione e gli artefatti richiesti sono gli stessi per le nuove destinazioni e le destinazioni esistenti che stai aggiornando.

Prima che la destinazione possa essere pubblicata nel [catalogo delle destinazioni di Experience Platform](/help/destinations/catalog/overview.md), devi fornire ad Adobe determinate informazioni sulla destinazione e sui test eseguiti, per garantire che gli utenti possano godere della migliore esperienza possibile durante l&#39;attivazione dei dati sulla piattaforma.

In questa pagina sono elencate tutte le informazioni che è necessario fornire quando si invia o si aggiorna una destinazione creata con Adobe Experience Platform Destination SDK. Per inviare correttamente una destinazione in Adobe Experience Platform, inviare un&#39;e-mail a <aepdestsdk@adobe.com> che includa:

* Una descrizione dei casi d’uso risolti dalla tua destinazione. Questa operazione è necessaria solo se si invia una nuova configurazione di destinazione.
* Una descrizione del motivo dell’invio a destinazione. Questa opzione è necessaria solo se si sta aggiornando una configurazione di destinazione esistente.
* Risultati del test dopo l’utilizzo dell’endpoint API di destinazione del test per eseguire una chiamata HTTP alla destinazione. Condividi con Adobe una chiamata API effettuata all’endpoint di destinazione e la risposta API ricevuta dall’endpoint di destinazione.
* Una registrazione schermata che mostra l’esperienza utente per qualcuno che si connette alla destinazione e procede attraverso i passaggi di attivazione.
* Requisiti aggiuntivi per le destinazioni basate su file:
   * Condividi una richiesta e un esempio di risposta dopo aver utilizzato l&#39;API di test per [testare la destinazione basata su file con profili di esempio](../testing-api/batch-destinations/file-based-destination-testing-api.md).
   * Allega un file di esempio generato dalla destinazione ed esportato nel percorso di archiviazione.
   * Inviare una bozza che attesti che il file esportato è stato correttamente acquisito dal percorso di archiviazione nel sistema.
* Prova di aver inviato una richiesta di pubblicazione di destinazione per la tua destinazione utilizzando l&#39;[API di pubblicazione di destinazione](../publishing-api/create-publishing-request.md).
* Una PR (richiesta pull) alla documentazione, seguendo le istruzioni descritte nel [processo di documentazione self-service](../docs-framework/documentation-instructions.md).
* Un file di immagine che verrà visualizzato come logo per la scheda di destinazione nel catalogo delle destinazioni di Experience Platform.

Puoi trovare informazioni dettagliate su ciascun elemento nelle sezioni seguenti:

## Descrizione del caso d’uso {#use-case-description}

Fornisci una descrizione dei casi d’uso che la tua destinazione risolve per i clienti Experience Platform. Le descrizioni possono essere simili ai casi d’uso dei partner esistenti:

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md): crea tipi di pubblico dai tuoi elenchi di clienti, da persone che hanno visitato il tuo sito o che hanno già interagito con il tuo contenuto su Pinterest.
* [Dati Yahoo X](/help/destinations/catalog/advertising/datax.md#use-cases): le API DataX sono disponibili per gli inserzionisti che desiderano indirizzare un gruppo di pubblico specifico ricavato dagli indirizzi e-mail in Verizon Media (VMG) possono creare rapidamente un nuovo pubblico e inviare un messaggio push al gruppo di pubblico desiderato utilizzando l&#39;API quasi in tempo reale di VMG.

## Motivo dell’aggiornamento {#reason-for-update}

>[!NOTE]
>
>Questa sezione è necessaria solo quando si aggiorna una configurazione esistente.

Fornisci una breve descrizione del problema che l’invio risolve per la destinazione esistente. Ad esempio, l’invio potrebbe aggiornare il nome, la descrizione e il logo della destinazione nel passaggio dalla versione beta a quella di disponibilità generale. In alternativa, l’invio potrebbe correggere un bug rilevato nella configurazione di destinazione.

## Risultati del test dopo l’utilizzo dell’API di destinazione del test {#testing-api-response}

Fornisci i risultati del test dopo aver utilizzato l&#39;endpoint [API](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) di destinazione del test per eseguire una chiamata HTTP alla destinazione. Ciò include:

* La richiesta API completa (intestazioni e corpo) effettuata all&#39;endpoint di destinazione, utilizzando l&#39;API di test.
* Risposta API ricevuta dall&#39;endpoint di destinazione.

Ad esempio, la richiesta e la risposta potrebbero essere simili agli esempi seguenti:

**Richiesta**

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

## Requisiti aggiuntivi per le destinazioni basate su file {#additional-file-based-destination-requirements}

Per le destinazioni basate su file, devi fornire un’ulteriore prova della corretta configurazione della destinazione. Assicurati di includere gli elementi seguenti:

### Verifica della risposta API {#testing-api-response-file-based}

Includi una richiesta e un esempio di risposta dopo aver utilizzato l&#39;API di test per [testare la destinazione basata su file con profili di esempio](../testing-api/batch-destinations/file-based-destination-testing-api.md).

### Allega file esportato {#attach-exported-file}

Nell&#39;[e-mail di invio](#download-sample-email), allega un file CSV esportato nel percorso di archiviazione dalla destinazione configurata.

### Prova della corretta acquisizione {#proof-of-successful-ingestion}

Infine, devi fornire una prova che i dati siano stati correttamente acquisiti nel sistema dopo essere stati esportati nel percorso di archiviazione fornito. Fornisci uno dei seguenti elementi:

* Screenshot o un breve video di cattura in cui il file viene prelevato manualmente dal percorso di archiviazione e caricato nel sistema.
* Screenshot o un breve video di screencapture in cui l’interfaccia utente del sistema conferma che il nome del file generato da Experience Platform è stato correttamente acquisito nel sistema.
* Righe di registro dal sistema che Adobe può correlare al nome del file o ai dati generati da Experience Platform.

## Prova di aver inviato una richiesta di pubblicazione di destinazione {#destination-publishing-request-proof}

Dopo aver testato correttamente la destinazione, devi utilizzare l&#39;[API di pubblicazione della destinazione](../publishing-api/create-publishing-request.md) per inviare la destinazione ad Adobe per la revisione e la pubblicazione.

Immetti l’ID della richiesta di pubblicazione per la destinazione. Per informazioni su come recuperare l&#39;ID della richiesta di pubblicazione, leggi come [recuperare le richieste di pubblicazione di destinazione](../publishing-api/retrieve-publishing-request.md).

## Documentazione di destinazione PR (richiesta pull) per le integrazioni prodotte {#documentation-pr}

Se sei un fornitore di software indipendente (ISV) o un integratore di sistemi (SI) che crea una [integrazione prodotta](../overview.md#productized-custom-integrations), devi utilizzare il [processo di documentazione self-service](../docs-framework/documentation-instructions.md) per creare una pagina di documentazione del prodotto per la tua destinazione. Come parte del processo di invio, fornisci la richiesta di pull (PR) per la documentazione di destinazione.

## Logo per la destinazione {#logo}

Il catalogo delle destinazioni include un logo per ogni scheda di destinazione. Nell’e-mail inviata, includi un’immagine con il logo della tua destinazione.

I requisiti dell&#39;immagine sono:
* **Formato**: `SVG`
* **Dimensioni**: meno di 2 MB

## Scarica e-mail di esempio {#download-sample-email}

[Scarica](../assets/guides/sample-email-submit-destination.rtf) un&#39;e-mail di esempio con tutte le informazioni necessarie da fornire ad Adobe.
