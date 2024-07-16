---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API per processi di sistema profilo
type: Documentation
description: Adobe Experience Platform consente di eliminare un set di dati o un batch dall’archivio profili per rimuovere i dati Profilo cliente in tempo reale che non sono più necessari o che sono stati aggiunti per errore. A tal fine è necessario utilizzare l’API di profilo per creare un processo di sistema del profilo o eliminare una richiesta.
role: Developer
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 3%

---

# Endpoint &quot;profile system jobs&quot; (richieste di eliminazione)

Adobe Experience Platform consente di acquisire dati da più origini e di creare profili affidabili per i singoli clienti. I dati acquisiti in [!DNL Platform] sono memorizzati in [!DNL Data Lake] e se i set di dati sono stati abilitati per il profilo, tali dati vengono memorizzati anche nell&#39;archivio dati [!DNL Real-Time Customer Profile]. Talvolta può essere necessario eliminare i dati di profilo associati a un set di dati dall’archivio Profili per rimuovere i dati non più necessari o che sono stati aggiunti per errore. È necessario utilizzare l&#39;API [!DNL Real-Time Customer Profile] per creare un processo di sistema [!DNL Profile], o `delete request`, che può anche essere modificato, monitorato o rimosso se necessario.

>[!NOTE]
>
>Se si sta tentando di eliminare set di dati o batch da [!DNL Data Lake], visitare la [panoramica del servizio catalogo](../../catalog/home.md) per ulteriori informazioni.

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte di [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Prima di continuare, consulta la [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e per le informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Visualizzare le richieste di eliminazione

Una richiesta di eliminazione è un processo asincrono a lungo termine, il che significa che l’organizzazione potrebbe eseguire più richieste di eliminazione contemporaneamente. Per visualizzare tutte le richieste di eliminazione attualmente in esecuzione nell&#39;organizzazione, è possibile eseguire una richiesta GET all&#39;endpoint `/system/jobs`.

Puoi anche utilizzare parametri di query facoltativi per filtrare l’elenco delle richieste di eliminazione restituite nella risposta. Per utilizzare più parametri, separare ogni parametro utilizzando una e commerciale (`&`).

**Formato API**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parametro | Descrizione |
|---|---|
| `start` | Offset della pagina dei risultati restituiti, in base all’ora di creazione della richiesta. Esempio: `start=4` |
| `limit` | Limita il numero di risultati restituiti. Esempio: `limit=10` |
| `page` | Restituisce una pagina di risultati specifica, in base all’ora di creazione della richiesta. Esempio: `page=2` |
| `sort` | Ordinare i risultati per un campo specifico in ordine crescente (`asc`) o decrescente (`desc`). Il parametro sort non funziona quando si restituiscono più pagine di risultati. Esempio: `sort=batchId:asc` |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

La risposta include un array &quot;figlio&quot; con un oggetto per ogni richiesta di eliminazione contenente i dettagli della richiesta.

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{ORG_ID}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{ORG_ID}",
      "dataSetId": "5c802d3cd83fc114b741c4b5",
      "jobType": "DELETE",
      "status": "PROCESSING",
      "metrics": "{\"recordsProcessed\":0,\"timeTakenInSec\":15}",
      "createEpoch": 1559025404,
      "updateEpoch": 1559025406
    }
  ]
}
```

| Proprietà | Descrizione |
|---|---|
| `_page.count` | Numero totale di richieste. La risposta è stata troncata per motivi di spazio. |
| `_page.next` | Se esiste una pagina di risultati aggiuntiva, visualizzare la pagina di risultati successiva sostituendo il valore ID in una [richiesta di ricerca](#view-a-specific-delete-request) con il valore `"next"` fornito. |
| `jobType` | Tipo di processo da creare. In questo caso, restituirà sempre `"DELETE"`. |
| `status` | Stato della richiesta di eliminazione. I valori possibili sono `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Oggetto che include il numero di record elaborati (`"recordsProcessed"`) e il tempo in secondi di elaborazione della richiesta oppure il tempo impiegato per il completamento della richiesta (`"timeTakenInSec"`). |

## Creare una richiesta di eliminazione {#create-a-delete-request}

L&#39;avvio di una nuova richiesta di eliminazione viene eseguito tramite una richiesta POST all&#39;endpoint `/systems/jobs`, in cui l&#39;ID del set di dati o del batch da eliminare viene fornito nel corpo della richiesta.

### Eliminare un set di dati e i dati del profilo associati

Per eliminare un set di dati e tutti i dati di profilo associati al set di dati dall’archivio profili, l’ID del set di dati deve essere incluso nel corpo della richiesta POST. Questa azione eliminerà TUTTI i dati per un dato set di dati. [!DNL Experience Platform] consente di eliminare i set di dati basati su schemi di record e serie temporali.

**Formato API**

```http
POST /system/jobs
```

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

| Proprietà | Descrizione |
|---|---|
| `dataSetId` | **(Obbligatorio)** ID del set di dati da eliminare. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della nuova richiesta di eliminazione creata, incluso un ID univoco di sola lettura generato dal sistema per la richiesta. Può essere utilizzato per cercare la richiesta e verificarne lo stato. Il `status` per la richiesta al momento della creazione è `"NEW"` fino a quando non inizia l&#39;elaborazione. Il `dataSetId` nella risposta deve corrispondere al `dataSetId` inviato nella richiesta.

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{ORG_ID}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| Proprietà | Descrizione |
|---|---|
| `id` | ID univoco generato dal sistema e di sola lettura della richiesta di eliminazione. |
| `dataSetId` | ID del set di dati, come specificato nella richiesta POST. |

