---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;abilita set di dati
title: Abilitare un set di dati per gli aggiornamenti dei profili tramite API
type: Tutorial
description: Questa esercitazione mostra come utilizzare le API di Adobe Experience Platform per abilitare un set di dati con funzionalità di "upsert" al fine di eseguire aggiornamenti ai dati del profilo cliente in tempo reale.
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: 5bd3e43e6b307cc1527e8734936c051fb4fc89c4
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 2%

---

# Abilitare un set di dati per gli aggiornamenti dei profili tramite API

Questa esercitazione descrive il processo di abilitazione di un set di dati con funzionalità &quot;upsert&quot; per effettuare aggiornamenti ai dati del profilo cliente in tempo reale. Ciò include passaggi per la creazione di un nuovo set di dati e la configurazione di un set di dati esistente.

>[!NOTE]
>
>Il flusso di lavoro upsert funziona solo per l’acquisizione batch. L’acquisizione in streaming è **not** supportato.

## Introduzione

Questa esercitazione richiede una comprensione approfondita di diversi servizi Adobe Experience Platform coinvolti nella gestione dei set di dati abilitati per il profilo. Prima di iniziare questa esercitazione, consulta la documentazione relativa a [!DNL Platform] servizi:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Catalog Service]](../../catalog/home.md): API RESTful che consente di creare set di dati e configurarli per [!DNL Real-time Customer Profile] e [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il quadro standardizzato [!DNL Platform] organizza i dati sulla customer experience.
- [Acquisizione batch](../../ingestion/batch-ingestion/overview.md): L’API di acquisizione in batch consente di inserire dati in Experience Platform come file batch.

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

## Creare un set di dati abilitato per gli aggiornamenti dei profili

Quando crei un nuovo set di dati, puoi abilitarlo per Profilo e abilitare le funzionalità di aggiornamento al momento della creazione.

>[!NOTE]
>
>Per creare un nuovo set di dati abilitato per il profilo, devi conoscere l’ID di uno schema XDM esistente abilitato per il profilo. Per informazioni su come cercare o creare uno schema abilitato per il profilo, consulta l’esercitazione su [creazione di uno schema tramite l’API del Registro di sistema dello schema](../../xdm/tutorials/create-schema-api.md).

Per creare un set di dati abilitato per Profilo e aggiornamenti, utilizza una richiesta di POST per `/dataSets` punto finale.

**Formato API**

```http
POST /dataSets
```

**Richiesta**

Includendo entrambi i `unifiedIdentity` e `unifiedProfile` sotto `tags` nel corpo della richiesta, il set di dati sarà abilitato per [!DNL Profile] al momento della creazione. All&#39;interno di `unifiedProfile` array, aggiunta `isUpsert:true` aggiunge la possibilità per il set di dati di supportare gli aggiornamenti.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "fields": [],
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "unifiedIdentity": [
                "enabled: true"
            ],
            "unifiedProfile": [
                "enabled: true",
                "isUpsert: true"
            ]
        }
      }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `schemaRef.id` | ID del [!DNL Profile]schema abilitato su cui verrà basato il set di dati. |
| `{TENANT_ID}` | Lo spazio dei nomi all’interno del [!DNL Schema Registry] che contiene risorse appartenenti all’organizzazione. Consulta la sezione [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) della sezione [!DNL Schema Registry] guida per sviluppatori per ulteriori informazioni. |

**Risposta**

