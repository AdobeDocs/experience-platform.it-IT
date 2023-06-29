---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;abilitare set di dati
title: Abilitare un set di dati per gli aggiornamenti del profilo tramite API
type: Tutorial
description: Questa esercitazione mostra come utilizzare le API di Adobe Experience Platform per abilitare un set di dati con funzionalità di "upsert" per apportare aggiornamenti ai dati del profilo cliente in tempo reale.
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: 6985ebf8705130636abdc50b5c3f50299a60f2aa
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 2%

---

# Abilitare un set di dati per gli aggiornamenti dei profili tramite API

Questa esercitazione illustra il processo di abilitazione di un set di dati con funzionalità di &quot;upsert&quot; per apportare aggiornamenti ai dati del profilo cliente in tempo reale. Ciò include i passaggi per creare un nuovo set di dati e configurare un set di dati esistente.

>[!NOTE]
>
>Il flusso di lavoro descritto in questa esercitazione funziona solo per l’acquisizione in batch. Per i programmi upsert di acquisizione in streaming, consulta la guida su [invio di aggiornamenti parziali delle righe a Real-Time Customer Profile tramite la preparazione dati](../../data-prep/upserts.md).

## Introduzione

Questo tutorial richiede una buona conoscenza di diversi servizi Adobe Experience Platform coinvolti nella gestione dei set di dati abilitati per il profilo. Prima di iniziare questo tutorial, consulta la documentazione relativa a [!DNL Platform] servizi:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Catalog Service]](../../catalog/home.md): API RESTful che consente di creare set di dati e configurarli per [!DNL Real-Time Customer Profile] e [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Platform] organizza i dati sull’esperienza del cliente.
- [Acquisizione in batch](../../ingestion/batch-ingestion/overview.md): l’API per l’acquisizione in batch consente di acquisire i dati in Experience Platform come file batch.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente le chiamate alle API di Platform.

