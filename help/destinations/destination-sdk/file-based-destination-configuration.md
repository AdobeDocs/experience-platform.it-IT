---
description: Questa configurazione consente di indicare informazioni essenziali per la destinazione basata su file, come il nome della destinazione, la categoria, la descrizione e altro ancora. Le impostazioni di questa configurazione determinano anche il modo in cui gli utenti Experienci Platform si autenticano nella destinazione, il modo in cui viene visualizzata nell’interfaccia utente di Experience Platform e le identità che possono essere esportate nella destinazione.
title: Opzioni di configurazione delle destinazioni basate su file per Destination SDK
exl-id: 6b0a0398-6392-470a-bb27-5b34b0062793
source-git-commit: 74f617afe8a0f678d43fb7b949d43cef25e78b9d
workflow-type: tm+mt
source-wordcount: '2982'
ht-degree: 4%

---

# Configurazione di destinazione basata su file {#destination-configuration}

## Panoramica {#overview}

Questa configurazione consente di indicare informazioni essenziali per la destinazione basata su file, come il nome della destinazione, la categoria, la descrizione e altro ancora. Le impostazioni di questa configurazione determinano anche il modo in cui gli utenti Experienci Platform si autenticano nella destinazione, il modo in cui viene visualizzata nell’interfaccia utente di Experience Platform e le identità che possono essere esportate nella destinazione. È inoltre possibile utilizzare questa configurazione per visualizzare le opzioni relative al tipo di file, al formato di file o alle impostazioni di compressione dei file esportati.

