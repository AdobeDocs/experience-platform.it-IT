---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare destinazioni di e-mail marketing
topic: tutorial
translation-type: tm+mt
source-git-commit: d833257b4dffbf2a02ab4a3fc7a6a9e7347e7df5
workflow-type: tm+mt
source-wordcount: '1611'
ht-degree: 1%

---


# Creare destinazioni di e-mail marketing e attivare i dati in  Adobe  [!DNL Real-time Customer Data Platform]

Questa esercitazione illustra come utilizzare le chiamate API per connettersi ai dati Adobe Experience Platform, creare una destinazione [di marketing per](../../rtcdp/destinations/email-marketing-destinations.md)e-mail, creare un flusso di dati per la nuova destinazione creata e attivare i dati per la nuova destinazione creata.

Questa esercitazione utilizza la  destinazione Adobe Campaign in tutti gli esempi, ma i passaggi sono identici per tutte le destinazioni di e-mail marketing.

![Panoramica: i passaggi per creare una destinazione e attivare i segmenti](/help/rtcdp/destinations/assets/flow-api-destinations-steps-overview.png)

Se preferite utilizzare l&#39;interfaccia utente in  Adobe  CDP in tempo reale per collegare una destinazione e attivare i dati, consultate le esercitazioni [Connetti una destinazione](../../rtcdp/destinations/connect-destination.md) e [Attiva profili e segmenti a una destinazione](../../rtcdp/destinations/activate-destinations.md) .

## introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
* [!DNL Catalog Service](../../catalog/home.md): [!DNL Catalog] è il sistema di record per la posizione dei dati e la linea all&#39;interno [!DNL Experience Platform].
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per attivare i dati per le destinazioni di marketing tramite e-mail in CDP  Adobe in tempo reale.

### Raccogli credenziali richieste

Per completare i passaggi di questa esercitazione, devi disporre delle seguenti credenziali, a seconda del tipo di destinazioni a cui stai connettendo e a cui stai attivando i segmenti.

* Per le connessioni [!DNL Amazon] S3 alle piattaforme di e-mail marketing: `accessId`, `secretKey`
* Per le connessioni SFTP alle piattaforme di e-mail marketing: `domain`, `port`, `username`, `password` o `ssh key` (a seconda del metodo di connessione alla posizione FTP)

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli i valori delle intestazioni obbligatorie e facoltative

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Le risorse in [!DNL Experience Platform] possono essere isolate in sandbox virtuali specifiche. Nelle richieste alle [!DNL Platform] API, potete specificare il nome e l&#39;ID della sandbox in cui avrà luogo l&#39;operazione. Questi sono parametri facoltativi.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!Nota]
>Per ulteriori informazioni sulle sandbox in [!DNL Experience Platform], consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* Content-Type: `application/json`

<!--

### Definitions

Before starting this tutorial, familiarize yourself with the following terms which we'll use throughout the tutorial:

**Flow**: 

**Base Connection**: 

**Target Connection**: 

**Source Connection**: 

-->

### Swagger, documentazione

In questa esercitazione potete trovare la documentazione di riferimento associata a tutte le chiamate API in Swagger. Consulta la documentazione API del servizio [di flusso  Adobe.io](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml). È consigliabile utilizzare questa esercitazione e la pagina della documentazione Swagger in parallelo.

## Ottenere l&#39;elenco delle destinazioni disponibili {#get-the-list-of-available-destinations}

![Passaggi di destinazione - Panoramica passo 1](/help/rtcdp/destinations/assets/flow-api-destinations-step1.png)

Come primo passo, devi decidere a quale destinazione di e-mail marketing inviare i dati. Per iniziare, esegui una chiamata per richiedere un elenco di destinazioni disponibili a cui puoi collegare e attivare i segmenti. Eseguite la seguente richiesta di GET all&#39; `connectionSpecs` endpoint per restituire un elenco di destinazioni disponibili:

**Formato API**

```http
GET /connectionSpecs
```

**Richiesta**

<!--

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \    
    -H 'Content-Type: application/json' \
```

-->

```
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Risposta**

