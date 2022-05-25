---
title: Endpoint API Time-to-Live (TTL) del set di dati
description: L’endpoint /ttl nell’API di igiene dati ti consente di pianificare programmaticamente i TTL dei set di dati in Adobe Experience Platform.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
hide: true
hidefromtoc: true
source-git-commit: c2e7cf1859f6a2b277783cdec535ecc208703fac
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 7%

---

# Endpoint time-to-live (TTL) del set di dati

>[!IMPORTANT]
>
>Le funzionalità di igiene dei dati in Adobe Experience Platform sono attualmente disponibili solo per le organizzazioni che hanno acquistato Adobe Shield per il settore sanitario.

La `/ttl` l’endpoint nell’API di igiene dati consente di pianificare i protocolli time-to-live (TTL) per i set di dati in Adobe Experience Platform.

Un TTL di set di dati è solo un’operazione di eliminazione ritardata per tempo. Il set di dati non è protetto nel frattempo, pertanto può essere cancellato con altri mezzi prima che sia raggiunta la sua scadenza.

>[!NOTE]
>
>Anche se la scadenza è specificata come un momento specifico nel tempo, ci possono essere fino a 24 ore di ritardo dopo la scadenza prima dell&#39;avvio della cancellazione effettiva. Una volta avviata l’eliminazione, possono essere necessari fino a sette giorni prima che tutte le tracce del set di dati siano state rimosse dai sistemi Platform.

In qualsiasi momento prima dell’avvio dell’eliminazione del set di dati, puoi annullare il TTL o modificarne il tempo di attivazione. Dopo aver annullato un TTL, puoi riaprirlo impostando una nuova scadenza.

