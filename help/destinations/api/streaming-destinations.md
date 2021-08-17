---
keywords: Experience Platform;home;argomenti popolari; Esercitazioni API; API per lo streaming delle destinazioni; Piattaforma
solution: Experience Platform
title: Connettiti alle destinazioni di streaming e attiva i dati utilizzando l’API del servizio di flusso in Adobe Experience Platform
description: Questo documento tratta la creazione di destinazioni di streaming utilizzando l’API Adobe Experience Platform
topic-legacy: tutorial
type: Tutorial
exl-id: 3e8d2745-8b83-4332-9179-a84d8c0b4400
source-git-commit: 02c22453470d55236d4235c479742997e8407ef3
workflow-type: tm+mt
source-wordcount: '2025'
ht-degree: 1%

---

# Connettiti alle destinazioni di streaming e attiva i dati utilizzando l’API del servizio di flusso

>[!NOTE]
>
>Le destinazioni [!DNL Amazon Kinesis] e [!DNL Azure Event Hubs] in Platform sono attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

Questa esercitazione illustra come utilizzare le chiamate API per connettersi ai dati di Adobe Experience Platform, creare una connessione a una destinazione di archiviazione cloud in streaming ([Amazon Kinesis](../catalog/cloud-storage/amazon-kinesis.md) o [Azure Event Hubs](../catalog/cloud-storage/azure-event-hubs.md)), creare un flusso di dati per la nuova destinazione creata e attivare i dati per la nuova destinazione creata.

Questa esercitazione utilizza la destinazione [!DNL Amazon Kinesis] in tutti gli esempi, ma i passaggi sono identici per [!DNL Azure Event Hubs].

![Panoramica : i passaggi per creare una destinazione di streaming e attivare i segmenti](../assets/api/streaming-destination/overview.png)

