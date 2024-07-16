---
description: Questa pagina elenca e descrive i passaggi necessari per configurare una destinazione basata su file utilizzando Destination SDK.
title: Utilizzare Destination SDK per configurare una destinazione basata su file
exl-id: 84d73452-88e4-4e0f-8fc7-d0d8e10f9ff5
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 1%

---

# Utilizzare Destination SDK per configurare una destinazione basata su file

## Panoramica {#overview}

In questa pagina viene descritto come utilizzare le informazioni in [Opzioni di configurazione nell&#39;SDK delle destinazioni](../functionality/configuration-options.md) e in altre funzionalità di Destination SDK e documenti di riferimento API per configurare una [destinazione basata su file](../../destination-types.md#file-based). I passaggi sono disposti in ordine sequenziale di seguito.

## Prerequisiti {#prerequisites}

Prima di passare ai passaggi illustrati di seguito, leggere la pagina della [guida introduttiva](../getting-started.md) di Destination SDK per informazioni su come ottenere le credenziali di autenticazione Adobe I/O necessarie e altri prerequisiti per l&#39;utilizzo delle API Destination SDK.

## Passaggi per utilizzare le opzioni di configurazione in Destination SDK per impostare la destinazione {#steps}

![Passaggi illustrati per l&#39;utilizzo degli endpoint Destination SDK](../assets/guides/destination-sdk-steps-batch.png)

## Passaggio 1: creare una configurazione di server e file {#create-server-file-configuration}

Iniziare [creando una configurazione di file e server](../authoring-api/destination-server/create-destination-server.md) utilizzando l&#39;endpoint `/destinations-server`.

Di seguito è riportata una configurazione di esempio per una destinazione [!DNL Amazon S3]. Per ulteriori dettagli sui campi utilizzati nella configurazione e per configurare altri tipi di destinazioni basate su file, vedere le [configurazioni server corrispondenti](../functionality/destination-server/server-specs.md).

**Formato API**

```shell
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucketName}}"
        },
        "path": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.path}}"
        }
    },
    "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

## Passaggio 2: creare la configurazione di destinazione {#create-destination-configuration}

Di seguito è riportato un esempio di configurazione di destinazione, creata utilizzando l&#39;endpoint API `/destinations`.

Per connettere la configurazione del server e del file dal passaggio 1 a questa configurazione di destinazione, aggiungere `instance ID` della configurazione del server e del file come `destinationServerId` qui.

**Formato API**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json {line-numbers="true" highlight="83"}
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucketName",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "compression",
            "title": "Select compression type",
            "description": "Select the file compression type used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "enum": [
                "GZIP",
                "NONE",
                "bzip2",
                "lz4",
                "snappy",
                "deflate"
            ]
        },
        {
            "name": "fileType",
            "title": "Select a file format",
            "description": "Select the file format to be used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false,
            "enum": [
                "csv",
                "json",
                "parquet"
            ],
            "default": "csv"
        }
    ],
    "uiAttributes": {
        "documentationLink": "https://www.adobe.com/go/destinations-YOURDESTINATION-en",
        "category": "S3",
        "connectionType": "S3",
        "flowRunsSupported": true,
        "monitoringSupported": true,
        "frequency": "Batch"
    },
    "destinationDelivery": [
        {
            "deliveryMatchers": [
                {
                    "type": "SOURCE",
                    "value": [
                        "batch"
                    ]
                }
            ],
            "authenticationRule": "CUSTOMER_AUTHENTICATION",
            "destinationServerId": "eec25bde-4f56-4c02-a830-9aa9ec73ee9d"
        }
    ],
    "schemaConfig": {
        "profileRequired": true,
        "segmentRequired": true,
        "identityRequired": true
    },
    "batchConfig": {
        "allowMandatoryFieldSelection": true,
        "allowDedupeKeyFieldSelection": true,
        "defaultExportMode": "DAILY_FULL_EXPORT",
        "allowedExportMode": [
            "DAILY_FULL_EXPORT",
            "FIRST_FULL_THEN_INCREMENTAL"
        ],
        "allowedScheduleFrequency": [
            "DAILY",
            "EVERY_3_HOURS",
            "EVERY_6_HOURS",
            "EVERY_8_HOURS",
            "EVERY_12_HOURS",
            "ONCE"
        ],
        "defaultFrequency": "DAILY",
        "defaultStartTime": "00:00",
       "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      }
    },
    "backfillHistoricalProfileData": true
}
```

## Passaggio 3: creare la configurazione dei metadati del pubblico {#create-audience-metadata-configuration}

Per alcune destinazioni, Destination SDK richiede la configurazione di una configurazione di metadati di pubblico per creare, aggiornare o eliminare in modo programmatico i tipi di pubblico nella destinazione. Consulta [Gestione dei metadati del pubblico](../functionality/audience-metadata-management.md) per informazioni su quando devi configurare questa configurazione e su come farlo.

Se utilizzi una configurazione di metadati di pubblico, devi collegarla alla configurazione di destinazione creata nel passaggio 2. Aggiungi l&#39;ID istanza della configurazione dei metadati del pubblico alla configurazione di destinazione come `audienceTemplateId`.

```json {line-numbers="true" highlight="90"}
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucketName",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "compression",
            "title": "Select compression type",
            "description": "Select the file compression type used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "enum": [
                "GZIP",
                "NONE",
                "bzip2",
                "lz4",
                "snappy",
                "deflate"
            ]
        },
        {
            "name": "fileType",
            "title": "Select a file format",
            "description": "Select the file format to be used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false,
            "enum": [
                "csv",
                "json",
                "parquet"
            ],
            "default": "csv"
        }
    ],
    "uiAttributes": {
        "documentationLink": "http://www.adobe.com/go/destinations-YOURDESTINATION-en",
        "category": "S3",
        "connectionType": "S3",
        "flowRunsSupported": true,
        "monitoringSupported": true,
        "frequency": "Batch"
    },
    "destinationDelivery": [
        {
            "deliveryMatchers": [
                {
                    "type": "SOURCE",
                    "value": [
                        "batch"
                    ]
                }
            ],
            "authenticationRule": "CUSTOMER_AUTHENTICATION",
            "destinationServerId": "eec25bde-4f56-4c02-a830-9aa9ec73ee9d"
        }
    ],
    "audienceMetadataConfig":{
    "mapExperiencePlatformSegmentName":false,
    "mapExperiencePlatformSegmentId":false,
    "mapUserInput":false,
    "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
    },   
    "schemaConfig": {
        "profileRequired": true,
        "segmentRequired": true,
        "identityRequired": true
    },
    "batchConfig": {
        "allowMandatoryFieldSelection": true,
        "allowDedupeKeyFieldSelection": true,
        "defaultExportMode": "DAILY_FULL_EXPORT",
        "allowedExportMode": [
            "DAILY_FULL_EXPORT",
            "FIRST_FULL_THEN_INCREMENTAL"
        ],
        "allowedScheduleFrequency": [
            "DAILY",
            "EVERY_3_HOURS",
            "EVERY_6_HOURS",
            "EVERY_8_HOURS",
            "EVERY_12_HOURS",
            "ONCE"
        ],
        "defaultFrequency": "DAILY",
        "defaultStartTime": "00:00",
       "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      }
    },
    "backfillHistoricalProfileData": true
}
```

## Passaggio 4: configurare l’autenticazione {#set-up-authentication}

A seconda che si specifichi `"authenticationRule": "CUSTOMER_AUTHENTICATION"` o `"authenticationRule": "PLATFORM_AUTHENTICATION"` nella configurazione di destinazione precedente, è possibile impostare l&#39;autenticazione per la destinazione utilizzando l&#39;endpoint `/destination` o `/credentials`.

>[!NOTE]
>
>`CUSTOMER_AUTHENTICATION` è la più comune delle due regole di autenticazione ed è quella da utilizzare se si richiede agli utenti di fornire una forma di autenticazione alla destinazione prima di poter impostare una connessione ed esportare dati.

* Se hai selezionato `"authenticationRule": "CUSTOMER_AUTHENTICATION"` nella configurazione di destinazione, consulta le sezioni seguenti per i tipi di autenticazione supportati da Destination SDK per le destinazioni basate su file:

   * [Autenticazione Amazon S3](../functionality/destination-configuration/customer-authentication.md#s3)
   * [BLOB di Azure](../functionality/destination-configuration/customer-authentication.md#blob)
   * [Archiviazione Azure Data Lake](../functionality/destination-configuration/customer-authentication.md#adls)
   * [Google Cloud Storage](../functionality/destination-configuration/customer-authentication.md#gcs)
   * [Autenticazione SFTP con chiave SSH](../functionality/destination-configuration/customer-authentication.md#sftp-ssh)
   * [Autenticazione SFTP con password](../functionality/destination-configuration/customer-authentication.md#sftp-password)

* Se hai selezionato `"authenticationRule": "PLATFORM_AUTHENTICATION"`, consulta la [documentazione API per la configurazione delle credenziali](../credentials-api/create-credential-configuration.md#when-to-use).


## Passaggio 5: testare la destinazione {#test-destination}

Dopo aver configurato la destinazione utilizzando gli endpoint di configurazione nei passaggi precedenti, puoi utilizzare lo [strumento di test della destinazione](../testing-api/batch-destinations/file-based-destination-testing-overview.md) per testare l&#39;integrazione tra Adobe Experience Platform e la destinazione.

Come parte del processo di test della destinazione, devi utilizzare l’interfaccia utente di Experience Platform per creare tipi di pubblico, che attiverai nella destinazione. Per istruzioni su come creare un pubblico in Experience Platform, consulta le due risorse seguenti:

* [Creare un pubblico - pagina della documentazione](/help/segmentation/ui/audience-portal.md#create-audience)
* [Creare un pubblico - procedura dettagliata per i video](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)

## Passaggio 6: Publish la tua destinazione {#publish-destination}

>[!NOTE]
>
>Questo passaggio non è necessario se stai creando una destinazione privata per il tuo utilizzo e non stai cercando di pubblicarla nel catalogo delle destinazioni affinché altri clienti la possano utilizzare.

Dopo aver configurato e testato la destinazione, utilizza l&#39;[API di pubblicazione della destinazione](../publishing-api/create-publishing-request.md) per inviare la configurazione ad Adobe per la revisione.

## Passaggio 7: documentare la destinazione {#document-destination}

>[!NOTE]
>
>Questo passaggio non è necessario se stai creando una destinazione privata per il tuo utilizzo e non stai cercando di pubblicarla nel catalogo delle destinazioni affinché altri clienti la possano utilizzare.

Se sei un fornitore di software indipendente (ISV) o un integratore di sistemi (SI) che sta creando una [integrazione prodotta](../overview.md#productized-custom-integrations), utilizza la [procedura di documentazione self-service](../docs-framework/documentation-instructions.md) per creare una pagina di documentazione del prodotto per la tua destinazione nel [catalogo delle destinazioni di Experience Platform](/help/destinations/catalog/overview.md).

## Passaggio 8: invia la destinazione per la revisione di Adobe {#submit-for-review}

>[!NOTE]
>
>Questo passaggio non è necessario se stai creando una destinazione privata per il tuo utilizzo e non stai cercando di pubblicarla nel catalogo delle destinazioni affinché altri clienti la possano utilizzare.

Infine, prima che la destinazione possa essere pubblicata nel catalogo di Experienci Platform e visibile a tutti i clienti di Experienci Platform, devi inviare ufficialmente la destinazione per la revisione di Adobi. Trova informazioni complete su come [inviare per la revisione una destinazione prodotta creata in Destination SDK](../guides/submit-destination.md).
