---
solution: Experience Platform
title: Endpoint API Schedules
description: Le pianificazioni sono uno strumento che può essere utilizzato per eseguire automaticamente processi di segmentazione batch una volta al giorno.
role: Developer
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: bf90e478b38463ec8219276efe71fcc1aab6b2aa
workflow-type: tm+mt
source-wordcount: '2104'
ht-degree: 3%

---

# Endpoint Schedules

Le pianificazioni sono uno strumento che può essere utilizzato per eseguire automaticamente processi di segmentazione batch una volta al giorno. È possibile utilizzare l&#39;endpoint `/config/schedules` per recuperare un elenco di pianificazioni, creare una nuova pianificazione, recuperare i dettagli di una pianificazione specifica, aggiornare una pianificazione specifica o eliminare una pianificazione specifica.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte dell&#39;API [!DNL Adobe Experience Platform Segmentation Service]. Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, incluse le intestazioni richieste e la lettura delle chiamate API di esempio.

## Recuperare un elenco di pianificazioni {#retrieve-list}

Per recuperare un elenco di tutte le pianificazioni per l&#39;organizzazione, eseguire una richiesta GET all&#39;endpoint `/config/schedules`.

**Formato API**

L&#39;endpoint `/config/schedules` supporta diversi parametri di query per filtrare i risultati. Anche se questi parametri sono facoltativi, si consiglia vivamente di utilizzarli per ridurre i costi generali. Effettuando una chiamata a questo endpoint senza parametri, verranno recuperate tutte le pianificazioni disponibili per la tua organizzazione. È possibile includere più parametri, separati da e commerciali (`&`).

```http
GET /config/schedules
GET /config/schedules?{QUERY_PARAMETERS}
```

**Parametri query**

+++ Elenco dei parametri di query disponibili.

| Parametro | Descrizione | Esempio |
| --------- | ----------- | ------- |
| `start` | Specifica da quale pagina inizierà l&#39;offset. Per impostazione predefinita, questo valore è 0. | `start=5` |
| `limit` | Specifica il numero di pianificazioni restituite. Per impostazione predefinita, questo valore è 100. | `limit=20` |

+++

**Richiesta**

La seguente richiesta recupererà le ultime dieci pianificazioni registrate nella tua organizzazione.

+++ Richiesta di esempio per recuperare un elenco di pianificazioni.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco di pianificazioni per l’organizzazione specificata come JSON.

>[!NOTE]
>
>La seguente risposta è stata troncata per motivi di spazio e mostra solo la prima pianificazione restituita.

+++ Una risposta di esempio durante il recupero di un elenco di pianificazioni.

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
| `children.properties.segments` | L&#39;utilizzo di `["*"]` garantisce l&#39;inclusione di tutti i segmenti. |
| `children.schedule` | Stringa contenente la pianificazione del processo. È possibile programmare l&#39;esecuzione dei job solo una volta al giorno, pertanto non è possibile programmare l&#39;esecuzione di un job più di una volta in un periodo di 24 ore. Per ulteriori informazioni sulle pianificazioni cron, leggere l&#39;appendice nel formato di espressione cron [](#appendix). In questo esempio, &quot;0 0 1 * *&quot; significa che la pianificazione verrà eseguita ogni giorno all’1. |
| `children.state` | Stringa contenente lo stato della pianificazione. I due stati supportati sono &quot;active&quot; e &quot;inactive&quot;. Per impostazione predefinita, lo stato è impostato su &quot;inattivo&quot;. |

+++

## Crea una nuova pianificazione {#create}

È possibile creare una nuova pianificazione effettuando una richiesta POST all&#39;endpoint `/config/schedules`.

**Formato API**

```http
POST /config/schedules
```

**Richiesta**

+++ Richiesta di esempio per creare una pianificazione.

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
| `name` | **Obbligatorio.** Il nome della pianificazione sotto forma di stringa. |
| `type` | **Obbligatorio.** Il tipo di processo come stringa. I due tipi supportati sono &quot;batch_segmentation&quot; ed &quot;export&quot;. |
| `properties` | **Obbligatorio.** Oggetto contenente proprietà aggiuntive relative alla pianificazione. |
| `properties.segments` | **Obbligatorio quando `type` è uguale a &quot;batch_segmentation&quot;.** L&#39;utilizzo di `["*"]` garantisce l&#39;inclusione di tutti i segmenti. |
| `schedule` | *Facoltativo.* Stringa contenente la pianificazione del processo. È possibile programmare l&#39;esecuzione dei job solo una volta al giorno, pertanto non è possibile programmare l&#39;esecuzione di un job più di una volta in un periodo di 24 ore. Per ulteriori informazioni sulle pianificazioni cron, leggere l&#39;appendice nel formato di espressione cron [](#appendix). In questo esempio, &quot;0 0 1 * *&quot; significa che la pianificazione verrà eseguita ogni giorno all’1. <br><br>Se questa stringa non viene fornita, verrà generata automaticamente una pianificazione generata dal sistema. |
| `state` | *Facoltativo.* Stringa contenente lo stato della pianificazione. I due stati supportati sono &quot;active&quot; e &quot;inactive&quot;. Per impostazione predefinita, lo stato è impostato su &quot;inattivo&quot;. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della pianificazione appena creata.

