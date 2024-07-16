---
title: Creare una connessione di origine e un flusso di dati per gli eventi SugarCRM tramite l’API del servizio Flusso
description: Scopri come collegare Adobe Experience Platform a eventi SugarCRM utilizzando l’API del servizio Flusso.
exl-id: 12d08010-569c-4111-ba95-697c6ce6f637
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1941'
ht-degree: 2%

---

# (Beta) Creare una connessione di origine e un flusso di dati per [!DNL SugarCRM Events] utilizzando l&#39;API del servizio Flusso

>[!NOTE]
>
>L&#39;origine [!DNL SugarCRM Events] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, vedere la [panoramica origini](../../../../home.md#terms-and-conditions).

Il seguente tutorial illustra i passaggi necessari per creare una connessione di origine [!DNL SugarCRM Events] e un flusso di dati per portare i dati degli eventi [[!DNL SugarCRM]](https://www.sugarcrm.com/) in Adobe Experience Platform utilizzando l&#39;[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL SugarCRM] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Per connettere [!DNL SugarCRM Events] a Platform, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| `host` | L’endpoint API di SugarCRM a cui l’origine si connette. | `developer.salesfusion.com` |
| `username` | Nome utente dell’account sviluppatore SugarCRM. | `abc.def@example.com@sugarmarketdemo000.com` |
| `password` | Password dell’account sviluppatore SugarCRM. | `123456789` |

## Connetti [!DNL SugarCRM Events] a Platform utilizzando l&#39;API [!DNL Flow Service]

Di seguito vengono descritti i passaggi necessari per autenticare l&#39;origine [!DNL SugarCRM], creare una connessione di origine e creare un flusso di dati per portare in Experience Platform i dati degli eventi.

### Creare una connessione di base {#base-connection}

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL SugarCRM Events] come parte del corpo della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL SugarCRM Events]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Events base connection",
      "description": "Create a live inbound connection to your SugarCRM Events instance, to ingest both historic and scheduled data into Experience Platform",
      "connectionSpec": {
          "id": "59a4b493-a615-40f9-bd38-f823d0909a2b",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Refresh Code",
          "params": {
              "host": "developer.salesfusion.com",
              "username": "{SUGARCRM_DEVELOPER_ACCOUNT_USERNAME}",
              "password": "{SUGARCRM_DEVELOPER_ACCOUNT_PASSWORD}"
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
| `auth.params.host` | Host API SugarCRM: *developer.salesfusion.com* |
| `auth.params.username` | Nome utente dell’account sviluppatore SugarCRM. |
| `auth.params.password` | Password dell’account sviluppatore SugarCRM. |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione di base appena creata, incluso il relativo identificatore univoco di connessione (`id`). Questo ID è necessario per esplorare la struttura e il contenuto del file sorgente nel passaggio successivo.

```json
{
     "id": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
     "etag": "\"4d08164f-0000-0200-0000-6368b7bf0000\""
}
```

### Esplora l’origine {#explore}

Utilizzando l’ID connessione di base generato nel passaggio precedente, puoi esplorare file e directory eseguendo richieste GET.
Utilizzare le seguenti chiamate per trovare il percorso del file che si desidera inserire in [!DNL Platform]:

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

Quando si eseguono richieste di GET per esplorare la struttura e il contenuto dei file dell’origine, è necessario includere i parametri di query elencati nella tabella seguente:

| Parametro | Descrizione |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | ID della connessione di base generato nel passaggio precedente. |
| `objectType=rest` | Tipo di oggetto che si desidera esplorare. Attualmente, questo valore è sempre impostato su `rest`. |
| `{OBJECT}` | Questo parametro è necessario solo quando si visualizza una directory specifica. Il relativo valore rappresenta il percorso della directory che desideri esplorare. Per questa origine il valore sarebbe `json`. |
| `fileType=json` | Il tipo di file che desideri portare su Platform. Attualmente, `json` è l&#39;unico tipo di file supportato. |
| `{PREVIEW}` | Valore booleano che definisce se il contenuto della connessione supporta l’anteprima. |
| `{SOURCE_PARAMS}` | Definisce i parametri per il file sorgente da portare a Platform. Per recuperare il tipo di formato accettato per `{SOURCE_PARAMS}`, è necessario codificare l&#39;intera stringa in base64. <br> [!DNL SugarCRM Events] non richiede alcun payload. Il valore per `{SOURCE_PARAMS}` viene passato come `{}`, codificato in base64 equivale a `e30=` come mostrato di seguito. |

**Richiesta**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=e30=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce la struttura del file su cui è stata eseguita la query. *Alcuni record sono stati rimossi per consentire una presentazione migliore.*

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "next": {
                "type": "string"
            },
            "page_number": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "previous": {},
            "total_count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "results": {
                "type": "object",
                "properties": {
                    "sessions": {
                        "type": "string"
                    },
                    "description": {
                        "type": "string"
                    },
                    "created_by": {
                        "type": "string"
                    },
                    "event_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "name": {
                        "type": "string"
                    },
                    "updated_by": {
                        "type": "string"
                    },
                    "updated_by_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "updated_date": {
                        "type": "string"
                    },
                    "created_date": {
                        "type": "string"
                    },
                    "created_by_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "event": {
                        "type": "string"
                    },
                    "folder_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "status": {
                        "type": "string"
                    }
                }
            },
            "page_size": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            }
        }
    },
    "data": [
        {
            "next": "https://developer.salesfusion.com/api/2.0/events/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 532,
            "count": 532,
            "results": {
                "event_id": 1,
                "event": "https://developer.salesfusion.com/api/2.0/events/1/",
                "sessions": "https://developer.salesfusion.com/api/2.0/events/1/sessions/",
                "name": "Test",
                "updated_date": "2022-08-30T11:20:11.813Z",
                "updated_by_id": 59,
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "created_date": "2022-08-28T23:40:11Z",
                "created_by_id": 59,
                "created_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "status": "Draft",
                "folder_id": 2
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/events/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 532,
            "count": 532,
            "results": {
                "event_id": 2,
                "event": "https://developer.salesfusion.com/api/2.0/events/2/",
                "sessions": "https://developer.salesfusion.com/api/2.0/events/2/sessions/",
                "name": "Infy Event",
                "description": "Test Event",
                "updated_date": "2022-09-15T16:26:43.697Z",
                "updated_by_id": 59,
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "created_date": "2022-09-27T23:40:11Z",
                "created_by_id": 59,
                "created_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "status": "Active",
                "folder_id": 2
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/events/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 532,
            "count": 532,
            "results": {
                "event_id": 3,
                "event": "https://developer.salesfusion.com/api/2.0/events/3/",
                "sessions": "https://developer.salesfusion.com/api/2.0/events/3/sessions/",
                "name": "Infy Workshop 1",
                "updated_date": "2022-10-11T18:12:28.767Z",
                "updated_by_id": 59,
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "created_date": "2022-09-14T23:40:11Z",
                "created_by_id": 59,
                "created_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "status": "Active",
                "folder_id": 2
            },
            "page_size": 100
        }
    ]
}
```

### Creare una connessione sorgente {#source-connection}

È possibile creare una connessione di origine effettuando una richiesta POST all&#39;API [!DNL Flow Service]. Una connessione di origine è costituita da un ID di connessione, un percorso del file di dati di origine e un ID della specifica di connessione.

**Formato API**

```https
POST /sourceConnections
```

**Richiesta**

La richiesta seguente crea una connessione di origine per [!DNL SugarCRM Events]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Source Connection",
      "description": "SugarCRM Source Connection",
      "baseConnectionId": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
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
| `baseConnectionId` | ID connessione di base di [!DNL SugarCRM Events]. Questo ID è stato generato in un passaggio precedente. |
| `connectionSpec.id` | ID della specifica di connessione corrispondente all&#39;origine. |
| `data.format` | Formato dei dati [!DNL SugarCRM Events] che si desidera acquisire. Attualmente, l&#39;unico formato di dati supportato è `json`. |

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;identificatore univoco (`id`) della connessione di origine appena creata. Questo ID è necessario in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "ffac1ae1-c137-4133-9f8d-0279468c11c9",
    "etag": "\"ed05abc3-0000-0200-0000-6368b3280000\""
}
```

### Creare uno schema XDM di destinazione {#target-schema}

Per utilizzare i dati sorgente in Platform, è necessario creare uno schema di destinazione che strutturi i dati sorgente in base alle tue esigenze. Lo schema di destinazione viene quindi utilizzato per creare un set di dati di Platform in cui sono contenuti i dati di origine.

È possibile creare uno schema XDM di destinazione eseguendo una richiesta POST all&#39;API [Schema Registry](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Per i passaggi dettagliati su come creare uno schema XDM di destinazione, consulta l&#39;esercitazione su [creazione di uno schema utilizzando l&#39;API](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html#create).

### Creare un set di dati di destinazione {#target-dataset}

È possibile creare un set di dati di destinazione eseguendo una richiesta POST all&#39;API [Catalog Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), fornendo l&#39;ID dello schema di destinazione all&#39;interno del payload.

Per i passaggi dettagliati su come creare un set di dati di destinazione, consulta l&#39;esercitazione su [creazione di un set di dati utilizzando l&#39;API](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html).

### Creare una connessione di destinazione {#target-connection}

Una connessione di destinazione rappresenta la connessione alla destinazione in cui devono essere memorizzati i dati acquisiti. Per creare una connessione di destinazione, devi fornire l’ID di specifica della connessione fissa che corrisponde al data lake. ID: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ora disponi degli identificatori univoci, di uno schema di destinazione, di un set di dati di destinazione e dell’ID della specifica di connessione al data lake. Utilizzando questi identificatori, è possibile creare una connessione di destinazione utilizzando l&#39;API [!DNL Flow Service] per specificare il set di dati che conterrà i dati di origine in entrata.

**Formato API**

```https
POST /targetConnections
```

**Richiesta**

La richiesta seguente crea una connessione di destinazione per [!DNL SugarCRM Events]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Target Connection Generic Rest",
      "description": "SugarCRM Target Connection Generic Rest",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b156e6f818f923e048199173c45e55e20fd2487f5eb03d22",
              "version": "1.22"
          }
      },
      "params": {
          "dataSetId": "6365389d1d37d01c077a81da"
      }
  }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Nome della connessione di destinazione. Assicurati che il nome della connessione di destinazione sia descrittivo, in quanto può essere utilizzato per cercare informazioni sulla connessione di destinazione. |