Una risposta corretta contiene un elenco delle destinazioni disponibili e dei relativi identificatori univoci (`id`). Memorizzate il valore della destinazione che intendete utilizzare, come sarà necessario in ulteriori passaggi. Ad esempio, se vuoi connettere e distribuire segmenti a  Adobe Campaign, cerca il frammento seguente nella risposta:

```json
{
    "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
  "name": "Adobe Campaign",
  ...
  ...
}
```

## Connessione ai [!DNL Experience Platform] dati {#connect-to-your-experience-platform-data}

![Passaggi di destinazione - Panoramica passo 2](/help/rtcdp/destinations/assets/flow-api-destinations-step2.png)

Successivamente, è necessario connettersi ai [!DNL Experience Platform] dati, in modo da poter esportare i dati del profilo e attivarli nella destinazione desiderata. Si tratta di due sottogruppi descritti di seguito.

1. Innanzitutto, è necessario eseguire una chiamata per autorizzare l&#39;accesso ai dati in [!DNL Experience Platform], configurando una connessione di base.
2. Quindi, utilizzando l&#39;ID connessione di base, effettuerai un&#39;altra chiamata in cui creerai una connessione di origine, che stabilirà la connessione ai tuoi [!DNL Experience Platform] dati.


### Autorizza l&#39;accesso ai tuoi dati in [!DNL Experience Platform]

**Formato API**

```http
POST /connections
```

**Richiesta**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
            
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC}",
                "version": "1.0"
            }
           }'
```

-->

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME} \
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


* `{CONNECTION_SPEC_ID}`: Utilizzate l&#39;ID delle specifiche di connessione per Unified Profile Service - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Risposta**

Una risposta corretta contiene l&#39;identificatore univoco (`id`) della connessione di base. Memorizzate questo valore come richiesto nel passaggio successivo per creare la connessione di origine.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Connessione ai [!DNL Experience Platform] dati

**Formato API**

```http
POST /sourceConnections
```

**Richiesta**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
  "name": "Connecting to Unified Profile Service",
  "description": "Optional",
  "baseConnectionId": "{BASE_CONNECTION_ID}",
  "connectionSpec": {
    "id": "{CONNECTION_SPEC}",
    "version": "1.0"
  },
  "data": {
    "format": "CSV",
    "schema": null
  }
  }
```

-->

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Unified Profile Service",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "CSV",
                "schema": null
            },
            "params" : {}
}'
```

* `{BASE_CONNECTION_ID}`: Utilizzate l&#39;ID ottenuto nel passaggio precedente.
* `{CONNECTION_SPEC_ID}`: Utilizzate l&#39;ID della specifica di connessione per [!DNL Unified Profile Service] - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Risposta**

Una risposta corretta restituisce l’identificatore univoco (`id`) per la nuova connessione di origine a [!DNL Unified Profile Service]. Questo conferma che la connessione ai [!DNL Experience Platform] dati è stata completata. Memorizza questo valore come richiesto in un passaggio successivo.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Connessione alla destinazione di e-mail marketing {#connect-to-email-marketing-destination}

![Passaggi di destinazione - Panoramica passo 3](/help/rtcdp/destinations/assets/flow-api-destinations-step3.png)

In questo passaggio, state configurando una connessione alla destinazione di marketing e-mail desiderata. Si tratta di due sottogruppi descritti di seguito.

1. Innanzitutto, è necessario eseguire una chiamata per autorizzare l&#39;accesso al provider del servizio e-mail, configurando una connessione di base.
2. Quindi, utilizzando l&#39;ID connessione di base, effettuerai un&#39;altra chiamata in cui creerai una connessione di destinazione, che specifica la posizione nell&#39;account di archiviazione in cui verranno inviati i dati esportati, nonché il formato dei dati che verranno esportati.

### Autorizzare l&#39;accesso alla destinazione di marketing delle e-mail

**Formato API**

```http
POST /connections
```

**Richiesta**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
            
            "name": "S3 Connection for Adobe Campaign",
            "description": "ACME company holiday campaign",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC}",
                "version": "1.0"
            },
            "auth": {
                "specName": "{S3 or SFTP}",
                "params": {
                    "accessId": "{ACCESS_ID}",
                    "secretKey": "{SECRET_KEY}"
                }
            }
           }'
```

