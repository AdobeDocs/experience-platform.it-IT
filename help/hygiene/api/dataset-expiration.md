---
title: Endpoint API per la scadenza del set di dati
description: L’endpoint /ttl nell’API di igiene dati ti consente di pianificare programmaticamente la scadenza dei set di dati in Adobe Experience Platform.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 83149c4e6e8ea483133da4766c37886b8ebd7316
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 5%

---

# Endpoint di scadenza del set di dati

>[!IMPORTANT]
>
>Le funzionalità di igiene dei dati in Adobe Experience Platform sono attualmente disponibili solo per le organizzazioni che hanno acquistato Adobe Healthcare Shield.

La `/ttl` L’endpoint nell’API di igiene dati ti consente di pianificare le date di scadenza per i set di dati in Adobe Experience Platform.

La scadenza di un set di dati è solo un’operazione di eliminazione ritardata e temporizzata. Il set di dati non è protetto nel frattempo, pertanto può essere cancellato con altri mezzi prima che sia raggiunta la sua scadenza.

>[!NOTE]
>
>Anche se la scadenza è specificata come un momento specifico nel tempo, ci possono essere fino a 24 ore di ritardo dopo la scadenza prima dell&#39;avvio della cancellazione effettiva. Una volta avviata l’eliminazione, possono essere necessari fino a sette giorni prima che tutte le tracce del set di dati siano state rimosse dai sistemi Platform.

In qualsiasi momento prima dell’avvio dell’eliminazione del set di dati, puoi annullare la scadenza o modificarne il tempo di attivazione. Dopo aver annullato la scadenza di un set di dati, puoi riaprirlo impostando una nuova scadenza.

Una volta avviata l’eliminazione del set di dati, il relativo processo di scadenza verrà contrassegnato come `executing`e non può essere ulteriormente modificato. Il set di dati stesso può essere recuperabile per un massimo di sette giorni, ma solo tramite un processo manuale avviato tramite una richiesta di servizio Adobe. Durante l’esecuzione della richiesta, il data lake, il servizio Identity e il profilo cliente in tempo reale iniziano processi separati per rimuovere il contenuto del set di dati dai rispettivi servizi. Una volta eliminati i dati da tutti e tre i servizi, la scadenza è contrassegnata come `executed`.

