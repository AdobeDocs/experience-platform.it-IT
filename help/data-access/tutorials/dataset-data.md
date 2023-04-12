---
keywords: Experience Platform;home;argomenti popolari;accesso ai dati;api di accesso ai dati;accesso ai dati di query
solution: Experience Platform
title: Visualizzare i dati del set di dati utilizzando l’API di accesso ai dati
type: Tutorial
description: Scopri come individuare, accedere e scaricare i dati memorizzati all’interno di un set di dati utilizzando l’API di accesso ai dati in Adobe Experience Platform. Verranno inoltre introdotte alcune funzionalità uniche dell’API di accesso ai dati, come il paging e i download parziali.
exl-id: 1c1e5549-d085-41d5-b2c8-990876000f08
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 4%

---

# Visualizzare i dati del set di dati utilizzando [!DNL Data Access] API

Questo documento fornisce un&#39;esercitazione dettagliata su come individuare, accedere e scaricare i dati archiviati all&#39;interno di un set di dati utilizzando [!DNL Data Access] API in Adobe Experience Platform. Verranno inoltre introdotte alcune delle caratteristiche uniche del [!DNL Data Access] API, ad esempio paging e download parziali.

## Introduzione

Questa esercitazione richiede una comprensione approfondita su come creare e popolare un set di dati. Consulta la sezione [esercitazione sulla creazione di set di dati](../../catalog/datasets/create.md) per ulteriori informazioni.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrai conoscere per effettuare correttamente le chiamate alle API di Platform.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione panoramica su sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Tipo di contenuto: application/json

## Diagramma della sequenza

Questa esercitazione segue i passaggi descritti nel diagramma di sequenza seguente, evidenziando le funzionalità di base del [!DNL Data Access] API.</br>
![](../images/sequence_diagram.png)

La [!DNL Catalog] L’API ti consente di recuperare informazioni relative a batch e file. La [!DNL Data Access] L’API ti consente di accedere e scaricare questi file tramite HTTP come download completo o parziale, a seconda delle dimensioni del file.

## Individuare i dati

Prima di iniziare a utilizzare il [!DNL Data Access] API, devi identificare la posizione dei dati a cui desideri accedere. In [!DNL Catalog] API, esistono due endpoint utilizzabili per sfogliare i metadati di un&#39;organizzazione e recuperare l&#39;ID di un batch o di un file a cui si desidera accedere:

- `GET /batches`: Restituisce un elenco di batch nell&#39;organizzazione
- `GET /dataSetFiles`: Restituisce un elenco di file nell&#39;organizzazione

