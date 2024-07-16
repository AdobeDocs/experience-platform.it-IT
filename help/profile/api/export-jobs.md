---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API per processi di esportazione profilo
type: Documentation
description: Real-Time Customer Profile consente di creare una singola visualizzazione dei singoli clienti all’interno di Adobe Experience Platform riunendo dati provenienti da più origini, inclusi sia i dati degli attributi che i dati comportamentali. I dati profilo possono quindi essere esportati in un set di dati per ulteriore elaborazione.
role: Developer
exl-id: d51b1d1c-ae17-4945-b045-4001e4942b67
source-git-commit: fd5042bee9b09182ac643bcc69482a0a2b3f8faa
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 2%

---

# Endpoint &quot;profile export jobs&quot;

[!DNL Real-Time Customer Profile] consente di creare una singola visualizzazione dei singoli clienti riunendo dati provenienti da più origini, inclusi sia i dati degli attributi che i dati comportamentali. I dati profilo possono quindi essere esportati in un set di dati per ulteriore elaborazione. Ad esempio, è possibile esportare i dati di [!DNL Profile] per l&#39;attivazione creando tipi di pubblico e gli attributi del profilo possono essere esportati per il reporting.

In questo documento vengono fornite istruzioni dettagliate per la creazione e la gestione dei processi di esportazione tramite l&#39;[API profilo](https://www.adobe.com/go/profile-apis-en).

>[!NOTE]
>
>Questa guida descrive l&#39;utilizzo dei processi di esportazione in [!DNL Profile API]. Per informazioni su come gestire i processi di esportazione per Adobe Experience Platform Segmentation Service, consulta la guida su [processi di esportazione nell&#39;API di segmentazione](../../profile/api/export-jobs.md).

Oltre a creare un processo di esportazione, è possibile accedere ai dati di [!DNL Profile] utilizzando l&#39;endpoint `/entities`, noto anche come &quot;[!DNL Profile Access]&quot;. Per ulteriori informazioni, consulta la [guida dell&#39;endpoint delle entità](./entities.md). Per i passaggi su come accedere ai dati di [!DNL Profile] tramite l&#39;interfaccia utente, fare riferimento alla [guida utente](../ui/user-guide.md).

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte dell&#39;API [!DNL Real-Time Customer Profile]. Prima di continuare, consulta la [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API [!DNL Experience Platform].

## Creare un processo di esportazione

L&#39;esportazione dei dati [!DNL Profile] richiede prima la creazione di un set di dati in cui verranno esportati i dati, quindi l&#39;avvio di un nuovo processo di esportazione. Entrambi i passaggi possono essere eseguiti utilizzando le API Experience Platform, con la prima che utilizza l’API Catalog Service e la seconda che utilizza l’API Profilo cliente in tempo reale. Le istruzioni dettagliate per il completamento di ciascun passaggio sono descritte nelle sezioni che seguono.

### Creare un set di dati di destinazione

Durante l&#39;esportazione dei dati [!DNL Profile], è necessario creare prima un set di dati di destinazione. È importante che il set di dati sia configurato correttamente per garantire l’esportazione in modo corretto.

