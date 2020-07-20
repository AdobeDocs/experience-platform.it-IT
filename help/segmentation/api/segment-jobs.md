---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Processi segmento
topic: developer guide
translation-type: tm+mt
source-git-commit: b3e6a6f1671a456b2ffa61139247c5799c495d92
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 3%

---


# Endpoint processi segmento

Un processo di segmento è un processo asincrono che crea un nuovo segmento di pubblico. Fa riferimento a una definizione [di](./segment-definitions.md)segmento, nonché a eventuali criteri [di](../../profile/api/merge-policies.md) unione che controllano il modo in cui [!DNL Real-time Customer Profile] unisce gli attributi sovrapposti nei frammenti di profilo. Quando un processo del segmento viene completato correttamente, potete raccogliere varie informazioni sul segmento, ad esempio eventuali errori che si sono verificati durante l&#39;elaborazione e le dimensioni finali del pubblico.

Questa guida fornisce informazioni utili per comprendere meglio i processi dei segmenti e include chiamate API di esempio per eseguire azioni di base tramite l&#39;API.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte dell&#39; [!DNL Adobe Experience Platform Segmentation Service] API. Prima di continuare, controllate la guida [](./getting-started.md) introduttiva per informazioni importanti che dovete conoscere per effettuare correttamente le chiamate all&#39;API, comprese le intestazioni richieste e come leggere le chiamate API di esempio.

## Recupero di un elenco di processi di segmento {#retrieve-list}

È possibile recuperare un elenco di tutti i processi del segmento per l&#39;organizzazione IMS effettuando una richiesta GET all&#39; `/segment/jobs` endpoint.

**Formato API**

L&#39; `/segment/jobs` endpoint supporta diversi parametri di query per facilitare il filtraggio dei risultati. Anche se questi parametri sono opzionali, il loro utilizzo è fortemente consigliato per ridurre i costi di sovraccarico. Effettuando una chiamata a questo endpoint senza parametri, tutti i processi di esportazione disponibili per la vostra organizzazione verranno recuperati. È possibile includere più parametri, separati da e-mail (`&`).

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**Parametri query**

| Parametro | Descrizione | Esempio |
| --------- | ----------- | ------- |
| `start` | Specifica l&#39;offset iniziale per i processi del segmento restituiti. | `start=1` |
| `limit` | Specifica il numero di processi di segmento restituiti per pagina. | `limit=20` |
| `status` | Filtra i risultati in base allo stato. I valori supportati sono NUOVO, IN CODA, ELABORAZIONE, SUCCESSO, NON RIUSCITO, ANNULLAMENTO, ANNULLATO | `status=NEW` |
| `sort` | Ordina i processi del segmento restituiti. È scritto nel formato `[attributeName]:[desc|asc]`. | `sort=creationTime:desc` |
| `property` | Filtra i processi del segmento e ottiene corrispondenze esatte per il filtro specificato. Può essere scritto in uno dei seguenti formati: <ul><li>`[jsonObjectPath]==[value]` - filtraggio sulla chiave dell&#39;oggetto</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` - filtraggio all&#39;interno dell&#39;array</li></ul> | `property=segments~segmentId==workInUS` |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un elenco di processi di segmento per l’organizzazione IMS specificata come JSON. La risposta seguente restituisce un elenco di tutti i processi del segmento riusciti per l&#39;organizzazione IMS.

>[!NOTE]
>
>La risposta seguente è stata troncata per lo spazio e mostrerà solo il primo processo restituito.

```json
{
    "_page": {
        "totalCount": 14,
        "pageSize": 14
    },
    "children": [
        {
            "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "profileInstanceId": "ups",
            "source": "scheduler",
            "status": "SUCCEEDED",
            "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
            "computeJobId": 8811,
            "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 1573203617195,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 778460
                },
                "profileSegmentationTime": {
                    "startTimeInMs": 1573204266727,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 128928
                },
                "totalProfiles": 0,
                "segmentedProfileCounter": {
                    "30230300-ccf1-48ad-8012-c5563a007069": 0,
                    "ca763983-5572-4ea4-809c-b7dff7e0d79b": 0
                },
                "segmentedProfileByNamespaceCounter": {
                    "30230300-ccf1-48ad-8012-c5563a007069": {},
                    "ca763983-5572-4ea4-809c-b7dff7e0d79b": {}
                }
            },
            "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "properties": {
                "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
                "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
            },
            "_links": {
                "cancel": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "DELETE"
                },
                "checkStatus": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "GET"
                }
            },
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | Identificatore di sola lettura generato dal sistema per il processo del segmento. |
| `status` | Lo stato corrente per il processo del segmento. I valori potenziali per lo stato includono &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;ANNULLAMENTO&quot;, &quot;ANNULLATO&quot;, &quot;FAILED&quot; e &quot;SUCCESSO&quot;. |
| `segments` | Un oggetto che contiene informazioni sulle definizioni del segmento restituite all&#39;interno del processo del segmento. |
| `segments.segment.id` | ID della definizione del segmento. |
| `segments.segment.expression` | Un oggetto che contiene informazioni sull&#39;espressione della definizione del segmento, scritta in PQL. |
| `metrics` | Un oggetto che contiene informazioni diagnostiche sul processo del segmento. |

## Creare un nuovo processo segmento {#create}

Puoi creare un nuovo processo per segmenti effettuando una richiesta POST all’ `/segment/jobs` endpoint e includendo nel corpo l’ID della definizione del segmento da cui desideri creare una nuova audience.

**Formato API**

```http
POST /segment/jobs
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
[
  {
    "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
  }
]'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `segmentId` | L’ID della definizione del segmento per cui desiderate creare un processo di segmento. Ulteriori informazioni sulle definizioni dei segmenti sono disponibili nella guida [all&#39;endpoint per la definizione dei](./segment-definitions.md)segmenti. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli del processo del segmento appena creato.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "NEW",
    "segments": [
        {
            "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "segment": {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                "mergePolicy": {
                    "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                    "version": 1
                }
            }
        }
    ],
    "requestId": "Hw1jdAHeuWHVKVxcAPFrLCbbjkriDl9v",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304260000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304260
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | Identificatore di sola lettura generato dal sistema per il processo di segmento appena creato. |
| `status` | Lo stato corrente per il processo del segmento. Poiché il processo del segmento viene creato di recente, lo stato sarà sempre &quot;NEW&quot;. |
| `segments` | Un oggetto che contiene informazioni sulle definizioni di segmento per le quali il processo di segmento è in esecuzione. |
| `segments.segment.id` | ID della definizione del segmento fornita. |
| `segments.segment.expression` | Un oggetto che contiene informazioni sull&#39;espressione della definizione del segmento, scritta in PQL. |

