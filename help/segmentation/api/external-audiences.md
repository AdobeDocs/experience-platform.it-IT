---
title: Endpoint API per tipi di pubblico esterni
description: Scopri come utilizzare l’API per tipi di pubblico esterni per creare, aggiornare, attivare ed eliminare i tipi di pubblico esterni da Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 74fa66e78ac36c8007eb89e8c271d989845c96f0
workflow-type: tm+mt
source-wordcount: '2312'
ht-degree: 5%

---


# Endpoint &quot;external audiences&quot;

I tipi di pubblico esterni ti consentono di caricare i dati del profilo da sorgenti esterne in Adobe Experience Platform. È possibile utilizzare l&#39;endpoint `/external-audience` nell&#39;API del servizio di segmentazione per acquisire un pubblico esterno in Experience Platform, visualizzare i dettagli e aggiornare i tipi di pubblico esterni, nonché eliminarli.

## Introduzione

>[!IMPORTANT]
>
>Gli endpoint in questa guida hanno il prefisso `/core/ais`, invece di `/core/ups`.

Per utilizzare le API di Experience Platform, è necessario aver completato l&#39;[esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste nelle chiamate API di Experience Platform, come mostrato di seguito:

- Autorizzazione: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API [!DNL Experience Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sull&#39;utilizzo delle sandbox in [!DNL Experience Platform], consulta la [documentazione panoramica sulle sandbox](../../sandboxes/home.md).

## Creare un pubblico esterno {#create-audience}

Per creare un pubblico esterno, devi eseguire una richiesta POST all&#39;endpoint `/external-audience/`.

**Formato API**

```http
POST /external-audience/
```

**Richiesta**

+++ Una richiesta di esempio per creare un pubblico esterno.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "path": "activation/sample-source/example.csv",
            "type": "file",
            "sourceType": "Cloud Storage",
            "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

| Proprietà | Tipo | Descrizione |
| -------- | ---- | ----------- |
| `name` | Stringa | Il nome del pubblico esterno. |
| `description` | Stringa | Una descrizione facoltativa per il pubblico esterno. |
| `customAudienceId` | Stringa | Un identificatore opzionale per il pubblico esterno. |
| `fields` | Array di oggetti | L’elenco dei campi e i relativi tipi di dati. Durante la creazione dell’elenco di campi, puoi aggiungere i seguenti elementi: <ul><li>`name`: **Obbligatorio** Il nome del campo che fa parte della specifica del pubblico esterno.</li><li>`type`: **Obbligatorio** tipo di dati da inserire nel campo. I valori supportati sono `string`, `number`, `long`, `integer`, `date` (`2025-05-13`), `datetime` (`2025-05-23T20:19:00+00:00`) e `boolean`.</li>`identityNs`: **Obbligatorio per il campo di identità** Spazio dei nomi utilizzato dal campo di identità. I valori supportati includono tutti gli spazi dei nomi validi, ad esempio `ECID` o `email`.li><li>`labels`: *Facoltativo* Matrice di etichette di controllo di accesso per il campo. Ulteriori informazioni sulle etichette di controllo di accesso disponibili sono disponibili nel glossario [etichette di utilizzo dati](/help/data-governance/labels/reference.md). </li></ul> |
| `sourceSpec` | Oggetto | Oggetto contenente le informazioni in cui si trova il pubblico esterno. Quando utilizzi questo oggetto, **devi** includere le seguenti informazioni: <ul><li>`path`: **Obbligatorio**: posizione del pubblico esterno o cartella che contiene il pubblico esterno all&#39;interno dell&#39;origine.</li><li>`type`: **Obbligatorio** Il tipo dell&#39;oggetto che si sta recuperando dall&#39;origine. Questo valore può essere `file` o `folder`.</li><li>`sourceType`: *Facoltativo* Il tipo di origine da cui si sta recuperando. Attualmente, l&#39;unico valore supportato è `Cloud Storage`.</li><li>`cloudType`: *Facoltativo* Il tipo di archiviazione cloud, basato sul tipo di origine. I valori supportati sono `S3`, `DLZ`, `GCS` e `SFTP`.</li><li>`baseConnectionId`: ID della connessione di base e fornito dal provider di origine. Questo valore è **obbligatorio** se si utilizza un valore `cloudType` di `S3`, `GCS` o `SFTP`. Per ulteriori informazioni, leggere la [panoramica dei connettori di origine](../../sources/home.md)li></ul> |
| `ttlInDays` | Intero | La scadenza dei dati per il pubblico esterno, in giorni. Questo valore può essere impostato da 1 a 90. Per impostazione predefinita, la scadenza dei dati è impostata su 30 giorni. |
| `audienceType` | Stringa | Il tipo di pubblico per il pubblico esterno. Attualmente, è supportato solo `people`. |
| `originName` | Stringa | **Obbligatorio** L&#39;origine del pubblico. Indica da dove proviene il pubblico. Per i tipi di pubblico esterni, utilizzare `CUSTOM_UPLOAD`. |
| `namespace` | Stringa | Lo spazio dei nomi per il pubblico. Per impostazione predefinita, questo valore è impostato su `CustomerAudienceUpload`. |
| `labels` | Array di stringhe | Etichette di controllo di accesso applicabili al pubblico esterno. Ulteriori informazioni sulle etichette di controllo di accesso disponibili sono disponibili nel glossario [etichette di utilizzo dati](/help/data-governance/labels/reference.md). |
| `tags` | Array di stringhe | I tag che desideri applicare al pubblico esterno. Ulteriori informazioni sui tag sono disponibili nella [guida gestione tag](/help/administrative-tags/ui/managing-tags.md). |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 con i dettagli del pubblico esterno appena creato.

+++ Una risposta di esempio durante la creazione di un pubblico esterno.

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "path": "activation/sample-source/example.csv",
            "type": "file",
            "sourceType": "Cloud Storage",
            "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }   
}
```

| Proprietà | Tipo | Descrizione |
| -------- | ---- | ----------- |
| `operationId` | Stringa | ID dell’operazione. Successivamente puoi utilizzare questo ID per recuperare lo stato di creazione del pubblico. |
| `operationDetails` | Oggetto | Oggetto contenente i dettagli della richiesta inviata per creare il pubblico esterno. |
| `name` | Stringa | Il nome del pubblico esterno. |
| `description` | Stringa | Descrizione del pubblico esterno. |
| `fields` | Array di oggetti | L’elenco dei campi e i relativi tipi di dati. Questo array determina i campi necessari nel pubblico esterno. |
| `sourceSpec` | Oggetto | Oggetto contenente le informazioni in cui si trova il pubblico esterno. |
| `ttlInDays` | Intero | La scadenza dei dati per il pubblico esterno, in giorni. Questo valore può essere impostato da 1 a 90. Per impostazione predefinita, la scadenza dei dati è impostata su 30 giorni. |
| `audienceType` | Stringa | Il tipo di pubblico per il pubblico esterno. |
| `originName` | Stringa | **Obbligatorio** L&#39;origine del pubblico. Indica da dove proviene il pubblico. |
| `namespace` | Stringa | Lo spazio dei nomi per il pubblico. |
| `labels` | Array di stringhe | Etichette di controllo di accesso applicabili al pubblico esterno. Ulteriori informazioni sulle etichette di controllo di accesso disponibili sono disponibili nel glossario [etichette di utilizzo dati](/help/data-governance/labels/reference.md). |


+++

## Recuperare lo stato di creazione del pubblico {#retrieve-status}

Per recuperare lo stato dell&#39;invio del pubblico esterno, devi eseguire una richiesta GET all&#39;endpoint `/external-audiences/operations` e fornire l&#39;ID dell&#39;operazione ricevuta dalla risposta di creazione del pubblico esterno.

**Formato API**

```http
GET /external-audiences/operations/{OPERATION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{OPERATION_ID}` | Valore `id` dell&#39;operazione da recuperare. |

**Richiesta**

+++ Una richiesta di esempio per recuperare lo stato operativo di un pubblico esterno.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/df8cd82f-a214-4b72-b549-d6ee23f1ff1a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli dello stato delle attività del pubblico esterno.

+++ Una risposta di esempio quando recuperi lo stato delle attività di un pubblico esterno.

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "status": "SUCCESS",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "path": "activation/sample-source/example.csv",
            "type": "file",
            "sourceType": "Cloud Storage",
            "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    },
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

| Proprietà | Tipo | Descrizione |
| -------- | ---- | ----------- |
| `operationId` | Stringa | ID dell&#39;operazione da recuperare. |
| `status` | Stringa | Stato dell&#39;operazione. Può essere uno dei seguenti valori: `SUCCESS`, `FAILED`, `PROCESSING`. |
| `operationDetails` | Oggetto | Oggetto contenente i dettagli del pubblico. |
| `audienceId` | Stringa | ID del pubblico esterno che viene inviato dall’operazione. |
| `createdBy` | Stringa | ID dell’utente che ha creato il pubblico esterno. |
| `createdAt` | Timestamp dell’epoca lunga | La marca temporale, in secondi, di invio della richiesta di creazione del pubblico esterno. |
| `updatedBy` | Stringa | ID dell’ultimo utente che ha aggiornato il pubblico. |
| `updatedAt` | Timestamp dell’epoca lunga | La marca temporale, in secondi, di quando il pubblico è stato aggiornato l’ultima volta. |

+++

## Aggiornare un pubblico esterno {#update-audience}

>[!NOTE]
>
>Per utilizzare il seguente endpoint, è necessario disporre di `audienceId` del pubblico esterno. Puoi ottenere `audienceId` da una chiamata all&#39;endpoint `GET /external-audiences/operations/{OPERATION_ID}` riuscita.

Per aggiornare i campi del pubblico esterno, devi eseguire una richiesta PATCH all&#39;endpoint `/external-audience` e fornire l&#39;ID del pubblico nel percorso della richiesta.

Quando utilizzi questo endpoint, puoi aggiornare i campi seguenti:

- Descrizione del pubblico
- Etichette di controllo dell’accesso a livello di campo
- Etichette di controllo dell’accesso a livello di pubblico

L&#39;aggiornamento del campo utilizzando questo endpoint **sostituisce** il contenuto del campo richiesto.

**Formato API**

```http
PATCH /external-audience/{AUDIENCE_ID}
```

**Richiesta**

+++ Una richiesta di esempio per aggiornare la descrizione del pubblico esterno.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab\
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "description": "New sample description"
 }'
```

| Proprietà | Tipo | Descrizione |
| -------- | ---- | ----------- |
| `description` | Stringa | Descrizione aggiornata per il pubblico esterno. |

Inoltre, puoi aggiornare i seguenti parametri:

| Proprietà | Tipo | Descrizione |
| -------- | ---- | ----------- |
| `labels` | Array | Matrice contenente l’elenco aggiornato delle etichette di accesso per il pubblico. Ulteriori informazioni sulle etichette di controllo di accesso disponibili sono disponibili nel glossario [etichette di utilizzo dati](/help/data-governance/labels/reference.md). |
| `fields` | Array di oggetti | Un array contenente i campi e le relative etichette associate per il pubblico esterno. Solo i campi elencati nella richiesta PATCH verranno aggiornati. Ulteriori informazioni sulle etichette di controllo di accesso disponibili sono disponibili nel glossario [etichette di utilizzo dati](/help/data-governance/labels/reference.md). |
| `ttlInDays` | Intero | La scadenza dei dati per il pubblico esterno, in giorni. Questo valore può essere impostato da 1 a 90. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli del pubblico esterno aggiornato.

+++ Una risposta di esempio durante l’aggiornamento della descrizione del pubblico esterno.

```json
{
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceName": "Sample external audience",
    "description": "New sample description",
    "fields": [
        {
            "name": "ppid",
            "type": "string",
            "identityNs": "Email"
        },
        {
            "name": "list_id",
            "type": "string",
            "labels": ["core/C2", "custom/deep"]
        },
        {
            "name": "delete",
            "type": "number"
        },
        {
            "name": "process_consent",
            "type": "string"
        }
    ],
    "sourceSpec": {
        "path": "activation/sample-source/example.csv",
        "type": "file",
        "sourceType": "Cloud Storage",
        "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
        },
    "ttlInDays": 40,
    "labels": ["core/C1"],
    "audienceType": "people",
    "originName": "CUSTOM_UPLOAD",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

+++

## Avvia l’acquisizione del pubblico {#start-audience-ingestion}

>[!IMPORTANT]
>
>**impossibile** avviare una nuova acquisizione per il pubblico esterno se è già in corso una precedente acquisizione del pubblico.

>[!NOTE]
>
>Per utilizzare il seguente endpoint, è necessario disporre di `audienceId` del pubblico esterno. Puoi ottenere `audienceId` da una chiamata all&#39;endpoint `GET /external-audiences/operations/{OPERATION_ID}` riuscita.

Per avviare l’acquisizione di un pubblico, effettua una richiesta POST all’endpoint seguente e specifica l’ID del pubblico.

**Formato API**

```http
POST /external-audience/{AUDIENCE_ID}/run
```

**Richiesta**

La seguente richiesta attiva un’acquisizione eseguita per il pubblico esterno.

+++ Una richiesta di esempio per avviare un’acquisizione di pubblico.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/run \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

| Proprietà | Tipo | Descrizione |
| -------- | ---- | ----------- |
| `dataFilterStartTime` | Timestamp epoca | **Obbligatorio** L&#39;intervallo che specifica l&#39;ora di inizio dell&#39;esecuzione del flusso per selezionare i file da elaborare. |
| `dataFilterEndTime` | Timestamp epoca | L’intervallo che specifica l’ora di fine in cui il flusso verrà eseguito per selezionare i file da elaborare. |
| `differentialIngestion` | Booleano | Campo che determina se l’acquisizione sarà un’acquisizione parziale in base alla differenza rispetto all’ultima acquisizione o a un’acquisizione completa di pubblico. Per impostazione predefinita, questo valore è `true`. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con dettagli sull’esecuzione dell’acquisizione.

+++ Una risposta di esempio all’avvio dell’acquisizione del pubblico.

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 4565657575,
    "createdAt": 4565657575,
    "createdBy:" "{USER_ID}"
}
```

| Proprietà | Tipo | Descrizione |
| -------- | ---- | ----------- |
| `audienceName` | Stringa | Il nome del pubblico per il quale stai avviando un’esecuzione di acquisizione. |
| `audienceId` | Stringa | ID del pubblico. |
| `runId` | Stringa | ID dell’esecuzione dell’acquisizione avviata. |
| `differentialIngestion` | Booleano | Campo che determina se l’acquisizione è un’acquisizione parziale in base alla differenza rispetto all’ultima acquisizione o a un’acquisizione completa di pubblico. |
| `dataFilterStartTime` | Timestamp epoca | L’intervallo che specifica l’ora di inizio dell’esecuzione del flusso per selezionare i file elaborati. |
| `dataFilterEndTime` | Timestamp epoca | L’intervallo che specifica il tempo finale di esecuzione del flusso per selezionare i file elaborati. |
| `createdAt` | Timestamp dell’epoca lunga | La marca temporale, in secondi, di invio della richiesta di creazione del pubblico esterno. |
| `createdBy` | Stringa | ID dell’utente che ha creato il pubblico esterno. |

+++

## Recuperare lo stato di acquisizione di un pubblico specifico {#retrieve-ingestion-status}

Per recuperare lo stato di un’acquisizione di pubblico, effettua una richiesta GET al seguente endpoint e allo stesso tempo fornisce sia l’ID del pubblico che gli ID di esecuzione.

**Formato API**

```http
GET /external-audience/{AUDIENCE_ID}/runs/{RUN_ID}
```

**Richiesta**

La seguente richiesta recupera lo stato di acquisizione per il pubblico esterno.

+++ Una richiesta di esempio per recuperare lo stato di acquisizione del pubblico esterno.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs/fb342311-725d-4b48-ab7d-c6105fbc2b8b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con dettagli sull’acquisizione del pubblico esterno.

+++ Una risposta di esempio durante il recupero dell’acquisizione del pubblico esterno.

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "status": "SUCCESS",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 3456788568,
    "createdAt": 1749324248,
    "createdBy": "{USER_ID}",
    "details": [
        {
            "stage": "DATASET_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        },
        {
            "stage": "PROFILE_STORE_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        }
    ]
}
```

| Proprietà | Tipo | Descrizione |
| -------- | ---- | ----------- |
| `audienceName` | Stringa | Il nome del pubblico. |
| `audienceId` | Stringa | ID del pubblico. |
| `runId` | Stringa | ID dell’esecuzione dell’acquisizione. |
| `status` | Stringa | Stato dell’esecuzione dell’acquisizione. Gli stati possibili includono `SUCCESS` e `FAILED`. |
| `differentialIngestion` | Booleano | Campo che determina se l’acquisizione è un’acquisizione parziale in base alla differenza rispetto all’ultima acquisizione o a un’acquisizione completa di pubblico. |
| `dataFilterStartTime` | Timestamp epoca | L’intervallo che specifica l’ora di inizio dell’esecuzione del flusso per selezionare i file elaborati. |
| `dataFilterEndTime` | Timestamp epoca | L’intervallo che specifica il tempo finale di esecuzione del flusso per selezionare i file elaborati. |
| `createdAt` | Timestamp dell’epoca lunga | La marca temporale, in secondi, di invio della richiesta di creazione del pubblico esterno. |
| `createdBy` | Stringa | ID dell’utente che ha creato il pubblico esterno. |
| `details` | Array di oggetti | Oggetto contenente i dettagli dell’esecuzione dell’acquisizione. <ul><li>`stage`: fase dell’esecuzione dell’acquisizione. Può essere `DATASET_INGEST` o `PROFILE_STORE_INGEST`, che rappresentano l’acquisizione del data lake e l’acquisizione del profilo.</li><li>`status`: stato dell’acquisizione nell’area di visualizzazione. Gli stati possibili includono `SUCCESS` e `FAILED`.</li><li>`flowRunId`: ID dell&#39;esecuzione del flusso di acquisizione della fase.</li></ul> |

+++

## Elencare gli stati di acquisizione del pubblico {#list-ingestion-statuses}

Per recuperare tutti gli stati di acquisizione per il pubblico esterno selezionato, effettua una richiesta GET al seguente endpoint e fornisci l’ID del pubblico. È possibile includere più parametri, separati da e commerciali (`&`).

**Formato API**

L’endpoint seguente supporta diversi parametri di query per aiutare a filtrare i risultati. Anche se questi parametri sono facoltativi, si consiglia vivamente di utilizzarli per rendere più mirati i risultati.

```http
GET /external-audience/{AUDIENCE_ID}/runs
GET /external-audience/{AUDIENCE_ID}/runs?{QUERY_PARAMETERS}
```

**Parametri query**

+++ Elenco dei parametri di query disponibili.

| Parametro | Descrizione | Esempio |
| --------- | ----------- | ------- |
| `limit` | Numero massimo di elementi restituiti nella risposta. Questo valore può essere compreso tra 1 e 40. Per impostazione predefinita, il limite è impostato su 20. | `limit=30` |
| `sortBy` | Ordine in cui vengono ordinati gli elementi restituiti. È possibile ordinare per `name` o per `ingestionTime`. Inoltre, puoi aggiungere un segno `-` per ordinare in base all&#39;ordine **discendente** invece che **ascendente**. Per impostazione predefinita, gli elementi sono ordinati per `ingestionTime` in ordine decrescente. | `sortBy=name` |
| `property` | Un filtro per determinare quali esecuzioni dell’acquisizione del pubblico vengono visualizzate. Puoi filtrare in base alle seguenti proprietà: <ul><li>`name`: consente di filtrare in base al nome del pubblico. Se si utilizza questa proprietà, è possibile eseguire il confronto utilizzando `=`, `!=`, `=contains` o `!=contains`. </li><li>`ingestionTime`: consente di filtrare in base al tempo di acquisizione. Se si utilizza questa proprietà, è possibile eseguire il confronto utilizzando `>=` o `<=`.</li><li>`status`: consente di filtrare in base allo stato dell’esecuzione dell’acquisizione. Se si utilizza questa proprietà, è possibile eseguire il confronto utilizzando `=`, `!=`, `=contains` o `!=contains`. </li></ul> | `property=ingestionTime<1683669114845`<br/>`property=name=demo_audience`<br/>`property=status=SUCCESS` |

+++

**Richiesta**

La richiesta seguente recupera tutti gli stati di acquisizione per il pubblico esterno.

+++ Una richiesta di esempio per ottenere un elenco degli stati di acquisizione del pubblico.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco degli stati di acquisizione per il pubblico esterno specificato.

+++ Una risposta di esempio quando recuperi un elenco degli stati di acquisizione del pubblico.

```json
{
    "runs": [
        {
            "audienceName": "Sample external audience",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1785678909,
            "createdBy": "{USER_NAME}",
            "details": [
                {
                    "stage": "DATASET_INGEST",
                    "status": "SUCCESS",
                    "flowRunId": "{FLOW_RUN_ID}"
                },
                {
                    "stage": "PROFILE_STORE_INGEST",
                    "status": "SUCCESS",
                    "flowRunId": "{FLOW_RUN_ID}"
                }
            ]
        },
        {
            "audienceName": "Sample external audience 2",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "406e38e4-fbd5-43e1-8d0c-01ccb3f9ad10",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1749324248,
            "createdBy": "{USER_ID}",
            "details": [
                {
                    "stage": "DATASET_INGEST",
                    "status": "SUCCESS",
                    "flowRunId": "{FLOW_RUN_ID}"
                },
                {
                    "stage": "PROFILE_STORE_INGEST",
                    "status": "SUCCESS",
                    "flowRunId": "{FLOW_RUN_ID}"
                }
            ]
        }
    ],
    "_page": {
        "limit": 20,
        "count": 2,
        "totalCount": 2
    }
}
```

| Proprietà | Tipo | Descrizione |
| -------- | ---- | ----------- |
| `runs` | Oggetto | Oggetto contenente l’elenco delle esecuzioni di acquisizione che appartiene al pubblico. Ulteriori informazioni su questo oggetto sono disponibili nella sezione [recupero stato acquisizione](#retrieve-ingestion-status). |
| `_page` | Oggetto | Oggetto contenente le informazioni di impaginazione relative all’elenco dei risultati. |

+++

## Eliminare un pubblico esterno {#delete-audience}

Per eliminare un pubblico esterno, effettua una richiesta DELETE al seguente endpoint e fornisci l’ID del pubblico.

**Formato API**

```http
DELETE /external-audience/{AUDIENCE_ID}
```

**Richiesta**

La richiesta seguente elimina il pubblico esterno specificato.

+++ Una richiesta di esempio per eliminare il pubblico esterno.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 con un corpo di risposta vuoto.

## Passaggi successivi {#next-steps}

Dopo aver letto questa guida, ora hai una migliore comprensione di come creare, gestire ed eliminare i tipi di pubblico esterni utilizzando le API di Experience Platform. Per informazioni su come utilizzare i tipi di pubblico esterni con l&#39;interfaccia utente di Experience Platform, consulta la [documentazione di Audience Portal](../ui/audience-portal.md).

## Appendice {#appendix}

Nella sezione seguente sono elencati i codici di errore disponibili quando si utilizza l’API per tipi di pubblico esterni.

| Codice errore piattaforma | Codice di stato | Messaggio | Descrizione |
| ------------------- | ----------- | ------- | ----------- |
| 100910-400 | 400 | `BAD_REQUEST` | Si è verificata una richiesta non valida a causa di un errore durante la convalida delle richieste. |
| 100911-400 | 400 | `BAD_REQUEST` | È stato fornito un token non valido. |
| 100920-401 | 401 | `UNAUTHORIZED` | Manca un’intestazione. |
| 100921-401 | 401 | `UNAUTHORIZED` | È stato fornito un `imsOrgId` non valido. |
| 100922-401 | 401 | `UNAUTHORIZED` | Non disponi dell’autorizzazione per utilizzare le API dei tipi di pubblico esterni. |
| 100940-404 | 404 | `NOT_FOUND` | Impossibile trovare il pubblico richiesto. |
| 100950-409 | 409 | `DUPLICATE_RESOURCE` | Il pubblico esiste già. |
| 100960-422 | 422 | `UNPROCESSABLE_ENTITY` | La struttura della richiesta è valida, ma non può essere elaborata a causa di errori logici o semantici. |
| 100970-500 | 500 | `INTERNAL_SERVER_ERROR` | Si è verificato un problema durante l’elaborazione della richiesta nel sistema. |
| 100970-502 | 502 | `BAD_GATEWAY` | Ci sono problemi di dipendenza a valle. |
