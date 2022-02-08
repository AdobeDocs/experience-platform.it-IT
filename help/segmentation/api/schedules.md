---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;pianificazioni;pianificazione;api;API;
solution: Experience Platform
title: Endpoint API di pianificazione
topic-legacy: developer guide
description: Le pianificazioni sono uno strumento che può essere utilizzato per eseguire automaticamente i processi di segmentazione batch una volta al giorno.
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: a4f5602365d5db28ba375db0794b80670229fa75
workflow-type: tm+mt
source-wordcount: '2013'
ht-degree: 4%

---

# Endpoint di pianificazione

Le pianificazioni sono uno strumento che può essere utilizzato per eseguire automaticamente i processi di segmentazione batch una volta al giorno. È possibile utilizzare `/config/schedules` per recuperare un elenco di pianificazioni, creare una nuova pianificazione, recuperare i dettagli di una pianificazione specifica, aggiornare una pianificazione specifica o eliminare una pianificazione specifica.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte del [!DNL Adobe Experience Platform Segmentation Service] API. Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, comprese le intestazioni richieste e come leggere le chiamate API di esempio.

## Recupera un elenco di pianificazioni {#retrieve-list}

Puoi recuperare un elenco di tutte le pianificazioni per la tua organizzazione IMS effettuando una richiesta di GET al `/config/schedules` punto finale.

**Formato API**

La `/config/schedules` l’endpoint supporta diversi parametri di query per facilitare il filtraggio dei risultati. Sebbene questi parametri siano opzionali, si consiglia vivamente di utilizzarli per ridurre i costi di overhead. Effettuare una chiamata a questo endpoint senza parametri recupererà tutte le pianificazioni disponibili per la tua organizzazione. È possibile includere più parametri, separati da e commerciale (`&`).

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
| `children.properties.segments` | Utilizzo `["*"]` assicura che tutti i segmenti siano inclusi. |
| `children.schedule` | Una stringa contenente la pianificazione del processo. L&#39;esecuzione dei processi può essere pianificata solo una volta al giorno, il che significa che non è possibile pianificare l&#39;esecuzione di un processo più di una volta durante un periodo di 24 ore. Per maggiori informazioni sugli orari dei cron, si prega di leggere l&#39;appendice sul [formato di espressione cron](#appendix). In questo esempio, &quot;0 1 * * *&quot; significa che questa pianificazione verrà eseguita all’1 di mattina ogni giorno. |
| `children.state` | Una stringa contenente lo stato della pianificazione. I due stati supportati sono &quot;attivi&quot; e &quot;inattivi&quot;. Per impostazione predefinita, lo stato è impostato su &quot;inattivo&quot;. |

## Crea una nuova pianificazione {#create}

Puoi creare una nuova pianificazione effettuando una richiesta POST al `/config/schedules` punto finale.

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
| `properties.segments` | **Obbligatorio quando `type` è uguale a &quot;batch_segmentation&quot;.** Utilizzo `["*"]` assicura che tutti i segmenti siano inclusi. |
| `schedule` | *Facoltativo.* Una stringa contenente la pianificazione del processo. L&#39;esecuzione dei processi può essere pianificata solo una volta al giorno, il che significa che non è possibile pianificare l&#39;esecuzione di un processo più di una volta durante un periodo di 24 ore. Per maggiori informazioni sugli orari dei cron, si prega di leggere l&#39;appendice sul [formato di espressione cron](#appendix). In questo esempio, &quot;0 1 * * *&quot; significa che questa pianificazione verrà eseguita all’1 di mattina ogni giorno. <br><br>Se questa stringa non viene fornita, verrà generata automaticamente una pianificazione generata dal sistema. |
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

Puoi recuperare informazioni dettagliate su una pianificazione specifica effettuando una richiesta di GET al `/config/schedules` e fornisce l’ID della pianificazione da recuperare nel percorso della richiesta.