Questa configurazione collega a questa anche le altre configurazioni necessarie per il funzionamento della destinazione (metadati del server di destinazione e del pubblico). Scopri come fare riferimento alle due configurazioni in una [sezione più avanti](./file-based-destination-configuration.md#connecting-all-configurations).

È possibile configurare la funzionalità descritta in questo documento utilizzando `/authoring/destinations` Endpoint API Letto [Operazioni degli endpoint API per le destinazioni](./destination-configuration-api.md) per un elenco completo delle operazioni che è possibile eseguire sull&#39;endpoint.

## Esempio di configurazione della destinazione Amazon S3 {#batch-example-configuration}

Di seguito è riportato un esempio di destinazione privata personalizzata di Amazon S3 creata tramite `/destinations` endpoint di configurazione.

```json
{
   "name":"S3 Destination with CSV Options",
   "description":"S3 Destination with CSV Options",
   "status":"TEST",
   "maxProfileAttributes":"2000",
   "maxIdentityAttributes":"10",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerEncryptionConfigurations":[
      
   ],
   "customerDataFields":[
      {
         "name":"bucketName",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
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
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
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
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
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
         "title":"header",
         "description":"Writes the names of columns as the first line.",
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
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
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
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
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
         "title":"Select a fileType",
         "description":"Select fileType",
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
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"S3",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
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
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"phoneNo",
            "title":"phoneNo",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
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
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `name` | Stringa | Indica il titolo della destinazione nel catalogo di Experienci Platform. |
| `description` | Stringa | Fornisci una descrizione della scheda di destinazione nel catalogo delle destinazioni di Experience Platform. Puntare a non più di 4-5 frasi. |
| `status` | Stringa | Indica lo stato del ciclo di vita della scheda di destinazione. I valori accettati sono `TEST`, `PUBLISHED` e `DELETED`. Utilizzare `TEST` la prima volta che configuri la destinazione. |
| `maxProfileAttributes` | Stringa | Indica il numero massimo di attributi di profilo che i clienti possono esportare nella destinazione. Il valore predefinito è `2000`. |
| `maxIdentityAttributes` | Stringa | Indica il numero massimo di spazi dei nomi di identità che i clienti possono esportare nella destinazione. Il valore predefinito è `10`. |

{style="table-layout:auto"}

## Configurazioni di autenticazione del cliente {#customer-authentication-configurations}

Questa sezione nella configurazione delle destinazioni genera il [Configurare una nuova destinazione](/help/destinations/ui/connect-destination.md) nell’interfaccia utente di Experience Platform, in cui gli utenti connettono Experience Platform agli account che hanno con la tua destinazione.

```json
"customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
```

A seconda di quale [opzione di autenticazione](authentication-configuration.md##supported-authentication-types) indichi nella `authType` , la pagina di Experience Platform viene generata come segue per gli utenti:

### Autenticazione Amazon S3 {#s3}

Quando configuri il tipo di autenticazione Amazon S3, gli utenti devono immettere le credenziali S3.

![Rendering dell’interfaccia utente con autenticazione S3](assets/s3-authentication-ui.png)

### Autenticazione BLOB di Azure  {#blob}

Quando configuri il tipo di autenticazione BLOB di Azure, gli utenti devono immettere la stringa di connessione.

![Rendering dell’interfaccia utente con autenticazione BLOB](assets/blob-authentication-ui.png)

### SFTP con autenticazione tramite password

Quando configuri SFTP con il tipo di autenticazione tramite password, gli utenti devono immettere il nome utente e la password SFTP, nonché il dominio e la porta SFTP (la porta predefinita è 22).

![Rendering dell’interfaccia utente con SFTP con autenticazione tramite password](assets/sftp-password-authentication-ui.png)

### SFTP con autenticazione della chiave SSH

Quando configuri SFTP con il tipo di autenticazione della chiave SSH, gli utenti devono immettere il nome utente SFTP e la chiave SSH, nonché il dominio SFTP e la porta (la porta predefinita è 22).

![Rendering dell’interfaccia utente con SFTP con autenticazione tramite chiave SSH](assets/sftp-key-authentication-ui.png)

## Campi dati cliente {#customer-data-fields}

Utilizza questa sezione per chiedere agli utenti di compilare campi personalizzati, specifici per la tua destinazione, durante la connessione alla destinazione nell’interfaccia utente di Experience Platform.

Nell’esempio seguente, `customerDataFields` richiede agli utenti di immettere un nome per la loro destinazione e di fornire un [!DNL Amazon S3] nome del bucket e percorso della cartella, nonché tipo di compressione, formato del file e diverse altre opzioni di formattazione del file.

Puoi accedere e utilizzare gli input dei clienti dai campi dati dei clienti nei modelli. Utilizzare la macro `{{customerData.exampleName}}`. Ad esempio, se chiedi agli utenti di inserire un campo bucket Amazon S3, con il nome `bucket`, è possibile accedervi nei modelli utilizzando la macro `{{customerData.bucket}}`. Visualizza un esempio dell&#39;utilizzo di un campo dati cliente in [configurazione del server di destinazione](/help/destinations/destination-sdk/server-and-file-configuration.md#s3-example).

```json
 "customerDataFields":[
      {
         "name":"bucket",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
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
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
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
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
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
         "title":"header",
         "description":"Writes the names of columns as the first line.",
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
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
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
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
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
         "title":"Select a fileType",
         "description":"Select fileType",
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
```

>[!TIP]
>
>Tutte le configurazioni di formattazione dei file elencate nell&#39;esempio precedente sono descritte in modo dettagliato nel [configurazione formattazione file](/help/destinations/destination-sdk/server-and-file-configuration.md#file-configuration) sezione.

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `name` | Stringa | Immetti un nome per il campo personalizzato che stai presentando. |
| `title` | Stringa | Indica il nome del campo, così come viene visualizzato dai clienti nell’interfaccia utente di Experience Platform. |
| `description` | Stringa | Fornisci una descrizione per il campo personalizzato. |
| `type` | Stringa | Indica il tipo di campo personalizzato che si sta introducendo. I valori accettati sono `string`, `object`, `integer`. |
| `isRequired` | Booleano | Indica se questo campo è obbligatorio nel flusso di lavoro di configurazione della destinazione. |
| `pattern` | Stringa | Se necessario, applica un pattern per il campo personalizzato. Utilizza espressioni regolari per applicare un pattern. Ad esempio, se gli ID cliente non includono numeri o trattini bassi, immetti `^[A-Za-z]+$` in questo campo. |
| `enum` | Stringa | Esegue il rendering del campo personalizzato come menu a discesa ed elenca le opzioni disponibili per l&#39;utente. |
| `default` | Stringa | Definisce il valore predefinito da un `enum` elenco. |

{style="table-layout:auto"}

## Attributi dell’interfaccia utente {#ui-attributes}

Questa sezione fa riferimento agli elementi dell’interfaccia utente nella configurazione precedente che l’Adobe deve utilizzare per la destinazione nell’interfaccia utente di Adobe Experience Platform.

```json
"uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"cloudStorage",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   }
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `documentationLink` | Stringa | Fa riferimento alla pagina della documentazione in [Catalogo delle destinazioni](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) per la tua destinazione. Utilizzare `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, dove `YOURDESTINATION` è il nome della destinazione. Per una destinazione chiamata Moviestar, puoi utilizzare `http://www.adobe.com/go/destinations-moviestar-en`. Tieni presente che questo collegamento funziona solo dopo che Adobe ha impostato la destinazione live e che la documentazione è stata pubblicata. |
| `category` | Stringa | Fa riferimento alla categoria assegnata alla destinazione in Adobe Experience Platform. Per ulteriori informazioni, consulta [Categorie di destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Utilizza uno dei seguenti valori: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `iconUrl` | Stringa | L’URL in cui hai ospitato l’icona da visualizzare nella scheda del catalogo delle destinazioni. Per le integrazioni personalizzate private, questo non è richiesto. Per le configurazioni prodotte, è necessario condividere un’icona con il team di Adobi quando [invia la destinazione per la revisione](/help/destinations/destination-sdk/submit-destination.md#logo). |
| `connectionType` | Stringa | Il tipo di connessione, a seconda della destinazione. Valori supportati: <ul><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li></ul> |
| `flowRunsSupported` | Booleano | Indica se la connessione di destinazione è inclusa nel [flusso esegue l’interfaccia utente](../../dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard). Quando si imposta questa opzione su `true`: <ul><li>Il **[!UICONTROL Data ultima esecuzione del flusso di dati]** e **[!UICONTROL Stato ultima esecuzione del flusso di dati]** vengono visualizzati nella pagina di navigazione di destinazione.</li><li>Il **[!UICONTROL Il flusso di dati viene eseguito]** e **[!UICONTROL Dati di attivazione]** nella pagina di visualizzazione della destinazione vengono visualizzate le schede.</li></ul> |
| `monitoringSupported` | Booleano | Indica se la connessione di destinazione è inclusa nel [interfaccia utente di monitoraggio](../ui/destinations-workspace.md#browse). Quando si imposta questa opzione su `true`, il **[!UICONTROL Visualizza nel monitoraggio]** nella pagina di navigazione di destinazione. |
| `frequency` | Stringa | Si riferisce al tipo di esportazione dei dati supportato dalla destinazione. Imposta su `Batch` per destinazioni basate su file. |

{style="table-layout:auto"}

## Consegna della destinazione {#destination-delivery}

La sezione di consegna della destinazione indica esattamente dove vanno i dati esportati e quale regola di autenticazione viene utilizzata nella posizione in cui verranno recapitati i dati. È necessario specificare uno o più `destinationServerId`s dove verranno consegnati i dati e e regola di autenticazione. Nella maggior parte dei casi, la regola di autenticazione da utilizzare è `CUSTOMER_AUTHENTICATION`.

Il `deliveryMatchers` è facoltativa e può essere utilizzata se si specificano più `destinationServerId`s. In caso affermativo, la `deliveryMatchers` indica come i dati esportati devono essere suddivisi tra i vari server di destinazione.

```json
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
   ]
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `authenticationRule` | Stringa | Indica come [!DNL Platform] i clienti si connettono alla tua destinazione. I valori accettati sono `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilizzare `CUSTOMER_AUTHENTICATION` se i clienti Platform effettuano l’accesso al sistema tramite uno dei seguenti metodi: <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Utilizzare `PLATFORM_AUTHENTICATION` se è presente un sistema di autenticazione globale tra Adobe e la tua destinazione e il [!DNL Platform] Il cliente non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso, è necessario creare un oggetto credenziali utilizzando [Credenziali](./credentials-configuration-api.md) configurazione. </li><li>Utilizzare `NONE` se non è richiesta alcuna autenticazione per inviare dati alla piattaforma di destinazione. </li></ul> |
| `destinationServerId` | Stringa | Il `instanceId` del [configurazione del server di destinazione](./server-and-file-configuration.md) che tu [creato](/help/destinations/destination-sdk/destination-server-api.md#create-file-based) per questa destinazione. |

{style="table-layout:auto"}

## Configurazione della mappatura dei segmenti {#segment-mapping}

Questa sezione della configurazione di destinazione fa riferimento al modo in cui i metadati del segmento come i nomi di segmento o gli ID devono essere condivisi tra Experience Platform e la destinazione.

Attraverso il `audienceTemplateId`, anche questa sezione unisce questa configurazione con [configurazione dei metadati del pubblico](./audience-metadata-management.md).

```json
   "segmentMappingConfig":{
       "mapExperiencePlatformSegmentName":false,
       "mapExperiencePlatformSegmentId":false,
       "mapUserInput":false,
       "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | Booleano | Controlla se l’ID di mappatura del segmento nel flusso di lavoro di attivazione della destinazione è il nome del segmento di Experience Platform. |
| `mapExperiencePlatformSegmentId` | Booleano | Controlla se l’ID di mappatura del segmento nel flusso di lavoro di attivazione della destinazione è l’ID del segmento di Experience Platform. |
| `mapUserInput` | Booleano | Controlla se l’ID di mappatura del segmento nel flusso di lavoro di attivazione della destinazione viene immesso dall’utente. |
| `audienceTemplateId` | Booleano | Il `instanceId` del [modello metadati pubblico](./audience-metadata-management.md) utilizzato per questa destinazione. Per impostare un modello di metadati per il pubblico, leggi [riferimento API per i metadati del pubblico](./audience-metadata-api.md). |

## Configurazione dello schema nel passaggio di mappatura {#schema-configuration}

Adobe Experience Platform Destination SDK supporta gli schemi definiti dai partner. Uno schema definito dal partner consente agli utenti di mappare gli attributi e le identità del profilo agli schemi personalizzati definiti dai partner di destinazione, in modo simile al [destinazioni di streaming](destination-configuration.md#schema-configuration) flusso di lavoro.

Utilizzare i parametri in `schemaConfig` per abilitare il passaggio di mappatura del flusso di lavoro di attivazione della destinazione. Utilizzando i parametri descritti di seguito, puoi determinare se gli utenti Experienci Platform possono mappare gli attributi e/o le identità del profilo alla destinazione basata su file.

Puoi creare campi di schema statici e hardcoded oppure specificare uno schema dinamico a cui Experience Platform deve connettersi per recuperare e popolare dinamicamente i campi nello schema di destinazione del flusso di lavoro di mappatura. Lo schema di destinazione è mostrato nella schermata seguente.

![Schermata che evidenzia i campi dello schema di destinazione nel passaggio di mappatura del flusso di lavoro di attivazione.](/help/destinations/destination-sdk/assets/target-schema-fields.png)

### Configurazione campo schema statico codificato

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           }
        ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `profileFields` | Array | Quando si aggiungono impostazioni predefinite `profileFields`, ad Experience Platform, gli utenti possono effettuare il mapping degli attributi di Platform agli attributi predefiniti nella destinazione. |
| `profileRequired` | Booleano | Utilizzare `true` gli utenti devono essere in grado di mappare gli attributi del profilo da Experience Platform ad attributi personalizzati sul lato della destinazione, come mostrato nella configurazione di esempio precedente. |
| `segmentRequired` | Booleano | Usa sempre `segmentRequired:true`. |
| `identityRequired` | Booleano | Utilizzare `true` gli utenti devono essere in grado di mappare gli spazi dei nomi delle identità dall’Experience Platform allo schema desiderato. |

{style="table-layout:auto"}

### Configurazione dello schema dinamico nel passaggio di mappatura {#dynamic-schema-configuration}

Utilizzare i parametri in  `dynamicSchemaConfig` per recuperare in modo dinamico il tuo schema su cui è possibile mappare gli attributi e/o le identità del profilo di Platform.

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"2aa8a809-c4ae-4f66-bb02-12df2e0a2279",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `profileRequired` | Booleano | Utilizzare `true` gli utenti devono essere in grado di mappare gli attributi del profilo da Experience Platform ad attributi personalizzati sul lato della destinazione, come mostrato nella configurazione di esempio precedente. |
| `segmentRequired` | Booleano | Usa sempre `segmentRequired:true`. |
| `identityRequired` | Booleano | Utilizzare `true` gli utenti devono essere in grado di mappare gli spazi dei nomi delle identità dall’Experience Platform allo schema desiderato. |
| `destinationServerId` | Stringa | Il `instanceId` del [configurazione del server di destinazione](./destination-server-api.md) creato per lo schema dinamico. Questo server di destinazione include l’endpoint HTTP che Experience Platform chiamerà per recuperare lo schema dinamico utilizzato per popolare i campi di destinazione. |
| `authenticationRule` | Stringa | Indica come [!DNL Platform] i clienti si connettono alla tua destinazione. I valori accettati sono `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilizzare `CUSTOMER_AUTHENTICATION` se i clienti Platform effettuano l’accesso al sistema tramite uno dei seguenti metodi: <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Utilizzare `PLATFORM_AUTHENTICATION` se è presente un sistema di autenticazione globale tra Adobe e la tua destinazione e il [!DNL Platform] Il cliente non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso, è necessario creare un oggetto credenziali utilizzando [Credenziali](./credentials-configuration-api.md) configurazione. </li><li>Utilizzare `NONE` se non è richiesta alcuna autenticazione per inviare dati alla piattaforma di destinazione. </li></ul> |
| `value` | Stringa | Il nome dello schema da visualizzare nell’interfaccia utente di Experience Platform, nel passaggio di mappatura. |
| `responseFormat` | Stringa | Sempre impostato su `SCHEMA` durante la definizione di uno schema personalizzato. |

{style="table-layout:auto"}

### Mappature richieste {#required-mappings}

All’interno della configurazione dello schema, puoi aggiungere mappature richieste (o predefinite). Si tratta di mappature che gli utenti possono visualizzare ma non modificare quando impostano una connessione alla destinazione. Ad esempio, puoi applicare che il campo dell’indirizzo e-mail venga sempre inviato alla destinazione nei file esportati. Di seguito sono riportati due esempi di configurazione di schema con mappature richieste e del loro aspetto nel passaggio di mappatura della [flusso di lavoro per l&#39;attivazione dei dati nelle destinazioni batch](/help/destinations/ui/activate-batch-profile-destinations.md).

```json
    "requiredMappingsOnly": true, // when this is selected true , users cannot map other attributes and identities in the activation flow, apart from the required mappings that you define.
    "requiredMappings": [
      {
        "destination": "identityMap.ExamplePartner_ID", //if only the destination field is specified, then the user is able to select a source field to map to the destination.
        "mandatoryRequired": true,
        "primaryKeyRequired": true
      }
    ] 
```

![Immagine delle mappature richieste nel flusso di attivazione dell’interfaccia utente.](/help/destinations/destination-sdk/assets/required-mappings-1.png)

```json
    "requiredMappingsOnly": true, // when this is selected true , users cannot map other attributes and identities in the activation flow, apart from the required mappings that you define.
    "requiredMappings": [
      {
        "sourceType": "text/x.schema-path",
        "source": "personalEmail.address",
        "destination": "personalEmail.address" //when both source and destination fields are specified as required mappings, then the user can not select or edit any of the two fields and can only view the selection.
      }
    ] 
```

![Immagine delle mappature richieste nel flusso di attivazione dell’interfaccia utente.](/help/destinations/destination-sdk/assets/required-mappings-2.png)

>[!NOTE]
>
>Le combinazioni attualmente supportate di mappature richieste sono:
>* Puoi configurare un campo di origine e un campo di destinazione obbligatori. In questo caso, gli utenti non possono modificare o selezionare nessuno dei due campi e possono solo visualizzare la selezione.
>* Puoi configurare solo un campo di destinazione richiesto. In questo caso, gli utenti saranno autorizzati a selezionare un campo di origine da mappare alla destinazione.
>
> La configurazione di un solo campo di origine obbligatorio è attualmente *non* supportati.

Se desideri aggiungere le mappature richieste nel flusso di lavoro di attivazione per la destinazione, utilizza i parametri descritti nella tabella seguente.

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `requiredMappingsOnly` | Booleano | Indica se gli utenti possono mappare altri attributi e identità nel flusso di attivazione, *oltre a* le mappature richieste che definisci. |
| `requiredMappings.mandatoryRequired` | Booleano | Imposta su true se questo campo deve essere un attributo obbligatorio, che deve sempre essere presente nelle esportazioni di file nella destinazione. Ulteriori informazioni su [attributi obbligatori](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `requiredMappings.primaryKeyRequired` | Booleano | Impostato su true se questo campo deve essere utilizzato come chiave di deduplicazione nelle esportazioni di file nella destinazione. Ulteriori informazioni su [chiavi di deduplicazione](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys). |
| `requiredMappings.sourceType` | Stringa | Utilizzato quando configuri un campo sorgente come richiesto. Utilizzare `"text/x.schema-path"`, che indica che il campo di origine è un attributo XDM predefinito |
| `requiredMappings.source` | Stringa | Indica quale deve essere il campo sorgente richiesto. |
| `requiredMappings.destination` | Stringa | Indica quale deve essere il campo di destinazione richiesto. |

{style="table-layout:auto"}

## Identità e attributi {#identities-and-attributes}

I parametri di questa sezione determinano le identità accettate dalla destinazione. Questa configurazione popola anche le identità e gli attributi di destinazione in [passaggio di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) dell’interfaccia utente di Experience Platform, in cui gli utenti mappano identità e attributi dai loro schemi XDM allo schema nella destinazione.


```json
"identityNamespaces": {
        "crm_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        },
        "mobile_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        }
    },
```

Indicare quale [!DNL Platform] identità che i clienti possono esportare nella tua destinazione. Alcuni esempi sono [!DNL Experience Cloud ID], e-mail con hash, ID dispositivo ([!DNL IDFA], [!DNL GAID]). Questi valori sono [!DNL Platform] spazi dei nomi di identità che i clienti possono mappare su spazi dei nomi di identità dalla tua destinazione. Puoi anche indicare se i clienti possono mappare spazi dei nomi personalizzati alle identità supportate dalla destinazione (`acceptsCustomNamespaces: true`) e se i clienti possono mappare gli attributi XDM standard sulle identità supportate dalla destinazione (`acceptsAttributes: true`).

Gli spazi dei nomi delle identità non richiedono una corrispondenza da 1 a 1 tra [!DNL Platform] e la tua destinazione.
Ad esempio, i clienti possono mappare una [!DNL Platform] [!DNL IDFA] spazio dei nomi in un [!DNL IDFA] dalla destinazione, oppure possono mappare lo stesso [!DNL Platform] [!DNL IDFA] spazio dei nomi in un [!DNL Customer ID] dello spazio dei nomi nella destinazione.

Ulteriori informazioni sulle identità in [Panoramica sullo spazio dei nomi delle identità](/help/identity-service/namespaces.md).


## Configurazione batch - Denominazione dei file e pianificazione delle esportazioni {#batch-configuration}

Questa sezione fa riferimento alle impostazioni di denominazione ed esportazione dei file che verranno visualizzate per la destinazione nell&#39;interfaccia utente di Adobe Experience Platform. I valori impostati qui vengono visualizzati in [Pianificare l’esportazione di segmenti](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) passaggio del flusso di lavoro di attivazione delle destinazioni basate su file.

```json
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
   }
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `allowMandatoryFieldSelection` | Booleano | Imposta su `true` per consentire ai clienti di specificare quali attributi di profilo sono obbligatori. Il valore predefinito è `false`. Consulta [Attributi obbligatori](../ui/activate-batch-profile-destinations.md#mandatory-attributes) per ulteriori informazioni. |
| `allowDedupeKeyFieldSelection` | Booleano | Imposta su `true` per consentire ai clienti di specificare le chiavi di deduplicazione. Il valore predefinito è `false`.  Consulta [Chiavi di deduplicazione](../ui/activate-batch-profile-destinations.md#deduplication-keys) per ulteriori informazioni. |
| `defaultExportMode` | Enum | Definisce la modalità di esportazione predefinita del file. Valori supportati:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> Il valore predefinito è `DAILY_FULL_EXPORT`. Consulta la [documentazione sull’attivazione batch](../ui/activate-batch-profile-destinations.md#scheduling) per informazioni dettagliate sulla pianificazione delle esportazioni di file. |
| `allowedExportModes` | Elenco | Definisce le modalità di esportazione dei file disponibili per i clienti. Valori supportati:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Elenco | Definisce la frequenza di esportazione dei file disponibile per i clienti. Valori supportati:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Enum | Definisce la frequenza di esportazione predefinita dei file. Valori supportati:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> Il valore predefinito è `DAILY`. |
| `defaultStartTime` | Stringa | Definisce l&#39;ora di inizio predefinita per l&#39;esportazione del file. Utilizza il formato file a 24 ore. Il valore predefinito è &quot;00:00&quot;. |
| `filenameConfig.allowedFilenameAppendOptions` | Stringa | *Obbligatorio*. Elenco delle macro di nomi file disponibili tra cui gli utenti possono scegliere. Questo determina quali elementi vengono aggiunti ai nomi dei file esportati (ID segmento, nome organizzazione, data e ora di esportazione e altri). Quando si imposta `defaultFilename`, assicurarsi di evitare la duplicazione delle macro. <br><br>Valori supportati: <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Indipendentemente dall&#39;ordine in cui si definiscono le macro, l&#39;interfaccia utente di Experience Platform le visualizzerà sempre nell&#39;ordine presentato qui. <br><br> Se `defaultFilename` è vuoto, il `allowedFilenameAppendOptions` l&#39;elenco deve contenere almeno una macro. |
| `filenameConfig.defaultFilenameAppendOptions` | Stringa | *Obbligatorio*. Macro dei nomi di file predefiniti preselezionate che gli utenti possono deselezionare.<br><br> Le macro di questo elenco sono un sottoinsieme di quelle definite in `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | Stringa | *Facoltativo*. Definisce le macro dei nomi di file predefiniti per i file esportati. Non possono essere sovrascritti dagli utenti. <br><br>Qualsiasi macro definita da `allowedFilenameAppendOptions` verrà aggiunto dopo il `defaultFilename` macro. <br><br>Se `defaultFilename` è vuoto, è necessario definire almeno una macro in `allowedFilenameAppendOptions`. |

{style="table-layout:auto"}

### Configurazione del nome file {#file-name-configuration}

Utilizzare le macro di configurazione dei nomi di file per definire i nomi di file esportati da includere. Le macro nella tabella seguente descrivono gli elementi presenti nell’interfaccia utente di [configurazione del nome file](../ui/activate-batch-profile-destinations.md#file-names) schermo.


>[!TIP]
> 
>Come best practice, devi sempre includere `SEGMENT_ID` nei nomi dei file esportati. Poiché gli ID segmento sono univoci, includerli nel nome file è il modo migliore per garantire che anche i nomi dei file siano univoci.

| Macro | Etichetta interfaccia utente | Descrizione | Esempio |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Destinazione] | Nome della destinazione nell’interfaccia utente. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL ID segmento] | ID segmento univoco generato dalla piattaforma | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Nome segmento] | Nome segmento definito dall&#39;utente | Abbonato VIP |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL ID destinazione] | ID univoco generato dalla piattaforma dell’istanza di destinazione | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Nome destinazione] | Nome definito dall&#39;utente dell&#39;istanza di destinazione. | La mia destinazione pubblicitaria 2022 |
| `ORGANIZATION_NAME` | [!UICONTROL Nome organizzazione] | Nome dell’organizzazione del cliente in Adobe Experience Platform. | Nome organizzazione |
| `SANDBOX_NAME` | [!UICONTROL Nome sandbox] | Nome della sandbox utilizzato dal cliente. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Data e ora] | `DATETIME` e `TIMESTAMP` entrambi definiscono quando il file è stato generato, ma in formati diversi. <br><br><ul><li>`DATETIME` utilizza il seguente formato: YYYYMMDD_HHMMSS.</li><li>`TIMESTAMP` utilizza il formato Unix a 10 cifre. </li></ul> `DATETIME` e `TIMESTAMP` si escludono a vicenda e non possono essere utilizzate simultaneamente. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Testo personalizzato] | Testo personalizzato definito dall&#39;utente da includere nel nome del file. Non può essere utilizzato in `defaultFilename`. | My_Custom_Text |
| `TIMESTAMP` | [!UICONTROL Data e ora] | Timestamp a 10 cifre dell’ora in cui è stato generato il file, in formato Unix. | 1652131584 |

{style="table-layout:auto"}

![Immagine dell&#39;interfaccia utente che mostra la schermata di configurazione del nome file con le macro preselezionate](assets/file-name-configuration.png)

Nell&#39;esempio riportato nell&#39;immagine precedente viene utilizzata la seguente configurazione di macro per il nome di file:

```json
"filenameConfig":{
   "allowedFilenameAppendOptions":[
      "CUSTOM_TEXT",
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilenameAppendOptions":[
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilename": "%DESTINATION%"
}
```


## Qualifiche del profilo storico {#profile-backfill}

È possibile utilizzare `backfillHistoricalProfileData` nella configurazione delle destinazioni per determinare se le qualifiche storiche del profilo devono essere esportate nella destinazione.

```json
   "backfillHistoricalProfileData":true
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `backfillHistoricalProfileData` | Booleano | Controlla se i dati storici del profilo vengono esportati quando i segmenti vengono attivati nella destinazione. <br> <ul><li> `true`: [!DNL Platform] invia i profili utente storici qualificati per il segmento prima che il segmento venga attivato. </li><li> `false`: [!DNL Platform] include solo i profili utente idonei per il segmento dopo l’attivazione del segmento. </li></ul> |

{style="table-layout:auto"}

## Come questa configurazione collega tutte le informazioni necessarie per la destinazione {#connecting-all-configurations}

Alcune delle impostazioni di destinazione devono essere configurate tramite [server di destinazione](./server-and-file-configuration.md) o [configurazione dei metadati del pubblico](./audience-metadata-management.md) endpoint. La configurazione di destinazione qui descritta collega tutte queste impostazioni facendo riferimento alle altre due configurazioni come segue:

* Utilizza il `destinationServerId` per fare riferimento alla configurazione del server di destinazione e del modello di file impostata per la destinazione.
* Utilizza il `audienceMetadataId` per fare riferimento alla configurazione dei metadati del pubblico impostata per la destinazione.
