---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;sorgente connettori;sorgenti sdk;sdk;SDK
solution: Experience Platform
title: Creare un flusso di dati per i membri Mailchimp tramite l’API del servizio Flusso
description: Scopri come connettere Adobe Experience Platform ai membri MailChimp utilizzando l’API del servizio Flusso.
exl-id: 900d4073-129c-47ba-b7df-5294d25a7219
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '2123'
ht-degree: 2%

---

# Creare un flusso di dati per [!DNL Mailchimp Members] utilizzo dell’API del servizio Flusso

Il seguente tutorial illustra i passaggi necessari per creare una connessione di origine e un flusso di dati da portare [!DNL Mailchimp Members] dati a Platform utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prerequisiti

Prima di connettersi [!DNL Mailchimp] a Adobe Experience Platform utilizzando il codice di aggiornamento OAuth 2, devi prima recuperare il token di accesso per [!DNL MailChimp.] Consulta la [[!DNL Mailchimp] Guida di OAuth 2](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/) per istruzioni dettagliate su come trovare il token di accesso.

## Creare una connessione di base {#base-connection}

Dopo aver recuperato [!DNL Mailchimp] credenziali di autenticazione, ora puoi avviare il processo di creazione del flusso di dati per portare [!DNL Mailchimp Members] su Platform. Il primo passaggio nella creazione di un flusso di dati consiste nel creare una connessione di base.

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

[!DNL Mailchimp] supporta sia l’autenticazione di base che il codice di aggiornamento OAuth 2. Per istruzioni su come eseguire l’autenticazione con uno dei tipi di autenticazione, consulta gli esempi seguenti.

### Creare un [!DNL Mailchimp] connessione di base tramite autenticazione di base