### Lettura delle chiamate API di esempio

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nel [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori per le intestazioni richieste

Per effettuare chiamate a [!DNL Platform] , devi prima completare le [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un ulteriore `Content-Type` intestazione. Il valore corretto per questa intestazione viene mostrato nelle richieste di esempio, se necessario.

Tutte le risorse in [!DNL Experience Platform] sono isolati in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un `x-sandbox-name` intestazione che specifica il nome della sandbox in cui verrà eseguita l’operazione. Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedere [documentazione di panoramica sulla sandbox](../../sandboxes/home.md).

## Creare un set di dati abilitato per gli aggiornamenti del profilo

Quando crei un nuovo set di dati, puoi abilitarlo per il profilo e abilitare le funzionalità di aggiornamento al momento della creazione.

>[!NOTE]
>
>Per creare un nuovo set di dati abilitato per il profilo, è necessario conoscere l’ID di uno schema XDM esistente abilitato per il profilo. Per informazioni su come cercare o creare uno schema abilitato per il profilo, consulta l’esercitazione su [creazione di uno schema tramite l’API Schema Registry](../../xdm/tutorials/create-schema-api.md).

Per creare un set di dati abilitato per Profilo e aggiornamenti, utilizza una richiesta POST al `/dataSets` endpoint.

**Formato API**

```http
POST /dataSets
```

**Richiesta**

Includendo entrambi `unifiedIdentity` e `unifiedProfile` in `tags` nel corpo della richiesta, il set di dati verrà abilitato per [!DNL Profile] alla creazione. All&#39;interno del `unifiedProfile` array, aggiunta `isUpsert:true` aggiunge la possibilità per il set di dati di supportare gli aggiornamenti.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Sample dataset",
        "description: "A sample dataset with a sample description.",
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
| `schemaRef.id` | ID del [!DNL Profile]Schema abilitato su cui verrà basato il set di dati. |
| `{TENANT_ID}` | Lo spazio dei nomi all’interno del [!DNL Schema Registry] che contiene risorse appartenenti alla tua organizzazione. Consulta la [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) sezione del [!DNL Schema Registry] guida per gli sviluppatori per ulteriori informazioni. |

**Risposta**

In caso di esito positivo, la risposta mostra un array contenente l’ID del set di dati appena creato sotto forma di `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurare un set di dati esistente {#configure-an-existing-dataset}

I passaggi seguenti descrivono come configurare un set di dati esistente abilitato per il profilo per la funzionalità di aggiornamento (upsert).

>[!NOTE]
>
>Per configurare un set di dati esistente abilitato per il profilo per l’upsert, devi prima disabilitare il set di dati per il profilo e quindi abilitarlo di nuovo insieme al `isUpsert` tag. Se il set di dati esistente non è abilitato per il profilo, puoi procedere direttamente ai passaggi per [abilitazione del set di dati per Profilo e upsert](#enable-the-dataset). In caso di dubbi, i passaggi seguenti mostrano come verificare se il set di dati è già abilitato.

### Verifica se il set di dati è abilitato per il profilo

Utilizzo di [!DNL Catalog] API, è possibile esaminare un set di dati esistente per determinare se è abilitato per l’utilizzo in [!DNL Real-Time Customer Profile]. La chiamata seguente recupera i dettagli di un set di dati per ID.

**Formato API**

```http
GET /dataSets/{DATASET_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASET_ID}` | ID di un set di dati da controllare. |

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
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "{VIEW_ID}",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "{SCHEMA}",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

Sotto `tags` proprietà, puoi vedere che `unifiedProfile` è presente con il valore `enabled:true`. Pertanto, [!DNL Real-Time Customer Profile] è abilitato per questo set di dati.

### Disattiva il set di dati per il profilo

Per configurare un set di dati abilitato per i profili per gli aggiornamenti, devi prima disabilitare il `unifiedProfile` e `unifiedIdentity` e quindi abilitarli di nuovo insieme alla `isUpsert` tag. Questa operazione viene eseguita utilizzando due richieste PATCH, una per disabilitare e una per riabilitare.

>[!WARNING]
>
>I dati acquisiti nel set di dati mentre è disabilitato non verranno acquisiti nell’archivio profili. Evita di acquisire i dati nel set di dati fino a quando non vengono riabilitati per il profilo.

**Formato API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASET_ID}` | ID del set di dati da aggiornare. |

**Richiesta**

Il primo corpo della richiesta PATCH include `path` a `unifiedProfile` e un `path` a `unifiedIdentity`, impostazione di `value` a `enabled:false` per entrambi questi percorsi, al fine di disabilitare i tag.

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

In caso di esito positivo, la richiesta PATCH restituisce lo stato HTTP 200 (OK) e una matrice contenente l’ID del set di dati aggiornato. Questo ID deve corrispondere a quello inviato nella richiesta PATCH. Il `unifiedProfile` e `unifiedIdentity` I tag ora sono stati disattivati.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### Abilita il set di dati per Profilo e upsert {#enable-the-dataset}

È possibile abilitare un set di dati esistente per gli aggiornamenti di profili e attributi utilizzando una singola richiesta PATCH.

>[!IMPORTANT]
>
>Quando abiliti il set di dati per il profilo, assicurati che lo schema a cui è associato il set di dati sia **anche** Abilitato per il profilo. Se lo schema non è abilitato per il profilo, il set di dati **non** nell’interfaccia utente di Platform, vengono visualizzati come abilitati per il profilo.

**Formato API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASET_ID}` | ID di un set di dati da aggiornare. |

**Richiesta**

Il corpo della richiesta include `path` a `unifiedProfile` impostazione di `value` per includere `enabled` e `isUpsert` tag, entrambi impostati su `true`, e un `path` a `unifiedIdentity` impostazione di `value` per includere `enabled` tag impostato su `true`.

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

In caso di esito positivo, la richiesta PATCH restituisce lo stato HTTP 200 (OK) e una matrice contenente l’ID del set di dati aggiornato. Questo ID deve corrispondere a quello inviato nella richiesta PATCH. Il `unifiedProfile` tag e `unifiedIdentity` tag ora sono stati abilitati e configurati per gli aggiornamenti degli attributi.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Passaggi successivi

Ora è possibile utilizzare il profilo e il set di dati abilitato per l’upsert tramite flussi di lavoro di acquisizione batch per apportare aggiornamenti ai dati del profilo. Per ulteriori informazioni sull’acquisizione di dati in Adobe Experience Platform, consulta la sezione [panoramica sull’acquisizione dei dati](../../ingestion/home.md).
