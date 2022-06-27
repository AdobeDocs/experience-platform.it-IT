---
description: Questa configurazione ti consente di indicare informazioni di base come il nome di destinazione, la categoria, la descrizione, il logo e altro ancora. Le impostazioni di questa configurazione determinano anche come gli utenti di Experience Platform si autenticano nella destinazione, come vengono visualizzati nell’interfaccia utente di Experience Platform e le identità che possono essere esportate nella destinazione.
title: (Beta) Opzioni di configurazione della destinazione basata su file per Destination SDK
exl-id: 6b0a0398-6392-470a-bb27-5b34b0062793
source-git-commit: bd89df0659604c05ffd049682343056dbe5667e3
workflow-type: tm+mt
source-wordcount: '2313'
ht-degree: 5%

---

# (Beta) Configurazione della destinazione basata su file {#destination-configuration}

## Panoramica {#overview}

>[!IMPORTANT]
>
>Il supporto per la destinazione basata su file in Adobe Experience Platform Destination SDK è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

Questa configurazione ti consente di indicare informazioni essenziali per la destinazione basata su file, come nome di destinazione, categoria, descrizione e altro ancora. Le impostazioni di questa configurazione determinano anche come gli utenti di Experience Platform si autenticano nella destinazione, come vengono visualizzati nell’interfaccia utente di Experience Platform e le identità che possono essere esportate nella destinazione.

