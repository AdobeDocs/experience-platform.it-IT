---
title: Endpoint API di scadenza set di dati
description: L’endpoint /ttl nell’API di igiene dei dati consente di pianificare in modo programmatico le scadenze dei set di dati in Adobe Experience Platform.
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 2%

---

# Endpoint di scadenza del set di dati

Il `/ttl` L’endpoint nell’API di igiene dei dati consente di pianificare le date di scadenza dei set di dati in Adobe Experience Platform.

La scadenza di un set di dati è solo un’operazione di eliminazione ritardata nel tempo. Il set di dati non è protetto nel frattempo, pertanto può essere cancellato con altri mezzi prima che sia raggiunta la sua scadenza.

>[!NOTE]
>
>Sebbene la scadenza sia specificata come un momento specifico nel tempo, possono trascorrere fino a 24 ore dalla scadenza prima che venga avviata l’effettiva cancellazione. Una volta avviata l’eliminazione, possono essere necessari fino a sette giorni prima che tutte le tracce del set di dati siano state rimosse dai sistemi Platform.

In qualsiasi momento, prima che l’eliminazione del set di dati venga effettivamente avviata, puoi annullare la scadenza o modificarne l’ora di attivazione. Dopo aver annullato la scadenza di un set di dati, puoi riaprirlo impostando una nuova scadenza.

Una volta avviata l’eliminazione del set di dati, il relativo processo di scadenza verrà contrassegnato come `executing`e non può essere ulteriormente modificata. Il set di dati può essere recuperato per un massimo di sette giorni, ma solo tramite un processo manuale avviato tramite una richiesta di servizio Adobe. Durante l’esecuzione della richiesta, il data lake, Identity Service e Real-Time Customer Profile avviano processi separati per rimuovere i contenuti del set di dati dai rispettivi servizi. Una volta eliminati i dati da tutti e tre i servizi, la scadenza viene contrassegnata come `executed`.

>[!WARNING]
>
>Se un set di dati è impostato per la scadenza, è necessario modificare manualmente i flussi di dati che potrebbero acquisire dati in tale set di dati in modo che i flussi di lavoro a valle non vengano influenzati negativamente.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’API di igiene dei dati. Prima di continuare, controlla [Guida API](./overview.md) per informazioni sulle intestazioni richieste per operazioni CRUD, messaggi di errore, raccolte Postman e come leggere chiamate API di esempio.

>[!IMPORTANT]
>
>Quando effettui chiamate all’API di igiene dei dati, devi utilizzare il comando -H `x-sandbox-name: {SANDBOX_NAME}` intestazione.

## Elenca scadenze set di dati {#list}

Per elencare tutte le scadenze dei set di dati per la tua organizzazione, devi eseguire una richiesta GET. I parametri di query possono essere utilizzati per filtrare la risposta in base ai risultati appropriati.

