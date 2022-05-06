---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;aggiornare i flussi di dati
solution: Experience Platform
title: Aggiornare i flussi di dati utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Questa esercitazione descrive i passaggi per l’aggiornamento di un flusso di dati, inclusi nome, descrizione e pianificazione, tramite l’API del servizio di flusso.
exl-id: 367a3a9e-0980-4144-a669-e4cfa7a9c722
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 3%

---

# Aggiornare i flussi di dati utilizzando l’API del servizio di flusso

Questa esercitazione descrive i passaggi per aggiornare un flusso di dati, incluse le informazioni di base, la pianificazione e i set di mappature che utilizzano [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa esercitazione richiede un ID di flusso valido. Se non disponi di un ID di flusso valido, seleziona il connettore di scelta dal [panoramica di origini](../../home.md) e segui i passaggi descritti prima di provare questa esercitazione.

Questa esercitazione richiede anche di avere una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../landing/api-guide.md).

## Ricerca dei dettagli del flusso di dati

Il primo passo per aggiornare il flusso di dati è quello di recuperare i dettagli del flusso di dati utilizzando il tuo ID di flusso. Puoi visualizzare i dettagli correnti di un flusso di dati esistente effettuando una richiesta di GET al `/flows` punto finale.

**Formato API**

```http
GET /flows/{FLOW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FLOW_ID}` | L&#39;unico `id` per il flusso di dati da recuperare. |

**Richiesta**

La seguente richiesta recupera le informazioni aggiornate relative all&#39;ID di flusso.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli correnti del flusso di dati, inclusa la relativa versione, pianificazione e identificatore univoco (`id`).

```json
{
    "items": [
        {
            "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
            "createdAt": 1612310475905,
            "updatedAt": 1614122324830,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Database dataflow using BigQuery",
            "description": "collecting test1.Mytable from Google BigQuery",
            "flowSpec": {
                "id": "14518937-270c-4525-bdec-c2ba7cce3860",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"5400d99c-0000-0200-0000-60358d540000\"",
            "etag": "\"5400d99c-0000-0200-0000-60358d540000\"",
            "sourceConnectionIds": [
                "b7581b59-c603-4df1-a689-d23d7ac440f3"
            ],
            "targetConnectionIds": [
                "320f119a-5ac1-4ab1-88ea-eb19e674ea2e"
            ],
            "inheritedAttributes": {
                "sourceConnections": [
                    {
                        "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
                        "connectionSpec": {
                            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
                            "connectionSpec": {
                                "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "320f119a-5ac1-4ab1-88ea-eb19e674ea2e",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "scheduleParams": {
                "startTime": "1612310466",
                "frequency": "week",
                "interval": "15",
                "backfill": "true"
            },
            "transformations": [
                {
                    "name": "Copy",
                    "params": {
                        "deltaColumn": {
                            "name": "Datefield",
                            "dateFormat": "YYYY-MM-DD",
                            "timezone": "UTC"
                        }
                    }
                },
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "0b090130b58b4819afc78b6dc98b484d",
                        "mappingVersion": "0"
                    }
                }
            ],
            "runs": "/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c/runs",
            "lastOperation": {
                "started": 1614122316652,
                "updated": 1614122324830,
                "percentCompleted": 100.0,
                "status": {
                    "value": "completed",
                    "errors": []
                },
                "ops": [
                    {
                        "op": "replace",
                        "path": "/scheduleParams/frequency",
                        "value": "week"
                    }
                ],
                "operation": "update"
            },
            "lastRunDetails": {
                "id": "a10cc80b-fbea-4c6b-873e-d7fd32f4d12d",
                "state": "success",
                "startedAtUTC": 1613079975512,
                "completedAtUTC": 1613080027511
            }
        }
    ]
}
```

## Aggiornamento del flusso di dati

Per aggiornare la pianificazione, il nome e la descrizione dell’esecuzione del flusso di dati, esegui una richiesta PATCH al [!DNL Flow Service] API fornendo al tempo stesso il tuo ID flusso, la versione e la nuova pianificazione che desideri utilizzare.

>[!IMPORTANT]
>
>La `If-Match` l’intestazione è necessaria quando si effettua una richiesta PATCH. Il valore di questa intestazione è la versione univoca della connessione che si desidera aggiornare. Il valore etag viene aggiornato con ogni aggiornamento corretto di un flusso di dati.

**Formato API**

```http
PATCH /flows/{FLOW_ID}
```

**Richiesta**

La richiesta seguente aggiorna la pianificazione di esecuzione del flusso, nonché il nome e la descrizione del flusso di dati.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/scheduleParams/frequency",
                "value": "day"
            },
            {
                "op": "replace",
                "path": "/name",
                "value": "Database Dataflow Feb2021"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "Database dataflow for testing update API"
            }
        ]'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `op` | La chiamata dell’operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace`e `remove`. |
| `path` | Definisce la parte del flusso da aggiornare. |
| `value` | Il nuovo valore con cui si desidera aggiornare il parametro. |

**Risposta**

Una risposta corretta restituisce il tuo ID flusso e un tag aggiornato. Puoi verificare l’aggiornamento effettuando una richiesta GET al [!DNL Flow Service] , fornendo al tempo stesso il tuo ID flusso.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Aggiornamento della mappatura

È possibile aggiornare il set di mappatura di un flusso di dati esistente effettuando una richiesta di PATCH al [!DNL Flow Service] API e fornitura di valori aggiornati per la `mappingId` e `mappingVersion`.

**Formato API**

```http
PATCH /flows/{FLOW_ID}
```

**Richiesta**

La richiesta seguente aggiorna il set di mappatura del flusso di dati.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "50014cc8-0000-0200-0000-6036eb720000"' \
    -d '[
        {
            "op": "replace",
            "path": "/transformations/0",
            "value": {
                "name": "Mapping",
                "params": {
                    "mappingId": "c5f22f04e09f44498e528901546a83b1",
                    "mappingVersion": 2
                }
            }
        }
    ]'
```

| Proprietà | Descrizione |
| --- | --- |
| `op` | La chiamata dell’operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace`e `remove`. |
| `path` | Definisce la parte del flusso da aggiornare. In questo esempio, `transformations` è in corso l&#39;aggiornamento. |
| `value.name` | Nome della proprietà da aggiornare. |
| `value.params.mappingId` | Il nuovo ID di mappatura da utilizzare per aggiornare il set di mappatura del flusso di dati. |
| `value.params.mappingVersion` | La nuova versione di mappatura associata all&#39;ID di mappatura aggiornato. |

**Risposta**

Una risposta corretta restituisce il tuo ID flusso e un tag aggiornato. Puoi verificare l’aggiornamento effettuando una richiesta GET al [!DNL Flow Service] , fornendo al tempo stesso il tuo ID flusso.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"2c000802-0000-0200-0000-613976440000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai aggiornato le informazioni di base, la pianificazione e i set di mappatura del flusso di dati utilizzando [!DNL Flow Service] API. Per ulteriori informazioni sull’utilizzo dei connettori sorgente, consulta la sezione [panoramica di origini](../../home.md).