Questa configurazione collega anche le altre configurazioni necessarie per la tua destinazione al lavoro - server di destinazione e metadati del pubblico - a questa. Scopri come fare riferimento alle due configurazioni in una [sezione successiva](./destination-configuration.md#connecting-all-configurations).

Puoi configurare la funzionalità descritta in questo documento utilizzando `/authoring/destinations` Endpoint API. Leggi [Operazioni degli endpoint API delle destinazioni](./destination-configuration-api.md) per un elenco completo delle operazioni eseguibili sull&#39;endpoint.

## Esempio di configurazione della destinazione Amazon S3 {#batch-example-configuration}

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
| `name` | Stringa | Indica il titolo della destinazione nel catalogo Experience Platform. |
| `description` | Stringa | Immetti una descrizione della scheda di destinazione nel catalogo delle destinazioni Experience Platform. Mirare a non più di 4-5 frasi. |
| `status` | Stringa | Indica lo stato del ciclo di vita della scheda di destinazione. I valori accettati sono `TEST`, `PUBLISHED` e `DELETED`. Utilizzo `TEST` la prima volta che configuri la destinazione. |
| `maxProfileAttributes` | Stringa | Indica il numero massimo di attributi di profilo che i clienti possono esportare nella destinazione. Il valore predefinito è `2000`. |
| `maxIdentityAttributes` | Stringa | Indica il numero massimo di spazi dei nomi di identità che i clienti possono esportare nella destinazione. Il valore predefinito è `10`. |

{style=&quot;table-layout:auto&quot;}

## Configurazioni di autenticazione dei clienti {#customer-authentication-configurations}

Questa sezione nella configurazione delle destinazioni genera il [Configurare una nuova destinazione](/help/destinations/ui/connect-destination.md) nell’interfaccia utente di Experience Platform, in cui gli utenti collegano Experience Platform agli account che hanno con la tua destinazione.

```json
"customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
```

A seconda di quale [opzione di autenticazione](authentication-configuration.md##supported-authentication-types) indica nella `authType` la pagina dell’Experience Platform viene generata per gli utenti come segue:

### Autenticazione Amazon S3 {#s3}

Quando si configura il tipo di autenticazione Amazon S3, gli utenti devono immettere le credenziali S3.

![Rendering dell’interfaccia utente con autenticazione S3](assets/s3-authentication-ui.png)

### Autenticazione BLOB di Azure  {#blob}

Quando configuri il tipo di autenticazione BLOB di Azure, gli utenti devono immettere la stringa di connessione.

![Rendering dell’interfaccia utente con autenticazione BLOB](assets/blob-authentication-ui.png)

### SFTP con autenticazione tramite password

Quando configuri l’SFTP con il tipo di autenticazione tramite password, gli utenti devono immettere il nome utente e la password SFTP, nonché il dominio e la porta SFTP (la porta predefinita è 22).

![Rendering dell’interfaccia utente con SFTP con autenticazione tramite password](assets/sftp-password-authentication-ui.png)

### SFTP con autenticazione a chiave SSH

Quando configuri l’SFTP con il tipo di autenticazione chiave SSH, gli utenti devono inserire il nome utente SFTP e la chiave SSH, nonché il dominio e la porta SFTP (la porta predefinita è 22).

![Rendering dell’interfaccia utente con SFTP con autenticazione a chiave SSH](assets/sftp-key-authentication-ui.png)

## Campi dati cliente {#customer-data-fields}

Usa questa sezione per chiedere agli utenti di compilare campi personalizzati, specifici per la tua destinazione, quando ti connetti alla destinazione nell’interfaccia utente di Experience Platform.

Nell’esempio seguente: `customerDataFields` richiede agli utenti di immettere un nome per la loro destinazione e di fornire un [!DNL Amazon S3] nome del bucket e percorso della cartella, nonché un tipo di compressione, un formato di file e diverse altre opzioni di esportazione del file.

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

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `name` | Stringa | Specifica un nome per il campo personalizzato che stai introducendo. |
| `title` | Stringa | Indica il nome del campo, come visualizzato dai clienti nell’interfaccia utente di Experience Platform. |
| `description` | Stringa | Immetti una descrizione del campo personalizzato. |
| `type` | Stringa | Indica il tipo di campo personalizzato che si sta introducendo. I valori accettati sono `string`, `object`, `integer`. |
| `isRequired` | Booleano | Indica se questo campo è obbligatorio nel flusso di lavoro di configurazione della destinazione. |
| `pattern` | Stringa | Applica un pattern per il campo personalizzato, se necessario. Utilizzare espressioni regolari per applicare un pattern. Ad esempio, se gli ID cliente non includono numeri o caratteri di sottolineatura, immetti `^[A-Za-z]+$` in questo campo. |
| `enum` | Stringa | Esegue il rendering del campo personalizzato come menu a discesa ed elenca le opzioni disponibili per l’utente. |
| `default` | Stringa | Definisce il valore predefinito da un `enum` elenco. |

{style=&quot;table-layout:auto&quot;}

## Attributi dell&#39;interfaccia utente {#ui-attributes}

Questa sezione fa riferimento agli elementi dell’interfaccia utente nella configurazione precedente che l’Adobe deve utilizzare per la destinazione nell’interfaccia utente di Adobe Experience Platform.

```json
"uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"S3",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   }
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `documentationLink` | Stringa | Si riferisce alla pagina della documentazione nel [Catalogo delle destinazioni](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) per la tua destinazione. Utilizzo `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, dove `YOURDESTINATION` è il nome della destinazione. Per una destinazione denominata Moviestar, puoi utilizzare `http://www.adobe.com/go/destinations-moviestar-en` |
| `category` | Stringa | Si riferisce alla categoria assegnata alla destinazione in Adobe Experience Platform. Per ulteriori informazioni, leggere [Categorie di destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Utilizzare uno dei seguenti valori: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `iconUrl` | Stringa | URL in cui hai ospitato l’icona da visualizzare nella scheda del catalogo delle destinazioni. |
| `connectionType` | Stringa | Il tipo di connessione, a seconda della destinazione. Valori supportati: <ul><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li></ul> |
| `flowRunsSupported` | Booleano | Indica se la connessione di destinazione è inclusa nel [interfaccia utente di flow](../../dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard). Quando si imposta questa opzione su `true`: <ul><li>La **[!UICONTROL Data ultima esecuzione del flusso di dati]** e **[!UICONTROL Stato dell&#39;ultima esecuzione del flusso di dati]** vengono visualizzati nella pagina di ricerca di destinazione.</li><li>La **[!UICONTROL Corse del flusso di dati]** e **[!UICONTROL Dati di attivazione]** le schede vengono visualizzate nella pagina di visualizzazione di destinazione.</li></ul> |
| `monitoringSupported` | Booleano | Indica se la connessione di destinazione è inclusa nel [interfaccia utente di monitoraggio](../ui/destinations-workspace.md#browse). Quando si imposta questa opzione su `true`, **[!UICONTROL Visualizza nel monitoraggio]** nella pagina di ricerca di destinazione viene visualizzata l’opzione . |
| `frequency` | Stringa | Si riferisce al tipo di esportazione di dati supportato dalla destinazione. Imposta su `Batch` per le destinazioni basate su file. |

{style=&quot;table-layout:auto&quot;}

## Consegna delle destinazioni {#destination-delivery}

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
| `authenticationRule` | Stringa | Indica come [!DNL Platform] i clienti si connettono alla destinazione. I valori accettati sono `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilizzo `CUSTOMER_AUTHENTICATION` se i clienti di Platform accedono al sistema tramite uno dei seguenti metodi: <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Utilizzo `PLATFORM_AUTHENTICATION` se esiste un sistema di autenticazione globale tra l’Adobe e la destinazione e [!DNL Platform] il cliente non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso è necessario creare un oggetto credenziali utilizzando [Credenziali](./credentials-configuration-api.md) configurazione. </li><li>Utilizzo `NONE` se non è richiesta alcuna autenticazione per inviare dati alla piattaforma di destinazione. </li></ul> |
| `destinationServerId` | Stringa | La `instanceId` del [configurazione del server di destinazione](./destination-server-api.md) utilizzato per questa destinazione. |

{style=&quot;table-layout:auto&quot;}

## Configurazione della mappatura dei segmenti {#segment-mapping}

Questa sezione della configurazione di destinazione si riferisce al modo in cui i metadati del segmento come i nomi dei segmenti o gli ID devono essere condivisi tra l’Experience Platform e la destinazione.

Attraverso il `audienceTemplateId`, questa sezione collega anche questa configurazione con [configurazione dei metadati del pubblico](./audience-metadata-management.md).

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
| `mapExperiencePlatformSegmentName` | Booleano | Controlla se l&#39;ID di mappatura del segmento nel flusso di lavoro di attivazione della destinazione è il nome del segmento di Experience Platform. |
| `mapExperiencePlatformSegmentId` | Booleano | Controlla se l&#39;ID di mappatura del segmento nel flusso di lavoro di attivazione della destinazione è l&#39;ID del segmento di Experience Platform. |
| `mapUserInput` | Booleano | Controlla se l&#39;ID di mappatura del segmento nel flusso di lavoro di attivazione della destinazione viene immesso dall&#39;utente. |
| `audienceTemplateId` | Booleano | La `instanceId` del [modello di metadati del pubblico](./audience-metadata-management.md) utilizzato per questa destinazione. Per impostare un modello di metadati del pubblico, leggi la sezione [riferimento API per metadati del pubblico](./audience-metadata-api.md). |

## Configurazione dello schema nella fase di mappatura {#schema-configuration}

Utilizza i parametri in `schemaConfig` per abilitare il passaggio di mappatura del flusso di lavoro di attivazione della destinazione. Utilizzando i parametri descritti di seguito, puoi determinare se gli utenti di Experience Platform possono mappare gli attributi e/o le identità del profilo sulla destinazione basata su file.

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
| `profileFields` | Array | Quando si aggiungono predefiniti `profileFields`, gli utenti di Experience Platform possono mappare gli attributi di Platform agli attributi predefiniti nella destinazione. |
| `profileRequired` | Booleano | Utilizzo `true` se gli utenti devono essere in grado di mappare gli attributi di profilo dall’Experience Platform agli attributi personalizzati sul lato della destinazione, come illustrato nella configurazione di esempio precedente. |
| `segmentRequired` | Booleano | Usa sempre `segmentRequired:true`. |
| `identityRequired` | Booleano | Utilizzo `true` se gli utenti devono essere in grado di mappare i namespace di identità dall&#39;Experience Platform allo schema desiderato. |

{style=&quot;table-layout:auto&quot;}

### Configurazione dello schema dinamico nel passaggio di mappatura {#dynamic-schema-configuration}

Adobe Experience Platform Destination SDK supporta schemi definiti da partner. Uno schema definito da un partner consente agli utenti di mappare attributi e identità di profilo a schemi personalizzati definiti dai partner di destinazione, in modo simile al [destinazioni di streaming](destination-configuration.md#schema-configuration) workflow.

Utilizza i parametri in  `dynamicSchemaConfig` per definire un proprio schema a cui è possibile mappare gli attributi e/o le identità del profilo di Platform.

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}",
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
| `profileRequired` | Booleano | Utilizzo `true` se gli utenti devono essere in grado di mappare gli attributi di profilo dall’Experience Platform agli attributi personalizzati sul lato della destinazione, come illustrato nella configurazione di esempio precedente. |
| `segmentRequired` | Booleano | Usa sempre `segmentRequired:true`. |
| `identityRequired` | Booleano | Utilizzo `true` se gli utenti devono essere in grado di mappare i namespace di identità dall&#39;Experience Platform allo schema desiderato. |
| `destinationServerId` | Stringa | La `instanceId` del [configurazione del server di destinazione](./destination-server-api.md) utilizzato per questa destinazione. |
| `authenticationRule` | Stringa | Indica come [!DNL Platform] i clienti si connettono alla destinazione. I valori accettati sono `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilizzo `CUSTOMER_AUTHENTICATION` se i clienti di Platform accedono al sistema tramite uno dei seguenti metodi: <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Utilizzo `PLATFORM_AUTHENTICATION` se esiste un sistema di autenticazione globale tra l’Adobe e la destinazione e [!DNL Platform] il cliente non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso è necessario creare un oggetto credenziali utilizzando [Credenziali](./credentials-configuration-api.md) configurazione. </li><li>Utilizzo `NONE` se non è richiesta alcuna autenticazione per inviare dati alla piattaforma di destinazione. </li></ul> |
| `value` | Stringa | Nome dello schema da visualizzare nell’interfaccia utente di Experience Platform, nel passaggio di mappatura. |
| `responseFormat` | Stringa | Sempre impostato su `SCHEMA` durante la definizione di uno schema personalizzato. |

{style=&quot;table-layout:auto&quot;}

## Identità e attributi {#identities-and-attributes}

I parametri di questa sezione determinano le identità accettate dalla destinazione. Questa configurazione popola anche le identità e gli attributi di destinazione nel [fase di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) dell’interfaccia utente di Experience Platform, in cui gli utenti mappano identità e attributi dai loro schemi XDM allo schema di destinazione.


```json
"identityNamespaces": {
        "adobe_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        },
        "mobile_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        }
    },
```

Indica quale [!DNL Platform] i clienti di identità possono esportare nella tua destinazione. Alcuni esempi [!DNL Experience Cloud ID], e-mail con hash, ID dispositivo ([!DNL IDFA], [!DNL GAID]). Questi valori sono [!DNL Platform] spazi dei nomi delle identità che i clienti possono mappare a spazi dei nomi delle identità dalla destinazione. Puoi anche indicare se i clienti possono mappare i namespace personalizzati alle identità supportate dalla tua destinazione.

Gli spazi dei nomi di identità non richiedono una corrispondenza 1-to-1 tra [!DNL Platform] e la destinazione.
Ad esempio, i clienti possono mappare un [!DNL Platform] [!DNL IDFA] spazio dei nomi in un [!DNL IDFA] spazio dei nomi dalla destinazione, oppure possono mappare lo stesso [!DNL Platform] [!DNL IDFA] spazio dei nomi in un [!DNL Customer ID] spazio dei nomi nella destinazione.

## Configurazione batch {#batch-configuration}

Questa sezione fa riferimento alle impostazioni di esportazione dei file nella configurazione precedente che l’Adobe deve utilizzare per la destinazione nell’interfaccia utente di Adobe Experience Platform.

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
| `allowMandatoryFieldSelection` | Booleano | Imposta su `true` per consentire ai clienti di specificare quali attributi di profilo sono obbligatori. Il valore predefinito è `false`. Vedi [Attributi obbligatori](../ui/activate-batch-profile-destinations.md#mandatory-attributes) per ulteriori informazioni. |
| `allowDedupeKeyFieldSelection` | Booleano | Imposta su `true` per consentire ai clienti di specificare le chiavi di deduplicazione. Il valore predefinito è `false`.  Vedi [Chiavi di deduplicazione](../ui/activate-batch-profile-destinations.md#deduplication-keys) per ulteriori informazioni. |
| `defaultExportMode` | Enum | Definisce la modalità di esportazione predefinita dei file. Valori supportati:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> Il valore predefinito è `DAILY_FULL_EXPORT`. Consulta la sezione [documentazione di attivazione batch](../ui/activate-batch-profile-destinations.md#scheduling) per informazioni sulla pianificazione delle esportazioni dei file. |
| `allowedExportModes` | Elenco | Definisce le modalità di esportazione dei file disponibili per i clienti. Valori supportati:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Elenco | Definisce la frequenza di esportazione del file disponibile per i clienti. Valori supportati:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Enum | Definisce la frequenza di esportazione predefinita del file.Valori supportati:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> Il valore predefinito è `DAILY`. |
| `defaultStartTime` | Stringa | Definisce l&#39;ora di inizio predefinita per l&#39;esportazione del file. Utilizza il formato file 24 ore su 24. Il valore predefinito è &quot;00:00&quot;. |
| `filenameConfig.allowedFilenameAppendOptions` | Stringa | *Obbligatorio*. Elenco delle macro dei nomi file disponibili tra cui gli utenti possono scegliere. Questo determina quali elementi vengono aggiunti ai nomi di file esportati (ID segmento, nome organizzazione, data e ora dell’esportazione e altri). Quando si imposta `defaultFilename`, evitare di duplicare le macro. <br><br>Valori supportati: <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Indipendentemente dall’ordine in cui vengono definite le macro, l’interfaccia utente Experience Platform le visualizza sempre nell’ordine indicato qui. <br><br> Se `defaultFilename` è vuoto, il `allowedFilenameAppendOptions` L&#39;elenco deve contenere almeno una macro. |
| `filenameConfig.defaultFilenameAppendOptions` | Stringa | *Obbligatorio*. Macro con nome file predefinito preselezionate che gli utenti possono deselezionare.<br><br> Le macro di questo elenco sono un sottoinsieme di quelle definite in `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | Stringa | *Facoltativo*. Definisce le macro dei nomi file predefiniti per i file esportati. Questi non possono essere sovrascritti dagli utenti. <br><br>Qualsiasi macro definita da `allowedFilenameAppendOptions` viene aggiunto dopo il `defaultFilename` macro. <br><br>Se `defaultFilename` è vuoto, è necessario definire almeno una macro in `allowedFilenameAppendOptions`. |

{style=&quot;table-layout:auto&quot;}

### Configurazione del nome file {#file-name-configuration}

Utilizzare le macro di configurazione del nome file per definire i nomi di file esportati da includere. Le macro nella tabella seguente descrivono gli elementi presenti nell’interfaccia utente di [configurazione del nome file](../ui/activate-batch-profile-destinations.md#file-names) schermo.

Come best practice, includi sempre `SEGMENT_ID` nei nomi dei file esportati. Gli ID dei segmenti sono univoci, pertanto includerli nel nome del file è il modo migliore per garantire che anche i nomi dei file siano univoci.

| Macro | Etichetta dell’interfaccia utente | Descrizione | Esempio |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Destinazione] | Nome della destinazione nell’interfaccia utente. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL ID segmento] | ID segmento univoco generato dalla piattaforma | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Nome segmento] | Nome del segmento definito dall’utente | Sottoscrittore VIP |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL ID destinazione] | ID univoco generato dalla piattaforma dell’istanza di destinazione | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Nome destinazione] | Nome definito dall&#39;utente dell&#39;istanza di destinazione. | La mia destinazione pubblicitaria 2022 |
| `ORGANIZATION_NAME` | [!UICONTROL Nome organizzazione] | Nome dell&#39;organizzazione del cliente in Adobe Experience Platform. | Nome organizzazione |
| `SANDBOX_NAME` | [!UICONTROL Nome sandbox] | Nome della sandbox utilizzata dal cliente. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Data e ora] | `DATETIME` e `TIMESTAMP` entrambi definiscono quando è stato generato il file, ma in formati diversi. <br><br><ul><li>`DATETIME` utilizza il formato seguente: YYYMMDD_HHMMSS.</li><li>`TIMESTAMP` utilizza il formato Unix a 10 cifre. </li></ul> `DATETIME` e `TIMESTAMP` si escludono a vicenda e non possono essere utilizzati contemporaneamente. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Testo personalizzato] | Testo personalizzato definito dall’utente da includere nel nome del file. Non può essere utilizzato in `defaultFilename`. | Testo_Personalizzato |
| `TIMESTAMP` | [!UICONTROL Data e ora] | Timestamp a 10 cifre dell’ora in cui è stato generato il file, in formato Unix. | 1652131584 |

{style=&quot;table-layout:auto&quot;}

![Immagine dell’interfaccia utente che mostra la schermata di configurazione del nome file con macro preselezionate](assets/file-name-configuration.png)

L&#39;esempio mostrato nell&#39;immagine precedente utilizza la seguente configurazione di macro del nome file:

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


## Qualifiche di profilo storiche {#profile-backfill}

È possibile utilizzare `backfillHistoricalProfileData` nella configurazione delle destinazioni per determinare se le qualifiche di profilo storico devono essere esportate nella destinazione.

```json
   "backfillHistoricalProfileData":true
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `backfillHistoricalProfileData` | Booleano | Controlla se i dati storici del profilo vengono esportati quando i segmenti vengono attivati nella destinazione. <br> <ul><li> `true`: [!DNL Platform] invia i profili utente storici qualificati per il segmento prima che il segmento venga attivato. </li><li> `false`: [!DNL Platform] include solo i profili utente qualificati per il segmento dopo l’attivazione del segmento. </li></ul> |

{style=&quot;table-layout:auto&quot;}

## Come questa configurazione connette tutte le informazioni necessarie per la destinazione {#connecting-all-configurations}

Alcune delle impostazioni di destinazione devono essere configurate tramite il [server di destinazione](./server-and-file-configuration.md) o [configurazione dei metadati del pubblico](./audience-metadata-management.md). La configurazione di destinazione qui descritta connette tutte queste impostazioni facendo riferimento alle altre due configurazioni come segue:

* Utilizza la `destinationServerId` per fare riferimento al server di destinazione e alla configurazione del modello impostata per la destinazione.
* Utilizza la `audienceMetadataId` per fare riferimento alla configurazione dei metadati del pubblico impostata per la destinazione.