**Formato API**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SCHEDULE_ID}` | La `id` valore della pianificazione che si desidera recuperare. |

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
| `properties.segments` | Utilizzo `["*"]` assicura che tutti i segmenti siano inclusi. |
| `schedule` | Una stringa contenente la pianificazione del processo. L&#39;esecuzione dei processi può essere pianificata solo una volta al giorno, il che significa che non è possibile pianificare l&#39;esecuzione di un processo più di una volta durante un periodo di 24 ore. Per maggiori informazioni sugli orari dei cron, si prega di leggere l&#39;appendice sul [formato di espressione cron](#appendix). In questo esempio, &quot;0 1 * * *&quot; significa che questa pianificazione verrà eseguita all’1 di mattina ogni giorno. |
| `state` | Una stringa contenente lo stato della pianificazione. I due stati supportati sono `active` e `inactive`. Per impostazione predefinita, lo stato è impostato su `inactive`. |

## Aggiorna i dettagli di una pianificazione specifica {#update}

È possibile aggiornare una pianificazione specifica effettuando una richiesta PATCH al `/config/schedules` e fornisce l&#39;ID della pianificazione che stai tentando di aggiornare nel percorso della richiesta.

La richiesta di PATCH consente di aggiornare [stato](#update-state) o [programma](#update-schedule) per un programma individuale.

### Aggiorna stato pianificazione {#update-state}

Puoi utilizzare un’operazione Patch JSON per aggiornare lo stato della pianificazione. Per aggiornare lo stato, dichiarare il `path` proprietà come `/state` e imposta `value` a `active` o `inactive`. Per ulteriori informazioni sulla patch JSON, consulta la sezione [Patch JSON](https://datatracker.ietf.org/doc/html/rfc6902) documentazione.

**Formato API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SCHEDULE_ID}` | La `id` valore della pianificazione da aggiornare. |

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
| `path` | Percorso del valore a cui si desidera applicare la patch. In questo caso, poiché aggiorni lo stato della pianificazione, devi impostare il valore di `path` a &quot;/state&quot;. |
| `value` | Valore aggiornato dello stato della pianificazione. Questo valore può essere impostato come &quot;attivo&quot; o &quot;inattivo&quot; per attivare o disattivare la pianificazione. Si prega di notare che **impossibile** disabilita una pianificazione se l’organizzazione IMS è stata abilitata per lo streaming. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (nessun contenuto).

### Aggiorna pianificazione cron {#update-schedule}

Puoi utilizzare un’operazione Patch JSON per aggiornare la pianificazione cron. Per aggiornare la pianificazione, dichiarare il `path` proprietà come `/schedule` e imposta `value` a una pianificazione di cron valida. Per ulteriori informazioni sulla patch JSON, consulta la sezione [Patch JSON](https://datatracker.ietf.org/doc/html/rfc6902) documentazione. Per maggiori informazioni sugli orari dei cron, si prega di leggere l&#39;appendice sul [formato di espressione cron](#appendix).

**Formato API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SCHEDULE_ID}` | La `id` valore della pianificazione da aggiornare. |

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
| `path` | Percorso del valore da aggiornare. In questo caso, poiché aggiorni la pianificazione cron, devi impostare il valore di `path` a `/schedule`. |
| `value` | Valore aggiornato della pianificazione cron. Questo valore deve essere sotto forma di programma cron. In questo esempio, la pianificazione verrà eseguita il secondo di ogni mese. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (nessun contenuto).

## Elimina una pianificazione specifica

È possibile richiedere l’eliminazione di una pianificazione specifica effettuando una richiesta di DELETE al `/config/schedules` e fornisce l’ID della pianificazione da eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SCHEDULE_ID}` | La `id` valore della pianificazione da eliminare. |

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

## Appendice {#appendix}

La seguente appendice spiega il formato delle espressioni cron utilizzate nei programmi.

### Formato

Un&#39;espressione cron è una stringa composta da 6 o 7 campi. L&#39;espressione avrà un aspetto simile al seguente:

`0 0 12 * * ?`

In una stringa di espressione cron, il primo campo rappresenta i secondi, il secondo campo rappresenta i minuti, il terzo campo rappresenta le ore, il quarto campo rappresenta il giorno del mese, il quinto campo rappresenta il mese e il sesto campo rappresenta il giorno della settimana. Facoltativamente, puoi anche includere un settimo campo, che rappresenta l’anno.

| Nome campo | Obbligatorio | Valori possibili | Caratteri speciali consentiti |
| ---------- | -------- | --------------- | -------------------------- |
| Seconds | Sì | 0-59 | `, - * /` |
| Minutes | Sì | 0-59 | `, - * /` |
| Ore | Sì | 0-23 | `, - * /` |
| Giorno del mese | Sì | 1-31 | `, - * ? / L W` |
| Mese | Sì | 1-12, JAN-DEC | `, - * /` |
| Giorno della settimana | Sì | 1-7, SUN-SAT | `, - * ? / L #` |
| Anno | No | Vuoto, 1970-2099 | `, - * /` |

>[!NOTE]
>
>I nomi dei mesi e i nomi dei giorni della settimana sono **not** sensibile a maiuscole e minuscole. Pertanto, `SUN` equivale a utilizzare `sun`.

I caratteri speciali consentiti rappresentano i seguenti significati:

| Carattere speciale | Descrizione |
| ----------------- | ----------- |
| `*` | Questo valore viene utilizzato per selezionare **tutto** in un campo. Ad esempio, inserendo `*` nel campo delle ore significa **ogni** ora. |
| `?` | Questo valore significa che non è richiesto alcun valore specifico. In genere viene utilizzato per specificare qualcosa in un campo in cui il carattere è consentito, ma non nell’altro. Ad esempio, se desideri che un evento venga attivato ogni 3 del mese, ma non ti interessa il giorno della settimana, puoi inserire `3` nel campo del giorno del mese e `?` nel campo giorno della settimana. |
| `-` | Questo valore viene utilizzato per specificare **inclusivo** Intervalli per il campo . Ad esempio, se metti `9-15` nel campo ore, questo significa che le ore includerebbero 9, 10, 11, 12, 13, 14 e 15. |
| `,` | Questo valore viene utilizzato per specificare valori aggiuntivi. Ad esempio, se metti `MON, FRI, SAT` nel campo del giorno della settimana, ciò significa che i giorni della settimana includeranno lunedì, venerdì e sabato. |
| `/` | Questo valore viene utilizzato per specificare gli incrementi. Il valore inserito prima della `/` determina da dove viene incrementato, mentre il valore inserito dopo il `/` determina la quantità di incremento. Ad esempio, se metti `1/7` nel campo dei minuti, ciò significa che i minuti includeranno 1, 8, 15, 22, 29, 36, 43, 50 e 57. |
| `L` | Questo valore viene utilizzato per specificare `Last`e ha un significato diverso a seconda del campo in cui viene utilizzato. Se viene utilizzato con il campo giorno del mese , rappresenta l’ultimo giorno del mese. Se viene utilizzato con il campo giorno della settimana di per sé, rappresenta l’ultimo giorno della settimana, che è sabato (`SAT`). Se viene utilizzato insieme al campo giorno della settimana, insieme a un altro valore, rappresenta l’ultimo giorno di quel tipo per il mese. Ad esempio, se metti `5L` nel campo del giorno della settimana, **only** includere l’ultimo venerdì del mese. |
| `W` | Questo valore viene utilizzato per specificare il giorno feriale più vicino al giorno specificato. Ad esempio, se metti `18W` nel campo del giorno del mese, e il 18 di quel mese era un sabato, attivava il venerdì del 17, che è il giorno feriale più vicino. Se il 18 di quel mese fosse una domenica, il trigger sarebbe il lunedì il 19, che è il giorno feriale più vicino. Si prega di notare che se si mette `1W` nel campo del giorno del mese e il giorno feriale più vicino è quello del mese precedente, l&#39;evento si attiva ancora il giorno feriale più vicino del **attuale** mese.</br></br>Inoltre, puoi combinare `L` e `W` fare `LW`, che specifica l’ultimo giorno della settimana del mese. |
| `#` | Questo valore viene utilizzato per specificare l’ennesimo giorno della settimana in un mese. Il valore inserito prima della `#` rappresenta il giorno della settimana, mentre il valore inserito dopo il `#` rappresenta l&#39;occorrenza nel mese in cui si trova. Ad esempio, se metti `1#3`, l&#39;evento si sarebbe verificato la terza domenica del mese. Si prega di notare che se si mette `X#5` e non c&#39;è quinta occorrenza di quel giorno della settimana in quel mese, l&#39;evento **not** essere attivate. Ad esempio, se metti `1#5`e non c&#39;è quinta domenica in quel mese, l&#39;evento **not** essere attivate. |

### Esempi

La tabella seguente mostra le stringhe di espressione cron di esempio e spiega cosa intendono.

| Espressione | Spiegazione |
| ---------- | ----------- |
| `0 0 13 * * ?` | L&#39;evento si attiverà alle 13 di ogni giorno. |
| `0 30 9 * * ? 2022` | L&#39;evento si attiverà ogni giorno alle 9.30 del mattino nel 2022. |
| `0 * 18 * * ?` | L&#39;evento si attiva ogni minuto, a partire dalle 18.00 e terminerà alle 18.59, ogni giorno. |
| `0 0/10 17 * * ?` | L&#39;evento si attiverà ogni 10 minuti, a partire dalle 17.00 e terminerà alle 18.00 di ogni giorno. |
| `0 13,38 5 ? 6 WED` | L&#39;evento si attiverà alle 5:13 e alle 5:38 ogni mercoledì di giugno. |
| `0 30 12 ? * 4#3` | L&#39;evento si attiverà alle 12.30 del pomeriggio del terzo mercoledì di ogni mese. |
| `0 30 12 ? * 6L` | L&#39;evento si attiverà alle 12.30 dell&#39;ultimo venerdì di ogni mese. |
| `0 45 11 ? * MON-THU` | L&#39;evento si attiverà ogni lunedì, martedì, mercoledì e giovedì alle 11:45. |