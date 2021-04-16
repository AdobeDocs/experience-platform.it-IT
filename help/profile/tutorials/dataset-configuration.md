---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;abilita set di dati
title: Configurare un set di dati per il servizio Profilo e identità utilizzando le API
topic: tutorial
type: Tutorial
description: Questa esercitazione mostra come abilitare un set di dati per l’utilizzo con Profilo cliente in tempo reale e il servizio Identity utilizzando le API di Adobe Experience Platform.
exl-id: 142cb7df-072a-4f3a-8a9c-9a78afb35312
translation-type: tm+mt
source-git-commit: 87729e4996b0b2ac26e1a0abaa80af717825f9e6
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 1%

---

# Configura un set di dati per [!DNL Profile] e [!DNL Identity Service] utilizzando le API

Questa esercitazione descrive il processo di abilitazione di un set di dati da utilizzare in [!DNL Real-time Customer Profile] e [!DNL Identity Service], suddivisi nei seguenti passaggi:

1. Abilita un set di dati da utilizzare in [!DNL Real-time Customer Profile] utilizzando una delle due opzioni seguenti:
   - [Creare un nuovo set di dati](#create-a-dataset-enabled-for-profile-and-identity)
   - [Configurare un set di dati esistente](#configure-an-existing-dataset)
1. [Inserire dati nel set di dati](#ingest-data-into-the-dataset)
1. [Conferma l’acquisizione dei dati per profilo cliente in tempo reale](#confirm-data-ingest-by-real-time-customer-profile)
1. [Conferma dell’acquisizione dei dati da parte del servizio Identity](#confirm-data-ingest-by-identity-service)

## Introduzione

Questa esercitazione richiede una comprensione approfondita dei vari servizi Adobe Experience Platform coinvolti nella gestione dei set di dati abilitati [!DNL Profile]. Prima di iniziare questa esercitazione, consulta la documentazione relativa a questi servizi [!DNL Platform] correlati:

- [[!DNL Real-time Customer Profile]](../home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Identity Service]](../../identity-service/home.md): Consente  [!DNL Real-time Customer Profile] di colmare le identità provenienti da origini dati diverse che vengono acquisite in  [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): API RESTful che consente di creare set di dati e configurarli per  [!DNL Real-time Customer Profile] e  [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Platform] vengono organizzati i dati sulla customer experience.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrai conoscere per effettuare correttamente le chiamate alle API di Platform.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Tipo di contenuto: application/json

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione. Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la documentazione di panoramica [sandbox](../../sandboxes/home.md).

- nome x-sandbox: `{SANDBOX_NAME}`

## Crea un set di dati abilitato per [!DNL Profile] e [!DNL Identity] {#create-a-dataset-enabled-for-profile-and-identity}

Puoi abilitare un set di dati per [!DNL Real-time Customer Profile] e [!DNL Identity Service] immediatamente dopo la creazione o in qualsiasi momento dopo la creazione del set di dati. Per abilitare un set di dati già creato, segui i passaggi per [configurare un set di dati esistente](#configure-an-existing-dataset) che si trovano più avanti in questo documento. Per creare un nuovo set di dati, devi conoscere l’ID di uno schema XDM esistente abilitato per Profilo cliente in tempo reale. Per informazioni su come cercare o creare uno schema abilitato per il profilo, consulta l’esercitazione su [creazione di uno schema utilizzando l’API del Registro di sistema dello schema](../../xdm/tutorials/create-schema-api.md). La seguente chiamata all’ API [!DNL Catalog] abilita un set di dati per [!DNL Profile] e [!DNL Identity Service].

**Formato API**

```http
POST /dataSets
```

**Richiesta**

Inserendo `unifiedProfile` e `unifiedIdentity` in `tags` nel corpo della richiesta, il set di dati verrà immediatamente abilitato per rispettivamente [!DNL Profile] e [!DNL Identity Service]. I valori di questi tag devono essere una matrice contenente la stringa `"enabled:true"`.

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
        "persisted": true
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
| `schemaRef.id` | ID dello schema abilitato [!DNL Profile] su cui verrà basato il set di dati. |
| `{TENANT_ID}` | Lo spazio dei nomi all’interno di [!DNL Schema Registry] che contiene risorse appartenenti all’organizzazione IMS. Per ulteriori informazioni, consulta la sezione [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) della guida per gli sviluppatori [!DNL Schema Registry] . |

**Risposta**

Una risposta corretta mostra un array contenente l’ID del set di dati appena creato sotto forma di `"@/dataSets/{DATASET_ID}"`. Dopo aver creato e abilitato correttamente un set di dati, procedi con i passaggi per [caricare i dati](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurare un set di dati esistente {#configure-an-existing-dataset}

I passaggi seguenti spiegano come abilitare un set di dati creato in precedenza per [!DNL Real-time Customer Profile] e [!DNL Identity Service]. Se hai già creato un set di dati abilitato per il profilo, procedi con i passaggi per [acquisizione di dati](#ingest-data-into-the-dataset).

### Verifica se il set di dati è abilitato {#check-if-the-dataset-is-enabled}

Utilizzando l’API [!DNL Catalog], puoi controllare un set di dati esistente per determinare se è abilitato per l’utilizzo in [!DNL Real-time Customer Profile] e [!DNL Identity Service]. La chiamata seguente recupera i dettagli di un set di dati per ID.

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
            "persisted": true
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

Sotto la proprietà `tags` , puoi vedere che `unifiedProfile` e `unifiedIdentity` sono entrambi presenti con il valore `enabled:true`. Pertanto, [!DNL Real-time Customer Profile] e [!DNL Identity Service] sono abilitati rispettivamente per questo set di dati.

### Abilita il set di dati {#enable-the-dataset}

Se il set di dati esistente non è stato abilitato per [!DNL Profile] o [!DNL Identity Service], puoi abilitarlo effettuando una richiesta PATCH utilizzando l’ID del set di dati.

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

Il corpo della richiesta include una proprietà `tags` che contiene due proprietà secondarie: `"unifiedProfile"` e `"unifiedIdentity"`. I valori di queste proprietà secondarie sono array contenenti la stringa `"enabled:true"`.

****
ResponseUna richiesta PATCH riuscita restituisce lo stato HTTP 200 (OK) e un array contenente l&#39;ID del set di dati aggiornato. Questo ID deve corrispondere a quello inviato nella richiesta di PATCH. I tag `"unifiedProfile"` e `"unifiedIdentity"` sono stati aggiunti e il set di dati è abilitato per l’uso da parte dei servizi Profilo e Identità.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Inserire dati nel set di dati {#ingest-data-into-the-dataset}

Sia [!DNL Real-time Customer Profile] che [!DNL Identity Service] utilizzano dati XDM durante l’acquisizione in un set di dati. Per istruzioni su come caricare i dati in un set di dati, consulta l’esercitazione su [creazione di un set di dati utilizzando le API](../../catalog/datasets/create.md). Quando pianifichi quali dati inviare al set di dati abilitato [!DNL Profile], prendi in considerazione le seguenti best practice:

- Includi tutti i dati che desideri utilizzare come criteri di segmento del pubblico.
- Includi tutti gli identificatori che puoi verificare dai dati del profilo per massimizzare il grafico delle identità. Questo consente a [!DNL Identity Service] di unire le identità tra i set di dati in modo più efficace.

## Conferma l’acquisizione dei dati per [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Quando carichi i dati in un nuovo set di dati per la prima volta o come parte di un processo che coinvolge una nuova ETL o una nuova origine dati, è consigliabile controllare attentamente i dati per assicurarsi che siano stati caricati come previsto. Utilizzando l’ API di accesso [!DNL Real-time Customer Profile] è possibile recuperare i dati batch caricati in un set di dati. Se non riesci a recuperare nessuna delle entità previste, il set di dati potrebbe non essere abilitato per [!DNL Real-time Customer Profile]. Dopo aver confermato che il set di dati è stato abilitato, assicurati che il formato e gli identificatori dei dati di origine supportino le tue aspettative. Per istruzioni dettagliate su come utilizzare l&#39;API [!DNL Real-time Customer Profile] per accedere ai dati [!DNL Profile], segui la [guida all&#39;endpoint entità](../api/entities.md), nota anche come API &quot;[!DNL Profile Access]&quot;.

## Conferma l’acquisizione dei dati da parte del servizio Identity {#confirm-data-ingest-by-identity-service}

Ogni frammento di dati acquisito che contiene più di un’identità crea un collegamento nel grafico della tua identità privata. Per ulteriori informazioni sui grafici di identità e sull’accesso ai dati di identità, inizia leggendo la [panoramica del servizio Identity](../../identity-service/home.md).
