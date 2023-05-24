---
keywords: Experience Platform;home;argomenti popolari;accesso ai dati;api di accesso ai dati;query data access
solution: Experience Platform
title: Visualizzare i dati del set di dati utilizzando l’API di accesso ai dati
type: Tutorial
description: Scopri come individuare, accedere e scaricare i dati memorizzati all’interno di un set di dati utilizzando l’API di accesso ai dati in Adobe Experience Platform. Verranno inoltre illustrate alcune delle funzioni univoche dell’API di accesso ai dati, come il paging e i download parziali.
exl-id: 1c1e5549-d085-41d5-b2c8-990876000f08
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 4%

---

# Visualizzare i dati del set di dati tramite [!DNL Data Access] API

Questo documento fornisce un tutorial dettagliato che illustra come individuare, accedere e scaricare i dati memorizzati all’interno di un set di dati utilizzando [!DNL Data Access] API in Adobe Experience Platform. Verranno inoltre presentate alcune delle funzionalità esclusive di [!DNL Data Access] API, come il paging e i download parziali.

## Introduzione

Questo tutorial richiede una buona conoscenza di come creare e popolare un set di dati. Consulta la [tutorial sulla creazione di set di dati](../../catalog/datasets/create.md) per ulteriori informazioni.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente le chiamate alle API di Platform.

