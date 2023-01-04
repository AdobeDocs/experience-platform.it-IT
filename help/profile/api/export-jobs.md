---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API per processi di esportazione del profilo
topic-legacy: guide
type: Documentation
description: Il Profilo del cliente in tempo reale consente di creare una singola visualizzazione dei singoli clienti all’interno di Adobe Experience Platform raggruppando i dati provenienti da più sorgenti, inclusi i dati degli attributi e i dati comportamentali. I dati del profilo possono quindi essere esportati in un set di dati per un’ulteriore elaborazione.
exl-id: d51b1d1c-ae17-4945-b045-4001e4942b67
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 2%

---

# Endpoint processi di esportazione del profilo

[!DNL Real-Time Customer Profile] consente di creare un’unica visualizzazione dei singoli clienti raggruppando i dati provenienti da più sorgenti, inclusi i dati degli attributi e i dati comportamentali. I dati del profilo possono quindi essere esportati in un set di dati per un’ulteriore elaborazione. Ad esempio, segmenti di pubblico da [!DNL Profile] i dati possono essere esportati per l’attivazione e gli attributi di profilo possono essere esportati per la generazione di rapporti.

Questo documento fornisce istruzioni dettagliate per la creazione e la gestione dei processi di esportazione utilizzando [API del profilo](https://www.adobe.com/go/profile-apis-en).

>[!NOTE]
>
>Questa guida riguarda l’utilizzo dei posti di lavoro per le esportazioni [!DNL Profile API]. Per informazioni su come gestire i lavori di esportazione per il servizio di segmentazione di Adobe Experience Platform, consulta la guida su [esportazione di lavori nell’API Segmentazione](../../profile/api/export-jobs.md).

Oltre a creare un processo di esportazione, puoi anche accedere a [!DNL Profile] i dati che utilizzano `/entities` endpoint, noto anche come &quot;[!DNL Profile Access]&quot;. Consulta la sezione [guida all’endpoint entità](./entities.md) per ulteriori informazioni. Per i passaggi su come accedere a [!DNL Profile] i dati che utilizzano l&#39;interfaccia utente, fare riferimento alla [guida utente](../ui/user-guide.md).

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte del [!DNL Real-Time Customer Profile] API. Prima di continuare, controlla la [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio presenti in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi [!DNL Experience Platform] API.

## Creare un processo di esportazione

Esportazione [!DNL Profile] i dati richiedono innanzitutto la creazione di un set di dati in cui verranno esportati i dati, quindi l’avvio di un nuovo processo di esportazione. Entrambi questi passaggi possono essere eseguiti utilizzando API di Experience Platform, con le API di servizi di catalogo utilizzate per le prime e le API di profilo cliente in tempo reale. Le istruzioni dettagliate per il completamento di ogni passaggio sono descritte nelle sezioni seguenti.

### Creare un set di dati di destinazione

Durante l&#39;esportazione [!DNL Profile] data, è prima necessario creare un set di dati di destinazione. È importante che il set di dati sia configurato correttamente per garantire che l’esportazione abbia esito positivo.

Una delle considerazioni chiave è lo schema su cui si basa il set di dati (`schemaRef.id` nella richiesta di esempio API di seguito). Per esportare i dati di profilo, il set di dati deve essere basato su [!DNL XDM Individual Profile] Schema dell&#39;unione (`https://ns.adobe.com/xdm/context/profile__union`). Uno schema di unione è uno schema generato dal sistema e di sola lettura che aggrega i campi degli schemi che condividono la stessa classe. In questo caso, la [!DNL XDM Individual Profile] classe. Per ulteriori informazioni sugli schemi di visualizzazione dell&#39;unione, consulta la sezione [sezione unione nella guida di base sulla composizione dello schema](../../xdm/schema/composition.md#union).

I passaggi seguenti in questa esercitazione descrivono come creare un set di dati che fa riferimento a [!DNL XDM Individual Profile] Schema dell&#39;Unione utilizzando [!DNL Catalog] API. È inoltre possibile utilizzare [!DNL Platform] interfaccia utente per creare un set di dati che fa riferimento allo schema di unione. I passaggi per l’utilizzo dell’interfaccia utente sono descritti in [questa esercitazione sull&#39;interfaccia utente per l&#39;esportazione di segmenti](../../segmentation/tutorials/create-dataset-export-segment.md) ma sono applicabili anche qui. Una volta completato, puoi tornare a questa esercitazione per procedere con i passaggi per [avvio di un nuovo processo di esportazione](#initiate).

Se disponi già di un set di dati compatibile e ne conosci l’ID, puoi procedere direttamente al passaggio per [avvio di un nuovo processo di esportazione](#initiate).

**Formato API**

```http
POST /dataSets
```

**Richiesta**

La seguente richiesta crea un nuovo set di dati, fornendo parametri di configurazione nel payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Profile Data Export",
        "schemaRef": {
          "id": "https://ns.adobe.com/xdm/context/profile__union",
          "contentType": "application/vnd.adobe.xed+json;version=1"
        }
      }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Un nome descrittivo per il set di dati. |
| `schemaRef.id` | ID della visualizzazione unione (schema) a cui sarà associato il set di dati. |

**Risposta**

Una risposta corretta restituisce un array contenente l’ID univoco di sola lettura, generato dal sistema, del set di dati appena creato. Per esportare correttamente i dati del profilo, è necessario un ID di set di dati configurato correttamente.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Avvia processo di esportazione {#initiate}

Una volta che disponi di un set di dati persistente nell’unione, puoi creare un processo di esportazione per mantenere i dati del profilo nel set di dati effettuando una richiesta di POST al gruppo di dati `/export/jobs` nell’API del profilo cliente in tempo reale e fornendo i dettagli dei dati che desideri esportare nel corpo della richiesta.

**Formato API**

```http
POST /export/jobs
```

**Richiesta**

La seguente richiesta crea un nuovo processo di esportazione, fornendo i parametri di configurazione nel payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields": {
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
| `mergePolicy` | *(Facoltativo)* Specifica il criterio di unione per la gestione dei dati esportati. Includi questo parametro quando sono in corso l’esportazione di più segmenti. |
| `mergePolicy.id` | ID del criterio di unione. |
| `mergePolicy.version` | Versione specifica del criterio di unione da utilizzare. L’eliminazione di questo valore viene eseguita per impostazione predefinita nella versione più recente. |
| `additionalFields.eventList` | *(Facoltativo)* Controlla i campi evento serie temporale esportati per oggetti secondari o associati fornendo una o più delle seguenti impostazioni:<ul><li>`eventList.fields`: Controlla i campi da esportare.</li><li>`eventList.filter`: Specifica i criteri che limitano i risultati inclusi dagli oggetti associati. Si attende un valore minimo necessario per l’esportazione, in genere una data.</li><li>`eventList.filter.fromIngestTimestamp`: Filtra gli eventi delle serie temporali in quelli che sono stati acquisiti dopo la marca temporale fornita. Questo non è il momento dell’evento stesso, ma il momento dell’acquisizione degli eventi.</li></ul> |
| `destination` | **(Obbligatorio)** Informazioni sulla destinazione per i dati esportati:<ul><li>`destination.datasetId`: **(Obbligatorio)** ID del set di dati in cui devono essere esportati i dati.</li><li>`destination.segmentPerBatch`: *(Facoltativo)* Un valore booleano che, se non viene fornito, utilizza per impostazione predefinita `false`. Un valore di `false` esporta tutti gli ID segmento in un singolo ID batch. Un valore di `true` esporta un ID segmento in un ID batch. Tieni presente che l’impostazione del valore deve essere `true` possono influire sulle prestazioni dell&#39;esportazione batch.</li></ul> |
| `schema.name` | **(Obbligatorio)** Nome dello schema associato al set di dati in cui devono essere esportati i dati. |

>[!NOTE]
>
>Per esportare solo i dati di profilo e non includere i dati relativi alle serie temporali, rimuovi l’oggetto &quot;additionalFields&quot; dalla richiesta.

**Risposta**

Una risposta corretta restituisce un set di dati popolato con dati di profilo come specificato nella richiesta.

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
      "dataSetId": "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{ORG_ID}",
    "creationTime": 1559674261657
}
```

## Elenca tutti i processi di esportazione

Puoi restituire un elenco di tutti i processi di esportazione per una particolare organizzazione IMS eseguendo una richiesta di GET a `export/jobs` punto finale. La richiesta supporta anche i parametri di query `limit` e `offset`, come illustrato di seguito.

**Formato API**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `start` | Offset la pagina dei risultati restituiti, in base al tempo di creazione della richiesta. Esempio: `start=4` |
| `limit` | Limita il numero di risultati restituiti. Esempio: `limit=10` |
| `page` | Restituisce una pagina specifica di risultati, in base al tempo di creazione della richiesta. Esempio: `page=2` |
| `sort` | Ordina i risultati per un campo specifico in ascendente ( **`asc`** ) o decrescente ( **`desc`** ). Il parametro di ordinamento non funziona quando si restituiscono più pagine di risultati. Esempio: `sort=updateTime:asc` |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Risposta**

La risposta include un `records` oggetto contenente i processi di esportazione creati dall’organizzazione IMS.

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
      "imsOrgId": "{ORG_ID}",
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
      "imsOrgId": "{ORG_ID}",
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

## Monitorare l’avanzamento dell’esportazione

Per visualizzare i dettagli di un processo di esportazione specifico o monitorarne lo stato durante il processo, puoi effettuare una richiesta di GET al `/export/jobs` e include `id` del processo di esportazione nel percorso. Il processo di esportazione viene completato una volta che il `status` restituisce il valore &quot;SUCCEEDED&quot;.

**Formato API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | La `id` del processo di esportazione a cui si desidera accedere. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
      "dataSetId": "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{ORG_ID}",
    "creationTime": 1559674261657
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `batchId` | Identificatore dei batch creati da un&#39;esportazione riuscita, da utilizzare a scopo di ricerca durante la lettura dei dati del profilo. |

## Annullare un processo di esportazione

L’Experience Platform ti consente di annullare un processo di esportazione esistente, che può essere utile per una serie di motivi, tra cui se il processo di esportazione non è stato completato o è rimasto bloccato nella fase di elaborazione. Per annullare un processo di esportazione, è possibile eseguire una richiesta di DELETE al `/export/jobs` e include `id` del processo di esportazione che si desidera annullare nel percorso della richiesta.

**Formato API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | La `id` del processo di esportazione a cui si desidera accedere. |

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una richiesta di eliminazione corretta restituisce lo stato HTTP 204 (nessun contenuto) e un corpo di risposta vuoto, a indicare che l&#39;operazione di annullamento è riuscita.

## Passaggi successivi

Una volta completata correttamente l’esportazione, i dati sono disponibili nell’Experience Platform Data Lake . È quindi possibile utilizzare la [API di accesso ai dati](https://www.adobe.io/experience-platform-apis/references/data-access/) per accedere ai dati utilizzando `batchId` associato all’esportazione. A seconda delle dimensioni dell&#39;esportazione, i dati possono essere in blocchi e il batch può essere costituito da più file.

Per istruzioni dettagliate su come utilizzare l’API di accesso ai dati per accedere e scaricare file batch, segui il [Esercitazione sull&#39;accesso ai dati](../../data-access/tutorials/dataset-data.md).

Puoi anche accedere ai dati del profilo cliente in tempo reale esportati correttamente utilizzando il servizio Query Adobe Experience Platform. Utilizzando l’interfaccia utente o l’API RESTful, Query Service consente di scrivere, convalidare ed eseguire query sui dati all’interno del Data Lake.

Per ulteriori informazioni su come eseguire query sui dati del pubblico, consulta la [Documentazione del servizio query](../../query-service/home.md).

## Appendice

La sezione seguente contiene informazioni aggiuntive sui lavori di esportazione nell’API del profilo.

### Esempi aggiuntivi di payload per l’esportazione

La chiamata API di esempio mostrata nella sezione su [avvio di un processo di esportazione](#initiate) crea un processo che contiene sia i dati del profilo (record) che quelli dell’evento (serie temporale). Questa sezione fornisce esempi di payload di richiesta aggiuntivi per limitare l’esportazione in modo che contenga un tipo di dati o l’altro.

Il seguente payload crea un processo di esportazione che contiene solo i dati di profilo (nessun evento):

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

Per creare un processo di esportazione che contiene solo i dati evento (nessun attributo di profilo), il payload potrebbe essere simile al seguente:

```json
{
    "fields": "identityMap",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields": {
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

Puoi anche utilizzare l’endpoint per i processi di esportazione per esportare i segmenti di pubblico invece di [!DNL Profile] dati. Consulta la guida su [esportazione di lavori nell’API Segmentazione](../../segmentation/api/export-jobs.md) per ulteriori informazioni.
