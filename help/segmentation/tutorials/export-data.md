---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Esportare i dati mediante le API
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 1%

---


# Esportare i dati del profilo utilizzando le API

Il profilo cliente in tempo reale consente di creare un&#39;unica vista dei singoli clienti riunendo i dati provenienti da più origini, inclusi i dati attributo e comportamentali. I dati disponibili in Profile (Profilo) possono quindi essere esportati in un dataset per un&#39;ulteriore elaborazione. Questa esercitazione fornisce istruzioni dettagliate per creare e gestire i processi di esportazione mediante l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)Segmentazione.

Oltre a creare un processo di esportazione, potete accedere ai dati del profilo anche tramite l’API di accesso al profilo e tramite proiezioni. Per ulteriori informazioni su questi altri pattern di accesso, consulta l’esercitazione [API](../../profile/api/entities.md) Profile Access o l’esercitazione sulla [configurazione di destinazioni e proiezioni](../../profile/api/edge-projections.md) edge.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei diversi servizi di Adobe Experience Platform  coinvolti nell&#39;utilizzo dei dati di profilo. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [Profilo](../../profile/home.md)cliente in tempo reale: Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [servizio](../home.md)di segmentazione Adobe Experience Platform: Consente di creare segmenti di pubblico dai dati del profilo cliente in tempo reale.
- [Experience Data Model (XDM)](../../xdm/home.md): Framework standard con cui Platform organizza i dati sull&#39;esperienza dei clienti.
- [Sandbox](../../sandboxes/home.md):  Experience Platform fornisce sandbox virtuali che dividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

### Intestazioni necessarie

Questa esercitazione richiede anche di aver completato l&#39;esercitazione [di](../../tutorials/authentication.md) autenticazione per effettuare correttamente le chiamate alle API Platform. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API Experience Platform, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in  Experience Platform sono isolate in sandbox virtuali specifiche. Le richieste alle API Platform richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Platform, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste POST, PUT e PATCH richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

## Creare un processo di esportazione

Per esportare i dati del profilo è innanzitutto necessario creare un set di dati in cui esportare i dati, quindi avviare un nuovo processo di esportazione. Entrambi questi passaggi possono essere eseguiti utilizzando  API Experience Platform, con le prime mediante l&#39;API Catalog Service e le seconde mediante l&#39;API Real-time Customer Profile. Le istruzioni dettagliate per completare ciascun passaggio sono descritte nelle sezioni che seguono.

- [Creare un set di dati](#create-a-target-dataset) di destinazione: creare un set di dati in cui memorizzare i dati esportati.
- [Avviare un nuovo processo](#initiate-export-job) di esportazione - Compilare il set di dati con i dati del profilo singolo XDM.

### Creare un dataset di destinazione

Quando si esportano i dati del profilo, è necessario creare prima un set di dati di destinazione. È importante che il set di dati sia configurato correttamente per garantire il successo dell&#39;esportazione.

Una delle considerazioni chiave è lo schema su cui si basa il dataset (`schemaRef.id` nella richiesta di esempio API di seguito). Per esportare un segmento, il set di dati deve essere basato sullo schema unionale profilo singolo XDM (`https://ns.adobe.com/xdm/context/profile__union`). Uno schema unione è uno schema di sola lettura generato dal sistema che aggrega i campi degli schemi che condividono la stessa classe, in questo caso si tratta della classe XDM Singolo profilo. Per ulteriori informazioni sugli schemi di visualizzazione dell&#39;unione, vedere la sezione Profilo cliente in tempo [reale della guida](../../xdm/schema/composition.md#union)per gli sviluppatori del Registro di sistema dello schema.

I passaggi che seguono in questa esercitazione descrivono come creare un dataset che faccia riferimento allo schema dell&#39;unione dei profili XDM utilizzando l&#39;API Catalog. È inoltre possibile utilizzare l&#39;interfaccia utente del Adobe Experience Platform  per creare un dataset che faccia riferimento allo schema unione. I passaggi per l’utilizzo dell’interfaccia utente sono descritti in [questa esercitazione sull’interfaccia utente per l’esportazione di segmenti](./create-dataset-export-segment.md) , ma sono applicabili anche qui. Al termine, potete tornare a questa esercitazione per procedere con i passaggi necessari per [avviare un nuovo processo](#initiate-export-job)di esportazione.

Se disponete già di un set di dati compatibile e ne conoscete l’ID, potete procedere direttamente al passaggio per [avviare un nuovo processo](#initiate-export-job)di esportazione.

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
| `fileDescription.persisted` | Un valore booleano che, se impostato su `true`, consente al dataset di persistere nella visualizzazione unione. |

**Risposta**

Una risposta corretta restituisce un array contenente l&#39;ID univoco, generato dal sistema, di sola lettura del set di dati appena creato. Per esportare correttamente i dati del profilo è necessario un ID di set di dati configurato correttamente.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Avvia processo di esportazione

Una volta ottenuto un set di dati persistente nell’unione, potete creare un processo di esportazione per mantenere i dati del profilo nel dataset effettuando una richiesta POST all’ `/export/jobs` endpoint nell’API del profilo cliente in tempo reale e fornendo i dettagli dei dati che desiderate esportare nel corpo della richiesta.

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
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ],
      "segmentQualificationTime": {
            "startTime": "2019-09-01T00:00:00Z",
            "endTime": "2019-09-02T00:00:00Z"
        },
      "fromIngestTimestamp": "2018-10-25T13:22:04-07:00",
      "emptyProfiles": false
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
      "segmentPerBatch": true
    },
    "schema": {
      "name": "_xdm.context.profile"
    },
    "evaluationInfo": {
        "segmentation": true
    }
  }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `fields` | *(Facoltativo)* Limita i campi di dati da includere nell’esportazione solo a quelli forniti in questo parametro. Lo stesso parametro è disponibile anche quando si crea un segmento, pertanto i campi nel segmento potrebbero essere già stati filtrati. Se si omette questo valore, tutti i campi verranno inclusi nei dati esportati. |
