---
description: Questa pagina elenca e descrive tutte le operazioni API che puoi eseguire utilizzando l'endpoint API `/authoring/destinations`.
title: Operazioni degli endpoint API delle destinazioni
exl-id: 96755e9d-be62-432f-b985-91330575b395
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '2537'
ht-degree: 5%

---

# Operazioni API per gli endpoint delle destinazioni {#destination-configuration}

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/destinations`

Questa pagina elenca e descrive tutte le operazioni API che puoi eseguire utilizzando `/authoring/destinations` Endpoint API. Per una descrizione delle funzionalità supportate da questo endpoint, leggere [configurazione di destinazione](./destination-configuration.md).

## Guida introduttiva alle operazioni API di destinazione {#get-started}

Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, tra cui come ottenere l’autorizzazione di authoring di destinazione richiesta e le intestazioni richieste.

## Creare una configurazione per una destinazione in streaming {#create}

Puoi creare una nuova configurazione di destinazione effettuando una richiesta di POST al `/authoring/destinations` punto finale.

**Formato API**

```http
POST /authoring/destinations
```

**Richiesta**

La richiesta seguente crea una nuova configurazione di destinazione dello streaming, configurata dai parametri forniti nel payload. Il payload seguente include tutti i parametri per le destinazioni di streaming accettate dal `/authoring/destinations` punto finale. Non è necessario aggiungere tutti i parametri alla chiamata e il modello è personalizzabile, in base ai requisiti API.

```json
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
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
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
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
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `name` | Stringa | Indica il titolo della destinazione nel catalogo Experience Platform |
| `description` | Stringa | Immetti una descrizione che Adobe utilizzerà nel catalogo delle destinazioni Experience Platform per la tua scheda di destinazione. Mirare a non più di 4-5 frasi. |
| `status` | Stringa | Indica lo stato del ciclo di vita della scheda di destinazione. I valori accettati sono `TEST`, `PUBLISHED` e `DELETED`. Utilizzo `TEST` la prima volta che configuri la destinazione. |
| `customerAuthenticationConfigurations` | Stringa | Indica la configurazione utilizzata per autenticare i clienti Experience Platform nel server. Vedi `authType` di seguito per i valori accettati. |
| `customerAuthenticationConfigurations.authType` | Stringa | I valori supportati per le destinazioni di streaming sono: <ul><li>`OAUTH2`</li><li>`BEARER`</li></ul> I valori supportati per le destinazioni basate su file sono: <ul><li>`S3`</li><li>`AZURE_CONNECTION_STRING`</li><li>`AZURE_SERVICE_PRINCIPAL`</li><li>`SFTP_WITH_SSH_KEY`</li><li>`SFTP_WITH_PASSWORD`</li></ul> |
| `customerDataFields.name` | Stringa | Specifica un nome per il campo personalizzato che stai introducendo. |
| `customerDataFields.type` | Stringa | Indica il tipo di campo personalizzato che si sta introducendo. I valori accettati sono `string`, `object`, `integer` |
| `customerDataFields.title` | Stringa | Indica il nome del campo, come visualizzato dai clienti nell’interfaccia utente di Experience Platform |
| `customerDataFields.description` | Stringa | Immetti una descrizione del campo personalizzato. |
| `customerDataFields.isRequired` | Booleano | Indica se questo campo è obbligatorio nel flusso di lavoro di configurazione della destinazione. |
| `customerDataFields.enum` | Stringa | Esegue il rendering del campo personalizzato come menu a discesa ed elenca le opzioni disponibili per l’utente. |
| `customerDataFields.pattern` | Stringa | Applica un pattern per il campo personalizzato, se necessario. Utilizzare espressioni regolari per applicare un pattern. Ad esempio, se gli ID cliente non includono numeri o caratteri di sottolineatura, immetti `^[A-Za-z]+$` in questo campo. |
| `uiAttributes.documentationLink` | Stringa | Si riferisce alla pagina della documentazione nel [Catalogo delle destinazioni](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) per la tua destinazione. Utilizzo `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, dove `YOURDESTINATION` è il nome della destinazione. Per una destinazione denominata Moviestar, puoi utilizzare `https://www.adobe.com/go/destinations-moviestar-en`. |
| `uiAttributes.category` | Stringa | Si riferisce alla categoria assegnata alla destinazione in Adobe Experience Platform. Per ulteriori informazioni, leggere [Categorie di destinazione](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Utilizzare uno dei seguenti valori: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `uiAttributes.connectionType` | Stringa | `Server-to-server` al momento è l’unica opzione disponibile. |
| `uiAttributes.frequency` | Stringa | `Streaming` al momento è l’unica opzione disponibile. |
| `identityNamespaces.externalId.acceptsAttributes` | Booleano | Indica se la destinazione accetta attributi di profilo standard. Di solito, questi attributi sono evidenziati nella documentazione dei nostri partner. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Booleano | Indica se i clienti possono impostare spazi dei nomi personalizzati nella destinazione. |
| `identityNamespaces.externalId.transformation` | Stringa | _Non mostrato nella configurazione di esempio_. Utilizzato, ad esempio, quando [!DNL Platform] il cliente ha indirizzi e-mail semplici come attributo e la tua piattaforma accetta solo e-mail con hash. Qui puoi fornire la trasformazione da applicare (ad esempio, trasforma l’e-mail in minuscolo e quindi hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Utilizzato per i casi in cui la piattaforma accetta [spazi dei nomi delle identità standard](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (ad esempio, IDFA), in modo da poter limitare gli utenti di Platform a selezionare solo questi namespace di identità. <br> Quando utilizzi `acceptedGlobalNamespaces`, puoi utilizzare `"requiredTransformation":"sha256(lower($))"` per gli indirizzi e-mail o i numeri di telefono in lettere minuscole e hash. |
| `destinationDelivery.authenticationRule` | Stringa | Indica come [!DNL Platform] i clienti si connettono alla destinazione. I valori accettati sono `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilizzo `CUSTOMER_AUTHENTICATION` se i clienti di Platform accedono al sistema tramite un nome utente e una password, un token portatore o un altro metodo di autenticazione. Ad esempio, puoi selezionare questa opzione se hai selezionato anche `authType: OAUTH2` o `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Utilizzo `PLATFORM_AUTHENTICATION` se esiste un sistema di autenticazione globale tra l’Adobe e la destinazione e [!DNL Platform] il cliente non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso è necessario creare un oggetto credenziali utilizzando [Credenziali](./credentials-configuration-api.md) configurazione. </li><li>Utilizzo `NONE` se non è richiesta alcuna autenticazione per inviare dati alla piattaforma di destinazione. </li></ul> |
| `destinationDelivery.destinationServerId` | Stringa | La `instanceId` del [modello server di destinazione](./destination-server-api.md) utilizzato per questa destinazione. |
| `backfillHistoricalProfileData` | Booleano | Controlla se i dati storici del profilo vengono esportati quando i segmenti vengono attivati nella destinazione. <br> <ul><li> `true`: [!DNL Platform] invia i profili utente storici qualificati per il segmento prima che il segmento venga attivato. </li><li> `false`: [!DNL Platform] include solo i profili utente qualificati per il segmento dopo l’attivazione del segmento. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Booleano | Controlla se l&#39;ID di mappatura del segmento nel flusso di lavoro di attivazione della destinazione viene immesso dall&#39;utente. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Booleano | Controlla se l&#39;ID di mappatura del segmento nel flusso di lavoro di attivazione della destinazione è l&#39;ID del segmento di Experience Platform. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Booleano | Controlla se l&#39;ID di mappatura del segmento nel flusso di lavoro di attivazione della destinazione è il nome del segmento di Experience Platform. |
| `segmentMappingConfig.audienceTemplateId` | Booleano | La `instanceId` del [modello di metadati del pubblico](./audience-metadata-api.md) utilizzato per questa destinazione. |
| `schemaConfig.profileFields` | Array | Quando si aggiungono predefiniti `profileFields` come mostrato nella configurazione precedente, gli utenti avranno la possibilità di mappare gli attributi Experienci Platform agli attributi predefiniti sul lato della destinazione. |
| `schemaConfig.profileRequired` | Booleano | Utilizzo `true` se gli utenti devono essere in grado di mappare gli attributi di profilo dall’Experience Platform agli attributi personalizzati sul lato della destinazione, come illustrato nella configurazione di esempio precedente. |
| `schemaConfig.segmentRequired` | Booleano | Usa sempre `segmentRequired:true`. |
| `schemaConfig.identityRequired` | Booleano | Utilizzo `true` se gli utenti devono essere in grado di mappare i namespace di identità dall&#39;Experience Platform allo schema desiderato. |
| `aggregation.aggregationType` | - | Seleziona `BEST_EFFORT` o `CONFIGURABLE_AGGREGATION`. La configurazione di esempio di cui sopra include `BEST_EFFORT` aggregazione. Per un esempio di `CONFIGURABLE_AGGREGATION`, fai riferimento alla configurazione di esempio nel [configurazione di destinazione](./destination-configuration.md#example-configuration) documento. I parametri relativi all’aggregazione configurabile sono indicati di seguito in questa tabella. |
| `aggregation.bestEffortAggregation.maxUsersPerRequest` | Intero | Experience Platform può aggregare più profili esportati in una singola chiamata HTTP. Specifica il numero massimo di profili che l&#39;endpoint deve ricevere in una singola chiamata HTTP. Tieni presente che si tratta di un’aggregazione dello sforzo migliore. Ad esempio, se specifichi il valore 100, Platform potrebbe inviare un numero qualsiasi di profili inferiore a 100 in una chiamata . <br> Se il server non accetta più utenti per richiesta, imposta questo valore su 1. |
| `aggregation.bestEffortAggregation.splitUserById` | Booleano | Usa questo flag se la chiamata alla destinazione deve essere divisa per identità. Imposta questo flag su `true` se il server accetta una sola identità per chiamata, per un determinato namespace. |
| `aggregation.configurableAggregation.splitUserById` | Booleano | Vedi parametro nella configurazione di esempio [qui](./destination-configuration.md#example-configuration). Usa questo flag se la chiamata alla destinazione deve essere divisa per identità. Imposta questo flag su `true` se il server accetta una sola identità per chiamata, per un determinato namespace. |
| `aggregation.configurableAggregation.maxBatchAgeInSecs` | Intero | <ul><li>*Valore minimo: 1800*</li><li>*Valore massimo: 3600*</li><li>Vedi parametro nella configurazione di esempio [qui](./destination-configuration.md#example-configuration). Configura un valore compreso tra il valore minimo e il valore massimo accettato. Insieme con `maxNumEventsInBatch`, questo parametro determina per quanto tempo Experience Platform deve aspettare fino all’invio di una chiamata API all’endpoint. <br> Ad esempio, se utilizzi il valore massimo per entrambi i parametri, Experience Platform attenderà 3600 secondi OR fino a quando non saranno disponibili 10.000 profili qualificati prima di effettuare la chiamata API, a seconda di quale dei due eventi si verifica per primo. </li></ul> |
| `aggregation.configurableAggregation.maxNumEventsInBatch` | Intero | <ul><li>*Valore minimo: 1000*</li><li>*Valore massimo: 10000*</li><li>Vedi parametro nella configurazione di esempio [qui](./destination-configuration.md#example-configuration). Configura un valore compreso tra il valore minimo e il valore massimo accettato. Per una descrizione di questo parametro, vedi `maxBatchAgeInSecs` appena sopra.</li></ul> |
| `aggregation.configurableAggregation.aggregationKey` | Booleano | Vedi parametro nella configurazione di esempio [qui](./destination-configuration.md#example-configuration). Consente di aggregare i profili esportati mappati alla destinazione in base ai parametri seguenti: <br> <ul><li>ID segmento</li><li> stato del segmento </li><li> spazio dei nomi identità </li></ul> |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentId` | Booleano | Vedi parametro nella configurazione di esempio [qui](./destination-configuration.md#example-configuration). Imposta questo su `true` se desideri raggruppare i profili esportati nella destinazione per ID segmento. |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentStatus` | Booleano | Vedi parametro nella configurazione di esempio [qui](./destination-configuration.md#example-configuration). È necessario impostare entrambi `includeSegmentId:true` e `includeSegmentStatus:true` se desideri raggruppare i profili esportati nella destinazione per ID segmento E stato del segmento. |
| `aggregation.configurableAggregation.aggregationKey.includeIdentity` | Booleano | Vedi parametro nella configurazione di esempio [qui](./destination-configuration.md#example-configuration). Imposta questo su `true` per raggruppare i profili esportati nella destinazione in base allo spazio dei nomi identità. |
| `aggregation.configurableAggregation.aggregationKey.oneIdentityPerGroup` | Booleano | Vedi parametro nella configurazione di esempio [qui](./destination-configuration.md#example-configuration). Usa questo parametro per specificare se desideri che i profili esportati siano aggregati in gruppi di una singola identità (GAID, IDFA, numeri di telefono, e-mail, ecc.). |
| `aggregation.configurableAggregation.aggregationKey.groups` | Stringa | Vedi parametro nella configurazione di esempio [qui](./destination-configuration.md#example-configuration). Crea elenchi di gruppi di identità se desideri raggruppare i profili esportati nella destinazione per gruppi di namespace di identità. Ad esempio, puoi combinare profili che contengono gli identificatori mobili IDFA e GAID in una chiamata alla tua destinazione ed e-mail in un&#39;altra utilizzando la configurazione nell&#39;esempio. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della configurazione di destinazione appena creata.

## Creare una configurazione per una destinazione basata su file {#create-file-based}

Puoi creare una nuova configurazione di destinazione effettuando una richiesta di POST al `/authoring/destinations` punto finale.

**Formato API**

```http
POST /authoring/destinations
```

**Richiesta**

La seguente richiesta crea una nuova [!DNL Amazon S3] configurazione di destinazione basata su file, configurata dai parametri forniti nel payload. Il payload seguente include tutti i parametri per le destinazioni basate su file accettate dal `/authoring/destinations` punto finale. Non è necessario aggiungere tutti i parametri alla chiamata e il modello è personalizzabile, in base ai requisiti API.

```json
{
        "name": "S3 Destination with CSV Options",
        "description": "S3 Destination with CSV Options",
        "releaseNotes": "S3 Destination with CSV Options",
        "status": "TEST",
        "customerAuthenticationConfigurations": [
            {
                "authType": "S3"
            }
        ],
        "customerEncryptionConfigurations": [
            {
                "encryptionAlgo": ""
            }
        ],
        "customerDataFields": [
            {
                "name": "bucket",
                "title": "Select S3 Bucket",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "path",
                "title": "S3 path",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "pattern": "^[A-Za-z]+$",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "sep",
                "title": "Select separator for each field and value",
                "description": "Select for each field and value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "encoding",
                "title": "Specify encoding (charset) of saved CSV files",
                "description": "Select encoding of csv files",
                "type": "string",
                "enum": ["UTF-8", "UTF-16"],
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quote",
                "title": "Select a single character used for escaping quoted values",
                "description": "Select single charachter for escaping quoted values",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quoteAll",
                "title": "Quote All",
                "description": "Select flag for escaping quoted values",
                "type": "string",
                "enum" : ["true","false"],
                "default": "true",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "escape",
                "title": "Select a single character used for escaping quotes",
                "description": "Select a single character used for escaping quotes inside an already quoted value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "escapeQuotes",
                "title": "Escape quotes",
                "description": "A flag indicating whether values containing quotes should always be enclosed in quotes",
                "type": "string",
                "enum" : ["true","false"],
                "isRequired": false,
                "default": "true",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "header",
                "title": "header",
                "description": "Writes the names of columns as the first line.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "ignoreLeadingWhiteSpace",
                "title": "Ignore leading white space",
                "description": "A flag indicating whether or not leading whitespaces from values being written should be skipped.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "nullValue",
                "title": "Select the string representation of a null value",
                "description": "Sets the string representation of a null value. ",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "dateFormat",
                "title": "Date format",
                "description": "Select the string that indicates a date format. ",
                "type": "string",
                "default": "yyyy-MM-dd",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "charToEscapeQuoteEscaping",
                "title": "Char to escape quote escaping",
                "description": "Sets a single character used for escaping the escape for the quote character",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "emptyValue",
                "title": "Select the string representation of an empty value",
                "description": "Select the string representation of an empty value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "default": "",
                "hidden": false
            },
            {
                "name": "compression",
                "title": "Select compression",
                "description": "Select compressiont",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "enum" : ["SNAPPY","GZIP","DEFLATE", "NONE"]
            },
            {
                "name": "fileType",
                "title": "Select a fileType",
                "description": "Select fileType",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false,
                "enum" :["csv", "json", "parquet"],
                "default" : "csv"
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
                "deliveryMatchers" : [
                    {
                        "type" : "SOURCE",
                        "value" : [
                            "batch"
                        ]
                    }
                ],
                "authenticationRule": "CUSTOMER_AUTHENTICATION",
                "destinationServerId": "{{destinationServerId}}"
            }
        ],
        "schemaConfig" : {
            "profileRequired" : true,
            "segmentRequired" : true,
            "identityRequired" : true
        },
        "batchConfig":{
            "allowMandatoryFieldSelection": true,
            "allowJoinKeyFieldSelection": true,
            "defaultExportMode": "DAILY_FULL_EXPORT",
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
            "defaultStartTime":"00:00"
        },
        "backfillHistoricalProfileData": true
    }
```

Per una descrizione dettagliata di tutti i parametri di cui sopra, vedi [configurazione di destinazione basata su file](file-based-destination-configuration.md).

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della configurazione di destinazione appena creata.

## Elenca configurazioni di destinazione {#retrieve-list}

Puoi recuperare un elenco di tutte le configurazioni di destinazione per la tua organizzazione IMS effettuando una richiesta di GET al `/authoring/destinations` punto finale.

**Formato API**


```http
GET /authoring/destinations
```

**Richiesta**

La richiesta seguente recupererà l’elenco delle configurazioni di destinazione a cui hai accesso, in base alla configurazione dell’organizzazione IMS e della sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta seguente restituisce lo stato HTTP 200 con un elenco di configurazioni di destinazione a cui hai accesso, in base all’ID organizzazione IMS e al nome della sandbox utilizzati. Uno `instanceId` corrisponde al modello per una destinazione. La risposta viene troncata per brevità.

```json
{
   "items":[
      {
         "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
         "createdDate":"2020-10-28T06:14:09.784471Z",
         "lastModifiedDate":"2021-06-28T06:14:09.784471Z",
         "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
         "sandboxName":"prod",
         "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
         "name":"Moviestar",
         "description":"Moviestar is a fictional destination, used for this example.",
         "status":"TEST",
         "customerAuthenticationConfigurations":[
            {
               "authType":"BEARER"
            }
         ],
         "customerDataFields":[
            {
               "name":"endpointsInstance",
               "type":"string",
               "title":"Select Endpoint",
               "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
               "isRequired":true,
               "enum":[
                  "US",
                  "EU",
                  "APAC",
                  "NZ"
               ]
            },
            {
               "name":"customerID",
               "type":"string",
               "title":"Moviestar Customer ID",
               "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
               "isRequired":true,
               "pattern":"^[A-Za-z]+$"
            }
         ],
         "uiAttributes":{
            "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
            "category":"mobile",
            "connectionType":"Server-to-server",
            "frequency":"Streaming"
         },
         "identityNamespaces":{
            "external_id":{
               "acceptsAttributes":true,
               "acceptsCustomNamespaces":true,
               "acceptedGlobalNamespaces":{
                  "Email":{
                     
                  }
               }
            },
            "another_id":{
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
                  "name":"a_custom_attribute",
                  "title":"a_custom_attribute",
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
         "aggregation":{
            "aggregationType":"BEST_EFFORT",
            "bestEffortAggregation":{
               "maxUsersPerRequest":10,
               "splitUserById":false
            }
         },
         "destinationDelivery":[
            {
               "authenticationRule":"CUSTOMER_AUTHENTICATION",
               "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
            }
         ],
         "destConfigId":"410631b8-f6b3-4b7c-82da-7998aa3f327c",
         "backfillHistoricalProfileData":true
      }
   ]
}
    
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `name` | Stringa | Indica il titolo della destinazione nel catalogo Experience Platform. |
| `description` | Stringa | Immetti una descrizione che Adobe utilizzerà nel catalogo delle destinazioni Experience Platform per la tua scheda di destinazione. Mirare a non più di 4-5 frasi. |
| `status` | Stringa | Indica lo stato del ciclo di vita della scheda di destinazione. I valori accettati sono `TEST`, `PUBLISHED` e `DELETED`. Utilizzo `TEST` la prima volta che configuri la destinazione. |
| `customerAuthenticationConfigurations` | Stringa | Indica la configurazione utilizzata per autenticare i clienti Experience Platform nel server. Vedi `authType` di seguito per i valori accettati. |
| `customerAuthenticationConfigurations.authType` | Stringa | I valori accettati sono `OAUTH2, BEARER`. |
| `customerDataFields.name` | Stringa | Specifica un nome per il campo personalizzato che stai introducendo. |
| `customerDataFields.type` | Stringa | Indica il tipo di campo personalizzato che si sta introducendo. I valori accettati sono `string`, `object`, `integer` |
| `customerDataFields.title` | Stringa | Indica il nome del campo, come visualizzato dai clienti nell’interfaccia utente di Experience Platform |
| `customerDataFields.description` | Stringa | Immetti una descrizione del campo personalizzato. |
| `customerDataFields.isRequired` | Booleano | Indica se questo campo è obbligatorio nel flusso di lavoro di configurazione della destinazione. |
| `customerDataFields.enum` | Stringa | Esegue il rendering del campo personalizzato come menu a discesa ed elenca le opzioni disponibili per l’utente. |
| `customerDataFields.pattern` | Stringa | Applica un pattern per il campo personalizzato, se necessario. Utilizzare espressioni regolari per applicare un pattern. Ad esempio, se gli ID cliente non includono numeri o caratteri di sottolineatura, immetti `^[A-Za-z]+$` in questo campo. |
| `uiAttributes.documentationLink` | Stringa | Si riferisce alla pagina della documentazione nel [Catalogo delle destinazioni](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) per la tua destinazione. Utilizzo `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, dove `YOURDESTINATION` è il nome della destinazione. Per una destinazione denominata Moviestar, puoi utilizzare `https://www.adobe.com/go/destinations-moviestar-en` |
| `uiAttributes.category` | Stringa | Si riferisce alla categoria assegnata alla destinazione in Adobe Experience Platform. Per ulteriori informazioni, leggere [Categorie di destinazione](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Utilizzare uno dei seguenti valori: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments` |
| `uiAttributes.connectionType` | Stringa | `Server-to-server` al momento è l’unica opzione disponibile. |
| `uiAttributes.frequency` | Stringa | `Streaming` al momento è l’unica opzione disponibile. |
| `identityNamespaces.externalId.acceptsAttributes` | Booleano | Indica se la destinazione accetta attributi di profilo standard. Di solito, questi attributi sono evidenziati nella documentazione dei nostri partner. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Booleano | Indica se i clienti possono impostare spazi dei nomi personalizzati nella destinazione. Ulteriori informazioni [spazi dei nomi personalizzati](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#manage-namespaces) in Adobe Experience Platform. |
| `identityNamespaces.externalId.transformation` | Stringa | _Non mostrato nella configurazione di esempio_. Utilizzato, ad esempio, quando [!DNL Platform] il cliente ha indirizzi e-mail semplici come attributo e la tua piattaforma accetta solo e-mail con hash. Qui puoi fornire la trasformazione da applicare (ad esempio, trasforma l’e-mail in minuscolo e quindi hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Utilizzato per i casi in cui la piattaforma accetta [spazi dei nomi delle identità standard](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (ad esempio, IDFA), in modo da poter limitare gli utenti di Platform a selezionare solo questi namespace di identità. |
| `destinationDelivery.authenticationRule` | Stringa | Indica come [!DNL Platform] i clienti si connettono alla destinazione. I valori accettati sono `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilizzo `CUSTOMER_AUTHENTICATION` se i clienti di Platform accedono al sistema tramite un nome utente e una password, un token portatore o un altro metodo di autenticazione. Ad esempio, puoi selezionare questa opzione se hai selezionato anche `authType: OAUTH2` o `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Utilizzo `PLATFORM_AUTHENTICATION` se esiste un sistema di autenticazione globale tra l’Adobe e la destinazione e [!DNL Platform] il cliente non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso è necessario creare un oggetto credenziali utilizzando [Credenziali](./authentication-configuration.md) configurazione. </li><li>Utilizzo `NONE` se non è richiesta alcuna autenticazione per inviare dati alla piattaforma di destinazione. </li></ul> |
| `destinationDelivery.destinationServerId` | Stringa | La `instanceId` del [modello server di destinazione](./destination-server-api.md) utilizzato per questa destinazione. |
| `destConfigId` | Stringa | Questo campo viene generato automaticamente e non richiede l’input. |
| `backfillHistoricalProfileData` | Booleano | Controlla se i dati storici del profilo vengono esportati quando i segmenti vengono attivati nella destinazione. <br> <ul><li> `true`: [!DNL Platform] invia i profili utente storici qualificati per il segmento prima che il segmento venga attivato. </li><li> `false`: [!DNL Platform] include solo i profili utente qualificati per il segmento dopo l’attivazione del segmento. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Booleano | Controlla se l&#39;ID di mappatura del segmento nel flusso di lavoro di attivazione della destinazione viene immesso dall&#39;utente. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Booleano | Controlla se l&#39;ID di mappatura del segmento nel flusso di lavoro di attivazione della destinazione è l&#39;ID del segmento di Experience Platform. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Booleano | Controlla se l&#39;ID di mappatura del segmento nel flusso di lavoro di attivazione della destinazione è il nome del segmento di Experience Platform. |
| `segmentMappingConfig.audienceTemplateId` | Booleano | La `instanceId` del [modello di metadati del pubblico](./audience-metadata-management.md) utilizzato per questa destinazione. Per impostare un modello di metadati del pubblico, leggi la sezione [riferimento API per metadati del pubblico](./audience-metadata-api.md). |

{style=&quot;table-layout:auto&quot;}

## Aggiornare una configurazione di destinazione esistente {#update}

Puoi aggiornare una configurazione di destinazione esistente effettuando una richiesta di PUT al `/authoring/destinations` e fornisce l&#39;ID istanza della configurazione di destinazione che desideri aggiornare. Nel corpo della chiamata , fornisci la configurazione di destinazione aggiornata.

**Formato API**


```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID della configurazione di destinazione da aggiornare. |

**Richiesta**

La richiesta seguente aggiorna una configurazione di destinazione esistente, configurata dai parametri forniti nel payload. Nella chiamata di esempio seguente, stiamo aggiornando la configurazione [creato in precedenza](./destination-configuration-api.md#create) per ora accettare GAID, IDFA e identificatori e-mail con hash come spazi dei nomi di identità.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-04-28T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
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
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
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
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

## Recupera una configurazione di destinazione specifica {#get}

Puoi recuperare informazioni dettagliate su una configurazione di destinazione specifica effettuando una richiesta GET al `/authoring/destinations` e fornisce l&#39;ID istanza della configurazione di destinazione che desideri recuperare.

**Formato API**


```http
GET /authoring/destinations/{INSTANCE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID della configurazione di destinazione da recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sulla configurazione di destinazione specificata.

```json
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-06-04T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
               
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
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
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
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
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```


## Eliminare una configurazione di destinazione specifica {#delete}

Puoi eliminare la configurazione di destinazione specificata effettuando una richiesta di DELETE al `/authoring/destinations` e fornisce l’ID della configurazione di destinazione che desideri eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{INSTANCE_ID}` | La `id` della configurazione di destinazione che desideri eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 insieme a una risposta HTTP vuota.

## Gestione degli errori API

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come configurare la destinazione utilizzando `/authoring/destinations` Endpoint API. Leggi [come utilizzare Destination SDK per configurare la destinazione](./configure-destination-instructions.md) per capire dove si adatta questo passaggio al processo di configurazione della destinazione.
