---
keywords: Experience Platform ;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API per processi di esportazione
topic: guide
type: Documentation
description: Il profilo cliente in tempo reale consente di creare una singola vista dei singoli clienti all'interno di Adobe Experience Platform riunendo i dati provenienti da più origini, inclusi i dati attributo e comportamentali. I dati del profilo possono quindi essere esportati in un set di dati per un’ulteriore elaborazione.
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 2%

---


# Endpoint processi di esportazione

[!DNL Real-time Customer Profile] consente di creare una singola vista dei singoli clienti riunendo i dati provenienti da più origini, inclusi i dati attributo e comportamentali. I dati del profilo possono quindi essere esportati in un set di dati per un’ulteriore elaborazione. Ad esempio, i segmenti di pubblico provenienti da [!DNL Profile] dati possono essere esportati per l&#39;attivazione e gli attributi di profilo possono essere esportati per il reporting.

Questo documento fornisce istruzioni dettagliate per la creazione e la gestione dei processi di esportazione mediante l&#39;API [Profile](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

>[!NOTE]
>
>Questa guida descrive l&#39;utilizzo dei processi di esportazione in [!DNL Profile API]. Per informazioni su come gestire i processi di esportazione per Adobe Experience Platform Segmentation Service, consulta la guida sui processi di [esportazione nell&#39;API di segmentazione](../../profile/api/export-jobs.md).

Oltre a creare un processo di esportazione, potete anche accedere ai dati [!DNL Profile] utilizzando l&#39;endpoint `/entities`, noto anche come &quot;[!DNL Profile Access]&quot;. Per ulteriori informazioni, vedere la [guida dell&#39;endpoint entità](./entities.md). Per i passaggi su come accedere ai dati [!DNL Profile] utilizzando l&#39;interfaccia utente, fare riferimento alla [guida utente](../ui/user-guide.md).

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte dell&#39;API [!DNL Real-time Customer Profile]. Prima di continuare, consultare la [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per eseguire correttamente chiamate a qualsiasi API [!DNL Experience Platform].

## Creare un processo di esportazione

L&#39;esportazione di dati [!DNL Profile] richiede innanzitutto la creazione di un dataset in cui esportare i dati, quindi l&#39;avvio di un nuovo processo di esportazione. Entrambi questi passaggi possono essere eseguiti utilizzando  API di Experience Platform, con le prime mediante l&#39;API Catalog Service e le seconde mediante l&#39;API Real-time Customer Profile. Le istruzioni dettagliate per completare ciascun passaggio sono descritte nelle sezioni che seguono.

### Creare un dataset di destinazione

Quando si esportano dati [!DNL Profile], è necessario creare prima un set di dati di destinazione. È importante che il set di dati sia configurato correttamente per garantire il successo dell&#39;esportazione.

Una delle considerazioni chiave è lo schema su cui si basa il dataset (`schemaRef.id` nella richiesta di esempio API di seguito). Per esportare i dati del profilo, il set di dati deve essere basato sullo [!DNL XDM Individual Profile] schema unionale (`https://ns.adobe.com/xdm/context/profile__union`). Uno schema unione è uno schema di sola lettura generato dal sistema che aggrega i campi degli schemi che condividono la stessa classe. In questo caso, si tratta della classe [!DNL XDM Individual Profile]. Per ulteriori informazioni sugli schemi di visualizzazione unione, vedere la sezione [unione nella guida di base della composizione dello schema](../../xdm/schema/composition.md#union).

I passaggi descritti in questa esercitazione descrivono come creare un dataset che faccia riferimento allo schema dell&#39;unione [!DNL XDM Individual Profile] utilizzando l&#39;API [!DNL Catalog]. È inoltre possibile utilizzare l&#39;interfaccia utente [!DNL Platform] per creare un dataset che faccia riferimento allo schema di unione. I passaggi per l&#39;utilizzo dell&#39;interfaccia utente sono descritti in [questa esercitazione sull&#39;interfaccia utente per l&#39;esportazione di segmenti](../../segmentation/tutorials/create-dataset-export-segment.md), ma sono applicabili anche qui. Una volta completata, è possibile tornare a questa esercitazione per procedere con i passaggi necessari per [avviare un nuovo processo di esportazione](#initiate).

Se disponete già di un set di dati compatibile e ne conoscete l&#39;ID, potete procedere direttamente al passaggio per [avviare un nuovo processo di esportazione](#initiate).

**Formato API**

```http
POST /dataSets
```

**Richiesta**

La richiesta seguente crea un nuovo dataset, fornendo i parametri di configurazione nel payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Profile Data Export",
        "schemaRef": {
          "id": "https://ns.adobe.com/xdm/context/profile__union",
          "contentType": "application/vnd.adobe.xed+json;version=1"
        },
        "fileDescription": {
          "persisted": true,
          "containerFormat": "parquet",
          "format": "parquet"
        }
      }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Un nome descrittivo per il set di dati. |
