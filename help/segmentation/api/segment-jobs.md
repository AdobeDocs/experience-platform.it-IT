---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;lavori di segmento;processo di segmento;API;api;
solution: Experience Platform
title: Endpoint API per i processi di segmento
description: L’endpoint per i processi di segmento nell’API del servizio di segmentazione di Adobe Experience Platform consente di gestire i processi di segmento a livello di programmazione per la tua organizzazione.
exl-id: 105481c2-1c25-4f0e-8fb0-c6577a4616b3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 3%

---

# Endpoint per processi di segmento

Un processo di segmento è un processo asincrono che crea un segmento di pubblico su richiesta. Fa riferimento a un [definizione del segmento](./segment-definitions.md), nonché [criteri di unione](../../profile/api/merge-policies.md) controllo [!DNL Real-Time Customer Profile] unisce attributi sovrapposti nei frammenti di profilo. Quando un processo di segmento viene completato con successo, puoi raccogliere varie informazioni sul segmento, ad esempio eventuali errori verificatisi durante l’elaborazione e le dimensioni finali del pubblico.

Questa guida fornisce informazioni utili per comprendere meglio i processi dei segmenti e include chiamate API di esempio per l’esecuzione di azioni di base tramite l’API.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte del [!DNL Adobe Experience Platform Segmentation Service] API. Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, comprese le intestazioni richieste e come leggere le chiamate API di esempio.

## Recupera un elenco di processi di segmento {#retrieve-list}

Puoi recuperare un elenco di tutti i processi di segmento per la tua organizzazione effettuando una richiesta di GET al `/segment/jobs` punto finale.

**Formato API**

La `/segment/jobs` l’endpoint supporta diversi parametri di query per facilitare il filtraggio dei risultati. Sebbene questi parametri siano opzionali, si consiglia vivamente di utilizzarli per ridurre i costi di overhead. Effettuare una chiamata a questo endpoint senza parametri recupererà tutti i processi di esportazione disponibili per la tua organizzazione. È possibile includere più parametri, separati da e commerciale (`&`).

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**Parametri query**

