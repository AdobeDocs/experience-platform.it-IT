---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;
title: (Beta) Crea un’esecuzione di flusso per l’acquisizione on-demand tramite l’API del servizio di flusso
description: Questa esercitazione descrive i passaggi per creare un’esecuzione di flusso per l’acquisizione su richiesta tramite l’API del servizio di flusso
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: 659f99a47b533bba2a6084bc8e235df2a29a6386
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 1%

---

# (Beta) Crea un’esecuzione di flusso per l’acquisizione on-demand utilizzando [!DNL Flow Service] API

>[!IMPORTANT]
>
>L’acquisizione su richiesta è attualmente in versione beta e la tua organizzazione potrebbe non averne ancora accesso. La funzionalità descritta in questa documentazione è soggetta a modifiche.

Le esecuzioni del flusso rappresentano un&#39;istanza di esecuzione del flusso. Ad esempio, se un flusso viene pianificato per essere eseguito ogni ora alle 09:00, 10:00 e 11:00, si avranno tre istanze di un’esecuzione di flusso. Le esecuzioni dei flussi sono specifiche per la tua organizzazione specifica.

L’acquisizione su richiesta consente di creare un’esecuzione di flusso rispetto a un determinato flusso di dati. Questo consente agli utenti di creare un’esecuzione di flusso, in base a determinati parametri e di creare un ciclo di acquisizione, senza token di servizio.

Questa esercitazione descrive i passaggi per utilizzare l’acquisizione on-demand e creare un’esecuzione di flusso utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

>[!NOTE]
>
>Per creare un’esecuzione di flusso, devi prima disporre dell’ID di flusso di un flusso di dati pianificato per l’inserimento una tantum.

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../landing/api-guide.md).

## Creazione di un&#39;esecuzione di flusso per un&#39;origine basata su tabella

Per creare un flusso per un’origine basata su tabella, invia una richiesta POST al [!DNL Flow Service] API fornendo l’ID del flusso su cui desideri creare l’esecuzione, nonché i valori per l’ora di inizio, l’ora di fine e la colonna delta.

>[!TIP]
>
>Le origini basate su tabelle includono le seguenti categorie di origine: pubblicità, analisi, consenso e preferenze, CRM, successo cliente, database, automazione marketing, pagamenti e protocolli.

**Formato API**

```http
POST /runs/
```

**Richiesta**

La seguente richiesta crea un’esecuzione di flusso per l’ID di flusso `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

>[!NOTE]
>
>Devi solo fornire `deltaColumn` durante la creazione della prima esecuzione di flusso. Dopo questo, `deltaColumn` saranno patch come parte di `copy` trasformazione nel flusso e sarà trattato come la fonte della verità. Qualsiasi tentativo di modificare il `deltaColumn` attraverso i parametri di esecuzione del flusso si verifica un errore.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567",
          "deltaColumn": {
              "name": "DOB"
          }
      }
  }'
```