| `schemaRef.id` | ID della visualizzazione unione (schema) a cui sarà associato il set di dati. |
| `fileDescription.persisted` | Un valore booleano che, se impostato su `true`, consente al dataset di rimanere nella visualizzazione unione. |

**Risposta**

Una risposta corretta restituisce un array contenente l&#39;ID univoco, generato dal sistema, di sola lettura del set di dati appena creato. Per esportare correttamente i dati del profilo è necessario un ID di set di dati configurato correttamente.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Avviare il processo di esportazione {#initiate}

Una volta ottenuto un dataset persistente nell&#39;unione, potete creare un processo di esportazione per mantenere i dati del profilo nel dataset effettuando una richiesta di POST all&#39;endpoint `/export/jobs` nell&#39;API del profilo cliente in tempo reale e fornendo i dettagli dei dati che desiderate esportare nel corpo della richiesta.

**Formato API**

```http
POST /export/jobs
```

**Richiesta**

La richiesta seguente crea un nuovo processo di esportazione, fornendo i parametri di configurazione nel payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    }
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }' 
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `fields` | *(Facoltativo)* Limita i campi di dati da includere nell’esportazione solo a quelli forniti in questo parametro. Se si omette questo valore, tutti i campi verranno inclusi nei dati esportati. |
| `mergePolicy` | *(Facoltativo)* Specifica il criterio di unione per la gestione dei dati esportati. Includete questo parametro quando vi sono più segmenti da esportare. |
| `mergePolicy.id` | ID del criterio di unione. |
| `mergePolicy.version` | Versione specifica del criterio di unione da utilizzare. Se si omette questo valore, per impostazione predefinita verrà utilizzata la versione più recente. |
| `additionalFields.eventList` | *(Facoltativo)* Controlla i campi evento delle serie temporali esportati per oggetti secondari o associati fornendo una o più delle seguenti impostazioni:<ul><li>`eventList.fields`: Controllare i campi da esportare.</li><li>`eventList.filter`: Specifica i criteri che limitano i risultati inclusi dagli oggetti associati. Si attende un valore minimo richiesto per l’esportazione, in genere una data.</li><li>`eventList.filter.fromIngestTimestamp`: Filtra gli eventi della serie temporale a quelli che sono stati acquisiti dopo la marca temporale fornita. Questo non è il momento dell’evento stesso ma il momento dell’inserimento degli eventi.</li></ul> |
| `destination` | **(Obbligatorio)Informazioni sulla** destinazione per i dati esportati:<ul><li>`destination.datasetId`:  **(Obbligatorio)** ID del set di dati in cui esportare i dati.</li><li>`destination.segmentPerBatch`:  *(Facoltativo)* Un valore booleano che, se non viene fornito, utilizza per impostazione predefinita  `false`. Un valore di `false` esporta tutti gli ID segmento in un singolo ID batch. Un valore di `true` esporta un ID segmento in un ID batch. Tenete presente che l&#39;impostazione del valore su `true` può influire sulle prestazioni di esportazione batch.</li></ul> |
| `schema.name` | **(Obbligatorio)** Nome dello schema associato al dataset in cui devono essere esportati i dati. |

>[!NOTE]
>
>Per esportare solo i dati del profilo e non includere i dati relativi alle serie temporali, rimuovere l&#39;oggetto &quot;AdditionalFields&quot; dalla richiesta.

**Risposta**

Una risposta corretta restituisce un dataset popolato con dati di profilo come specificato nella richiesta.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

## Elenca tutti i processi di esportazione

Potete restituire un elenco di tutti i processi di esportazione per una particolare organizzazione IMS eseguendo una richiesta di GET all&#39;endpoint `export/jobs`. La richiesta supporta anche i parametri di query `limit` e `offset`, come mostrato di seguito.

**Formato API**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `start` | Consente di scostare la pagina dei risultati restituiti, in base al tempo di creazione della richiesta. Esempio: `start=4` |
| `limit` | Limita il numero di risultati restituiti. Esempio: `limit=10` |
| `page` | Restituisce una pagina specifica di risultati, in base all’ora di creazione della richiesta. Esempio: `page=2` |
| `sort` | Ordinare i risultati in base a un campo specifico in ordine crescente ( **`asc`** ) o decrescente ( **`desc`** ). Il parametro sort non funziona quando si restituiscono più pagine di risultati. Esempio: `sort=updateTime:asc` |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Risposta**

