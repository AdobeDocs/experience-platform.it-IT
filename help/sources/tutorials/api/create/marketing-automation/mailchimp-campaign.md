---
keywords: Experience Platform;home;argomenti popolari;sorgenti;connettori;connettori sorgente;origini sdk;sdk;SDK
solution: Experience Platform
title: Creare un flusso di dati per la campagna Mailchimp utilizzando l’API del servizio di flusso
topic-legacy: tutorial
description: Scopri come collegare Adobe Experience Platform a MailChimp Campaign utilizzando l’API del servizio di flusso.
exl-id: fd4821c7-6fe1-4cad-8e13-3549dbe0ce98
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '2319'
ht-degree: 3%

---

# Creare un flusso di dati per [!DNL Mailchimp Campaign] utilizzo dell’API del servizio di flusso

L’esercitazione seguente illustra i passaggi necessari per creare una connessione sorgente e un flusso di dati per [!DNL Mailchimp Campaign] dati a Platform tramite [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prerequisiti

Prima di poterti connettere [!DNL Mailchimp] per Adobe Experience Platform utilizzando il codice di aggiornamento OAuth 2, devi prima recuperare il token di accesso per [!DNL MailChimp.] Consulta la sezione [[!DNL Mailchimp] Guida di OAuth 2](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/) per istruzioni dettagliate su come trovare il token di accesso.

## Creare una connessione di base {#base-connection}

Una volta recuperato il [!DNL Mailchimp] credenziali di autenticazione, ora puoi avviare il processo di creazione del flusso di dati per portare [!DNL Mailchimp Campaign] a Platform. Il primo passaggio nella creazione di un flusso di dati consiste nel creare una connessione di base.

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

[!DNL Mailchimp] supporta sia l’autenticazione di base che il codice di aggiornamento OAuth 2. Per informazioni su come eseguire l’autenticazione con uno dei due tipi di autenticazione, consulta gli esempi seguenti.

### Crea un [!DNL Mailchimp] connessione di base tramite autenticazione di base

Per creare una [!DNL Mailchimp] connessione di base utilizzando l’autenticazione di base, effettuare una richiesta di POST al `/connections` punto finale [!DNL Flow Service] API fornendo le credenziali `host`, `authorizationTestUrl`, `username`e `password`.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Mailchimp base connection with basic authentication",
      "description": "Mailchimp Campaign base connection with basic authentication",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della connessione di base. Assicurati che il nome della connessione di base sia descrittivo, in quanto puoi utilizzarlo per cercare informazioni sulla connessione di base. |
| `description` | (Facoltativo) Proprietà che è possibile includere per fornire ulteriori informazioni sulla connessione di base. |
| `connectionSpec.id` | ID della specifica di connessione dell&#39;origine. Questo ID può essere recuperato dopo la registrazione e l&#39;approvazione della sorgente tramite [!DNL Flow Service] API. |
| `auth.specName` | Tipo di autenticazione utilizzato per collegare l’origine a Platform. |
| `auth.params.host` | URL principale utilizzato per la connessione a [!DNL Mailchimp] API. Il formato dell’URL principale è `https://{DC}.api.mailchimp.com`, dove `{DC}` rappresenta il data center che corrisponde al tuo account. |
| `auth.params.authorizationTestUrl` | (Facoltativo) L&#39;URL del test di autorizzazione viene utilizzato per convalidare le credenziali durante la creazione di una connessione di base. Se non viene fornito, le credenziali vengono automaticamente controllate durante il passaggio di creazione della connessione di origine. |
| `auth.params.username` | Il nome utente che corrisponde al tuo [!DNL Mailchimp] conto. Questo è necessario per l’autenticazione di base. |
| `auth.params.password` | La password che corrisponde alla tua [!DNL Mailchimp] conto. Questo è necessario per l’autenticazione di base. |

**Risposta**

Una risposta corretta restituisce la nuova connessione di base creata, incluso l&#39;identificatore di connessione univoco (`id`). Questo ID è necessario per esplorare la struttura file e il contenuto della tua sorgente nel passaggio successivo.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

### Crea un [!DNL Mailchimp] connessione di base tramite codice di aggiornamento OAuth 2

Per creare una [!DNL Mailchimp] connessione di base tramite il codice di aggiornamento OAuth 2, effettuare una richiesta POST al `/connections` endpoint durante la fornitura delle credenziali `host`, `authorizationTestUrl`e `accessToken`.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Mailchimp base connection with OAuth 2 refresh code",
      "description": "Mailchimp Campaign base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "host": "{HOST}",
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della connessione di base. Assicurati che il nome della connessione di base sia descrittivo, in quanto puoi utilizzarlo per cercare informazioni sulla connessione di base. |
| `description` | (Facoltativo) Proprietà che è possibile includere per fornire ulteriori informazioni sulla connessione di base. |
| `connectionSpec.id` | ID della specifica di connessione dell&#39;origine. Questo ID può essere recuperato dopo la registrazione della sorgente utilizzando [!DNL Flow Service] API. |
| `auth.specName` | Il tipo di autenticazione utilizzato per autenticare l’origine in Platform. |
| `auth.params.host` | URL principale utilizzato per la connessione a [!DNL Mailchimp] API. Il formato dell’URL principale è `https://{DC}.api.mailchimp.com`, dove `{DC}` rappresenta il data center che corrisponde al tuo account. |
| `auth.params.authorizationTestUrl` | (Facoltativo) L&#39;URL di test dell&#39;autorizzazione viene utilizzato per convalidare le credenziali durante la creazione di una connessione di base. Se non viene fornito, le credenziali vengono automaticamente controllate durante il passaggio di creazione della connessione di origine. |
| `auth.params.accessToken` | Il token di accesso corrispondente utilizzato per autenticare l&#39;origine. Questo è necessario per l’autenticazione basata su OAuth. |

**Risposta**

Una risposta corretta restituisce la nuova connessione di base creata, incluso l&#39;identificatore di connessione univoco (`id`). Questo ID è necessario per esplorare la struttura file e il contenuto della tua sorgente nel passaggio successivo.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## Esplorare la sorgente {#explore}

Utilizzando l’ID di connessione di base generato nel passaggio precedente, puoi esplorare file e directory eseguendo richieste di GET. Quando si eseguono richieste di GET per esplorare la struttura e il contenuto del file di origine, è necessario includere i parametri di query elencati nella tabella seguente:

| Parametro | Descrizione |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | ID connessione di base generato nel passaggio precedente. |
| `{OBJECT_TYPE}` | Il tipo di oggetto da esplorare. Per le origini REST, il valore predefinito è `rest`. |
| `{OBJECT}` | Oggetto da esplorare. |
| `{FILE_TYPE}` | Questo parametro è necessario solo quando si visualizza una directory specifica. Il suo valore rappresenta il percorso della directory che desideri esplorare. |
| `{PREVIEW}` | Valore booleano che definisce se il contenuto della connessione supporta l’anteprima. |
| `{SOURCE_PARAMS}` | Una stringa codificata base64 del tuo `campaign_id`. |

>[!TIP]
>
>Per recuperare il tipo di formato accettato per `{SOURCE_PARAMS}`, devi codificare l’intero `campaignId` stringa in base64. Ad esempio: `{"campaignId": "c66a200cda"}` codificato in base64 equivale a `eyJjYW1wYWlnbklkIjoiYzY2YTIwMGNkYSJ9`.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&objectType={OBJECT_TYPE}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

**Richiesta**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/05c595e5-edc3-45c8-90bb-fcf556b57c4b/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJjYW1wYWlnbklkIjoiYzY2YTIwMGNkYSJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce la struttura del file interrogato.

```json
{
    "data": [
        {
            "emails": [
                {
                    "campaign_id": "c66a200cda",
                    "list_id": "10c097ca71",
                    "list_is_active": true,
                    "email_id": "cff65fb4c5f5828666ad846443720efd",
                    "email_address": "kendall2134@gmail.com",
                    "_links": [
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/CollectionResponse.json"
                        },
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/Response.json"
                        },
                        {
                            "rel": "member",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        }
                    ]
                },
                {
                    "campaign_id": "c66a200cda",
                    "list_id": "10c097ca71",
                    "list_is_active": true,
                    "email_id": "a16b82774b211afaf60902d1afd8abc5",
                    "email_address": "logan9935890967@gmail.com",
                    "_links": [
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/CollectionResponse.json"
                        },
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity/a16b82774b211afaf60902d1afd8abc5",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/Response.json"
                        },
                        {
                            "rel": "member",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/a16b82774b211afaf60902d1afd8abc5",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        }
                    ]
                },
            ]
        }
    ]    
}
```

## Creazione di una connessione sorgente {#source-connection}

È possibile creare una connessione sorgente effettuando una richiesta di POST al [!DNL Flow Service] API. Una connessione di origine è costituita da un ID connessione, un percorso del file di dati di origine e un ID della specifica di connessione.

Per creare una connessione di origine, è inoltre necessario definire un valore enum per l&#39;attributo del formato dati.

Utilizza i seguenti valori enum per le origini basate su file:

| Formato dati | Valore Enum |
| ----------- | ---------- |
| Delimitato | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Per tutte le origini basate su tabella, impostare il valore su `tabular`.

**Formato API**

```https
POST /sourceConnections
```

**Richiesta**

La richiesta seguente crea una connessione di origine per [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp source connection to ingest campaign ID",
      "description": "MailChimp Campaign source connection to ingest campaign ID",
      "baseConnectionId": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "campaignId": "c66a200cda"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della connessione di origine. Assicurati che il nome della connessione sorgente sia descrittivo, in quanto puoi utilizzarlo per cercare informazioni sulla connessione sorgente. |
| `description` | Un valore facoltativo che può essere incluso per fornire ulteriori informazioni sulla connessione sorgente. |
| `baseConnectionId` | ID connessione di base di [!DNL Mailchimp]. Questo ID è stato generato in un passaggio precedente. |
| `connectionSpec.id` | ID della specifica di connessione corrispondente alla tua origine. |
| `data.format` | Il formato del [!DNL Mailchimp] dati da acquisire. |
| `params.campaignId` | La [!DNL Mailchimp] l&#39;ID della campagna identifica un [!DNL Mailchimp] campaign, che ti consente di inviare e-mail ai tuoi elenchi/tipi di pubblico. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della nuova connessione sorgente creata. Questo ID è necessario in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "d6557bf1-7347-415f-964c-9316bd4cbf56",
    "etag": "\"e205c206-0000-0200-0000-615b5c070000\""
}
```

## Creare uno schema XDM di destinazione {#target-schema}

Affinché i dati di origine possano essere utilizzati in Platform, è necessario creare uno schema di destinazione per strutturare i dati di origine in base alle tue esigenze. Lo schema di destinazione viene quindi utilizzato per creare un set di dati di Platform in cui sono contenuti i dati di origine.

È possibile creare uno schema XDM di destinazione effettuando una richiesta POST al [API del Registro di sistema dello schema](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Per i passaggi dettagliati su come creare uno schema XDM di destinazione, consulta l’esercitazione su [creazione di uno schema tramite API](../../../../../xdm/api/schemas.md).

### Creare un set di dati di destinazione {#target-dataset}

È possibile creare un set di dati di destinazione eseguendo una richiesta di POST al [API del servizio catalogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), fornendo l’ID dello schema di destinazione all’interno del payload.

Per i passaggi dettagliati su come creare un set di dati di destinazione, consulta l’esercitazione su [creazione di un set di dati tramite API](../../../../../catalog/api/create-dataset.md).

## Creare una connessione di destinazione {#target-connection}

Una connessione di destinazione rappresenta la connessione alla destinazione in cui i dati acquisiti arrivano. Per creare una connessione di destinazione, è necessario fornire l’ID di specifica di connessione fissa corrispondente al [!DNL Data Lake]. Questo ID è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ora disponi degli identificatori univoci di uno schema di destinazione di un set di dati di destinazione e dell’ID della specifica di connessione di [!DNL Data Lake]. Utilizzando questi identificatori, puoi creare una connessione di destinazione utilizzando [!DNL Flow Service] API per specificare il set di dati che conterrà i dati di origine in entrata.

**Formato API**

```https
POST /targetConnections
```

**Richiesta**

La seguente richiesta crea una connessione di destinazione per [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp target connection",
      "description": "MailChimp Campaign target connection",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/570630b91eb9d5cf5db0436756abb110d02912917a67da2d",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6155e3a9bd13651949515f14"
      }
  }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Nome della connessione di destinazione. Assicurati che il nome della connessione di destinazione sia descrittivo, in quanto puoi utilizzarlo per cercare informazioni sulla connessione di destinazione. |
| `description` | Un valore facoltativo che può essere incluso per fornire ulteriori informazioni sulla connessione di destinazione. |
| `connectionSpec.id` | ID della specifica di connessione corrispondente a [!DNL Data Lake]. Questo ID fisso è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Il formato del [!DNL Mailchimp] i dati che desideri inserire in Platform. |
| `params.dataSetId` | ID del set di dati di destinazione recuperato in un passaggio precedente. |


**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco della nuova connessione di destinazione (`id`). Questo ID è necessario nei passaggi successivi.

```json
{
    "id": "9463fe9c-027d-4347-a423-894fcd105647",
    "etag": "\"b902e822-0000-0200-0000-615b5c370000\""
}
```

>[!IMPORTANT]
>
>Le funzioni di preparazione dei dati non sono attualmente supportate per [!DNL Mailchimp Campaign].

<!--
## Create a mapping {#mapping}

In order for the source data to be ingested into a target dataset, it must first be mapped to the target schema that the target dataset adheres to. This is achieved by performing a POST request to Conversion Service with data mappings defined within the request payload.

**API format**

```http
POST /conversion/mappingSets
```

**Request**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "_{TENANT_ID}.schemas.570630b91eb9d5cf5db0436756abb110d02912917a67da2d",
      "xdmVersion": "1.0",
      "mappings": [
      {
        "destinationXdmPath": "person.name.firstName",
        "sourceAttribute": "merge_fields.FNAME",
        "identity": false,
        "version": 0
      },
      {
        "destinationXdmPath": "person.name.lastName",
        "sourceAttribute": "merge_fields.LNAME",
        "identity": false,
        "version": 0
      }
    ]
  }'
```

| Property | Description |
| --- | --- |
| `xdmSchema` | The ID of the [target XDM schema](#target-schema) generated in an earlier step. |
| `mappings.destinationXdmPath` | The destination XDM path where the source attribute is being mapped to. |
| `mappings.sourceAttribute` | The source attribute that needs to be mapped to a destination XDM path. |
| `mappings.identity` | A boolean value that designates whether the mapping set will be marked for [!DNL Identity Service]. |

**Response**

A successful response returns details of the newly created mapping including its unique identifier (`id`). This value is required in a later step to create a dataflow.

```json
{
    "id": "5a365b23962d4653b9d9be25832ee5b4",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

--->

## Creare un flusso {#flow}

L&#39;ultimo passo verso [!DNL Mailchimp] In Platform viene creato un flusso di dati. A questo punto sono stati preparati i seguenti valori richiesti:

* [ID connessione di origine](#source-connection)
* [ID connessione di destinazione](#target-connection)

Un flusso di dati è responsabile della pianificazione e della raccolta dei dati da un’origine. È possibile creare un flusso di dati eseguendo una richiesta di POST fornendo al contempo i valori precedentemente menzionati all’interno del payload.

Per pianificare un’acquisizione, è innanzitutto necessario impostare il valore dell’ora di inizio in modo che l’ora di inizio sia espressa in secondi. Quindi, è necessario impostare il valore della frequenza su una delle cinque opzioni: `once`, `minute`, `hour`, `day`oppure `week`. Il valore dell’intervallo indica il periodo tra due acquisizioni consecutive e la creazione di un’acquisizione una tantum (`once`) non richiede l’impostazione di un intervallo. Per tutte le altre frequenze, il valore dell&#39;intervallo deve essere impostato su uguale o maggiore di `15`.


**Formato API**

```http
POST /flows
```

**Richiesta**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp Campaign dataflow",
      "description": "MailChimp Campaign dataflow",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "d6557bf1-7347-415f-964c-9316bd4cbf56"
      ],
      "targetConnectionIds": [
          "9463fe9c-027d-4347-a423-894fcd105647"
      ],
      "scheduleParams": {
          "startTime": "1632809759",
          "frequency": "minute",
          "interval": 15
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome del flusso di dati. Assicurati che il nome del flusso di dati sia descrittivo in quanto puoi utilizzarlo per cercare informazioni sul flusso di dati. |
| `description` | (Facoltativo) Proprietà che puoi includere per fornire ulteriori informazioni sul flusso di dati. |
| `flowSpec.id` | ID delle specifiche di flusso necessario per creare un flusso di dati. Questo ID fisso è: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | Versione corrispondente dell’ID della specifica di flusso. Questo valore predefinito è `1.0`. |
| `sourceConnectionIds` | La [ID connessione di origine](#source-connection) generato in un passaggio precedente. |
| `targetConnectionIds` | La [ID connessione di destinazione](#target-connection) generato in un passaggio precedente. |
| `scheduleParams.startTime` | Ora di inizio designata per l’inizio della prima acquisizione di dati. |
| `scheduleParams.frequency` | Frequenza con cui il flusso di dati raccoglie i dati. I valori accettabili includono: `once`, `minute`, `hour`, `day`oppure `week`. |
| `scheduleParams.interval` | L&#39;intervallo indica il periodo tra due esecuzioni di flusso consecutive. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero. L&#39;intervallo non è necessario quando la frequenza è impostata come `once` e deve essere maggiore o uguale a `15` per altri valori di frequenza. |

**Risposta**

Una risposta corretta restituisce l&#39;ID (`id`) del flusso di dati appena creato. Puoi utilizzare questo ID per monitorare, aggiornare o eliminare il flusso di dati.

```json
{
    "id": "be2d5249-eeaf-4a74-bdbd-b7bf62f7b2da",
    "etag": "\"7e010621-0000-0200-0000-615b5c9b0000\""
}
```

## Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni sulle esecuzioni del flusso, lo stato di completamento e gli errori.

**Formato API**

```http
GET /runs?property=flowId=={FLOW_ID}
```

**Richiesta**

La richiesta seguente recupera le specifiche per un flusso di dati esistente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli relativi all’esecuzione del flusso, incluse informazioni sulla data di creazione, sulle connessioni di origine e di destinazione, nonché l’identificatore univoco dell’esecuzione del flusso (`id`).

```json
{
    "items": [
        {
            "id": "209812ad-7bef-430c-b5b2-a648aae72094",
            "createdAt": 1633044829955,
            "updatedAt": 1633044838006,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "MailChimp Campaign dataflow",
            "description": "MailChimp Campaign dataflow",
            "flowSpec": {
                "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"7e01322c-0000-0200-0000-615b5d520000\"",
            "etag": "\"7e01322c-0000-0200-0000-615b5d520000\"",
            "sourceConnectionIds": [
                "d6557bf1-7347-415f-964c-9316bd4cbf56"
            ],
            "targetConnectionIds": [
                "9463fe9c-027d-4347-a423-894fcd105647"
            ],
            "inheritedAttributes": {
                "sourceConnections": [
                    {
                        "id": "d6557bf1-7347-415f-964c-9316bd4cbf56",
                        "connectionSpec": {
                            "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "9601747c-6874-4c02-bb00-5732a8c43086",
                            "connectionSpec": {
                                "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "9463fe9c-027d-4347-a423-894fcd105647",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "scheduleParams": {
                "startTime": "1633377385",
                "frequency": "minute",
                "interval": 15
            },
            "runs": "/flows/be2d5249-eeaf-4a74-bdbd-b7bf62f7b2da/runs",
            "lastOperation": {
                "started": 1633377421476,
                "updated": 0,
                "operation": "create"
            },
            "lastRunDetails": {
                "id": "84f95788-3e83-4ce0-8e45-c0a89117c6f1",
                "state": "failed",
                "startedAtUTC": 1633377445979,
                "completedAtUTC": 1633377487082
            }
        }
    ]
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `items` | Contiene un singolo payload di metadati associati all’esecuzione di flusso specifica. |
| `id` | Visualizza l&#39;ID corrispondente al flusso di dati. |
| `state` | Visualizza lo stato corrente del flusso di dati. |
| `inheritedAttributes` | Contiene gli attributi che definiscono il flusso, ad esempio gli ID per la connessione di base, sorgente e destinazione corrispondente. |
| `scheduleParams` | Contiene informazioni sulla pianificazione dell’acquisizione del flusso di dati, ad esempio l’ora di inizio (in epoch time), la frequenza e l’intervallo. |
| `transformations` | Contiene informazioni sulle proprietà di trasformazione applicate al flusso di dati. |
| `runs` | Visualizza l&#39;ID di esecuzione corrispondente del flusso. Puoi usare questo ID per monitorare esecuzioni di flussi specifiche. |

## Aggiornare il flusso di dati

Per aggiornare la pianificazione, il nome e la descrizione dell’esecuzione del flusso di dati, esegui una richiesta PATCH al [!DNL Flow Service] API fornendo al tempo stesso il tuo ID flusso, la versione e la nuova pianificazione che desideri utilizzare.

>[!IMPORTANT]
>
>La `If-Match` l’intestazione è necessaria quando si effettua una richiesta PATCH. Il valore di questa intestazione è la versione univoca della connessione che si desidera aggiornare.

**Formato API**

```http
PATCH /flows/{FLOW_ID}
```

**Richiesta**

La richiesta seguente aggiorna la pianificazione di esecuzione del flusso, nonché il nome e la descrizione del flusso di dati.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/209812ad-7bef-430c-b5b2-a648aae72094' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "2e01f11d-0000-0200-0000-615649660000"' \
  -d '[
          {
              "op": "replace",
              "path": "/scheduleParams/frequency",
              "value": "day"
          },
          {
              "op": "replace",
              "path": "/name",
              "value": "MailChimp Campaign Dataflow 2.0"
          },
          {
              "op": "replace",
              "path": "/description",
              "value": "MailChimp Campaign Dataflow Updated"
          }
      ]'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `op` | La chiamata dell’operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace`e `remove`. |
| `path` | Percorso del parametro da aggiornare. |
| `value` | Il nuovo valore con cui si desidera aggiornare il parametro. |

**Risposta**

Una risposta corretta restituisce il tuo ID flusso e un tag aggiornato. Puoi verificare l’aggiornamento effettuando una richiesta GET al [!DNL Flow Service] , fornendo al tempo stesso il tuo ID flusso.

```json
{
    "id": "209812ad-7bef-430c-b5b2-a648aae72094",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Elimina il flusso di dati

Con un ID flusso esistente, puoi eliminare un flusso di dati eseguendo una richiesta DELETE al [!DNL Flow Service] API.

**Formato API**

```http
DELETE /flows/{FLOW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FLOW_ID}` | L&#39;unico `id` del flusso di dati da eliminare. |

**Richiesta**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/flows/209812ad-7bef-430c-b5b2-a648aae72094' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto. Puoi confermare l’eliminazione tentando una richiesta di ricerca (GET) al flusso di dati. L’API restituirà un errore HTTP 404 (Non trovato) che indica che il flusso di dati è stato eliminato.

## Aggiorna la connessione

Per aggiornare il nome, la descrizione e le credenziali della tua connessione, esegui una richiesta PATCH al [!DNL Flow Service] API fornendo l&#39;ID di connessione di base, la versione e le nuove informazioni che si desidera utilizzare.

>[!IMPORTANT]
>
>La `If-Match` l’intestazione è necessaria quando si effettua una richiesta PATCH. Il valore di questa intestazione è la versione univoca della connessione che si desidera aggiornare.

**Formato API**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | L&#39;unico `id` valore della connessione che si desidera aggiornare. |

**Richiesta**

La richiesta seguente fornisce un nuovo nome e una nuova descrizione, nonché un nuovo set di credenziali, con cui aggiornare la connessione.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/connections/4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: 4000cff7-0000-0200-0000-6154bad60000' \
  -d '[
      {
          "op": "replace",
          "path": "/auth/params",
          "value": {
              "username": "mailchimp-member-activity-user",
              "password": "{NEW_PASSWORD}"
          }
      },
      {
          "op": "replace",
          "path": "/name",
          "value": "MailChimp Campaign Connection 2.0"
      },
      {
          "op": "add",
          "path": "/description",
          "value": "Updated MailChimp Campaign Connection"
      }
  ]'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `op` | Chiamata dell’operazione utilizzata per definire l’azione necessaria per aggiornare la connessione. Le operazioni includono: `add`, `replace`e `remove`. |
| `path` | Percorso del parametro da aggiornare. |
| `value` | Il nuovo valore con cui si desidera aggiornare il parametro. |

**Risposta**

Una risposta corretta restituisce l&#39;ID di connessione di base e un tag aggiornato. Puoi verificare l’aggiornamento effettuando una richiesta GET al [!DNL Flow Service] , fornendo al tempo stesso l&#39;ID di connessione.

```json
{
    "id": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Elimina la connessione

Una volta ottenuto l’ID di connessione di base esistente, esegui una richiesta DELETE al [!DNL Flow Service] API.

**Formato API**

```http
DELETE /connections/{CONNECTION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | L&#39;unico `id` valore della connessione di base che si desidera eliminare. |

**Richiesta**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/connections/4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto.

Puoi confermare l’eliminazione tentando una richiesta di ricerca (GET) alla connessione.
