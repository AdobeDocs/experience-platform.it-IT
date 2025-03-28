---
solution: Experience Platform
title: Endpoint API per processi di segmento
description: L’endpoint per i processi di segmento nell’API del servizio di segmentazione di Adobe Experience Platform consente di gestire in modo programmatico i processi di segmento per la tua organizzazione.
role: Developer
exl-id: 105481c2-1c25-4f0e-8fb0-c6577a4616b3
source-git-commit: 9eb5ccc24db58a887473f61c66a83aa92e16efa7
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 3%

---

# Endpoint &quot;segment jobs&quot;

Un processo di segmentazione è un processo asincrono che crea un segmento di pubblico su richiesta. Fa riferimento a una [definizione segmento](./segment-definitions.md), nonché a qualsiasi [criterio di unione](../../profile/api/merge-policies.md) che controlla come [!DNL Real-Time Customer Profile] unisce attributi sovrapposti nei frammenti di profilo. Al termine di un processo di segmentazione, puoi raccogliere varie informazioni sul segmento, ad esempio eventuali errori che si sono verificati durante l’elaborazione e le dimensioni finali del pubblico.

Questa guida fornisce informazioni utili per comprendere meglio i processi dei segmenti e include chiamate API di esempio per eseguire azioni di base utilizzando l’API.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte dell&#39;API [!DNL Adobe Experience Platform Segmentation Service]. Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, incluse le intestazioni richieste e la lettura delle chiamate API di esempio.

## Recuperare un elenco di processi di segmentazione {#retrieve-list}

Per recuperare un elenco di tutti i processi dei segmenti per l&#39;organizzazione, eseguire una richiesta GET all&#39;endpoint `/segment/jobs`.

**Formato API**

L&#39;endpoint `/segment/jobs` supporta diversi parametri di query per filtrare i risultati. Anche se questi parametri sono facoltativi, si consiglia vivamente di utilizzarli per ridurre i costi generali. Effettuando una chiamata a questo endpoint senza parametri, verranno recuperati tutti i processi di esportazione disponibili per la tua organizzazione. È possibile includere più parametri, separati da e commerciali (`&`).

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**Parametri query**

+++ Elenco dei parametri di query disponibili.

