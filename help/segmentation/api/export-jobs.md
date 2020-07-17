---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida all’endpoint dei processi di esportazione
topic: developer guide
translation-type: tm+mt
source-git-commit: 3e39333207ef6c94b6d792be33a4605f185ff5ab
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 2%

---


# Guida all’endpoint dei processi di esportazione

I processi di esportazione sono processi asincroni utilizzati per mantenere i membri del segmento di pubblico nei set di dati. Potete utilizzare l&#39; `/export/jobs` endpoint nell&#39;API di segmentazione  Adobe Experience Platform, che consente di recuperare, creare e annullare i processi di esportazione a livello di programmazione.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte dell&#39; [!DNL Adobe Experience Platform Segmentation Service] API. Prima di continuare, controllate la guida [](./getting-started.md) introduttiva per informazioni importanti che dovete conoscere per effettuare correttamente le chiamate all&#39;API, comprese le intestazioni richieste e come leggere le chiamate API di esempio.

## Recuperare un elenco di processi di esportazione {#retrieve-list}

È possibile recuperare un elenco di tutti i processi di esportazione per l&#39;organizzazione IMS effettuando una richiesta GET all&#39; `/export/jobs` endpoint.

**Formato API**

L&#39; `/export/jobs` endpoint supporta diversi parametri di query per facilitare il filtraggio dei risultati. Anche se questi parametri sono opzionali, il loro utilizzo è fortemente consigliato per ridurre i costi di sovraccarico. Effettuando una chiamata a questo endpoint senza parametri, tutti i processi di esportazione disponibili per la vostra organizzazione verranno recuperati. È possibile includere più parametri, separati da e-mail (`&`).

```http
GET /export/jobs
GET /export/jobs?limit={LIMIT}
GET /export/jobs?offset={OFFSET}
GET /export/jobs?status={STATUS}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{LIMIT}` | Specifica il numero di processi di esportazione restituiti. |
| `{OFFSET}` | Specifica l&#39;offset delle pagine di risultati. |
| `{STATUS}` | Filtra i risultati in base allo stato. I valori supportati sono &quot;NEW&quot;, &quot;SUCCEEDED&quot; e &quot;FAILED&quot;. |

**Richiesta**

Nella seguente richiesta vengono recuperati gli ultimi due processi di esportazione all’interno dell’organizzazione IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta seguente restituisce lo stato HTTP 200 con un elenco di processi di esportazione completati correttamente, in base al parametro di query fornito nel percorso della richiesta.

