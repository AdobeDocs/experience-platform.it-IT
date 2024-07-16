---
description: Questa pagina esemplifica la chiamata API utilizzata per aggiornare una configurazione di destinazione esistente tramite il Adobe Experience Platform Destination SDK.
title: Aggiornare una configurazione di destinazione
exl-id: d7f18689-9806-4f73-a63a-fa112569819c
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 2%

---

# Aggiornare una configurazione di destinazione

Questa pagina esemplifica la richiesta API e il payload che è possibile utilizzare per aggiornare una configurazione di destinazione esistente, utilizzando l&#39;endpoint API `/authoring/destinations`.

>[!TIP]
>
>Qualsiasi operazione di aggiornamento sulle destinazioni pubbliche/di produzione è visibile solo dopo aver utilizzato l&#39;[API di pubblicazione](../../publishing-api/create-publishing-request.md) e aver inviato l&#39;aggiornamento per una revisione di Adobe.

Per una descrizione dettagliata delle funzionalità di una configurazione di destinazione, leggi i seguenti articoli:

* [Configurazione autenticazione cliente](../../functionality/destination-configuration/customer-authentication.md)
* [Autorizzazione OAuth2](../../functionality/destination-configuration/oauth2-authorization.md)
* [Campi dati cliente](../../functionality/destination-configuration/customer-data-fields.md)
* [Attributi dell’interfaccia utente](../../functionality/destination-configuration/ui-attributes.md)
* [Configurazione dello schema](../../functionality/destination-configuration/schema-configuration.md)
* [Configurazione dello spazio dei nomi dell’identità](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [Consegna della destinazione](../../functionality/destination-configuration/destination-delivery.md)
* [Configurazione dei metadati del pubblico](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Configurazione dei metadati del pubblico](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Criterio di aggregazione](../../functionality/destination-configuration/aggregation-policy.md)
* [Configurazione batch](../../functionality/destination-configuration/batch-configuration.md)
* [Qualifiche del profilo storico](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API di configurazione di destinazione {#get-started}

Prima di continuare, consulta la [guida introduttiva](../../getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, tra cui come ottenere l&#39;autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Aggiornare una configurazione di destinazione {#update}

È possibile aggiornare una configurazione di destinazione [esistente](create-destination-configuration.md) effettuando una richiesta `PUT` all&#39;endpoint `/authoring/destinations` con il payload aggiornato.

>[!TIP]
>
>Endpoint API: `platform.adobe.io/data/core/activation/authoring/destinations`

Per ottenere una configurazione di destinazione esistente e i corrispondenti `{INSTANCE_ID}`, vedere l&#39;articolo relativo al [recupero di una configurazione di destinazione](retrieve-destination-configuration.md).

**Formato API**

```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID della configurazione di destinazione che desideri aggiornare. Per ottenere una configurazione di destinazione esistente e i corrispondenti `{INSTANCE_ID}`, vedere [Recuperare una configurazione di destinazione](retrieve-destination-configuration.md). |

+++Richiesta

La richiesta seguente aggiorna la destinazione creata in [questo esempio](create-destination-configuration.md#create) con diverse opzioni `filenameConfig`.

```shell {line-numbers="true" highlight="115-128"}
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Amazon S3 destination with predefined CSV formatting options",
   "description":"Amazon S3 destination with predefined CSV formatting options",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"bucket",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Compression format",
         "description":"Select the desired file compression format.",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "enum":[
            "SNAPPY",
            "GZIP",
            "DEFLATE",
            "NONE"
         ]
      },
      {
         "name":"fileType",
         "title":"File type",
         "description":"Select the exported file type.",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false,
         "enum":[
            "csv",
            "json",
            "parquet"
         ],
         "default":"csv"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-amazon-s3-en",
      "category":"cloudStorage",
      "icon":{
         "key":"amazonS3"
      },
      "connectionType":"S3",
      "frequency":"Batch"
   },
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ],
   "schemaConfig":{
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "allowDedupeKeyFieldSelection":true,
      "defaultExportMode":"DAILY_FULL_EXPORT",
      "allowedExportMode":[
         "DAILY_FULL_EXPORT",
         "FIRST_FULL_THEN_INCREMENTAL"
      ],
      "allowedScheduleFrequency":[
         "DAILY",
         "EVERY_3_HOURS",
         "EVERY_6_HOURS",
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%_%DESTINATION_INSTANCE_ID%,"
      },
      "backfillHistoricalProfileData":true
   }
}'
```

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione di destinazione aggiornata.

+++

## Gestione degli errori API {#error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](../../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, sai come aggiornare una configurazione di destinazione tramite l&#39;endpoint API Destination SDK `/authoring/destinations`.

Per ulteriori informazioni su cosa è possibile fare con questo endpoint, consulta i seguenti articoli:

* [Creare una configurazione di destinazione](create-destination-configuration.md)
* [Recuperare una configurazione di destinazione](retrieve-destination-configuration.md)
* [Eliminare una configurazione di destinazione](delete-destination-configuration.md)