| Parametro | Descrizione | Esempio |
| --------- | ----------- | ------- |
| `start` | Specifica l&#39;offset iniziale per i processi del segmento restituiti. | `start=1` |
| `limit` | Specifica il numero di processi di segmento restituiti per pagina. | `limit=20` |
| `status` | Filtra i risultati in base allo stato. I valori supportati sono NEW, QUEUED, PROCESSING, SUCCEEDED, FAILED, CANCELING, CANCELLED | `status=NEW` |
| `sort` | Ordina i lavori del segmento restituiti. È scritto nel formato `[attributeName]:[desc|asc]`. | `sort=creationTime:desc` |
| `property` | Filtra i processi del segmento e ottiene corrispondenze esatte per il filtro specificato. Può essere scritto in uno dei seguenti formati: <ul><li>`[jsonObjectPath]==[value]` - filtro sul tasto oggetto</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` - filtro all&#39;interno dell&#39;array</li></ul> | `property=segments~segmentId==workInUS` |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un elenco di processi di segmento per l’organizzazione specificata come JSON. Tuttavia, la risposta sarà diversa, a seconda del numero di segmenti all’interno del processo del segmento.

**Minore o uguale a 1500 segmenti nel processo del segmento**

Se hai meno di 1500 segmenti in esecuzione nel tuo processo di segmento, verrà visualizzato un elenco completo di tutti i segmenti all’interno del `children.segments` attributo.

>[!NOTE]
>
>La risposta seguente è stata troncata per lo spazio e mostrerà solo il primo lavoro restituito.

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

**Più di 1500 segmenti**

Se hai più di 1500 segmenti da eseguire nel tuo lavoro di segmento, la `children.segments` verrà visualizzato l&#39;attributo `*`, che indica che tutti i segmenti vengono valutati.

>[!NOTE]
>
>La risposta seguente è stata troncata per lo spazio e mostrerà solo il primo lavoro restituito.

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
                    "segmentId": "*",
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
                "totalProfiles": 13146432,
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
| `id` | Identificatore di sola lettura generato dal sistema per il processo del segmento. |
| `status` | Lo stato corrente del processo del segmento. I valori potenziali dello stato includono &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELLED&quot;, &quot;FAILED&quot; e &quot;SUCCEEDED&quot;. |
| `segments` | Un oggetto che contiene informazioni sulle definizioni dei segmenti restituite all&#39;interno del processo di segmento. |
| `segments.segment.id` | ID della definizione del segmento. |
| `segments.segment.expression` | Un oggetto che contiene informazioni sull&#39;espressione della definizione del segmento, scritta in PQL. |
| `metrics` | Oggetto che contiene informazioni di diagnostica sul processo del segmento. |
| `metrics.totalTime` | Un oggetto che contiene informazioni sui tempi di inizio e fine del processo di segmentazione, nonché sul tempo totale impiegato. |
| `metrics.profileSegmentationTime` | Un oggetto che contiene informazioni sui tempi di avvio e fine della valutazione della segmentazione, nonché sul tempo totale impiegato. |
| `metrics.segmentProfileCounter` | Il numero di profili qualificati in base a segmento. |
| `metrics.segmentedProfileByNamespaceCounter` | Il numero di profili qualificati per ogni namespace di identità in base a segmento. |
| `metrics.segmentProfileByStatusCounter` | Il conteggio dei profili per ogni stato. Sono supportati i tre stati seguenti: <ul><li>&quot;Realizzato&quot; - Il numero di profili idonei per il segmento.</li><li>&quot;uscito&quot; - Il numero di segmenti di profilo che non esistono più nel segmento.</li></ul> |
| `metrics.totalProfilesByMergePolicy` | Numero totale di profili uniti in base ai criteri di unione. |

## Crea un nuovo processo di segmento {#create}

Puoi creare un nuovo processo di segmento effettuando una richiesta di POST al `/segment/jobs` e include nel corpo l&#39;ID della definizione del segmento da cui desideri creare un nuovo pubblico.

**Formato API**

```http
POST /segment/jobs
```

Quando crei un nuovo processo di segmento, la richiesta e la risposta variano a seconda del numero di segmenti all’interno del processo di segmento.

**Minore o uguale a 1500 segmenti nel processo del segmento**

**Richiesta**

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
    }
 ]'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `segmentId` | ID della definizione del segmento per cui si desidera creare un processo del segmento. Queste definizioni di segmenti possono appartenere a diversi criteri di unione. Ulteriori informazioni sulle definizioni dei segmenti sono disponibili nella sezione [guida all’endpoint definizione dei segmenti](./segment-definitions.md). |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con le informazioni sul processo del segmento appena creato.

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
| `id` | Identificatore di sola lettura generato dal sistema per il processo del segmento appena creato. |
| `status` | Lo stato corrente del processo del segmento. Poiché il processo del segmento è stato appena creato, lo stato sarà sempre &quot;NEW&quot;. |
| `segments` | Oggetto che contiene informazioni sulle definizioni dei segmenti per cui è in esecuzione il processo di segmento. |
| `segments.segment.id` | ID della definizione del segmento fornita. |
| `segments.segment.expression` | Un oggetto che contiene informazioni sull&#39;espressione della definizione del segmento, scritta in PQL. |

**Più di 1500 segmenti**

**Richiesta**

>[!NOTE]
>
>Anche se puoi creare un lavoro di segmento con più di 1500 segmenti, è **altamente non consigliato**.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "segments": [
        {
            "segmentId": "*"
        }
    ]
 }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `schema.name` | Nome dello schema per i segmenti. |
| `segments.segmentId` | Quando esegui un processo di segmento con più di 1500 segmenti, dovrai passare `*` come ID del segmento per indicare che desideri eseguire un processo di segmentazione con tutti i segmenti. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli del processo del segmento appena creato.

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
            "segmentId": "*"
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
| `id` | Identificatore di sola lettura generato dal sistema per il processo del segmento appena creato. |
| `status` | Lo stato corrente del processo del segmento. Poiché il processo del segmento è stato appena creato, lo stato sarà sempre `NEW`. |
| `segments` | Oggetto che contiene informazioni sulle definizioni dei segmenti per cui è in esecuzione il processo di segmento. |
| `segments.segment.id` | La `*` significa che questo processo del segmento è in esecuzione per tutti i segmenti all’interno della tua organizzazione. |

## Recupera un processo di segmento specifico {#get}

Puoi recuperare informazioni dettagliate su un processo di segmento specifico effettuando una richiesta di GET al `/segment/jobs` e fornisce l’ID del processo del segmento che desideri recuperare nel percorso della richiesta.

**Formato API**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | La `id` valore del processo del segmento che si desidera recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sul processo del segmento specificato.  Tuttavia, la risposta varia a seconda del numero di segmenti all’interno del processo del segmento.

**Minore o uguale a 1500 segmenti nel processo del segmento**

Se hai meno di 1500 segmenti in esecuzione nel tuo processo di segmento, verrà visualizzato un elenco completo di tutti i segmenti all’interno del `children.segments` attributo.

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

**Più di 1500 segmenti**

Se hai più di 1500 segmenti da eseguire nel tuo lavoro di segmento, la `children.segments` verrà visualizzato l&#39;attributo `*`, che indica che tutti i segmenti vengono valutati.

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
    "status": "SUCCEEDED",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "*"
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
| `id` | Identificatore di sola lettura generato dal sistema per il processo del segmento. |
| `status` | Lo stato corrente del processo del segmento. I valori potenziali dello stato includono &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELLED&quot;, &quot;FAILED&quot; e &quot;SUCCEEDED&quot;. |
| `segments` | Un oggetto che contiene informazioni sulle definizioni dei segmenti restituite all&#39;interno del processo di segmento. |
| `segments.segment.id` | ID della definizione del segmento. |
| `segments.segment.expression` | Un oggetto che contiene informazioni sull&#39;espressione della definizione del segmento, scritta in PQL. |
| `metrics` | Oggetto che contiene informazioni di diagnostica sul processo del segmento. |

## Processi di recupero in blocco dei segmenti {#bulk-get}

Puoi recuperare informazioni dettagliate su più processi di segmento effettuando una richiesta di POST al `/segment/jobs/bulk-get` e fornisce  `id` i valori dei processi del segmento nel corpo della richiesta.

**Formato API**

```http
POST /segment/jobs/bulk-get
```

**Richiesta**

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

**Risposta**

Una risposta corretta restituisce lo stato HTTP 207 con i processi di segmento richiesti. Tuttavia, il valore del `children.segments` l’attributo varia a seconda che il processo del segmento sia in esecuzione per più di 1500 segmenti.

>[!NOTE]
>
>La risposta seguente è stata troncata per lo spazio, mostrando solo dettagli parziali di ciascun processo di segmento. La risposta completa elencherà tutti i dettagli per i processi del segmento richiesti.

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
                    "segmentId": "*"
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
| `status` | Lo stato corrente del processo del segmento. I valori potenziali dello stato includono &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELLED&quot;, &quot;FAILED&quot; e &quot;SUCCEEDED&quot;. |
| `segments` | Un oggetto che contiene informazioni sulle definizioni dei segmenti restituite all&#39;interno del processo di segmento. |
| `segments.segment.id` | ID della definizione del segmento. |
| `segments.segment.expression` | Un oggetto che contiene informazioni sull&#39;espressione della definizione del segmento, scritta in PQL. |

## Annullare o eliminare un processo di segmento specifico {#delete}

Puoi eliminare un processo di segmento specifico effettuando una richiesta di DELETE al `/segment/jobs` e fornisce l’ID del processo del segmento da eliminare nel percorso della richiesta.

>[!NOTE]
>
>La risposta API alla richiesta di cancellazione è immediata. Tuttavia, l’eliminazione effettiva del processo del segmento è asincrona. In altre parole, esiste una differenza di tempo tra quando viene effettuata la richiesta di eliminazione al processo del segmento e quando viene applicata.

**Formato API**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | La `id` valore del processo del segmento da eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Dopo aver letto questa guida hai ora una migliore comprensione di come funzionano i lavori dei segmenti.