+++ Una risposta di esempio durante la creazione di una pianificazione.

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

+++

## Recuperare una pianificazione specifica {#get}

Per recuperare informazioni dettagliate su una pianificazione specifica, eseguire una richiesta di GET all&#39;endpoint `/config/schedules` e fornire l&#39;ID della pianificazione da recuperare nel percorso della richiesta.

**Formato API**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Il valore `id` della pianificazione da recuperare. |

**Richiesta**

+++ Richiesta di esempio per recuperare una pianificazione.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni dettagliate sulla pianificazione specificata.

+++ Una risposta di esempio durante il recupero di una pianificazione.

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
| `properties.segments` | L&#39;utilizzo di `["*"]` garantisce l&#39;inclusione di tutti i segmenti. |
| `schedule` | Stringa contenente la pianificazione del processo. È possibile programmare l&#39;esecuzione dei job solo una volta al giorno, pertanto non è possibile programmare l&#39;esecuzione di un job più di una volta in un periodo di 24 ore. Per ulteriori informazioni sulle pianificazioni cron, leggere l&#39;appendice nel formato di espressione cron [](#appendix). In questo esempio, &quot;0 0 1 * *&quot; significa che la pianificazione verrà eseguita ogni giorno all’1. |
| `state` | Stringa contenente lo stato della pianificazione. I due stati supportati sono `active` e `inactive`. Per impostazione predefinita, lo stato è impostato su `inactive`. |

+++

## Aggiorna i dettagli per una pianificazione specifica {#update}

È possibile aggiornare una pianificazione specifica effettuando una richiesta PATCH all&#39;endpoint `/config/schedules` e fornendo l&#39;ID della pianificazione che si sta tentando di aggiornare nel percorso della richiesta.