Una delle considerazioni chiave è lo schema su cui si basa il set di dati (`schemaRef.id` nella richiesta di esempio API seguente). Per esportare i dati del profilo, il set di dati deve essere basato sullo schema di unione [!DNL XDM Individual Profile] (`https://ns.adobe.com/xdm/context/profile__union`). Uno schema di unione è uno schema di sola lettura generato dal sistema che aggrega i campi degli schemi che condividono la stessa classe. In questo caso, questa è la classe [!DNL XDM Individual Profile]. Per ulteriori informazioni sugli schemi di visualizzazione unione, consulta la sezione [union nella guida di base della composizione dello schema](../../xdm/schema/composition.md#union).

I passaggi seguenti in questa esercitazione descrivono come creare un set di dati che fa riferimento allo schema di unione [!DNL XDM Individual Profile] utilizzando l&#39;API [!DNL Catalog]. È inoltre possibile utilizzare l&#39;interfaccia utente [!DNL Platform] per creare un set di dati che faccia riferimento allo schema di unione. I passaggi per l&#39;utilizzo dell&#39;interfaccia utente sono descritti in [questa esercitazione dell&#39;interfaccia utente per l&#39;esportazione di tipi di pubblico](../../segmentation/tutorials/create-dataset-export-segment.md), ma sono applicabili anche qui. Una volta completato, puoi tornare a questo tutorial per procedere con i passaggi per [l&#39;avvio di un nuovo processo di esportazione](#initiate).

Se disponi già di un set di dati compatibile e conosci il relativo ID, puoi procedere direttamente al passaggio per [avviare un nuovo processo di esportazione](#initiate).

**Formato API**

```http
POST /dataSets
```

**Richiesta**

La richiesta seguente crea un nuovo set di dati, fornendo i parametri di configurazione nel payload.

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
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
| `name` | Nome descrittivo del set di dati. |
| `schemaRef.id` | ID della visualizzazione unione (schema) a cui verrà associato il set di dati. |

**Risposta**

In caso di esito positivo, la risposta restituisce un array contenente l’ID univoco di sola lettura generato dal sistema del set di dati appena creato. Per esportare correttamente i dati profilo è necessario un ID set di dati configurato correttamente.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Avvia processo di esportazione {#initiate}

Dopo aver creato un set di dati persistente nell’unione, puoi creare un processo di esportazione per rendere persistenti i dati profilo nel set di dati eseguendo una richiesta POST all’endpoint `/export/jobs` nell’API Profilo cliente in tempo reale e fornendo i dettagli dei dati da esportare nel corpo della richiesta.

**Formato API**

```http
POST /export/jobs
```

**Richiesta**

La richiesta seguente crea un nuovo processo di esportazione, fornendo i parametri di configurazione nel payload.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
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
    },
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
| `fields` | *(Facoltativo)* Limita i campi dati da includere nell&#39;esportazione solo a quelli forniti in questo parametro. Omettendo questo valore, tutti i campi verranno inclusi nei dati esportati. |
| `mergePolicy` | *(Facoltativo)* Specifica il criterio di unione da applicare ai dati esportati. Includi questo parametro quando vengono esportati più tipi di pubblico. |
| `mergePolicy.id` | ID del criterio di unione. |
| `mergePolicy.version` | Versione specifica del criterio di unione da utilizzare. Se si omette questo valore, per impostazione predefinita viene utilizzata la versione più recente. |
| `additionalFields.eventList` | *(Facoltativo)* Controlla i campi evento della serie temporale esportati per oggetti figlio o associati fornendo una o più delle seguenti impostazioni:<ul><li>`eventList.fields`: controlla i campi da esportare.</li><li>`eventList.filter`: specifica i criteri che limitano i risultati inclusi dagli oggetti associati. Prevede un valore minimo richiesto per l&#39;esportazione, in genere una data.</li><li>`eventList.filter.fromIngestTimestamp`: filtra gli eventi della serie temporale con quelli che sono stati acquisiti dopo la marca temporale fornita. Non è l’ora dell’evento in sé, ma il tempo di acquisizione degli eventi.</li></ul> |
| `destination` | **(Obbligatorio)** Informazioni di destinazione per i dati esportati:<ul><li>`destination.datasetId`: **(obbligatorio)** ID del set di dati in cui devono essere esportati i dati.</li><li>`destination.segmentPerBatch`: *(Facoltativo)* Valore booleano che, se non specificato, viene impostato automaticamente su `false`. Un valore di `false` esporta tutti gli ID di definizione del segmento in un singolo ID batch. Un valore di `true` esporta un ID di definizione segmento in un ID batch. L&#39;impostazione del valore su `true` può influire sulle prestazioni di esportazione batch.</li></ul> |
| `schema.name` | **(Obbligatorio)** Il nome dello schema associato al set di dati in cui devono essere esportati i dati. |

>[!NOTE]
>
>Per esportare solo i dati di profilo e non includere i dati di serie temporali correlati, rimuovere l&#39;oggetto &quot;additionalFields&quot; dalla richiesta.

**Risposta**

In caso di esito positivo, la risposta restituisce un set di dati popolato con dati di profilo come specificato nella richiesta.

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

È possibile restituire un elenco di tutti i processi di esportazione per una particolare organizzazione eseguendo una richiesta di GET all&#39;endpoint `export/jobs`. La richiesta supporta anche i parametri di query `limit` e `offset`, come illustrato di seguito.

**Formato API**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `start` | Offset della pagina dei risultati restituiti, in base all’ora di creazione della richiesta. Esempio: `start=4` |
| `limit` | Limita il numero di risultati restituiti. Esempio: `limit=10` |
| `page` | Restituisce una pagina di risultati specifica, in base all’ora di creazione della richiesta. Esempio: `page=2` |
| `sort` | Ordinare i risultati in base a un campo specifico in ordine crescente ( **`asc`** ) o decrescente ( **`desc`** ). Il parametro sort non funziona quando si restituiscono più pagine di risultati. Esempio: `sort=updateTime:asc` |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Risposta**

La risposta include un oggetto `records` contenente i processi di esportazione creati dall&#39;organizzazione.

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

Per visualizzare i dettagli di un processo di esportazione specifico o monitorarne lo stato durante l&#39;elaborazione, è possibile effettuare una richiesta di GET all&#39;endpoint `/export/jobs` e includere `id` del processo di esportazione nel percorso. Il processo di esportazione viene completato quando il campo `status` restituisce il valore &quot;SUCCESSEDED&quot;.

**Formato API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | `id` del processo di esportazione a cui desideri accedere. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/24115 \
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
| `batchId` | Identificatore dei batch creati da un’esportazione riuscita, da utilizzare a scopo di ricerca durante la lettura dei dati del profilo. |

## Annullare un processo di esportazione

Experience Platform consente di annullare un processo di esportazione esistente. Ciò può essere utile per diversi motivi, tra cui se il processo di esportazione non è stato completato o si è bloccato nella fase di elaborazione. Per annullare un processo di esportazione, è possibile eseguire una richiesta DELETE all&#39;endpoint `/export/jobs` e includere `id` del processo di esportazione che si desidera annullare nel percorso della richiesta.

**Formato API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | `id` del processo di esportazione a cui desideri accedere. |

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la richiesta di eliminazione restituisce lo stato HTTP 204 (nessun contenuto) e un corpo di risposta vuoto, a indicare che l’operazione di annullamento è riuscita.

## Passaggi successivi

Una volta completata correttamente l’esportazione, i dati sono disponibili all’interno del Data Lake in Experience Platform. È quindi possibile utilizzare l&#39;[API di accesso ai dati](https://www.adobe.io/experience-platform-apis/references/data-access/) per accedere ai dati utilizzando il `batchId` associato all&#39;esportazione. A seconda delle dimensioni dell’esportazione, i dati possono essere in blocchi e il batch può essere costituito da diversi file.

Per istruzioni dettagliate sull&#39;utilizzo dell&#39;API di accesso ai dati per accedere e scaricare file batch, seguire l&#39;[esercitazione sull&#39;accesso ai dati](../../data-access/tutorials/dataset-data.md).

Puoi anche accedere ai dati Real-Time Customer Profile esportati correttamente tramite Adobe Experience Platform Query Service. Utilizzando l’interfaccia utente o l’API RESTful, Query Service consente di scrivere, convalidare ed eseguire query sui dati all’interno del Data Lake.

Per ulteriori informazioni su come eseguire query sui dati del pubblico, consulta la [documentazione di Query Service](../../query-service/home.md).

## Appendice

La sezione seguente contiene informazioni aggiuntive relative ai processi di esportazione nell’API di profilo.

### Ulteriori esempi di payload di esportazione

La chiamata API di esempio mostrata nella sezione relativa all&#39;avvio di un processo di esportazione ](#initiate) crea un processo che contiene sia dati di profilo (record) che dati di evento (serie temporali). [ Questa sezione fornisce ulteriori esempi di payload di richiesta per limitare l’esportazione in modo che contenga un tipo di dati o l’altro.

Il seguente payload crea un processo di esportazione che contiene solo dati di profilo (nessun evento):

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

Per creare un processo di esportazione che contenga solo dati evento (senza attributi di profilo), il payload potrebbe essere simile al seguente:

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

### Esportazione di tipi di pubblico

È inoltre possibile utilizzare l&#39;endpoint dei processi di esportazione per esportare tipi di pubblico anziché [!DNL Profile] dati. Per ulteriori informazioni, consulta la guida sui [processi di esportazione nell&#39;API di segmentazione](../../segmentation/api/export-jobs.md).
