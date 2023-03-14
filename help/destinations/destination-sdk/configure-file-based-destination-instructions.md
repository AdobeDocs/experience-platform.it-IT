---
description: Questa pagina elenca e descrive i passaggi necessari per configurare una destinazione basata su file utilizzando Destination SDK.
title: Utilizzare Destination SDK per configurare una destinazione basata su file
exl-id: 84d73452-88e4-4e0f-8fc7-d0d8e10f9ff5
source-git-commit: 04e4b0f6b6d84d04d0a24a462383420ebd9a2daf
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# Utilizzare Destination SDK per configurare una destinazione basata su file

## Panoramica {#overview}

Questa pagina descrive come utilizzare le informazioni in [Opzioni di configurazione nell’SDK delle destinazioni](./configuration-options.md) e in altri documenti di riferimento API e funzionalità Destination SDK per configurare un [destinazione basata su file](../../destinations/destination-types.md#file-based). I passaggi sono disposti in ordine sequenziale di seguito.

## Prerequisiti {#prerequisites}

Prima di procedere con i passaggi illustrati di seguito, leggere la [Destination SDK introduzione](./getting-started.md) per informazioni su come ottenere le credenziali di autenticazione Adobe I/O necessarie e altri prerequisiti per lavorare con le API Destination SDK.

## Passaggi per utilizzare le opzioni di configurazione in Destination SDK per impostare la destinazione {#steps}

![Passaggi illustrati per l’utilizzo degli endpoint Destination SDK](./assets/destination-sdk-steps-batch.png)

## Passaggio 1: creare una configurazione di server e file {#create-server-file-configuration}

Per iniziare, crea un server e una configurazione di file utilizzando `/destinations-server` endpoint (lettura [Riferimento API](./destination-server-api.md)).

Di seguito è riportato un esempio di configurazione per un [!DNL Amazon S3] destinazione. Per configurare altri tipi di destinazioni basate su file, vedi le corrispondenti [configurazioni server](server-and-file-configuration.md).

**Formato API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucketName": {
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

Di seguito è riportato un esempio di configurazione di destinazione, creata utilizzando `/destinations` Endpoint API Per ulteriori informazioni su questa configurazione, consulta [Configurazione della destinazione](./file-based-destination-configuration.md).

Per connettere il server e la configurazione file nel passaggio 1 a questa configurazione di destinazione, aggiungi l’ID istanza del server e la configurazione modello come `destinationServerId` qui.

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

## Passaggio 3: creare la configurazione dei metadati del pubblico {#create-audience-metadata-configuration}

Per alcune destinazioni, Destination SDK richiede la configurazione di una configurazione di metadati di pubblico per creare, aggiornare o eliminare in modo programmatico i tipi di pubblico nella destinazione. Fai riferimento a [Gestione dei metadati del pubblico](./audience-metadata-management.md) per informazioni su quando è necessario impostare questa configurazione e su come eseguire questa operazione.

Se utilizzi una configurazione di metadati di pubblico, devi collegarla alla configurazione di destinazione creata nel passaggio 2. Aggiungi l&#39;ID istanza della configurazione dei metadati del pubblico alla configurazione di destinazione come `audienceTemplateId`.

## Passaggio 4: configurare l’autenticazione {#set-up-authentication}

A seconda che tu specifichi `"authenticationRule": "CUSTOMER_AUTHENTICATION"` o `"authenticationRule": "PLATFORM_AUTHENTICATION"` nella configurazione di destinazione precedente, puoi impostare l&#39;autenticazione per la destinazione utilizzando `/destination` o `/credentials` endpoint.

* Se hai selezionato `"authenticationRule": "CUSTOMER_AUTHENTICATION"` nella configurazione di destinazione, consulta le sezioni seguenti per i tipi di autenticazione supportati da Destination SDK per le destinazioni basate su file:

   * [Autenticazione Amazon S3](authentication-configuration.md#s3)
   * [BLOB di Azure](authentication-configuration.md#blob)
   * [Archiviazione Azure Data Lake](authentication-configuration.md#adls)
   * [Archiviazione cloud Google](authentication-configuration.md#gcs)
   * [Autenticazione SFTP con chiave SSH](authentication-configuration.md#sftp-ssh)
   * [Autenticazione SFTP con password](authentication-configuration.md#sftp-password)

* Se hai selezionato `"authenticationRule": "PLATFORM_AUTHENTICATION"`, fare riferimento a [Configurazione dell’autenticazione](./authentication-configuration.md#when-to-use).


## Passaggio 5: testare la destinazione {#test-destination}

Dopo aver impostato la destinazione utilizzando gli endpoint di configurazione nei passaggi precedenti, puoi utilizzare [strumento di test di destinazione](./file-based-destination-testing-overview.md) per testare l’integrazione tra Adobe Experience Platform e la tua destinazione.

Come parte del processo di test della destinazione, devi utilizzare l’interfaccia utente di Experience Platform per creare i segmenti, che attiverai nella destinazione. Per istruzioni su come creare segmenti in Experience Platform, consulta le due risorse seguenti:

* [Creare una pagina di documentazione del segmento](/help/segmentation/ui/overview.md#create-segment)
* [Procedura dettagliata sulla creazione di un video segmento](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## Passaggio 6: pubblicare la destinazione {#publish-destination}

>[!NOTE]
>
>Questo passaggio non è necessario se stai creando una destinazione privata per il tuo utilizzo e non stai cercando di pubblicarla nel catalogo delle destinazioni affinché altri clienti la possano utilizzare.

Dopo aver configurato e testato la destinazione, utilizza [API di pubblicazione della destinazione](./destination-publish-api.md) per inviare la configurazione all&#39;Adobe per la revisione.

## Passaggio 7: documentare la destinazione {#document-destination}

>[!NOTE]
>
>Questo passaggio non è necessario se stai creando una destinazione privata per il tuo utilizzo e non stai cercando di pubblicarla nel catalogo delle destinazioni affinché altri clienti la possano utilizzare.

Se si è un fornitore di software indipendente (ISV) o un integratore di sistemi (SI) che crea un [integrazione di produzione](./overview.md#productized-custom-integrations), utilizza [processo di documentazione self-service](./docs-framework/documentation-instructions.md) per creare una pagina di documentazione del prodotto per la destinazione in [catalogo delle destinazioni di Experience Platform](/help/destinations/catalog/overview.md).

## Passaggio 8: invia la destinazione per la revisione di Adobe {#submit-for-review}

>[!NOTE]
>
>Questo passaggio non è necessario se stai creando una destinazione privata per il tuo utilizzo e non stai cercando di pubblicarla nel catalogo delle destinazioni affinché altri clienti la possano utilizzare.

Infine, prima che la destinazione possa essere pubblicata nel catalogo di Experienci Platform e visibile a tutti i clienti di Experienci Platform, devi inviare ufficialmente la destinazione per la revisione di Adobi. Informazioni complete su come [invia per la revisione una destinazione prodotta creata con Destination SDK](/help/destinations/destination-sdk/submit-destination.md).