>[!WARNING]
>
>Se un set di dati è impostato per la scadenza, devi modificare manualmente tutti i flussi di dati che potrebbero acquisire dati in tale set di dati in modo che i flussi di lavoro downstream non ne risentano.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’API di igiene dei dati. Prima di continuare, controlla la [panoramica](./overview.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e importanti informazioni sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Elencare le scadenze dei set di dati {#list}

Puoi elencare tutte le scadenze dei set di dati per la tua organizzazione effettuando una richiesta GET.

**Formato API**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUERY_PARAMETERS}` | Elenco di parametri di query facoltativi, con più parametri separati da `&` caratteri. I parametri comuni includono: `size` e `page` a scopo di impaginazione. Per un elenco completo dei parametri di query supportati, consulta [sezione appendice](#query-params). |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%Jane Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta elenca le scadenze risultanti del set di dati. L&#39;esempio seguente è stato troncato per lo spazio.

```json
{
  "totalRecords": 3,
  "ttlDetails": [
    {
      "status": "completed",
      "workorderId": "SDc17a9501345c4997878c1383c475a77b",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "f440ac301c414bf1b6ba419162866346",
      "expiry": "2021-07-07T13:14:15Z",
      "updatedAt": "2021-07-07T13:14:15Z",
      "updatedBy": "Jane Doe <jane.doe@example.com> d741b5b877bf47cf@AdobeId"
    },
    {
      "status": "pending",
      "workorderId": "SD8ef60b33dbed444fb81861cced5da10b",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "80f0d38820a74879a2c5be82e38b1a94",
      "expiry": "2099-02-02T00:00:00Z",
      "updatedAt": "2021-02-02T13:00:00Z",
      "updatedBy": "John Q. Public <jqp@example.com> 93220281bad34ed0@AdobeId"
    },
    {
      "status": "pending",
      "workorderId": "SD2140ad4eaf1f47a1b24c05cce53e303e",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "9e63f9b25896416ba811657678b4fcb7",
      "expiry": "2099-01-01T00:00:00Z",
      "updatedAt": "2021-01-01T13:00:00Z",
      "updatedBy": "Jane Doe <jane.doe@example.com> d741b5b877bf47cf@AdobeId"
    }
  ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `totalRecords` | Il numero di scadenze del set di dati che corrispondono ai parametri della chiamata di elenco. |
| `ttlDetails` | Contiene i dettagli delle scadenze del set di dati restituito. Per ulteriori dettagli sulle proprietà della scadenza di un set di dati, consulta la sezione relativa alla risposta per creare un [chiamata di ricerca](#lookup). |

{style=&quot;table-layout:auto&quot;}

## Cercare la scadenza di un set di dati {#lookup}

Puoi cercare la scadenza di un set di dati tramite una richiesta GET.

**Formato API**

```http
GET /ttl/{DATASET_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | ID del set di dati di cui vuoi cercare la scadenza. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La seguente richiesta cerca i dettagli di scadenza del set di dati `62759f2ede9e601b63a2ee14`:

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli della scadenza del set di dati.

```json
{
    "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}",
    "displayName": "Example Dataset Expiration Request",
    "description": "A dataset expiration request that will execute at the end of 2023"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `workorderId` | ID della scadenza del set di dati. |
| `datasetId` | ID del set di dati a cui si applica questa scadenza. |
| `imsOrg` | L&#39;ID della tua organizzazione. |
| `status` | Lo stato corrente della scadenza del set di dati. |
| `expiry` | Data e ora pianificate in cui il set di dati verrà eliminato. |
| `updatedAt` | Una marca temporale dell’ultimo aggiornamento della scadenza. |
| `updatedBy` | L’ultimo utente che ha aggiornato la scadenza. |
| `displayName` | Nome visualizzato della richiesta di scadenza. |
| `description` | Una descrizione della richiesta di scadenza. |

{style=&quot;table-layout:auto&quot;}

### Tag di scadenza del catalogo

Quando utilizzi [API del catalogo](../../catalog/api/getting-started.md) per cercare i dettagli del set di dati, se il set di dati ha una scadenza attiva, verrà elencato in `tags.adobe/hygiene/ttl`.

Il seguente JSON rappresenta una risposta troncata per i dettagli di un set di dati da Catalog, che rappresenta un valore di scadenza di `32503680000000`. Il valore del tag codifica la scadenza come numero intero di millisecondi dall&#39;inizio dell&#39;epoch Unix.

```json
{
  "63212313c308d51b997858ba": {
    "name": "TTL Test Dataset",
    "description": "A piecrust promise, made to be broken",
    "imsOrg": "0FCC747E56F59C747F000101@AdobeOrg",
    "sandboxId": "8dc51b90-d0f9-11e9-b164-ed6a398c8b35",
    "tags": {
      "adobe/hygiene/ttl": [ "32503680000000" ],
      ...
    },
    ...
  }
}
```

## Creare o aggiornare una scadenza di un set di dati {#create-or-update}

Puoi creare o aggiornare una data di scadenza per un set di dati tramite una richiesta di PUT.

**Formato API**

```http
PUT /ttl/{DATASET_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | ID del set di dati per il quale vuoi pianificare una scadenza. |

**Richiesta**

La seguente richiesta pianifica un set di dati `5b020a27e7040801dedbf46e` per la cancellazione alla fine del 2022 (Greenwich Mean Time). Se non viene trovata alcuna scadenza esistente per il set di dati, viene creata una nuova scadenza. Se il set di dati ha già una scadenza in sospeso, tale scadenza viene aggiornata con la nuova `expiry` valore.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2022-12-31T23:59:59Z",
        "displayName": "Example Expiration Request",
        "description": "Cleanup identities required by JIRA request 12345 across all datasets in the prod sandbox."
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `expiry` | Timestamp ISO 8601 per quando il set di dati verrà eliminato. |
| `displayName` | Un nome visualizzato per la richiesta di scadenza. |
| `description` | Una descrizione facoltativa per la richiesta di scadenza. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli della scadenza del set di dati, con stato HTTP 200 (OK) se è stata aggiornata una scadenza preesistente, o 201 (Creata) se non c&#39;è stata una scadenza preesistente.

```json
{
    "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2032-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "{USER_ID}",
    "displayName": "Example Expiration Request",
    "description": "Cleanup identities required by JIRA request 12345 across all datasets in the prod sandbox."
}
```

| Proprietà | Descrizione |
| --- | --- |
| `workorderId` | ID della scadenza del set di dati. |
| `datasetId` | ID del set di dati a cui si applica questa scadenza. |
| `imsOrg` | L&#39;ID della tua organizzazione. |
| `status` | Lo stato corrente della scadenza del set di dati. |
| `expiry` | Data e ora pianificate in cui il set di dati verrà eliminato. |
| `updatedAt` | Una marca temporale dell’ultimo aggiornamento della scadenza. |
| `updatedBy` | L’ultimo utente che ha aggiornato la scadenza. |

{style=&quot;table-layout:auto&quot;}

## Annullare la scadenza di un set di dati {#delete}

Puoi annullare la scadenza di un set di dati effettuando una richiesta DELETE.

>[!NOTE]
>
>Solo le scadenze del set di dati con uno stato `pending` può essere annullato. Il tentativo di annullare una scadenza eseguita o già annullata restituisce un errore HTTP 404.

**Formato API**

```http
DELETE /ttl/{EXPIRATION_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{EXPIRATION_ID}` | La `workorderId` della scadenza del set di dati che si desidera annullare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La seguente richiesta annulla la scadenza di un set di dati con ID `SD5cfd7a11b25543a9bcd9ef647db3d8df`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD5cfd7a11b25543a9bcd9ef647db3d8df \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (nessun contenuto) e la `status` attributo impostato su `cancelled`.

## Recupera la cronologia dello stato di scadenza di un set di dati

Puoi cercare la cronologia dello stato di scadenza di un set di dati specifico utilizzando il parametro di query `include=history` in una richiesta di ricerca. Il risultato include informazioni sulla creazione della scadenza del set di dati, sugli eventuali aggiornamenti applicati e sulla relativa cancellazione o esecuzione (se applicabile).

**Formato API**

```http
GET /ttl/{DATASET_ID}?include=history
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | ID del set di dati di cui vuoi cercare la cronologia di scadenza. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14?include=history \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli della scadenza del set di dati, con un `history` array che fornisce i dettagli `status`, `expiry`, `updatedAt`e `updatedBy` per ciascuno dei relativi aggiornamenti registrati.

```json
{
  "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
  "datasetId": "62759f2ede9e601b63a2ee14",
  "datasetName": "Example Dataset",
  "sandboxName": "prod",
  "displayName": "Expiration Request 123",
  "description": "Expiration Request 123 Description",
  "imsOrg": "{ORG_ID}",
  "status": "cancelled",
  "expiry": "2022-05-09T23:47:30.071186Z",
  "updatedAt": "2022-05-09T23:47:30.071186Z",
  "updatedBy": "{USER_ID}",
  "history": [
    {
      "status": "created",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:38:40.393115Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "updated",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "cancelled",
      "expiry": "2022-05-09T23:47:30.071186Z",
      "updatedAt": "2022-05-09T23:47:30.071186Z",
      "updatedBy": "{USER_ID}"
    }
  ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `workorderId` | ID della scadenza del set di dati. |
| `datasetId` | ID del set di dati a cui si applica questa scadenza. |
| `datasetName` | Nome visualizzato del set di dati a cui si applica questa scadenza. |
| `sandboxName` | Il nome della sandbox in cui si trova il set di dati di destinazione. |
| `displayName` | Nome visualizzato della richiesta di scadenza. |
| `description` | Una descrizione della richiesta di scadenza. |
| `imsOrg` | L&#39;ID della tua organizzazione. |
| `history` | Elenca la cronologia degli aggiornamenti per la scadenza come array di oggetti, con ogni oggetto contenente la `status`, `expiry`, `updatedAt`e `updatedBy` alla scadenza dell’aggiornamento. |

{style=&quot;table-layout:auto&quot;}

## Appendice

### Parametri di query accettati {#query-params}

La tabella seguente delinea i parametri di query disponibili quando [elenco delle scadenze dei set di dati](#list):

| Parametro | Descrizione | Esempio |
| --- | --- | --- |
| `size` | Un numero intero compreso tra 1 e 100 che indica il numero massimo di scadenze da restituire. Il valore predefinito è 25. | `size=50` |
| `page` | Un numero intero che indica la pagina di scadenza da restituire. | `page=3` |
| `orgId` | Corrisponde alle scadenze dei set di dati il cui ID organizzazione corrisponde a quello del parametro . Il valore predefinito è quello del `x-gw-ims-org-id` Le intestazioni e vengono ignorate a meno che la richiesta non fornisca un token di servizio. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `status` | Elenco di stati separati da virgole. Quando è inclusa, la risposta corrisponde alle scadenze del set di dati il cui stato corrente è tra quelli elencati. | `status=pending,cancelled` |
| `author` | Corrisponde alle scadenze di cui `created_by` è una corrispondenza per la stringa di ricerca. Se la stringa di ricerca inizia con `LIKE` o `NOT LIKE`, il resto viene trattato come un pattern di ricerca SQL. In caso contrario, l’intera stringa di ricerca viene trattata come una stringa letterale che deve corrispondere esattamente all’intero contenuto di un `created_by` campo . | `author=LIKE %john%` |
| `sandboxName` | Corrisponde alle scadenze del set di dati il cui nome sandbox corrisponde esattamente all’argomento . Impostazione predefinita del nome della sandbox nel `x-sandbox-name` intestazione. Utilizzo `sandboxName=*` per includere le scadenze dei set di dati da tutte le sandbox. | `sandboxName=dev1` |
| `datasetId` | Corrisponde alle scadenze applicabili a un set di dati specifico. | `datasetId=62b3925ff20f8e1b990a7434` |
| `createdDate` | Corrisponde alle scadenze create nella finestra di 24 ore a partire dall&#39;ora indicata.<br><br>Tieni presente che le date non hanno un&#39;ora (come `2021-12-07`) rappresenta il datetime all&#39;inizio di quel giorno. Pertanto, `createdDate=2021-12-07` si riferisce a qualsiasi scadenza creata il 7 dicembre 2021, a partire da `00:00:00` attraverso `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Corrisponde alle scadenze create al momento o dopo l’ora indicata. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Corrisponde alle scadenze create al momento indicato o prima. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Simile `createdDate` / `createdFromDate` / `createdToDate`, ma corrisponde al tempo di aggiornamento della scadenza di un set di dati anziché al tempo di creazione.<br><br>Una scadenza viene considerata aggiornata a ogni modifica, anche quando viene creata, annullata o eseguita. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Corrisponde alle scadenze che sono state annullate in qualsiasi momento nell&#39;intervallo indicato. Ciò si applica anche se la scadenza è stata successivamente riaperta (impostando una nuova scadenza per lo stesso set di dati). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Corrisponde alle scadenze completate durante l&#39;intervallo specificato. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Corrisponde alle scadenze che devono essere eseguite o sono già state eseguite nell&#39;intervallo specificato. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
