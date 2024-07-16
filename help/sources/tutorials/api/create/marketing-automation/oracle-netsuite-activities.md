---
title: Creazione di una connessione di origine e di un flusso di dati per attività NetSuite di Oracle mediante l'API del servizio Flusso
description: Scopri come creare una connessione di origine e un flusso di dati per portare i dati degli eventi di Oracle NetSuite all’Experience Platform utilizzando l’API del servizio Flusso.
hide: true
hidefromtoc: true
badge: Beta
exl-id: 4f695389-2261-469c-8d40-7bd29a4e7f77
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '1961'
ht-degree: 2%

---

# Creare una connessione di origine e un flusso di dati per [!DNL Oracle NetSuite Activities] utilizzando l&#39;API del servizio Flusso

>[!NOTE]
>
>L&#39;origine [!DNL Oracle NetSuite Activities] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, vedere la [panoramica origini](../../../../home.md#terms-and-conditions).

Leggi il seguente tutorial per scoprire come portare i dati degli eventi dal tuo account [!DNL Oracle NetSuite Activities] a Adobe Experience Platform utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Oracle NetSuite Activities] utilizzando l&#39;API [!DNL Flow Service].

### Autenticazione

Leggi la [[!DNL Oracle NetSuite] panoramica](../../../../connectors/marketing-automation/oracle-netsuite.md) per informazioni su come recuperare le credenziali di autenticazione.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Connetti [!DNL Oracle NetSuite Activities] a Platform utilizzando l&#39;API [!DNL Flow Service]

Segui la guida seguente per scoprire come autenticare l&#39;origine [!DNL Oracle NetSuite Activities], creare una connessione di origine e creare un flusso di dati per portare a Experience Platform i dati degli eventi.

### Creare una connessione di base {#base-connection}

Una connessione di base mantiene le informazioni tra l&#39;origine e l&#39;Experience Platform, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Oracle NetSuite Activities] come parte del corpo della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Oracle NetSuite Activities]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NeSuite Activities base connection",
      "description": "Authenticated base connection for Oracle NetSuite Activities",
      "connectionSpec": {
          "id": "fdf850b4-5a8d-4a5a-9ce8-4caef9abb2a8",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params": {
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
              "accessTokenUrl": "{ACCESS_TOKEN_URL}",
              "accessToken": "{ACCESS_TOKEN_URL}"
          }
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della connessione di base. Verificare che il nome della connessione di base sia descrittivo, in quanto è possibile utilizzarlo per cercare informazioni sulla connessione di base. |
| `description` | Valore facoltativo che è possibile includere per fornire ulteriori informazioni sulla connessione di base. |
| `connectionSpec.id` | ID della specifica di connessione dell&#39;origine. Questo ID può essere recuperato dopo che l&#39;origine è stata registrata e approvata tramite l&#39;API [!DNL Flow Service]. |
| `auth.specName` | Tipo di autenticazione utilizzato per autenticare l’origine in Platform. |
| `auth.params.clientId` | Il valore ID client quando crei il record di integrazione. Il processo per la creazione di un record di integrazione è disponibile [qui](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981). Il valore è una stringa di 64 caratteri simile a `7fce.....b42f`. |
| `auth.params.clientSecret` | Il valore ID client quando crei il record di integrazione. Il processo per la creazione di un record di integrazione è disponibile [qui](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981). Il valore è una stringa di 64 caratteri simile a `5c98.....1b46`. |
| `auth.params.accessTokenUrl` | L&#39;URL del token di accesso [!DNL NetSuite], simile a `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/auth/oauth2/v1/token`, in cui sostituirai ACCOUNT_ID con l&#39;ID account [!DNL NetSuite]. |
| `auth.params.accessToken` | Il valore del token di accesso viene generato alla fine del [passaggio due](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint) dell&#39;esercitazione [Flusso di concessione codice di autorizzazione OAuth 2.0](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow). La scadenza dei token di accesso è valida solo per 60 minuti. il valore è una stringa di 1024 caratteri formattata come JSON Web Token (JWT) simile a `eyJr......f4V0`. |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione di base appena creata, incluso il relativo identificatore univoco di connessione (`id`). Questo ID è necessario per esplorare la struttura e il contenuto del file sorgente nel passaggio successivo.

