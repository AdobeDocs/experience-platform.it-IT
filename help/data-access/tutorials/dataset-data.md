---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica sull'accesso ai dati
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 2%

---


# Dati del set di query tramite API Data Access

Questo documento fornisce un&#39;esercitazione passo-passo che illustra come individuare, accedere e scaricare i dati memorizzati in un dataset utilizzando l&#39;API di accesso ai dati in  Adobe Experience Platform. Verranno inoltre introdotte alcune delle caratteristiche uniche dell&#39;API di accesso ai dati, come il paging e i download parziali.

## Introduzione

Questa esercitazione spiega come creare e compilare un dataset. Per ulteriori informazioni, consulta l’esercitazione [sulla creazione dei](../../catalog/datasets/create.md) set di dati.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente chiamate alle API Platform.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi di  Experience Platform.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API Platform, è prima necessario completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API Experience Platform, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in  Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API Platform richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Platform, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

## Diagramma della sequenza

Questa esercitazione segue i passaggi descritti nel diagramma di sequenza seguente, evidenziando le funzionalità di base dell&#39;API di accesso ai dati.</br>
![](../images/sequence_diagram.png)

L&#39;API Catalog consente di recuperare informazioni relative a batch e file. L&#39;API di accesso ai dati consente di accedere e scaricare questi file via HTTP come download completi o parziali, a seconda delle dimensioni del file.

## Individuare i dati

Prima di poter iniziare a utilizzare l&#39;API di accesso ai dati, è necessario identificare la posizione dei dati a cui si desidera accedere. Nell&#39;API Catalog sono disponibili due endpoint che potete utilizzare per sfogliare i metadati di un&#39;organizzazione e recuperare l&#39;ID di un batch o di un file a cui desiderate accedere:

- `GET /batches`: Restituisce un elenco di batch all&#39;interno dell&#39;organizzazione
- `GET /dataSetFiles`: Restituisce un elenco di file nell&#39;organizzazione

Per un elenco completo degli endpoint nell&#39;API Catalog, fate riferimento a Riferimento [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)API.

## Recupera un elenco di batch nell&#39;organizzazione IMS

Utilizzando l’API Catalog, potete restituire un elenco di batch nell’organizzazione:

**Formato API**

```http
GET /batches
```

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta include un oggetto che elenca tutti i batch relativi all&#39;organizzazione IMS, con ogni valore di livello principale che rappresenta un batch. I singoli oggetti batch contengono i dettagli per il batch specifico. La risposta riportata di seguito è stata ridotta a icona per lo spazio disponibile.