Una volta avviata l’eliminazione del set di dati, il relativo TTL viene contrassegnato come `executing`e non può essere ulteriormente modificato. Il set di dati stesso può essere recuperabile per un massimo di sette giorni, ma solo tramite un processo manuale avviato tramite una richiesta di servizio Adobe.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’API di igiene dei dati. Prima di continuare, controlla la [panoramica](./overview.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e importanti informazioni sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Elencare TTL dei set di dati {#list}

Puoi elencare tutti i set di dati TTL per la tua organizzazione effettuando una richiesta GET.

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

Una risposta corretta elenca i TTL risultanti. L&#39;esempio seguente è stato troncato per lo spazio.

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
| `results` | Contiene i dettagli dei TTL restituiti. Per ulteriori dettagli sulle proprietà di un’entità TTL, consulta la sezione risposta per creare un [chiamata di ricerca](#lookup). |
| `current_page` | La pagina corrente dei risultati elencati. |
| `total_pages` | Il numero totale di pagine nella risposta. |
| `total_count` | Numero totale di entità TTL nella risposta. |

{style=&quot;table-layout:auto&quot;}

## Cerca un TTL {#lookup}

Puoi cercare un TTL di set di dati tramite una richiesta GET.

**Formato API**

```http
GET /ttl/{TTL_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{TTL_ID}` | L’ID del TTL da cercare. |

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

Una risposta corretta restituisce i dettagli del TTL.

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
| `ttlId` | ID del TTL del set di dati. |
| `datasetId` | ID del set di dati a cui si applica questo TTL. |
| `imsOrg` | L&#39;ID della tua organizzazione. |
| `status` | Lo stato corrente del TTL. |
| `expiry` | Data e ora pianificate in cui il set di dati verrà eliminato. |
| `updatedAt` | Timestamp dell’ultimo aggiornamento del TTL. |
| `updatedBy` | L’utente che ha aggiornato l’ultimo valore TTL. |

{style=&quot;table-layout:auto&quot;}

## Creare un TTL {#create}

È possibile aggiungere un TTL per un set di dati tramite una richiesta di POST.

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
| `datasetId` | ID del set di dati per cui si desidera pianificare un TTL. |
| `expiry` | Timestamp ISO 8601 per quando il set di dati verrà eliminato. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli del TTL, con stato HTTP 200 (OK) se è stato aggiornato un TTL preesistente, o 201 (Creato) se non era presente un TTL preesistente.

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
| `ttlId` | ID del TTL del set di dati. |
| `datasetId` | ID del set di dati a cui si applica questo TTL. |
| `imsOrg` | L&#39;ID della tua organizzazione. |
| `status` | Lo stato corrente del TTL. |
| `expiry` | Data e ora pianificate in cui il set di dati verrà eliminato. |
| `updatedAt` | Timestamp dell’ultimo aggiornamento del TTL. |
| `updatedBy` | L’utente che ha aggiornato l’ultimo valore TTL. |

{style=&quot;table-layout:auto&quot;}

## Aggiornare un TTL {#update}

È possibile aggiornare un TTL per un set di dati tramite una richiesta PUT.

**Formato API**

```http
PUT /ttl/{TTL_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{TTL_ID}` | ID del TTL che desideri modificare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La seguente richiesta aggiorna il TTL per il set di dati `5b020a27e7040801dedbf46e` quindi scade alla fine del 2023 (Greenwich Mean Time).

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

Una risposta corretta restituisce i dettagli del TTL aggiornato.

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
| `ttlId` | ID del TTL del set di dati. |
| `datasetId` | ID del set di dati a cui si applica questo TTL. |
| `imsOrg` | L&#39;ID della tua organizzazione. |
| `status` | Lo stato corrente del TTL. |
| `expiry` | Data e ora pianificate in cui il set di dati verrà eliminato. |
| `updatedAt` | Timestamp dell’ultimo aggiornamento del TTL. |
| `updatedBy` | L’utente che ha aggiornato l’ultimo valore TTL. |

{style=&quot;table-layout:auto&quot;}

## Annullare un TTL {#delete}

È possibile annullare un TTL effettuando una richiesta di DELETE.

**Formato API**

```http
DELETE /ttl/{TTL_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{TTL_ID}` | ID del TTL che si desidera annullare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La seguente richiesta aggiorna il TTL per il set di dati `5b020a27e7040801dedbf46e` quindi scade alla fine del 2023 (Greenwich Mean Time).

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli del TTL, con i relativi `status` attributo impostato su `cancelled`.

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
| `ttlId` | ID del TTL del set di dati. |
| `datasetId` | ID del set di dati a cui si applica questo TTL. |
| `imsOrg` | L&#39;ID della tua organizzazione. |
| `status` | Lo stato corrente del TTL. |
| `expiry` | Data e ora pianificate in cui il set di dati verrà eliminato. |
| `updatedAt` | Timestamp dell’ultimo aggiornamento del TTL. |
| `updatedBy` | L’utente che ha aggiornato l’ultimo valore TTL. |

{style=&quot;table-layout:auto&quot;}

## Recupera la cronologia di un TTL

Puoi cercare la cronologia di un TTL specifico utilizzando il parametro di query `include=history` in una richiesta di ricerca. Il risultato include informazioni sulla creazione del TTL, gli eventuali aggiornamenti applicati e la relativa cancellazione o esecuzione (se applicabile).

**Formato API**

```http
GET /ttl/{TTL_ID}?include=history
```

| Parametro | Descrizione |
| --- | --- |
| `{TTL_ID}` | ID del TTL di cui si desidera cercare la cronologia. |

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

Una risposta corretta restituisce i dettagli del TTL, con un `history` array che fornisce i dettagli `status`, `expiry`, `updatedAt`e `updatedBy` per ciascuno dei relativi aggiornamenti registrati.

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
| `ttlId` | ID del TTL del set di dati. |
| `datasetId` | ID del set di dati a cui si applica questo TTL. |
| `imsOrg` | L&#39;ID della tua organizzazione. |
| `history` | Elenca la cronologia degli aggiornamenti del TTL come array di oggetti, con ogni oggetto contenente il `status`, `expiry`, `updatedAt`e `updatedBy` attributi per il TTL al momento dell’aggiornamento. |

{style=&quot;table-layout:auto&quot;}

## Appendice

### Parametri di query accettati {#query-params}

La tabella seguente delinea i parametri di query disponibili quando [elencare i TTL dei set di dati](#list):

| Parametro | Descrizione | Esempio |
| --- | --- | --- |
| `size` | Un numero intero compreso tra 1 e 100 che indica il numero massimo di TTL da restituire. Il valore predefinito è 25. | `size=50` |
| `page` | Un numero intero che indica la pagina di TTL da restituire. | `page=3` |
| `status` | Elenco di stati separati da virgole. Se inclusa, la risposta corrisponde ai TTL il cui stato corrente è tra quelli elencati. | `status=pending,cancelled` |
| `author` | Corrisponde a TTL di cui `created_by` è una corrispondenza per la stringa di ricerca. Se la stringa di ricerca inizia con `LIKE` o `NOT LIKE`, il resto viene trattato come un pattern di ricerca SQL. In caso contrario, l’intera stringa di ricerca viene trattata come una stringa letterale che deve corrispondere esattamente all’intero contenuto di un `created_by` campo . | `author=LIKE %john%` |
| `createdDate` | Corrisponde ai TTL creati nella finestra di 24 ore a partire dall’ora indicata.<br><br>Tieni presente che le date non hanno un&#39;ora (come `2021-12-07`) rappresenta il datetime all&#39;inizio di quel giorno. Pertanto, `createdDate=2021-12-07` si riferisce a qualsiasi TTL creato il 7 dicembre 2021, a partire da `00:00:00` attraverso `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Corrisponde ai TTL creati al momento o dopo l’ora indicata. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Corrisponde ai TTL creati al momento o prima dell’ora indicata. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Simile `createdDate` / `createdFromDate` / `createdToDate`, ma corrisponde al tempo di aggiornamento di un TTL anziché al tempo di creazione.<br><br>Un TTL viene considerato aggiornato a ogni modifica, anche quando viene creato, annullato o eseguito. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Corrisponde ai TTL annullati in qualsiasi momento nell’intervallo indicato. Ciò si applica anche se il TTL è stato successivamente riaperto (impostando una nuova scadenza per lo stesso set di dati). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Corrisponde ai TTL completati durante l’intervallo specificato. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Corrisponde ai TTL che devono essere eseguiti o sono già stati eseguiti nell’intervallo specificato. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