| `mergePolicy` | *(Facoltativo)* Specifica il criterio di unione da applicare ai dati esportati. Includete questo parametro quando vi sono più segmenti da esportare. Se si omette questo valore, il servizio di esportazione utilizzerà il criterio di unione fornito dal segmento. |
| `mergePolicy.id` | ID del criterio di unione. |
| `mergePolicy.version` | Versione specifica del criterio di unione da utilizzare. Se si omette questo valore, per impostazione predefinita verrà utilizzata la versione più recente. |
| `filter` | *(Facoltativo)* Specifica uno o più dei seguenti filtri da applicare al segmento prima dell&#39;esportazione. |
| `filter.segments` | *(Facoltativo)* Specifica i segmenti da esportare. Se si omette questo valore, verranno esportati tutti i dati di tutti i profili. Accetta un array di oggetti segmento, ciascuno dei quali contiene i campi seguenti:<ul><li>`segmentId`: **(Obbligatorio se si utilizza`segments`)** ID segmento per i profili da esportare.</li><li>`segmentNs` *(Facoltativo)* Spazio dei nomi del segmento per il dato `segmentID`.</li><li>`status` *(Facoltativo)* Un array di stringhe che fornisce un filtro di stato per l&#39;oggetto `segmentID`. Per impostazione predefinita, `status` il valore `["realized", "existing"]` rappresenta tutti i profili che rientrano nel segmento al momento corrente. I valori possibili sono: `"realized"`, `"existing"`e `"exited"`.</br></br>Per ulteriori informazioni, consulta l’esercitazione sulla [creazione di segmenti](./create-a-segment.md).</li></ul> |
| `filter.segmentQualificationTime` | *(Facoltativo)* Filtra in base al tempo di qualificazione del segmento. È possibile specificare l&#39;ora di inizio e/o di fine. |
| `filter.segmentQualificationTime.startTime` | *(Facoltativo)* Ora di inizio qualifica segmento per un ID segmento per un dato stato. Non viene fornito, non verrà applicato alcun filtro all&#39;ora di inizio per la qualifica ID segmento. La marca temporale deve essere fornita in formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.segmentQualificationTime.endTime` | *(Facoltativo)* Tempo di fine qualifica segmento per un ID segmento per un dato stato. Non viene fornito, non verrà applicato alcun filtro all&#39;ora di fine per la qualifica di ID segmento. La marca temporale deve essere fornita in formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.fromIngestTimestamp ` | *(Facoltativo)* Limita i profili esportati a includere solo quelli che sono stati aggiornati dopo questa marca temporale. La marca temporale deve essere fornita in formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . <ul><li>`fromIngestTimestamp` per **i profili**, se forniti: Include tutti i profili uniti in cui la marca temporale aggiornata unita è maggiore della marca temporale specificata. Supporta `greater_than` l&#39;operando.</li><li>`fromTimestamp` per **gli eventi**: Tutti gli eventi acquisiti dopo questa marca temporale verranno esportati in base al risultato del profilo risultante. Questo non è il momento dell’evento stesso ma il momento dell’inserimento degli eventi.</li> |
| `filter.emptyProfiles` | *(Facoltativo)* Valore Boolean. I profili possono contenere record Profilo, record ExperienceEvent o entrambi. I profili senza record Profilo e solo i record ExperienceEvent sono denominati &quot;emptyProfiles&quot;. Per esportare tutti i profili nell’archivio profili, inclusi i &quot;emptyProfiles&quot;, imposta il valore di `emptyProfiles` su `true`. Se `emptyProfiles` è impostato su `false`, vengono esportati solo i profili con record Profilo nello store. Per impostazione predefinita, se `emptyProfiles` l’attributo non è incluso, vengono esportati solo i profili contenenti i record Profilo. |
| `additionalFields.eventList` | *(Facoltativo)* Controlla i campi evento delle serie temporali esportati per oggetti secondari o associati fornendo una o più delle seguenti impostazioni:<ul><li>`eventList.fields`: Controllare i campi da esportare.</li><li>`eventList.filter`: Specifica i criteri che limitano i risultati inclusi dagli oggetti associati. Si attende un valore minimo richiesto per l&#39;esportazione, in genere una data.</li><li>`eventList.filter.fromIngestTimestamp`: Filtra gli eventi delle serie temporali a quelli che sono stati acquisiti dopo la marca temporale fornita. Questo non è il momento dell’evento stesso ma il momento dell’inserimento degli eventi.</li></ul> |
| `destination` | **(Obbligatorio)** Informazioni sulla destinazione per i dati esportati:<ul><li>`destination.datasetId`: **(Obbligatorio)** L&#39;ID del set di dati in cui devono essere esportati i dati.</li><li>`destination.segmentPerBatch`: *(Facoltativo)* Un valore booleano che, se non viene fornito, utilizza per impostazione predefinita `false`. Un valore di `false` esporta tutti gli ID segmento in un unico ID batch. Un valore di `true` esportazione consente di esportare un ID segmento in un ID batch. Tenete presente che l’impostazione del valore da assegnare `true` può influire sulle prestazioni di esportazione batch.</li></ul> |
| `schema.name` | **(Obbligatorio)** Il nome dello schema associato al dataset in cui devono essere esportati i dati. |
| `evaluationInfo.segmentation` | *(Facoltativo)* Un valore booleano che, se non viene fornito, utilizza per impostazione predefinita `false`. Un valore di `true` indica che la segmentazione deve essere eseguita nel processo di esportazione. |