-->

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "S3 Connection for Adobe Campaign",
    "description": "your company's holiday campaign",
    "connectionSpec": {
        "id": "{_CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "auth": {
        "specName": "{S3 or SFTP}",
        "params": {
            "accessId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}"
        }
    }
}'
```

* `{CONNECTION_SPEC_ID}`: Utilizza l&#39;ID delle specifiche di connessione ottenuto nel passaggio [Ottieni l&#39;elenco delle destinazioni](#get-the-list-of-available-destinations)disponibili.
* `{S3 or SFTP}`: compila il tipo di connessione desiderato per questa destinazione. Nel catalogo [di](../../rtcdp/destinations/destinations-catalog.md)destinazione, scorrete fino alla destinazione desiderata per verificare se sono supportati i tipi di connessione S3 e/o SFTP.
* `{ACCESS_ID}`: L&#39;ID di accesso per la posizione di archiviazione [!DNL Amazon] S3.
* `{SECRET_KEY}`: Chiave segreta per la posizione di archiviazione [!DNL Amazon] S3.

**Risposta**

Una risposta corretta contiene l&#39;identificatore univoco (`id`) della connessione di base. Archiviate questo valore come richiesto nel passaggio successivo per creare una connessione di destinazione.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Specificare la posizione di memorizzazione e il formato dei dati

**Formato API**

```http
POST /targetConnections
```

**Richiesta**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \    
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
   "baseConnectionId": "{BASE_CONNECTION_ID}",
   "name": "TargetConnection for Adobe Campaign",
   "data": {
       "format": "CSV",
       "schema": {
           "id": "1.0",
           "version": "1.0"
       },
    "connectionSpec": {
    "id": "{CONNECTION_SPEC_ID}",
    "version": "1.0"
   },
   "params": {
       "mode": "S3",
       "bucketName": "{BUCKETNAME}",
       "path": "{FILEPATH}"
    }
    }
```

-->

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Adobe Campaign",
    "description": "Connection to Adobe Campaign",
    "baseConnection": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKETNAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
}'
```

* `{BASE_CONNECTION_ID}`: Utilizzate l&#39;ID di connessione di base ottenuto nel passaggio precedente.
* `{CONNECTION_SPEC_ID}`: Utilizzare le specifiche di connessione ottenute nel passaggio [Ottenere l&#39;elenco delle destinazioni](#get-the-list-of-available-destinations)disponibili.
* `{BUCKETNAME}`: Il bucket [!DNL Amazon] S3, dove CDP in tempo reale depositerà l&#39;esportazione dei dati.
* `{FILEPATH}`: Percorso nella directory del bucket [!DNL Amazon] S3 in cui il CDP in tempo reale depositerà l&#39;esportazione dei dati.

**Risposta**

Una risposta corretta restituisce l’identificatore univoco (`id`) per la nuova connessione di destinazione alla destinazione di marketing dell’e-mail. Memorizza questo valore come richiesto nei passaggi successivi.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Creare un flusso di dati

![Passaggi di destinazione - Panoramica passo 4](/help/rtcdp/destinations/assets/flow-api-destinations-step4.png)

Utilizzando gli ID ottenuti nei passaggi precedenti, ora puoi creare un flusso di dati tra [!DNL Experience Platform] i dati e la destinazione in cui attiverai i dati. Considerate questo passaggio come la costruzione della pipeline, attraverso la quale i dati scorreranno successivamente, tra la destinazione [!DNL Experience Platform] e quella desiderata.

Per creare un flusso di dati, eseguite una richiesta di POST, come mostrato di seguito, fornendo al contempo i valori indicati di seguito all&#39;interno del payload.

Eseguite la seguente richiesta di POST per creare un flusso di dati.

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
   
        "name": "Activate segments to Adobe Campaign",
        "description": "This operation creates a dataflow which we will later use to activate segments to Adobe Campaign",
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
                    "segmentSelectors": {
                        "selectors": []
                    },
                    "profileSelectors": {
                        "selectors": []
                    }
                }
            }
        ]
    }
```

