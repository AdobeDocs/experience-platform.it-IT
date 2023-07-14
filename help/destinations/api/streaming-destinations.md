---
keywords: Experience Platform;home;argomenti popolari; esercitazioni API; destinazioni di streaming API; Platform
solution: Experience Platform
title: Connettersi alle destinazioni di streaming e attivare i dati utilizzando l’API del servizio Flusso in Adobe Experience Platform
description: Questo documento descrive la creazione di destinazioni di streaming utilizzando l’API Adobe Experience Platform
type: Tutorial
exl-id: 3e8d2745-8b83-4332-9179-a84d8c0b4400
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '2241'
ht-degree: 3%

---

# Connettersi alle destinazioni di streaming e attivare i dati utilizzando l’API del servizio Flow

>[!IMPORTANT]
> 
>Per connettersi a una destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions).
>
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions).
>
>Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Questo tutorial illustra come utilizzare le chiamate API per connettersi ai dati Adobe Experience Platform e creare una connessione a una destinazione di archiviazione cloud in streaming ([Amazon Kinesis](../catalog/cloud-storage/amazon-kinesis.md) o [Hub eventi di Azure](../catalog/cloud-storage/azure-event-hubs.md)), crea un flusso di dati nella nuova destinazione creata e attiva i dati nella nuova destinazione creata.

Questa esercitazione utilizza [!DNL Amazon Kinesis] destinazione in tutti gli esempi, ma i passaggi sono identici per [!DNL Azure Event Hubs].

![Panoramica: i passaggi per creare una destinazione di streaming e attivare i tipi di pubblico](../assets/api/streaming-destination/overview.png)