**Formato API**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUERY_PARAMETERS}` | Elenco di parametri di query facoltativi, con più parametri separati da `&` caratteri. I parametri comuni includono `limit` e `page` a scopo di impaginazione. Per un elenco completo dei parametri di query supportati, consulta [sezione dell&#39;appendice](#query-params). |

{style="table-layout:auto"}

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

In caso di esito positivo, la risposta elenca le scadenze risultanti del set di dati. L&#39;esempio seguente è stato troncato per motivi di spazio.

```json
{
  "results": [
    {
      "ttlId": "SD-b16c8b48-a15a-45c8-9215-587ea89369bf",
      "datasetId": "629bd9125b31471b2da7645c",
      "datasetName": "Sample Acme dataset",
      "sandboxName": "hygiene-beta",
      "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
      "status": "pending",
      "expiry": "2050-01-01T00:00:00Z",
      "updatedAt": "2023-06-09T16:52:44.136028Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| Proprietà | Descrizione |
| --- | --- |
| `totalRecords` | Il conteggio delle scadenze del set di dati che corrispondono ai parametri della chiamata di elenco. |
| `ttlDetails` | Contiene i dettagli delle scadenze dei set di dati restituiti. Per ulteriori dettagli sulle proprietà di scadenza di un set di dati, consulta la sezione della risposta per creare un [chiamata di ricerca](#lookup). |

{style="table-layout:auto"}

## Cercare una scadenza del set di dati {#lookup}

Per cercare la scadenza di un set di dati, effettua una richiesta GET con `datasetId` o `ttlId`.

**Formato API**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{TTL_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | ID del set di dati di cui desideri cercare la scadenza. |
| `{TTL_ID}` | ID della scadenza del set di dati. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente cerca i dettagli di scadenza per il set di dati `62759f2ede9e601b63a2ee14`:

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della scadenza del set di dati.

<!-- Is there a different response from making a GET request to either '/ttl/{DATASET_ID}?include=history' or '/ttl/{TTL_ID}'? If so please can you provide the response for both (or just the ttl endpoint itf it differs from teh example) -->

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "datasetName": "XtVRwq9-38734",
    "sandboxName": "prod",
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2024-05-11T15:12:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| Proprietà | Descrizione |
| --- | --- |
| `ttlId` | ID della scadenza del set di dati. |
| `datasetId` | ID del set di dati a cui si applica questa scadenza. |
| `datasetName` | Nome visualizzato del set di dati a cui si applica questa scadenza. |
| `sandboxName` | Il nome della sandbox in cui si trova il set di dati di destinazione. |
| `imsOrg` | ID organizzazione. |
| `status` | Lo stato corrente della scadenza del set di dati. |
| `expiry` | La data e l’ora pianificate in cui il set di dati verrà eliminato. |
| `updatedAt` | Timestamp dell’ultimo aggiornamento della scadenza. |
| `updatedBy` | L’ultimo utente che ha aggiornato la scadenza. |
| `displayName` | Nome visualizzato della richiesta di scadenza. |
| `description` | Descrizione della richiesta di scadenza. |

{style="table-layout:auto"}

### Tag di scadenza del catalogo

Quando si utilizza [API catalogo](../../catalog/api/getting-started.md) per cercare i dettagli del set di dati, se il set di dati ha una scadenza attiva verrà elencato in `tags.adobe/hygiene/ttl`.

Il seguente JSON rappresenta una risposta troncata per i dettagli di un set di dati dal catalogo, che un valore di scadenza di `32503680000000`. Il valore del tag codifica la scadenza come numero intero di millisecondi dall’inizio dell’epoca Unix.

```json
{
  "63212313c308d51b997858ba": {
    "name": "Test Dataset",
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

## Creare o aggiornare la scadenza di un set di dati {#create-or-update}

Crea o aggiorna una data di scadenza per un set di dati tramite una richiesta PUT. La richiesta PUT utilizza `datasetId` o `ttlId`.

**Formato API**

```http
PUT /ttl/{DATASET_ID}
PUT /ttl/{TTL_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | ID del set di dati per cui pianificare una scadenza. |
| `{TTL_ID}` | ID della scadenza del set di dati. |

**Richiesta**

La richiesta seguente pianifica un set di dati `5b020a27e7040801dedbf46e` da sopprimere alla fine del 2022 (ora di Greenwich). Se non viene trovata alcuna scadenza esistente per il set di dati, viene creata una nuova scadenza. Se il set di dati ha già una scadenza in sospeso, tale scadenza viene aggiornata con il nuovo `expiry` valore.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2024-12-31T23:59:59Z",
        "displayName": "Delete Acme Data before 2025",
        "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `expiry` | Data e ora nel formato ISO 8601. Se la stringa non presenta scostamenti di fuso orario espliciti, si presume che il fuso orario sia UTC. La durata dei dati all’interno del sistema viene impostata in base al valore di scadenza fornito. Eventuali marche temporali di scadenza precedenti per lo stesso set di dati vengono sostituite dal nuovo valore di scadenza fornito. |
| `displayName` | Nome visualizzato per la richiesta di scadenza. |
| `description` | Descrizione facoltativa della richiesta di scadenza. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della scadenza del set di dati, con lo stato HTTP 200 (OK) se è stata aggiornata una scadenza preesistente, oppure 201 (Creato) se non vi era alcuna scadenza preesistente.

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| Proprietà | Descrizione |
| --- | --- |
| `ttlId` | ID della scadenza del set di dati. |
| `datasetId` | ID del set di dati a cui si applica questa scadenza. |
| `imsOrg` | ID organizzazione. |
| `status` | Lo stato corrente della scadenza del set di dati. |
| `expiry` | La data e l’ora pianificate in cui il set di dati verrà eliminato. |
| `updatedAt` | Timestamp dell’ultimo aggiornamento della scadenza. |
| `updatedBy` | L’ultimo utente che ha aggiornato la scadenza. |

{style="table-layout:auto"}

## Annullare la scadenza di un set di dati {#delete}

Per annullare la scadenza di un set di dati, devi eseguire una richiesta DELETE.

>[!NOTE]
>
>Solo le scadenze dei set di dati con stato `pending` può essere annullato. Se si tenta di annullare una scadenza già annullata o eseguita, viene restituito un errore HTTP 404.

**Formato API**

```http
DELETE /ttl/{EXPIRATION_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{EXPIRATION_ID}` | Il `ttlId` della scadenza del set di dati che desideri annullare. |

{style="table-layout:auto"}

**Richiesta**

La seguente richiesta annulla la scadenza di un set di dati con ID `SD-b16c8b48-a15a-45c8-9215-587ea89369bf`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-b16c8b48-a15a-45c8-9215-587ea89369bf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto) e il campo `status` attributo impostato su `cancelled`.

## Recuperare la cronologia dello stato di scadenza di un set di dati {#retrieve-expiration-history}

Puoi cercare la cronologia dello stato di scadenza di un set di dati specifico utilizzando il parametro di query `include=history` in una richiesta di ricerca. Il risultato include informazioni sulla creazione della scadenza del set di dati, su eventuali aggiornamenti applicati e sulla relativa cancellazione o esecuzione (se applicabile). È inoltre possibile utilizzare `ttlId` della scadenza del set di dati.

**Formato API**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{TTL_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | ID del set di dati di cui desideri cercare la cronologia delle scadenze. |
| `{TTL_ID}` | ID della scadenza del set di dati. |

{style="table-layout:auto"}

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

Una risposta corretta restituisce i dettagli della scadenza del set di dati, con un `history` array che fornisce i dettagli relativi ai `status`, `expiry`, `updatedAt`, e `updatedBy` attributi per ciascuno degli aggiornamenti registrati.

```json
{
  "ttlId": "SD-b16c8b48-a15a-45c8-9215-587ea89369bf",
  "datasetId": "62759f2ede9e601b63a2ee14",
  "datasetName": "Example Dataset",
  "sandboxName": "prod",
  "displayName": "Expiration Request 123",
  "description": "Expiration Request 123 Description",
  "imsOrg": "0FCC747E56F59C747F000101@AdobeOrg",
  "status": "cancelled",
  "expiry": "2022-05-09T23:47:30.071186Z",
  "updatedAt": "2022-05-09T23:47:30.071186Z",
  "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
  "history": [
    {
      "status": "created",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:38:40.393115Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    },
    {
      "status": "updated",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    },
    {
      "status": "cancelled",
      "expiry": "2022-05-09T23:47:30.071186Z",
      "updatedAt": "2022-05-09T23:47:30.071186Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    }
  ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `ttlId` | ID della scadenza del set di dati. |
| `datasetId` | ID del set di dati a cui si applica questa scadenza. |
| `datasetName` | Nome visualizzato del set di dati a cui si applica questa scadenza. |
| `sandboxName` | Il nome della sandbox in cui si trova il set di dati di destinazione. |
| `displayName` | Nome visualizzato della richiesta di scadenza. |
| `description` | Descrizione della richiesta di scadenza. |
| `imsOrg` | ID organizzazione. |
| `history` | Elenca la cronologia degli aggiornamenti per la scadenza sotto forma di array di oggetti, con ogni oggetto contenente `status`, `expiry`, `updatedAt`, e `updatedBy` attributi per la scadenza al momento dell’aggiornamento. |

{style="table-layout:auto"}

## Appendice

### Parametri di query accettati {#query-params}

La tabella seguente illustra i parametri di query disponibili quando [elenco scadenze set di dati](#list):

>[!NOTE]
>
>Il `description`, `displayName`, e `datasetName` Tutti i parametri contengono la possibilità di cercare per valori LIKE. Ciò significa che puoi trovare le scadenze pianificate del set di dati denominate: &quot;Name123&quot;, &quot;Name183&quot;, &quot;DisplayName1234&quot; cercando la stringa &quot;Name1&quot;.

| Parametro | Descrizione | Esempio |
| --- | --- | --- |
| `author` | Corrisponde a scadenze il cui `created_by` corrisponde alla stringa di ricerca. Se la stringa di ricerca inizia con `LIKE` o `NOT LIKE`, il resto viene trattato come un modello di ricerca SQL. In caso contrario, l’intera stringa di ricerca viene trattata come una stringa letterale che deve corrispondere esattamente all’intero contenuto di una `created_by` campo. | `author=LIKE %john%`, `author=John Q. Public` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Corrisponde alle scadenze annullate in qualsiasi momento nell’intervallo indicato. Ciò si applica anche se la scadenza è stata successivamente riaperta (impostando una nuova scadenza per lo stesso set di dati). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Corrisponde alle scadenze completate durante l’intervallo specificato. | `completedToDate=2021-11-11-06:00` |
| `createdDate` | Corrisponde alle scadenze create nell’intervallo di 24 ore a partire dall’ora indicata.<br><br>Tieni presente che le date senza un’ora (come `2021-12-07`) rappresentano il datetime all&#39;inizio di tale giorno. Pertanto, `createdDate=2021-12-07` si riferisce a qualsiasi scadenza creata il 7 dicembre 2021, a partire da `00:00:00` da a `23:59:59.999999999` (UTC) | `createdDate=2021-12-07` |
| `createdFromDate` | Corrisponde alle scadenze create all’ora indicata o successivamente. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Corrisponde alle scadenze create entro l’ora indicata o prima di essa. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `datasetId` | Corrisponde alle scadenze che si applicano a un set di dati specifico. | `datasetId=62b3925ff20f8e1b990a7434` |
| `datasetName` | Corrisponde a scadenze il cui nome del set di dati contiene la stringa di ricerca fornita. La corrispondenza non distingue tra maiuscole e minuscole. | `datasetName=Acme` |
| `description` |   | `description=Handle expiration of Acme information through the end of 2024.` |
| `displayName` | Corrisponde a scadenze il cui nome visualizzato contiene la stringa di ricerca fornita. La corrispondenza non distingue tra maiuscole e minuscole. | `displayName=License Expiry` |
| `executedDate` / `executedFromDate` / `executedToDate` | Filtra i risultati in base a una data di esecuzione esatta, una data di fine per l’esecuzione o una data di inizio per l’esecuzione. Vengono utilizzati per recuperare dati o record associati all&#39;esecuzione di un&#39;operazione in una data specifica, prima di una data specifica o dopo una data specifica. | `executedDate=2023-02-05T19:34:40.383615Z` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Corrisponde alle scadenze che devono essere eseguite, o che sono già state eseguite, durante l’intervallo specificato. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |
| `limit` | Un numero intero compreso tra 1 e 100 che indica il numero massimo di scadenze da restituire. Impostazione predefinita: 25. | `limit=50` |
| `orderBy` | Il `orderBy` Il parametro query specifica l’ordinamento dei risultati restituiti dall’API. Utilizzalo per disporre i dati in base a uno o più campi, in ordine crescente (ASC) o decrescente (DESC). Utilizzare il prefisso + o - per indicare rispettivamente ASC e DESC. Sono accettati i seguenti valori: `displayName`, `description`, `datasetName`, `id`, `updatedBy`, `updatedAt`, `expiry`, `status`. | `-datasetName` |
| `orgId` | Corrisponde alle scadenze dei set di dati il cui ID organizzazione corrisponde a quello del parametro. Questo valore viene impostato automaticamente su quello del `x-gw-ims-org-id` e viene ignorato a meno che la richiesta non fornisca un token di servizio. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `page` | Numero intero che indica la pagina di scadenze da restituire. | `page=3` |
| `sandboxName` | Corrisponde alle scadenze del set di dati il cui nome di sandbox corrisponde esattamente all’argomento. Viene impostato automaticamente sul nome della sandbox nel campo `x-sandbox-name` intestazione. Utilizzare `sandboxName=*` per includere le scadenze dei set di dati da tutte le sandbox. | `sandboxName=dev1` |
| `search` | Corrisponde a scadenze in cui la stringa specificata corrisponde esattamente all’ID scadenza o è **contenuto** in uno di questi campi:<br><ul><li>author</li><li>nome visualizzato</li><li>descrizione</li><li>nome visualizzato</li><li>nome set di dati</li></ul> | `search=TESTING` |
| `status` | Elenco di stati separato da virgole. Se inclusa, la risposta corrisponde alle scadenze del set di dati il cui stato corrente è tra quelli elencati. | `status=pending,cancelled` |
| `ttlId` | Corrisponde alla richiesta di scadenza con l’ID specificato. | `ttlID=SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Mi piace `createdDate` / `createdFromDate` / `createdToDate`, ma corrisponde all’ora di aggiornamento della scadenza di un set di dati invece dell’ora di creazione.<br><br>Una scadenza viene considerata aggiornata a ogni modifica, anche quando viene creata, annullata o eseguita. | `updatedDate=2022-01-01` |

{style="table-layout:auto"}
