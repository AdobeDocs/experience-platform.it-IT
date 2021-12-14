---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Connettiti alle destinazioni di marketing e-mail e attiva i dati utilizzando l’API del servizio di flusso
description: Questo documento tratta la creazione di destinazioni di marketing e-mail utilizzando l’API Adobe Experience Platform
topic-legacy: tutorial
type: Tutorial
exl-id: 41fd295d-7cda-4ab1-a65e-b47e6c485562
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '1701'
ht-degree: 2%

---

# Connettiti alle destinazioni di marketing e-mail e attiva i dati utilizzando l’API del servizio di flusso

Questa esercitazione illustra come utilizzare le chiamate API per connettersi ai dati di Adobe Experience Platform, creare un [destinazione di e-mail marketing](../catalog/email-marketing/overview.md), crea un flusso di dati per la nuova destinazione creata e attiva i dati per la nuova destinazione creata.

Questa esercitazione utilizza la destinazione Adobe Campaign in tutti gli esempi, ma i passaggi sono identici per tutte le destinazioni di e-mail marketing.

![Panoramica : i passaggi per creare una destinazione e attivare i segmenti](../assets/api/email-marketing/overview.png)

Se preferisci utilizzare l’interfaccia utente di Platform per collegare una destinazione e attivare i dati, consulta la sezione [Collegare una destinazione](../ui/connect-destination.md) e [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../ui/activate-batch-profile-destinations.md) esercitazioni.

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] è il sistema di registrazione per la posizione dei dati e la derivazione all&#39;interno di [!DNL Experience Platform].
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per attivare i dati nelle destinazioni di e-mail marketing in Platform.

### Raccogli credenziali richieste

Per completare i passaggi descritti in questa esercitazione, devi disporre delle seguenti credenziali, a seconda del tipo di destinazioni a cui stai connettendo e attivando i segmenti.