```json
{
    "id": "60c81023-99b4-4aae-9c31-472397576dd2",
    "etag": "\"fa003785-0000-0200-0000-6555c5310000\""
}
```

### Esplora l’origine {#explore}

Una volta ottenuto l&#39;ID connessione di base, è ora possibile esplorare il contenuto e la struttura dei dati di origine eseguendo una richiesta di GET all&#39;endpoint `/connections` e fornendo l&#39;ID connessione di base come parametro di query.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

**Richiesta**

Quando si eseguono richieste di GET per esplorare la struttura e il contenuto dei file dell’origine, è necessario includere i parametri di query elencati nella tabella seguente:

| Parametro | Descrizione |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | ID della connessione di base generato nel passaggio precedente. |
| `objectType=rest` | Tipo di oggetto che si desidera esplorare. Attualmente, questo valore è sempre impostato su `rest`. |
| `{OBJECT}` | Questo parametro è necessario solo quando si visualizza una directory specifica. Il relativo valore rappresenta il percorso della directory che desideri esplorare. Per questa origine il valore sarebbe `json`. |
| `fileType=json` | Il tipo di file che desideri portare su Platform. Attualmente, `json` è l&#39;unico tipo di file supportato. |
| `{PREVIEW}` | Valore booleano che definisce se il contenuto della connessione supporta l’anteprima. |
| `{SOURCE_PARAMS}` | Definisce i parametri per il file sorgente da portare a Platform. Per recuperare il formato accettato per `{SOURCE_PARAMS}`, è necessario codificare l&#39;intera stringa in base64. <br> Valore vuoto per [!DNL Oracle NetSuite Activities].</li></ul> |

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=e30%3D' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce una struttura JSON come segue:

+++Seleziona per visualizzare il payload JSON

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "totalResults": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "offset": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "hasMore": {
                "type": "boolean"
            },
            "links": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "rel": {
                            "type": "string"
                        },
                        "href": {
                            "type": "string"
                        }
                    }
                }
            },
            "items": {
                "type": "object",
                "properties": {
                    "owner": {
                        "type": "string"
                    },
                    "createddate": {
                        "type": "string"
                    },
                    "lastmodifieddate": {
                        "type": "string"
                    },
                    "accesslevel": {
                        "type": "string"
                    },
                    "alldayevent": {
                        "type": "string"
                    },
                    "message": {
                        "type": "string"
                    },
                    "startdate": {
                        "type": "string"
                    },
                    "title": {
                        "type": "string"
                    },
                    "organizer": {
                        "type": "string"
                    },
                    "response": {
                        "type": "string"
                    },
                    "links": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {}
                        }
                    },
                    "location": {
                        "type": "string"
                    },
                    "timedevent": {
                        "type": "string"
                    },
                    "id": {
                        "type": "string"
                    },
                    "status": {
                        "type": "string"
                    }
                }
            }
        }
    },
    "data": [
        {
            "totalResults": 13,
            "offset": 0,
            "count": 13,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "accesslevel": "BUSY",
                "alldayevent": "F",
                "createddate": "2022-12-15",
                "id": "5",
                "lastmodifieddate": "2022-12-15",
                "location": "Caffe West",
                "message": "Bring Monthly Results",
                "organizer": "-5",
                "owner": "-5",
                "response": "ACCEPTED",
                "startdate": "2022-12-15",
                "status": "CONFIRMED",
                "timedevent": "T",
                "title": "Meeting with Tom"
            }
        },
        {
            "totalResults": 13,
            "offset": 0,
            "count": 13,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "accesslevel": "BUSY",
                "alldayevent": "F",
                "createddate": "2023-02-01",
                "id": "103",
                "lastmodifieddate": "2023-02-01",
                "location": "Caffe West",
                "message": "Bring Monthly Results",
                "organizer": "-5",
                "owner": "-5",
                "response": "ACCEPTED",
                "startdate": "2022-12-15",
                "status": "CONFIRMED",
                "timedevent": "T",
                "title": "Meeting with Tom"
            }
        },
        {
            "totalResults": 13,
            "offset": 0,
            "count": 13,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "accesslevel": "BUSY",
                "alldayevent": "F",
                "createddate": "2023-11-09",
                "id": "204",
                "lastmodifieddate": "2023-11-09",
                "location": "Caffe West",
                "message": "Bring Monthly Results",
                "organizer": "-5",
                "owner": "-5",
                "response": "ACCEPTED",
                "startdate": "2023-12-15",
                "status": "CONFIRMED",
                "timedevent": "T",
                "title": "Meeting with Tom"
            }
        },
    ]
}
```

+++

### Creare una connessione sorgente {#source-connection}

È possibile creare una connessione di origine effettuando una richiesta POST all&#39;endpoint `/sourceConnections` dell&#39;API [!DNL Flow Service]. Una connessione di origine è costituita da un ID di connessione, un percorso del file di dati di origine e un ID della specifica di connessione.

**Formato API**

```https
POST /sourceConnections
```

**Richiesta**

La richiesta seguente crea una connessione di origine per [!DNL Oracle NetSuite Activities].

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Activities Source Connection",
      "description": "Oracle NetSuite Activities Source Connection",
      "baseConnectionId": "60c81023-99b4-4aae-9c31-472397576dd2",
      "connectionSpec": {
          "id": "fdf850b4-5a8d-4a5a-9ce8-4caef9abb2a8",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della connessione di origine. Assicurati che il nome della connessione sorgente sia descrittivo, in quanto può essere utilizzato per cercare informazioni sulla connessione sorgente. |
| `description` | Valore facoltativo che è possibile includere per fornire ulteriori informazioni sulla connessione di origine. |
| `baseConnectionId` | ID connessione di base di [!DNL Oracle NetSuite Activities]. Questo ID è stato generato in un passaggio precedente. |
| `connectionSpec.id` | ID della specifica di connessione corrispondente all&#39;origine. |
| `data.format` | Formato dei dati [!DNL Oracle NetSuite Activities] che si desidera acquisire. Attualmente, l&#39;unico formato di dati supportato è `json`. |

In caso di esito positivo, la risposta restituisce l&#39;identificatore univoco (`id`) della connessione di origine appena creata. Questo ID è necessario in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "574c049f-29fc-411f-be0d-f80002025f51",
    "etag": "\"0704acb3-0000-0200-0000-6555c5470000\""
}
```

### Creare uno schema XDM di destinazione {#target-schema}

Per utilizzare i dati sorgente in Platform, è necessario creare uno schema di destinazione che strutturi i dati sorgente in base alle tue esigenze. Lo schema di destinazione viene quindi utilizzato per creare un set di dati di Platform in cui sono contenuti i dati di origine.

È possibile creare uno schema XDM di destinazione eseguendo una richiesta POST all&#39;API [Schema Registry](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Per i passaggi dettagliati su come creare uno schema XDM di destinazione, consulta l&#39;esercitazione su [creazione di uno schema utilizzando l&#39;API](../../../../../xdm/api/schemas.md#create-a-schema).

### Creare un set di dati di destinazione {#target-dataset}

È possibile creare un set di dati di destinazione eseguendo una richiesta POST all&#39;API [Catalog Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), fornendo l&#39;ID dello schema di destinazione all&#39;interno del payload.

Per i passaggi dettagliati su come creare un set di dati di destinazione, consulta l&#39;esercitazione su [creazione di un set di dati utilizzando l&#39;API](../../../../../catalog/api/create-dataset.md).

### Creare una connessione di destinazione {#target-connection}

Una connessione di destinazione rappresenta la connessione alla destinazione in cui devono essere memorizzati i dati acquisiti. Per creare una connessione di destinazione, devi fornire l’ID della specifica di connessione fissa che corrisponde al data lake. ID: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ora disponi degli identificatori univoci, di uno schema di destinazione, di un set di dati di destinazione e dell’ID della specifica di connessione al data lake. Utilizzando questi identificatori, è possibile creare una connessione di destinazione utilizzando l&#39;API [!DNL Flow Service] per specificare il set di dati che conterrà i dati di origine in entrata.