Se preferisci utilizzare l’interfaccia utente di Platform per connetterti a una destinazione e attivare i dati, consulta le esercitazioni [Connetti una destinazione](../ui/connect-destination.md) e [Attiva i dati del pubblico per le destinazioni di esportazione dei segmenti in streaming](../ui/activate-segment-streaming-destinations.md) .

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
* [[!DNL Catalog Service]](../../catalog/home.md):  [!DNL Catalog] è il sistema di registrazione per la posizione dei dati e la derivazione all&#39;interno di Experience Platform.
* [Sandbox](../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per attivare i dati alle destinazioni di streaming in Platform.

### Raccogli credenziali richieste

Per completare i passaggi descritti in questa esercitazione, devi disporre delle seguenti credenziali, a seconda del tipo di destinazioni a cui stai connettendo e attivando i segmenti.

* Per le connessioni [!DNL Amazon Kinesis]: `accessKeyId`, `secretKey`, `region` o `connectionUrl`
* Per le connessioni [!DNL Azure Event Hubs]: `sasKeyName`, `sasKey`, `namespace`

### Lettura di chiamate API di esempio {#reading-sample-api-calls}

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

### Raccogli i valori delle intestazioni richieste e facoltative {#gather-values}

Per effettuare chiamate alle API di Platform, devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Le risorse in Experience Platform possono essere isolate in sandbox virtuali specifiche. Nelle richieste alle API di Platform, puoi specificare il nome e l’ID della sandbox in cui avrà luogo l’operazione. Si tratta di parametri facoltativi.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox nell’Experience Platform, consulta la documentazione di panoramica [sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* Content-Type: `application/json`

### Documentazione Swagger {#swagger-docs}

In Swagger puoi trovare la documentazione di riferimento associata per tutte le chiamate API in questa esercitazione. Consulta la [documentazione API del servizio di flusso su Adobe I/O](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml). È consigliabile utilizzare questa esercitazione e la pagina della documentazione Swagger in parallelo.

## Ottieni l’elenco delle destinazioni di streaming disponibili {#get-the-list-of-available-streaming-destinations}

![Passaggio 1: panoramica dei passaggi di destinazione](../assets/api/streaming-destination/step1.png)

Come primo passo, devi decidere a quale destinazione di streaming attivare i dati. Per iniziare, esegui una chiamata per richiedere un elenco di destinazioni disponibili a cui puoi collegare e attivare i segmenti. Esegui la seguente richiesta di GET all’endpoint `connectionSpecs` per restituire un elenco di destinazioni disponibili:

**Formato API**

```http
GET /connectionSpecs
```

**Richiesta**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Risposta**

Una risposta corretta contiene un elenco delle destinazioni disponibili e dei relativi identificatori univoci (`id`). Memorizza il valore della destinazione che intendi utilizzare, come sarà necessario in ulteriori passaggi. Ad esempio, se desideri collegare e consegnare segmenti a [!DNL Amazon Kinesis] o [!DNL Azure Event Hubs], cerca il seguente frammento nella risposta:

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
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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


* `{CONNECTION_SPEC_ID}`: Utilizza l’ID delle specifiche di connessione per il servizio profili -  `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

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
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "params" : {}
}'
```

* `{BASE_CONNECTION_ID}`: Utilizza l&#39;ID ottenuto nel passaggio precedente.
* `{CONNECTION_SPEC_ID}`: Utilizza l’ID delle specifiche di connessione per il servizio profili -  `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Risposta**

Una risposta corretta restituisce l’identificatore univoco (`id`) per la nuova connessione sorgente al servizio profilo appena creata. Conferma che la connessione ai dati di Experience Platform è stata completata. Memorizza questo valore come richiesto in un passaggio successivo.

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
>L&#39;esempio seguente include i commenti di codice con prefisso `//`. Questi commenti evidenziano dove devono essere utilizzati valori diversi per destinazioni di streaming diverse. Rimuovere i commenti prima di utilizzare lo snippet.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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

* `{CONNECTION_SPEC_ID}`: Utilizza l’ID delle specifiche di connessione ottenuto nel passaggio  [Ottieni l’elenco delle destinazioni](#get-the-list-of-available-destinations) disponibili.
* `{AUTHENTICATION_CREDENTIALS}`: compila il nome della destinazione di streaming:  `Aws Kinesis authentication credentials` o  `Azure EventHub authentication credentials`.
* `{ACCESS_ID}`:  *Per  [!DNL Amazon Kinesis] le connessioni.* ID di accesso per la posizione di archiviazione Kinesis di Amazon.
* `{SECRET_KEY}`:  *Per  [!DNL Amazon Kinesis] le connessioni.* Chiave segreta per la posizione di archiviazione Kinesis di Amazon.
* `{REGION}`:  *Per  [!DNL Amazon Kinesis] le connessioni.* La regione nel tuo  [!DNL Amazon Kinesis] account in cui Platform eseguirà lo streaming dei dati.
* `{SAS_KEY_NAME}`:  *Per  [!DNL Azure Event Hubs] le connessioni.* Immettere il nome della chiave SAS. Informazioni sull&#39;autenticazione in [!DNL Azure Event Hubs] con chiavi SAS nella [documentazione Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{SAS_KEY}`:  *Per  [!DNL Azure Event Hubs] le connessioni.* Inserire la chiave SAS. Informazioni sull&#39;autenticazione in [!DNL Azure Event Hubs] con chiavi SAS nella [documentazione Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{EVENT_HUB_NAMESPACE}`:  *Per  [!DNL Azure Event Hubs] le connessioni.* Inserisci lo  [!DNL Azure Event Hubs] spazio dei nomi in cui Platform eseguirà lo streaming dei dati. Per ulteriori informazioni, consulta [Creare un namespace Event Hubs](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) nella documentazione [!DNL Microsoft] .

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
>L&#39;esempio seguente include i commenti di codice con prefisso `//`. Questi commenti evidenziano dove devono essere utilizzati valori diversi per destinazioni di streaming diverse. Rimuovere i commenti prima di utilizzare lo snippet.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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
* `{CONNECTION_SPEC_ID}`: Utilizza le specifiche di connessione ottenute nel passaggio  [Ottieni l’elenco delle destinazioni](#get-the-list-of-available-destinations) disponibili.
* `{NAME_OF_DATA_STREAM}`:  *Per  [!DNL Amazon Kinesis] le connessioni.* Immetti il nome del flusso di dati esistente nel tuo  [!DNL Amazon Kinesis] account. Platform esporta i dati in questo flusso.
* `{REGION}`:  *Per  [!DNL Amazon Kinesis] le connessioni.* La regione nel tuo account Amazon Kinesis in cui Platform eseguirà lo streaming dei tuoi dati.
* `{EVENT_HUB_NAME}`:  *Per  [!DNL Azure Event Hubs] le connessioni.* Inserisci il  [!DNL Azure Event Hub] nome in cui Platform eseguirà lo streaming dei dati. Per ulteriori informazioni, consulta [Creare un hub eventi](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) nella documentazione [!DNL Microsoft] .

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
-H 'x-gw-ims-org-id: {IMS_ORG}' \
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

* `{FLOW_SPEC_ID}`: L’ID della specifica di flusso per le destinazioni basate su profili è  `71471eba-b620-49e4-90fd-23f1fa0174d8`. Utilizza questo valore nella chiamata di .
* `{SOURCE_CONNECTION_ID}`: Utilizza l&#39;ID di connessione sorgente ottenuto nel passaggio  [Connetti all&#39;Experience Platform](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`: Utilizza l&#39;ID di connessione di destinazione ottenuto nel passaggio  [Connetti a destinazione](#connect-to-streaming-destination) streaming.

**Risposta**

Una risposta corretta restituisce l&#39;ID (`id`) del flusso di dati appena creato e un valore `etag`. Annotare entrambi i valori. come li eseguirai nel passaggio successivo, per attivare i segmenti.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Attiva i dati nella nuova destinazione {#activate-data}

![Passaggi di destinazione: passaggio 5](../assets/api/streaming-destination/step5.png)

Dopo aver creato tutte le connessioni e il flusso di dati, ora puoi attivare i dati del profilo sulla piattaforma streaming. In questo passaggio, seleziona i segmenti e gli attributi di profilo che stai inviando alla destinazione e puoi pianificare e inviare i dati alla destinazione.

Per attivare i segmenti nella nuova destinazione, è necessario eseguire un’operazione JSON PATCH, simile all’esempio seguente. Puoi attivare più segmenti e attributi di profilo in una sola chiamata. Per ulteriori informazioni su JSON PATCH, consulta la [specifica RFC](https://tools.ietf.org/html/rfc6902).

**Formato API**

```http
PATCH /flows
```

**Richiesta**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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

* `{DATAFLOW_ID}`: Utilizza il flusso di dati ottenuto nel passaggio precedente.
* `{ETAG}`: Utilizza il tag ottenuto nel passaggio precedente.
* `{SEGMENT_ID}`: Fornisci l’ID del segmento da esportare a questa destinazione. Per recuperare gli ID dei segmenti per i segmenti che si desidera attivare, vai su **https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/**, seleziona **[!UICONTROL API Servizio di segmentazione]** nel menu di navigazione a sinistra e cerca l&#39;operazione `GET /segment/definitions` in **[!UICONTROL Definizioni dei segmenti]**.
* `{PROFILE_ATTRIBUTE}`: Ad esempio,  `personalEmail.address` o  `person.lastName`

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
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`: Utilizza il flusso di dati del passaggio precedente.
* `{ETAG}`: Utilizza il tag del passaggio precedente.

**Risposta**

La risposta restituita deve includere nel parametro `transformations` i segmenti e gli attributi di profilo inviati nel passaggio precedente. Di seguito è riportato un parametro di esempio `transformations` nella risposta:

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
> Oltre agli attributi di profilo e ai segmenti nel passaggio [Attiva i dati nella nuova destinazione](#activate-data), i dati esportati in [!DNL AWS Kinesis] e [!DNL Azure Event Hubs] includeranno anche informazioni sulla mappa di identità. Rappresenta le identità dei profili esportati (ad esempio [ECID](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html), mobile ID, Google ID, indirizzo e-mail, ecc.). Vedi un esempio qui sotto.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
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

## Utilizzo delle raccolte Postman per connettersi alle destinazioni in streaming  {#collections}

Per collegarti alle destinazioni di streaming descritte in questa esercitazione in modo più semplice, puoi utilizzare [[!DNL Postman]](https://www.postman.com/).

[!DNL Postman] è uno strumento che puoi utilizzare per effettuare chiamate API e gestire le librerie di chiamate e ambienti predefiniti.

Per questa esercitazione specifica sono state aggiunte le seguenti [!DNL Postman] raccolte:

* [!DNL AWS Kinesis] [!DNL Postman] raccolta
* [!DNL Azure Event Hubs] [!DNL Postman] raccolta

Fai clic [qui](../assets/api/streaming-destination/DestinationPostmanCollection.zip) per scaricare l&#39;archivio delle raccolte.

Ogni raccolta include le richieste e le variabili di ambiente necessarie, rispettivamente per [!DNL AWS Kinesis] e [!DNL Azure Event Hub].

### Come utilizzare le raccolte Postman

Per connettersi correttamente alle destinazioni utilizzando le raccolte [!DNL Postman] allegate, effettua le seguenti operazioni:

* Scarica e installa [!DNL Postman];
* [](../assets/api/streaming-destination/DestinationPostmanCollection.zip) Scaricare e decomprimere le raccolte allegate;
* Importa le raccolte dalle loro cartelle corrispondenti in Postman;
* Compila le variabili d&#39;ambiente secondo le istruzioni del presente articolo;
* Esegui le richieste [!DNL API] da Postman, in base alle istruzioni contenute in questo articolo.

## Passaggi successivi

Seguendo questa esercitazione, hai collegato Platform a una delle tue destinazioni di streaming preferite e hai impostato un flusso di dati per la rispettiva destinazione. I dati in uscita possono ora essere utilizzati nella destinazione per l’analisi dei clienti o per qualsiasi altra operazione di dati che desideri eseguire. Per ulteriori informazioni, consulta le pagine seguenti:

* [Panoramica sulle destinazioni](../home.md)
* [Panoramica del catalogo delle destinazioni](../catalog/overview.md)
