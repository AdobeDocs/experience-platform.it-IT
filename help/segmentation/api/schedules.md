---
solution: Experience Platform
title: Endpoint API Schedules
description: Le pianificazioni sono uno strumento che può essere utilizzato per eseguire automaticamente processi di segmentazione batch una volta al giorno.
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '1996'
ht-degree: 4%

---

# Endpoint Schedules

Le pianificazioni sono uno strumento che può essere utilizzato per eseguire automaticamente processi di segmentazione batch una volta al giorno. È possibile utilizzare `/config/schedules` endpoint per recuperare un elenco di pianificazioni, creare una nuova pianificazione, recuperare i dettagli di una pianificazione specifica, aggiornare una pianificazione specifica o eliminarla.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte del [!DNL Adobe Experience Platform Segmentation Service] API. Prima di continuare, controlla [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all’API, incluse le intestazioni richieste e la lettura di esempi di chiamate API.

## Recuperare un elenco di pianificazioni {#retrieve-list}

È possibile recuperare un elenco di tutte le pianificazioni per l&#39;organizzazione effettuando una richiesta di GET al `/config/schedules` endpoint.

**Formato API**

Il `/config/schedules` l’endpoint supporta diversi parametri di query per aiutare a filtrare i risultati. Anche se questi parametri sono facoltativi, si consiglia vivamente di utilizzarli per ridurre i costi generali. Effettuando una chiamata a questo endpoint senza parametri, verranno recuperate tutte le pianificazioni disponibili per la tua organizzazione. È possibile includere più parametri, separati da e commerciali (`&`).

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{START}` | Specifica da quale pagina inizierà l&#39;offset. Per impostazione predefinita, questo valore è 0. |
| `{LIMIT}` | Specifica il numero di pianificazioni restituite. Per impostazione predefinita, questo valore è 100. |

**Richiesta**

La seguente richiesta recupererà le ultime dieci pianificazioni registrate nella tua organizzazione.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco di pianificazioni per l’organizzazione specificata come JSON.

>[!NOTE]
>
>La seguente risposta è stata troncata per motivi di spazio e mostra solo la prima pianificazione restituita.

```json
{
    "_page": {
        "totalCount": 10,
        "pageSize": 1
    },
    "children": [
        {
            "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
            "imsOrgId": "{ORG_ID}",
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
| `children.name` | Nome della pianificazione sotto forma di stringa. |
| `children.type` | Tipo di processo come stringa. I due tipi supportati sono &quot;batch_segmentation&quot; ed &quot;export&quot;. |
| `children.properties` | Oggetto contenente proprietà aggiuntive correlate alla pianificazione. |
| `children.properties.segments` | Utilizzo di `["*"]` assicura che tutti i segmenti siano inclusi. |
| `children.schedule` | Stringa contenente la pianificazione del processo. È possibile programmare l&#39;esecuzione dei job solo una volta al giorno, pertanto non è possibile programmare l&#39;esecuzione di un job più di una volta in un periodo di 24 ore. Per ulteriori informazioni sulle pianificazioni cron, leggere l&#39;appendice del [formato espressione cron](#appendix). In questo esempio, &quot;0 0 1 * *&quot; significa che la pianificazione verrà eseguita ogni giorno all’1. |
| `children.state` | Stringa contenente lo stato della pianificazione. I due stati supportati sono &quot;active&quot; e &quot;inactive&quot;. Per impostazione predefinita, lo stato è impostato su &quot;inattivo&quot;. |

## Crea una nuova pianificazione {#create}

Per creare una nuova pianificazione, devi effettuare una richiesta POST al `/config/schedules` endpoint.

**Formato API**

```http
POST /config/schedules
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | **Obbligatorio.** Nome della pianificazione sotto forma di stringa. |
| `type` | **Obbligatorio.** Tipo di processo come stringa. I due tipi supportati sono &quot;batch_segmentation&quot; ed &quot;export&quot;. |
| `properties` | **Obbligatorio.** Oggetto contenente proprietà aggiuntive correlate alla pianificazione. |
| `properties.segments` | **Obbligatorio quando `type` è uguale a &quot;batch_segmentation&quot;.** Utilizzo di `["*"]` assicura che tutti i segmenti siano inclusi. |
| `schedule` | *Facoltativo.* Stringa contenente la pianificazione del processo. È possibile programmare l&#39;esecuzione dei job solo una volta al giorno, pertanto non è possibile programmare l&#39;esecuzione di un job più di una volta in un periodo di 24 ore. Per ulteriori informazioni sulle pianificazioni cron, leggere l&#39;appendice del [formato espressione cron](#appendix). In questo esempio, &quot;0 0 1 * *&quot; significa che la pianificazione verrà eseguita ogni giorno all’1. <br><br>Se questa stringa non viene fornita, verrà generata automaticamente una pianificazione generata dal sistema. |
| `state` | *Facoltativo.* Stringa contenente lo stato della pianificazione. I due stati supportati sono &quot;active&quot; e &quot;inactive&quot;. Per impostazione predefinita, lo stato è impostato su &quot;inattivo&quot;. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della pianificazione appena creata.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
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

## Recuperare una pianificazione specifica {#get}

Per recuperare informazioni dettagliate su una pianificazione specifica, effettua una richiesta GET al `/config/schedules` e fornendo l’ID della pianificazione da recuperare nel percorso della richiesta.

**Formato API**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Il `id` valore della pianificazione da recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni dettagliate sulla pianificazione specificata.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
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
| `name` | Nome della pianificazione sotto forma di stringa. |
| `type` | Tipo di processo come stringa. I due tipi supportati sono `batch_segmentation` e `export`. |
| `properties` | Oggetto contenente proprietà aggiuntive correlate alla pianificazione. |
| `properties.segments` | Utilizzo di `["*"]` assicura che tutti i segmenti siano inclusi. |
| `schedule` | Stringa contenente la pianificazione del processo. È possibile programmare l&#39;esecuzione dei job solo una volta al giorno, pertanto non è possibile programmare l&#39;esecuzione di un job più di una volta in un periodo di 24 ore. Per ulteriori informazioni sulle pianificazioni cron, leggere l&#39;appendice del [formato espressione cron](#appendix). In questo esempio, &quot;0 0 1 * *&quot; significa che la pianificazione verrà eseguita ogni giorno all’1. |
| `state` | Stringa contenente lo stato della pianificazione. I due stati supportati sono `active` e `inactive`. Per impostazione predefinita, lo stato è impostato su `inactive`. |

## Aggiorna i dettagli per una pianificazione specifica {#update}

Per aggiornare una pianificazione specifica, effettua una richiesta PATCH al `/config/schedules` e fornendo l’ID della pianificazione che stai tentando di aggiornare nel percorso della richiesta.

La richiesta PATCH ti consente di aggiornare [stato](#update-state) o [pianificazione cron](#update-schedule) per un singolo programma.

### Aggiorna stato pianificazione {#update-state}

È possibile utilizzare un’operazione Patch JSON per aggiornare lo stato della pianificazione. Per aggiornare lo stato, dichiarare `path` proprietà come `/state` e imposta `value` a `active` o `inactive`. Per ulteriori informazioni sulla patch JSON, leggere [Patch JSON](https://datatracker.ietf.org/doc/html/rfc6902) documentazione.

**Formato API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Il `id` valore della pianificazione da aggiornare. |

**Richiesta**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `path` | Percorso del valore a cui applicare la patch. In questo caso, poiché stai aggiornando lo stato della pianificazione, devi impostare il valore di `path` a &quot;/state&quot;. |
| `value` | Il valore aggiornato dello stato della pianificazione. Questo valore può essere impostato come &quot;attivo&quot; o &quot;inattivo&quot; per attivare o disattivare la pianificazione. Nota che **non può** disabilita una pianificazione se l’organizzazione è stata abilitata per lo streaming. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto).

### Aggiorna pianificazione cron {#update-schedule}

È possibile utilizzare un’operazione Patch JSON per aggiornare la pianificazione cron. Per aggiornare la pianificazione, dichiarare `path` proprietà come `/schedule` e imposta `value` a una pianificazione cron valida. Per ulteriori informazioni sulla patch JSON, leggere [Patch JSON](https://datatracker.ietf.org/doc/html/rfc6902) documentazione. Per ulteriori informazioni sulle pianificazioni cron, leggere l&#39;appendice del [formato espressione cron](#appendix).

**Formato API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Il `id` valore della pianificazione da aggiornare. |

**Richiesta**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op":"add",
        "path":"/schedule",
        "value":"0 0 2 * * ?"
    }
]'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `path` | Percorso del valore da aggiornare. In questo caso, poiché stai aggiornando la pianificazione cron, devi impostare il valore di `path` a `/schedule`. |
| `value` | Il valore aggiornato della pianificazione cron. Questo valore deve essere sotto forma di una pianificazione cron. In questo esempio, la pianificazione verrà eseguita il secondo di ogni mese. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto).

## Eliminare una pianificazione specifica

Per richiedere l’eliminazione di una pianificazione specifica, effettua una richiesta DELETE al `/config/schedules` e fornendo l’ID della pianificazione da eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Il `id` valore della pianificazione da eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto).

## Passaggi successivi

Dopo aver letto questa guida, ora hai una migliore comprensione di come funzionano le pianificazioni.

## Appendice {#appendix}

Nell&#39;appendice seguente viene illustrato il formato delle espressioni cron utilizzate nelle pianificazioni.

### Formato

Un&#39;espressione cron è una stringa composta da 6 o 7 campi. L’espressione sarà simile alla seguente:

`0 0 12 * * ?`

In una stringa di espressione cron, il primo campo rappresenta i secondi, il secondo campo rappresenta i minuti, il terzo campo rappresenta le ore, il quarto campo rappresenta il giorno del mese, il quinto campo rappresenta il mese e il sesto campo rappresenta il giorno della settimana. Facoltativamente, è anche possibile includere un settimo campo, che rappresenta l’anno.

| Nome campo | Obbligatorio | Valori possibili | Caratteri speciali consentiti |
| ---------- | -------- | --------------- | -------------------------- |
| Seconds | Sì | 0-59 | `, - * /` |
| Minutes | Sì | 0-59 | `, - * /` |
| Ore | Sì | 0-23 | `, - * /` |
| Giorno del mese | Sì | 1-31 | `, - * ? / L W` |
| Mese | Sì | 1-12 GEN-DIC | `, - * /` |
| Giorno della settimana | Sì | 1-7, SUN-SAT | `, - * ? / L #` |
| Anno | No | Vuoto, 1970-2099 | `, - * /` |

>[!NOTE]
>
>I nomi dei mesi e dei giorni della settimana sono **non** distinzione tra maiuscole e minuscole. Pertanto, `SUN` equivale a utilizzare `sun`.

I caratteri speciali consentiti rappresentano i seguenti significati:

| Carattere speciale | Descrizione |
| ----------------- | ----------- |
| `*` | Questo valore viene utilizzato per selezionare **tutto** valori in un campo. Ad esempio, inserendo `*` nel campo ore indica **ogni** ora. |
| `?` | Questo valore significa che non è richiesto alcun valore specifico. Questo generalmente viene utilizzato per specificare qualcosa in un campo in cui il carattere è consentito, ma non specificarlo nell’altro. Ad esempio, se desideri che un evento venga attivato ogni 3 del mese, ma non ti importa di quale giorno della settimana si tratti, inserisci `3` nel campo del giorno del mese e `?` nel campo giorno della settimana. |
| `-` | Questo valore viene utilizzato per specificare **inclusivo** intervalli per il campo. Ad esempio, se inserisci `9-15` nel campo ore, questo significherebbe che le ore includerebbero 9, 10, 11, 12, 13, 14 e 15. |
| `,` | Questo valore viene utilizzato per specificare valori aggiuntivi. Ad esempio, se inserisci `MON, FRI, SAT` nel campo giorno della settimana, i giorni della settimana includeranno lunedì, venerdì e sabato. |
| `/` | Questo valore viene utilizzato per specificare gli incrementi. Il valore inserito prima del `/` determina da dove viene incrementato, mentre il valore posizionato dopo il `/` determina di quanto viene incrementato. Ad esempio, se inserisci `1/7` nel campo minuti ciò significa che i minuti includono 1, 8, 15, 22, 29, 36, 43, 50 e 57. |
| `L` | Questo valore viene utilizzato per specificare `Last`, e ha un significato diverso a seconda del campo da cui viene utilizzato. Se viene utilizzato con il campo del giorno del mese, rappresenta l’ultimo giorno del mese. Se viene utilizzato con il campo del giorno della settimana, rappresenta l&#39;ultimo giorno della settimana, ovvero il sabato (`SAT`). Se viene utilizzato insieme al campo giorno della settimana e a un altro valore, rappresenta l&#39;ultimo giorno di quel tipo per il mese. Ad esempio, se inserisci `5L` nel campo del giorno della settimana, **solo** includi l’ultimo venerdì del mese. |
| `W` | Questo valore viene utilizzato per specificare il giorno feriale più vicino al giorno specificato. Ad esempio, se inserisci `18W` nel campo del giorno del mese, e il 18 di quel mese era un sabato, si attivava venerdì 17, che è il giorno feriale più vicino. Se il 18 di quel mese fosse una domenica, sarebbe attivato lunedì 19, che è il giorno feriale più vicino. Si prega di notare che se mette `1W` nel campo del giorno del mese, e il giorno feriale più vicino è nel mese precedente, l’evento si attiva ancora nel giorno feriale più vicino del mese **corrente** mese.</br></br>Inoltre, è possibile combinare `L` e `W` per effettuare `LW`, che specifica l’ultimo giorno feriale del mese. |
| `#` | Questo valore viene utilizzato per specificare l’ennesimo giorno della settimana in un mese. Il valore inserito prima del `#` rappresenta il giorno della settimana, mentre il valore inserito dopo il `#` rappresenta l’occorrenza nel mese in cui si trova. Ad esempio, se inserisci `1#3`, l’evento si attiva la terza domenica del mese. Si prega di notare che se mette `X#5` e non si verifica il quinto giorno della settimana in quel mese, l&#39;evento **non** essere attivata. Ad esempio, se inserisci `1#5`, e non c&#39;è una quinta domenica in quel mese, l&#39;evento **non** essere attivata. |

### Esempi

La tabella seguente mostra alcune stringhe di espressioni cron di esempio e ne spiega il significato.

| Espressione | Spiegazione |
| ---------- | ----------- |
| `0 0 13 * * ?` | L&#39;evento si attiva ogni giorno alle 13. |
| `0 30 9 * * ? 2022` | L’evento si attiva ogni giorno alle 9:30 del 2022. |
| `0 * 18 * * ?` | L’evento si attiva ogni minuto, dalle 18:00 alle 18:59, tutti i giorni. |
| `0 0/10 17 * * ?` | L’evento si attiva ogni 10 minuti, dalle 17:00 alle 18:00, in qualsiasi giornata. |
| `0 13,38 5 ? 6 WED` | L&#39;evento si attiverà alle 5:13 del mattino e alle 5:38 di ogni mercoledì di giugno. |
| `0 30 12 ? * 4#3` | L&#39;evento si attiva alle 12:30 del terzo mercoledì di ogni mese. |
| `0 30 12 ? * 6L` | L&#39;evento verrà attivato alle 12:30 dell&#39;ultimo venerdì di ogni mese. |
| `0 45 11 ? * MON-THU` | L’evento si attiva alle 11:45 di ogni lunedì, martedì, mercoledì e giovedì. |