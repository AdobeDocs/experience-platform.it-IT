---
keywords: ' Experience Platform;home;argomenti popolari;monitorare i flussi di dati;servizio flusso api;servizio flusso'
solution: Experience Platform
title: Flussi di monitoraggio e esecuzioni
topic: overview
type: Tutorial
description: Questa esercitazione descrive i passaggi per monitorare i dati di esecuzione del flusso per la completezza, gli errori e le metriche utilizzando l'API del servizio di flusso.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 1%

---


# Monitorare i flussi di dati mediante l&#39;API di Flusso Service

Adobe Experience Platform consente l&#39;acquisizione di dati da origini esterne, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando i servizi [!DNL Platform]. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, database e molti altri. Inoltre,  Experience Platform consente l&#39;attivazione dei dati ai partner esterni.

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie origini all&#39;interno di Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegabili tutte le origini e le destinazioni supportate.

Questa esercitazione descrive i passaggi necessari per monitorare i dati di esecuzione del flusso al fine di verificare la completezza, gli errori e le metriche utilizzando [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introduzione

Per questa esercitazione è necessario avere il valore ID di un flusso di dati valido. Se non si dispone di un ID di flusso di dati valido, selezionare il connettore desiderato dalla [panoramica delle origini](../../sources/home.md) o [panoramica delle destinazioni](../../destinations/catalog/overview.md) e seguire i passaggi descritti prima di eseguire l&#39;esercitazione.

Questa esercitazione richiede inoltre di conoscere i seguenti componenti di Adobe Experience Platform:

- [Destinazioni](../../destinations/home.md): Le destinazioni sono integrazioni predefinite con applicazioni comunemente utilizzate che consentono l&#39;attivazione senza soluzione di continuità dei dati dalla piattaforma per campagne di marketing multicanale, campagne e-mail, pubblicità mirata e molti altri casi di utilizzo.
- [Origini](../../sources/home.md):  [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
- [Sandbox](../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per monitorare correttamente le esecuzioni di flusso utilizzando l&#39;API [!DNL Flow Service].

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a2/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come illustrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

- `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

- `Content-Type: application/json`

## Correnti di flusso del monitor

Dopo aver eseguito un flusso di dati, esegui una richiesta di GET all&#39;API [!DNL Flow Service].

**Formato API**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FLOW_ID}` | Valore `id` univoco per il flusso di dati da monitorare. |

**Richiesta**

La richiesta seguente recupera le specifiche per un flusso di dati esistente.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli relativi all&#39;esecuzione del flusso, incluse informazioni sulla data di creazione, sulle connessioni di origine e di destinazione, nonché l&#39;identificatore univoco dell&#39;esecuzione del flusso (`id`).

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
            "imsOrgId": "{IMS_ORG_ID}",
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
| `metrics` | Caratteristiche dei dati nell&#39;esecuzione del flusso. |
| `activities` | Mostra la trasformazione dei dati. |
| `durationSummary` | Ora di inizio e di fine dell&#39;esecuzione del flusso. |
| `sizeSummary` | Il volume dei dati in byte. |
| `recordSummary` | Il conteggio record dei dati. |
| `fileSummary` | Conteggio dei dati nel file. |
| `fileSummary.extensions` | Contiene informazioni specifiche per l&#39;attività. Ad esempio, `manifest` è solo una parte dell&#39;&quot;Attività di promozione&quot; e pertanto è inclusa con l&#39;oggetto `extensions`. |
| `statusSummary` | Indica se l&#39;esecuzione del flusso è riuscita o meno. |

## Passaggi successivi

Seguendo questa esercitazione, hai recuperato le metriche e le informazioni sugli errori nel flusso di dati utilizzando l&#39;API [!DNL Flow Service]. Ora puoi continuare a monitorare il flusso di dati, a seconda della pianificazione dell&#39;assimilazione, per monitorarne lo stato e le percentuali di assimilazione. Per informazioni su come monitorare i flussi di dati per le origini, leggere i [flussi di dati di monitoraggio per le origini utilizzando l&#39;interfaccia utente](../ui/monitor-sources.md) tutorial. Per ulteriori informazioni su come monitorare i flussi di dati per le destinazioni, leggere i [flussi di dati di monitoraggio per le destinazioni utilizzando l&#39;interfaccia utente](../ui/monitor-destinations.md) tutorial.