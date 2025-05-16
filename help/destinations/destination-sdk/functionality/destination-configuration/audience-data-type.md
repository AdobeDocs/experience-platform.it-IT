---
description: Scopri come configurare il tipo di pubblico per le destinazioni create con Destination SDK.
title: Configurare il tipo di dati del pubblico
exl-id: c56fb0f9-adb2-4fb2-ab06-c0398d828600
source-git-commit: 5d84ea1baa96c288d9d37606122e0a41880478b9
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 2%

---

# Configurare il tipo di dati del pubblico

Quando crei un connettore di destinazione con Destination SDK, puoi definire il tipo di pubblico che verrà esportato nella tua destinazione. La configurazione del tipo di dati corretto per il pubblico garantisce che la destinazione riceva i dati corretti per il caso d’uso previsto, che si tratti di campagne di marketing, strategie basate su account o analisi di dati.

Leggi i tipi di dati sul pubblico riportati di seguito per scoprire le differenze tra di essi e identificare il tipo necessario per la tua integrazione. Quindi, leggi le sezioni riportate di seguito nella pagina per scoprire come configurare la tua destinazione per esportare diversi tipi di pubblico.

| Tipo di dati del pubblico | Descrizione | Casi d’uso |
|---------|----------|---------|
| [Tipi di pubblico per persone](../../../../segmentation/types/people-audiences.md) | In base ai profili dei clienti, consente di eseguire il targeting di gruppi specifici di persone per campagne di marketing. | Acquirenti frequenti, abbandoni del carrello |
| [Pubblico dell&#39;account](../../../../segmentation/types/account-audiences.md) | Puoi indirizzare l’attività a singoli utenti all’interno di organizzazioni specifiche per strategie di marketing basate sull’account. | Marketing B2B |
| [Pubblico potenziale](../../../../segmentation/types/prospect-audiences.md) | Puoi indirizzare l’attività a singoli utenti che non sono ancora clienti, ma che condividono alcune caratteristiche con il tuo pubblico di destinazione. | Ricerca di dati di terze parti |
| [Esportazioni set di dati](../../../../catalog/datasets/overview.md) | Raccolte di dati strutturati archiviati nel Data Lake di Adobe Experience Platform. | Reporting, flussi di lavoro di data science |

Il tipo di dati del pubblico supportato dipende dal tipo di destinazione creato.
Fai riferimento alla tabella seguente per capire quali tipi di destinazione supportano quali tipi di dati di pubblico.

| Tipo di destinazione | Pubblico persone | Pubblico dell’account | Pubblico potenziale | Set di dati |
|---------|----------|---------|---------|---------|
| Streaming | ✓ | ✓ | X | X |
| Basato su file | ✓ | ✓ | ✓ | ✓ |

{style="table-layout:auto"}

## L&#39;array `sources` {#sources}

L&#39;array `sources` specifica il tipo di dati del pubblico supportato dalla destinazione. È richiesta per i tipi di pubblico dell’account, i tipi di pubblico potenziali e le esportazioni di set di dati, ma non è necessaria per i tipi di pubblico delle persone, in quanto è supportata per impostazione predefinita.

```json
"sources":[
   "ACCOUNTS" // Specifies that this destination supports account audiences
]
```

L&#39;array `sources` accetta i seguenti valori:

* `"ACCOUNTS"`: specifica che la destinazione supporta l&#39;esportazione dei tipi di pubblico dell&#39;account.
* `"UNIFIED_PROFILE_PROSPECTS"`: specifica che la destinazione supporta l&#39;esportazione dei tipi di pubblico potenziali.
* `"DATASETS"`: specifica che la destinazione supporta l&#39;esportazione di set di dati.

A seconda del tipo di pubblico che desideri esportare nella destinazione, consulta le sezioni seguenti per esempi di configurazione della destinazione.

## Esporta tipi di pubblico per persone {#people-audiences}

I tipi di pubblico Persone sono supportati per impostazione predefinita per tutti i tipi di destinazione e non richiedono un valore `sources` specifico. Per creare una destinazione che supporti i tipi di pubblico people, non è necessario utilizzare l&#39;array `sources`, in quanto si tratta del comportamento predefinito.

+++ Esempio di configurazione della destinazione di streaming con supporto per il pubblico di persone

Questo è un esempio di destinazione di streaming che esporta i tipi di pubblico delle persone. Si noti che non è presente alcun array `sources` nella configurazione.&quot;

```shell
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
         "pattern":""
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false
   },
   "audienceMetadataConfig":{
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "aggregationPolicyId":null,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":null
         },
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ]
}
```

+++

## Esporta tipi di pubblico account {#account}

Prendere in considerazione l&#39;aggiunta del supporto per il pubblico dell&#39;account alla destinazione quando si desidera configurare una destinazione [!DNL B2B] per il marketing basato sull&#39;account. È ad esempio possibile utilizzare i tipi di pubblico basati sull&#39;account per recuperare i record di tutti gli account che non dispongono di informazioni di contatto per le persone con titolo [!DNL Chief Operating Officer (COO)] o [!DNL Chief Marketing Officer (CMO)].

Per creare una destinazione che supporti l&#39;esportazione dei tipi di pubblico dell&#39;account, aggiungi lo snippet di configurazione seguente alla [configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md).

```json
"sources":[
   "ACCOUNTS" // Specifies that this destination supports account audiences
] 
```

+++ Esempio di configurazione della destinazione di streaming con supporto per il pubblico dell’account

```shell {line-numbers="true" highlight="12-14"}
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
   "sources":[
      "ACCOUNTS"
   ],
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
         "pattern":""
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false
   },
   "audienceMetadataConfig":{
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "aggregationPolicyId":null,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":null
         },
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ]
}
```

+++

## Esporta tipi di pubblico potenziali {#prospect}

Prendi in considerazione l’aggiunta del supporto per il pubblico potenziale alla tua destinazione quando desideri eseguire il targeting di individui che non sono ancora clienti ma che condividono caratteristiche con il pubblico di destinazione. Con i profili di potenziali clienti, puoi integrare i profili dei clienti con attributi di partner di terze parti affidabili. Per ulteriori informazioni, consulta questo [caso di utilizzo per la ricerca di potenziali clienti](../../../../rtcdp/partner-data/prospecting.md).

Per creare una destinazione che supporti l&#39;esportazione di pubblici potenziali, aggiungi lo snippet di configurazione seguente alla [configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md).


```json
"sources":[
   "UNIFIED_PROFILE_PROSPECTS" // Specifies that this destination supports prospect audiences
] 
```

+++ Esempio di configurazione della destinazione di streaming con supporto di audience prospect

```shell {line-numbers="true" highlight="12-14"}
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
   "sources":[
      "UNIFIED_PROFILE_PROSPECTS"
   ],
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"bucketName",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
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
            "GZIP",
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
            "json",
            "parquet"
         ],
         "default":"parquet"
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false
   },
   "audienceMetadataConfig":{
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "aggregationPolicyId":null,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":null
         },
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ]
}
```

+++

## Esporta set di dati {#datasets}

Prendi in considerazione l’aggiunta del supporto per l’esportazione dei set di dati nella destinazione quando desideri esportare set di dati non elaborati, che non sono raggruppati o strutturati in base agli interessi o alle qualifiche del pubblico. Puoi utilizzare questi dati per reporting, flussi di lavoro sulla scienza dei dati e molti altri casi d’uso. Ad esempio, in qualità di amministratore, ingegnere dati o analista, puoi esportare dati da Experience Platform per sincronizzarli con il tuo data warehouse, utilizzarli negli strumenti di analisi [!DNL BI], negli strumenti per il cloud esterno [!DNL ML] o archiviarli nel tuo sistema per esigenze di archiviazione a lungo termine.

Per creare una destinazione che supporti l&#39;esportazione di set di dati, aggiungi lo snippet di configurazione seguente alla [configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md).

```json
"sources":[
   "DATASETS" // Specifies that this destination supports dataset exports
]
```

+++ Esempio di configurazione della destinazione basata su file con supporto per l’esportazione del set di dati

```shell {line-numbers="true" highlight="12-14"}
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Amazon S3 destination with dataset export capability",
   "description":"Amazon S3 destination with dataset export capability",
   "status":"TEST",
   "sources":[
      "DATASETS"
   ],
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerDataFields":[
      {
         "name":"bucketName",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
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
            "GZIP",
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
            "json",
            "parquet"
         ],
         "default":"parquet"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-dataset-export-en",
      "category":"cloudStorage",
      "frequency":"Batch",
      "monitoringSupported":true,
      "flowRunsSupported":true
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"19c8fc89-9b73-4e0f-893e-549410b23f39"
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT"
   },
   "destinationDelivery":[
      {
         "authenticationRule":"PLATFORM_AUTHENTICATION",
         "authenticationId":"2fff57e1-6603-4927-8a9c-147c90839bdb",
         "destinationServerId":"e59de90a-6df6-471a-bd55-11f7bdb52fae"
      }
   ],
   "inputSchemaId":"70d0bd4734cc49c98d48c4b162e9a1b7",
   "schemaConfig":{
      "useCustomerSchemaForAttributeMapping":false,
      "requiredMappingsOnly":false,
      "profileRequired":false,
      "segmentRequired":false,
      "identityRequired":false
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":false,
      "autoSelectJoinKeyOnPartnerSchemaSelection":false,
      "joinKeyTitle":"DEDUPLICATION KEY",
      "defaultExportMode":"FIRST_FULL_THEN_INCREMENTAL",
      "allowedExportModes":[
         
      ],
      "allowedScheduleFrequency":[
         
      ],
      "defaultFrequency":"EVERY_HOUR",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            
         ],
         "defaultFilenameAppendOptions":[
            
         ],
         "defaultFilename":""
      },
      "datasetBatchConfig":{
         "allowedFoldernameAppendOptions":[
            "DESTINATION",
            "DATASET_ID",
            "DATASET_NAME",
            "EXPORT_TIME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFoldernameAppendOptions":[
            "DATASET_ID",
            "EXPORT_TIME"
         ],
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
            "ONCE"
         ]
      },
      "allowDedupKeyFieldSelection":false
   },
   "maxProfileAttributes":9000,
   "maxIdentityAttributes":1000,
   "destConfigId":"069280b7-40fc-490c-85c4-3bcae17b5441",
   "backfillHistoricalProfileData":true
}
```

+++

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, avrai una migliore comprensione di come configurare il tipo di dati sul pubblico per la tua destinazione.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Configurazione autenticazione cliente](customer-authentication.md)
* [Autorizzazione OAuth2](oauth2-authorization.md)
* [Campi dati cliente](customer-data-fields.md)
* [Attributi dell’interfaccia utente](ui-attributes.md)
* [Configurazione dello schema](schema-configuration.md)
* [Configurazione dello spazio dei nomi dell’identità](identity-namespace-configuration.md)
* [Configurazioni di mappatura supportate](supported-mapping-configurations.md)
* [Consegna della destinazione](destination-delivery.md)
* [Configurazione dei metadati del pubblico](audience-metadata-configuration.md)
* [Criterio di aggregazione](aggregation-policy.md)
* [Configurazione batch](batch-configuration.md)
* [Qualifiche del profilo storico](historical-profile-qualifications.md)