```json
{
    "records": [
        {
            "id": 100,
            "jobType": "BATCH",
            "destination": {
                "datasetId": "5b7c86968f7b6501e21ba9df",
                "segmentPerBatch": false,
                "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
            },
            "fields": "identities.id,personalEmail.address",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
            "status": "SUCCEEDED",
            "filter": {
                "segments": [
                    {
                        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                        "segmentNs": "ups",
                        "status": [
                            "realized"
                        ]
                    }
                ]
            },
            "mergePolicy": {
                "id": "timestampOrdered-none-mp",
                "version": 1
            },
            "profileInstanceId": "ups",
            "errors": [
                {
                    "code": "0100000003",
                    "msg": "Error in Export Job",
                    "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger"
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 123456789000,
                    "endTimeInMs": 123456799000,
                    "totalTimeInMs": 10000
                },
                "profileExportTime": {
                    "startTimeInMs": 123456789000,
                    "endTimeInMs": 123456799000,
                    "totalTimeInMs": 10000
                },
                "totalExportedProfileCounter": 20,
                "exportedProfileByNamespaceCounter": {
                    "namespace1": 10,
                    "namespace2": 5
                }
            },
            "computeGatewayJobId": {
                "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
            },
            "creationTime": 1538615973895,
            "updateTime": 1538616233239,
            "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
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
                        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                        "segmentNs": "AAM",
                        "status": ["realized", "existing"]
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
                "segmentPerBatch": false,
                "batchId": "IWEQ6920712f9475762D"
            },
            "updateTime": 1538573922551,
            "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
            "creationTime": 1538573416687
        }
    ],
    "page":{
        "sortField": "createdTime",
        "sort": "desc",
        "pageOffset": "1540974701302_96",
        "pageSize": 2
    },
    "link":{
        "next": "/export/jobs/?limit=2&offset=1538573416687_722"
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `destination` | Informazioni sulla destinazione dei dati esportati:<ul><li>`datasetId`: ID del set di dati in cui sono stati esportati i dati.</li><li>`segmentPerBatch`: Un valore booleano che mostra se gli ID del segmento sono consolidati o meno. Il valore &quot;false&quot; indica che tutti gli ID del segmento vengono esportati in un unico ID batch. Il valore &quot;true&quot; indica che un ID segmento viene esportato in un ID batch. **Nota:** L&#39;impostazione del valore su true può influire sulle prestazioni dell&#39;esportazione batch.</li></ul> |
| `fields` | Elenco dei campi esportati, separati da virgole. |
| `schema.name` | Nome dello schema associato al dataset in cui devono essere esportati i dati. |
| `filter.segments` | I segmenti esportati. Sono inclusi i campi seguenti:<ul><li>`segmentId`: L’ID del segmento in cui verranno esportati i profili.</li><li>`segmentNs`: Spazio dei nomi del segmento per il dato `segmentID`.</li><li>`status`: Un array di stringhe che fornisce un filtro di stato per l&#39;oggetto `segmentID`. Per impostazione predefinita, `status` il valore `["realized", "existing"]` rappresenta tutti i profili che rientrano nel segmento al momento corrente. I valori possibili sono: &quot;realizzate&quot;, &quot;esistenti&quot; e &quot;uscite&quot;.</li></ul> |
| `mergePolicy` | Unisci informazioni sul criterio per i dati esportati. |
| `metrics.totalTime` | Campo che indica il tempo totale di esecuzione del processo di esportazione. |
| `metrics.profileExportTime` | Campo che indica il tempo necessario per l&#39;esportazione dei profili. |
| `page` | Informazioni sull’impaginazione dei processi di esportazione richiesti. |
| `link.next` | Collegamento alla pagina successiva dei processi di esportazione. |

## Creare un nuovo processo di esportazione {#create}

Per creare un nuovo processo di esportazione, effettuate una richiesta POST all’ `/export/jobs` endpoint.

**Formato API**

```http
POST /export/jobs
```

**Richiesta**

La richiesta seguente crea un nuovo processo di esportazione, configurato dai parametri forniti nel payload.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status": [
                    "realized"
                ]
            }
        ],
        "segmentQualificationTime": {
            "startTime": "2018-01-01T00:00:00Z",
            "endTime": "2018-02-01T00:00:00Z"
        },
        "fromIngestTimestamp": "2018-01-01T00:00:00Z",
        "emptyProfiles": true
    },
    "additionalFields": {
        "eventList": {
            "fields": "string",
            "filter": {
                "fromIngestTimestamp": "2018-01-01T00:00:00Z",
                "toIngestTimestamp": "2020-01-01T00:00:00Z"
            }
        }
    },
    "destination":{
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false
    },
    "schema":{
        "name": "_xdm.context.profile"
    }
}'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `fields` | Elenco dei campi esportati, separati da virgole. Se lasciato vuoto, verranno esportati tutti i campi. |
| `mergePolicy` | Specifica il criterio di unione da applicare ai dati esportati. Includete questo parametro quando vi sono più segmenti da esportare. Se non viene fornito, l&#39;esportazione avrà lo stesso criterio di unione del segmento specificato. |
| `filter` | Un oggetto che specifica i segmenti che verranno inclusi nel processo di esportazione per ID, tempo di qualifica o tempo di caricamento, a seconda delle proprietà secondarie elencate di seguito. Se lasciato vuoto, tutti i dati verranno esportati. |
| `filter.segments` | Specifica i segmenti da esportare. Se si omette questo valore, verranno esportati tutti i dati di tutti i profili. Accetta un array di oggetti segmento, ciascuno dei quali contiene i campi seguenti:<ul><li>`segmentId`: **(Obbligatorio se si utilizza`segments`)** ID segmento per i profili da esportare.</li><li>`segmentNs` *(Facoltativo)* Spazio dei nomi del segmento per il dato `segmentID`.</li><li>`status` *(Facoltativo)* Un array di stringhe che fornisce un filtro di stato per l&#39;oggetto `segmentID`. Per impostazione predefinita, `status` il valore `["realized", "existing"]` rappresenta tutti i profili che rientrano nel segmento al momento corrente. I valori possibili sono: `"realized"`, `"existing"`e `"exited"`.</li></ul> |
| `filter.segmentQualificationTime` | Filtra in base al tempo di qualificazione del segmento. È possibile specificare l&#39;ora di inizio e/o di fine. |
| `filter.segmentQualificationTime.startTime` | Ora di inizio della qualifica del segmento per un ID segmento per un dato stato. Non viene fornito, non verrà applicato alcun filtro all&#39;ora di inizio per la qualifica ID segmento. La marca temporale deve essere fornita in formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.segmentQualificationTime.endTime` | Ora di fine qualifica segmento per un ID segmento per un dato stato. Non viene fornito, non verrà applicato alcun filtro all&#39;ora di fine per la qualifica di ID segmento. La marca temporale deve essere fornita in formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.fromIngestTimestamp ` | Limita i profili esportati a includere solo quelli che sono stati aggiornati dopo questa marca temporale. La marca temporale deve essere fornita in formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . <ul><li>`fromIngestTimestamp` per **i profili**, se forniti: Include tutti i profili uniti in cui la marca temporale aggiornata unita è maggiore della marca temporale specificata. Supporta `greater_than` l&#39;operando.</li><li>`fromIngestTimestamp` per **gli eventi**: Tutti gli eventi acquisiti dopo questa marca temporale verranno esportati in base al risultato del profilo risultante. Questo non è il momento dell’evento stesso ma il momento dell’inserimento degli eventi.</li> |
| `filter.emptyProfiles` | Un valore booleano che indica se filtrare i profili vuoti. I profili possono contenere record di profilo, record ExperienceEvent o entrambi. I profili senza record di profilo e solo i record ExperienceEvent sono denominati &quot;emptyProfiles&quot;. Per esportare tutti i profili nell’archivio profili, inclusi i &quot;emptyProfiles&quot;, impostate il valore di `emptyProfiles` su `true`. Se `emptyProfiles` è impostato su `false`, vengono esportati solo i profili con record di profilo nello store. Per impostazione predefinita, se `emptyProfiles` l&#39;attributo non è incluso, vengono esportati solo i profili che contengono record di profilo. |
| `additionalFields.eventList` | Controlla i campi evento delle serie temporali esportati per oggetti secondari o associati fornendo una o più delle seguenti impostazioni:<ul><li>`fields`: Controllare i campi da esportare.</li><li>`filter`: Specifica i criteri che limitano i risultati inclusi dagli oggetti associati. Si attende un valore minimo richiesto per l&#39;esportazione, in genere una data.</li><li>`filter.fromIngestTimestamp`: Filtra gli eventi della serie temporale a quelli che sono stati acquisiti dopo la marca temporale fornita. Questo non è il momento dell’evento stesso ma il momento dell’inserimento degli eventi.</li><li>`filter.toIngestTimestamp`: Filtra la marca temporale a quelle che sono state caricate prima della marca temporale specificata. Questo non è il momento dell’evento stesso ma il momento dell’inserimento degli eventi.</li></ul> |
| `destination` | **(Obbligatorio)** Informazioni sui dati esportati:<ul><li>`datasetId`: **(Obbligatorio)** L&#39;ID del set di dati in cui devono essere esportati i dati.</li><li>`segmentPerBatch`: *(Facoltativo)* Un valore booleano che, se non viene fornito, per impostazione predefinita è &quot;false&quot;. Il valore &quot;false&quot; esporta tutti gli ID segmento in un unico ID batch. Il valore &quot;true&quot; esporta un ID segmento in un ID batch. Tenete presente che l’impostazione del valore su &quot;true&quot; può influire sulle prestazioni di esportazione batch.</li></ul> |
| `schema.name` | **(Obbligatorio)** Il nome dello schema associato al dataset in cui devono essere esportati i dati. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli del processo di esportazione appena creato.

