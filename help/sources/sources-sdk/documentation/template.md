---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;sorgente connettori;sorgenti sdk;sdk;SDK
title: Modello self-service della documentazione
description: Scopri come collegare Adobe Experience Platform a YOURSOURCE utilizzando l’API del servizio Flusso.
exl-id: c6927a71-3721-461e-9752-8ebc0b7b1cca
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 2%

---

# Crea una connessione *YOURSOURCE* utilizzando l&#39;API [!DNL Flow Service]

*Sostituire o eliminare tutti i paragrafi in corsivo a partire da questo modello.*

*Per iniziare, aggiorna i metadati (titolo e descrizione) nella parte superiore della pagina. Ignora tutte le istanze di DNL in questa pagina. Questo tag aiuta i nostri processi di traduzione automatica a tradurre correttamente la pagina nelle diverse lingue supportate. Dopo l&#39;invio aggiungeremo i tag alla documentazione.*

## Panoramica

*Fornisci una breve panoramica della tua azienda, compreso il valore che offre ai clienti. Includi un collegamento alla home page della documentazione del prodotto per ulteriori informazioni.*

>[!IMPORTANT]
>
>Il connettore di origine e la pagina della documentazione vengono creati e gestiti dal team *YourSource*. Per eventuali richieste di informazioni o richieste di aggiornamento, è possibile contattarle direttamente all&#39;indirizzo *Inserire il collegamento o l&#39;indirizzo di posta elettronica a cui è possibile accedere per gli aggiornamenti*.

## Prerequisiti

*Aggiungere informazioni in questa sezione su qualsiasi elemento di cui i clienti devono essere a conoscenza prima di iniziare a configurare l&#39;origine nell&#39;interfaccia utente di Adobe Experience Platform. Informazioni su:*

* *da aggiungere a un elenco consentiti*
* *requisiti per l&#39;hashing delle e-mail*
* *qualsiasi specifica account sul tuo lato*
* *come ottenere una chiave API per connettersi alla piattaforma*

### Raccogli le credenziali richieste

Per connettere *YOURSOURCE* ad Experience Platform, è necessario fornire i valori per le proprietà di connessione seguenti:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| *credenziali uno* | *Aggiungere qui una breve descrizione alle credenziali di autenticazione dell&#39;origine* | *Aggiungi qui un esempio delle credenziali di autenticazione dell&#39;origine* |
| *credenziali due* | *Aggiungere qui una breve descrizione alle credenziali di autenticazione dell&#39;origine* | *Aggiungi qui un esempio delle credenziali di autenticazione dell&#39;origine* |
| *credenziali tre* | *Aggiungere qui una breve descrizione alle credenziali di autenticazione dell&#39;origine* | *Aggiungi qui un esempio delle credenziali di autenticazione dell&#39;origine* |

Per ulteriori informazioni su queste credenziali, vedere la documentazione relativa all&#39;autenticazione di *YOURSOURCE*. *Aggiungi qui il collegamento alla documentazione di autenticazione della tua piattaforma*.

## Connetti *YOURSOURCE* a Platform utilizzando l&#39;API [!DNL Flow Service]

Il seguente tutorial illustra i passaggi necessari per creare una connessione di origine *YOURSOURCE* e un flusso di dati per portare i dati *YOURSOURCE* in Platform utilizzando l&#39;API [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

