---
keywords: ' Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;abilita set di dati'
title: Configurare un set di dati per il servizio Profilo e identità utilizzando le API
topic: tutorial
type: Tutorial
description: Questa esercitazione mostra come abilitare un dataset da utilizzare con il profilo cliente e il servizio identità in tempo reale mediante le API Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: f34983dc13a900e7c8fe2e2cef454400c1b6a726
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 1%

---


# Configurare un dataset per [!DNL Profile] e [!DNL Identity Service] utilizzando le API

Questa esercitazione descrive il processo di abilitazione di un dataset da utilizzare in [!DNL Real-time Customer Profile] e [!DNL Identity Service], suddivisi nei seguenti passaggi:

1. Abilitare un set di dati da utilizzare in [!DNL Real-time Customer Profile], utilizzando una delle due opzioni seguenti:
   - [Creare un nuovo dataset](#create-a-dataset-enabled-for-profile-and-identity)
   - [Configurare un dataset esistente](#configure-an-existing-dataset)
1. [Inserimento di dati nel dataset](#ingest-data-into-the-dataset)
1. [Conferma acquisizione dati per profilo cliente in tempo reale](#confirm-data-ingest-by-real-time-customer-profile)
1. [Conferma dell&#39;acquisizione dei dati da parte del servizio identità](#confirm-data-ingest-by-identity-service)

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei diversi servizi Adobe Experience Platform coinvolti nella gestione dei set di dati [!DNL Profile] abilitati. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi [!DNL Platform] correlati:

- [[!DNL Real-time Customer Profile]](../home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Identity Service]](../../identity-service/home.md): Consente  [!DNL Real-time Customer Profile] di colmare le identità provenienti da origini dati diverse in cui viene eseguito il caricamento  [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): Un&#39;API RESTful che consente di creare set di dati e configurarli per  [!DNL Real-time Customer Profile] e  [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standard con cui  [!DNL Platform] organizzare i dati relativi all&#39;esperienza dei clienti.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente chiamate alle API della piattaforma.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a2/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione. Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione di [panoramica sulla sandbox](../../sandboxes/home.md).

- x-sandbox-name: `{SANDBOX_NAME}`

## Creare un set di dati abilitato per [!DNL Profile] e [!DNL Identity] {#create-a-dataset-enabled-for-profile-and-identity}

È possibile abilitare un dataset per [!DNL Real-time Customer Profile] e [!DNL Identity Service] immediatamente dopo la creazione o in qualsiasi momento dopo la creazione del dataset. Se si desidera abilitare un dataset già creato, seguire i passaggi per [configurare un dataset esistente](#configure-an-existing-dataset) trovato più avanti in questo documento. Per creare un nuovo set di dati, è necessario conoscere l&#39;ID di uno schema XDM esistente abilitato per il profilo cliente in tempo reale. Per informazioni su come ricercare o creare uno schema abilitato per il profilo, vedere l&#39;esercitazione su [creazione di uno schema tramite l&#39;API del Registro di sistema dello schema](../../xdm/tutorials/create-schema-api.md). La seguente chiamata all&#39;API [!DNL Catalog] abilita un dataset per [!DNL Profile] e [!DNL Identity Service].

**Formato API**

```http
POST /dataSets
```

**Richiesta**

Inserendo `unifiedProfile` e `unifiedIdentity` in `tags` nel corpo della richiesta, il set di dati sarà immediatamente abilitato per [!DNL Profile] e [!DNL Identity Service], rispettivamente. I valori di questi tag devono essere una matrice contenente la stringa `"enabled:true"`.

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
| `schemaRef.id` | ID dello schema [!DNL Profile] abilitato su cui verrà basato il dataset. |
| `{TENANT_ID}` | Lo spazio dei nomi all&#39;interno di [!DNL Schema Registry] che contiene risorse appartenenti all&#39;organizzazione IMS. Per ulteriori informazioni, vedere la sezione [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) della guida per gli sviluppatori [!DNL Schema Registry]. |

**Risposta**

Una risposta corretta mostra un array contenente l&#39;ID del set di dati appena creato, sotto forma di `"@/dataSets/{DATASET_ID}"`. Dopo aver creato e attivato correttamente un dataset, procedere con i passaggi per [caricare i dati](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurare un dataset esistente {#configure-an-existing-dataset}

I passaggi seguenti descrivono come abilitare un dataset creato in precedenza per [!DNL Real-time Customer Profile] e [!DNL Identity Service]. Se hai già creato un dataset abilitato per il profilo, procedi con i passaggi per [assimilare i dati](#ingest-data-into-the-dataset).

### Verifica se il set di dati è abilitato {#check-if-the-dataset-is-enabled}

Utilizzando l&#39;API [!DNL Catalog], potete ispezionare un dataset esistente per determinare se è abilitato per l&#39;uso in [!DNL Real-time Customer Profile] e [!DNL Identity Service]. La seguente chiamata recupera i dettagli di un set di dati per ID.

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

Sotto la proprietà `tags` è possibile vedere che `unifiedProfile` e `unifiedIdentity` sono entrambi presenti con il valore `enabled:true`. Di conseguenza, [!DNL Real-time Customer Profile] e [!DNL Identity Service] sono abilitati rispettivamente per questo dataset.

### Abilitare il set di dati {#enable-the-dataset}

Se il set di dati esistente non è stato abilitato per [!DNL Profile] o [!DNL Identity Service], è possibile abilitarlo effettuando una richiesta di PATCH utilizzando l&#39;ID del set di dati.

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

Il corpo della richiesta include una proprietà `tags`, che contiene due proprietà secondarie: `"unifiedProfile"` e `"unifiedIdentity"`. I valori di queste proprietà secondarie sono matrici contenenti la stringa `"enabled:true"`.

**La richiesta di PATCH**
ResponseUna richiesta riuscita restituisce lo stato HTTP 200 (OK) e una matrice contenente l&#39;ID del set di dati aggiornato. Questo ID deve corrispondere a quello inviato nella richiesta PATCH. Sono stati aggiunti i tag `"unifiedProfile"` e `"unifiedIdentity"` e il set di dati è abilitato per l&#39;uso da parte dei servizi di identità e profilo.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Inserire i dati nel set di dati {#ingest-data-into-the-dataset}

Sia [!DNL Real-time Customer Profile] che [!DNL Identity Service] utilizzano i dati XDM durante l&#39;assimilazione in un dataset. Per istruzioni su come caricare i dati in un dataset, fare riferimento all&#39;esercitazione su [creazione di un set di dati tramite APIs](../../catalog/datasets/create.md). Quando pianificate quali dati inviare al dataset abilitato [!DNL Profile], tenete presenti le seguenti procedure ottimali:

- Includete tutti i dati che desiderate utilizzare come criteri di segmento dell&#39;audience.
- Includi tutti gli identificatori che puoi verificare dai dati del tuo profilo per massimizzare il grafico di identità. Questo consente a [!DNL Identity Service] di unire più efficacemente le identità tra i set di dati.

## Confermare l&#39;acquisizione dei dati per [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Quando si caricano i dati in un nuovo dataset per la prima volta, o come parte di un processo che coinvolge una nuova ETL o una nuova origine dati, si consiglia di controllare attentamente i dati per assicurarsi che siano stati caricati come previsto. Utilizzando l&#39;API di accesso [!DNL Real-time Customer Profile] è possibile recuperare i dati batch mentre vengono caricati in un dataset. Se non è possibile recuperare nessuna delle entità previste, il set di dati potrebbe non essere abilitato per [!DNL Real-time Customer Profile]. Dopo aver confermato che il set di dati è stato abilitato, accertati che il formato e gli identificatori dei dati di origine supportino le tue aspettative. Per istruzioni dettagliate su come utilizzare l&#39;API [!DNL Real-time Customer Profile] per accedere ai dati [!DNL Profile], seguire la guida [alle entità endpoint](../api/entities.md), nota anche come &quot;[!DNL Profile Access] API&quot;.

## Conferma acquisizione dati da parte del servizio identità {#confirm-data-ingest-by-identity-service}

Ogni frammento di dati inserito contenente più identità crea un collegamento nel grafico dell&#39;identità privata. Per ulteriori informazioni sui grafici di identità e sui dati di identità, leggere la [Panoramica del servizio identità](../../identity-service/home.md).