**Formato API**

```https
POST /targetConnections
```

**Richiesta**

La richiesta seguente crea una connessione di destinazione per [!DNL Oracle NetSuite Activities]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Activities Target Connection Generic Rest",
      "description": "Oracle NetSuite Activities Target Connection Generic Rest",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
              "version": "1.2"
          }
      },
      "params": {
          "dataSetId": "65004470082ac828d2c3d6a0"
      }
  }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Nome della connessione di destinazione. Assicurati che il nome della connessione di destinazione sia descrittivo, in quanto può essere utilizzato per cercare informazioni sulla connessione di destinazione. |
| `description` | Valore facoltativo che è possibile includere per fornire ulteriori informazioni sulla connessione di destinazione. |
| `connectionSpec.id` | ID della specifica di connessione corrispondente al data lake. ID corretto: `6b137bf6-d2a0-48c8-914b-d50f4942eb85`. |
| `data.format` | Formato dei dati [!DNL Oracle NetSuite Activities] che si desidera acquisire. |
| `params.dataSetId` | ID del set di dati di destinazione recuperato in un passaggio precedente. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco della nuova connessione di destinazione (`id`). Questo ID è richiesto nei passaggi successivi.

```json
{
    "id": "382fc614-3c5b-46b9-a971-786fb0ae6c5d",
    "etag": "\"e0016100-0000-0200-0000-655707a40000\""
}
```

### Creare una mappatura {#mapping}

Per poter acquisire i dati di origine in un set di dati di destinazione, è necessario prima mapparli sullo schema di destinazione a cui il set di dati di destinazione aderisce. Ciò si ottiene eseguendo una richiesta POST all&#39;API [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) con mappature dati definite nel payload della richiesta.

**Formato API**

```http
POST /conversion/mappingSets
```

**Richiesta**