```json
{
    "id": 100,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{IMS_ORG}",
    "status": "NEW",
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status": [
                    "realized"
                ]
            }
        ],
        "segmentQualificationTime": {
            "startTime": "2018-01-01T00:00:00Z",
            "endTime": "2018-02-01T00:00:00Z"
        },
        "fromIngestTimestamp": "2018-01-01T00:00:00Z",
        "emptyProfiles": true
    },
    "additionalFields": {
        "eventList": {
            "fields": "_id, _experience",
            "filter": {
                "fromIngestTimestamp": "2018-01-01T00:00:00Z"
            }
        }
    },
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "profileInstanceId": "ups",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 123456789000,
        }
    },
    "computeGatewayJobId": {
        "exportJob": ""    
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | Valore di sola lettura generato dal sistema che identifica il processo di esportazione appena creato. |

In alternativa, se `destination.segmentPerBatch` fosse stato impostato su `true`, l&#39; `destination` oggetto sopra avrebbe una `batches` matrice, come illustrato di seguito:

```json
    "destination": {
        "dataSetId" : "{DATASET_ID}",
        "segmentPerBatch": true,
        "batches" : [
            {
                "segmentId": "segment1",
                "segmentNs": "ups",
                "status": ["realized"],
                "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
            },
            {
                "segmentId": "segment2",
                "segmentNs": "AdCloud",
                "status": "exited",
                "batchId": "df4gssdfb93a09f7e37fa53ad52"
            }
        ]
    }