Una risposta corretta mostra un array contenente l’ID del set di dati appena creato sotto forma di `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurare un set di dati esistente {#configure-an-existing-dataset}

I passaggi seguenti spiegano come configurare un set di dati esistente abilitato per il profilo per la funzionalità di aggiornamento (upsert).

>[!NOTE]
>
>Per configurare un set di dati abilitato per il profilo esistente per l’aggiornamento, devi prima disabilitare il set di dati per il profilo e quindi riabilitarlo insieme al `isUpsert` tag . Se il set di dati esistente non è abilitato per Profilo, puoi procedere direttamente ai passaggi per [abilitazione del set di dati per Profilo e aggiornamento](#enable-the-dataset). Se non sei sicuro, i passaggi seguenti mostrano come verificare se il set di dati è già abilitato.

### Controlla se il set di dati è abilitato per Profilo

Utilizzo della [!DNL Catalog] API, puoi controllare un set di dati esistente per determinare se è abilitato per l’utilizzo in [!DNL Real-time Customer Profile]. La chiamata seguente recupera i dettagli di un set di dati per ID.

**Formato API**

```http
GET /dataSets/{DATASET_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASET_ID}` | ID di un set di dati da esaminare. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "{DATASET_NAME}",
        "imsOrg": "{ORG_ID}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ],
            "unifiedProfile": [
                "enabled:true"
            ]
        },
        "lastBatchId": "{BATCH_ID}",
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
        "viewId": "{VIEW_ID}",
        "status": "enabled",
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "{SCHEMA}",
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

Sotto la `tags` puoi vedere che `unifiedProfile` è presente con il valore `enabled:true`. Pertanto, [!DNL Real-time Customer Profile] è abilitato per questo set di dati.

### Disattiva il set di dati per il profilo

Per configurare un set di dati abilitato per il profilo per gli aggiornamenti, devi prima disabilitare il `unifiedProfile` e `unifiedIdentity` e quindi riattivarli insieme ai tag `isUpsert` tag . Questa operazione viene eseguita utilizzando due richieste PATCH, una volta per disabilitare e una per riabilitare.

>[!WARNING]
>
>I dati acquisiti nel set di dati quando è disattivato non verranno acquisiti nell’archivio profili. Evita di acquisire i dati nel set di dati fino a quando non è stato riabilitato per Profilo.

**Formato API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASET_ID}` | ID del set di dati da aggiornare. |

**Richiesta**

Il primo corpo della richiesta di PATCH include un `path` a `unifiedProfile` e `path` a `unifiedIdentity`, impostando `value` a `enabled:false` per entrambi i percorsi per disabilitare i tag.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "replace", 
            "path": "/tags/unifiedProfile", 
            "value": ["enabled:false"] 
        },
        {
            "op": "replace",
            "path": "/tags/unifiedIdentity",
            "value": ["enabled:false"]
        }
      ]'
```

**Risposta**

Una richiesta PATCH corretta restituisce lo stato HTTP 200 (OK) e un array contenente l&#39;ID del set di dati aggiornato. Questo ID deve corrispondere a quello inviato nella richiesta di PATCH. La `unifiedProfile` e `unifiedIdentity` I tag sono stati disattivati.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### Abilita il set di dati per Profilo e aggiornamento {#enable-the-dataset}

Un set di dati esistente può essere abilitato per gli aggiornamenti di profili e attributi utilizzando una singola richiesta PATCH.

**Formato API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASET_ID}` | ID di un set di dati da aggiornare. |

**Richiesta**

Il corpo della richiesta include un `path` a `unifiedProfile` impostazione `value` per includere `enabled` e `isUpsert` tag, entrambi impostati su `true`e `path` a `unifiedIdentity` impostazione `value` per includere `enabled` è impostato su `true`.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "add", 
            "path": "/tags/unifiedProfile", 
            "value": [
                "enabled:true",
                "isUpsert:true"
            ] 
        },
        {
            "op": "add",
            "path": "/tags/unifiedIdentity",
            "value": [
                "enabled:true"
            ]
        }
      ]'
```

**Risposta**

Una richiesta PATCH corretta restituisce lo stato HTTP 200 (OK) e un array contenente l&#39;ID del set di dati aggiornato. Questo ID deve corrispondere a quello inviato nella richiesta di PATCH. La `unifiedProfile` tag e `unifiedIdentity` Il tag è stato ora abilitato e configurato per gli aggiornamenti degli attributi.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Passaggi successivi

Il tuo profilo e il set di dati abilitato per gli utenti possono ora essere utilizzati dai flussi di lavoro di acquisizione batch per effettuare aggiornamenti ai dati del profilo. Per ulteriori informazioni sull’acquisizione di dati in Adobe Experience Platform, consulta la sezione [panoramica sull’acquisizione dei dati](../../ingestion/home.md).
