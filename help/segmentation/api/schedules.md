---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Pianificazioni
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# Pianifica la guida per gli sviluppatori

introduzione

- Recupero di un elenco di pianificazioni
- Creare una nuova pianificazione
- Recuperare una pianificazione specifica
- Aggiornare una pianificazione specifica
- Eliminare una pianificazione specifica

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte dell&#39;API di segmentazione. Prima di continuare, consulta la guida [per lo sviluppatore di](./getting-started.md)segmentazione.

In particolare, la sezione [](./getting-started.md#getting-started) introduttiva della guida per gli sviluppatori di segmentazione include collegamenti a argomenti correlati, una guida alla lettura delle chiamate API di esempio nel documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente chiamate a qualsiasi API della piattaforma Experience.

## Recupero di un elenco di pianificazioni

Puoi recuperare un elenco di tutte le pianificazioni per la tua organizzazione IMS effettuando una richiesta GET all&#39; `/config/schedules` endpoint.

**Formato API**

```http
GET /config/schedules
GET /config/schedules?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Facoltativo*) Parametri aggiunti al percorso di richiesta che configurano i risultati restituiti nella risposta. È possibile includere più parametri, separati da e-mail (`&`). I parametri disponibili sono elencati di seguito.

**Parametri query**

Di seguito è riportato un elenco di parametri di query disponibili per le pianificazioni di elenco. Tutti questi parametri sono facoltativi. Effettuando una chiamata a questo endpoint senza parametri, tutte le pianificazioni disponibili per l&#39;organizzazione verranno recuperate.

| Parametro | Descrizione |
| --------- | ----------- |
| `start` | Specifica da quale pagina inizia l&#39;offset. Per impostazione predefinita, questo valore è 0. |
| `limit` | Specifica il numero di pianificazioni restituite. Per impostazione predefinita, questo valore è 100. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=X \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un elenco di pianificazioni per l’organizzazione IMS specificata come JSON.

```json
{
    "_page": {
        "totalCount": 1,
        "pageSize": 1
    },
    "children": [
        {
            "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "Batch Segmentation",
            "state": "active",
            "type": "batch_segmentation",
            "schedule": "0 0 1 * * ?",
            "properties": {
                "segments": []
            },
            "createEpoch": 1573158851,
            "updateEpoch": 1574365202
        }
    ],
    "_links": {
        "next": {}
    }
}
```

## Creare una nuova pianificazione

Potete creare una nuova pianificazione effettuando una richiesta POST all’ `/config/schedules` endpoint.

**Formato API**

```http
POST /config/schedules
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "name": "profile-default",
  "type": "batch_segmentation",
  "properties": {
    "segments": [
      "*"
    ]
  },
  "schedule": "0 0 1 * * ?",
  "state": "inactive"
}
 '
```

| Parametro | Descrizione |
| --------- | ------------ |
| `name` | **Obbligatorio.** Nome della pianificazione come stringa. |
| `type` | **Obbligatorio.** Il tipo di processo come stringa. I due tipi supportati sono `batch_segmentation` e `export`. |
| `properties` | **Obbligatorio.** Un oggetto contenente proprietà aggiuntive correlate alla pianificazione. |
| `properties.segments` | **Obbligatorio se`type`è uguale a`batch_segmentation`.** L&#39;utilizzo `["*"]` assicura che tutti i segmenti siano inclusi. |
| `schedule` | **Obbligatorio.** Una stringa contenente la pianificazione del processo. Per ulteriori informazioni sulle pianificazioni cron, consulta la documentazione sul formato [delle espressioni](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron. In questo esempio, &quot;0 0 1 * * *&quot; significa che questa pianificazione si terrà a mezzanotte il primo di ogni mese. |
| `state` | *Facoltativo.* Una stringa contenente lo stato di pianificazione. I due stati supportati sono `active` e `inactive`. Per impostazione predefinita, lo stato è impostato su `inactive`. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della nuova pianificazione creata.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

## Recuperare una pianificazione specifica

Potete recuperare informazioni dettagliate su una pianificazione specifica eseguendo una richiesta GET all&#39; `/config/schedules` endpoint e fornendo il valore della pianificazione `id` nel percorso della richiesta.

**Formato API**

```http
GET /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: Il `id` valore della pianificazione da recuperare.

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID}
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sulla pianificazione specificata.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
```

## Aggiornamento dei dettagli di una pianificazione specifica

È possibile aggiornare una pianificazione specificata eseguendo una richiesta PATCH all&#39; `/config/schedules` endpoint e fornendo il valore della pianificazione `id` nel percorso della richiesta.

La richiesta PATCH supporta due percorsi diversi: `/state` e `/schedule`.

### Aggiorna stato pianificazione

È possibile utilizzare `/state` per aggiornare lo stato della pianificazione: ATTIVO o INATTIVO. Per aggiornare lo stato, è necessario impostare il valore come `active` o `inactive`.

**Formato API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: Il `id` valore della pianificazione da aggiornare.

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
  {
    "op": "add",
    "path": "/state",
    "value": "active"
  }
]
'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `path` | Percorso del valore da applicare alla patch. In questo caso, poiché si aggiorna lo stato della pianificazione, è necessario impostare il valore di `path` a `/state`. |
| `value` | Il valore aggiornato dell&#39; `/state`. Questo valore può essere impostato come `active` o `inactive` per attivare o disattivare la pianificazione. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (nessun contenuto).

### Aggiorna pianificazione cron

È possibile utilizzare `schedule` per aggiornare la pianificazione cron. Per ulteriori informazioni sulle pianificazioni cron, consulta la documentazione sul formato [delle espressioni](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron.

**Formato API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: Il `id` valore della pianificazione da aggiornare.

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
  {
    "op": "add",
    "path": "/schedule",
    "value": "0 0 2 * *"
  }
]
'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `path` | Percorso del valore da applicare alla patch. In questo caso, poiché si sta aggiornando la pianificazione cron della pianificazione, è necessario impostare il valore di `path` a `/schedule`. |
| `value` | Il valore aggiornato dell&#39; `/state`. Questo valore deve essere sotto forma di programmazione cron. In questo esempio, la pianificazione verrà eseguita il secondo di ogni mese. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (nessun contenuto).

## Eliminare una pianificazione specifica

È possibile richiedere di eliminare una pianificazione specificata eseguendo una richiesta DELETE al programma `/config/schedules` e fornendo il valore della pianificazione `id` nel percorso della richiesta.

**Formato API**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: Il `id` valore della pianificazione da eliminare.

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (nessun contenuto) con il seguente messaggio:

```json
(No Content) Schedule deleted successfully
```

## Passaggi successivi