Per un elenco completo degli endpoint nel [!DNL Catalog] API, fai riferimento al [Riferimento API](https://www.adobe.io/experience-platform-apis/references/catalog/).

## Recupera un elenco di batch nell&#39;organizzazione

Utilizzo della [!DNL Catalog] API, puoi restituire un elenco di batch sotto la tua organizzazione:

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

La risposta include un oggetto che elenca tutti i batch relativi all&#39;organizzazione, con ogni valore di livello superiore che rappresenta un batch. I singoli oggetti batch contengono i dettagli di quel batch specifico. La risposta seguente è stata ridotta a icona per lo spazio.

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

Spesso sono necessari filtri per trovare un particolare batch al fine di recuperare i dati rilevanti per un particolare caso d’uso. I parametri possono essere aggiunti a un `GET /batches` per filtrare la risposta restituita. La richiesta seguente restituisce tutti i batch creati dopo un determinato periodo di tempo, all’interno di un particolare set di dati, ordinati in base a quando sono stati creati.

**Formato API**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{START_TIMESTAMP}` | La marca temporale iniziale in millisecondi (ad esempio, 1514836799000). |
| `{DATASET_ID}` | Identificatore del set di dati. |
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

Un elenco completo dei parametri e dei filtri è disponibile nella sezione [Riferimento API per catalogo](https://www.adobe.io/experience-platform-apis/references/catalog/).

## Recupera un elenco di tutti i file appartenenti a un particolare batch

Ora che disponi dell’ID del batch a cui desideri accedere, puoi utilizzare il [!DNL Data Access] API per ottenere un elenco di file appartenenti a quel batch.

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
| `data._links.self.href` | URL per accedere a questo file. |

La risposta contiene un array di dati che elenca tutti i file all&#39;interno del batch specificato. I file sono referenziati dal loro ID file, che si trova nella sezione `dataSetFileId` campo .

## Accedere a un file utilizzando un ID file

Una volta ottenuto un ID file univoco, puoi utilizzare la funzione [!DNL Data Access] API per accedere ai dettagli specifici del file, inclusi nome, dimensione in byte e collegamento per scaricarlo.

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

A seconda che l’ID del file punti a un singolo file o a una directory, l’array di dati restituito può contenere una singola voce o un elenco di file appartenenti a tale directory. Ogni elemento del file conterrà dettagli quali il nome del file, la dimensione in byte e un collegamento per scaricare il file.

**Caso 1: L&#39;ID del file punta a un singolo file**

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
| `_links.self.href` | URL per scaricare il file. |

**Caso 2: L&#39;ID del file punta a una directory**

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

Questa risposta restituisce una directory contenente due file separati, con ID `{FILE_ID_2}` e `{FILE_ID_3}`. In questo scenario, per accedere al file dovrai seguire l’URL di ciascun file .

## Recupera i metadati di un file

È possibile recuperare i metadati di un file effettuando una richiesta di HEAD. Questo restituisce le intestazioni dei metadati del file, incluse le dimensioni in byte e il formato del file.

**Formato API**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_ID}` | Identificatore del file. |
| `{FILE_NAME}` | Nome del file (ad esempio, profiles.parquet) |

**Richiesta**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Le intestazioni di risposta contengono i metadati del file interrogato, tra cui:
- `Content-Length`: Indica la dimensione del payload in byte
- `Content-Type`: Indica il tipo di file.

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

Una risposta corretta restituisce il contenuto del file.

## Scaricare il contenuto parziale di un file

La [!DNL Data Access] L’API consente di scaricare i file in blocchi. È possibile specificare un&#39;intestazione di intervallo durante un `GET /files/{FILE_ID}` per scaricare un intervallo specifico di byte da un file. Se l’intervallo non è specificato, l’API scaricherà l’intero file per impostazione predefinita.

L’esempio di HEAD nel [sezione precedente](#retrieve-the-metadata-of-a-file) fornisce le dimensioni di un file specifico in byte.

**Formato API**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_ID} ` | Identificatore del file. |
| `{FILE_NAME}` | Nome del file (ad esempio, profiles.parquet) |

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
| `Range: bytes=0-99` | Specifica l&#39;intervallo di byte da scaricare. Se non viene specificato, l’API scaricherà l’intero file. In questo esempio verranno scaricati i primi 100 byte. |

**Risposta**

Il corpo della risposta include i primi 100 byte del file (come specificato dall&#39;intestazione &quot;Range&quot; nella richiesta) insieme allo stato HTTP 206 (Contenuti parziali). La risposta include anche le seguenti intestazioni:

- Lunghezza del contenuto: 100 (il numero di byte restituiti)
- Tipo di contenuto: application/parquet (è stato richiesto un file Parquet, quindi il tipo di contenuto della risposta è `parquet`)
- Intervallo di contenuti: byte 0-99/249058 (l&#39;intervallo richiesto (0-99) sul numero totale di byte (249058))

## Configurare l’impaginazione delle risposte API

Risposte all’interno della [!DNL Data Access] Le API sono impaginate. Per impostazione predefinita, il numero massimo di voci per pagina è 100. I parametri di paging possono essere utilizzati per modificare il comportamento predefinito.

- `limit`: Puoi specificare il numero di voci per pagina in base alle tue esigenze utilizzando il parametro &quot;limit&quot; (Limite).
- `start`: L&#39;offset può essere impostato dal parametro di query &quot;start&quot;.
- `&`: Puoi utilizzare una e commerciale per combinare più parametri in una singola chiamata.

**Formato API**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | Identificatore batch del batch a cui si sta tentando di accedere. |
| `{OFFSET}` | Indice specificato per avviare la matrice dei risultati (ad esempio, start=0) |
| `{LIMIT}` | Controlla quanti risultati vengono restituiti nella matrice dei risultati (ad esempio, limit=1) |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**:

La risposta contiene un `"data"` array con un singolo elemento, come specificato dal parametro della richiesta `limit=1`. Questo elemento è un oggetto contenente i dettagli del primo file disponibile, come specificato dal `start=0` nella richiesta (ricorda che nella numerazione basata su zero il primo elemento è &quot;0&quot;).

La `_links.next.href` contiene il collegamento alla pagina successiva di risposte, in cui puoi vedere che il `start` è stato avanzato per `start=1`.

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