```

## Recuperare un processo di esportazione specifico {#get}

Potete recuperare informazioni dettagliate su un processo di esportazione specifico eseguendo una richiesta GET all&#39; `/export/jobs` endpoint e fornendo l&#39;ID del processo di esportazione che desiderate recuperare nel percorso della richiesta.

**Formato API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | Indica `id` il processo di esportazione a cui si desidera accedere. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sul processo di esportazione specificato.

```json
{
    "id": 11037,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{IMS_ORG}",
    "status": "SUCCEEDED",
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status":[
                    "realized"
                ]
            }
        ]
    },
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "profileInstanceId": "ups",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 123456789000,
            "endTimeInMs": 123456799000,
            "totalTimeInMs": 10000
        },
        "profileExportTime": {
            "startTimeInMs": 123456789000,
            "endTimeInMs": 123456799000,
            "totalTimeInMs": 10000
        },
        "totalExportedProfileCounter": 20,
        "exportedProfileByNamespaceCounter": {
            "namespace1": 10,
            "namespace2": 5
        }
    },
    "computeGatewayJobId": {
        "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `destination` | Informazioni sulla destinazione dei dati esportati:<ul><li>`datasetId`: ID del set di dati in cui sono stati esportati i dati.</li><li>`segmentPerBatch`: Un valore booleano che mostra se gli ID del segmento sono consolidati o meno. Un valore di `false` indica che tutti gli ID del segmento erano in un unico ID batch. Un valore `true` indica che un ID segmento viene esportato in un ID batch.</li></ul> |
| `fields` | Elenco dei campi esportati, separati da virgole. |
| `schema.name` | Nome dello schema associato al dataset in cui devono essere esportati i dati. |
| `filter.segments` | I segmenti esportati. Sono inclusi i campi seguenti:<ul><li>`segmentId`: ID segmento per i profili da esportare.</li><li>`segmentNs`: Spazio dei nomi del segmento per il dato `segmentID`.</li><li>`status`: Un array di stringhe che fornisce un filtro di stato per l&#39;oggetto `segmentID`. Per impostazione predefinita, `status` il valore `["realized", "existing"]` rappresenta tutti i profili che rientrano nel segmento al momento corrente. I valori possibili sono: &quot;realizzate&quot;, &quot;esistenti&quot; e &quot;uscite&quot;.</li></ul> |
| `mergePolicy` | Unisci informazioni sul criterio per i dati esportati. |
| `metrics.totalTime` | Campo che indica il tempo totale di esecuzione del processo di esportazione. |
| `metrics.profileExportTime` | Campo che indica il tempo necessario per l&#39;esportazione dei profili. |
| `totalExportedProfileCounter` | Numero totale di profili esportati in tutti i batch. |

## Annullare o eliminare un processo di esportazione specifico {#delete}

Potete richiedere di eliminare il processo di esportazione specificato eseguendo una richiesta di DELETE all’ `/export/jobs` endpoint e fornendo l’ID del processo di esportazione da eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | Indica `id` il processo di esportazione da eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 con il seguente messaggio:

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## Passaggi successivi

Dopo aver letto questa guida è ora possibile comprendere meglio come funzionano i processi di esportazione.