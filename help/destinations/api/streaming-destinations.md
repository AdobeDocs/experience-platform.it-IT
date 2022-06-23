---
keywords: Experience Platform;home;argomenti popolari; Esercitazioni API; API per lo streaming delle destinazioni; Piattaforma
solution: Experience Platform
title: Connettiti alle destinazioni di streaming e attiva i dati utilizzando l’API del servizio di flusso in Adobe Experience Platform
description: Questo documento tratta la creazione di destinazioni di streaming utilizzando l’API Adobe Experience Platform
topic-legacy: tutorial
type: Tutorial
exl-id: 3e8d2745-8b83-4332-9179-a84d8c0b4400
source-git-commit: 183830318a3dd5012f27a73a8dd2753638aff83f
workflow-type: tm+mt
source-wordcount: '2241'
ht-degree: 2%

---

# Connettiti alle destinazioni di streaming e attiva i dati utilizzando l’API del servizio di flusso

>[!IMPORTANT]
> 
>Per connettersi a una destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions).
>
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions).
>
>Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Questa esercitazione illustra come utilizzare le chiamate API per connettersi ai dati di Adobe Experience Platform e creare una connessione a una destinazione di archiviazione cloud in streaming ([Amazon Kinesis](../catalog/cloud-storage/amazon-kinesis.md) o [Hub eventi di Azure](../catalog/cloud-storage/azure-event-hubs.md)), crea un flusso di dati per la nuova destinazione creata e attiva i dati per la nuova destinazione creata.

Questa esercitazione utilizza la funzione [!DNL Amazon Kinesis] destinazione in tutti gli esempi, ma i passaggi sono identici per [!DNL Azure Event Hubs].

![Panoramica : i passaggi per creare una destinazione di streaming e attivare i segmenti](../assets/api/streaming-destination/overview.png)

