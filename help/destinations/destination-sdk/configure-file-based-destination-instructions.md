---
description: Questa pagina elenca e descrive i passaggi necessari per configurare una destinazione basata su file utilizzando Destination SDK.
title: Utilizzare Destination SDK per configurare una destinazione basata su file
exl-id: 84d73452-88e4-4e0f-8fc7-d0d8e10f9ff5
source-git-commit: 557db5b7eefdd7902895e428f7bc34e3ad8a6f58
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Utilizzare Destination SDK per configurare una destinazione basata su file

## Panoramica {#overview}

>[!IMPORTANT]
>
>La funzionalità per configurare e inviare destinazioni basate su file tramite Adobe Experience Platform Destination SDK è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

Questa pagina descrive come utilizzare le informazioni in [Opzioni di configurazione nell’SDK delle destinazioni](./configuration-options.md) e in altri documenti di riferimento sulle funzionalità di Destination SDK e API per configurare un [destinazione basata su file](../../destinations/destination-types.md#file-based). I passaggi sono disposti in ordine sequenziale di seguito.

## Prerequisiti {#prerequisites}

Prima di passare ai passaggi illustrati di seguito, leggere il [Guida introduttiva alla Destination SDK](./getting-started.md) per informazioni su come ottenere le credenziali di autenticazione necessarie per l’Adobe I/O e altri prerequisiti per l’utilizzo con le API Destination SDK.

## Passaggi per utilizzare le opzioni di configurazione in Destination SDK per impostare la destinazione {#steps}

![Passaggi illustrativi dell’utilizzo degli endpoint Destination SDK](./assets/destination-sdk-steps-batch.png)

## Passaggio 1: Creare una configurazione del server e del file {#create-server-file-configuration}

Per iniziare, crea un server e una configurazione di file utilizzando `/destinations-server` endpoint (lettura [Riferimento API](./destination-server-api.md)).

Di seguito è riportato un esempio di configurazione per un [!DNL Amazon S3] destinazione. Per configurare altri tipi di destinazioni basate su file, consulta le relative [configurazioni del server](server-and-file-configuration.md).

**Formato API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucket}}"
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

## Passaggio 2: Creare la configurazione di destinazione {#create-destination-configuration}

Di seguito è riportato un esempio di configurazione di destinazione, creata utilizzando `/destinations` Endpoint API. Per ulteriori informazioni su questa configurazione, consulta [Configurazione della destinazione](./file-based-destination-configuration.md).

Per collegare il server e la configurazione del file nel passaggio 1 a questa configurazione di destinazione, aggiungi l&#39;ID istanza del server e la configurazione del modello come `destinationServerId` qui.

**Formato API**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "releaseNotes": "Test",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucket",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[A-Za-z]+$",
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
        "documentationLink": "https://www.adobe.io/apis/experienceplatform.html",
        "category": "S3",
        "iconUrl": "https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
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
        "defaultStartTime": "00:00"
    },
    "backfillHistoricalProfileData": true
}
```

## Passaggio 3: Creare la configurazione dei metadati del pubblico {#create-audience-metadata-configuration}

Per alcune destinazioni, Destination SDK richiede di configurare una configurazione di metadati del pubblico per creare, aggiornare o eliminare in modo programmatico i tipi di pubblico nella destinazione. Fai riferimento a [Gestione dei metadati del pubblico](./audience-metadata-management.md) per informazioni su quando è necessario configurare questa configurazione e su come eseguirla.

Se utilizzi una configurazione di metadati del pubblico, devi connetterla alla configurazione di destinazione creata nel passaggio 2. Aggiungi l&#39;ID istanza della configurazione dei metadati del pubblico alla configurazione di destinazione come `audienceTemplateId`.

## Passaggio 4: Configurare l’autenticazione {#set-up-authentication}

A seconda se si specifica `"authenticationRule": "CUSTOMER_AUTHENTICATION"` o `"authenticationRule": "PLATFORM_AUTHENTICATION"` nella configurazione di destinazione di cui sopra, puoi impostare l’autenticazione per la tua destinazione utilizzando `/destination` o `/credentials` punto finale.

* Se hai selezionato `"authenticationRule": "CUSTOMER_AUTHENTICATION"` nella configurazione di destinazione, consulta le sezioni seguenti per i tipi di autenticazione supportati da Destination SDK per le destinazioni basate su file:

   * [Autenticazione Amazon S3](authentication-configuration.md#s3)
   * [BLOB di Azure](authentication-configuration.md#blob)
   * [Archiviazione Data Lake di Azure](authentication-configuration.md#adls)
   * [Google Cloud Storage](authentication-configuration.md#gcs)
   * [Autenticazione SFTP con chiave SSH](authentication-configuration.md#sftp-ssh)
   * [Autenticazione SFTP con password](authentication-configuration.md#sftp-password)

* Se hai selezionato `"authenticationRule": "PLATFORM_AUTHENTICATION"`, fare riferimento alla [Configurazione dell’autenticazione](./authentication-configuration.md#when-to-use).


<!-- ## Step 5: Test your destination {#test-destination}

After setting up your destination using the configuration endpoints in the previous steps, you can use the [destination testing tool](./create-template.md) to test the integration between Adobe Experience Platform and your destination.

As part of the process to test your destination, you must use the Experience Platform UI to create segments, which you will activate to your destination. Refer to the two resources below for instructions how to create segments in Experience Platform:

* [Create a segment documentation page](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Create a segment video walkthrough](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) -->

## Passaggio 5: Pubblicare la destinazione {#publish-destination}

>[!NOTE]
>
>Questo passaggio non è necessario se crei una destinazione privata per tuo uso e non desideri pubblicarla nel catalogo delle destinazioni affinché altri clienti possano utilizzarla.

Dopo aver configurato e testato la destinazione, utilizza il [API di pubblicazione della destinazione](./destination-publish-api.md) per inviare la configurazione ad Adobe per la revisione.

## Passaggio 6: Documentare la destinazione {#document-destination}

>[!NOTE]
>
>Questo passaggio non è necessario se crei una destinazione privata per tuo uso e non desideri pubblicarla nel catalogo delle destinazioni affinché altri clienti possano utilizzarla.

Se sei un fornitore di software indipendente (ISV) o un integratore di sistema (SI) che crea un [integrazione di prodotti](./overview.md#productized-custom-integrations), utilizza [processo di documentazione self-service](./docs-framework/documentation-instructions.md) per creare una pagina di documentazione del prodotto per la destinazione in [Catalogo delle destinazioni di Experience Platform](/help/destinations/catalog/overview.md).