### Eliminare un batch

Per eliminare un batch, l’ID del batch deve essere incluso nel corpo della richiesta POST. Si noti che non è possibile eliminare batch per set di dati basati su schemi di record. È possibile eliminare solo i batch per i set di dati basati su schemi di serie temporali.

>[!NOTE]
>
> Il motivo per cui non è possibile eliminare i batch per i set di dati basati su schemi di record è che i batch di set di dati di tipo record sovrascrivono i record precedenti e pertanto non possono essere &quot;annullati&quot; o eliminati. L’unico modo per rimuovere l’impatto di batch errati per i set di dati basati su schemi di record consiste nel riacquisire il batch con i dati corretti in modo da sovrascrivere i record errati.

Per ulteriori informazioni sul comportamento di record e serie temporali, consulta la [sezione sui comportamenti dei dati XDM](../../xdm/home.md#data-behaviors) nella panoramica di [!DNL XDM System].

**Formato API**

```http
POST /system/jobs
```

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| Proprietà | Descrizione |
|---|---|
| `batchId` | **(Obbligatorio)** ID del batch da eliminare. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della nuova richiesta di eliminazione creata, incluso un ID univoco di sola lettura generato dal sistema per la richiesta. Può essere utilizzato per cercare la richiesta e verificarne lo stato. Il `"status"` per la richiesta al momento della creazione è `"NEW"` fino a quando non inizia l&#39;elaborazione. Il valore `"batchId"` nella risposta deve corrispondere al valore `"batchId"` inviato nella richiesta.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| Proprietà | Descrizione |
|---|---|
| `id` | ID univoco generato dal sistema e di sola lettura della richiesta di eliminazione. |
| `batchId` | ID del batch, come specificato nella richiesta POST. |

Se si tenta di avviare una richiesta di eliminazione per un batch di set di dati Record, si verifica un errore a 400 livelli, simile al seguente:

```json
{
    "requestId": "bc4eb29f-63a8-4653-9133-71238884bb81",
    "errors": {
        "400": [
            {
                "code": "500",
                "message": "Batch can only be specified for EE type 'a294e36d382649dab2cc6ad64a41b674'"
            }
        ]
    }
}
```

## Visualizzare una richiesta di eliminazione specifica {#view-a-specific-delete-request}

Per visualizzare una richiesta di eliminazione specifica, inclusi dettagli quali lo stato, è possibile eseguire una richiesta di ricerca (GET) all&#39;endpoint `/system/jobs` e includere l&#39;ID della richiesta di eliminazione nel percorso.

**Formato API**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Parametro | Descrizione |
|---|---|
| `{DELETE_REQUEST_ID}` | **(Obbligatorio)** ID della richiesta di eliminazione che si desidera visualizzare. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

La risposta fornisce i dettagli della richiesta di eliminazione, compreso il suo stato aggiornato. L&#39;ID della richiesta di eliminazione nella risposta (il valore `"id"`) deve corrispondere all&#39;ID inviato nel percorso della richiesta.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "COMPLETED",
    "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
    "createEpoch": 1559026134,
    "updateEpoch": 1559026137
}
```

| Proprietà | Descrizione |
|---|---|
| `jobType` | Tipo di processo in fase di creazione. In questo caso, restituirà sempre `"DELETE"`. |
| `status` | Stato della richiesta di eliminazione. Valori possibili: `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Matrice che include il numero di record elaborati (`"recordsProcessed"`) e il tempo in secondi di elaborazione della richiesta oppure il tempo impiegato per il completamento della richiesta (`"timeTakenInSec"`). |

Quando lo stato della richiesta di eliminazione è `"COMPLETED"`, è possibile confermare che i dati sono stati eliminati tentando di accedere ai dati eliminati tramite l&#39;API di accesso ai dati. Per istruzioni su come utilizzare l&#39;API di accesso ai dati per accedere ai set di dati e ai batch, consulta la [documentazione sull&#39;accesso ai dati](../../data-access/home.md).

## Rimuovere una richiesta di eliminazione

[!DNL Experience Platform] consente di eliminare una richiesta precedente, che può essere utile per diversi motivi, tra cui se il processo di eliminazione non è stato completato o si è bloccato nella fase di elaborazione. Per rimuovere una richiesta di eliminazione, è possibile eseguire una richiesta DELETE all&#39;endpoint `/system/jobs` e includere l&#39;ID della richiesta di eliminazione che si desidera rimuovere nel percorso della richiesta.

**Formato API**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| Parametro | Descrizione |
|---|---|
| {DELETE_REQUEST_ID} | ID della richiesta di eliminazione che desideri rimuovere. |

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

In caso di esito positivo, la richiesta di eliminazione restituisce lo stato HTTP 200 (OK) e un corpo di risposta vuoto. Per confermare l’eliminazione della richiesta, esegui una richiesta GET per visualizzarla in base al relativo ID. Questo dovrebbe restituire lo stato HTTP 404 (Non trovato), che indica che la richiesta di eliminazione è stata rimossa.

## Passaggi successivi

Ora che si conoscono i passaggi necessari per eliminare i set di dati e i batch da [!DNL Profile store] in [!DNL Experience Platform], è possibile eliminare in modo sicuro i dati aggiunti erroneamente o di cui l&#39;organizzazione non ha più bisogno. Tieni presente che una richiesta di cancellazione non può essere annullata, pertanto devi eliminare solo i dati che ritieni non necessari al momento e che non saranno necessari in futuro.
