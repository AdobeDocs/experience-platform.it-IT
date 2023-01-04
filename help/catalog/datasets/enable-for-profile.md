---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;abilita set di dati
title: Abilitare un set di dati per il servizio Profilo e identità utilizzando le API
type: Tutorial
description: Questa esercitazione mostra come abilitare un set di dati per l’utilizzo con Profilo cliente in tempo reale e il servizio Identity utilizzando le API di Adobe Experience Platform.
exl-id: a115e126-6775-466d-ad7e-ee36b0b8b49c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 1%

---

# Abilita un set di dati per [!DNL Profile] e [!DNL Identity Service] utilizzo delle API

Questa esercitazione descrive il processo di abilitazione di un set di dati da utilizzare in [!DNL Real-Time Customer Profile] e [!DNL Identity Service], suddivisi nei seguenti passaggi:

1. Abilita un set di dati da utilizzare in [!DNL Real-Time Customer Profile], utilizzando una delle due opzioni seguenti:
   - [Creare un nuovo set di dati](#create-a-dataset-enabled-for-profile-and-identity)
   - [Configurare un set di dati esistente](#configure-an-existing-dataset)
1. [Inserire dati nel set di dati](#ingest-data-into-the-dataset)
1. [Conferma l’acquisizione dei dati per profilo cliente in tempo reale](#confirm-data-ingest-by-real-time-customer-profile)
1. [Conferma dell’acquisizione dei dati da parte del servizio Identity](#confirm-data-ingest-by-identity-service)

## Introduzione

Questa esercitazione richiede una comprensione approfondita di diversi servizi Adobe Experience Platform coinvolti nella gestione dei set di dati abilitati per il profilo. Prima di iniziare questa esercitazione, consulta la documentazione relativa a [!DNL Platform] servizi:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Identity Service]](../../identity-service/home.md): Abilita [!DNL Real-Time Customer Profile] colmando le identità di diverse fonti di dati che vengono ingerite in [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): API RESTful che consente di creare set di dati e configurarli per [!DNL Real-Time Customer Profile] e [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il quadro standardizzato [!DNL Platform] organizza i dati sulla customer experience.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrai conoscere per effettuare correttamente le chiamate alle API di Platform.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un `Content-Type` intestazione. Il valore corretto per questa intestazione viene mostrato nelle richieste di esempio, se necessario.

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un `x-sandbox-name` intestazione che specifica il nome della sandbox in cui verrà effettuata l’operazione. Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione panoramica su sandbox](../../sandboxes/home.md).

## Creare un set di dati abilitato per Profilo e identità {#create-a-dataset-enabled-for-profile-and-identity}

Puoi abilitare un set di dati per Profilo cliente in tempo reale e Servizio identità immediatamente dopo la creazione o in qualsiasi momento dopo la creazione del set di dati. Se desideri abilitare un set di dati già creato, segui i passaggi per [configurazione di un set di dati esistente](#configure-an-existing-dataset) trovato più avanti in questo documento.

>[!NOTE]
>
>Per creare un nuovo set di dati abilitato per il profilo, devi conoscere l’ID di uno schema XDM esistente abilitato per il profilo. Per informazioni su come cercare o creare uno schema abilitato per il profilo, consulta l’esercitazione su [creazione di uno schema tramite l’API del Registro di sistema dello schema](../../xdm/tutorials/create-schema-api.md).

Per creare un set di dati abilitato per Profilo, puoi utilizzare una richiesta di POST per `/dataSets` punto finale.

**Formato API**

```http
POST /dataSets
```

**Richiesta**

Includendo `unifiedProfile` e `unifiedIdentity` sotto `tags` nel corpo della richiesta, il set di dati sarà immediatamente abilitato per [!DNL Profile] e [!DNL Identity Service], rispettivamente. I valori di questi tag devono essere una matrice contenente la stringa `"enabled:true"`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields":[],
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
    },
    "tags": {
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| Proprietà | Descrizione |
|---|---|
| `schemaRef.id` | ID del [!DNL Profile]schema abilitato su cui verrà basato il set di dati. |
| `{TENANT_ID}` | Lo spazio dei nomi all’interno del [!DNL Schema Registry] che contiene risorse appartenenti all’organizzazione IMS. Consulta la sezione [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) della sezione [!DNL Schema Registry] guida per sviluppatori per ulteriori informazioni. |

**Risposta**

Una risposta corretta mostra un array contenente l’ID del set di dati appena creato sotto forma di `"@/dataSets/{DATASET_ID}"`. Dopo aver creato e abilitato correttamente un set di dati, procedi ai passaggi per [caricamento dei dati](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurare un set di dati esistente {#configure-an-existing-dataset}

I passaggi seguenti spiegano come abilitare un set di dati creato in precedenza per [!DNL Real-Time Customer Profile] e [!DNL Identity Service]. Se hai già creato un set di dati abilitato per il profilo, procedi con i passaggi per [acquisizione di dati](#ingest-data-into-the-dataset).

### Controlla se il set di dati è abilitato {#check-if-the-dataset-is-enabled}

Utilizzo della [!DNL Catalog] API, puoi controllare un set di dati esistente per determinare se è abilitato per l’utilizzo in [!DNL Real-Time Customer Profile] e [!DNL Identity Service]. La chiamata seguente recupera i dettagli di un set di dati per ID.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "Commission Program Events DataSet",
        "imsOrg": "{ORG_ID}",
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
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "@/xdms/context/experienceevent",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

Sotto la `tags` puoi vedere che `unifiedProfile` e `unifiedIdentity` sono entrambi presenti con il valore `enabled:true`. Pertanto, [!DNL Real-Time Customer Profile] e [!DNL Identity Service] sono abilitati rispettivamente per questo set di dati.

### Abilitare il set di dati {#enable-the-dataset}

Se il set di dati esistente non è stato abilitato per [!DNL Profile] o [!DNL Identity Service], puoi abilitarlo effettuando una richiesta di PATCH utilizzando l’ID del set di dati.

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
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true"] },
        { "op": "add", "path": "/tags/unifiedIdentity", "value": ["enabled:true"] } 
      ]'
```

Il corpo della richiesta include un `path` a due tipi di tag, `unifiedProfile` e `unifiedIdentity`. La `value` di ciascuno sono array contenenti la stringa `enabled:true`.

**Risposta**
Una richiesta PATCH corretta restituisce lo stato HTTP 200 (OK) e un array contenente l&#39;ID del set di dati aggiornato. Questo ID deve corrispondere a quello inviato nella richiesta di PATCH. La `unifiedProfile` e `unifiedIdentity` Sono stati aggiunti dei tag e il set di dati è abilitato per i servizi Profilo e Identità .

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Inserire dati nel set di dati {#ingest-data-into-the-dataset}

Entrambi [!DNL Real-Time Customer Profile] e [!DNL Identity Service] utilizza i dati XDM durante l’acquisizione in un set di dati. Per istruzioni su come caricare dati in un set di dati, consulta l’esercitazione su [creazione di un set di dati tramite API](../../catalog/datasets/create.md). Quando pianifichi quali dati inviare al tuo [!DNL Profile]Set di dati abilitato, considera le seguenti best practice:

- Includi tutti i dati che desideri utilizzare come criteri di segmentazione.
- Includi tutti gli identificatori che puoi verificare dai dati del profilo per massimizzare il grafico delle identità. Ciò consente [!DNL Identity Service] unire le identità tra i set di dati in modo più efficace.

## Conferma dell’acquisizione dei dati per [!DNL Real-Time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Quando carichi i dati in un nuovo set di dati per la prima volta o come parte di un processo che coinvolge una nuova ETL o una nuova origine dati, è consigliabile controllare attentamente i dati per assicurarsi che siano stati caricati come previsto. Utilizzo della [!DNL Real-Time Customer Profile] Access API (API di accesso), è possibile recuperare dati batch durante il caricamento in un set di dati. Se non riesci a recuperare nessuna delle entità previste, il set di dati potrebbe non essere abilitato per [!DNL Real-Time Customer Profile]. Dopo aver confermato che il set di dati è stato abilitato, assicurati che il formato e gli identificatori dei dati di origine supportino le tue aspettative. Per istruzioni dettagliate su come utilizzare il [!DNL Real-Time Customer Profile] API per accedere [!DNL Profile] dati, fare riferimento alla [guida all’endpoint entità](../../profile/api/entities.md), noto anche come &quot;[!DNL Profile Access]&quot; API.

## Conferma dell’acquisizione dei dati da parte del servizio Identity {#confirm-data-ingest-by-identity-service}

Ogni frammento di dati acquisito che contiene più di un’identità crea un collegamento nel grafico della tua identità privata. Per ulteriori informazioni sui grafici di identità e sull&#39;accesso ai dati di identità, si prega di iniziare leggendo [Panoramica del servizio Identity](../../identity-service/home.md).