### Lettura delle chiamate API di esempio

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nel [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori per le intestazioni richieste

Per effettuare chiamate a [!DNL Platform] , devi prima completare le [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolati in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedere [documentazione di panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Content-Type: application/json

## Diagramma sequenza

Questa esercitazione segue i passaggi descritti nel diagramma di sequenza riportato di seguito, evidenziando le funzionalità principali di [!DNL Data Access] API.</br>
![](../images/sequence_diagram.png)

Il [!DNL Catalog] API consente di recuperare informazioni relative a batch e file. Il [!DNL Data Access] API consente di accedere e scaricare questi file tramite HTTP come download completi o parziali, a seconda delle dimensioni del file.

## Individuare i dati

Prima di iniziare a utilizzare il [!DNL Data Access] API, è necessario identificare la posizione dei dati a cui desideri accedere. In [!DNL Catalog] API, puoi utilizzare due endpoint per sfogliare i metadati di un’organizzazione e recuperare l’ID di un batch o di un file a cui desideri accedere:

- `GET /batches`: restituisce un elenco di batch nell’organizzazione
- `GET /dataSetFiles`: restituisce un elenco di file dell’organizzazione

Per un elenco completo degli endpoint nel [!DNL Catalog] API, fare riferimento al [Riferimento API](https://www.adobe.io/experience-platform-apis/references/catalog/).

## Recuperare un elenco di batch nell&#39;organizzazione

Utilizzo di [!DNL Catalog] API, puoi restituire un elenco di batch all’interno della tua organizzazione:

**Formato API**

```http
GET /batches
```

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta include un oggetto che elenca tutti i batch correlati all’organizzazione, con ogni valore di livello superiore che rappresenta un batch. I singoli oggetti batch contengono i dettagli per quel batch specifico. La risposta seguente è stata ridotta a icona per motivi di spazio.

```json
{
    "{BATCH_ID_1}": {
        "imsOrg": "{ORG_ID}",
        "created": 1516640135526,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1516640135526,
        "status": "processing",
        "version": "1.0.0",
        "availableDates": {}
    },
    "{BATCH_ID_2}": {
    ...
    }
}
```

### Filtrare l’elenco dei batch

I filtri sono spesso necessari per trovare un particolare batch al fine di recuperare dati rilevanti per un particolare caso d’uso. I parametri possono essere aggiunti a una `GET /batches` per filtrare la risposta restituita. La richiesta seguente restituirà tutti i batch creati dopo un determinato periodo di tempo, all’interno di un particolare set di dati, ordinati in base al momento della creazione.

**Formato API**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{START_TIMESTAMP}` | Il timestamp di inizio in millisecondi (ad esempio, 1514836799000). |
| `{DATASET_ID}` | L’identificatore del set di dati. |
| `{SORT_BY}` | Ordina la risposta in base al valore fornito. Ad esempio: `desc:created` ordina gli oggetti in base alla data di creazione in ordine decrescente. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1521053542579&dataSet=5cd9146b21dae914b71f654f&orderBy=desc:created' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```json
{   "{BATCH_ID_3}": {
        "imsOrg": "{ORG_ID}",
        "relatedObjects": [
            {
                "id": "5c01a91863540f14cd3d0439",
                "type": "dataSet"
            },
            {
                "id": "00998255b4a148a2bfd4804c2f327324",
                "type": "batch"
            }
        ],
        "status": "success",
        "metrics": {
            "recordsFailed": 0,
            "recordsWritten": 2,
            "startTime": 1550791835809,
            "endTime": 1550791994636
        },
        "errors": [],
        "created": 1550791457173,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1550792060301,
        "version": "1.0.116"
    },
    "{BATCH_ID_4}": {
        "imsOrg": "{ORG_ID}",
        "status": "success",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "00aff31a9ae84a169d69b886cc63c063"
            },
            {
                "type": "dataSet",
                "id": "5bfde8c5905c5a000082857d"
            }
        ],
        "metrics": {
            "startTime": 1544571333876,
            "endTime": 1544571358291,
            "recordsRead": 4,
            "recordsWritten": 4
        },
        "errors": [],
        "created": 1544571077325,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1544571368776,
        "version": "1.0.3"
    }
}
```

Un elenco completo dei parametri e dei filtri è disponibile nella sezione [Riferimento API catalogo](https://www.adobe.io/experience-platform-apis/references/catalog/).

## Recuperare un elenco di tutti i file appartenenti a un batch specifico

Ora che disponi dell’ID del batch a cui desideri accedere, puoi utilizzare [!DNL Data Access] API per ottenere un elenco di file appartenenti a tale batch.

**Formato API**

```http
GET /batches/{BATCH_ID}/files
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | Identificatore batch del batch a cui si sta tentando di accedere. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c6f332168966814cd81d3d3/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```json
{
    "data": [
        {
            "dataSetFileId": "8dcedb36-1cb2-4496-9a38-7b2041114b56-1",
            "dataSetViewId": "5cc6a9b60d4a5914b7940a7f",
            "version": "1.0.0",
            "created": "1558522305708",
            "updated": "1558522305708",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `data._links.self.href` | URL di accesso al file. |

La risposta contiene un array di dati che elenca tutti i file all’interno del batch specificato. I file sono referenziati dal loro ID file, che si trova sotto `dataSetFileId` campo.

## Accedere a un file utilizzando un ID file

Una volta che hai un ID file univoco, puoi utilizzare [!DNL Data Access] API per accedere ai dettagli specifici sul file, tra cui il nome, la dimensione in byte e un collegamento per scaricarlo.

**Formato API**

```http
GET /files/{FILE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_ID}` | Identificatore del file a cui si desidera accedere. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

A seconda che l’ID file punti a un singolo file o a una directory, l’array di dati restituito può contenere una singola voce o un elenco di file appartenenti a tale directory. Ogni elemento del file conterrà dettagli quali il nome del file, la dimensione in byte e un collegamento per scaricare il file.

**Caso 1: l’ID file punta a un singolo file**

**Risposta**

```json
{
    "data": [
        {
            "name": "{FILE_NAME}.parquet",
            "length": "249058",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}?path={FILE_NAME_1}.parquet"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_NAME}.parquet` | Nome del file. |
| `_links.self.href` | URL per il download del file. |

**Caso 2: l’ID file punta a una directory**

**Risposta**

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_2}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267347",
            "updated": "150151267347",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
                }
            }
        },
        {
            "dataSetFileId": "{FILE_ID_3}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267685",
            "updated": "150151267685",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_3}"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- | 
| `data._links.self.href` | URL per scaricare il file associato. |

Questa risposta restituisce una directory contenente due file separati, con ID `{FILE_ID_2}` e `{FILE_ID_3}`. In questo caso, per accedere al file dovrai seguire l’URL di ciascun file.

## Recuperare i metadati di un file

