---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;abilita set di dati
title: Abilitare un set di dati per gli aggiornamenti dei profili tramite API
type: Tutorial
description: Questa esercitazione mostra come utilizzare le API di Adobe Experience Platform per abilitare un set di dati con funzionalità di "upsert" al fine di eseguire aggiornamenti ai dati del profilo cliente in tempo reale.
source-git-commit: 3b34cf37182ae98545651a7b54f586df7d811f34
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 2%

---


# Abilitare un set di dati per gli aggiornamenti dei profili tramite API

Questa esercitazione descrive il processo di abilitazione di un set di dati con funzionalità &quot;upsert&quot; per effettuare aggiornamenti ai dati del profilo cliente in tempo reale. Ciò include passaggi per la creazione di un nuovo set di dati e la configurazione di un set di dati esistente.

## Introduzione

Questa esercitazione richiede una comprensione approfondita di diversi servizi Adobe Experience Platform coinvolti nella gestione dei set di dati abilitati per il profilo. Prima di iniziare questa esercitazione, consulta la documentazione relativa a questi servizi DNL Platform correlati:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Catalog Service]](../../catalog/home.md): API RESTful che consente di creare set di dati e configurarli per  [!DNL Real-time Customer Profile] e  [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Platform] vengono organizzati i dati sulla customer experience.
- [Acquisizione batch](../../ingestion/batch-ingestion/overview.md)

Le sezioni seguenti forniscono informazioni aggiuntive che dovrai conoscere per effettuare correttamente le chiamate alle API di Platform.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva `Content-Type`. Il valore corretto per questa intestazione viene mostrato nelle richieste di esempio, se necessario.

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione `x-sandbox-name` che specifica il nome della sandbox in cui avrà luogo l’operazione. Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la documentazione di panoramica [sandbox](../../sandboxes/home.md).

## Creare un set di dati abilitato per gli aggiornamenti dei profili

Quando crei un nuovo set di dati, puoi abilitarlo per Profilo e abilitare le funzionalità di aggiornamento al momento della creazione.

>[!NOTE]
>
>Per creare un nuovo set di dati abilitato per il profilo, devi conoscere l’ID di uno schema XDM esistente abilitato per il profilo. Per informazioni su come cercare o creare uno schema abilitato per il profilo, consulta l’esercitazione su [creazione di uno schema utilizzando l’API del Registro di sistema dello schema](../../xdm/tutorials/create-schema-api.md).

Per creare un set di dati abilitato per Profilo e aggiornamenti, utilizza una richiesta POST all’endpoint `/dataSets` .

**Formato API**

```http
POST /dataSets
```

**Richiesta**

Inserendo `unifiedProfile` in `tags` nel corpo della richiesta, il set di dati verrà abilitato per [!DNL Profile] al momento della creazione. All’interno della matrice `unifiedProfile`, l’aggiunta di `isUpsert:true` consentirà al set di dati di supportare gli aggiornamenti.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "fields":[],
        "schemaRef" : {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
          "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags" : {
          "unifiedProfile": [
            "enabled:true",
            "isUpsert:true"
          ]
        }
      }'
```

| Proprietà | Descrizione |
|---|---|
| `schemaRef.id` | ID dello schema abilitato [!DNL Profile] su cui verrà basato il set di dati. |
| `{TENANT_ID}` | Lo spazio dei nomi all’interno di [!DNL Schema Registry] che contiene risorse appartenenti all’organizzazione IMS. Per ulteriori informazioni, consulta la sezione [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) della guida per gli sviluppatori [!DNL Schema Registry] . |

**Risposta**

Una risposta corretta mostra un array contenente l’ID del set di dati appena creato sotto forma di `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurare un set di dati esistente {#configure-an-existing-dataset}

I passaggi seguenti spiegano come configurare un set di dati esistente abilitato per il profilo per la funzionalità di aggiornamento (&quot;upsert&quot;).

>[!NOTE]
>
>Per configurare un set di dati abilitato per il profilo esistente per l’utente, devi prima disabilitare il set di dati per il profilo e quindi riabilitarlo insieme al tag `isUpsert` . Se il set di dati esistente non è abilitato per Profilo, puoi procedere direttamente ai passaggi per [abilitare il set di dati per Profilo e aggiornare](#enable-the-dataset). Se non sei sicuro, i passaggi seguenti mostrano come verificare se il set di dati è già abilitato.

### Controlla se il set di dati è abilitato per Profilo

Utilizzando l’API [!DNL Catalog], puoi controllare un set di dati esistente per determinare se è abilitato per l’utilizzo in [!DNL Real-time Customer Profile]. La chiamata seguente recupera i dettagli di un set di dati per ID.

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
        "name": "{DATASET_NAME}",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
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

Sotto la proprietà `tags` , puoi vedere che `unifiedProfile` è presente con il valore `enabled:true`. Pertanto, [!DNL Real-time Customer Profile] è abilitato per questo set di dati.

### Disattiva il set di dati per il profilo

Per configurare un set di dati abilitato per il profilo per gli aggiornamenti, devi prima disabilitare il tag `unifiedProfile` e quindi riabilitarlo insieme al tag `isUpsert` . Questa operazione viene eseguita utilizzando due richieste PATCH, una volta per disabilitare e una per riabilitare.

>[!WARNING]
>
>I dati acquisiti nel set di dati quando è disattivato non verranno acquisiti nell’archivio profili. Si consiglia di evitare di acquisire dati nel set di dati fino a quando non viene riabilitato per Profilo.

**Formato API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parametro | Descrizione |
|---|---|
| `{DATASET_ID}` | ID di un set di dati da aggiornare. |

**Richiesta**

Il primo corpo della richiesta PATCH include un tag `path` in `unifiedProfile` che imposta il tag `value` su `enabled:false` per disattivarlo.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "replace", "path": "/tags/unifiedProfile", "value": ["enabled:false"] },
      ]'
```

****
ResponseUna richiesta PATCH riuscita restituisce lo stato HTTP 200 (OK) e un array contenente l&#39;ID del set di dati aggiornato. Questo ID deve corrispondere a quello inviato nella richiesta di PATCH. Il tag `unifiedProfile` è stato disattivato.

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
|---|---|
| `{DATASET_ID}` | ID di un set di dati da aggiornare. |

**Richiesta**

Il corpo della richiesta include un tag `path` in `unifiedProfile` che imposta il tag `value` per includere i tag `enabled` e `isUpsert`, entrambi impostati su `true`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true","isUpsert:true"] },
      ]'
```

****
ResponseUna richiesta PATCH riuscita restituisce lo stato HTTP 200 (OK) e un array contenente l&#39;ID del set di dati aggiornato. Questo ID deve corrispondere a quello inviato nella richiesta di PATCH. Il tag `unifiedProfile` è ora abilitato e configurato per gli aggiornamenti degli attributi.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Passaggi successivi

Il set di dati abilitato per profili e per gli utenti può ora essere utilizzato dai flussi di lavoro di acquisizione in batch e in streaming per apportare aggiornamenti ai dati del profilo. Per ulteriori informazioni sull&#39;acquisizione di dati in Adobe Experience Platform, inizia leggendo la [panoramica sull&#39;acquisizione di dati](../../ingestion/home.md).
