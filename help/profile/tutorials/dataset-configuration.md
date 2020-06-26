---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Configurare un set di dati per il servizio Profilo e identità utilizzando le API
topic: tutorial
translation-type: tm+mt
source-git-commit: 93aae0e394e1ea9b6089d01c585a94871863818e
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 1%

---


# Configurare un set di dati per il servizio Profilo e identità utilizzando le API

Questa esercitazione descrive il processo di attivazione di un dataset da utilizzare in Real-time Customer Profile and Identity Service, suddiviso nei seguenti passaggi:

1. Abilita un set di dati da utilizzare nel profilo cliente in tempo reale, utilizzando una delle due opzioni seguenti:
   - [Creare un nuovo dataset](#create-a-dataset-enabled-for-profile-and-identity)
   - [Configurare un dataset esistente](#configure-an-existing-dataset)
1. [Inserimento di dati nel dataset](#ingest-data-into-the-dataset)
1. [Conferma acquisizione dati per profilo cliente in tempo reale](#confirm-data-ingest-by-real-time-customer-profile)
1. [Conferma dell&#39;acquisizione dei dati da parte del servizio identità](#confirm-data-ingest-by-identity-service)

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei diversi servizi di Adobe Experience Platform  coinvolti nella gestione dei set di dati abilitati per il profilo. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi Platform:

- [Profilo](../home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [Servizio](../../identity-service/home.md)identità: Abilita il profilo cliente in tempo reale collegando identità da origini dati diverse che vengono caricate in Platform.
- [Servizio](../../catalog/home.md)catalogo: API RESTful che consente di creare set di dati e configurarli per il profilo cliente e il servizio identità in tempo reale.
- [Experience Data Model (XDM)](../../xdm/home.md): Framework standard con cui Platform organizza i dati sull&#39;esperienza dei clienti.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente chiamate alle API Platform.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi di  Experience Platform.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API Platform, è prima necessario completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API Experience Platform, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

Tutte le risorse in  Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API Platform richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione. Per ulteriori informazioni sulle sandbox in Platform, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

- x-sandbox-name: `{SANDBOX_NAME}`

## Crea un set di dati abilitato per Profilo e Identità {#create-a-dataset-enabled-for-profile-and-identity}

Puoi abilitare un set di dati per il profilo cliente e il servizio identità in tempo reale immediatamente dopo la creazione o in qualsiasi momento dopo la creazione del set di dati. Se si desidera abilitare un dataset già creato, seguire i passaggi per [configurare un dataset](#configure-an-existing-dataset) esistente trovato più avanti in questo documento. Per creare un nuovo set di dati, è necessario conoscere l&#39;ID di uno schema XDM esistente abilitato per il profilo cliente in tempo reale. Per informazioni su come ricercare o creare uno schema abilitato per il profilo, vedere l&#39;esercitazione sulla [creazione di uno schema tramite l&#39;API](../../xdm/tutorials/create-schema-api.md)del Registro di sistema dello schema. La seguente chiamata all&#39;API Catalog abilita un set di dati per Profile and Identity Service.

**Formato API**

```http
POST /dataSets
```

**Richiesta**

Includendo `unifiedProfile` e `unifiedIdentity` sotto `tags` nel corpo della richiesta, il set di dati sarà attivato immediatamente rispettivamente per Profile e Identity Service. I valori di questi tag devono essere una matrice contenente la stringa `"enabled:true"`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fileDescription" : {
    "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    },
    "fields":[],
    "schemaRef" : {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
    },
    "tags" : {
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| Proprietà | Descrizione |
|---|---|
| `schemaRef.id` | ID dello schema abilitato per il profilo su cui verrà basato il dataset. |
| `{TENANT_ID}` | Lo spazio dei nomi all&#39;interno del Registro di sistema dello schema che contiene le risorse appartenenti all&#39;organizzazione IMS. Per ulteriori informazioni, vedere la sezione [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) della guida per gli sviluppatori del Registro di sistema dello schema. |

**Risposta**

Una risposta corretta mostra un array contenente l&#39;ID del set di dati appena creato sotto forma di `"@/dataSets/{DATASET_ID}"`. Dopo aver creato e attivato correttamente un dataset, procedere con i passaggi necessari per [caricare i dati](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurare un dataset esistente {#configure-an-existing-dataset}

Nei passaggi seguenti viene illustrato come abilitare un dataset creato in precedenza per il profilo cliente e il servizio identità in tempo reale. Se hai già creato un set di dati con abilitazione per il profilo, procedi alla procedura di [acquisizione dei dati](#ingest-data-into-the-dataset).

### Verifica se il set di dati è abilitato {#check-if-the-dataset-is-enabled}

Utilizzando l&#39;API Catalog, potete ispezionare un set di dati esistente per determinare se è abilitato per l&#39;uso in Real-time Customer Profile and Identity Service. La seguente chiamata recupera i dettagli di un set di dati per ID.

**Formato API**

```http
GET /dataSets/{DATASET_ID}
```

| Parametro | Descrizione |
|---|---|
| `{DATASET_ID}` | ID di un set di dati da esaminare. |

**Richiesta**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "Commission Program Events DataSet",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedProfile": [
                "enabled:true"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ]
        },
        "lastBatchId": "6dcd9128a1c84e6aa5177641165e18e4",
        "lastBatchStatus": "success",
        "dule": {},
        "statsCache": {
            "startDate": null,
            "endDate": null
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "5b020a27e7040801dedbf46f",
        "status": "enabled",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "@/xdms/context/experienceevent",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": [],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

Sotto la `tags` proprietà, è possibile vedere che `unifiedProfile` e `unifiedIdentity` sono entrambi presenti con il valore `enabled:true`. Di conseguenza, i profili cliente e i servizi identità in tempo reale sono abilitati rispettivamente per questo set di dati.

### Abilitare il set di dati {#enable-the-dataset}

Se il set di dati esistente non è stato abilitato per il servizio Profilo o Identità, puoi attivarlo effettuando una richiesta PATCH utilizzando l’ID del set di dati.

**Formato API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parametro | Descrizione |
|---|---|
| `{DATASET_ID}` | ID di un set di dati da aggiornare. |

**Richiesta**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags" : {
        "unifiedProfile": ["enabled:true"],
        "unifiedIdentity": ["enabled:true"]
    }
  }'
```

Il corpo della richiesta include una `tags` proprietà, che contiene due proprietà secondarie: `"unifiedProfile"` e `"unifiedIdentity"`. I valori di queste proprietà secondarie sono matrici contenenti la stringa `"enabled:true"`.

**Risposta** Una richiesta PATCH riuscita restituisce lo stato HTTP 200 (OK) e un array contenente l&#39;ID del set di dati aggiornato. Questo ID deve corrispondere a quello inviato nella richiesta PATCH. Sono stati aggiunti `"unifiedProfile"` e `"unifiedIdentity"` i tag e il set di dati è abilitato per l&#39;uso da parte dei servizi Profilo e Identità.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Inserimento di dati nel dataset {#ingest-data-into-the-dataset}

Sia il profilo cliente in tempo reale che il servizio identità utilizzano i dati XDM durante l&#39;assimilazione in un dataset. Per istruzioni su come caricare i dati in un dataset, fare riferimento all&#39;esercitazione sulla [creazione di un dataset mediante le API](../../catalog/datasets/create.md). Quando pianificate quali dati inviare al set di dati abilitato per il profilo, tenete presenti le seguenti procedure ottimali:

- Includete tutti i dati che desiderate utilizzare come criteri di segmento dell&#39;audience.
- Includi tutti gli identificatori che puoi verificare dai dati del tuo profilo per massimizzare il grafico di identità. In questo modo, Servizio identità può unire più efficacemente le identità tra i set di dati.

## Conferma acquisizione dati per profilo cliente in tempo reale {#confirm-data-ingest-by-real-time-customer-profile}

Quando si caricano i dati in un nuovo dataset per la prima volta, o come parte di un processo che coinvolge una nuova ETL o una nuova origine dati, si consiglia di controllare attentamente i dati per assicurarsi che siano stati caricati come previsto. Utilizzando l&#39;API Real-time Customer Profile Access, potete recuperare i dati batch mentre vengono caricati in un dataset. Se non riesci a recuperare nessuna delle entità previste, il set di dati potrebbe non essere abilitato per il profilo cliente in tempo reale. Dopo aver confermato che il set di dati è stato abilitato, accertati che il formato e gli identificatori dei dati di origine supportino le tue aspettative. Per istruzioni dettagliate su come utilizzare l&#39;API del profilo cliente in tempo reale per accedere ai dati del profilo, segui la guida [all&#39;endpoint](../api/entities.md)entità, nota anche come &quot;API di accesso profilo&quot;.

## Conferma dell&#39;acquisizione dei dati da parte del servizio identità {#confirm-data-ingest-by-identity-service}

Ogni frammento di dati inserito contenente più identità crea un collegamento nel grafico dell&#39;identità privata. Per ulteriori informazioni sui grafici identità e sui dati di accesso all&#39;identità, leggere la panoramica [del servizio](../../identity-service/home.md)identità.