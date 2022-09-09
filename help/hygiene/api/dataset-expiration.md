---
title: Endpoint API per le scadenze del set di dati
description: L’endpoint /ttl nell’API di igiene dati ti consente di pianificare programmaticamente la scadenza dei set di dati in Adobe Experience Platform.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 5a12c75a54f420b2ca831dbfe05105dfd856dc4d
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 6%

---

# Endpoint di scadenza del set di dati

>[!IMPORTANT]
>
>Le funzionalità di igiene dei dati in Adobe Experience Platform sono attualmente disponibili solo per le organizzazioni che hanno acquistato Healthcare Shield.

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
  https://platform.adobe.io/data/core/hygiene/ttl?page=1&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta elenca le scadenze risultanti del set di dati. L&#39;esempio seguente è stato troncato per lo spazio.

```json
{
  "results": [
    {
      "ttlId": "SDfba908e9fb2e427ab4275d20465631d7",
      "datasetId": "62799c3e1151781b63ccaa28",
      "imsOrg": "{ORG_ID}",
      "status": "cancelled",
      "expiry": "2022-05-09T22:57:05.531024Z",
      "updatedAt": "2022-05-09T22:57:05.531025Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
      "datasetId": "62759f2ede9e601b63a2ee14",
      "imsOrg": "{ORG_ID}",
      "status": "pending",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "{USER_ID}"
    }
  ],
  "current_page": 1,
  "total_pages": 36,
  "total_count": 886
}
```