### Creare una connessione di base {#base-connection}

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione *YOURSOURCE* come parte del corpo della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per *YOURSOURCE*:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} base connection",
        "description": "{YOURSOURCE} base connection to authenticate to Platform",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "auth": {
            "specName": "OAuth generic-rest-connector",
            "params": {
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}",
                "expirationDate": "{EXPIRATION_DATE}"
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
| `auth.params.` | Contiene le credenziali necessarie per autenticare l’origine. |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione di base appena creata, incluso il relativo identificatore univoco di connessione (`id`). Questo ID è necessario per esplorare la struttura e il contenuto del file sorgente nel passaggio successivo.

```json
{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
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
| `{OBJECT}` | Questo parametro è necessario solo quando si visualizza una directory specifica. Il relativo valore rappresenta il percorso della directory che desideri esplorare. |
| `fileType=json` | Il tipo di file che desideri portare su Platform. Attualmente, `json` è l&#39;unico tipo di file supportato. |
| `{PREVIEW}` | Valore booleano che definisce se il contenuto della connessione supporta l’anteprima. |
| `{SOURCE_PARAMS}` | Definisce i parametri per il file sorgente da portare a Platform. Per recuperare il formato accettato per `{SOURCE_PARAMS}`, è necessario codificare l&#39;intera stringa `list_id` in base64. Nell&#39;esempio seguente, `"list_id": "10c097ca71"` codificato in base64 equivale a `eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=`. |


**Richiesta**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/70383d02-2777-4be7-a309-9dd6eea1b46d/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=' \
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
      "members": [
        {
          "id": "cff65fb4c5f5828666ad846443720efd",
          "email_address": "roykent@gmail.com",
          "unique_email_id": "72c758cbf1",
          "full_name": "Roy Kent",
          "web_id": 547094062,
          "email_type": "html",
          "status": "subscribed",
          "merge_fields": {
            "FNAME": "Roy",
            "LNAME": "Kent",
            "ADDRESS": {
              "addr1": "",
              "addr2": "",
              "city": "Richmond",
              "state": "Virginia",
              "zip": "",
              "country": "US"
            },
            "PHONE": "",
            "BIRTHDAY": ""
          },
          "stats": {
            "avg_open_rate": 0,
            "avg_click_rate": 0
          },
          "ip_signup": "",
          "timestamp_signup": "",
          "ip_opt": "103.43.112.97",
          "timestamp_opt": "2021-06-01T15:31:36+00:00",
          "member_rating": 2,
          "last_changed": "2021-06-01T15:31:36+00:00",
          "language": "",
          "vip": false,
          "email_client": "",
          "location": {
            "latitude": 0,
            "longitude": 0,
            "gmtoff": 0,
            "dstoff": 0,
            "country_code": "",
            "timezone": ""
          },
          "source": "Admin Add",
          "tags_count": 0,
          "tags": [
             
          ],
          "list_id": "10c097ca71"
        }
      ],
      "list_id": "10c097ca71",
      "total_items": 2,
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
      ]
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

La richiesta seguente crea una connessione di origine per *YOURSOURCE*:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} Source Connection",
        "description": "{YOURSOURCE} Source Connection",
        "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "server": "us6",
            "listId": "10c097ca71"
        }
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della connessione di origine. Assicurati che il nome della connessione sorgente sia descrittivo, in quanto può essere utilizzato per cercare informazioni sulla connessione sorgente. |
| `description` | Valore facoltativo che è possibile includere per fornire ulteriori informazioni sulla connessione di origine. |
| `baseConnectionId` | ID connessione di base di *YOURSOURCE*. Questo ID è stato generato in un passaggio precedente. |
| `connectionSpec.id` | ID della specifica di connessione corrispondente all&#39;origine. |
| `data.format` | Formato dei dati *YOURSOURCE* che si desidera acquisire. Attualmente, l&#39;unico formato di dati supportato è `json`. |

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;identificatore univoco (`id`) della connessione di origine appena creata. Questo ID è necessario in un passaggio successivo per creare un flusso di dati.

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
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

Una connessione di destinazione rappresenta la connessione alla destinazione in cui devono essere memorizzati i dati acquisiti. Per creare una connessione di destinazione, è necessario fornire l&#39;ID della specifica di connessione fissa corrispondente a [!DNL Data Lake]. ID: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ora disponi degli identificatori univoci uno schema di destinazione un set di dati di destinazione e l&#39;ID della specifica di connessione a [!DNL Data Lake]. Utilizzando questi identificatori, è possibile creare una connessione di destinazione utilizzando l&#39;API [!DNL Flow Service] per specificare il set di dati che conterrà i dati di origine in entrata.

**Formato API**

```https
POST /targetConnections
```

**Richiesta**

La richiesta seguente crea una connessione di destinazione per *YOURSOURCE*:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} Target Connection",
        "description": "{YOURSOURCE} Target Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "dataSetId": "5ef4551c52e054191a61a99f"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Nome della connessione di destinazione. Assicurati che il nome della connessione di destinazione sia descrittivo, in quanto può essere utilizzato per cercare informazioni sulla connessione di destinazione. |
| `description` | Valore facoltativo che è possibile includere per fornire ulteriori informazioni sulla connessione di destinazione. |
| `connectionSpec.id` | ID della specifica di connessione corrispondente a [!DNL Data Lake]. ID corretto: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Formato dei dati *YOURSOURCE* che si desidera portare in Platform. |
| `params.dataSetId` | ID del set di dati di destinazione recuperato in un passaggio precedente. |


**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco della nuova connessione di destinazione (`id`). Questo ID è richiesto nei passaggi successivi.

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
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
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `xdmSchema` | ID dello schema XDM [target](#target-schema) generato in un passaggio precedente. |
| `mappings.destinationXdmPath` | Percorso XDM di destinazione in cui viene eseguito il mapping dell’attributo di origine. |
| `mappings.sourceAttribute` | L’attributo di origine che deve essere mappato su un percorso XDM di destinazione. |
| `mappings.identity` | Valore booleano che indica se il set di mappatura verrà contrassegnato per [!DNL Identity Service]. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della mappatura appena creata, incluso il relativo identificatore univoco (`id`). Questo valore è necessario in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Creare un flusso {#flow}

L&#39;ultimo passaggio per portare i dati da *YOURSOURCE* a Platform consiste nel creare un flusso di dati. A questo punto sono stati preparati i seguenti valori obbligatori:

* [ID connessione Source](#source-connection)
* [ID connessione di destinazione](#target-connection)
* [ID di mappatura](#mapping)

Un flusso di dati è responsabile della pianificazione e della raccolta di dati da un’origine. Puoi creare un flusso di dati eseguendo una richiesta POST e fornendo i valori precedentemente menzionati all’interno del payload.

Per pianificare un’acquisizione, devi prima impostare il valore dell’ora di inizio su tempo epoca in secondi. Impostare quindi il valore della frequenza su una delle cinque opzioni seguenti: `once`, `minute`, `hour`, `day` o `week`. Il valore di intervallo indica il periodo tra due acquisizioni consecutive, tuttavia, la creazione di un’acquisizione una tantum non richiede l’impostazione di un intervallo. Per tutte le altre frequenze, il valore dell&#39;intervallo deve essere impostato su uguale o maggiore di `15`.


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
        "name": "{YOURSOURCE} dataflow",
        "description": "{YOURSOURCE} dataflow",
        "flowSpec": {
            "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "246d052c-da4a-494a-937f-a0d17b1c6cf5"
        ],
        "targetConnectionIds": [
            "7c96c827-3ffd-460c-a573-e9558f72f263"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1625040887",
            "frequency": "minute",
            "interval": 15
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
| `scheduleParams.frequency` | La frequenza con cui il flusso di dati raccoglierà i dati. I valori accettabili includono: `once`, `minute`, `hour`, `day` o `week`. |
| `scheduleParams.interval` | L’intervallo indica il periodo tra due esecuzioni consecutive del flusso. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero. L&#39;intervallo non è necessario quando la frequenza è impostata come `once` e deve essere maggiore o uguale a `15` per gli altri valori di frequenza. |

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;ID (`id`) del flusso di dati appena creato. Puoi usare questo ID per monitorare, aggiornare o eliminare il flusso di dati.

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
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