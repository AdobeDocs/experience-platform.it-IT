---
description: Scopri come utilizzare Destination SDK per configurare una destinazione DLZ (Data Landing Zone) con opzioni di formattazione dei file personalizzate e configurazione del nome file personalizzato.
title: Configura una destinazione DLZ (Data Landing Zone) con opzioni di formattazione dei file personalizzate e configurazione del nome file personalizzato.
exl-id: 3a5c1188-c2b5-4e81-ae41-9fff797f08a6
source-git-commit: 557db5b7eefdd7902895e428f7bc34e3ad8a6f58
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Configura un [!DNL Data Landing Zone (DLZ)] destinazione con opzioni di formattazione file personalizzate e configurazione del nome file personalizzato

## Panoramica {#overview}

>[!IMPORTANT]
>
>La funzionalità per configurare destinazioni basate su file utilizzando Adobe Experience Platform Destination SDK è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

Questa pagina descrive come utilizzare Destination SDK per configurare un [!DNL Data Landing Zone] destinazione con personalizzato [opzioni di formattazione dei file](../../server-and-file-configuration.md#file-configuration) e una [configurazione del nome file](../../file-based-destination-configuration.md#file-name-configuration).

Questa pagina mostra tutte le opzioni di configurazione disponibili per [!DNL Data Landing Zone] destinazioni. Puoi modificare le configurazioni mostrate nei passaggi seguenti o eliminare alcune parti delle configurazioni, in base alle esigenze.

## Prerequisiti {#prerequisites}

Prima di passare ai passaggi descritti di seguito, leggere il [Guida introduttiva alla Destination SDK](../../getting-started.md) per informazioni su come ottenere le credenziali di autenticazione necessarie per l’Adobe I/O e altri prerequisiti per l’utilizzo con le API Destination SDK.

## Passaggio 1: Creare una configurazione del server e del file {#create-server-file-configuration}

Inizia utilizzando `/destination-server` per creare un server e una configurazione di file. Per descrizioni dettagliate dei parametri nella richiesta HTTP, leggi la [specifiche di configurazione del server e dei file per le destinazioni basate su file](../../server-and-file-configuration.md#adls-example) e i [configurazioni di formattazione dei file](../../server-and-file-configuration.md#file-configuration).

**Formato API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Richiesta**

La richiesta seguente crea una nuova configurazione del server di destinazione, configurata dai parametri forniti nel payload.
Il payload seguente include un [!DNL Data Landing Zone] configurazione, con [Formattazione file CSV](../../server-and-file-configuration.md#file-configuration) parametri di configurazione che gli utenti possono definire nell’interfaccia utente di Experience Platform.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
 -d '
{
   "name":"DLZ Destination Server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "fileConfigurations":{
         "compression":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.compression}}"
         },
         "fileType":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.fileType}}"
         },
         "csvOptions":{
            "sep":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.sep}}"
            },
            "encoding":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.encoding}}"
            },
            "quote":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.quote}}"
            },
            "quoteAll":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.quoteAll}}"
            },
            "escape":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.escape}}"
            },
            "escapeQuotes":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.escapeQuotes}}"
            },
            "header":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.header}}"
            },
            "ignoreLeadingWhiteSpace":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.ignoreLeadingWhiteSpace}}"
            },
            "nullValue":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.nullValue}}"
            },
            "dateFormat":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.dateFormat}}"
            },
            "charToEscapeQuoteEscaping":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.charToEscapeQuoteEscaping}}"
            },
            "emptyValue":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.dateFormat}}"
            }
         }
      }
   }
}'
```

Una risposta corretta restituisce la nuova configurazione del server di destinazione, incluso l&#39;identificatore univoco (`instanceId`) della configurazione. Memorizza questo valore come necessario nel passaggio successivo.

## Passaggio 2: Creare la configurazione di destinazione {#create-destination-configuration}

Dopo aver creato il server di destinazione e la configurazione di formattazione del file nel passaggio precedente, puoi ora utilizzare il `/destinations` Endpoint API per creare una configurazione di destinazione.

Per collegare la configurazione del server in [passaggio 1](#create-server-file-configuration) in questa configurazione di destinazione, sostituisci il `destinationServerId` nella richiesta API seguente con il valore ottenuto durante la creazione del server di destinazione in [passaggio 1](#create-server-file-configuration).

Per una descrizione dettagliata dei parametri utilizzati di seguito, consulta le pagine seguenti:

* [Configurazione dell’autenticazione](../../authentication-configuration.md#adls)
* [Configurazione della destinazione batch](../../file-based-destination-configuration.md#batch-configuration)
* [Operazioni API per la configurazione della destinazione basata su file](../../destination-configuration-api.md#create-file-based)

**Formato API**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"DLZ Destination",
   "description":"SSD DLZ Destination",
   "releaseNotes":"Test release notes for DLZ Destination",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
       
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"path",
         "title":"Folder path",
         "description":"Enter the path to your Data Landing Zone folder",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter your desired separator for each field and value",
         "description":"Enter your desired separator for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Select the desired CSV file encoding",
         "description":"Select the desired CSV file encoding",
         "type":"string",
         "enum":[
            "UTF-8",
            "UTF-16"
         ],
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quote",
         "title":"Quoted values escape character",
         "description":"Enter the desired character to be used for escaping quoted values.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values.",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "default":"true",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escape",
         "title":"Quote escaping character",
         "description":"Enter the desired character to be used for escaping quotes inside an already quoted value.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Enclose quoted values within quotes",
         "description":"Select whether values containing quotes should always be enclosed in quotes.",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "isRequired":false,
         "default":"true",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"header",
         "title":"Generate file header.",
         "description":"Select whether to write the names of columns as the first line of the exported files.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"ignoreLeadingWhiteSpace",
         "title":"Ignore leading white space",
         "description":"Select whether leading whitespaces should be trimmed from exported values.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"nullValue",
         "title":"NULL value string format",
         "description":"Enter the string representation of a NULL value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Enter the desired date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Quote escaping escape character",
         "description":"Enter the desired character to be used for escaping the escaping of a quote character.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Empty value string format",
         "description":"Enter the string representation of an empty value.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
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
      "documentationLink":"https://www.adobe.io/apis/experienceplatform.html",
      "category":"DLZ",
      "connectionType":"Server-to-server",
      "frequency":"Batch",
      "flowRunsSupported":true,
      "monitoringSupported":true
   },
   "identityNamespaces":{
      "adobe_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "mobile_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false
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
         "authenticationRule":"NONE",
         "destinationServerId":"{{instanceID of your destination server}}"
      }
   ],
   "schemaConfig":{
      "profileRequired":true,
      "identityRequired":true,
      "segmentRequired":true
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "autoSelectJoinKeyOnPartnerSchemaSelection":false,
      "joinKeyTitle":"DEDUPLICATION KEY",
      "defaultExportMode":"DAILY_FULL_EXPORT",
      "allowedExportModes":[
         "DAILY_FULL_EXPORT",
         "FIRST_FULL_THEN_INCREMENTAL"
      ],
      "allowedScheduleFrequency":[
         "DAILY",
         "EVERY_3_HOURS",
         "EVERY_6_HOURS",
         "EVERY_12_HOURS",
         "EVERY_8_HOURS",
         "ONCE",
         "EVERY_HOUR"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
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
      },
      "allowDedupKeyFieldSelection":true
   },
   "backfillHistoricalProfileData":true
}'
```

