---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;processi di esportazione;api;
solution: Experience Platform
title: Endpoint API per i processi di esportazione
topic-legacy: developer guide
description: I processi di esportazione sono processi asincroni utilizzati per mantenere i membri dei segmenti di pubblico nei set di dati. Puoi utilizzare l’endpoint /export/jobs nell’API del servizio di segmentazione di Adobe Experience Platform, che consente di recuperare, creare e annullare programmaticamente i processi di esportazione.
exl-id: 5b504a4d-291a-4969-93df-c23ff5994553
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1680'
ht-degree: 2%

---

# Endpoint per processi di esportazione

I processi di esportazione sono processi asincroni utilizzati per mantenere i membri dei segmenti di pubblico nei set di dati. È possibile utilizzare `/export/jobs` endpoint nell’API di segmentazione di Adobe Experience Platform, che consente di recuperare, creare e annullare programmaticamente i processi di esportazione.

>[!NOTE]
>
>Questa guida riguarda l’utilizzo dei posti di lavoro per le esportazioni [!DNL Segmentation API]. Per informazioni su come gestire i processi di esportazione per [!DNL Real-time Customer Profile] dati, consulta la guida su [esportazione di lavori nell’API del profilo](../../profile/api/export-jobs.md)

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte del [!DNL Adobe Experience Platform Segmentation Service] API. Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, comprese le intestazioni richieste e come leggere le chiamate API di esempio.

## Recupera un elenco di processi di esportazione {#retrieve-list}

Puoi recuperare un elenco di tutti i processi di esportazione per la tua organizzazione IMS effettuando una richiesta di GET al `/export/jobs` punto finale.

**Formato API**

La `/export/jobs` l’endpoint supporta diversi parametri di query per facilitare il filtraggio dei risultati. Sebbene questi parametri siano opzionali, si consiglia vivamente di utilizzarli per ridurre i costi di overhead. Effettuare una chiamata a questo endpoint senza parametri recupererà tutti i processi di esportazione disponibili per la tua organizzazione. È possibile includere più parametri, separati da e commerciale (`&`).

```http
GET /export/jobs
GET /export/jobs?limit={LIMIT}
GET /export/jobs?offset={OFFSET}
GET /export/jobs?status={STATUS}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{LIMIT}` | Specifica il numero di processi di esportazione restituiti. |
| `{OFFSET}` | Specifica l&#39;offset delle pagine dei risultati. |
| `{STATUS}` | Filtra i risultati in base allo stato. I valori supportati sono &quot;NEW&quot;, &quot;SUCCEEDED&quot; e &quot;FAILED&quot;. |

**Richiesta**

La seguente richiesta recupererà gli ultimi due processi di esportazione all’interno dell’organizzazione IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `destination` | Informazioni sulla destinazione per i dati esportati:<ul><li>`datasetId`: ID del set di dati in cui sono stati esportati i dati.</li><li>`segmentPerBatch`: Un valore booleano che indica se gli ID del segmento sono consolidati o meno. Il valore &quot;false&quot; indica che tutti gli ID del segmento vengono esportati in un singolo ID batch. Il valore &quot;true&quot; indica che un ID segmento viene esportato in un ID batch. **Nota:** L&#39;impostazione del valore su true può influire sulle prestazioni dell&#39;esportazione batch.</li></ul> |
| `fields` | Elenco dei campi esportati, separati da virgole. |
| `schema.name` | Nome dello schema associato al set di dati in cui devono essere esportati i dati. |
| `filter.segments` | I segmenti esportati. Sono inclusi i campi seguenti:<ul><li>`segmentId`: L’ID del segmento in cui verranno esportati i profili.</li><li>`segmentNs`: Spazio dei nomi del segmento per la `segmentID`.</li><li>`status`: Matrice di stringhe che fornisce un filtro di stato per il `segmentID`. Per impostazione predefinita, `status` avrà il valore `["realized", "existing"]` che rappresenta tutti i profili che rientrano nel segmento al momento corrente. I valori possibili sono: &quot;realizzato&quot;, &quot;esistente&quot; e &quot;uscito&quot;. Un valore di &quot;realizzato&quot; indica che il profilo sta entrando nel segmento. Un valore di &quot;esistente&quot; indica che il profilo continua a trovarsi nel segmento. Un valore di &quot;exiting&quot; indica che il profilo sta uscendo dal segmento.</li></ul> |
| `mergePolicy` | Informazioni sui criteri di unione per i dati esportati. |
| `metrics.totalTime` | Campo che indica il tempo totale di esecuzione del processo di esportazione. |
| `metrics.profileExportTime` | Campo che indica il tempo necessario all’esportazione dei profili. |
| `page` | Informazioni sull’impaginazione dei processi di esportazione richiesti. |
| `link.next` | Collegamento alla pagina successiva dei processi di esportazione. |