Per creare un [!DNL Mailchimp] connessione di base tramite autenticazione di base, invia una richiesta POST al `/connections` endpoint di [!DNL Flow Service] fornendo al contempo le credenziali per il `authorizationTestUrl`, `username`, e `password`.

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
      "description": "Mailchimp Members base connection with basic authentication",
      "connectionSpec": {
          "id": "2e8580db-6489-4726-96de-e33f5f60295f",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della connessione di base. Verificare che il nome della connessione di base sia descrittivo, in quanto è possibile utilizzarlo per cercare informazioni sulla connessione di base. |
| `description` | (Facoltativo) Proprietà che è possibile includere per fornire ulteriori informazioni sulla connessione di base. |
| `connectionSpec.id` | ID della specifica di connessione dell&#39;origine. Questo ID può essere recuperato dopo che l&#39;origine è stata registrata e approvata tramite [!DNL Flow Service] API. |
| `auth.specName` | Tipo di autenticazione utilizzato per connettere l’origine a Platform. |
| `auth.params.authorizationTestUrl` | (Facoltativo) L’URL del test di autorizzazione viene utilizzato per convalidare le credenziali durante la creazione di una connessione di base. Se non vengono fornite, le credenziali vengono controllate automaticamente durante il passaggio di creazione della connessione di origine. |
| `auth.params.username` | Il nome utente che corrisponde al [!DNL Mailchimp] account. Questa opzione è necessaria per l’autenticazione di base. |
| `auth.params.password` | La password che corrisponde al tuo [!DNL Mailchimp] account. Questa opzione è necessaria per l’autenticazione di base. |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione di base appena creata, incluso il relativo identificatore univoco di connessione (`id`). Questo ID è necessario per esplorare la struttura e il contenuto del file sorgente nel passaggio successivo.

```json
{
    "id": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
    "etag": "\"4000cff7-0000-0200-0000-6154bad60000\""
}
```

### Creare un [!DNL Mailchimp] connessione di base tramite codice di aggiornamento OAuth 2

Per creare un [!DNL Mailchimp] connessione di base utilizzando il codice di aggiornamento OAuth 2, invia una richiesta POST al `/connections` mentre si forniscono le credenziali per il proprio `authorizationTestUrl`, e `accessToken`.

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
      "name": "MailChimp base connection with OAuth 2 refresh code",
      "description": "MailChimp Members base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "2e8580db-6489-4726-96de-e33f5f60295f",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della connessione di base. Verificare che il nome della connessione di base sia descrittivo, in quanto è possibile utilizzarlo per cercare informazioni sulla connessione di base. |
| `description` | (Facoltativo) Proprietà che è possibile includere per fornire ulteriori informazioni sulla connessione di base. |
| `connectionSpec.id` | ID della specifica di connessione dell&#39;origine. Questo ID può essere recuperato dopo la registrazione della sorgente tramite [!DNL Flow Service] API. |
| `auth.specName` | Tipo di autenticazione utilizzato per autenticare l’origine in Platform. |
| `auth.params.authorizationTestUrl` | (Facoltativo) L’URL del test di autorizzazione viene utilizzato per convalidare le credenziali durante la creazione di una connessione di base. Se non vengono fornite, le credenziali vengono controllate automaticamente durante il passaggio di creazione della connessione di origine. |
| `auth.params.accessToken` | Il token di accesso corrispondente utilizzato per autenticare l’origine. Questo è richiesto per l’autenticazione basata su OAuth. |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione di base appena creata, incluso il relativo identificatore univoco di connessione (`id`). Questo ID è necessario per esplorare la struttura e il contenuto del file sorgente nel passaggio successivo.

```json
{
    "id": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
    "etag": "\"4000cff7-0000-0200-0000-6154bad60000\""
}
```

## Esplora l’origine {#explore}

Utilizzando l’ID connessione di base generato nel passaggio precedente, puoi esplorare file e directory eseguendo richieste GET.

>[!TIP]
>
>Per recuperare il formato accettato per `{SOURCE_PARAMS}`, è necessario codificare l&#39;intero `list_id` stringa in base64. Ad esempio: `"list_id": "10c097ca71"` codificato in base64 equivale a `eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=`.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

Quando si eseguono richieste di GET per esplorare la struttura e il contenuto dei file dell’origine, è necessario includere i parametri di query elencati nella tabella seguente:

| Parametro | Descrizione |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | ID della connessione di base generato nel passaggio precedente. |
| `{OBJECT_TYPE}` | Il tipo di oggetto che desideri esplorare. Per le origini REST, il valore predefinito è `rest`. |
| `{OBJECT}` | L’oggetto che desideri esplorare. |
| `{FILE_TYPE}` | Questo parametro è necessario solo quando si visualizza una directory specifica. Il relativo valore rappresenta il percorso della directory che desideri esplorare. |
| `{PREVIEW}` | Valore booleano che definisce se il contenuto della connessione supporta l’anteprima. |
| `{SOURCE_PARAMS}` | Una stringa con codifica base64 del file `list_id`. |

**Richiesta**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/05c595e5-edc3-45c8-90bb-fcf556b57c4b/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce la struttura del file su cui è stata eseguita la query.

```json
{ 
"data": [
    {
        "list_id": "10c097ca71",
        "_links": [
            {
                "rel": "self",
                "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
                "method": "GET",
                "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/CollectionResponse.json",
                "schema": "https://us6.api.mailchimp.com/schema/3.0/Paths/Lists/Members/Collection.json"
            },
            {
                "rel": "parent",
                "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71",
                "method": "GET",
                "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
            },
            {
                "rel": "create",
                "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
                "method": "POST",
                "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
                "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/POST.json"
            }
        ],
        "members": [
            {
                "id": "cff65fb4c5f5828666ad846443720efd",
                "email_address": "kendallt2134@gmail.com",
                "unique_email_id": "72c758cbf1",
                "contact_id": "874a0d6e9ddb89d8b4a31e416ead2d6f",
                "full_name": "Kendall Roy",
                "web_id": 547094062,
                "email_type": "html",
                "status": "subscribed",
                "consents_to_one_to_one_messaging": true,
                "merge_fields": {
                    "FNAME": "Kendall",
                    "LNAME": "Roy",
                    "ADDRESS": {
                        "country": "US"
                    }
                },
                "stats": {
                    "avg_open_rate": 0,
                    "avg_click_rate": 0
                },
                "ip_opt": "103.43.112.97",
                "timestamp_opt": "2021-06-01T15:31:36+00:00",
                "member_rating": 2,
                "last_changed": "2021-06-01T15:31:36+00:00",
                "vip": false,
                "location": {
                    "latitude": 0,
                    "longitude": 0,
                    "gmtoff": 0,
                    "dstoff": 0
                },
                "source": "Admin Add",
                "tags_count": 0,
                "list_id": "10c097ca71",
                "_links": [
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        },
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/CollectionResponse.json",
                            "schema": "https://us6.api.mailchimp.com/schema/3.0/Paths/Lists/Members/Collection.json"
                        },
                        {
                            "rel": "update",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "PATCH",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
                            "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/PATCH.json"
                        },
                        {
                            "rel": "upsert",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "PUT",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
                            "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/PUT.json"
                        },
                        {
                            "rel": "delete",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "DELETE"
                        },
                        {
                            "rel": "activity",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Activity/Response.json"
                        },
                        {
                            "rel": "goals",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/goals",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Goals/Response.json"
                        },
                        {
                            "rel": "notes",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/notes",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Notes/CollectionResponse.json"
                        },
                        {
                            "rel": "events",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/events",
                            "method": "POST",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Events/POST.json"
                        },
                        {
                            "rel": "delete_permanent",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/actions/delete-permanent",
                            "method": "POST"
                        }
                    ]
                }
            ]  
        }
    ]
}
```

## Creare una connessione sorgente {#source-connection}

Puoi creare una connessione sorgente effettuando una richiesta POST al [!DNL Flow Service] API. Una connessione di origine è costituita da un ID di connessione, un percorso del file di dati di origine e un ID della specifica di connessione.

Per creare una connessione di origine, è inoltre necessario definire un valore enum per l&#39;attributo formato dati.

Utilizzare i seguenti valori enum per le origini basate su file:

| Formato dati | Valore enum |
| ----------- | ---------- |
| Delimitato | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Per tutte le origini basate su tabelle, imposta il valore su `tabular`.

**Formato API**

```https
POST /sourceConnections
```

**Richiesta**

La richiesta seguente crea una connessione sorgente per [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp source connection to ingest listId",
      "description": "MailChimp Members source connection to ingest listId",
      "baseConnectionId": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
      "connectionSpec": {
          "id": "2e8580db-6489-4726-96de-e33f5f60295f",
          "version": "1.0"
      },
      "data": {
          "format": "json",
      },
      "params": {
          "listId": "10c097ca71"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della connessione di origine. Assicurati che il nome della connessione sorgente sia descrittivo, in quanto può essere utilizzato per cercare informazioni sulla connessione sorgente. |
| `description` | (Facoltativo) Proprietà che è possibile includere per fornire ulteriori informazioni sulla connessione di origine. |
| `baseConnectionId` | ID connessione di base di [!DNL Mailchimp]. Questo ID è stato generato in un passaggio precedente. |
| `connectionSpec.id` | ID della specifica di connessione corrispondente all&#39;origine. |
| `data.format` | Il formato del [!DNL Mailchimp] i dati che desideri acquisire. |
| `params.listId` | Anche noto come ID pubblico, il [!DNL Mailchimp] l’ID elenco consente il trasferimento dei dati sul pubblico ad altre integrazioni. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’identificatore univoco (`id`) della connessione sorgente appena creata. Questo ID è necessario in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "a51e4cf6-65ef-45f4-b4bf-4f03da5f01cc",
    "etag": "\"6b02b65d-0000-0200-0000-6154bfbe0000\""
}
```

## Creare uno schema XDM di destinazione {#target-schema}

Per utilizzare i dati sorgente in Platform, è necessario creare uno schema di destinazione che strutturi i dati sorgente in base alle tue esigenze. Lo schema di destinazione viene quindi utilizzato per creare un set di dati di Platform in cui sono contenuti i dati di origine.

È possibile creare uno schema XDM di destinazione eseguendo una richiesta POST al [API del registro dello schema](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Per i passaggi dettagliati su come creare uno schema XDM di destinazione, consulta l’esercitazione su [creazione di uno schema tramite l’API](../../../../../xdm/api/schemas.md).

### Creare un set di dati di destinazione {#target-dataset}

È possibile creare un set di dati di destinazione eseguendo una richiesta POST al [API Catalog Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), che fornisce l’ID dello schema di destinazione all’interno del payload.

Per i passaggi dettagliati su come creare un set di dati di destinazione, consulta l’esercitazione su [creazione di un set di dati tramite l’API](../../../../../catalog/api/create-dataset.md).

## Creare una connessione di destinazione {#target-connection}

Una connessione di destinazione rappresenta la connessione alla destinazione in cui arrivano i dati acquisiti. Per creare una connessione di destinazione, devi fornire l&#39;ID di specifica della connessione fissa che corrisponde al [!DNL Data Lake]. Questo ID è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ora disponi degli identificatori univoci, di uno schema di destinazione, di un set di dati di destinazione e dell’ID della specifica di connessione al [!DNL Data Lake]. Utilizzando questi identificatori, puoi creare una connessione di destinazione utilizzando [!DNL Flow Service] API per specificare il set di dati che conterrà i dati di origine in entrata.

**Formato API**

```https
POST /targetConnections
```

**Richiesta**

La richiesta seguente crea una connessione di destinazione per [!DNL Mailchimp]:

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
      "description": "MailChimp Members target connection",
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
| `name` | Nome della connessione di destinazione. Assicurati che il nome della connessione di destinazione sia descrittivo, in quanto può essere utilizzato per cercare informazioni sulla connessione di destinazione. |
| `description` | (Facoltativo) Proprietà che puoi includere per fornire ulteriori informazioni sulla connessione di destinazione. |
| `connectionSpec.id` | ID della specifica di connessione che corrisponde a [!DNL Data Lake]. Questo ID fisso è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Il formato del [!DNL Mailchimp] dati da inserire in Platform. |
| `params.dataSetId` | ID del set di dati di destinazione recuperato in un passaggio precedente. |


**Risposta**

In caso di esito positivo, la risposta restituisce l’identificatore univoco della nuova connessione di destinazione (`id`). Questo ID è richiesto nei passaggi successivi.

```json
{
    "id": "8db5fb4a-6ce8-4370-afc0-1765e39535a5",
    "etag": "\"960093ce-0000-0200-0000-6154da3e0000\""
}
```

## Creare una mappatura {#mapping}

Per poter acquisire i dati di origine in un set di dati di destinazione, è necessario prima mapparli sullo schema di destinazione a cui il set di dati di destinazione aderisce. Ciò si ottiene eseguendo una richiesta POST al [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) con mappature di dati definite nel payload della richiesta.

**Formato API**

```http
POST /conversion/mappingSets
```

**Richiesta**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
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

| Proprietà | Descrizione |
| --- | --- |
| `xdmSchema` | ID del [schema XDM di destinazione](#target-schema) generato in un passaggio precedente. |
| `mappings.destinationXdmPath` | Percorso XDM di destinazione in cui viene eseguito il mapping dell’attributo di origine. |
| `mappings.sourceAttribute` | L’attributo di origine che deve essere mappato su un percorso XDM di destinazione. |
| `mappings.identity` | Valore booleano che indica se il set di mappatura verrà contrassegnato per [!DNL Identity Service]. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della mappatura appena creata, compreso l’identificatore univoco (`id`). Questo valore è necessario in un passaggio successivo per creare un flusso di dati.

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

## Creare un flusso {#flow}

L&#39;ultimo passo verso la [!DNL Mailchimp] I dati da a Platform consistono nel creare un flusso di dati. A questo punto sono stati preparati i seguenti valori obbligatori:

* [ID connessione sorgente](#source-connection)
* [ID connessione di destinazione](#target-connection)
* [ID mappatura](#mapping)

Un flusso di dati è responsabile della pianificazione e della raccolta di dati da un’origine. Puoi creare un flusso di dati eseguendo una richiesta POST e fornendo i valori precedentemente menzionati all’interno del payload.

Per pianificare un’acquisizione, devi prima impostare il valore dell’ora di inizio su tempo epoca in secondi. Quindi, è necessario impostare il valore della frequenza su una delle cinque opzioni seguenti: `once`, `minute`, `hour`, `day`, o `week`. Il valore di intervallo indica il periodo tra due acquisizioni consecutive e la creazione di un’acquisizione una tantum non richiede l’impostazione di un intervallo. Per tutte le altre frequenze, il valore dell&#39;intervallo deve essere impostato su uguale o maggiore di `15`.


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
      "name": "MailChimp Members dataflow",
      "description": "MailChimp Members dataflow",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "a51e4cf6-65ef-45f4-b4bf-4f03da5f01cc"
      ],
      "targetConnectionIds": [
          "8db5fb4a-6ce8-4370-afc0-1765e39535a5"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "5a365b23962d4653b9d9be25832ee5b4",
                  "mappingVersion": 0
              }
          }
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
| `name` | Nome del flusso di dati. Assicurati che il nome del flusso di dati sia descrittivo, in quanto può essere utilizzato per cercare informazioni sul flusso di dati. |
| `description` | (Facoltativo) Una proprietà che puoi includere per fornire ulteriori informazioni sul flusso di dati. |
| `flowSpec.id` | ID della specifica di flusso necessario per creare un flusso di dati. Questo ID fisso è: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | Versione corrispondente dell&#39;ID della specifica di flusso. Questo valore viene impostato automaticamente su `1.0`. |
| `sourceConnectionIds` | Il [ID connessione sorgente](#source-connection) generato in un passaggio precedente. |
| `targetConnectionIds` | Il [ID connessione di destinazione](#target-connection) generato in un passaggio precedente. |
| `transformations` | Questa proprietà contiene le varie trasformazioni che devono essere applicate ai dati. Questa proprietà è necessaria per portare dati non conformi a XDM su Platform. |
| `transformations.name` | Nome assegnato alla trasformazione. |
| `transformations.params.mappingId` | Il [ID mappatura](#mapping) generato in un passaggio precedente. |
| `transformations.params.mappingVersion` | Versione corrispondente dell&#39;ID di mappatura. Questo valore viene impostato automaticamente su `0`. |
| `scheduleParams.startTime` | L’ora di inizio designata per l’inizio della prima acquisizione dei dati. |
| `scheduleParams.frequency` | La frequenza con cui il flusso di dati raccoglierà i dati. I valori accettabili includono: `once`, `minute`, `hour`, `day`, o `week`. |
| `scheduleParams.interval` | L’intervallo indica il periodo tra due esecuzioni consecutive del flusso. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero. Intervallo non richiesto quando la frequenza è impostata come `once` e deve essere maggiore o uguale a `15` per altri valori di frequenza. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID (`id`) del flusso di dati appena creato. Puoi usare questo ID per monitorare, aggiornare o eliminare il flusso di dati.

```json
{
    "id": "209812ad-7bef-430c-b5b2-a648aae72094",
    "etag": "\"2e01f11d-0000-0200-0000-615649660000\""
}
```

## Appendice

La sezione seguente fornisce informazioni sui passaggi possibili per monitorare, aggiornare ed eliminare il flusso di dati.

### Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni sulle esecuzioni del flusso, sullo stato di completamento e sugli errori. Per esempi API completi, consulta la guida su [monitoraggio dei flussi di dati di origine tramite l’API](../../monitor.md).

### Aggiornare il flusso di dati

Aggiorna i dettagli del flusso di dati, ad esempio il nome e la descrizione, nonché la pianificazione di esecuzione e i set di mappatura associati, effettuando una richiesta PATCH al `/flows` endpoint di [!DNL Flow Service] e fornire l’ID del flusso di dati. Quando effettui una richiesta PATCH, devi fornire il codice univoco del flusso di dati `etag` nel `If-Match` intestazione. Per esempi API completi, consulta la guida su [aggiornamento dei flussi di dati di origine tramite l’API](../../update-dataflows.md).

### Aggiornare l’account

Aggiorna il nome, la descrizione e le credenziali dell’account di origine eseguendo una richiesta PATCH al [!DNL Flow Service] fornendo l’ID connessione di base come parametro di query. Quando effettui una richiesta PATCH, devi fornire il codice univoco dell’account sorgente `etag` nel `If-Match` intestazione. Per esempi API completi, consulta la guida su [aggiornamento dell’account sorgente tramite l’API](../../update.md).

### Eliminare il flusso di dati

Elimina il flusso di dati eseguendo una richiesta DELETE al [!DNL Flow Service] fornendo l’ID del flusso di dati che desideri eliminare come parte del parametro di query. Per esempi API completi, consulta la guida su [eliminazione dei flussi di dati tramite API](../../delete-dataflows.md).

### Elimina l’account

Elimina l’account eseguendo una richiesta DELETE al [!DNL Flow Service] fornendo l’ID della connessione di base dell’account da eliminare. Per esempi API completi, consulta la guida su [eliminazione dell’account sorgente tramite l’API](../../delete.md).