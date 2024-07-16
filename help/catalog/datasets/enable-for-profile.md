---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;abilitare set di dati
title: Abilitare un set di dati per il profilo e il servizio Identity tramite API
type: Tutorial
description: Questa esercitazione mostra come abilitare un set di dati per l’utilizzo con Real-Time Customer Profile e Identity Service tramite le API di Adobe Experience Platform.
exl-id: a115e126-6775-466d-ad7e-ee36b0b8b49c
source-git-commit: b80d8349fc54a955ebb3362d67a482d752871420
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 6%

---

# Abilita un set di dati per [!DNL Profile] e [!DNL Identity Service] tramite API

Questo tutorial descrive il processo di abilitazione di un set di dati da utilizzare in [!DNL Real-Time Customer Profile] e [!DNL Identity Service], suddiviso nei seguenti passaggi:

1. Abilitare un set di dati per l&#39;utilizzo in [!DNL Real-Time Customer Profile] utilizzando una delle due opzioni seguenti:
   - [Creare un nuovo set di dati](#create-a-dataset-enabled-for-profile-and-identity)
   - [Configurare un set di dati esistente](#configure-an-existing-dataset)
1. [Inserire dati nel set di dati](#ingest-data-into-the-dataset)
1. [Conferma acquisizione dati da Real-Time Customer Profile](#confirm-data-ingest-by-real-time-customer-profile)
1. [Conferma acquisizione dati da parte di Identity Service](#confirm-data-ingest-by-identity-service)

## Introduzione

Questo tutorial richiede una buona conoscenza di diversi servizi Adobe Experience Platform coinvolti nella gestione dei set di dati abilitati per il profilo. Prima di iniziare questo tutorial, consulta la documentazione di questi servizi [!DNL Platform] correlati:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Identity Service]](../../identity-service/home.md): abilita [!DNL Real-Time Customer Profile] collegando identità da origini dati diverse acquisite in [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): API RESTful che consente di creare set di dati e configurarli per [!DNL Real-Time Customer Profile] e [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Platform] organizza i dati sull&#39;esperienza del cliente.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente le chiamate alle API di Platform.

### Lettura delle chiamate API di esempio

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione `Content-Type` aggiuntiva. Il valore corretto per questa intestazione viene mostrato nelle richieste di esempio, se necessario.

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione `x-sandbox-name` che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione. Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

## Creare un set di dati abilitato per Profilo e Identità {#create-a-dataset-enabled-for-profile-and-identity}

Puoi abilitare un set di dati per Real-Time Customer Profile e Identity Service immediatamente dopo la creazione o in qualsiasi momento dopo la creazione del set di dati. Se desideri abilitare un set di dati già creato, segui i passaggi per [configurare un set di dati esistente](#configure-an-existing-dataset) che si trova più avanti in questo documento.

>[!NOTE]
>
>Per creare un nuovo set di dati abilitato per il profilo, è necessario conoscere l’ID di uno schema XDM esistente abilitato per il profilo. Per informazioni su come cercare o creare uno schema abilitato per il profilo, vedere il tutorial su [creazione di uno schema tramite l&#39;API Schema Registry](../../xdm/tutorials/create-schema-api.md).

Per creare un set di dati abilitato per il profilo, è possibile utilizzare una richiesta POST all&#39;endpoint `/dataSets`.

**Formato API**

```http
POST /dataSets
```

**Richiesta**

Includendo `unifiedProfile` e `unifiedIdentity` in `tags` nel corpo della richiesta, il set di dati verrà immediatamente abilitato per [!DNL Profile] e [!DNL Identity Service], rispettivamente. I valori di questi tag devono essere una matrice contenente la stringa `"enabled:true"`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
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
| `schemaRef.id` | ID dello schema abilitato per [!DNL Profile] su cui verrà basato il set di dati. |
| `{TENANT_ID}` | Lo spazio dei nomi all&#39;interno di [!DNL Schema Registry] che contiene le risorse appartenenti alla tua organizzazione. Per ulteriori informazioni, vedere la sezione [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) della Guida per gli sviluppatori di [!DNL Schema Registry]. |

**Risposta**

In caso di esito positivo, la risposta mostra un array contenente l&#39;ID del set di dati appena creato sotto forma di `"@/dataSets/{DATASET_ID}"`. Dopo aver creato e attivato correttamente un set di dati, procedi con i passaggi per il [caricamento dei dati](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurare un set di dati esistente {#configure-an-existing-dataset}

Nei passaggi seguenti viene descritto come abilitare un set di dati creato in precedenza per [!DNL Real-Time Customer Profile] e [!DNL Identity Service]. Se hai già creato un set di dati abilitato per il profilo, procedi ai passaggi per [l&#39;acquisizione dei dati](#ingest-data-into-the-dataset).

### Controlla se il set di dati è abilitato {#check-if-the-dataset-is-enabled}

Utilizzando l&#39;API [!DNL Catalog], è possibile esaminare un set di dati esistente per determinare se è abilitato per l&#39;utilizzo in [!DNL Real-Time Customer Profile] e [!DNL Identity Service]. La chiamata seguente recupera i dettagli di un set di dati per ID.

**Formato API**

```http
GET /dataSets/{DATASET_ID}
```

| Parametro | Descrizione |
|---|---|
| `{DATASET_ID}` | ID di un set di dati da controllare. |

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
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "5b020a27e7040801dedbf46f",
        "files": "@/dataSetFiles?dataSetId=5b020a27e7040801dedbf46e",
        "schema": "@/xdms/context/experienceevent",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

Nella proprietà `tags`, è possibile vedere che `unifiedProfile` e `unifiedIdentity` sono entrambi presenti con il valore `enabled:true`. Pertanto, [!DNL Real-Time Customer Profile] e [!DNL Identity Service] sono abilitati rispettivamente per questo set di dati.

### Abilitare il set di dati {#enable-the-dataset}

Se il set di dati esistente non è stato abilitato per [!DNL Profile] o [!DNL Identity Service], è possibile abilitarlo effettuando una richiesta PATCH utilizzando l&#39;ID del set di dati.

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

Il corpo della richiesta include da `path` a due tipi di tag, `unifiedProfile` e `unifiedIdentity`. I `value` di ciascuno sono matrici contenenti la stringa `enabled:true`.

**Risposta**

In caso di esito positivo, la richiesta PATCH restituisce lo stato HTTP 200 (OK) e una matrice contenente l’ID del set di dati aggiornato. Questo ID deve corrispondere a quello inviato nella richiesta PATCH. I tag `unifiedProfile` e `unifiedIdentity` sono stati aggiunti e il set di dati è abilitato per l&#39;utilizzo da parte dei servizi Profilo e Identità.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Inserire dati nel set di dati {#ingest-data-into-the-dataset}

Sia [!DNL Real-Time Customer Profile] che [!DNL Identity Service] utilizzano dati XDM durante l&#39;acquisizione in un set di dati. Per istruzioni su come caricare dati in un set di dati, consulta l&#39;esercitazione su [creazione di un set di dati tramite API](../../catalog/datasets/create.md). Quando si pianificano i dati da inviare al set di dati abilitato per [!DNL Profile], prendere in considerazione le seguenti best practice:

- Includi tutti i dati da utilizzare come criteri di segmentazione.
- Includi tutti gli identificatori che puoi verificare dai dati del profilo per massimizzare il grafico delle identità. Questo consente a [!DNL Identity Service] di unire le identità in modo più efficace tra i set di dati.

## Conferma acquisizione dati da [!DNL Real-Time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Quando si caricano dati in un nuovo set di dati per la prima volta, o come parte di un processo che coinvolge una nuova ETL o sorgente di dati, si consiglia di controllare attentamente i dati per assicurarsi che siano stati caricati come previsto. Utilizzando l&#39;API di accesso [!DNL Real-Time Customer Profile], è possibile recuperare i dati batch durante il caricamento in un set di dati. Se non riesci a recuperare le entità previste, il set di dati potrebbe non essere abilitato per [!DNL Real-Time Customer Profile]. Dopo aver confermato che il set di dati è stato abilitato, assicurati che il formato e gli identificatori dei dati di origine supportino le aspettative. Per istruzioni dettagliate su come utilizzare l&#39;API [!DNL Real-Time Customer Profile] per accedere ai dati [!DNL Profile], fare riferimento alla [guida dell&#39;endpoint entità](../../profile/api/entities.md), nota anche come API &quot;[!DNL Profile Access]&quot;.

## Conferma dell’acquisizione dei dati da parte del servizio Identity {#confirm-data-ingest-by-identity-service}

Ogni frammento di dati acquisito che contiene più di un’identità crea un collegamento nel grafico dell’identità privata. Per ulteriori informazioni sui grafici delle identità e accedere ai dati delle identità, leggere la [panoramica del servizio Identity](../../identity-service/home.md).
