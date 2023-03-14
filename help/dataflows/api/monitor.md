---
keywords: Experience Platform;home;argomenti popolari;monitorare flussi di dati;servizio di flusso api;Flow Service
solution: Experience Platform
title: Monitorare i flussi di dati utilizzando l’API del servizio Flusso
type: Tutorial
description: Questo tutorial illustra i passaggi necessari per monitorare i dati di esecuzione del flusso per verificarne la completezza, gli errori e le metriche tramite l’API del servizio Flusso.
exl-id: c4b2db97-eba4-460d-8c00-c76c666ed70e
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 1%

---

# Monitorare i flussi di dati tramite l’API del servizio Flusso

Adobe Experience Platform consente di acquisire dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre. Inoltre, Experience Platform consente di attivare i dati per i partner esterni.

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da diverse origini all’interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui tutte le origini e le destinazioni supportate sono collegabili.

Questa esercitazione descrive i passaggi per monitorare i dati di esecuzione del flusso per completezza, errori e metriche utilizzando [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa esercitazione richiede di avere il valore ID di un flusso di dati valido. Se non disponi di un ID di flusso di dati valido, seleziona il connettore desiderato dall’elenco [panoramica sulle origini](../../sources/home.md) o [panoramica sulle destinazioni](../../destinations/catalog/overview.md) e segui i passaggi descritti prima di provare questa esercitazione.

Questo tutorial richiede anche una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Destinazioni](../../destinations/home.md): le destinazioni sono integrazioni predefinite con applicazioni di uso comune che consentono l’attivazione diretta dei dati da Platform per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.
- [Sorgenti](../../sources/home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per monitorare correttamente le esecuzioni del flusso utilizzando [!DNL Flow Service] API.

### Lettura delle chiamate API di esempio

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nel [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori per le intestazioni richieste

Per effettuare chiamate a [!DNL Platform] , devi prima completare le [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], compresi quelli appartenenti a [!DNL Flow Service], sono isolate in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

- `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

- `Content-Type: application/json`

## Monitorare le esecuzioni del flusso

Dopo aver creato un flusso di dati, esegui una richiesta di GET a [!DNL Flow Service] API.

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
            "id": "65b7cfcc-6b2e-47c8-8194-13005b792752",
            "createdAt": 1607520228894,
            "updatedAt": 1607520276948,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "prod",
            "imsOrgId": "{ORG_ID}",
            "flowId": "f00c8762-df2f-432b-a7d7-38999fef5e8e",
            "etag": "\"560266dc-0000-0200-0000-5fd0d0140000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1607520205922,
                    "completedAtUTC": 1607520262413
                },
                "sizeSummary": {
                    "inputBytes": 87885,
                    "outputBytes": 56730
                },
                "recordSummary": {
                    "inputRecordCount": 26758,
                    "outputRecordCount": 26758,
                    "failedRecordCount": 0
                },
                "fileSummary": {
                    "inputFileCount": 11,
                    "outputFileCount": 11,
                    "activityRefs": [
                        "37b34f84-1ada-11eb-adc1-0242ac120002"
                    ]
                },
                "statusSummary": {
                    "status": "success"
                }
            },
            "activities": [
                {
                    "id": "4f008a00-3a04-11eb-adc1-0242ac120002",
                    "name": "Copy Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520205922,
                        "completedAtUTC": 1607520236968
                    },
                    "sizeSummary": {
                        "inputBytes": 87885,
                        "outputBytes": 87885
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 11
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                },
                {
                    "id": "37b34f84-1ada-11eb-adc1-0242ac120002",
                    "name": "Promotion Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520244985,
                        "completedAtUTC": 1607520262413
                    },
                    "sizeSummary": {
                        "inputBytes": 26758,
                        "outputBytes": 56730
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758,
                        "failedRecordCount": 0
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 2,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01ES3TRN69E9W2DZ770XCGYAH1/meta?path=input_files",
                                "pathPrefix": "bucket1/csv_test/"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                }
            ]
        }
    ]
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `items` | Contiene un singolo payload di metadati associati all’esecuzione del flusso specifica. |
| `metrics` | Le caratteristiche dei dati nell’esecuzione del flusso. |
| `activities` | Mostra come vengono trasformati i dati. |
| `durationSummary` | Ora di inizio e di fine dell’esecuzione del flusso. |
| `sizeSummary` | Volume dei dati in byte. |
| `recordSummary` | Numero di record dei dati. |
| `fileSummary` | I conteggi dei file dei dati. |
| `fileSummary.extensions` | Contiene informazioni specifiche dell’attività. Ad esempio: `manifest` fa solo parte dell’&quot;Attività di promozione&quot; e pertanto è inclusa con `extensions` oggetto. |
| `statusSummary` | Mostra se l’esecuzione del flusso è riuscita o meno. |

## Passaggi successivi

Seguendo questa esercitazione, hai recuperato metriche e informazioni di errore sul flusso di dati utilizzando [!DNL Flow Service] API. Ora puoi continuare a monitorare il flusso di dati, a seconda della pianificazione di acquisizione, per monitorarne lo stato e i tassi di acquisizione. Per informazioni su come monitorare i flussi di dati per le origini, consulta la sezione [monitoraggio dei flussi di dati per le origini tramite l’interfaccia utente](../ui/monitor-sources.md) esercitazione. Per ulteriori informazioni su come monitorare i flussi di dati per le destinazioni, consulta la sezione [monitoraggio dei flussi di dati per le destinazioni tramite l’interfaccia utente](../ui/monitor-destinations.md) esercitazione.