Una risposta corretta restituisce la nuova configurazione di destinazione, incluso l&#39;identificatore univoco (`instanceId`) della configurazione. Memorizza questo valore come necessario se devi effettuare ulteriori richieste HTTP per aggiornare la configurazione di destinazione.

## Passaggio 3: Verificare l’interfaccia utente di Experience Platform {#verify-ui}

In base alle configurazioni di cui sopra, il catalogo di Experience Platform mostrerà ora una nuova scheda di destinazione privata da utilizzare.

![Registrazione su schermo che mostra la pagina del catalogo delle destinazioni con una scheda di destinazione selezionata.](../../assets/dlz-destination-card.gif)

Nelle immagini e nelle registrazioni seguenti, tieni presente come le opzioni nel [flusso di lavoro di attivazione per destinazioni basate su file](/help/destinations/ui/activate-batch-profile-destinations.md) corrispondono alle opzioni selezionate nella configurazione di destinazione.

Quando si compilano i dettagli sulla destinazione, notare come i campi visualizzati sono i campi dati personalizzati impostati nella configurazione.

>[!TIP]
>
>L’ordine in cui si aggiungono i campi dati personalizzati alla configurazione di destinazione non viene rispecchiato nell’interfaccia utente. I campi dati personalizzati vengono sempre visualizzati nell’ordine visualizzato nella schermata di registrazione sottostante.

![compila i dettagli della destinazione](../../assets/file-configuration-options.gif)

Quando pianifichi gli intervalli di esportazione, osserva come i campi visualizzati sono i campi impostati nella variabile `batchConfig` configurazione.
![opzioni di programmazione esportazione](../../assets/file-export-scheduling.png)

Quando visualizzi le opzioni di configurazione del nome file, osserva come i campi visualizzati rappresentano il `filenameConfig` opzioni configurate nella configurazione.
![opzioni di configurazione del nome file](../../assets/file-naming-options.gif)

Per regolare uno dei campi sopra menzionati, ripetere [step uno](#create-server-file-configuration) e [due](#create-destination-configuration) per modificare le configurazioni in base alle tue esigenze.

## Passaggio 4: (Facoltativo) Pubblica la destinazione {#publish-destination}

>[!NOTE]
>
>Questo passaggio non è necessario se crei una destinazione privata per tuo uso e non desideri pubblicarla nel catalogo delle destinazioni affinché altri clienti possano utilizzarla.

Dopo aver configurato la destinazione, utilizza la [API di pubblicazione della destinazione](../../destination-publish-api.md) per inviare la configurazione ad Adobe per la revisione.

## Passaggio 5: (Facoltativo) Documentare la destinazione {#document-destination}

>[!NOTE]
>
>Questo passaggio non è necessario se crei una destinazione privata per tuo uso e non desideri pubblicarla nel catalogo delle destinazioni affinché altri clienti possano utilizzarla.

Se sei un fornitore di software indipendente (ISV) o un integratore di sistema (SI) che crea un [integrazione di prodotti](../../overview.md#productized-custom-integrations), utilizza [processo di documentazione self-service](../../docs-framework/documentation-instructions.md) per creare una pagina di documentazione del prodotto per la destinazione in [Catalogo delle destinazioni di Experience Platform](../../../catalog/overview.md).

## Passaggi successivi {#next-steps}

Leggendo questo articolo, ora sai come creare un [!DNL Data Landing Zone] destinazione utilizzando la Destination SDK. Successivamente, il team può utilizzare [flusso di lavoro di attivazione per destinazioni basate su file](../../../ui/activate-batch-profile-destinations.md) per esportare i dati nella destinazione.
