---
description: Scopri come utilizzare Destination SDK per configurare una destinazione SFTP con opzioni di formattazione file predefinite e configurazione del nome file personalizzato.
title: (Beta) Configura una destinazione SFTP con opzioni di formattazione file predefinite e configurazione del nome file personalizzato.
exl-id: 6e0fe019-7fbb-48e4-9469-6cc7fc3cb6e4
source-git-commit: a43bb18182ac6e591e011b585719da955ee681b7
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 1%

---

# (Beta) Configura una destinazione SFTP con opzioni di formattazione file predefinite e configurazione del nome file personalizzato

## Panoramica {#overview}

>[!IMPORTANT]
>
>La funzionalità per configurare destinazioni basate su file utilizzando Adobe Experience Platform Destination SDK è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

Questa pagina descrive come utilizzare Destination SDK per configurare una destinazione SFTP con impostazione predefinita [opzioni di formattazione dei file](../../server-and-file-configuration.md#file-configuration) e una [configurazione del nome file](../../file-based-destination-configuration.md#file-name-configuration).

Questa pagina mostra tutte le opzioni di configurazione disponibili per le destinazioni SFTP. Puoi modificare le configurazioni mostrate nei passaggi seguenti o eliminare alcune parti delle configurazioni, in base alle esigenze.

## Prerequisiti {#prerequisites}

Prima di passare ai passaggi descritti di seguito, leggere il [Guida introduttiva alla Destination SDK](../../getting-started.md) per informazioni su come ottenere le credenziali di autenticazione necessarie per l’Adobe I/O e altri prerequisiti per l’utilizzo con le API Destination SDK.

## Passaggio 1: Creare una configurazione del server e del file {#create-server-file-configuration}

Inizia utilizzando `/destination-server` per creare un server e una configurazione di file. Per descrizioni dettagliate dei parametri nella richiesta HTTP, leggi la [specifiche di configurazione del server e dei file per le destinazioni basate su file](../../server-and-file-configuration.md#sftp-example) e i [configurazioni di formattazione dei file](../../server-and-file-configuration.md#file-configuration).

**Formato API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Richiesta**

La richiesta seguente crea una nuova configurazione del server di destinazione, configurata dai parametri forniti nel payload.
Il payload seguente include una configurazione SFTP generica con impostazione predefinita [Formattazione file CSV](../../server-and-file-configuration.md#file-configuration) parametri di configurazione che gli utenti possono definire nell’interfaccia utente di Experience Platform.

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

Una risposta corretta restituisce la nuova configurazione del server di destinazione, incluso l&#39;identificatore univoco (`instanceId`) della configurazione. Memorizza questo valore come necessario nel passaggio successivo.

## Passaggio 2: Creare la configurazione di destinazione {#create-destination-configuration}

Dopo aver creato il server di destinazione e la configurazione di formattazione del file nel passaggio precedente, puoi ora utilizzare il `/destinations` Endpoint API per creare una configurazione di destinazione.

Per collegare la configurazione del server in [passaggio 1](#create-server-file-configuration) in questa configurazione di destinazione, sostituisci il `destinationServerId` nella richiesta API seguente con il valore ottenuto durante la creazione del server di destinazione in [passaggio 1](#create-server-file-configuration).

Per una descrizione dettagliata dei parametri utilizzati di seguito, consulta le pagine seguenti:

* [Configurazione dell’autenticazione](../../authentication-configuration.md#sftp)
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
   "name":"SFTP destination with predefined CSV formatting options",
   "description":"SFTP destination with predefined CSV formatting options",
   "releaseNotes":"",
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

Una risposta corretta restituisce la nuova configurazione di destinazione, incluso l&#39;identificatore univoco (`instanceId`) della configurazione. Memorizza questo valore come necessario se devi effettuare ulteriori richieste HTTP per aggiornare la configurazione di destinazione.

## Passaggio 3: Verificare l’interfaccia utente di Experience Platform {#verify-ui}

In base alle configurazioni di cui sopra, il catalogo di Experience Platform mostrerà ora una nuova scheda di destinazione privata da utilizzare.

![Registrazione su schermo che mostra la pagina del catalogo delle destinazioni con una scheda di destinazione selezionata.](../../assets/destination-card.gif)

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

Leggendo questo articolo, ora sai come creare una destinazione SFTP personalizzata utilizzando Destination SDK. Successivamente, il team può utilizzare [flusso di lavoro di attivazione per destinazioni basate su file](../../../ui/activate-batch-profile-destinations.md) per esportare i dati nella destinazione.