* Per [!DNL Amazon] Connessioni S3 alle piattaforme di marketing e-mail: `accessId`, `secretKey`
* Per le connessioni SFTP alle piattaforme di marketing e-mail: `domain`, `port`, `username`, `password` o `ssh key` (a seconda del metodo di connessione alla posizione FTP)

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste e facoltative

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Risorse in [!DNL Experience Platform] possono essere isolate in sandbox virtuali specifiche. Nelle richieste a [!DNL Platform] API, puoi specificare il nome e l’ID della sandbox in cui avrà luogo l’operazione. Si tratta di parametri facoltativi.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Experience Platform], vedi [documentazione panoramica su sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* Content-Type: `application/json`

### Documentazione Swagger

In Swagger puoi trovare la documentazione di riferimento associata per tutte le chiamate API in questa esercitazione. Consulta la sezione [Documentazione API del servizio di flusso sull’Adobe I/O](https://www.adobe.io/experience-platform-apis/references/flow-service/). È consigliabile utilizzare questa esercitazione e la pagina della documentazione Swagger in parallelo.

## Ottieni l’elenco delle destinazioni disponibili {#get-the-list-of-available-destinations}

![Passaggio 1: panoramica dei passaggi di destinazione](../assets/api/email-marketing/step1.png)

Come primo passo, devi decidere a quale destinazione di marketing e-mail attivare i dati. Per iniziare, esegui una chiamata per richiedere un elenco di destinazioni disponibili a cui puoi collegare e attivare i segmenti. Esegui la seguente richiesta di GET al `connectionSpecs` per restituire un elenco di destinazioni disponibili:

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

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Risposta**

Una risposta corretta contiene un elenco delle destinazioni disponibili e dei relativi identificatori univoci (`id`). Memorizza il valore della destinazione che intendi utilizzare, come sarà necessario in ulteriori passaggi. Ad esempio, se desideri collegare e consegnare segmenti ad Adobe Campaign, cerca il seguente frammento nella risposta:

```json
{
    "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
  "name": "Adobe Campaign",
  ...
  ...
}
```

## Collegati al tuo [!DNL Experience Platform] dati {#connect-to-your-experience-platform-data}

![Passaggio 2: panoramica dei passaggi di destinazione](../assets/api/email-marketing/step2.png)

Successivamente, è necessario connettersi al [!DNL Experience Platform] in modo da esportare i dati del profilo e attivarli nella destinazione desiderata. Si tratta di due sottoregimi descritti di seguito.

1. Innanzitutto, devi eseguire una chiamata per autorizzare l’accesso ai tuoi dati in [!DNL Experience Platform], impostando una connessione di base.
2. Quindi, utilizzando l&#39;ID di connessione di base, effettuerai un&#39;altra chiamata in cui crei una connessione sorgente, che stabilisce la connessione al tuo [!DNL Experience Platform] dati.


### Autorizzare l’accesso ai dati in [!DNL Experience Platform]

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


* `{CONNECTION_SPEC_ID}`: Utilizza l’ID delle specifiche di connessione per il servizio profili - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Risposta**

Una risposta corretta contiene l&#39;identificatore univoco della connessione di base (`id`). Memorizza questo valore come necessario nel passaggio successivo per creare la connessione sorgente.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Collegati al tuo [!DNL Experience Platform] dati {#connect-to-platform-data}

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
  "name": "Connecting to Profile Service",
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
                "format": "CSV",
                "schema": null
            },
            "params": {}
}'
```

* `{BASE_CONNECTION_ID}`: Utilizza l&#39;ID ottenuto nel passaggio precedente.
* `{CONNECTION_SPEC_ID}`: Utilizza l’ID delle specifiche di connessione per [!DNL Profile Service] - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) per la nuova connessione sorgente a [!DNL Profile Service]. Ciò conferma che la connessione al [!DNL Experience Platform] dati. Memorizza questo valore come richiesto in un passaggio successivo.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Connessione a una destinazione di e-mail marketing {#connect-to-email-marketing-destination}

![Passaggi di destinazione: passaggio 3](../assets/api/email-marketing/step3.png)

In questo passaggio, stai configurando una connessione alla destinazione di marketing e-mail desiderata. Si tratta di due sottoregimi descritti di seguito.

1. Innanzitutto, devi eseguire una chiamata per autorizzare l’accesso al provider di servizi e-mail, impostando una connessione di base.
2. Quindi, utilizzando l&#39;ID di connessione di base, effettuerai un&#39;altra chiamata in cui crei una connessione di destinazione, che specifica la posizione nell&#39;account di archiviazione in cui verranno inviati i dati esportati, nonché il formato dei dati che verranno esportati.

### Autorizzare l’accesso alla destinazione di marketing e-mail

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

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "S3 Connection for Adobe Campaign",
    "description": "summer advertising campaign",
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

* `{CONNECTION_SPEC_ID}`: Utilizza l’ID della specifica di connessione ottenuto nel passaggio [Ottieni l’elenco delle destinazioni disponibili](#get-the-list-of-available-destinations).
* `{S3 or SFTP}`: compila il tipo di connessione desiderato per questa destinazione. In [catalogo di destinazione](../catalog/overview.md), scorri fino alla destinazione desiderata per verificare se i tipi di connessione S3 e/o SFTP sono supportati.
* `{ACCESS_ID}`: Il tuo ID di accesso per il tuo [!DNL Amazon] Percorso di archiviazione S3.
* `{SECRET_KEY}`: La tua chiave segreta per la tua [!DNL Amazon] Percorso di archiviazione S3.

**Risposta**

Una risposta corretta contiene l&#39;identificatore univoco della connessione di base (`id`). Memorizza questo valore come necessario nel passaggio successivo per creare una connessione di destinazione.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Specificare il percorso di archiviazione e il formato dei dati

[!DNL Adobe Experience Platform] esporta i dati per le destinazioni di marketing e archiviazione cloud sotto forma di [!DNL CSV] file.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] divide automaticamente i file di esportazione a 5 milioni di record (righe) per file. Ogni riga rappresenta un profilo.
>
>I nomi dei file divisi vengono aggiunti con un numero che indica che il file fa parte di un’esportazione più grande, in quanto tale: `filename.csv`, `filename_2.csv`, `filename_3.csv`.

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

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Adobe Campaign",
    "description": "Connection to Adobe Campaign",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
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

* `{BASE_CONNECTION_ID}`: Utilizza l&#39;ID di connessione di base ottenuto nel passaggio precedente.
* `{CONNECTION_SPEC_ID}`: Utilizza le specifiche di connessione ottenute nel passaggio [Ottieni l’elenco delle destinazioni disponibili](#get-the-list-of-available-destinations).
* `{BUCKETNAME}`: Le [!DNL Amazon] bucket S3, in cui Platform depositerà l’esportazione dei dati.
* `{FILEPATH}`: Il percorso nel [!DNL Amazon] Directory del bucket S3 in cui Platform depositerà l’esportazione dei dati.

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) per la nuova connessione di destinazione alla destinazione di marketing e-mail. Memorizza questo valore come richiesto nei passaggi successivi.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Creare un flusso di dati

![Passaggi di destinazione: passaggio 4](../assets/api/email-marketing/step4.png)

Utilizzando gli ID ottenuti nei passaggi precedenti, ora puoi creare un flusso di dati tra [!DNL Experience Platform] e la destinazione in cui verranno attivati i dati. Considera questo passaggio come la costruzione della pipeline, attraverso la quale i dati scorreranno successivamente, tra [!DNL Experience Platform] e la destinazione desiderata.

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

* `{FLOW_SPEC_ID}`: Utilizza il flusso per la destinazione di marketing e-mail a cui desideri connetterti. Per ottenere la specifica di flusso, esegui un’operazione di GET sul `flowspecs` punto finale. Vedi la documentazione Swagger qui: https://platform.adobe.io/data/foundation/flowservice/swagger#/Flow%20Specs%20API/getFlowSpecs. Nella risposta , cerca `upsTo` e copia l’ID corrispondente della destinazione di marketing e-mail a cui desideri connetterti. Ad esempio, per Adobe Campaign, cerca `upsToCampaign` e copia il `id` parametro .
* `{SOURCE_CONNECTION_ID}`: Utilizza l’ID di connessione sorgente ottenuto nel passaggio [Connettiti al tuo Experience Platform](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`: Utilizza l’ID di connessione di destinazione ottenuto nel passaggio [Connessione a una destinazione di e-mail marketing](#connect-to-email-marketing-destination).

**Risposta**

Una risposta corretta restituisce l&#39;ID (`id`) del flusso di dati appena creato e un `etag`. Annotare entrambi i valori. come li eseguirai nel passaggio successivo, per attivare i segmenti.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Attiva i dati nella nuova destinazione

![Passaggi di destinazione: passaggio 5](../assets/api/email-marketing/step5.png)

Dopo aver creato tutte le connessioni e il flusso di dati, ora puoi attivare i dati del profilo sulla piattaforma di e-mail marketing. In questo passaggio, seleziona i segmenti e gli attributi di profilo che stai inviando alla destinazione e puoi pianificare e inviare i dati alla destinazione.

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

* `{DATAFLOW_ID}`: Utilizza il flusso di dati ottenuto nel passaggio precedente.
* `{ETAG}`: Utilizza il tag ottenuto nel passaggio precedente.
* `{SEGMENT_ID}`: Fornisci l’ID del segmento da esportare a questa destinazione. Per recuperare gli ID del segmento per i segmenti che desideri attivare, passa a **https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/**, seleziona **[!UICONTROL API del servizio di segmentazione]** nel menu di navigazione a sinistra e cerca il `GET /segment/definitions` funzionamento **[!UICONTROL Definizioni dei segmenti]**.
* `{PROFILE_ATTRIBUTE}`: Esempio, `"person.lastName"`

**Risposta**

Cerca una risposta 202 OK. Non viene restituito alcun corpo di risposta. Per verificare che la richiesta fosse corretta, vedi il passaggio successivo, Convalida il flusso di dati.

## Convalidare il flusso di dati

![Passaggi di destinazione: passaggio 6](../assets/api/email-marketing/step6.png)

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

La risposta restituita deve includere nel `transformations` i segmenti e gli attributi di profilo inviati nel passaggio precedente. Un campione `transformations` nella risposta potrebbe essere simile al seguente:

```json
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

Seguendo questa esercitazione, hai collegato Platform a una delle tue destinazioni di e-mail marketing preferite e hai impostato un flusso di dati per la rispettiva destinazione. I dati in uscita possono ora essere utilizzati nella destinazione per campagne e-mail, pubblicità mirata e molti altri casi d’uso. Per ulteriori informazioni, consulta le pagine seguenti:

* [Panoramica sulle destinazioni](../home.md)
* [Panoramica del catalogo delle destinazioni](../catalog/overview.md)
