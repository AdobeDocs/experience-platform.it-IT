---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;pianificazioni;pianificazione;api;API;
solution: Experience Platform
title: Endpoint API di pianificazione
topic-legacy: developer guide
description: Le pianificazioni sono uno strumento che può essere utilizzato per eseguire automaticamente i processi di segmentazione batch una volta al giorno.
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 3%

---

# Endpoint di pianificazione

Le pianificazioni sono uno strumento che può essere utilizzato per eseguire automaticamente i processi di segmentazione batch una volta al giorno. È possibile utilizzare l&#39;endpoint `/config/schedules` per recuperare un elenco di pianificazioni, creare una nuova pianificazione, recuperare i dettagli di una pianificazione specifica, aggiornare una pianificazione specifica o eliminare una pianificazione specifica.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte dell’ API [!DNL Adobe Experience Platform Segmentation Service] . Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all&#39;API, comprese le intestazioni richieste e come leggere le chiamate API di esempio.

## Recupera un elenco di pianificazioni {#retrieve-list}

Puoi recuperare un elenco di tutte le pianificazioni per la tua organizzazione IMS effettuando una richiesta di GET all’ endpoint `/config/schedules` .

**Formato API**

L’endpoint `/config/schedules` supporta diversi parametri di query per filtrare i risultati. Sebbene questi parametri siano opzionali, si consiglia vivamente di utilizzarli per ridurre i costi di overhead. Effettuare una chiamata a questo endpoint senza parametri recupererà tutte le pianificazioni disponibili per la tua organizzazione. È possibile includere più parametri, separati da e commerciali (`&`).

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{START}` | Specifica da quale pagina inizierà l&#39;offset. Per impostazione predefinita, questo valore è pari a 0. |
| `{LIMIT}` | Specifica il numero di pianificazioni restituite. Per impostazione predefinita, questo valore è 100. |

**Richiesta**

La seguente richiesta recupererà le ultime dieci pianificazioni pubblicate nell’organizzazione IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un elenco di pianificazioni per l’organizzazione IMS specificata come JSON.

>[!NOTE]
>
>La risposta seguente è stata troncata per lo spazio e mostra solo la prima pianificazione restituita.

```json
{
    "_page": {
        "totalCount": 10,
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

| Proprietà | Descrizione |
| -------- | ------------ |
| `_page.totalCount` | Numero totale di pianificazioni restituite. |
| `_page.pageSize` | Dimensione della pagina delle pianificazioni. |
| `children.name` | Nome della pianificazione come stringa. |
| `children.type` | Il tipo di processo come stringa. I due tipi supportati sono &quot;batch_segmentation&quot; e &quot;export&quot;. |
| `children.properties` | Un oggetto contenente proprietà aggiuntive correlate alla pianificazione. |
| `children.properties.segments` | L’utilizzo di `["*"]` assicura che tutti i segmenti siano inclusi. |
| `children.schedule` | Una stringa contenente la pianificazione del processo. L&#39;esecuzione dei processi può essere pianificata solo una volta al giorno, il che significa che non è possibile pianificare l&#39;esecuzione di un processo più di una volta durante un periodo di 24 ore. Per ulteriori informazioni sulle pianificazioni cron, leggere la documentazione [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) . In questo esempio, &quot;0 1 * * *&quot; significa che la pianificazione verrà eseguita a mezzanotte del primo di ogni mese. |
| `children.state` | Una stringa contenente lo stato della pianificazione. I due stati supportati sono &quot;attivi&quot; e &quot;inattivi&quot;. Per impostazione predefinita, lo stato è impostato su &quot;inattivo&quot;. |

## Crea una nuova pianificazione {#create}

Puoi creare una nuova pianificazione effettuando una richiesta POST all’endpoint `/config/schedules` .

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
    "name":"profile-default",
    "type":"batch_segmentation",
    "properties":{
        "segments":[
            "*"
        ]
    },
    "schedule":"0 0 1 * * ?",
    "state":"inactive"
}'
```

| Proprietà | Descrizione |
| -------- | ------------ |
| `name` | **Obbligatorio.** Nome della pianificazione come stringa. |
| `type` | **Obbligatorio.** Il tipo di processo come stringa. I due tipi supportati sono &quot;batch_segmentation&quot; e &quot;export&quot;. |
| `properties` | **Obbligatorio.** Un oggetto contenente proprietà aggiuntive correlate alla pianificazione. |
| `properties.segments` | **Obbligatorio quando  `type` è uguale a &quot;batch_segmentation&quot;.** L’utilizzo di  `["*"]` assicura che tutti i segmenti siano inclusi. |
| `schedule` | *Facoltativo.* Una stringa contenente la pianificazione del processo. L&#39;esecuzione dei processi può essere pianificata solo una volta al giorno, il che significa che non è possibile pianificare l&#39;esecuzione di un processo più di una volta durante un periodo di 24 ore. Per ulteriori informazioni sulle pianificazioni cron, leggere la documentazione [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) . In questo esempio, &quot;0 1 * * *&quot; significa che la pianificazione verrà eseguita a mezzanotte del primo di ogni mese. <br><br>Se questa stringa non viene fornita, verrà generata automaticamente una pianificazione generata dal sistema. |
| `state` | *Facoltativo.* Una stringa contenente lo stato della pianificazione. I due stati supportati sono &quot;attivi&quot; e &quot;inattivi&quot;. Per impostazione predefinita, lo stato è impostato su &quot;inattivo&quot;. |

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

## Recupera una pianificazione specifica {#get}

Puoi recuperare informazioni dettagliate su una pianificazione specifica effettuando una richiesta di GET all’ endpoint `/config/schedules` e fornendo l’ID della pianificazione da recuperare nel percorso della richiesta.

**Formato API**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Il valore `id` della pianificazione da recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
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
}
```

| Proprietà | Descrizione |
| -------- | ------------ |
| `name` | Nome della pianificazione come stringa. |
| `type` | Il tipo di processo come stringa. I due tipi supportati sono `batch_segmentation` e `export`. |
| `properties` | Un oggetto contenente proprietà aggiuntive correlate alla pianificazione. |
| `properties.segments` | L’utilizzo di `["*"]` assicura che tutti i segmenti siano inclusi. |
| `schedule` | Una stringa contenente la pianificazione del processo. L&#39;esecuzione dei processi può essere pianificata solo una volta al giorno, il che significa che non è possibile pianificare l&#39;esecuzione di un processo più di una volta durante un periodo di 24 ore. Per ulteriori informazioni sulle pianificazioni cron, leggere la documentazione [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) . In questo esempio, &quot;0 1 * * *&quot; significa che la pianificazione verrà eseguita a mezzanotte del primo di ogni mese. |
| `state` | Una stringa contenente lo stato della pianificazione. I due stati supportati sono `active` e `inactive`. Per impostazione predefinita, lo stato è impostato su `inactive`. |

## Aggiorna i dettagli di una pianificazione specifica {#update}

Puoi aggiornare una pianificazione specifica effettuando una richiesta PATCH all’ endpoint `/config/schedules` e fornendo l’ID della pianificazione che stai tentando di aggiornare nel percorso della richiesta.

La richiesta di PATCH ti consente di aggiornare [state](#update-state) o [cron pianificazione](#update-schedule) per una singola pianificazione.

### Aggiorna stato pianificazione {#update-state}

Puoi utilizzare un’operazione Patch JSON per aggiornare lo stato della pianificazione. Per aggiornare lo stato, dichiarare la proprietà `path` come `/state` e impostare `value` su `active` o `inactive`. Per ulteriori informazioni sulla patch JSON, consulta la documentazione [Patch JSON](http://jsonpatch.com/) .

**Formato API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Il valore `id` della pianificazione da aggiornare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
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
]'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `path` | Percorso del valore a cui si desidera applicare la patch. In questo caso, poiché stai aggiornando lo stato della pianificazione, devi impostare il valore di `path` su &quot;/state&quot;. |
| `value` | Valore aggiornato dello stato della pianificazione. Questo valore può essere impostato come &quot;attivo&quot; o &quot;inattivo&quot; per attivare o disattivare la pianificazione. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (nessun contenuto).

### Aggiorna pianificazione cron {#update-schedule}

Puoi utilizzare un’operazione Patch JSON per aggiornare la pianificazione cron. Per aggiornare la pianificazione, dichiarare la proprietà `path` come `/schedule` e impostare `value` su una pianificazione cron valida. Per ulteriori informazioni sulla patch JSON, consulta la documentazione [Patch JSON](http://jsonpatch.com/) . Per ulteriori informazioni sulle pianificazioni cron, leggere la documentazione [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) .

**Formato API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Il valore `id` della pianificazione da aggiornare. |

**Richiesta**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op":"add",
        "path":"/schedule",
        "value":"0 0 2 * *"
    }
]'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `path` | Percorso del valore da aggiornare. In questo caso, poiché aggiorni la pianificazione cron, è necessario impostare il valore di `path` su `/schedule`. |
| `value` | Valore aggiornato della pianificazione cron. Questo valore deve essere sotto forma di programma cron. In questo esempio, la pianificazione verrà eseguita il secondo di ogni mese. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (nessun contenuto).

## Elimina una pianificazione specifica

Puoi richiedere di eliminare una pianificazione specifica effettuando una richiesta DELETE all’ endpoint `/config/schedules` e fornendo l’ID della pianificazione da eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Il valore `id` della pianificazione da eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (nessun contenuto).

## Passaggi successivi

Dopo aver letto questa guida hai ora una migliore comprensione di come funzionano i programmi.
