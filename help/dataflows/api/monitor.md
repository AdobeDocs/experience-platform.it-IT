---
keywords: Experience Platform;home;argomenti popolari;monitorare i flussi di dati;api del servizio di flusso;servizio di flusso
solution: Experience Platform
title: Monitorare i flussi di dati tramite l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Questa esercitazione descrive i passaggi per il monitoraggio dei dati di esecuzione del flusso per la completezza, gli errori e le metriche utilizzando l’API del servizio di flusso.
exl-id: c4b2db97-eba4-460d-8c00-c76c666ed70e
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 1%

---

# Monitorare i flussi di dati tramite l’API del servizio di flusso

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri. Inoltre, l’Experience Platform consente l’attivazione dei dati ai partner esterni.

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti all&#39;interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui è possibile collegare tutte le origini e le destinazioni supportate.

Questa esercitazione descrive i passaggi per il monitoraggio dei dati di esecuzione del flusso per la completezza, gli errori e le metriche utilizzando [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa esercitazione richiede di avere il valore ID di un flusso di dati valido. Se non disponi di un ID flusso di dati valido, seleziona il connettore di scelta dal [panoramica di origini](../../sources/home.md) o [panoramica sulle destinazioni](../../destinations/catalog/overview.md) e segui i passaggi descritti prima di provare questa esercitazione.

Questa esercitazione richiede anche di avere una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Destinazioni](../../destinations/home.md): Le destinazioni sono integrazioni predefinite con applicazioni comunemente utilizzate che consentono l’attivazione senza soluzione di continuità dei dati da Platform per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.
- [Origini](../../sources/home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per monitorare correttamente le esecuzioni di flusso utilizzando il [!DNL Flow Service] API.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], compresi quelli appartenenti [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

- `Content-Type: application/json`

## Correnze di flusso del monitor

Una volta effettuato un flusso di dati, esegui una richiesta di GET al [!DNL Flow Service] API.

**Formato API**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FLOW_ID}` | L&#39;unico `id` per il flusso di dati da monitorare. |

**Richiesta**

La richiesta seguente recupera le specifiche per un flusso di dati esistente.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli relativi all’esecuzione del flusso, incluse informazioni sulla data di creazione, sulle connessioni di origine e di destinazione, nonché l’identificatore univoco dell’esecuzione del flusso (`id`).

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
| `items` | Contiene un singolo payload di metadati associati all’esecuzione di flusso specifica. |
| `metrics` | Le caratteristiche dei dati nell&#39;esecuzione del flusso. |
| `activities` | Mostra come vengono trasformati i dati. |
| `durationSummary` | Ora di inizio e di fine dell&#39;esecuzione del flusso. |
| `sizeSummary` | Il volume dei dati in byte. |
| `recordSummary` | Il conteggio record dei dati. |
| `fileSummary` | Il file conta i dati. |
| `fileSummary.extensions` | Contiene informazioni specifiche per l’attività. Ad esempio: `manifest` fa solo parte dell’&quot;Attività di promozione&quot;, e quindi è inclusa nella `extensions` oggetto. |
| `statusSummary` | Mostra se l’esecuzione del flusso è riuscita o meno. |

## Passaggi successivi

Seguendo questa esercitazione, hai recuperato le metriche e le informazioni sugli errori nel flusso di dati utilizzando [!DNL Flow Service] API. Ora puoi continuare a monitorare il flusso di dati, a seconda della pianificazione dell’acquisizione, per monitorarne lo stato e le percentuali di acquisizione. Per informazioni su come monitorare i flussi di dati per le sorgenti, leggere il [monitoraggio dei flussi di dati per le sorgenti che utilizzano l’interfaccia utente](../ui/monitor-sources.md) esercitazione. Per ulteriori informazioni su come monitorare i flussi di dati per le destinazioni, consulta il [monitoraggio dei flussi di dati per le destinazioni tramite l’interfaccia utente](../ui/monitor-destinations.md) esercitazione.