## Recuperare un processo segmento specifico {#get}

Potete recuperare informazioni dettagliate su un processo segmento specifico eseguendo una richiesta GET all&#39; `/segment/jobs` endpoint e fornendo l&#39;ID del processo del segmento che desiderate recuperare nel percorso della richiesta.

**Formato API**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | Il `id` valore del processo del segmento da recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sul processo del segmento specificato.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "SUCCEEDED",
    "batchId": "651fc109-3963-48d2-aa98-9e3cc2003bac",
    "computeJobId": 39312,
    "computeGatewayJobId": "a0099ab6-11ab-4c2b-a0ea-6162e16806bd",
    "segments": [
        {
            "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "segment": {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                "mergePolicy": {
                    "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1579304313411
        },
        "profileSegmentationTime": {}
    },
    "requestId": "Hw1jdAHeuWHVKVxcAPFrLCbbjkriDl9v",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304339000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304339
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | Identificatore di sola lettura generato dal sistema per il processo del segmento. |
| `status` | Lo stato corrente per il processo del segmento. I valori potenziali per lo stato includono &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;ANNULLAMENTO&quot;, &quot;ANNULLATO&quot;, &quot;FAILED&quot; e &quot;SUCCESSO&quot;. |
| `segments` | Un oggetto che contiene informazioni sulle definizioni del segmento restituite all&#39;interno del processo del segmento. |
| `segments.segment.id` | ID della definizione del segmento. |
| `segments.segment.expression` | Un oggetto che contiene informazioni sull&#39;espressione della definizione del segmento, scritta in PQL. |
| `metrics` | Un oggetto che contiene informazioni diagnostiche sul processo del segmento. |

## Recupero in blocco dei processi dei segmenti {#bulk-get}

Potete recuperare informazioni dettagliate su più processi del segmento eseguendo una richiesta POST all’ `/segment/jobs/bulk-get` endpoint e fornendo i `id` valori dei processi del segmento nel corpo della richiesta.

**Formato API**

```http
POST /segment/jobs/bulk-get
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "cc3419d3-0389-47f1-b174-fead6b3c830d"
            },
            {
                "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8"
            }
        ]
    }'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 207 con i processi di segmento richiesti.

>[!NOTE]
>
>La risposta seguente è stata troncata per lo spazio, mostrando solo dettagli parziali di ciascun processo del segmento. La risposta completa elenca tutti i dettagli per i processi del segmento richiesti.

```json
{
    "results": {
        "cc3419d3-0389-47f1-b174-fead6b3c830d": {
            "id": "cc3419d3-0389-47f1-b174-fead6b3c830d",
            "imsOrgId": "{IMS_ORG}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        },
        "c527dc3f-07fe-4b96-be4e-23f38e734ff8": {
            "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8",
            "imsOrgId": "{IMS_ORG}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                    "segment": {
                        "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | Identificatore di sola lettura generato dal sistema per il processo del segmento. |
| `status` | Lo stato corrente per il processo del segmento. I valori potenziali per lo stato includono &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;ANNULLAMENTO&quot;, &quot;ANNULLATO&quot;, &quot;FAILED&quot; e &quot;SUCCESSO&quot;. |
| `segments` | Un oggetto che contiene informazioni sulle definizioni del segmento restituite all&#39;interno del processo del segmento. |
| `segments.segment.id` | ID della definizione del segmento. |
| `segments.segment.expression` | Un oggetto che contiene informazioni sull&#39;espressione della definizione del segmento, scritta in PQL. |

## Annullamento o eliminazione di un processo di segmento specifico {#delete}

Potete eliminare un processo segmento specifico effettuando una richiesta di DELETE all’ `/segment/jobs` endpoint e fornendo l’ID del processo del segmento da eliminare nel percorso della richiesta.

>[!NOTE]
>
>La risposta API alla richiesta di eliminazione è immediata. Tuttavia, l&#39;eliminazione effettiva del processo del segmento è asincrona. In altre parole, esiste una differenza di tempo tra quando viene effettuata la richiesta di eliminazione al processo del segmento e quando viene applicata.

**Formato API**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | Il `id` valore del processo del segmento da eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 con le seguenti informazioni.

```json
{
    "status": true,
    "message": "Segment job with id 'd3b4a50d-dfea-43eb-9fca-557ea53771fd' has been marked for cancelling"
}
```

## Passaggi successivi

Dopo aver letto questa guida è ora possibile comprendere meglio come funzionano i processi di segmento.