| Proprietà | Descrizione |
| --- | --- |
| `results` | Contiene i dettagli delle scadenze del set di dati restituito. Per ulteriori dettagli sulle proprietà della scadenza di un set di dati, consulta la sezione relativa alla risposta per creare un [chiamata di ricerca](#lookup). |
| `current_page` | La pagina corrente dei risultati elencati. |
| `total_pages` | Il numero totale di pagine nella risposta. |
| `total_count` | Il numero totale di scadenze del set di dati nella risposta. |

{style=&quot;table-layout:auto&quot;}

## Cercare la scadenza di un set di dati {#lookup}

Puoi cercare la scadenza di un set di dati tramite una richiesta GET.

**Formato API**

```http
GET /ttl/{TTL_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{TTL_ID}` | ID della scadenza del set di dati da cercare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli della scadenza del set di dati.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `ttlId` | ID della scadenza del set di dati. |
| `datasetId` | ID del set di dati a cui si applica questa scadenza. |
| `imsOrg` | L&#39;ID della tua organizzazione. |
| `status` | Lo stato corrente della scadenza del set di dati. |
| `expiry` | Data e ora pianificate in cui il set di dati verrà eliminato. |
| `updatedAt` | Una marca temporale dell’ultimo aggiornamento della scadenza. |
| `updatedBy` | L’ultimo utente che ha aggiornato la scadenza. |

{style=&quot;table-layout:auto&quot;}

## Creare una scadenza del set di dati {#create}

Puoi creare una data di scadenza per un set di dati tramite una richiesta di POST.

**Formato API**

```http
POST /ttl
```

**Richiesta**

La seguente richiesta pianifica un set di dati `5b020a27e7040801dedbf46e` per la cancellazione alla fine del 2022 (Greenwich Mean Time).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "datasetId": "5b020a27e7040801dedbf46e",
        "expiry": "2022-12-31T23:59:59Z"
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `datasetId` | ID del set di dati per il quale vuoi pianificare una data di scadenza. |
| `expiry` | Timestamp ISO 8601 per quando il set di dati verrà eliminato. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli della scadenza del set di dati, con stato HTTP 200 (OK) se è stata aggiornata una scadenza preesistente, o 201 (Creata) se non c&#39;è stata una scadenza preesistente.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2032-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `ttlId` | ID della scadenza del set di dati. |
| `datasetId` | ID del set di dati a cui si applica questa scadenza. |
| `imsOrg` | L&#39;ID della tua organizzazione. |
| `status` | Lo stato corrente della scadenza del set di dati. |
| `expiry` | Data e ora pianificate in cui il set di dati verrà eliminato. |
| `updatedAt` | Una marca temporale dell’ultimo aggiornamento della scadenza. |
| `updatedBy` | L’ultimo utente che ha aggiornato la scadenza. |

{style=&quot;table-layout:auto&quot;}

## Aggiornare la scadenza di un set di dati {#update}

Puoi aggiornare la scadenza di un set di dati tramite una richiesta PUT.

**Formato API**

```http
PUT /ttl/{TTL_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{TTL_ID}` | ID della scadenza del set di dati da modificare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La seguente richiesta aggiorna la scadenza del set di dati `5b020a27e7040801dedbf46e` quindi scade alla fine del 2023 (Greenwich Mean Time).

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2023-12-31T23:59:59Z"
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `expiry` | Timestamp ISO 8601 per quando il set di dati verrà eliminato. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli della scadenza aggiornata.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `ttlId` | ID della scadenza del set di dati. |
| `datasetId` | ID del set di dati a cui si applica questa scadenza. |
| `imsOrg` | L&#39;ID della tua organizzazione. |
| `status` | Lo stato corrente della scadenza del set di dati. |
| `expiry` | Data e ora pianificate in cui il set di dati verrà eliminato. |
| `updatedAt` | Una marca temporale dell’ultimo aggiornamento della scadenza. |
| `updatedBy` | L’ultimo utente che ha aggiornato la scadenza. |

{style=&quot;table-layout:auto&quot;}

## Annullare la scadenza di un set di dati {#delete}

Puoi annullare la scadenza di un set di dati effettuando una richiesta DELETE.

**Formato API**

```http
DELETE /ttl/{TTL_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{TTL_ID}` | ID della scadenza del set di dati da annullare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La seguente richiesta aggiorna la scadenza del set di dati `5b020a27e7040801dedbf46e` quindi scade alla fine del 2023 (Greenwich Mean Time).

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli della scadenza del set di dati, con la relativa `status` attributo impostato su `cancelled`.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "cancelled",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T23:47:30.071186Z",
    "updatedBy": "{USER_ID}"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `ttlId` | ID della scadenza del set di dati. |
| `datasetId` | ID del set di dati a cui si applica questa scadenza. |
| `imsOrg` | L&#39;ID della tua organizzazione. |
| `status` | Lo stato corrente della scadenza del set di dati. |
| `expiry` | Data e ora pianificate in cui il set di dati verrà eliminato. |
| `updatedAt` | Una marca temporale dell’ultimo aggiornamento della scadenza. |
| `updatedBy` | L’ultimo utente che ha aggiornato la scadenza. |

{style=&quot;table-layout:auto&quot;}

## Recupera la cronologia della scadenza di un set di dati

Puoi cercare la cronologia di una specifica scadenza di set di dati utilizzando il parametro query `include=history` in una richiesta di ricerca. Il risultato include informazioni sulla creazione della scadenza del set di dati, sugli eventuali aggiornamenti applicati e sulla relativa cancellazione o esecuzione (se applicabile).

**Formato API**

```http
GET /ttl/{TTL_ID}?include=history
```

| Parametro | Descrizione |
| --- | --- |
| `{TTL_ID}` | ID della scadenza del set di dati di cui vuoi cercare la cronologia. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e?include=history \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli della scadenza del set di dati, con un `history` array che fornisce i dettagli `status`, `expiry`, `updatedAt`e `updatedBy` per ciascuno dei relativi aggiornamenti registrati.

```json
{
  "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
  "datasetId": "62759f2ede9e601b63a2ee14",
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
| `ttlId` | ID della scadenza del set di dati. |
| `datasetId` | ID del set di dati a cui si applica questa scadenza. |
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
| `status` | Elenco di stati separati da virgole. Quando è inclusa, la risposta corrisponde alle scadenze del set di dati il cui stato corrente è tra quelli elencati. | `status=pending,cancelled` |
| `author` | Corrisponde alle scadenze di cui `created_by` è una corrispondenza per la stringa di ricerca. Se la stringa di ricerca inizia con `LIKE` o `NOT LIKE`, il resto viene trattato come un pattern di ricerca SQL. In caso contrario, l’intera stringa di ricerca viene trattata come una stringa letterale che deve corrispondere esattamente all’intero contenuto di un `created_by` campo . | `author=LIKE %john%` |
| `createdDate` | Corrisponde alle scadenze create nella finestra di 24 ore a partire dall&#39;ora indicata.<br><br>Tieni presente che le date non hanno un&#39;ora (come `2021-12-07`) rappresenta il datetime all&#39;inizio di quel giorno. Pertanto, `createdDate=2021-12-07` si riferisce a qualsiasi scadenza creata il 7 dicembre 2021, a partire da `00:00:00` attraverso `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Corrisponde alle scadenze create al momento o dopo l’ora indicata. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Corrisponde alle scadenze create al momento indicato o prima. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Simile `createdDate` / `createdFromDate` / `createdToDate`, ma corrisponde al tempo di aggiornamento della scadenza di un set di dati anziché al tempo di creazione.<br><br>Una scadenza viene considerata aggiornata a ogni modifica, anche quando viene creata, annullata o eseguita. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Corrisponde alle scadenze che sono state annullate in qualsiasi momento nell&#39;intervallo indicato. Ciò si applica anche se la scadenza è stata successivamente riaperta (impostando una nuova scadenza per lo stesso set di dati). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Corrisponde alle scadenze completate durante l&#39;intervallo specificato. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Corrisponde alle scadenze che devono essere eseguite o sono già state eseguite nell&#39;intervallo specificato. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