La richiesta PATCH ti consente di aggiornare [state](#update-state) o la [cron schedule](#update-schedule) per una singola pianificazione.

**Formato API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Il valore `id` della pianificazione da aggiornare. |

>[!BEGINTABS]

>[!TAB Aggiorna stato pianificazione]

È possibile utilizzare un’operazione Patch JSON per aggiornare lo stato della pianificazione. Per aggiornare lo stato, dichiarare la proprietà `path` come `/state` e impostare `value` su `active` o `inactive`. Per ulteriori informazioni sulla patch JSON, leggere la documentazione della patch [JSON](https://datatracker.ietf.org/doc/html/rfc6902).

**Richiesta**

+++ Richiesta di esempio per aggiornare lo stato della pianificazione.

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

+++

| Proprietà | Descrizione |
| -------- | ----------- |
| `path` | Percorso del valore a cui applicare la patch. In questo caso, poiché si sta aggiornando lo stato della pianificazione, è necessario impostare il valore di `path` su &quot;/state&quot;. |
| `value` | Il valore aggiornato dello stato della pianificazione. Questo valore può essere impostato come &quot;attivo&quot; o &quot;inattivo&quot; per attivare o disattivare la pianificazione. **impossibile** disabilitare una pianificazione se l&#39;organizzazione è stata abilitata per lo streaming. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto).

>[!TAB Aggiorna pianificazione cron]

È possibile utilizzare un’operazione Patch JSON per aggiornare la pianificazione cron. Per aggiornare la pianificazione, dichiarare la proprietà `path` come `/schedule` e impostare `value` su una pianificazione cron valida. Per ulteriori informazioni sulla patch JSON, leggere la documentazione della patch [JSON](https://datatracker.ietf.org/doc/html/rfc6902). Per ulteriori informazioni sulle pianificazioni cron, leggere l&#39;appendice nel formato di espressione cron [](#appendix).

>[!ENDTABS]

**Richiesta**

+++ Richiesta di esempio per aggiornare la pianificazione.

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
| `path` | Percorso del valore da aggiornare. In questo caso, poiché si sta aggiornando la pianificazione cron, è necessario impostare il valore di `path` su `/schedule`. |
| `value` | Il valore aggiornato della pianificazione cron. Questo valore deve essere sotto forma di una pianificazione cron. In questo esempio, la pianificazione verrà eseguita il secondo di ogni mese. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto).

## Eliminare una pianificazione specifica

È possibile richiedere l&#39;eliminazione di una pianificazione specifica effettuando una richiesta DELETE all&#39;endpoint `/config/schedules` e fornendo l&#39;ID della pianificazione da eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Il valore `id` della pianificazione da eliminare. |

**Richiesta**

+++ Richiesta di esempio per eliminare una pianificazione.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

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
>I nomi dei mesi e dei giorni della settimana sono **senza** distinzione tra maiuscole e minuscole. Pertanto, `SUN` equivale a utilizzare `sun`.

I caratteri speciali consentiti rappresentano i seguenti significati:

| Carattere speciale | Descrizione |
| ----------------- | ----------- |
| `*` | Questo valore viene utilizzato per selezionare **tutti** valori in un campo. Ad esempio, inserire `*` nel campo ore significherebbe **ogni** ora. |
| `?` | Questo valore significa che non è richiesto alcun valore specifico. Questo generalmente viene utilizzato per specificare qualcosa in un campo in cui il carattere è consentito, ma non specificarlo nell’altro. Ad esempio, se desideri che un evento venga attivato ogni 3 del mese, ma non importa di quale giorno della settimana si tratti, inserisci `3` nel campo del giorno del mese e `?` nel campo del giorno della settimana. |
| `-` | Questo valore viene utilizzato per specificare **inclusivo** intervalli per il campo. Ad esempio, se inserisci `9-15` nel campo ore, significa che le ore includerebbero 9, 10, 11, 12, 13, 14 e 15. |
| `,` | Questo valore viene utilizzato per specificare valori aggiuntivi. Se ad esempio si inserisce `MON, FRI, SAT` nel campo del giorno della settimana, i giorni della settimana includeranno lunedì, venerdì e sabato. |
| `/` | Questo valore viene utilizzato per specificare gli incrementi. Il valore posizionato prima di `/` determina da dove viene incrementato, mentre il valore posizionato dopo `/` determina di quanto viene incrementato. Se ad esempio si inserisce `1/7` nel campo minuti, i minuti includeranno 1, 8, 15, 22, 29, 36, 43, 50 e 57. |
| `L` | Questo valore viene utilizzato per specificare `Last` e ha un significato diverso a seconda del campo da cui viene utilizzato. Se viene utilizzato con il campo del giorno del mese, rappresenta l’ultimo giorno del mese. Se viene utilizzato con il campo del giorno della settimana, rappresenta l&#39;ultimo giorno della settimana, ovvero il sabato (`SAT`). Se viene utilizzato insieme al campo giorno della settimana e a un altro valore, rappresenta l&#39;ultimo giorno di quel tipo per il mese. Se ad esempio si inserisce `5L` nel campo del giorno della settimana, **solo** includerebbe l&#39;ultimo venerdì del mese. |
| `W` | Questo valore viene utilizzato per specificare il giorno feriale più vicino al giorno specificato. Ad esempio, se si inserisce `18W` nel campo del giorno del mese e il 18 di quel mese è un sabato, l&#39;attivazione avverrà venerdì 17, che è il giorno feriale più vicino. Se il 18 di quel mese fosse una domenica, sarebbe attivato lunedì 19, che è il giorno feriale più vicino. Tieni presente che se inserisci `1W` nel campo del giorno del mese e il giorno feriale più vicino è nel mese precedente, l&#39;evento verrà comunque attivato nel giorno feriale più vicino del mese **corrente**.</br></br>È inoltre possibile combinare `L` e `W` per creare `LW`, che specificherebbe l&#39;ultimo giorno feriale del mese. |
| `#` | Questo valore viene utilizzato per specificare l’ennesimo giorno della settimana in un mese. Il valore inserito prima del `#` rappresenta il giorno della settimana, mentre il valore inserito dopo il `#` rappresenta l&#39;occorrenza nel mese in cui si trova. Se ad esempio si inserisce `1#3`, l&#39;evento verrà attivato la terza domenica del mese. Tieni presente che se inserisci `X#5` e non si verifica un quinto evento di quel giorno della settimana in quel mese, l&#39;evento **non** verrà attivato. Ad esempio, se inserisci `1#5` e non c&#39;è una quinta domenica in quel mese, l&#39;evento **non** verrà attivato. |

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