Se preferisci utilizzare l’interfaccia utente di Platform per connettersi a una destinazione e attivare i dati, consulta la sezione [Connettere una destinazione](../ui/connect-destination.md) e [Attiva i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../ui/activate-segment-streaming-destinations.md) esercitazioni.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull’esperienza del cliente.
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] è il sistema di registrazione per la posizione e la derivazione dei dati in Experience Platform.
* [Sandbox](../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per attivare i dati nelle destinazioni di streaming in Platform.

### Raccogli le credenziali richieste

Per completare i passaggi descritti in questa esercitazione, è necessario disporre delle seguenti credenziali pronte, a seconda del tipo di destinazioni a cui si connettono e si attivano i tipi di pubblico.

* Per [!DNL Amazon Kinesis] connessioni: `accessKeyId`, `secretKey`, `region` o `connectionUrl`
* Per [!DNL Azure Event Hubs] connessioni: `sasKeyName`, `sasKey`, `namespace`

### Lettura delle chiamate API di esempio {#reading-sample-api-calls}

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

### Raccogli i valori per le intestazioni obbligatorie e facoltative {#gather-values}

Per effettuare chiamate alle API di Platform, devi prima completare la sezione [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* Autorizzazione: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Le risorse di Experience Platform possono essere isolate in specifiche sandbox virtuali. Nelle richieste alle API di Platform, puoi specificare il nome e l’ID della sandbox in cui verrà eseguita l’operazione. Si tratta di parametri facoltativi.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Experience Platform, consulta la sezione [documentazione di panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* Content-Type: `application/json`

### Documentazione di Swagger {#swagger-docs}

Puoi trovare la documentazione di riferimento di accompagnamento per tutte le chiamate API in questa esercitazione in Swagger. Consulta la [Documentazione API del servizio Flusso su Adobe I/O](https://www.adobe.io/experience-platform-apis/references/flow-service/). È consigliabile utilizzare questa esercitazione e la pagina della documentazione di Swagger in parallelo.

## Ottieni l’elenco delle destinazioni di streaming disponibili {#get-the-list-of-available-streaming-destinations}

![Panoramica dei passaggi di destinazione passaggio 1](../assets/api/streaming-destination/step1.png)

Come primo passo, devi decidere a quale destinazione di streaming attivare i dati. Per iniziare, effettua una chiamata per richiedere un elenco delle destinazioni disponibili a cui puoi connettere e attivare i tipi di pubblico. Esegui la seguente richiesta di GET a `connectionSpecs` endpoint per restituire un elenco di destinazioni disponibili:

**Formato API**

```http
GET /connectionSpecs
```

**Richiesta**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Risposta**

In caso di esito positivo, la risposta contiene un elenco delle destinazioni disponibili e i relativi identificatori univoci (`id`). Memorizza il valore della destinazione che intendi utilizzare, come richiesto nei passaggi successivi. Ad esempio, se desideri connettere e inviare tipi di pubblico a [!DNL Amazon Kinesis] o [!DNL Azure Event Hubs], cerca il seguente frammento nella risposta:

```json
{
    "id": "86043421-563b-46ec-8e6c-e23184711bf6",
  "name": "Amazon Kinesis",
  ...
  ...
}

{
    "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
  "name": "Azure Event Hubs",
  ...
  ...
}
```

## Connettersi ai dati Experienci Platform {#connect-to-your-experience-platform-data}

![Panoramica dei passaggi di destinazione passaggio 2](../assets/api/streaming-destination/step2.png)

Successivamente, devi connetterti ai dati di Experience Platform, in modo da poter esportare i dati di profilo e attivarli nella destinazione preferita. Si tratta di due passaggi che sono descritti di seguito.

1. Innanzitutto, devi eseguire una chiamata per autorizzare l’accesso ai tuoi dati in Experience Platform, impostando una connessione di base.
2. Quindi, utilizzando l’ID connessione di base, effettuerai un’altra chiamata in cui crei una connessione di origine, che stabilisce la connessione ai dati di Experience Platform.


### Autorizzare l’accesso ai dati in Experience Platform

**Formato API**

```http
POST /connections
```

**Richiesta**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            }
}'
```


* `{CONNECTION_SPEC_ID}`: utilizza l’ID della specifica di connessione per il servizio profili - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Risposta**

Una risposta corretta contiene l’identificatore univoco della connessione di base (`id`). Memorizza questo valore come richiesto nel passaggio successivo per creare la connessione sorgente.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Connettersi ai dati Experienci Platform {#connect-to-platform-data}

**Formato API**

```http
POST /sourceConnections
```

**Richiesta**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Profile Service",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "json"
            },
            "params": {}
}'
```

* `{BASE_CONNECTION_ID}`: utilizza l’ID ottenuto nel passaggio precedente.
* `{CONNECTION_SPEC_ID}`: utilizza l’ID della specifica di connessione per il servizio profili - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Risposta**

In caso di esito positivo, la risposta restituisce l’identificatore univoco (`id`) per la nuova connessione sorgente creata al servizio profilo. Ciò conferma che hai effettuato correttamente la connessione ai dati di Experience Platform. Memorizza questo valore come richiesto in un passaggio successivo.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Connetti a destinazione di streaming {#connect-to-streaming-destination}

![Panoramica dei passaggi di destinazione passaggio 3](../assets/api/streaming-destination/step3.png)

In questo passaggio, stai impostando una connessione alla destinazione di streaming desiderata. Si tratta di due passaggi che sono descritti di seguito.

1. Innanzitutto, devi eseguire una chiamata per autorizzare l’accesso alla destinazione di streaming impostando una connessione di base.
2. Quindi, utilizzando l’ID connessione di base, effettuerai un’altra chiamata in cui crei una connessione di destinazione, che specifica la posizione nell’account di archiviazione in cui verranno consegnati i dati esportati e il formato dei dati che verranno esportati.

### Autorizza l’accesso alla destinazione di streaming

**Formato API**

```http
POST /connections
```

**Richiesta**

>[!IMPORTANT]
>
>L’esempio seguente include commenti di codice con il prefisso `//`. Questi commenti evidenziano dove è necessario utilizzare valori diversi per destinazioni di streaming diverse. Rimuovere i commenti prima di utilizzare lo snippet.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connection for Amazon Kinesis/ Azure Event Hubs",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "{_CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "auth": {
        "specName": "{AUTHENTICATION_CREDENTIALS}",
        "params": { // use these values for Amazon Kinesis connections
            "accessKeyId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}",
            "region": "{REGION}"
        },
        "params": { // use these values for Azure Event Hubs connections
            "sasKeyName": "{SAS_KEY_NAME}",
            "sasKey": "{SAS_KEY}",
            "namespace": "{EVENT_HUB_NAMESPACE}"
        }        
    }
}'
```

* `{CONNECTION_SPEC_ID}`: utilizza l’ID della specifica di connessione ottenuto nel passaggio [Ottieni l’elenco delle destinazioni disponibili](#get-the-list-of-available-destinations).
* `{AUTHENTICATION_CREDENTIALS}`: inserisci il nome della destinazione di streaming: `Aws Kinesis authentication credentials` o `Azure EventHub authentication credentials`.
* `{ACCESS_ID}`: *Per [!DNL Amazon Kinesis] connessioni.* ID di accesso per la posizione di archiviazione di Amazon Kinesis.
* `{SECRET_KEY}`: *Per [!DNL Amazon Kinesis] connessioni.* La chiave segreta per la posizione di archiviazione di Amazon Kinesis.
* `{REGION}`: *Per [!DNL Amazon Kinesis] connessioni.* L’area geografica nel tuo [!DNL Amazon Kinesis] account in cui Platform invierà i dati in streaming.
* `{SAS_KEY_NAME}`: *Per [!DNL Azure Event Hubs] connessioni.* Immettere il nome della chiave SAS. Scopri come eseguire l’autenticazione in [!DNL Azure Event Hubs] con le chiavi SAS nel [Documentazione di Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{SAS_KEY}`: *Per [!DNL Azure Event Hubs] connessioni.* Inserire la chiave SAS. Scopri come eseguire l’autenticazione in [!DNL Azure Event Hubs] con le chiavi SAS nel [Documentazione di Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{EVENT_HUB_NAMESPACE}`: *Per [!DNL Azure Event Hubs] connessioni.* Compila il [!DNL Azure Event Hubs] spazio dei nomi in cui Platform invierà i dati in streaming. Per ulteriori informazioni, consulta [Creare uno spazio dei nomi degli hub eventi](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) nel [!DNL Microsoft] documentazione.

**Risposta**

Una risposta corretta contiene l’identificatore univoco della connessione di base (`id`). Memorizza questo valore come richiesto nel passaggio successivo per creare una connessione di destinazione.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Specificare il percorso di archiviazione e il formato dei dati

**Formato API**

```http
POST /targetConnections
```

**Richiesta**

>[!IMPORTANT]
>
>L’esempio seguente include commenti di codice con il prefisso `//`. Questi commenti evidenziano dove è necessario utilizzare valori diversi per destinazioni di streaming diverse. Rimuovere i commenti prima di utilizzare lo snippet.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Amazon Kinesis/ Azure Event Hubs target connection",
    "description": "Connection to Amazon Kinesis/ Azure Event Hubs",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "data": {
        "format": "json"
    },
    "params": { // use these values for Amazon Kinesis connections
        "stream": "{NAME_OF_DATA_STREAM}", 
        "region": "{REGION}"
    },
    "params": { // use these values for Azure Event Hubs connections
        "eventHubName": "{EVENT_HUB_NAME}"
    }
}'
```

* `{BASE_CONNECTION_ID}`: utilizza l’ID connessione di base ottenuto nel passaggio precedente.
* `{CONNECTION_SPEC_ID}`: utilizza la specifica di connessione ottenuta nel passaggio [Ottieni l’elenco delle destinazioni disponibili](#get-the-list-of-available-destinations).
* `{NAME_OF_DATA_STREAM}`: *Per [!DNL Amazon Kinesis] connessioni.* Immetti il nome del flusso di dati esistente nel tuo [!DNL Amazon Kinesis] account. Platform esporterà i dati in questo flusso.
* `{REGION}`: *Per [!DNL Amazon Kinesis] connessioni.* L’area dell’account Amazon Kinesis in cui Platform invierà i dati in streaming.
* `{EVENT_HUB_NAME}`: *Per [!DNL Azure Event Hubs] connessioni.* Compila il [!DNL Azure Event Hub] nome in cui Platform invierà i dati in streaming. Per ulteriori informazioni, consulta [Creare un hub eventi](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) nel [!DNL Microsoft] documentazione.

**Risposta**

In caso di esito positivo, la risposta restituisce l’identificatore univoco (`id`) per la connessione di destinazione appena creata alla destinazione di streaming. Memorizza questo valore come richiesto nei passaggi successivi.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Creare un flusso di dati

![Panoramica dei passaggi di destinazione 4](../assets/api/streaming-destination/step4.png)

Utilizzando gli ID ottenuti nei passaggi precedenti, ora puoi creare un flusso di dati tra i dati dell’Experience Platform e la destinazione in cui attiverai i dati. Considera questo passaggio come la costruzione della pipeline, attraverso la quale i dati fluiranno in seguito, tra Experience Platform e la destinazione desiderata.

Per creare un flusso di dati, esegui una richiesta POST, come mostrato di seguito, fornendo i valori menzionati di seguito all’interno del payload.

Per creare un flusso di dati, esegui la seguente richiesta POST.

**Formato API**

```http
POST /flows
```

**Richiesta**

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/flows' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
  "name": "Azure Event Hubs",
  "description": "Azure Event Hubs",
  "flowSpec": {
    "id": "{FLOW_SPEC_ID}",
    "version": "1.0"
  },
  "sourceConnectionIds": [
    "{SOURCE_CONNECTION_ID}"
  ],
  "targetConnectionIds": [
    "{TARGET_CONNECTION_ID}"
  ],
  "transformations": [
    {
      "name": "GeneralTransform",
      "params": {
        "profileSelectors": {
          "selectors": [
            
          ]
        },
        "segmentSelectors": {
          "selectors": [
            
          ]
        }
      }
    }
  ]
}
```

* `{FLOW_SPEC_ID}`: l’ID della specifica di flusso per le destinazioni basate su profili è `71471eba-b620-49e4-90fd-23f1fa0174d8`. Utilizza questo valore nella chiamata di.
* `{SOURCE_CONNECTION_ID}`: utilizza l’ID connessione sorgente ottenuto nel passaggio [Connetti all’Experience Platform](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`: utilizza l’ID connessione di destinazione ottenuto nel passaggio [Connetti a destinazione di streaming](#connect-to-streaming-destination).

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID (`id`) del flusso di dati appena creato e un `etag`. Annotare entrambi i valori. nel passaggio successivo, per attivare i tipi di pubblico.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Attiva i dati nella nuova destinazione {#activate-data}

![Panoramica dei passaggi di destinazione passaggio 5](../assets/api/streaming-destination/step5.png)

Dopo aver creato tutte le connessioni e il flusso di dati, ora puoi attivare i dati del profilo nella piattaforma di streaming. In questo passaggio, puoi selezionare i tipi di pubblico e gli attributi di profilo da inviare alla destinazione, nonché pianificare e inviare dati alla destinazione.

Per attivare i tipi di pubblico nella nuova destinazione, devi eseguire un’operazione JSON PATCH, simile all’esempio di seguito. Puoi attivare più tipi di pubblico e attributi di profilo in una sola chiamata. Per ulteriori informazioni su JSON PATCH, consulta [Specifiche RFC](https://tools.ietf.org/html/rfc6902).

**Formato API**

```http
PATCH /flows
```

**Richiesta**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'If-Match: "{ETAG}"' \
--data-raw '[
  {
    "op": "add",
    "path": "/transformations/0/params/segmentSelectors/selectors/-",
    "value": {
      "type": "PLATFORM_SEGMENT",
      "value": {
        "name": "Name of the audience that you are activating",
        "description": "Description of the audience that you are activating",
        "id": "{SEGMENT_ID}"
      }
    }
  },
  {
    "op": "add",
    "path": "/transformations/0/params/profileSelectors/selectors/-",
    "value": {
      "type": "JSON_PATH",
      "value": {
        "operator": "EXISTS",
        "path": "{PROFILE_ATTRIBUTE}"
      }
    }
  }
]
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `{DATAFLOW_ID}` | Nell’URL, utilizza l’ID del flusso di dati creato nel passaggio precedente. |
| `{ETAG}` | Ottieni `{ETAG}` dalla risposta della fase precedente, [Creare un flusso di dati](#create-dataflow). Il formato della risposta nel passaggio precedente contiene virgolette di escape. Devi utilizzare i valori senza escape nell’intestazione della richiesta. Vedi l’esempio seguente: <br> <ul><li>Esempio di risposta: `"etag":""7400453a-0000-1a00-0000-62b1c7a90000""`</li><li>Valore da utilizzare nella richiesta: `"etag": "7400453a-0000-1a00-0000-62b1c7a90000"`</li></ul> <br> Il valore etag viene aggiornato a ogni aggiornamento riuscito di un flusso di dati. |
| `{SEGMENT_ID}` | Specifica l’ID del pubblico da esportare in questa destinazione. Per recuperare gli ID del pubblico per i tipi di pubblico che desideri attivare, consulta [recuperare una definizione di pubblico](https://www.adobe.io/experience-platform-apis/references/segmentation/#operation/retrieveSegmentDefinitionById) nel riferimento API di Experience Platform. |
| `{PROFILE_ATTRIBUTE}` | Ad esempio, `"person.lastName"` |
| `op` | Chiamata di operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace`, e `remove`. Per aggiungere un pubblico a un flusso di dati, utilizza `add` operazione. |
| `path` | Definisce la parte del flusso da aggiornare. Quando aggiungi un pubblico a un flusso di dati, utilizza il percorso specificato nell’esempio. |
| `value` | Il nuovo valore con cui desideri aggiornare il parametro. |
| `id` | Specifica l’ID del pubblico che stai aggiungendo al flusso di dati di destinazione. |
| `name` | *Facoltativo*. Specifica il nome del pubblico che stai aggiungendo al flusso di dati di destinazione. Tieni presente che questo campo non è obbligatorio e puoi aggiungere correttamente un pubblico al flusso di dati di destinazione senza specificarne il nome. |

**Risposta**

Cercate una risposta 202 OK. Nessun corpo di risposta restituito. Per verificare che la richiesta sia corretta, consulta il passaggio successivo, Convalidare il flusso di dati.

## Convalidare il flusso di dati

![Panoramica dei passaggi di destinazione 6](../assets/api/streaming-destination/step6.png)

Come ultimo passaggio dell’esercitazione, devi verificare che i tipi di pubblico e gli attributi del profilo siano stati effettivamente mappati correttamente al flusso di dati.

Per convalidarlo, esegui la seguente richiesta GET:

**Formato API**

```http
GET /flows
```

**Richiesta**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`: utilizza il flusso di dati del passaggio precedente.
* `{ETAG}`: utilizza l’eTag del passaggio precedente.

**Risposta**

La risposta restituita deve includere nel `transformations` specifica i tipi di pubblico e gli attributi del profilo inviati nel passaggio precedente. Un esempio `transformations` Il parametro nella risposta potrebbe essere simile al seguente:

```json
"transformations": [
    {
        "name": "GeneralTransform",
        "params": {
            "profileSelectors": {
                        "selectors": [
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "personalEmail.address",
                                    "operator": "EXISTS"
                                }
                            },
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "person.lastname",
                                    "operator": "EXISTS"
                                }
                            }
                        ]
                    },
            "segmentSelectors": {
                "selectors": [
                    {
                        "type": "PLATFORM_SEGMENT",
                        "value": {
                            "name": "Men over 50",
                            "description": "",
                            "id": "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02"
                        }
                    }
                ]
            }
        }
    }
],
```

**Dati esportati**

>[!IMPORTANT]
>
> Oltre agli attributi del profilo e ai tipi di pubblico nel passaggio [Attiva i dati nella nuova destinazione](#activate-data), i dati esportati in [!DNL AWS Kinesis] e [!DNL Azure Event Hubs] includerà anche informazioni sulla mappa delle identità. Rappresenta le identità dei profili esportati (ad esempio [ECID](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html), ID dispositivo mobile, ID Google, indirizzo e-mail, ecc.). Vedi un esempio qui sotto.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02": {
        "lastQualificationTime": "2020-03-03T21:24:39Z",
        "status": "exited"
      },
      "7841ba61-23c1-4bb3-a495-00d695fe1e93": {
        "lastQualificationTime": "2020-03-04T23:37:33Z",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## Utilizzo di [!DNL Postman] raccolte per la connessione a destinazioni di streaming  {#collections}

Per connetterti alle destinazioni di streaming descritte in questo tutorial in modo più semplice, puoi utilizzare [[!DNL Postman]](https://www.postman.com/).

[!DNL Postman] è uno strumento che puoi utilizzare per effettuare chiamate API e gestire librerie di chiamate e ambienti predefiniti.

Per questo tutorial specifico, le seguenti [!DNL Postman] le raccolte sono state aggiunte:

* [!DNL AWS Kinesis] [!DNL Postman] raccolta
* [!DNL Azure Event Hubs] [!DNL Postman] raccolta

Clic [qui](../assets/api/streaming-destination/DestinationPostmanCollection.zip) per scaricare l’archivio delle raccolte.

Ogni raccolta include le richieste e le variabili di ambiente necessarie, per [!DNL AWS Kinesis], e [!DNL Azure Event Hub], rispettivamente.

### Come utilizzare il [!DNL Postman] raccolte {#how-to-use-postman-collections}

Per connettersi correttamente alle destinazioni utilizzando il [!DNL Postman] raccolte, segui questi passaggi:

* Scarica e installa [!DNL Postman];
* [Scarica](../assets/api/streaming-destination/DestinationPostmanCollection.zip) e decomprimi le raccolte collegate;
* Importare le raccolte dalle cartelle corrispondenti in [!DNL Postman];
* Compilare le variabili di ambiente seguendo le istruzioni riportate in questo articolo;
* Esegui il [!DNL API] richieste da [!DNL Postman], in base alle istruzioni contenute in questo articolo.

## Gestione degli errori API {#api-error-handling}

Gli endpoint API in questa esercitazione seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](/help/landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](/help/landing/troubleshooting.md#request-header-errors) per ulteriori informazioni sull’interpretazione delle risposte di errore, consulta la guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai connesso correttamente Platform a una delle tue destinazioni di streaming preferite e hai impostato un flusso di dati per la rispettiva destinazione. I dati in uscita possono ora essere utilizzati nella destinazione per l’analisi dei clienti o per qualsiasi altra operazione sui dati che desideri eseguire. Per ulteriori informazioni, consulta le pagine seguenti:

* [Panoramica sulle destinazioni](../home.md)
* [Panoramica del catalogo delle destinazioni](../catalog/overview.md)