>[!NOTE]
>
>Per esportare solo i dati del profilo e non includere i dati relativi a ExperienceEvent, rimuovete l’oggetto &quot;AdditionalFields&quot; dalla richiesta.

**Risposta**

Una risposta corretta restituisce un dataset popolato con dati di profilo come specificato nella richiesta.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
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
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

Se non `destination.segmentPerBatch` fosse stato incluso nella richiesta (se non presente, è `false`il valore predefinito) o se il valore fosse stato impostato su `false`, l&#39; `destination` oggetto nella risposta precedente non avrebbe una `batches` matrice e ne avrebbe invece inclusa solo una `batchId`, come mostrato di seguito. Tale batch singolo includerebbe tutti gli ID del segmento, mentre la risposta precedente mostra un ID segmento singolo per ID batch.

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

## Elenca tutti i processi di esportazione

Potete restituire un elenco di tutti i processi di esportazione per una particolare organizzazione IMS eseguendo una richiesta GET all&#39; `export/jobs` endpoint. La richiesta supporta anche i parametri di query `limit` e `offset`, come mostrato di seguito.

**Formato API**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `limit` | Specificare il numero di record da restituire. |
| `offset` | Consente di scostare la pagina dei risultati da restituire in base al numero fornito. |

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

La risposta include un `records` oggetto contenente i processi di esportazione creati dall&#39;organizzazione IMS.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "filter": {
          "segments": [
              {
                  "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff"
              }
          ]
      },
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

Per visualizzare i dettagli di un processo di esportazione specifico o controllarne lo stato durante l&#39;elaborazione, potete effettuare una richiesta GET all&#39; `/export/jobs` endpoint e includere nel percorso `id` il processo di esportazione. Il processo di esportazione viene completato una volta che il `status` campo restituisce il valore &quot;SUCCEEDED&quot;.

**Formato API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | Indica `id` il processo di esportazione a cui si desidera accedere. |

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
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
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
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
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

 Experience Platform consente di annullare un processo di esportazione esistente, che può essere utile per diversi motivi, ad esempio se il processo di esportazione non è stato completato o si è bloccato nella fase di elaborazione. Per annullare un processo di esportazione, potete eseguire una richiesta DELETE all’ `/export/jobs` endpoint e includere il processo `id` di esportazione che desiderate annullare nel percorso della richiesta.

**Formato API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | Indica `id` il processo di esportazione a cui si desidera accedere. |

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

Una volta completata l&#39;esportazione, i dati sono disponibili all&#39;interno del Data Lake in  Experience Platform. Potete quindi utilizzare l&#39;API [di accesso ai](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) dati per accedere ai dati utilizzando l&#39; `batchId` API associata all&#39;esportazione. A seconda delle dimensioni dell’esportazione, i dati possono essere in blocchi e il batch può essere costituito da più file.

Per istruzioni dettagliate su come utilizzare l&#39;API di accesso ai dati per accedere e scaricare file batch, segui l&#39;esercitazione [sull&#39;accesso ai](../../data-access/tutorials/dataset-data.md)dati.

Potete inoltre accedere ai dati del profilo cliente in tempo reale esportati correttamente utilizzando  Adobe Experience Platform Query Service. Utilizzando l&#39;interfaccia utente o l&#39;API RESTful, Query Service consente di scrivere, convalidare ed eseguire query sui dati all&#39;interno del Data Lake.

Per ulteriori informazioni su come eseguire query sui dati del pubblico, consulta la documentazione [del servizio](../../query-service/home.md)Query.