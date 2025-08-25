---
description: Scopri come strutturare una chiamata API per creare una configurazione di destinazione tramite Adobe Experience Platform Destination SDK.
title: Creare una configurazione di destinazione
exl-id: aae4aaa8-1dd0-4041-a86c-5c86f04d7d13
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 3%

---

# Creare una configurazione di destinazione

Questa pagina esemplifica la richiesta API e il payload che è possibile utilizzare per creare la propria configurazione di destinazione, utilizzando l&#39;endpoint API `/authoring/destinations`.

Per una descrizione dettagliata delle funzionalità che puoi configurare tramite questo endpoint, leggi i seguenti articoli:

* [Configurazione autenticazione cliente](../../functionality/destination-configuration/customer-authentication.md)
* [Autorizzazione OAuth2](../../functionality/destination-configuration/oauth2-authorization.md)
* [Campi dati cliente](../../functionality/destination-configuration/customer-data-fields.md)
* [Attributi dell’interfaccia utente](../../functionality/destination-configuration/ui-attributes.md)
* [Configurazione dello schema](../../functionality/destination-configuration/schema-configuration.md)
* [Configurazione dello spazio dei nomi dell’identità](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [Consegna della destinazione](../../functionality/destination-configuration/destination-delivery.md)
* [Configurazione dei metadati del pubblico](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Configurazione dei metadati del pubblico](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Criterio di aggregazione](../../functionality/destination-configuration/aggregation-policy.md)
* [Configurazione batch](../../functionality/destination-configuration/batch-configuration.md)
* [Qualifiche del profilo storico](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API di configurazione di destinazione {#get-started}

Prima di continuare, consulta la [guida introduttiva](../../getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, tra cui come ottenere l&#39;autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Creare una configurazione di destinazione {#create}

È possibile creare una nuova configurazione di destinazione effettuando una richiesta POST all&#39;endpoint `/authoring/destinations`.

>[!TIP]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/destinations`

**Formato API**

```http
POST /authoring/destinations
```

La richiesta seguente crea una nuova configurazione di destinazione [!DNL Amazon S3], configurata dai parametri forniti nel payload. Il payload seguente include tutti i parametri per le destinazioni basate su file accettate dall&#39;endpoint `/authoring/destinations`.

Tieni presente che non è necessario aggiungere tutti i parametri alla chiamata API e che il payload è personalizzabile in base ai requisiti API.

+++Richiesta

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Amazon S3 destination with predefined CSV formatting options",
   "description":"Amazon S3 destination with predefined CSV formatting options",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerDataFields":[
      {
         "name":"bucket",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
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
      "documentationLink":"https://www.adobe.com/go/destinations-amazon-s3-en",
      "category":"cloudStorage",
      "icon":{
         "key":"amazonS3"
      },
      "connectionType":"S3",
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

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `name` | Stringa | Indica il titolo della destinazione nel catalogo Experience Platform. |
| `description` | Stringa | Fornisci una descrizione che Adobe utilizzerà nel catalogo delle destinazioni di Experience Platform per la tua scheda di destinazione. Puntare a non più di 4-5 frasi. ![Immagine dell&#39;interfaccia utente di Experience Platform con la descrizione della destinazione.](../../assets/authoring-api/destination-configuration/destination-description.png "Descrizione destinazione"){width="100" zoomable="yes"} |
| `status` | Stringa | Indica lo stato del ciclo di vita della scheda di destinazione. I valori accettati sono `TEST`, `PUBLISHED` e `DELETED`. Utilizza `TEST` quando configuri per la prima volta la destinazione. |
| `customerAuthenticationConfigurations.authType` | Stringa | Indica la configurazione utilizzata per autenticare i clienti Experience Platform nel server di destinazione. Per informazioni dettagliate sui tipi di autenticazione supportati, vedere [configurazione dell&#39;autenticazione del cliente](../../functionality/destination-configuration/customer-authentication.md). |
| `customerDataFields.name` | Stringa | Immetti un nome per il campo personalizzato che stai presentando. <br/><br/> Per informazioni dettagliate su queste impostazioni, vedere [Campi dati cliente](../../functionality/destination-configuration/customer-data-fields.md). ![Immagine dell&#39;interfaccia utente di Experience Platform con i campi dei dati del cliente.](../../assets/authoring-api/destination-configuration/customer-data-fields.png "Campo dati cliente"){width="100" zoomable="yes"} |
| `customerDataFields.type` | Stringa | Indica il tipo di campo personalizzato che si sta introducendo. I valori accettati sono `string`, `object`, `integer`. <br/><br/> Per informazioni dettagliate su queste impostazioni, vedere [Campi dati cliente](../../functionality/destination-configuration/customer-data-fields.md). |
| `customerDataFields.title` | Stringa | Indica il nome del campo, così come viene visualizzato dai clienti nell’interfaccia utente di Experience Platform. <br/><br/> Per informazioni dettagliate su queste impostazioni, vedere [Campi dati cliente](../../functionality/destination-configuration/customer-data-fields.md). |
| `customerDataFields.description` | Stringa | Fornisci una descrizione per il campo personalizzato. Per informazioni dettagliate su queste impostazioni, vedere [Campi dati cliente](../../functionality/destination-configuration/customer-data-fields.md). |
| `customerDataFields.isRequired` | Booleano | Indica se questo campo è obbligatorio nel flusso di lavoro di configurazione della destinazione. <br/><br/> Per informazioni dettagliate su queste impostazioni, vedere [Campi dati cliente](../../functionality/destination-configuration/customer-data-fields.md). |
| `customerDataFields.enum` | Stringa | Esegue il rendering del campo personalizzato come menu a discesa ed elenca le opzioni disponibili per l&#39;utente. <br/><br/> Per informazioni dettagliate su queste impostazioni, vedere [Campi dati cliente](../../functionality/destination-configuration/customer-data-fields.md). |
| `customerDataFields.default` | Stringa | Definisce il valore predefinito da un elenco `enum`. |
| `customerDataFields.pattern` | Stringa | Se necessario, applica un pattern per il campo personalizzato. Utilizza espressioni regolari per applicare un pattern. Ad esempio, se gli ID cliente non includono numeri o trattini bassi, immetti `^[A-Za-z]+$` in questo campo. <br/><br/> Per informazioni dettagliate su queste impostazioni, vedere [Campi dati cliente](../../functionality/destination-configuration/customer-data-fields.md). |
| `uiAttributes.documentationLink` | Stringa | Fa riferimento alla pagina della documentazione nel [Catalogo destinazioni](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=it#catalog) per la tua destinazione. Utilizza `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, dove `YOURDESTINATION` è il nome della tua destinazione. Per una destinazione denominata Moviestar, si utilizza `https://www.adobe.com/go/destinations-moviestar-en`. Tieni presente che questo collegamento funziona solo dopo che Adobe ha impostato la destinazione in tempo reale e ha pubblicato la documentazione. <br/><br/> Per informazioni dettagliate su queste impostazioni, vedere [Attributi dell&#39;interfaccia utente](../../functionality/destination-configuration/ui-attributes.md). ![Immagine dell&#39;interfaccia utente di Experience Platform con il collegamento alla documentazione.](../../assets/authoring-api/destination-configuration/documentation-url.png "URL documentazione"){width="100" zoomable="yes"} |
| `uiAttributes.category` | Stringa | Fa riferimento alla categoria assegnata alla destinazione in Adobe Experience Platform. Per ulteriori informazioni, leggere [Categorie di destinazione](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=it#destination-categories). Utilizzare uno dei valori seguenti: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. <br/><br/> Per informazioni dettagliate su queste impostazioni, vedere [Attributi dell&#39;interfaccia utente](../../functionality/destination-configuration/ui-attributes.md). |
| `uiAttributes.connectionType` | Stringa | Il tipo di connessione, a seconda della destinazione. Valori supportati: <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul> |
| `uiAttributes.frequency` | Stringa | Si riferisce al tipo di esportazione dei dati supportato dalla destinazione. Impostato su `Streaming` per le integrazioni basate su API, oppure su `Batch` quando si esportano file nelle destinazioni. |
| `identityNamespaces.externalId.acceptsAttributes` | Booleano | Indica se i clienti possono mappare gli attributi di profilo standard all’identità che stai configurando. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Booleano | Indica se i clienti possono mappare le identità appartenenti a [spazi dei nomi personalizzati](/help/identity-service/features/namespaces.md#manage-namespaces) all&#39;identità che si sta configurando. |
| `identityNamespaces.externalId.transformation` | Stringa | _Non visualizzato nella configurazione di esempio_. Utilizzato, ad esempio, quando il cliente [!DNL Experience Platform] ha come attributo indirizzi e-mail semplici e la tua piattaforma accetta solo e-mail con hash. Qui puoi fornire la trasformazione da applicare (ad esempio, trasformare l’e-mail in minuscolo, quindi in hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Indica quali [spazi dei nomi di identità standard](/help/identity-service/features/namespaces.md#standard) (ad esempio, IDFA) i clienti possono mappare all&#39;identità che stai configurando. <br> Quando si utilizza `acceptedGlobalNamespaces`, è possibile utilizzare `"requiredTransformation":"sha256(lower($))"` per inserire indirizzi e-mail o numeri di telefono in minuscolo e con hash. |
| `destinationDelivery.authenticationRule` | Stringa | Indica come [!DNL Experience Platform] clienti si connettono alla destinazione. I valori accettati sono `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilizza `CUSTOMER_AUTHENTICATION` se i clienti di Experience Platform accedono al tuo sistema tramite un nome utente e una password, un token Bearer o un altro metodo di autenticazione. Ad esempio, è possibile selezionare questa opzione se si seleziona anche `authType: OAUTH2` o `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Utilizzare `PLATFORM_AUTHENTICATION` se esiste un sistema di autenticazione globale tra Adobe e la destinazione e il cliente [!DNL Experience Platform] non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso, è necessario creare un oggetto credenziali utilizzando la configurazione [credentials API](../../credentials-api/create-credential-configuration.md) e passare l&#39;ID dell&#39;oggetto credenziali nel parametro `authenticationId` nella configurazione [destination delivery](/help/destinations/destination-sdk/functionality/destination-configuration/destination-delivery.md#platform-authentication). </li><li>Utilizza `NONE` se non è richiesta alcuna autenticazione per inviare dati alla piattaforma di destinazione. </li></ul> |
| `destinationDelivery.destinationServerId` | Stringa | `instanceId` del [modello del server di destinazione](../destination-server/create-destination-server.md) utilizzato per questa destinazione. |
| `backfillHistoricalProfileData` | Booleano | Controlla se i dati storici del profilo vengono esportati quando i tipi di pubblico vengono attivati nella destinazione. Imposta sempre `true`. |
| `segmentMappingConfig.mapUserInput` | Booleano | Controlla se l’ID di mappatura del pubblico nel flusso di lavoro di attivazione della destinazione viene immesso dall’utente. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Booleano | Controlla se l’ID di mappatura del pubblico nel flusso di lavoro di attivazione della destinazione è l’ID del pubblico di Experience Platform. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Booleano | Controlla se l’ID di mappatura del pubblico nel flusso di lavoro di attivazione della destinazione è il nome del pubblico di Experience Platform. |
| `segmentMappingConfig.audienceTemplateId` | Stringa | `instanceId` del [modello di metadati del pubblico](../../metadata-api/create-audience-template.md) utilizzato per questa destinazione. |
| `schemaConfig.profileFields` | Array | Quando si aggiunge `profileFields` predefinito come mostrato nella configurazione precedente, gli utenti avranno la possibilità di mappare gli attributi di Experience Platform agli attributi predefiniti sul lato della destinazione. |
| `schemaConfig.profileRequired` | Booleano | Utilizza `true` se gli utenti devono essere in grado di mappare gli attributi del profilo da Experience Platform agli attributi personalizzati sul lato della destinazione, come mostrato nella configurazione di esempio precedente. |
| `schemaConfig.segmentRequired` | Booleano | Usa sempre `segmentRequired:true`. |
| `schemaConfig.identityRequired` | Booleano | Utilizza `true` se gli utenti devono essere in grado di mappare gli spazi dei nomi delle identità da Experience Platform allo schema desiderato. |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della nuova configurazione di destinazione creata.

+++

## Gestione degli errori API

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](../../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Experience Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come creare una nuova configurazione di destinazione tramite l&#39;endpoint API `/authoring/destinations` di Destination SDK.

Per ulteriori informazioni su cosa è possibile fare con questo endpoint, consulta i seguenti articoli:

* [Recuperare una configurazione di destinazione](retrieve-destination-configuration.md)
* [Aggiornare una configurazione di destinazione](update-destination-configuration.md)
* [Eliminare una configurazione di destinazione](delete-destination-configuration.md)

Per capire dove questo endpoint si inserisce nel processo di authoring della destinazione, vedi i seguenti articoli:

* [Utilizzare Destination SDK per configurare una destinazione di streaming](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Utilizzare Destination SDK per configurare una destinazione basata su file](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)