Se preferisci utilizzare l’interfaccia utente di Platform per connettersi a una destinazione e attivare i dati, consulta la sezione [Collegare una destinazione](../ui/connect-destination.md) e [Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](../ui/activate-segment-streaming-destinations.md) esercitazioni.

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] è il sistema di registrazione per la posizione dei dati e la derivazione all&#39;interno di Experience Platform.
* [Sandbox](../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per attivare i dati alle destinazioni di streaming in Platform.

### Raccogli credenziali richieste

Per completare i passaggi descritti in questa esercitazione, devi disporre delle seguenti credenziali, a seconda del tipo di destinazioni a cui stai connettendo e attivando i segmenti.

* Per [!DNL Amazon Kinesis] connessioni: `accessKeyId`, `secretKey`, `region` o `connectionUrl`
* Per [!DNL Azure Event Hubs] connessioni: `sasKeyName`, `sasKey`, `namespace`

### Lettura di chiamate API di esempio {#reading-sample-api-calls}

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

### Raccogli i valori delle intestazioni richieste e facoltative {#gather-values}

Per effettuare chiamate alle API di Platform, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Le risorse in Experience Platform possono essere isolate in sandbox virtuali specifiche. Nelle richieste alle API di Platform, puoi specificare il nome e l’ID della sandbox in cui avrà luogo l’operazione. Si tratta di parametri facoltativi.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Experience Platform, consulta la sezione [documentazione panoramica su sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* Content-Type: `application/json`

### Documentazione Swagger {#swagger-docs}

In Swagger puoi trovare la documentazione di riferimento associata per tutte le chiamate API in questa esercitazione. Consulta la sezione [Documentazione API del servizio di flusso sull’Adobe I/O](https://www.adobe.io/experience-platform-apis/references/flow-service/). È consigliabile utilizzare questa esercitazione e la pagina della documentazione Swagger in parallelo.

## Ottieni l’elenco delle destinazioni di streaming disponibili {#get-the-list-of-available-streaming-destinations}

![Passaggio 1: panoramica dei passaggi di destinazione](../assets/api/streaming-destination/step1.png)

Come primo passo, devi decidere a quale destinazione di streaming attivare i dati. Per iniziare, esegui una chiamata per richiedere un elenco di destinazioni disponibili a cui puoi collegare e attivare i segmenti. Esegui la seguente richiesta di GET al `connectionSpecs` per restituire un elenco di destinazioni disponibili:

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

Una risposta corretta contiene un elenco delle destinazioni disponibili e dei relativi identificatori univoci (`id`). Memorizza il valore della destinazione che intendi utilizzare, come sarà necessario in ulteriori passaggi. Ad esempio, se desideri collegare e distribuire segmenti a [!DNL Amazon Kinesis] o [!DNL Azure Event Hubs], cerca il seguente frammento nella risposta:

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

## Connettersi ai dati di Experience Platform {#connect-to-your-experience-platform-data}

![Passaggio 2: panoramica dei passaggi di destinazione](../assets/api/streaming-destination/step2.png)

Successivamente, devi connetterti ai dati di Experience Platform, in modo da poter esportare i dati di profilo e attivarli nella destinazione desiderata. Si tratta di due sottoregimi descritti di seguito.

1. Innanzitutto, devi eseguire una chiamata per autorizzare l&#39;accesso ai tuoi dati in Experience Platform, configurando una connessione di base.
2. Quindi, utilizzando l&#39;ID di connessione di base, effettuerai un&#39;altra chiamata in cui crei una connessione sorgente, che stabilisce la connessione ai dati del tuo Experience Platform.


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


* `{CONNECTION_SPEC_ID}`: Utilizza l’ID delle specifiche di connessione per il servizio profili - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Risposta**

Una risposta corretta contiene l&#39;identificatore univoco della connessione di base (`id`). Memorizza questo valore come necessario nel passaggio successivo per creare la connessione sorgente.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Connettersi ai dati di Experience Platform {#connect-to-platform-data}

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

* `{BASE_CONNECTION_ID}`: Utilizza l&#39;ID ottenuto nel passaggio precedente.
* `{CONNECTION_SPEC_ID}`: Utilizza l’ID delle specifiche di connessione per il servizio profili - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) per la nuova connessione sorgente al servizio profilo. Conferma che la connessione ai dati di Experience Platform è stata completata. Memorizza questo valore come richiesto in un passaggio successivo.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Connessione alla destinazione streaming {#connect-to-streaming-destination}

![Passaggi di destinazione: passaggio 3](../assets/api/streaming-destination/step3.png)

In questo passaggio, stai impostando una connessione alla destinazione di streaming desiderata. Si tratta di due sottoregimi descritti di seguito.

1. Innanzitutto, devi eseguire una chiamata per autorizzare l’accesso alla destinazione streaming, impostando una connessione di base.
2. Quindi, utilizzando l&#39;ID di connessione di base, effettuerai un&#39;altra chiamata in cui crei una connessione di destinazione, che specifica la posizione nell&#39;account di archiviazione in cui verranno inviati i dati esportati, nonché il formato dei dati che verranno esportati.

### Autorizzare l&#39;accesso alla destinazione streaming

**Formato API**

```http
POST /connections
```

**Richiesta**

>[!IMPORTANT]
>
>L&#39;esempio seguente include i commenti di codice con il prefisso `//`. Questi commenti evidenziano dove devono essere utilizzati valori diversi per destinazioni di streaming diverse. Rimuovere i commenti prima di utilizzare lo snippet.

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

* `{CONNECTION_SPEC_ID}`: Utilizza l’ID della specifica di connessione ottenuto nel passaggio [Ottieni l’elenco delle destinazioni disponibili](#get-the-list-of-available-destinations).
* `{AUTHENTICATION_CREDENTIALS}`: compila il nome della destinazione di streaming: `Aws Kinesis authentication credentials` o `Azure EventHub authentication credentials`.
* `{ACCESS_ID}`: *Per [!DNL Amazon Kinesis] connessioni.* ID di accesso per la posizione di archiviazione Kinesis di Amazon.
* `{SECRET_KEY}`: *Per [!DNL Amazon Kinesis] connessioni.* Chiave segreta per la posizione di archiviazione Kinesis di Amazon.
* `{REGION}`: *Per [!DNL Amazon Kinesis] connessioni.* La regione nel tuo [!DNL Amazon Kinesis] account in cui Platform eseguirà lo streaming dei dati.
* `{SAS_KEY_NAME}`: *Per [!DNL Azure Event Hubs] connessioni.* Immettere il nome della chiave SAS. Informazioni sull&#39;autenticazione in [!DNL Azure Event Hubs] con le chiavi SAS nel [Documentazione di Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{SAS_KEY}`: *Per [!DNL Azure Event Hubs] connessioni.* Inserire la chiave SAS. Informazioni sull&#39;autenticazione in [!DNL Azure Event Hubs] con le chiavi SAS nel [Documentazione di Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{EVENT_HUB_NAMESPACE}`: *Per [!DNL Azure Event Hubs] connessioni.* Compila il [!DNL Azure Event Hubs] spazio dei nomi in cui Platform eseguirà lo streaming dei dati. Per ulteriori informazioni, consulta [Creare uno spazio dei nomi Hubs evento](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) in [!DNL Microsoft] documentazione.

**Risposta**

Una risposta corretta contiene l&#39;identificatore univoco della connessione di base (`id`). Memorizza questo valore come necessario nel passaggio successivo per creare una connessione di destinazione.

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
>L&#39;esempio seguente include i commenti di codice con il prefisso `//`. Questi commenti evidenziano dove devono essere utilizzati valori diversi per destinazioni di streaming diverse. Rimuovere i commenti prima di utilizzare lo snippet.

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

* `{BASE_CONNECTION_ID}`: Utilizza l&#39;ID di connessione di base ottenuto nel passaggio precedente.
* `{CONNECTION_SPEC_ID}`: Utilizza le specifiche di connessione ottenute nel passaggio [Ottieni l’elenco delle destinazioni disponibili](#get-the-list-of-available-destinations).
* `{NAME_OF_DATA_STREAM}`: *Per [!DNL Amazon Kinesis] connessioni.* Immetti il nome del flusso di dati esistente nel tuo [!DNL Amazon Kinesis] conto. Platform esporta i dati in questo flusso.
* `{REGION}`: *Per [!DNL Amazon Kinesis] connessioni.* La regione nel tuo account Amazon Kinesis in cui Platform eseguirà lo streaming dei tuoi dati.
* `{EVENT_HUB_NAME}`: *Per [!DNL Azure Event Hubs] connessioni.* Compila il [!DNL Azure Event Hub] nome in cui Platform eseguirà lo streaming dei dati. Per ulteriori informazioni, consulta [Creare un hub eventi](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) in [!DNL Microsoft] documentazione.

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) per la nuova connessione di destinazione alla destinazione di streaming. Memorizza questo valore come richiesto nei passaggi successivi.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Creazione di un flusso di dati

![Passaggi di destinazione: passaggio 4](../assets/api/streaming-destination/step4.png)

Utilizzando gli ID ottenuti nei passaggi precedenti, ora puoi creare un flusso di dati tra i dati di Experience Platform e la destinazione in cui attiverai i dati. Considera questo passaggio come la costruzione della pipeline, attraverso la quale i dati scorreranno successivamente, tra l’Experience Platform e la destinazione desiderata.

Per creare un flusso di dati, esegui una richiesta POST, come mostrato di seguito, fornendo al tempo stesso i valori indicati di seguito all’interno del payload.

Esegui la seguente richiesta POST per creare un flusso di dati.

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

* `{FLOW_SPEC_ID}`: L’ID della specifica di flusso per le destinazioni basate su profili è `71471eba-b620-49e4-90fd-23f1fa0174d8`. Utilizza questo valore nella chiamata di .
* `{SOURCE_CONNECTION_ID}`: Utilizza l’ID di connessione sorgente ottenuto nel passaggio [Connettiti al tuo Experience Platform](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`: Utilizza l’ID di connessione di destinazione ottenuto nel passaggio [Connessione alla destinazione streaming](#connect-to-streaming-destination).

**Risposta**

Una risposta corretta restituisce l&#39;ID (`id`) del flusso di dati appena creato e un `etag`. Annotare entrambi i valori. come li eseguirai nel passaggio successivo, per attivare i segmenti.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Attiva i dati nella nuova destinazione {#activate-data}

![Passaggi di destinazione: passaggio 5](../assets/api/streaming-destination/step5.png)

Dopo aver creato tutte le connessioni e il flusso di dati, ora puoi attivare i dati del profilo sulla piattaforma streaming. In questo passaggio, seleziona i segmenti e gli attributi di profilo che stai inviando alla destinazione e puoi pianificare e inviare i dati alla destinazione.

Per attivare i segmenti nella nuova destinazione, è necessario eseguire un’operazione JSON PATCH, simile all’esempio seguente. Puoi attivare più segmenti e attributi di profilo in una sola chiamata. Per ulteriori informazioni su JSON PATCH, consulta la sezione [Specifica RFC](https://tools.ietf.org/html/rfc6902).

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
        "name": "Name of the segment that you are activating",
        "description": "Description of the segment that you are activating",
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
| `{ETAG}` | Ottieni il `{ETAG}` dalla risposta nel passaggio precedente, [Creare un flusso di dati](#create-dataflow). Il formato di risposta nel passaggio precedente è evitato dalle virgolette. È necessario utilizzare i valori non preceduti nell’intestazione della richiesta. Vedi l&#39;esempio seguente: <br> <ul><li>Esempio di risposta: `"etag":""7400453a-0000-1a00-0000-62b1c7a90000""`</li><li>Valore da utilizzare nella richiesta: `"etag": "7400453a-0000-1a00-0000-62b1c7a90000"`</li></ul> <br> Il valore etag viene aggiornato con ogni aggiornamento corretto di un flusso di dati. |
| `{SEGMENT_ID}` | Fornisci l’ID del segmento da esportare a questa destinazione. Per recuperare gli ID dei segmenti per i segmenti che desideri attivare, vedi [recuperare una definizione di segmento](https://www.adobe.io/experience-platform-apis/references/segmentation/#operation/retrieveSegmentDefinitionById) nel riferimento API di Experience Platform. |
| `{PROFILE_ATTRIBUTE}` | Ad esempio, `"person.lastName"` |
| `op` | La chiamata dell’operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace`e `remove`. Per aggiungere un segmento a un flusso di dati, utilizza il `add` funzionamento. |
| `path` | Definisce la parte del flusso da aggiornare. Quando aggiungi un segmento a un flusso di dati, utilizza il percorso specificato nell’esempio. |
| `value` | Il nuovo valore con cui si desidera aggiornare il parametro. |
| `id` | Specifica l’ID del segmento che stai aggiungendo al flusso di dati di destinazione. |
| `name` | *Facoltativo*. Specifica il nome del segmento che stai aggiungendo al flusso di dati di destinazione. Tieni presente che questo campo non è obbligatorio ed è possibile aggiungere correttamente un segmento al flusso di dati di destinazione senza specificarne il nome. |

**Risposta**

Cerca una risposta 202 OK. Non viene restituito alcun corpo di risposta. Per verificare che la richiesta fosse corretta, vedi il passaggio successivo, Convalida il flusso di dati.

## Convalidare il flusso di dati

![Passaggi di destinazione: passaggio 6](../assets/api/streaming-destination/step6.png)

Come passaggio finale nell’esercitazione, dovresti verificare che i segmenti e gli attributi di profilo siano stati mappati correttamente al flusso di dati.

Per convalidarlo, esegui la seguente richiesta di GET:

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

* `{DATAFLOW_ID}`: Utilizza il flusso di dati del passaggio precedente.
* `{ETAG}`: Utilizza il tag del passaggio precedente.

**Risposta**

La risposta restituita deve includere nel `transformations` i segmenti e gli attributi di profilo inviati nel passaggio precedente. Un campione `transformations` nella risposta potrebbe essere simile al seguente:

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
> Oltre agli attributi del profilo e ai segmenti nel passaggio [Attiva i dati nella nuova destinazione](#activate-data), i dati esportati in [!DNL AWS Kinesis] e [!DNL Azure Event Hubs] includerà anche informazioni sulla mappa di identità. Rappresenta le identità dei profili esportati (ad esempio [ECID](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html), ID mobile, Google ID, indirizzo e-mail, ecc.). Vedi un esempio qui sotto.

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
        "status": "existing"
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

## Utilizzo [!DNL Postman] raccolte per connettersi alle destinazioni di streaming  {#collections}

Per collegarti alle destinazioni di streaming descritte in questa esercitazione in modo più semplice, puoi utilizzare [[!DNL Postman]](https://www.postman.com/).

[!DNL Postman] è uno strumento che puoi utilizzare per effettuare chiamate API e gestire le librerie di chiamate e ambienti predefiniti.

Per questa esercitazione specifica, procedi come segue [!DNL Postman] le raccolte sono state allegate:

* [!DNL AWS Kinesis] [!DNL Postman] raccolta
* [!DNL Azure Event Hubs] [!DNL Postman] raccolta

Fai clic su [qui](../assets/api/streaming-destination/DestinationPostmanCollection.zip) per scaricare l&#39;archivio delle raccolte.

Ogni raccolta include le richieste necessarie e le variabili di ambiente, per [!DNL AWS Kinesis]e [!DNL Azure Event Hub], rispettivamente.

### Come utilizzare il [!DNL Postman] collezioni {#how-to-use-postman-collections}

Per connettersi correttamente alle destinazioni utilizzando l&#39;allegato [!DNL Postman] raccolte, segui questi passaggi:

* Scarica e installa [!DNL Postman];
* [Scarica](../assets/api/streaming-destination/DestinationPostmanCollection.zip) e decomprimere le raccolte allegate;
* Importare le raccolte dalle cartelle corrispondenti in [!DNL Postman];
* Compila le variabili d&#39;ambiente secondo le istruzioni del presente articolo;
* Esegui il [!DNL API] richieste da [!DNL Postman], in base alle istruzioni contenute nel presente articolo.

## Gestione degli errori API {#api-error-handling}

Gli endpoint API in questa esercitazione seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](/help/landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](/help/landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform per ulteriori informazioni sull’interpretazione delle risposte agli errori.

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai collegato Platform a una delle tue destinazioni di streaming preferite e hai impostato un flusso di dati per la rispettiva destinazione. I dati in uscita possono ora essere utilizzati nella destinazione per l’analisi dei clienti o per qualsiasi altra operazione di dati che desideri eseguire. Per ulteriori informazioni, consulta le pagine seguenti:

* [Panoramica sulle destinazioni](../home.md)
* [Panoramica del catalogo delle destinazioni](../catalog/overview.md)