La richiesta seguente crea una mappatura per [!DNL DNL NetSuite Activities]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b156e6f818f923e048199173c45e55e20fd2487f5eb03d22",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.id",
            "destination": "_extconndev.NSA_ID"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.title",
            "destination": "_extconndev.NSA_title"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.createddate",
            "destination": "_extconndev.NSA_createddate"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.location",
            "destination": "_extconndev.NSA_location"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.lastmodifieddate",
            "destination": "_extconndev.NSA_lastmodifieddate"
        }
      ],
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `outputSchema.schemaRef.id` | ID dello schema XDM [target](#target-schema) generato in un passaggio precedente. |
| `mappings.sourceType` | Tipo di attributo di origine di cui viene eseguito il mapping. |
| `mappings.source` | L’attributo di origine che deve essere mappato su un percorso XDM di destinazione. |
| `mappings.destination` | Percorso XDM di destinazione in cui viene eseguito il mapping dell’attributo di origine. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della mappatura appena creata, incluso il relativo identificatore univoco (`id`). Questo valore è necessario in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "ddf0592bcc9d4ac391803f15f2429f87",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Creare un flusso {#flow}

L&#39;ultimo passaggio per portare i dati da [!DNL Oracle NetSuite Activities] a Platform consiste nel creare un flusso di dati. A questo punto sono stati preparati i seguenti valori obbligatori:

* [ID connessione Source](#source-connection)
* [ID connessione di destinazione](#target-connection)
* [ID di mappatura](#mapping)

Un flusso di dati è responsabile della pianificazione e della raccolta di dati da un’origine. Puoi creare un flusso di dati eseguendo una richiesta POST e fornendo i valori precedentemente menzionati all’interno del payload.

**Formato API**

```http
POST /flows
```

**Richiesta**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Oracle NetSuite Activities connector Flow Generic Rest",
    "description": "Oracle NetSuite Activities connector Description Flow Generic Rest",
    "flowSpec": {
        "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "d8827440-339f-428d-bf38-5e2ab1f0f7bb"
    ],
    "targetConnectionIds": [
        "e349a15e-c639-4047-8b2a-154aa7a857d7"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "10787532e0994eb686e76bdab69a9e88",
                "mappingVersion": 0
            }
        }
    ],
      "scheduleParams": {
          "startTime": 1700202649,
          "frequency": "once"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome del flusso di dati. Assicurati che il nome del flusso di dati sia descrittivo, in quanto può essere utilizzato per cercare informazioni sul flusso di dati. |
| `description` | Valore facoltativo che puoi includere per fornire ulteriori informazioni sul flusso di dati. |
| `flowSpec.id` | ID della specifica di flusso necessario per creare un flusso di dati. ID corretto: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | Versione corrispondente dell&#39;ID della specifica di flusso. Il valore predefinito è `1.0`. |
| `sourceConnectionIds` | L&#39;[ID connessione di origine](#source-connection) generato in un passaggio precedente. |
| `targetConnectionIds` | L&#39;ID [connessione di destinazione](#target-connection) generato in un passaggio precedente. |
| `transformations` | Questa proprietà contiene le varie trasformazioni che devono essere applicate ai dati. Questa proprietà è necessaria per portare dati non conformi a XDM su Platform. |
| `transformations.name` | Nome assegnato alla trasformazione. |
| `transformations.params.mappingId` | L&#39;[ID mappatura](#mapping) generato in un passaggio precedente. |
| `transformations.params.mappingVersion` | Versione corrispondente dell&#39;ID di mappatura. Il valore predefinito è `0`. |
| `scheduleParams.startTime` | Questa proprietà contiene informazioni sulla pianificazione dell’acquisizione del flusso di dati. |
| `scheduleParams.frequency` | La frequenza con cui il flusso di dati raccoglierà i dati. |
| `scheduleParams.interval` | L’intervallo indica il periodo tra due esecuzioni consecutive del flusso. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero. |

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;ID (`id`) del flusso di dati appena creato. Puoi usare questo ID per monitorare, aggiornare o eliminare il flusso di dati.

```json
{
     "id": "84c64142-1741-4b0b-95a9-65644eba0cf6",
     "etag": "\"3901770b-0000-0200-0000-655708970000\""
}
```

## Appendice

La sezione seguente fornisce informazioni sui passaggi possibili per monitorare, aggiornare ed eliminare il flusso di dati.

### Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni sulle esecuzioni del flusso, sullo stato di completamento e sugli errori. Per esempi API completi, consulta la guida su [monitoraggio dei flussi di dati di origine tramite API](../../monitor.md).

### Aggiornare il flusso di dati

Aggiorna i dettagli del flusso di dati, ad esempio il nome e la descrizione, nonché la pianificazione dell&#39;esecuzione e i set di mappatura associati, effettuando una richiesta PATCH all&#39;endpoint `/flows` dell&#39;API [!DNL Flow Service] e fornendo al contempo l&#39;ID del flusso di dati. Quando si effettua una richiesta PATCH, è necessario fornire `etag` univoco del flusso di dati nell&#39;intestazione `If-Match`. Per esempi API completi, leggere la guida sull&#39;aggiornamento dei flussi di dati di origine in [tramite API](../../update-dataflows.md).

### Aggiornare l’account

Aggiornare il nome, la descrizione e le credenziali dell&#39;account di origine eseguendo una richiesta PATCH all&#39;API [!DNL Flow Service] e fornendo l&#39;ID connessione di base come parametro di query. Quando si effettua una richiesta PATCH, è necessario fornire `etag` univoco dell&#39;account di origine nell&#39;intestazione `If-Match`. Per esempi API completi, consulta la guida in [aggiornamento dell&#39;account di origine tramite l&#39;API](../../update.md).

### Eliminare il flusso di dati

Elimina il flusso di dati eseguendo una richiesta DELETE all&#39;API [!DNL Flow Service] e fornendo l&#39;ID del flusso di dati che desideri eliminare come parte del parametro di query. Per esempi API completi, consulta la guida su [eliminazione dei flussi di dati tramite l&#39;API](../../delete-dataflows.md).

### Elimina l’account

Eliminare l&#39;account eseguendo una richiesta DELETE all&#39;API [!DNL Flow Service] e fornendo l&#39;ID connessione di base dell&#39;account che si desidera eliminare. Per esempi API completi, leggere la guida in [eliminazione dell&#39;account di origine tramite l&#39;API](../../delete.md).