```json
{
    "{BATCH_ID_1}": {
        "imsOrg": "{IMS_ORG}",
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

I filtri sono spesso necessari per trovare un particolare lotto al fine di recuperare i dati rilevanti per un particolare caso d’uso. I parametri possono essere aggiunti a una `GET /batches` richiesta per filtrare la risposta restituita. Nella richiesta seguente verranno restituiti tutti i batch creati dopo un determinato periodo di tempo, all’interno di un particolare set di dati, ordinati in base a quando sono stati creati.

**Formato API**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{START_TIMESTAMP}` | Il timestamp iniziale in millisecondi (ad esempio, 1514836799000). |
| `{DATASET_ID}` | Identificatore del set di dati. |
| `{SORT_BY}` | Ordina la risposta in base al valore fornito. Ad esempio, `desc:created` ordina gli oggetti per data di creazione in ordine decrescente. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1521053542579&dataSet=5cd9146b21dae914b71f654f&orderBy=desc:created' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```json
{   "{BATCH_ID_3}": {
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
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

Un elenco completo di parametri e filtri si trova nel riferimento [API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)Catalog.

## Recuperare un elenco di tutti i file appartenenti a un particolare batch

Ora che disponete dell&#39;ID del batch a cui desiderate accedere, potete utilizzare l&#39;API di accesso ai dati per ottenere un elenco di file appartenenti a tale batch.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

La risposta contiene un array di dati che elenca tutti i file all&#39;interno del batch specificato. Ai file viene fatto riferimento dal relativo ID file, che si trova nel `dataSetFileId` campo.

## Accesso a un file con un ID file

Una volta ottenuto un ID file univoco, è possibile utilizzare l&#39;API di accesso ai dati per accedere ai dettagli specifici sul file, incluso il nome, la dimensione in byte e un collegamento per scaricarlo.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

A seconda che l&#39;ID file punti a un singolo file o a una directory, l&#39;array di dati restituito può contenere una singola voce o un elenco di file appartenenti a tale directory. Ogni elemento del file conterrà dettagli quali il nome del file, la dimensione in byte e un collegamento per scaricare il file.

**Caso 1: L&#39;ID file punta a un singolo file**

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

**Caso 2: L&#39;ID file punta a una directory**

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

Questa risposta restituisce una directory contenente due file separati, con ID `{FILE_ID_2}` e `{FILE_ID_3}`. In questo scenario, per accedere al file dovrete seguire l&#39;URL di ciascun file.

## Recuperare i metadati di un file

Potete recuperare i metadati di un file effettuando una richiesta HEAD. Questo restituisce le intestazioni dei metadati del file, incluse le dimensioni in byte e il formato del file.

**Formato API**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_ID}` | Identificatore del file. |
| `{FILE_NAME`} | Nome del file (ad esempio, profile.parquet) |

**Richiesta**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Le intestazioni di risposta contengono i metadati del file interrogato, compresi:
- `Content-Length`: Indica la dimensione del payload in byte
- `Content-Type`: Indica il tipo di file.

## Accesso al contenuto di un file

È inoltre possibile accedere al contenuto di un file utilizzando l&#39;API di accesso ai dati.

**Formato API**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_ID}` | Identificatore del file. |
| `{FILE_NAME`} | Il nome del file (ad esempio, profile.parquet). |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce il contenuto del file.

## Scaricare contenuti parziali di un file

L&#39;API di accesso ai dati consente di scaricare i file in blocchi. È possibile specificare un&#39;intestazione di intervallo durante una `GET /files/{FILE_ID}` richiesta per scaricare un intervallo specifico di byte da un file. Se l&#39;intervallo non è specificato, l&#39;API scaricherà l&#39;intero file per impostazione predefinita.

L&#39;esempio HEAD nella sezione [](#retrieve-the-metadata-of-a-file) precedente indica la dimensione di un file specifico in byte.

**Formato API**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_ID} ` | Identificatore del file. |
| `{FILE_NAME}` | Nome del file (ad esempio, profile.parquet) |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Range: bytes=0-99'
```

| Proprietà | Descrizione |
| -------- | ----------- | 
| `Range: bytes=0-99` | Specifica l&#39;intervallo di byte da scaricare. Se non viene specificato, l&#39;API scaricherà l&#39;intero file. In questo esempio, verranno scaricati i primi 100 byte. |

**Risposta**

Il corpo della risposta include i primi 100 byte del file (come specificato dall&#39;intestazione &quot;Range&quot; nella richiesta) insieme allo stato HTTP 206 (Contenuti parziali). La risposta include anche le seguenti intestazioni:

- Durata contenuto: 100 (numero di byte restituiti)
- Tipo di contenuto: application/parquet (è stato richiesto un file parquet, pertanto il tipo di contenuto della risposta è parquet)
- Content-Range: byte 0-99/249058 (l&#39;intervallo richiesto (0-99) del numero totale di byte (249058)

## Configurare l&#39;impaginazione delle risposte API

Le risposte all&#39;interno dell&#39;API di accesso ai dati sono impaginate. Per impostazione predefinita, il numero massimo di voci per pagina è 100. I parametri di paging possono essere utilizzati per modificare il comportamento predefinito.

- `limit`: Potete specificare il numero di voci per pagina in base alle vostre esigenze utilizzando il parametro &quot;limit&quot;.
- `start`: L&#39;offset può essere impostato dal parametro di query &quot;start&quot;.
- `&`: Puoi utilizzare una e-mail per combinare più parametri in una singola chiamata.

**Formato API**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | Identificatore batch del batch a cui si sta tentando di accedere. |
| `{OFFSET}` | L&#39;indice specificato per avviare l&#39;array dei risultati (ad esempio, start=0) |
| `{LIMIT}` | Controlla quanti risultati vengono restituiti nell&#39;array dei risultati (ad esempio, limit=1) |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**:

La risposta contiene un `"data"` array con un singolo elemento, come specificato dal parametro request `limit=1`. Questo elemento è un oggetto che contiene i dettagli del primo file disponibile, come specificato dal `start=0` parametro nella richiesta (ricordate che nella numerazione a base zero, il primo elemento è &quot;0&quot;).

Il `_links.next.href` valore contiene il collegamento alla pagina successiva di risposte, dove è possibile vedere che il `start` parametro è avanzato `start=1`.

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