| `description` | Valore facoltativo che è possibile includere per fornire ulteriori informazioni sulla connessione di destinazione. |
| `connectionSpec.id` | ID della specifica di connessione corrispondente al data lake. ID corretto: `6b137bf6-d2a0-48c8-914b-d50f4942eb85`. |
| `data.format` | Formato dei dati [!DNL SugarCRM Events] che si desidera acquisire. |
| `params.dataSetId` | ID del set di dati di destinazione recuperato in un passaggio precedente. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco della nuova connessione di destinazione (`id`). Questo ID è richiesto nei passaggi successivi.

```json
{
    "id": "dfe9113e-be98-4d63-80a9-f41761721049",
    "etag": "\"84050267-0000-0200-0000-6368b3640000\""
}
```

### Creare una mappatura {#mapping}

Per poter acquisire i dati di origine in un set di dati di destinazione, è necessario prima mapparli sullo schema di destinazione a cui il set di dati di destinazione aderisce. Ciò si ottiene eseguendo una richiesta POST all&#39;API [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) con mappature dati definite nel payload della richiesta.

**Formato API**

```http
POST /conversion/mappingSets
```

**Richiesta**

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
          "source": "results.created_by",
          "destination": "_extconndev.created_by"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.created_by_id",
          "destination": "_extconndev.created_by_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.created_date",
          "destination": "_extconndev.created_date"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.name",
          "destination": "_extconndev.name_event"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.event_id",
          "destination": "_extconndev.id_event"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.event_id",
          "destination": "_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.sessions",
          "destination": "_extconndev.sessions"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_by",
          "destination": "_extconndev.updated_by"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_by_id",
          "destination": "_extconndev.updated_by_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_date",
          "destination": "_extconndev.updated_date"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_date",
          "destination": "timestamp"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.event",
          "destination": "_extconndev.event"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.description",
          "destination": "_extconndev.description"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.folder_id",
          "destination": "_extconndev.folder_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.status",
          "destination": "_extconndev.status"
      }
      ]
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
    "id": "d3845beaceeb49669228973f5f937f89",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Creare un flusso {#flow}

L&#39;ultimo passaggio per portare i dati da [!DNL SugarCRM Events] a Platform consiste nel creare un flusso di dati. A questo punto sono stati preparati i seguenti valori obbligatori:

* [ID connessione Source](#source-connection)
* [ID connessione di destinazione](#target-connection)
* [ID di mappatura](#mapping)

Un flusso di dati è responsabile della pianificazione e della raccolta di dati da un’origine. Puoi creare un flusso di dati eseguendo una richiesta POST e fornendo i valori precedentemente menzionati all’interno del payload.

Per pianificare un’acquisizione, devi prima impostare il valore dell’ora di inizio su tempo epoca in secondi. Quindi impostare il valore della frequenza su uno di `hour` o `day`. Il valore dell’intervallo indica il periodo tra due acquisizioni consecutive. Il valore dell&#39;intervallo deve essere impostato come `1` o `24` a seconda della selezione `scheduleParams.frequency` di `hour` o `day`.

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
      "name": "SugarCRM Connector Description Flow Generic Rest",
      "description": "SugarCRM Connector Description Flow Generic Rest",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3"
      ],
      "targetConnectionIds": [
          "6b137bf6-d2a0-48c8-914b-d50f4942eb85"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "d3845beaceeb49669228973f5f937f89",
                  "mappingVersion": "0"
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1625040887",
          "frequency": "hour",
          "interval": 1
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
| `scheduleParams.frequency` | La frequenza con cui il flusso di dati raccoglierà i dati. I valori accettabili includono: `hour` o `day`. |
| `scheduleParams.interval` | L’intervallo indica il periodo tra due esecuzioni consecutive del flusso. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero. Il valore dell&#39;intervallo deve essere impostato come `1` o `24` a seconda della selezione `scheduleParams.frequency` di `hour` o `day`. |

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;ID (`id`) del flusso di dati appena creato. Puoi usare questo ID per monitorare, aggiornare o eliminare il flusso di dati.

```json
{
     "id": "fcd16140-81b4-422a-8f9a-eaa92796c4f4",
     "etag": "\"9200a171-0000-0200-0000-6368c1da0000\""
}
```

## Appendice

La sezione seguente fornisce informazioni sui passaggi possibili per monitorare, aggiornare ed eliminare il flusso di dati.

### Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni sulle esecuzioni del flusso, sullo stato di completamento e sugli errori. Per esempi API completi, consulta la guida su [monitoraggio dei flussi di dati di origine tramite API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### Aggiornare il flusso di dati

Aggiorna i dettagli del flusso di dati, ad esempio il nome e la descrizione, nonché la pianificazione dell&#39;esecuzione e i set di mappatura associati, effettuando una richiesta PATCH all&#39;endpoint `/flows` dell&#39;API [!DNL Flow Service] e fornendo al contempo l&#39;ID del flusso di dati. Quando si effettua una richiesta PATCH, è necessario fornire `etag` univoco del flusso di dati nell&#39;intestazione `If-Match`. Per esempi API completi, leggere la guida sull&#39;[aggiornamento dei flussi di dati di origine tramite API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### Aggiornare l’account

Aggiornare il nome, la descrizione e le credenziali dell&#39;account di origine eseguendo una richiesta PATCH all&#39;API [!DNL Flow Service] e fornendo l&#39;ID connessione di base come parametro di query. Quando si effettua una richiesta PATCH, è necessario fornire `etag` univoco dell&#39;account di origine nell&#39;intestazione `If-Match`. Per esempi API completi, consulta la guida in [aggiornamento dell&#39;account di origine tramite l&#39;API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### Eliminare il flusso di dati

Elimina il flusso di dati eseguendo una richiesta DELETE all&#39;API [!DNL Flow Service] e fornendo l&#39;ID del flusso di dati che desideri eliminare come parte del parametro di query. Per esempi API completi, consulta la guida su [eliminazione dei flussi di dati tramite l&#39;API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### Elimina l’account

Eliminare l&#39;account eseguendo una richiesta DELETE all&#39;API [!DNL Flow Service] e fornendo l&#39;ID connessione di base dell&#39;account che si desidera eliminare. Per esempi API completi, leggere la guida in [eliminazione dell&#39;account di origine tramite l&#39;API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).