Per recuperare i metadati di un file, effettua una richiesta HEAD. In questo modo vengono restituite le intestazioni di metadati del file, incluse le dimensioni in byte e nel formato di file.

**Formato API**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_ID}` | Identificatore del file. |
| `{FILE_NAME}` | Il nome del file (ad esempio, profiles.parquet) |

**Richiesta**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Le intestazioni di risposta contengono i metadati del file sottoposto a query, tra cui:
- `Content-Length`: indica la dimensione del payload in byte
- `Content-Type`: indica il tipo di file.

## Accedere al contenuto di un file

È inoltre possibile accedere al contenuto di un file utilizzando [!DNL Data Access] API.

**Formato API**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_ID}` | Identificatore del file. |
| `{FILE_NAME}` | Il nome del file (ad esempio, profiles.parquet). |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce il contenuto del file.

## Scaricare il contenuto parziale di un file

Il [!DNL Data Access] API consente di scaricare i file in blocchi. È possibile specificare un&#39;intestazione di intervallo durante un `GET /files/{FILE_ID}` richiesta di scaricare un intervallo specifico di byte da un file. Se l’intervallo non è specificato, l’API scaricherà l’intero file per impostazione predefinita.

L’esempio di HEAD in [sezione precedente](#retrieve-the-metadata-of-a-file) fornisce la dimensione di un file specifico in byte.

**Formato API**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_ID} ` | Identificatore del file. |
| `{FILE_NAME}` | Il nome del file (ad esempio, profiles.parquet) |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Range: bytes=0-99'
```

| Proprietà | Descrizione |
| -------- | ----------- | 
| `Range: bytes=0-99` | Specifica l&#39;intervallo di byte da scaricare. Se non viene specificato, l’API scaricherà l’intero file. In questo esempio, verranno scaricati i primi 100 byte. |

**Risposta**

Il corpo della risposta include i primi 100 byte del file (come specificato dall’intestazione &quot;Range&quot; nella richiesta) insieme allo stato HTTP 206 (Contenuti parziali). La risposta include anche le seguenti intestazioni:

- Content-Length: 100 (numero di byte restituiti)
- Tipo di contenuto: applicazione/parquet (è stato richiesto un file Parquet, pertanto il tipo di contenuto della risposta è `parquet`)
- Content-Range: byte 0-99/249058 (l&#39;intervallo richiesto (0-99) del numero totale di byte (249058))

## Configurare l’impaginazione della risposta API

Risposte all’interno di [!DNL Data Access] API impaginate. Per impostazione predefinita, il numero massimo di voci per pagina è 100. I parametri di paging possono essere utilizzati per modificare il comportamento predefinito.

- `limit`: puoi specificare il numero di voci per pagina in base alle tue esigenze utilizzando il parametro &quot;limit&quot;.
- `start`: l’offset può essere impostato dal parametro di query &quot;start&quot;.
- `&`: puoi utilizzare una e commerciale per combinare più parametri in una singola chiamata.

**Formato API**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | Identificatore batch del batch a cui si sta tentando di accedere. |
| `{OFFSET}` | L&#39;indice specificato per avviare la matrice dei risultati (ad esempio, start=0) |
| `{LIMIT}` | Controlla il numero di risultati restituiti nella matrice dei risultati (ad esempio, limit=1) |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**:

La risposta contiene un `"data"` con un singolo elemento, come specificato dal parametro di richiesta `limit=1`. Questo elemento è un oggetto contenente i dettagli del primo file disponibile, come specificato da `start=0` nella richiesta (ricorda che nella numerazione basata su zero il primo elemento è &quot;0&quot;).

Il `_links.next.href` contiene il collegamento alla pagina successiva delle risposte, in cui è possibile vedere che `start` il parametro è stato avanzato fino a `start=1`.

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_1}",
            "dataSetViewId": "5a9f264c2aa0cf01da4d82fa",
            "version": "1.0.0",
            "created": "1521053793635",
            "updated": "1521053793635",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
                }
            }
        }
    ],
    "_page": {
        "limit": 1,
        "count": 6
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=1&limit=1"
        },
        "page": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1",
            "templated": true
        }
    }
}
```
