---
description: Scopri come utilizzare Destination SDK per configurare una destinazione di archiviazione BLOB di Azure con opzioni di formattazione del file personalizzate e configurazione del nome file personalizzato.
title: Configura una destinazione dell’archiviazione BLOB di Azure con opzioni di formattazione del file personalizzate e configurazione del nome file personalizzato.
exl-id: effbd218-3a7c-4986-9fba-f5727a21e480
source-git-commit: d47c82339afa602a9d6914c1dd36a4fc9528ea32
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 1%

---

# Configura una destinazione [!DNL Azure Blob Storage] con opzioni di formattazione del file personalizzate e configurazione del nome file personalizzato

## Panoramica {#overview}

In questa pagina viene descritto come utilizzare Destination SDK per configurare una destinazione [!DNL Azure Blob Storage] con [opzioni di formattazione file](configure-file-formatting-options.md) personalizzate e una [configurazione nome file](../../functionality/destination-configuration/batch-configuration.md#file-name-configuration) personalizzata.

Questa pagina mostra tutte le opzioni di configurazione disponibili per le destinazioni di archiviazione BLOB di Azure. Puoi modificare le configurazioni mostrate nei passaggi seguenti o eliminare alcune parti delle configurazioni, in base alle esigenze.

Per le descrizioni dettagliate dei parametri utilizzati di seguito, vedi [opzioni di configurazione nell&#39;SDK delle destinazioni](../../functionality/configuration-options.md).

## Prerequisiti {#prerequisites}

Prima di procedere con i passaggi descritti di seguito, leggere la pagina della [guida introduttiva](../../getting-started.md) di Destination SDK per informazioni su come ottenere le credenziali di autenticazione Adobe I/O necessarie e altri prerequisiti per l&#39;utilizzo delle API Destination SDK.

## Passaggio 1: creare una configurazione di server e file {#create-server-file-configuration}

Iniziare utilizzando l&#39;endpoint `/destination-server` per [creare una configurazione del server e del file](../../authoring-api/destination-server/create-destination-server.md).

**Formato API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Richiesta**

La richiesta seguente crea una nuova configurazione del server di destinazione, configurata dai parametri forniti nel payload.
Il payload seguente include una configurazione BLOB di Azure generica, con parametri di configurazione [per la formattazione del file CSV](../../functionality/destination-server/file-formatting.md) personalizzati che gli utenti possono definire nell&#39;interfaccia utente di Experience Platform.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
 -d '
{
   "name":"Azure Blob server with custom file formatting options and custom file name configuration",
   "description":"Azure Blob server with custom file formatting options and custom file name configuration",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
      }
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
}'
```

Una risposta corretta restituisce la nuova configurazione del server di destinazione, incluso l&#39;identificatore univoco (`instanceId`) della configurazione. Memorizza questo valore come richiesto nel passaggio successivo.

## Passaggio 2: creare la configurazione di destinazione {#create-destination-configuration}

Dopo aver creato la configurazione del server di destinazione e della formattazione del file nel passaggio precedente, è ora possibile utilizzare l&#39;endpoint API `/destinations` per creare una configurazione di destinazione.

Per connettere la configurazione del server in [passaggio 1](#create-server-file-configuration) a questa configurazione di destinazione, sostituire il valore `destinationServerId` nella richiesta API seguente con il valore ottenuto durante la creazione del server di destinazione in [passaggio 1](#create-server-file-configuration).

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
 -d ' {
   "name":"Azure Blob Storage destination with custom file formatting options and custom file name configuration",
   "description":"Azure Blob Storage destination with custom file formatting options and custom file name configuration",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"AZURE_CONNECTION_STRING"
      }
   ],
   "customerDataFields":[
      {
         "name":"path",
         "title":"Folder path",
         "description":"Enter your Azure Blob folder path",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"container",
         "title":"Azure Blob container name",
         "description":"Enter your Azure Blob container name",
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
      "documentationLink":"https://www.adobe.com/go/destinations-blob-connection-parameters-en",
      "category":"cloudStorage",
      "connectionType":"Azure Blob",
      "frequency":"Batch",
      "flowRunsSupported":true,
      "monitoringSupported":true
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
         "destinationServerId":"{{instanceID of your destination server}}"
      }
   ],
   "schemaConfig":{
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "allowJoinKeyFieldSelection":true,
      "defaultExportMode":"DAILY_FULL_EXPORT",
      "allowedExportMode":[
         "DAILY_FULL_EXPORT",
         "FIRST_FULL_THEN_INCREMENTAL"
      ],
      "allowedScheduleFrequency":[
         "DAILY",
         "EVERY_3_HOURS",
         "EVERY_6_HOURS",
         "EVERY_8_HOURS",
         "EVERY_12_HOURS",
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
      "backfillHistoricalProfileData":true
   }
}'
```

Una risposta corretta restituisce la nuova configurazione di destinazione, incluso l&#39;identificatore univoco (`instanceId`) della configurazione. Memorizza questo valore in quanto è necessario se devi effettuare ulteriori richieste HTTP per aggiornare la configurazione di destinazione.

## Passaggio 3: verificare l’interfaccia utente di Experience Platform {#verify-ui}

In base alle configurazioni di cui sopra, nel catalogo di Experience Platform verrà ora visualizzata una nuova scheda di destinazione privata da utilizzare.

![Registrazione schermata che mostra la pagina del catalogo delle destinazioni con una scheda di destinazione selezionata.](../../assets/guides/batch/blob-destination-card.gif)

Nelle immagini e nelle registrazioni seguenti, tieni presente che le opzioni nel flusso di lavoro di attivazione [per le destinazioni basate su file](/help/destinations/ui/activate-batch-profile-destinations.md) corrispondono a quelle selezionate nella configurazione di destinazione.

Durante la compilazione dei dettagli sulla destinazione, noterai come i campi visualizzati sono campi dati personalizzati impostati nella configurazione.

>[!TIP]
>
>L’ordine in cui si aggiungono i campi dati personalizzati alla configurazione di destinazione non si riflette nell’interfaccia utente. I campi dati personalizzati vengono sempre visualizzati nell’ordine indicato nella registrazione schermata seguente.

![inserisci i dettagli della destinazione](../../assets/guides/batch/file-configuration-options.gif)

Durante la pianificazione degli intervalli di esportazione, notare come i campi visualizzati sono quelli impostati nella configurazione `batchConfig`.
![esporta opzioni di pianificazione](../../assets/guides/batch/file-export-scheduling.png)

Quando si visualizzano le opzioni di configurazione del nome file, si noti come i campi visualizzati rappresentano le opzioni `filenameConfig` impostate nella configurazione.
![opzioni di configurazione filename](../../assets/guides/batch/file-naming-options.gif)

Se desideri modificare uno dei campi sopra menzionati, ripeti [i passaggi uno](#create-server-file-configuration) e [due](#create-destination-configuration) per modificare le configurazioni in base alle tue esigenze.

## Passaggio 4: (facoltativo) Publish della tua destinazione {#publish-destination}

>[!NOTE]
>
>Questo passaggio non è necessario se stai creando una destinazione privata per il tuo utilizzo e non stai cercando di pubblicarla nel catalogo delle destinazioni affinché altri clienti la possano utilizzare.

Dopo aver configurato la destinazione, utilizza l&#39;[API di pubblicazione della destinazione](../../publishing-api/create-publishing-request.md) per inviare la configurazione ad Adobe per la revisione.

## Passaggio 5: (facoltativo) documenta la destinazione {#document-destination}

>[!NOTE]
>
>Questo passaggio non è necessario se stai creando una destinazione privata per il tuo utilizzo e non stai cercando di pubblicarla nel catalogo delle destinazioni affinché altri clienti la possano utilizzare.

Se sei un fornitore di software indipendente (ISV) o un integratore di sistemi (SI) che sta creando una [integrazione prodotta](../../overview.md#productized-custom-integrations), utilizza la [procedura di documentazione self-service](../../docs-framework/documentation-instructions.md) per creare una pagina di documentazione del prodotto per la tua destinazione nel [catalogo delle destinazioni di Experience Platform](../../../catalog/overview.md).

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, saprai come creare una destinazione [!DNL Azure Blob Storage] personalizzata utilizzando Destination SDK. Successivamente, il tuo team può utilizzare il [flusso di lavoro di attivazione per le destinazioni basate su file](../../../ui/activate-batch-profile-destinations.md) per esportare i dati nella destinazione.
