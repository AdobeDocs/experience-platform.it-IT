---
keywords: Experience Platform;home;argomenti popolari;segmentazione;segmentazione;servizio di segmentazione;processi di esportazione;api;
solution: Experience Platform
title: Endpoint API per processi di esportazione segmenti
description: I processi di esportazione sono processi asincroni utilizzati per rendere persistenti i membri del segmento di pubblico nei set di dati. Puoi utilizzare l’endpoint /export/jobs nell’API del servizio di segmentazione di Adobe Experience Platform, che consente di recuperare, creare e annullare a livello di programmazione i processi di esportazione.
exl-id: 5b504a4d-291a-4969-93df-c23ff5994553
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 2%

---

# Endpoint &quot;segment export jobs&quot;

I processi di esportazione sono processi asincroni utilizzati per rendere persistenti i membri del segmento di pubblico nei set di dati. È possibile utilizzare `/export/jobs` nell’API di segmentazione di Adobe Experience Platform, che consente di recuperare, creare e annullare a livello di programmazione i processi di esportazione.

>[!NOTE]
>
>Questa guida descrive l’utilizzo dei processi di esportazione nel [!DNL Segmentation API]. Per informazioni su come gestire i processi di esportazione per [!DNL Real-Time Customer Profile] , consulta la guida su [processi di esportazione nell’API del profilo](../../profile/api/export-jobs.md)

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte del [!DNL Adobe Experience Platform Segmentation Service] API. Prima di continuare, controlla [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all’API, incluse le intestazioni richieste e la lettura di esempi di chiamate API.

## Recuperare un elenco di processi di esportazione {#retrieve-list}

Per recuperare un elenco di tutti i processi di esportazione per l’organizzazione IMS, invia una richiesta GET al `/export/jobs` endpoint.

**Formato API**

Il `/export/jobs` l’endpoint supporta diversi parametri di query per aiutare a filtrare i risultati. Anche se questi parametri sono facoltativi, si consiglia vivamente di utilizzarli per ridurre i costi generali. Effettuando una chiamata a questo endpoint senza parametri, verranno recuperati tutti i processi di esportazione disponibili per la tua organizzazione. È possibile includere più parametri, separati da e commerciali (`&`).

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
| `{STATUS}` | Filtra i risultati in base allo stato. I valori supportati sono &quot;NEW&quot;, &quot;SUCCESSEDED&quot; e &quot;FAILED&quot;. |

**Richiesta**

La seguente richiesta recupererà gli ultimi due processi di esportazione nell’organizzazione IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La seguente risposta restituisce lo stato HTTP 200 con un elenco dei processi di esportazione completati correttamente, in base al parametro di query fornito nel percorso della richiesta.

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
| `destination` | Informazioni sulla destinazione dei dati esportati:<ul><li>`datasetId`: ID del set di dati in cui sono stati esportati i dati.</li><li>`segmentPerBatch`: valore booleano che indica se gli ID segmento sono consolidati o meno. Il valore &quot;false&quot; indica che tutti gli ID segmento vengono esportati in un singolo ID batch. Il valore &quot;true&quot; indica che un ID segmento viene esportato in un ID batch. **Nota:** L&#39;impostazione del valore su true può influire sulle prestazioni dell&#39;esportazione batch.</li></ul> |
| `fields` | Elenco dei campi esportati, separati da virgole. |
| `schema.name` | Nome dello schema associato al set di dati in cui devono essere esportati i dati. |
| `filter.segments` | I segmenti esportati. Sono inclusi i seguenti campi:<ul><li>`segmentId`: ID segmento in cui verranno esportati i profili.</li><li>`segmentNs`: spazio dei nomi del segmento per il dato `segmentID`.</li><li>`status`: array di stringhe che fornisce un filtro di stato per `segmentID`. Per impostazione predefinita, `status` avrà il valore `["realized", "existing"]` che rappresenta tutti i profili che rientrano nel segmento al momento corrente. I valori possibili includono: &quot;realized&quot; (realizzato), &quot;existing&quot; (esistente) ed &quot;exited&quot; (uscito). Il valore &quot;realized&quot; (realizzato) indica che il profilo sta entrando nel segmento. Il valore &quot;existing&quot; indica che il profilo continua a trovarsi nel segmento. Il valore &quot;exiting&quot; (uscita) indica che il profilo sta uscendo dal segmento.</li></ul> |
| `mergePolicy` | Informazioni sui criteri di unione per i dati esportati. |
| `metrics.totalTime` | Campo che indica il tempo totale richiesto per l&#39;esecuzione del processo di esportazione. |
| `metrics.profileExportTime` | Un campo che indica il tempo necessario per l’esportazione dei profili. |
| `page` | Informazioni sull’impaginazione dei processi di esportazione richiesti. |
| `link.next` | Un collegamento alla pagina successiva dei processi di esportazione. |

## Crea un nuovo processo di esportazione {#create}

Per creare un nuovo processo di esportazione, devi effettuare una richiesta POST al `/export/jobs` endpoint.

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
| `fields` | Elenco dei campi esportati, separati da virgole. Se questo campo viene lasciato vuoto, verranno esportati tutti i campi. |
| `mergePolicy` | Specifica il criterio di unione da applicare ai dati esportati. Includi questo parametro quando vengono esportati più segmenti. Se non specificato, l’esportazione accetta lo stesso criterio di unione del segmento specificato. |
| `filter` | Oggetto che specifica i segmenti da includere nel processo di esportazione in base all’ID, al tempo di qualifica o al tempo di acquisizione, a seconda delle sottoproprietà elencate di seguito. Se questo campo viene lasciato vuoto, verranno esportati tutti i dati. |
| `filter.segments` | Specifica i segmenti da esportare. Omettendo questo valore, tutti i dati di tutti i profili vengono esportati. Accetta un array di oggetti segmento, ciascuno contenente i seguenti campi:<ul><li>`segmentId`: **(Obbligatorio se si utilizza `segments`)** ID segmento per i profili da esportare.</li><li>`segmentNs` *(Facoltativo)* Spazio dei nomi del segmento per il dato `segmentID`.</li><li>`status` *(Facoltativo)* Matrice di stringhe che fornisce un filtro di stato per `segmentID`. Per impostazione predefinita, `status` avrà il valore `["realized", "existing"]` che rappresenta tutti i profili che rientrano nel segmento al momento corrente. I valori possibili includono: `"realized"`, `"existing"`, e `"exited"`.  Il valore &quot;realized&quot; (realizzato) indica che il profilo sta entrando nel segmento. Il valore &quot;existing&quot; indica che il profilo continua a trovarsi nel segmento. Il valore &quot;exiting&quot; (uscita) indica che il profilo sta uscendo dal segmento.</li></ul> |
| `filter.segmentQualificationTime` | Filtra in base al tempo di qualifica del segmento. È possibile specificare l&#39;ora di inizio e/o di fine. |
| `filter.segmentQualificationTime.startTime` | Ora di inizio della qualifica del segmento per un ID segmento per un determinato stato. Se non specificato, non sarà presente alcun filtro sull’ora di inizio per la qualifica di un ID segmento. La marca temporale deve essere fornita in [RFC 3339](https://tools.ietf.org/html/rfc3339) formato. |
| `filter.segmentQualificationTime.endTime` | Ora di fine della qualifica del segmento per un ID segmento per un determinato stato. Se non specificato, non sarà presente alcun filtro sull’ora di fine per la qualifica di un ID segmento. La marca temporale deve essere fornita in [RFC 3339](https://tools.ietf.org/html/rfc3339) formato. |
| `filter.fromIngestTimestamp ` | Limita i profili esportati a includere solo quelli che sono stati aggiornati dopo questa marca temporale. La marca temporale deve essere fornita in [RFC 3339](https://tools.ietf.org/html/rfc3339) formato. <ul><li>`fromIngestTimestamp` per **profili**, se fornito: include tutti i profili uniti in cui la marca temporale aggiornata unita è maggiore della marca temporale specificata. Supporti `greater_than` operando.</li><li>`fromIngestTimestamp` per **Eventi**: tutti gli eventi acquisiti dopo questa marca temporale verranno esportati in modo corrispondente al risultato del profilo risultante. Non è l’ora dell’evento in sé, ma il tempo di acquisizione degli eventi.</li> |
| `filter.emptyProfiles` | Valore booleano che indica se filtrare i profili vuoti. I profili possono contenere record di profilo, record ExperienceEvent o entrambi. I profili senza record di profilo e solo i record ExperienceEvent sono denominati &quot;emptyProfiles&quot;. Per esportare tutti i profili nell’archivio dei profili, inclusi i &quot;emptyProfiles&quot;, imposta il valore di `emptyProfiles` a `true`. Se `emptyProfiles` è impostato su `false`, vengono esportati solo i profili con record di profilo nell’archivio. Per impostazione predefinita, se `emptyProfiles` non è incluso, vengono esportati solo i profili contenenti record di profilo. |
| `additionalFields.eventList` | Controlla i campi evento della serie temporale esportati per gli oggetti figlio o associati fornendo una o più delle seguenti impostazioni:<ul><li>`fields`: controlla i campi da esportare.</li><li>`filter`: specifica i criteri che limitano i risultati inclusi dagli oggetti associati. Prevede un valore minimo richiesto per l&#39;esportazione, in genere una data.</li><li>`filter.fromIngestTimestamp`: filtra gli eventi della serie temporale con quelli che sono stati acquisiti dopo la marca temporale fornita. Non è l’ora dell’evento in sé, ma il tempo di acquisizione degli eventi.</li><li>`filter.toIngestTimestamp`: filtra la marca temporale in base a quelle che sono state acquisite prima della marca temporale fornita. Non è l’ora dell’evento in sé, ma il tempo di acquisizione degli eventi.</li></ul> |
| `destination` | **(Obbligatorio)** Informazioni sui dati esportati:<ul><li>`datasetId`: **(Obbligatorio)** ID del set di dati in cui devono essere esportati i dati.</li><li>`segmentPerBatch`: *(Facoltativo)* Valore booleano che, se non specificato, viene impostato automaticamente su &quot;false&quot;. Il valore &quot;false&quot; esporta tutti gli ID segmento in un singolo ID batch. Il valore &quot;true&quot; esporta un ID segmento in un ID batch. L&#39;impostazione del valore su &quot;true&quot; può influire sulle prestazioni di esportazione batch.</li></ul> |
| `schema.name` | **(Obbligatorio)** Nome dello schema associato al set di dati in cui devono essere esportati i dati. |
| `evaluationInfo.segmentation` | *(Facoltativo)* Valore booleano che, se non specificato, viene utilizzato per impostazione predefinita `false`. Un valore di `true` indica che è necessario eseguire la segmentazione sul processo di esportazione. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli del nuovo processo di esportazione creato.

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

In alternativa, se `destination.segmentPerBatch` è stato impostato su `true`, il `destination` l&#39;oggetto di cui sopra avrebbe un `batches` come mostrato di seguito:

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

## Recuperare un processo di esportazione specifico {#get}

Per recuperare informazioni dettagliate su un processo di esportazione specifico, devi effettuare una richiesta GET al `/export/jobs` e fornendo l’ID del processo di esportazione che desideri recuperare nel percorso della richiesta.

**Formato API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | Il `id` del processo di esportazione a cui desideri accedere. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni dettagliate sul processo di esportazione specificato.

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
| `destination` | Informazioni sulla destinazione dei dati esportati:<ul><li>`datasetId`: ID del set di dati in cui sono stati esportati i dati.</li><li>`segmentPerBatch`: valore booleano che indica se gli ID segmento sono consolidati o meno. Un valore di `false` significa che tutti gli ID del segmento erano in un singolo ID batch. Un valore di `true` significa che un ID segmento viene esportato in un ID batch.</li></ul> |
| `fields` | Elenco dei campi esportati, separati da virgole. |
| `schema.name` | Nome dello schema associato al set di dati in cui devono essere esportati i dati. |
| `filter.segments` | I segmenti esportati. Sono inclusi i seguenti campi:<ul><li>`segmentId`: ID segmento per i profili da esportare.</li><li>`segmentNs`: spazio dei nomi del segmento per il dato `segmentID`.</li><li>`status`: array di stringhe che fornisce un filtro di stato per `segmentID`. Per impostazione predefinita, `status` avrà il valore `["realized", "existing"]` che rappresenta tutti i profili che rientrano nel segmento al momento corrente. I valori possibili includono: &quot;realized&quot; (realizzato), &quot;existing&quot; (esistente) ed &quot;exited&quot; (uscito).  Il valore &quot;realized&quot; (realizzato) indica che il profilo sta entrando nel segmento. Il valore &quot;existing&quot; indica che il profilo continua a trovarsi nel segmento. Il valore &quot;exiting&quot; (uscita) indica che il profilo sta uscendo dal segmento.</li></ul> |
| `mergePolicy` | Informazioni sui criteri di unione per i dati esportati. |
| `metrics.totalTime` | Campo che indica il tempo totale richiesto per l&#39;esecuzione del processo di esportazione. |
| `metrics.profileExportTime` | Un campo che indica il tempo necessario per l’esportazione dei profili. |
| `totalExportedProfileCounter` | Numero totale di profili esportati in tutti i batch. |

## Annullare o eliminare un processo di esportazione specifico {#delete}

Per richiedere l’eliminazione del processo di esportazione specificato, effettua una richiesta DELETE al `/export/jobs` e fornendo l’ID del processo di esportazione da eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | Il `id` del processo di esportazione che desideri eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 con il seguente messaggio:

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## Passaggi successivi

Dopo aver letto questa guida ora hai una migliore comprensione di come funzionano i processi di esportazione.
