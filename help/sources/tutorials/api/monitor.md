---
keywords: Experience Platform;home;argomenti popolari;monitorare flussi di dati;servizio di flusso api;Flow Service
solution: Experience Platform
title: Monitorare i flussi di dati delle origini utilizzando l’API del servizio Flusso
type: Tutorial
description: Questo tutorial illustra i passaggi necessari per monitorare i dati di esecuzione del flusso per verificarne la completezza, gli errori e le metriche tramite l’API del servizio Flusso.
exl-id: 5b7d1aa4-5e6d-48f4-82bd-5348dc0e890d
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 2%

---

# Monitorare i flussi di dati delle origini utilizzando l’API del servizio Flusso

Questa esercitazione descrive i passaggi per monitorare i dati di esecuzione del flusso per completezza, errori e metriche utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Questa esercitazione richiede di avere il valore ID di un flusso di dati valido. Se non disponi di un ID di flusso di dati valido, seleziona il connettore desiderato dall’elenco [panoramica sulle origini](../../home.md) e segui i passaggi descritti per creare un flusso di dati prima di provare questa esercitazione.

## Introduzione

Questo tutorial richiede anche una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../landing/api-guide.md).

## Monitorare i flussi di dati

Per visualizzare lo stato del flusso di dati, effettua una richiesta GET al [!DNL Flow Service] , fornendo al tempo stesso l’ID di flusso corrispondente del flusso di dati.

**Formato API**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FLOW_ID}` | L&#39;unico `id` valore per il flusso di dati che desideri monitorare. |

**Richiesta**

La richiesta seguente recupera le specifiche di un flusso di dati esistente.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce dettagli relativi all’esecuzione del flusso, incluse informazioni sulla data di creazione, sulle connessioni di origine e di destinazione e sull’identificatore univoco dell’esecuzione del flusso (`id`).

```json
{
    "items": [
        {
            "createdAt": 1596656079576,
            "updatedAt": 1596656113526,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
            "sandboxName": "prod",
            "id": "9830305a-985f-47d0-b030-5a985fd7d004",
            "flowId": "c9cef9cb-c934-4467-8ef9-cbc934546741",
            "etag": "\"b8003af1-0000-0200-0000-5f2b09f10000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1596656058198,
                    "completedAtUTC": 1596656113306
                },
                "sizeSummary": {
                    "inputBytes": 24012,
                    "outputBytes": 17128
                },
                "recordSummary": {
                    "inputRecordCount": 100,
                    "outputRecordCount": 99,
                    "failedRecordCount": 1
                },
                "fileSummary": {
                    "inputFileCount": 1,
                    "outputFileCount": 1,
                    "activityRefs": [
                        "promotionActivity"
                    ]
                },
                "statusSummary": {
                    "status": "success",
                    "errors": [
                        {
                            "code": "CONNECTOR-2001-500",
                            "message": "Error occurred at promotion activity."
                        }
                    ],
                    "activityRefs": [
                        "promotionActivity"
                    ]
                }
            },
            "activities": [
                {
                    "id": "copyActivity",
                    "updatedAtUTC": 1596656095088,
                    "durationSummary": {
                        "startedAtUTC": 1596656058198,
                        "completedAtUTC": 1596656089650,
                        "extensions": {
                            "windowStart": 1596653708000,
                            "windowEnd": 1596655508000
                        }
                    },
                    "sizeSummary": {
                        "inputBytes": 24012,
                        "outputBytes": 24012
                    },
                    "recordSummary": {},
                    "fileSummary": {
                        "inputFileCount": 1,
                        "outputFileCount": 1
                    },
                    "statusSummary": {
                        "status": "success",
                        "extensions": {
                            "type": "one-time"
                        }
                    },
                    "sourceInfo": [
                        {
                            "id": "c0e18602-f9ea-44f9-a186-02f9ea64f9ac",
                            "type": "SourceConnection",
                            "reference": {
                                "type": "AdfRunId",
                                "ids": [
                                    "8a8eb0cc-e283-4605-ac70-65a5adb1baef"
                                ]
                            }
                        }
                    ]
                },
                {
                    "id": "promotionActivity",
                    "updatedAtUTC": 1596656113485,
                    "durationSummary": {
                        "startedAtUTC": 1596656095333,
                        "completedAtUTC": 1596656113306
                    },
                    "sizeSummary": {
                        "inputBytes": 24012,
                        "outputBytes": 17128
                    },
                    "recordSummary": {
                        "inputRecordCount": 100,
                        "outputRecordCount": 99,
                        "failedRecordCount": 1
                    },
                    "fileSummary": {
                        "inputFileCount": 2,
                        "outputFileCount": 1,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=input_files"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success",
                        "errors": [
                            {
                                "code": "CONNECTOR-2001-500",
                                "message": "Error occurred at promotion activity."
                            }
                        ],
                        "extensions": {
                            "manifest": {
                                "failedRecords": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=row_errors",
                                "sampleErrors": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=row_error_samples.json"
                            },
                            "errors": [
                                {
                                    "code": "INGEST-1212-400",
                                    "message": "Encountered 1 errors in the data. Successfully ingested 99 rows. Review the associated diagnostic files for additional details."
                                },
                                {
                                    "code": "MAPPER-3700-400",
                                    "recordCount": 1,
                                    "message": "Mapper Transform Error"
                                }
                            ]
                        }
                    },
                    "targetInfo": [
                        {
                            "id": "47166b83-01c7-4b65-966b-8301c70b6562",
                            "type": "TargetConnection",
                            "reference": {
                                "type": "Batch",
                                "ids": [
                                    "01EF01X41KJD82Y9ZX6ET54PCZ"
                                ]
                            }
                        }
                    ]
                }
            ]
        }
    ],
    "_links": {}
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `items` | Contiene un singolo payload di metadati associati all’esecuzione del flusso specifica. |
| `metrics` | Definisce le caratteristiche dei dati nell’esecuzione del flusso. |
| `activities` | Definisce la modalità di trasformazione dei dati. |
| `durationSummary` | Definisce l’ora di inizio e di fine dell’esecuzione del flusso. |
| `sizeSummary` | Definisce il volume dei dati in byte. |
| `recordSummary` | Definisce il conteggio dei record dei dati. |
| `fileSummary` | Definisce il conteggio dei file dei dati. |
| `statusSummary` | Definisce se l’esecuzione del flusso è riuscita o meno. |

## Passaggi successivi

Seguendo questa esercitazione, hai recuperato metriche e informazioni di errore sul flusso di dati utilizzando [!DNL Flow Service] API. Ora puoi continuare a monitorare il flusso di dati, a seconda della pianificazione di acquisizione, per monitorarne lo stato e i tassi di acquisizione. Per informazioni su come eseguire le stesse attività utilizzando l’interfaccia utente, consulta l’esercitazione su [monitoraggio dei flussi di dati tramite l’interfaccia utente](../ui/monitor.md)