## Crea un nuovo processo di esportazione {#create}

Puoi creare un nuovo processo di esportazione effettuando una richiesta POST al `/export/jobs` punto finale.

**Formato API**

```http
POST /export/jobs
```

**Richiesta**

La seguente richiesta crea un nuovo processo di esportazione, configurato dai parametri forniti nel payload.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    },
    "evaluationInfo": {
        "segmentation": true
    }
}'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `fields` | Elenco dei campi esportati, separati da virgole. Se lasciato vuoto, verranno esportati tutti i campi. |
| `mergePolicy` | Specifica il criterio di unione per la gestione dei dati esportati. Includi questo parametro quando sono in corso l’esportazione di più segmenti. Se non viene fornito, l’esportazione avrà lo stesso criterio di unione del segmento specificato. |
| `filter` | Un oggetto che specifica i segmenti che verranno inclusi nel processo di esportazione per ID, tempo di qualificazione o tempo di acquisizione, a seconda delle proprietà secondarie elencate di seguito. Se lasciato vuoto, verranno esportati tutti i dati. |
| `filter.segments` | Specifica i segmenti da esportare. Se si omette questo valore, verranno esportati tutti i dati di tutti i profili. Accetta una matrice di oggetti segmento, ciascuno contenente i campi seguenti:<ul><li>`segmentId`: **(Obbligatorio se si utilizza `segments`)** ID segmento per i profili da esportare.</li><li>`segmentNs` *(Facoltativo)* Spazio dei nomi del segmento per la `segmentID`.</li><li>`status` *(Facoltativo)* Matrice di stringhe che fornisce un filtro di stato per il `segmentID`. Per impostazione predefinita, `status` avrà il valore `["realized", "existing"]` che rappresenta tutti i profili che rientrano nel segmento al momento corrente. I valori possibili sono: `"realized"`, `"existing"`e `"exited"`.  Un valore di &quot;realizzato&quot; indica che il profilo sta entrando nel segmento. Un valore di &quot;esistente&quot; indica che il profilo continua a trovarsi nel segmento. Un valore di &quot;exiting&quot; indica che il profilo sta uscendo dal segmento.</li></ul> |
| `filter.segmentQualificationTime` | Filtra in base al tempo di qualificazione del segmento. È possibile specificare l’ora di inizio e/o di fine. |
| `filter.segmentQualificationTime.startTime` | Ora di inizio della qualifica del segmento per un ID segmento per un dato stato. Non viene fornito, non ci saranno filtri all&#39;ora di inizio per la qualifica di un ID segmento. La marca temporale deve essere fornita in [RFC 3339](https://tools.ietf.org/html/rfc3339) formato. |
| `filter.segmentQualificationTime.endTime` | Ora di fine della qualifica del segmento per un ID segmento per un dato stato. Non viene fornito, non ci saranno filtri all&#39;ora di fine per la qualifica di un ID segmento. La marca temporale deve essere fornita in [RFC 3339](https://tools.ietf.org/html/rfc3339) formato. |
| `filter.fromIngestTimestamp ` | Limita i profili esportati a includere solo quelli che sono stati aggiornati dopo questa marca temporale. La marca temporale deve essere fornita in [RFC 3339](https://tools.ietf.org/html/rfc3339) formato. <ul><li>`fromIngestTimestamp` per **profiles**, se fornito: Include tutti i profili uniti in cui la marca temporale aggiornata unita è maggiore della marca temporale specificata. Supporti `greater_than` operando.</li><li>`fromIngestTimestamp` per **events**: Tutti gli eventi acquisiti dopo questa marca temporale verranno esportati in base al risultato del profilo risultante. Questo non è il momento dell’evento stesso, ma il momento dell’acquisizione degli eventi.</li> |
| `filter.emptyProfiles` | Un valore booleano che indica se filtrare i profili vuoti. I profili possono contenere record di profilo, record ExperienceEvent o entrambi. I profili senza record di profilo e solo i record ExperienceEvent sono denominati &quot;emptyProfiles&quot;. Per esportare tutti i profili nell’archivio dei profili, inclusi i &quot;emptyProfiles&quot;, imposta il valore di `emptyProfiles` a `true`. Se `emptyProfiles` è impostato su `false`, vengono esportati solo i profili con record di profilo nell’archivio. Per impostazione predefinita, se `emptyProfiles` l’attributo non è incluso, vengono esportati solo i profili contenenti record di profilo. |
| `additionalFields.eventList` | Controlla i campi evento serie temporale esportati per oggetti secondari o associati fornendo una o più delle seguenti impostazioni:<ul><li>`fields`: Controlla i campi da esportare.</li><li>`filter`: Specifica i criteri che limitano i risultati inclusi dagli oggetti associati. Si attende un valore minimo necessario per l’esportazione, in genere una data.</li><li>`filter.fromIngestTimestamp`: Filtra gli eventi delle serie temporali in quelli che sono stati acquisiti dopo la marca temporale fornita. Questo non è il momento dell’evento stesso, ma il momento dell’acquisizione degli eventi.</li><li>`filter.toIngestTimestamp`: Filtra la marca temporale per quelle che sono state acquisite prima della marca temporale fornita. Questo non è il momento dell’evento stesso, ma il momento dell’acquisizione degli eventi.</li></ul> |
| `destination` | **(Obbligatorio)** Informazioni sui dati esportati:<ul><li>`datasetId`: **(Obbligatorio)** ID del set di dati in cui devono essere esportati i dati.</li><li>`segmentPerBatch`: *(Facoltativo)* Un valore booleano che, se non specificato, viene impostato automaticamente su &quot;false&quot;. Il valore &quot;false&quot; esporta tutti gli ID segmento in un singolo ID batch. Il valore &quot;true&quot; esporta un ID segmento in un ID batch. Tieni presente che l’impostazione del valore su &quot;true&quot; può influire sulle prestazioni dell’esportazione batch.</li></ul> |
| `schema.name` | **(Obbligatorio)** Nome dello schema associato al set di dati in cui devono essere esportati i dati. |
| `evaluationInfo.segmentation` | *(Facoltativo)* Un valore booleano che, se non viene fornito, utilizza per impostazione predefinita `false`. Un valore di `true` indica che la segmentazione deve essere eseguita sul processo di esportazione. |

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
    "imsOrgId": "{ORG_ID}",
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

In alternativa, se `destination.segmentPerBatch` è stato impostato su `true`, `destination` l&#39;oggetto sopra avrebbe un `batches` come mostrato di seguito:

```json
    "destination": {
        "dataSetId": "{DATASET_ID}",
        "segmentPerBatch": true,
        "batches": [
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

## Recupera un processo di esportazione specifico {#get}

Puoi recuperare informazioni dettagliate su un processo di esportazione specifico effettuando una richiesta di GET al `/export/jobs` e fornendo l&#39;ID del processo di esportazione che si desidera recuperare nel percorso della richiesta.

**Formato API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | La `id` del processo di esportazione a cui si desidera accedere. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrgId": "{ORG_ID}",
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
| `destination` | Informazioni sulla destinazione per i dati esportati:<ul><li>`datasetId`: ID del set di dati in cui sono stati esportati i dati.</li><li>`segmentPerBatch`: Un valore booleano che indica se gli ID del segmento sono consolidati o meno. Un valore di `false` significa che tutti gli ID del segmento erano in un singolo ID batch. Un valore di `true` significa che un ID segmento viene esportato in un ID batch.</li></ul> |
| `fields` | Elenco dei campi esportati, separati da virgole. |
| `schema.name` | Nome dello schema associato al set di dati in cui devono essere esportati i dati. |
| `filter.segments` | I segmenti esportati. Sono inclusi i campi seguenti:<ul><li>`segmentId`: ID segmento per i profili da esportare.</li><li>`segmentNs`: Spazio dei nomi del segmento per la `segmentID`.</li><li>`status`: Matrice di stringhe che fornisce un filtro di stato per il `segmentID`. Per impostazione predefinita, `status` avrà il valore `["realized", "existing"]` che rappresenta tutti i profili che rientrano nel segmento al momento corrente. I valori possibili sono: &quot;realizzato&quot;, &quot;esistente&quot; e &quot;uscito&quot;.  Un valore di &quot;realizzato&quot; indica che il profilo sta entrando nel segmento. Un valore di &quot;esistente&quot; indica che il profilo continua a trovarsi nel segmento. Un valore di &quot;exiting&quot; indica che il profilo sta uscendo dal segmento.</li></ul> |
| `mergePolicy` | Informazioni sui criteri di unione per i dati esportati. |
| `metrics.totalTime` | Campo che indica il tempo totale di esecuzione del processo di esportazione. |
| `metrics.profileExportTime` | Campo che indica il tempo necessario all’esportazione dei profili. |
| `totalExportedProfileCounter` | Il numero totale di profili esportati in tutti i batch. |

## Annullare o eliminare un processo di esportazione specifico {#delete}

Puoi richiedere di eliminare il processo di esportazione specificato effettuando una richiesta di DELETE al `/export/jobs` e fornendo l&#39;ID del processo di esportazione da eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | La `id` del processo di esportazione da eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Dopo aver letto questa guida hai ora una migliore comprensione di come funzionano i lavori di esportazione.