| Parametro | Descrizione |
| --- | --- |
| `flowId` | ID del flusso in cui verrà creata l&#39;esecuzione del flusso. |
| `params.windowStartTime` | Un numero intero che definisce l&#39;ora iniziale della finestra durante la quale i dati devono essere estratti. Il valore è rappresentato in tempo unix. |
| `params.windowEndTime` | Un numero intero che definisce l&#39;ora di fine della finestra durante la quale i dati devono essere estratti. Il valore è rappresentato in tempo unix. |
| `params.deltaColumn` | La colonna delta è necessaria per suddividere i dati e separare i dati appena acquisiti dai dati storici. |
| `params.deltaColumn.name` | Nome della colonna delta. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova esecuzione di flusso creata, inclusa la sua esecuzione univoca `id`.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "createdAt": 1651587212543,
    "updatedAt": 1651587223839,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "imsOrgId": "{ORGANIZATION_ID}",
    "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
    "params": {
        "windowStartTime": "1651584991",
        "windowEndTime": "16515859567",
        "deltaColumn": {
            "name": "DOB"
        }
    },
    "etag": "\"1100c53e-0000-0200-0000-627138980000\"",
    "metrics": {
        "statusSummary": {
            "status": "scheduled"
        }
    },
    "activities": []
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID della nuova esecuzione di flusso creata. Consulta la guida su [recupero delle specifiche di flusso](../api/collect/database-nosql.md#specs) per ulteriori informazioni sulle specifiche di esecuzione basate su tabelle. |
| `createdAt` | La marca temporale unix che indica quando è stata creata l’esecuzione del flusso. |
| `updatedAt` | La marca temporale unix che designa l’ultimo aggiornamento dell’esecuzione del flusso. |
| `createdBy` | ID organizzazione dell’utente che ha creato l’esecuzione di flusso. |
| `updatedBy` | ID organizzazione dell’utente che ha aggiornato l’ultima volta l’esecuzione del flusso. |
| `createdClient` | Client dell&#39;applicazione che ha creato l&#39;esecuzione del flusso. |
| `updatedClient` | Client dell&#39;applicazione che ha aggiornato l&#39;esecuzione del flusso per l&#39;ultima volta. |
| `sandboxId` | ID della sandbox che contiene l’esecuzione del flusso. |
| `sandboxName` | Nome della sandbox contenente l’esecuzione del flusso. |
| `imsOrgId` | ID organizzazione. |
| `flowId` | L&#39;ID del flusso in cui viene creata l&#39;esecuzione del flusso. |
| `params.windowStartTime` | Un numero intero che definisce l&#39;ora iniziale della finestra durante la quale i dati devono essere estratti. Il valore è rappresentato in tempo unix. |
| `params.windowEndTime` | Un numero intero che definisce l&#39;ora di fine della finestra durante la quale i dati devono essere estratti. Il valore è rappresentato in tempo unix. |
| `params.deltaColumn` | La colonna delta è necessaria per suddividere i dati e separare i dati appena acquisiti dai dati storici. **Nota**: La `deltaColumn` è necessario solo durante la creazione della prima esecuzione di flusso. |
| `params.deltaColumn.name` | Nome della colonna delta. |
| `etag` | Versione risorsa dell&#39;esecuzione del flusso. |
| `metrics` | Questa proprietà visualizza un riepilogo dello stato per l&#39;esecuzione del flusso. |

## Creazione di un&#39;esecuzione di flusso per un&#39;origine basata su file

Per creare un flusso per un’origine basata su file, invia una richiesta POST al [!DNL Flow Service] API fornendo l’ID del flusso con cui desideri creare i valori di esecuzione rispetto a e per l’ora di inizio e di fine.

>[!TIP]
>
>Le origini basate su file includono tutte le origini di archiviazione cloud.

**Formato API**

```http
POST /runs/
```

**Richiesta**

La seguente richiesta crea un’esecuzione di flusso per l’ID di flusso `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| Parametro | Descrizione |
| --- | --- |
| `flowId` | ID del flusso in cui verrà creata l&#39;esecuzione del flusso. |
| `params.windowStartTime` | Un numero intero che definisce l&#39;ora iniziale della finestra durante la quale i dati devono essere estratti. Il valore è rappresentato in tempo unix. |
| `params.windowEndTime` | Un numero intero che definisce l&#39;ora di fine della finestra durante la quale i dati devono essere estratti. Il valore è rappresentato in tempo unix. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova esecuzione di flusso creata, inclusa la sua esecuzione univoca `id`.


```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "createdAt": 1651587212543,
    "updatedAt": 1651587223839,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "imsOrgId": "{ORGANIZATION_ID}",
    "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
    "params": {
        "windowStartTime": "1651584991",
        "windowEndTime": "16515859567"
    },
    "etag": "\"1100c53e-0000-0200-0000-627138980000\"",
    "metrics": {
        "statusSummary": {
            "status": "scheduled"
        }
    },
    "activities": []
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID della nuova esecuzione di flusso creata. Consulta la guida su [recupero delle specifiche di flusso](../api/collect/cloud-storage.md#specs) per ulteriori informazioni sulle specifiche di esecuzione basate su file. |
| `createdAt` | La marca temporale unix che indica quando è stata creata l’esecuzione del flusso. |
| `updatedAt` | La marca temporale unix che designa l’ultimo aggiornamento dell’esecuzione del flusso. |
| `createdBy` | ID organizzazione dell’utente che ha creato l’esecuzione di flusso. |
| `updatedBy` | ID organizzazione dell’utente che ha aggiornato l’ultima volta l’esecuzione del flusso. |
| `createdClient` | Client dell&#39;applicazione che ha creato l&#39;esecuzione del flusso. |
| `updatedClient` | Client dell&#39;applicazione che ha aggiornato l&#39;esecuzione del flusso per l&#39;ultima volta. |
| `sandboxId` | ID della sandbox che contiene l’esecuzione del flusso. |
| `sandboxName` | Nome della sandbox contenente l’esecuzione del flusso. |
| `imsOrgId` | ID organizzazione. |
| `flowId` | L&#39;ID del flusso in cui viene creata l&#39;esecuzione del flusso. |
| `params.windowStartTime` | Un numero intero che definisce l&#39;ora iniziale della finestra durante la quale i dati devono essere estratti. Il valore è rappresentato in tempo unix. |
| `params.windowEndTime` | Un numero intero che definisce l&#39;ora di fine della finestra durante la quale i dati devono essere estratti. Il valore è rappresentato in tempo unix. |
| `etag` | Versione risorsa dell&#39;esecuzione del flusso. |
| `metrics` | Questa proprietà visualizza un riepilogo dello stato per l&#39;esecuzione del flusso. |


## Monitorare le esecuzioni dei flussi

Una volta creata l’esecuzione di flusso, puoi monitorare i dati che vengono acquisiti tramite di essa per visualizzare informazioni sulle esecuzioni di flusso, sullo stato di completamento e sugli errori. Per monitorare le esecuzioni di flusso utilizzando l’API, consulta l’esercitazione su [monitoraggio dei flussi di dati nell’API ](./monitor.md). Per monitorare le esecuzioni del flusso tramite l’interfaccia utente di Platform, consulta la guida su [monitoraggio dei flussi di dati delle origini tramite il dashboard di monitoraggio](../../../dataflows/ui/monitor-sources.md).
