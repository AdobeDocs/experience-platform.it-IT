---
description: Scopri come utilizzare Destination SDK per configurare una destinazione SFTP con opzioni di formattazione di file predefinite e configurazione del nome file personalizzato.
title: Configura una destinazione SFTP con opzioni di formattazione del file predefinite e configurazione del nome file personalizzato.
exl-id: 6e0fe019-7fbb-48e4-9469-6cc7fc3cb6e4
source-git-commit: d47c82339afa602a9d6914c1dd36a4fc9528ea32
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 1%

---

# Configurare una destinazione SFTP con opzioni di formattazione file predefinite e configurazione del nome file personalizzato

## Panoramica {#overview}

In questa pagina viene descritto come utilizzare Destination SDK per configurare una destinazione SFTP con [opzioni di formattazione file predefinite](configure-file-formatting-options.md) e una [configurazione nome file](../../functionality/destination-configuration/batch-configuration.md#file-name-configuration) personalizzata.

Questa pagina mostra tutte le opzioni di configurazione disponibili per le destinazioni SFTP. Puoi modificare le configurazioni mostrate nei passaggi seguenti o eliminare alcune parti delle configurazioni, in base alle esigenze.

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
Il payload seguente include una configurazione SFTP generica, con [parametri di configurazione predefiniti di formattazione del file CSV](../../functionality/destination-server/file-formatting.md) che gli utenti possono definire nell&#39;interfaccia utente di Experience Platform.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "name": "SFTP destination with predefined CSV formatting options",
    "destinationServerType": "FILE_BASED_SFTP",
    "fileBasedSFTPDestination": {
        "hostname": {
            "templatingStrategy": "NONE",
            "value": "{{customerData.hostname}}"
        },
        "rootDirectory": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.remotePath}}"
        },
        "port": 22
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
 -d '
{
   "name":"SFTP destination with predefined CSV formatting options",
   "description":"SFTP destination with predefined CSV formatting options",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"SFTP_WITH_PASSWORD"
      },
      {
         "authType":"SFTP_WITH_SSH_KEY"
      }
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"remotePath",
         "title":"Root directory",
         "description":"Enter root directory",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"hostname",
         "title":"Hostname",
         "description":"Enter hostname",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-sftp-en",
      "category":"SFTP",
      "connectionType":"SFTP",
      "monitoringSupported":true,
      "flowRunsSupported":true,
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
         "EVERY_8_HOURS",
         "EVERY_12_HOURS",
         "ONCE"
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

![Registrazione schermata che mostra la pagina del catalogo delle destinazioni con una scheda di destinazione selezionata.](../../assets/guides/batch/destination-card.gif)

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

Una volta letto questo articolo, sai come creare una destinazione SFTP personalizzata utilizzando Destination SDK. Successivamente, il tuo team può utilizzare il [flusso di lavoro di attivazione per le destinazioni basate su file](../../../ui/activate-batch-profile-destinations.md) per esportare i dati nella destinazione.