* `{FLOW_SPEC_ID}`: Utilizzate il flusso per la destinazione di e-mail marketing a cui desiderate connettervi. Per ottenere la specifica di flusso, eseguire un&#39;operazione di GET sull&#39; `flowspecs` endpoint. Consulta la documentazione Swagger qui: https://platform.adobe.io/data/foundation/flowservice/swagger#/Flow%20Specs%20API/getFlowSpecs. Nella risposta, cercate `upsTo` e copiate l&#39;ID corrispondente della destinazione di e-mail marketing a cui desiderate connettervi. Ad esempio, per  Adobe Campaign, cercate `upsToCampaign` e copiate il `id` parametro.
* `{SOURCE_CONNECTION_ID}`: Utilizzate l&#39;ID di connessione di origine ottenuto nel passaggio [Connetti al Experience Platform](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`: Utilizzate l&#39;ID di connessione di destinazione ottenuto nel passaggio [Connetti alla destinazione](#connect-to-email-marketing-destination)di e-mail marketing.

**Risposta**

Una risposta corretta restituisce l’ID (`id`) del flusso di dati appena creato e un ID `etag`. Prendete nota di entrambi i valori. come previsto nel passaggio successivo, per attivare i segmenti.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Attivare i dati per la nuova destinazione

![Passaggi di destinazione - Panoramica passo 5](/help/rtcdp/destinations/assets/flow-api-destinations-step5.png)

Dopo aver creato tutte le connessioni e il flusso di dati, ora puoi attivare i dati del profilo nella piattaforma di e-mail marketing. In questo passaggio, puoi selezionare i segmenti e gli attributi di profilo che stai inviando alla destinazione e pianificare e inviare i dati alla destinazione.

Per attivare i segmenti nella nuova destinazione, è necessario eseguire un&#39;operazione PATCH JSON, simile all&#39;esempio seguente. Puoi attivare più segmenti e attributi di profilo in una sola chiamata. Per ulteriori informazioni sul PATCH JSON, consultate la specifica [](https://tools.ietf.org/html/rfc6902)RFC.

**Formato API**

```http
PATCH /flows
```

**Richiesta**

```
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

* `{DATAFLOW_ID}`: Utilizzare il flusso di dati ottenuto nel passaggio precedente.
* `{ETAG}`: Utilizzate il tag ottenuto nel passaggio precedente.
* `{SEGMENT_ID}`: Specifica l&#39;ID del segmento da esportare in questa destinazione. Per recuperare gli ID del segmento per i segmenti da attivare, andate a https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/ e cercate l’ `GET /segment/jobs` operazione.
* `{PROFILE_ATTRIBUTE}`: Ad esempio, `"person.lastName"`

**Risposta**

Cercate una risposta OK 202. Non viene restituito alcun corpo di risposta. Per verificare che la richiesta fosse corretta, vedere il passaggio successivo, Convalida del flusso di dati.

## Convalida del flusso di dati

![Passaggi di destinazione - panoramica passo 6](/help/rtcdp/destinations/assets/flow-api-destinations-step6.png)

Come ultimo passaggio nell&#39;esercitazione, devi verificare che i segmenti e gli attributi di profilo siano stati mappati correttamente al flusso di dati.

Per convalidarlo, eseguire la seguente richiesta di GET:

**Formato API**

```http
GET /flows
```

**Richiesta**

```
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`: Utilizzare il flusso di dati del passaggio precedente.
* `{ETAG}`: Utilizzate il tag del passaggio precedente.

**Risposta**

La risposta restituita deve includere nel `transformations` parametro i segmenti e gli attributi di profilo inviati nel passaggio precedente. Un `transformations` parametro di esempio nella risposta potrebbe essere simile al seguente:

```
"transformations": [
    {
        "name": "GeneralTransform",
        "params": {
            "profileSelectors": {
                "selectors": []
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

## Passaggi successivi

Seguendo questa esercitazione, hai collegato con successo CDP in tempo reale a una delle tue destinazioni di e-mail marketing preferite e hai configurato un flusso di dati per la rispettiva destinazione. I dati in uscita possono ora essere utilizzati nella destinazione per campagne e-mail, pubblicità mirata e molti altri casi di utilizzo. Per ulteriori informazioni, consulta le pagine seguenti:

* [Panoramica sulle destinazioni](../../rtcdp/destinations/destinations-overview.md)
* [Panoramica del catalogo delle destinazioni](../../rtcdp/destinations/destinations-catalog.md)