| Parametro | Descrizione | Esempio |
| --------- | ----------- | ------- |
| `start` | Specifica l&#39;offset iniziale per i processi di segmento restituiti. | `start=1` |
| `limit` | Specifica il numero di processi di segmento restituiti per pagina. | `limit=20` |
| `status` | Filtra i risultati in base allo stato. I valori supportati sono NEW, QUEUED, PROCESSING, SUCCESSEDED, FAILED, CANCELING, CANCELED | `status=NEW` |
| `sort` | Ordina i processi segmento restituiti. È scritto nel formato `[attributeName]:[desc|asc]`. | `sort=creationTime:desc` |
| `property` | Filtra i processi di segmentazione e ottiene corrispondenze esatte per il filtro specificato. Può essere scritto in uno dei seguenti formati: <ul><li>`[jsonObjectPath]==[value]` - filtro sulla chiave oggetto</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` - filtro all&#39;interno dell&#39;array</li></ul> | `property=segments~segmentId==workInUS` |

+++

**Richiesta**

+++ Una richiesta di esempio per visualizzare un elenco di processi di segmentazione.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco di processi di segmento per l’organizzazione specificata come JSON. Nell&#39;attributo `children.segments` verrà visualizzato un elenco completo di tutte le definizioni di segmento.

>[!NOTE]
>
>La seguente risposta è stata troncata per motivi di spazio e mostrerà solo il primo processo restituito.

+++ Una risposta di esempio durante il recupero di un elenco di processi di segmento.

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
                        "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                        "mergePolicy": {
                            "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
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
                "totalProfiles":13146432,
                "segmentedProfileCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":1033
                },
                "segmentedProfileByNamespaceCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "tenantiduserobjid":1033,
                        "campaign_profile_mscom_mkt_prod2":1033
                    }
                },
                "segmentedProfileByStatusCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "exited":144646,
                        "realized":2056
                    }
                },
                "totalProfilesByMergePolicy":{
                    "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
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
| `id` | Identificatore di sola lettura generato dal sistema per il processo di segmentazione. |
| `status` | Lo stato corrente del processo di segmentazione. I valori potenziali per lo stato includono &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELED&quot;, &quot;FAILED&quot; e &quot;SUCCESSEDED&quot;. |
| `segments` | Oggetto contenente informazioni sulle definizioni dei segmenti restituite all’interno del processo di segmentazione. |
| `segments.segment.id` | ID della definizione del segmento. |
| `segments.segment.expression` | Oggetto contenente informazioni sull’espressione della definizione del segmento, scritta in PQL. |
| `metrics` | Oggetto contenente informazioni diagnostiche sul processo di segmentazione. |
| `metrics.totalTime` | Oggetto che contiene informazioni sulle ore di inizio e fine del processo di segmentazione, nonché sul tempo totale impiegato. |
| `metrics.profileSegmentationTime` | Oggetto che contiene informazioni sulle ore di inizio e fine della valutazione della segmentazione, nonché sul tempo totale impiegato. |
| `metrics.segmentProfileCounter` | Il numero di profili qualificati per segmento. |
| `metrics.segmentedProfileByNamespaceCounter` | Il numero di profili qualificati per ogni spazio dei nomi delle identità in base alla definizione dei singoli segmenti. |
| `metrics.segmentProfileByStatusCounter` | Il conteggio dei profili per ogni stato. Sono supportati i tre stati seguenti: <ul><li>&quot;realized&quot; (realizzato): numero di profili idonei per la definizione del segmento.</li><li>&quot;exited&quot;: il numero di profili che non esistono più nella definizione del segmento.</li></ul> |
| `metrics.totalProfilesByMergePolicy` | Numero totale di profili uniti per criterio di unione. |

+++

## Crea un nuovo processo di segmentazione {#create}

Per creare un nuovo processo di segmento, devi eseguire una richiesta POST all&#39;endpoint `/segment/jobs` e includere gli ID della definizione del segmento nel corpo della richiesta.

**Formato API**

```http
POST /segment/jobs
```

**Richiesta**

+++Richiesta di esempio per la creazione di un nuovo processo di segmentazione

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '[
    {
        "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e"
    },
    {
        "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85"
    }
 ]'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `segmentId` | ID della definizione del segmento che desideri valutare. Queste definizioni dei segmenti possono appartenere a diversi criteri di unione. Ulteriori informazioni sulle definizioni dei segmenti sono disponibili nella [guida dell&#39;endpoint di definizione dei segmenti](./segment-definitions.md). |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni sul processo di segmentazione appena creato.

+++ Una risposta di esempio durante la creazione di un nuovo processo di segmentazione.

```json
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
    "status": "PROCESSING",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e",
            "segment": {
                "id": "7863c010-e092-41c8-ae5e-9e533186752e",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85",
            "segment": {
                "id": "07d39471-05d1-4083-a310-d96978fd7c85",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
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
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
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
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | Identificatore di sola lettura generato dal sistema per il processo di segmentazione appena creato. |
| `status` | Lo stato corrente del processo di segmentazione. Poiché il processo di segmentazione è stato appena creato, lo stato sarà sempre &quot;NUOVO&quot;. |
| `segments` | Oggetto contenente informazioni sulle definizioni dei segmenti per cui è in esecuzione questo processo di segmentazione. |
| `segments.segment.id` | ID della definizione di segmento fornita. |
| `segments.segment.expression` | Oggetto contenente informazioni sull’espressione della definizione del segmento, scritta in PQL. |

+++

## Recuperare un processo di segmento specifico {#get}

Per recuperare informazioni dettagliate su un processo di segmentazione specifico, effettua una richiesta GET all&#39;endpoint `/segment/jobs` e fornisci l&#39;ID del processo di segmentazione da recuperare nel percorso della richiesta.

**Formato API**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | Il valore `id` del processo di segmentazione che si desidera recuperare. |

**Richiesta**

+++ Richiesta di esempio per recuperare un processo di segmentazione.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni dettagliate sul processo di segmentazione specificato. Nell&#39;attributo `children.segments` verrà visualizzato un elenco completo di tutte le definizioni di segmento.

+++ Risposta di esempio per recuperare un processo di segmentazione.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{ORG_ID}",
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
| `id` | Identificatore di sola lettura generato dal sistema per il processo di segmentazione. |
| `status` | Lo stato corrente del processo di segmentazione. I valori potenziali per lo stato includono &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELED&quot;, &quot;FAILED&quot; e &quot;SUCCESSEDED&quot;. |
| `segments` | Oggetto contenente informazioni sulle definizioni dei segmenti restituite all’interno del processo di segmentazione. |
| `segments.segment.id` | ID della definizione del segmento. |
| `segments.segment.expression` | Oggetto contenente informazioni sull’espressione della definizione del segmento, scritta in PQL. |
| `metrics` | Oggetto contenente informazioni diagnostiche sul processo di segmentazione. |

+++

>[!ENDTABS]

## Processi di recupero in blocco dei segmenti {#bulk-get}

Per recuperare informazioni dettagliate su più processi di segmentazione, effettua una richiesta POST all&#39;endpoint `/segment/jobs/bulk-get` e fornisci i valori `id` dei processi di segmentazione nel corpo della richiesta.

**Formato API**

```http
POST /segment/jobs/bulk-get
```

**Richiesta**

+++ Richiesta di esempio per l’utilizzo dell’endpoint di recupero in blocco.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 207 con i processi di segmento richiesti.

>[!NOTE]
>
>La seguente risposta è stata troncata per motivi di spazio, mostrando solo dettagli parziali di ciascun processo di segmentazione. Nella risposta completa verranno elencati tutti i dettagli dei processi di segmentazione richiesti.

+++ Una risposta di esempio quando si utilizza la risposta bulk-get.

```json
{
    "results": {
        "cc3419d3-0389-47f1-b174-fead6b3c830d": {
            "id": "cc3419d3-0389-47f1-b174-fead6b3c830d",
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "30230300-d78c-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-d78c-48ad-8012-c5563a007069",
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
| `id` | Identificatore di sola lettura generato dal sistema per il processo di segmentazione. |
| `status` | Lo stato corrente del processo di segmentazione. I valori potenziali per lo stato includono &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELED&quot;, &quot;FAILED&quot; e &quot;SUCCESSEDED&quot;. |
| `segments` | Oggetto contenente informazioni sulle definizioni dei segmenti restituite all’interno del processo di segmentazione. |
| `segments.segment.id` | ID della definizione del segmento. |
| `segments.segment.expression` | Oggetto contenente informazioni sull’espressione della definizione del segmento, scritta in PQL. |

+++

## Annullare o eliminare un processo di segmento specifico {#delete}

È possibile eliminare un processo di segmento specifico effettuando una richiesta DELETE all&#39;endpoint `/segment/jobs` e fornendo l&#39;ID del processo di segmento che si desidera eliminare nel percorso della richiesta.

>[!NOTE]
>
>La risposta API alla richiesta di eliminazione è immediata. Tuttavia, l’effettiva eliminazione del processo di segmentazione è asincrona. In altre parole, esiste una differenza di tempo tra il momento in cui viene effettuata la richiesta di eliminazione del processo di segmentazione e quello in cui viene applicata.

**Formato API**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | Valore `id` del processo di segmentazione da eliminare. |

**Richiesta**

+++ Richiesta di esempio per eliminare un processo di segmentazione.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 con un corpo di risposta vuoto.

## Passaggi successivi

Dopo aver letto questa guida hai acquisito una migliore comprensione del funzionamento dei processi di segmentazione.