La risposta include un oggetto `records` contenente i processi di esportazione creati dall&#39;organizzazione IMS.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538615973895
    },
    {
      "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
      "errors": [
        {
          "code": "0090000009",
          "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
          "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
        },
        {
          "code": "unknown",
          "msg": "Job aborted.",
          "callStack": "org.apache.spark.SparkException: Job aborted."
        }
      ],
      "jobType": "BATCH",
      "filter": {
        "segments": [
            {
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
            }
        ]
      },
      "id": 722,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
          "version": 1
      },
      "status": "FAILED",
      "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
      "computeGatewayJobId": {
          "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538573416687,
              "endTimeInMs": 1538573922551,
              "totalTimeInMs": 505864
          },
          "profileExportTime": {
              "startTimeInMs": 1538573872211,
              "endTimeInMs": 1538573918809,
              "totalTimeInMs": 46598
          }
      },
      "destination": {
          "datasetId": "5bb4c46757920712f924a3eb",
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

## Monitorare l&#39;avanzamento dell&#39;esportazione

Per visualizzare i dettagli di un processo di esportazione specifico, o controllarne lo stato durante l&#39;elaborazione, potete effettuare una richiesta di GET all&#39;endpoint `/export/jobs` e includere nel percorso `id` del processo di esportazione. Il processo di esportazione viene completato una volta che il campo `status` restituisce il valore &quot;SUCCEEDED&quot;.

**Formato API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | `id` del processo di esportazione a cui si desidera accedere. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `batchId` | Identificatore dei batch creati da un&#39;esportazione riuscita, da utilizzare a scopo di ricerca durante la lettura dei dati del profilo. |

## Annullamento di un processo di esportazione

 Experience Platform consente di annullare un processo di esportazione esistente, che può essere utile per diversi motivi, ad esempio se il processo di esportazione non è stato completato o si è bloccato nella fase di elaborazione. Per annullare un processo di esportazione, potete eseguire una richiesta di DELETE all&#39;endpoint `/export/jobs` e includere la `id` del processo di esportazione che desiderate annullare nel percorso della richiesta.

**Formato API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | `id` del processo di esportazione a cui si desidera accedere. |

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una richiesta di eliminazione riuscita restituisce lo stato HTTP 204 (nessun contenuto) e un corpo di risposta vuoto, a indicare l&#39;esito dell&#39;operazione di annullamento.

## Passaggi successivi

Una volta completata l&#39;esportazione, i dati sono disponibili all&#39;interno del Data Lake  Experience Platform. È quindi possibile utilizzare l&#39; [API di accesso ai dati](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) per accedere ai dati utilizzando l&#39; `batchId` associato all&#39;esportazione. A seconda delle dimensioni dell’esportazione, i dati possono essere in blocchi e il batch può essere costituito da più file.

Per istruzioni dettagliate su come utilizzare l&#39;API di accesso ai dati per accedere e scaricare file batch, seguire l&#39; [esercitazione sull&#39;accesso ai dati](../../data-access/tutorials/dataset-data.md).

È inoltre possibile accedere ai dati del profilo cliente in tempo reale esportati correttamente tramite Adobe Experience Platform Query Service. Utilizzando l&#39;interfaccia utente o l&#39;API RESTful, Query Service consente di scrivere, convalidare ed eseguire query sui dati all&#39;interno del Data Lake.

Per ulteriori informazioni su come eseguire query ai dati sul pubblico, consultare la [documentazione del servizio query](../../query-service/home.md).

## Appendice

La sezione seguente contiene informazioni aggiuntive sui processi di esportazione nell’API del profilo.

### Esempi di payload di esportazione aggiuntivi

La chiamata API di esempio mostrata nella sezione relativa all&#39; [avvio di un processo di esportazione](#initiate) crea un processo che contiene sia dati di profilo (record) che di evento (serie temporale). Questa sezione fornisce esempi di payload di richieste aggiuntivi per limitare l’esportazione in modo che contenga un tipo di dati o l’altro.

Il payload seguente crea un processo di esportazione che contiene solo i dati del profilo (nessun evento):

```json
{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

Per creare un processo di esportazione che contiene solo i dati dell’evento (nessun attributo del profilo), il payload potrebbe essere simile al seguente:

```json
{
    "fields": "identityMap",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

### Esportazione di segmenti

Potete inoltre utilizzare l&#39;endpoint dei processi di esportazione per esportare segmenti di pubblico invece dei dati [!DNL Profile]. Per ulteriori informazioni, consulta la guida sui processi di esportazione [nell&#39;API di segmentazione](../../segmentation/api/export-jobs.md).