---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;
title: Creare un’esecuzione del flusso per l’acquisizione su richiesta utilizzando l’API del servizio Flusso
description: Scopri come creare un’esecuzione del flusso per l’acquisizione on-demand utilizzando l’API del servizio Flusso
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: 5aefa362d7a7d93c12f9997d56311127e548497e
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 2%

---

# Creare un&#39;esecuzione di flusso per l&#39;acquisizione su richiesta utilizzando l&#39;API [!DNL Flow Service]

Le esecuzioni del flusso rappresentano un’istanza dell’esecuzione del flusso. Ad esempio, se un flusso è pianificato per essere eseguito ogni ora alle 9:00, alle 10:00 e alle 11:00, sono disponibili tre istanze di un flusso. Le esecuzioni del flusso sono specifiche per la tua particolare organizzazione.

L’acquisizione su richiesta consente di creare un flusso eseguito su un determinato flusso di dati. Questo consente agli utenti di creare un’esecuzione del flusso, basata su parametri specifici, e un ciclo di acquisizione, senza token di servizio. Il supporto per l’acquisizione su richiesta è disponibile solo per le origini batch.

Questo tutorial illustra i passaggi per utilizzare l&#39;acquisizione su richiesta e creare un&#39;esecuzione del flusso utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

>[!NOTE]
>
>Per creare un’esecuzione del flusso, devi innanzitutto disporre dell’ID di flusso di un flusso di dati pianificato per l’acquisizione una tantum.

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../landing/api-guide.md).

## Creare un&#39;esecuzione di flusso per un&#39;origine basata su tabella

Per creare un flusso per un&#39;origine basata su tabella, eseguire una richiesta POST all&#39;API [!DNL Flow Service] fornendo l&#39;ID del flusso su cui si desidera creare l&#39;esecuzione, nonché i valori per l&#39;ora di inizio, l&#39;ora di fine e la colonna delta.

>[!TIP]
>
>Le origini basate su tabelle includono le seguenti categorie di origini: pubblicità, analisi, consenso e preferenze, CRM, successo del cliente, database, automazione marketing, pagamenti e protocolli.

**Formato API**

```http
POST /runs/
```

**Richiesta**

La richiesta seguente crea un&#39;esecuzione di flusso per l&#39;ID di flusso `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

>[!NOTE]
>
>È necessario fornire `deltaColumn` solo quando si crea la prima esecuzione del flusso. In seguito, `deltaColumn` riceverà la patch come parte della trasformazione `copy` nel flusso e verrà trattato come l&#39;origine della verità. Eventuali tentativi di modificare il valore `deltaColumn` tramite i parametri di esecuzione del flusso genereranno un errore.

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
          "startTime": "1663735590",
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
| `flowId` | ID del flusso su cui verrà creata l’esecuzione del flusso. |
| `params.startTime` | L’ora programmata di inizio dell’esecuzione del flusso su richiesta. Questo valore è rappresentato nel tempo unix. |
| `params.windowStartTime` | La prima data e ora da cui verranno recuperati i dati. Questo valore è rappresentato nel tempo unix. |
| `params.windowEndTime` | La data e l’ora in cui i dati verranno recuperati. Questo valore è rappresentato nel tempo unix. |
| `params.deltaColumn` | La colonna delta è necessaria per partizionare i dati e separare i dati appena acquisiti da quelli storici. **Nota**: `deltaColumn` è necessario solo durante la creazione della prima esecuzione del flusso. |
| `params.deltaColumn.name` | Nome della colonna delta. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della nuova esecuzione di flusso creata, inclusa l&#39;esecuzione univoca `id`.

```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID dell’esecuzione del flusso appena creata. Per ulteriori informazioni sulle specifiche di esecuzione basate su tabelle, vedere la guida al [recupero delle specifiche di flusso](../api/collect/database-nosql.md#specs). |
| `etag` | Versione risorsa dell’esecuzione del flusso. |

<!-- 
| `createdAt` | The unix timestamp that designates when the flow run was created. |
| `updatedAt` | The unix timestamp that designates when the flow run was last updated. |
| `createdBy` | The organization ID of the user who created the flow run. |
| `updatedBy` | The organization ID of the user who last updated the flow run. |
| `createdClient` | The application client that created the flow run. |
| `updatedClient` | The application client that last updated the flow run. |
| `sandboxId` | The ID of the sandbox that contains the flow run. |
| `sandboxName` | The name of the sandbox that contains the flow run. |
| `imsOrgId` | The organization ID. |
| `flowId` | The ID of the flow in which the flow run is created against. |
| `params.windowStartTime` | An integer that defines the start time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.windowEndTime` | An integer that defines the end time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.deltaColumn` | The delta column is required to partition the data and separate newly ingested data from historic data. **Note**: The `deltaColumn` is only needed when creating your firs flow run. |
| `params.deltaColumn.name` | The name of the delta column. |
| `etag` | The resource version of the flow run. |
| `metrics` | This property displays a status summary for the flow run. | -->

## Creare un&#39;esecuzione di flusso per un&#39;origine basata su file

Per creare un flusso per un&#39;origine basata su file, effettuare una richiesta POST all&#39;API [!DNL Flow Service] fornendo l&#39;ID del flusso su cui si desidera creare i valori e per l&#39;ora di inizio e di fine.

>[!TIP]
>
>Le origini basate su file includono tutte le origini di archiviazione cloud.

**Formato API**

```http
POST /runs/
```

**Richiesta**

La richiesta seguente crea un&#39;esecuzione di flusso per l&#39;ID di flusso `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

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
          "startTime": "1663735590",
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| Parametro | Descrizione |
| --- | --- |
| `flowId` | ID del flusso su cui verrà creata l’esecuzione del flusso. |
| `params.startTime` | L’ora programmata di inizio dell’esecuzione del flusso su richiesta. Questo valore è rappresentato nel tempo unix. |
| `params.windowStartTime` | La prima data e ora da cui verranno recuperati i dati. Questo valore è rappresentato nel tempo unix. |
| `params.windowEndTime` | La data e l’ora in cui i dati verranno recuperati. Questo valore è rappresentato nel tempo unix. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della nuova esecuzione di flusso creata, inclusa l&#39;esecuzione univoca `id`.


```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID dell’esecuzione del flusso appena creata. Per ulteriori informazioni sulle specifiche di esecuzione basate su tabelle, vedere la guida al [recupero delle specifiche di flusso](../api/collect/database-nosql.md#specs). |
| `etag` | Versione risorsa dell’esecuzione del flusso. |

## Monitorare le esecuzioni del flusso

Una volta creata l’esecuzione del flusso, puoi monitorare i dati che vengono acquisiti tramite di essa per visualizzare informazioni sulle esecuzioni del flusso, sullo stato di completamento e sugli errori. Per monitorare il flusso eseguito utilizzando l&#39;API, consulta l&#39;esercitazione sul [monitoraggio dei flussi di dati nell&#39;API](./monitor.md). Per monitorare le esecuzioni del flusso tramite l&#39;interfaccia utente di Platform, consulta la guida su [flussi di dati di origine monitoraggio tramite il dashboard di monitoraggio](../../../dataflows/ui/monitor-sources.md).
