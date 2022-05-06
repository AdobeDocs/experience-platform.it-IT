---
keywords: Experience Platform;home;argomenti popolari;sorgenti;connettori;connettori sorgente;origini sdk;sdk;SDK
solution: Experience Platform
title: Modello self-service della documentazione
topic-legacy: tutorial
description: Scopri come collegare Adobe Experience Platform a YOURSOURCE utilizzando l’API del servizio di flusso.
hide: true
hidefromtoc: true
exl-id: c6927a71-3721-461e-9752-8ebc0b7b1cca
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '2296'
ht-degree: 3%

---

# Crea un *GIOVANE* connessione tramite l’API del servizio di flusso

*Passando al modello, sostituisci o elimina tutti i paragrafi in corsivo (a partire da questo).*

*Per iniziare, aggiorna i metadati (titolo e descrizione) nella parte superiore della pagina. Ignora tutte le istanze di DNL in questa pagina. Questo è un tag che aiuta i nostri processi di traduzione automatica a tradurre correttamente la pagina nelle diverse lingue supportate. Dopo l’invio verranno aggiunti dei tag alla documentazione.*

## Panoramica

*Fornisci una breve panoramica della tua azienda, compreso il valore che fornisce ai clienti. Includi un collegamento alla pagina principale della documentazione del prodotto per ulteriori informazioni.*

>[!IMPORTANT]
>
>Questa pagina della documentazione è stata creata da *GIOVANE* squadra. Per qualsiasi richiesta di informazioni o di aggiornamento, contattali direttamente all&#39;indirizzo *Inserire un collegamento o un indirizzo e-mail dove è possibile ottenere gli aggiornamenti*.

## Prerequisiti

*Aggiungi in questa sezione informazioni su qualsiasi cosa i clienti devono sapere prima di iniziare a configurare l’origine nell’interfaccia utente di Adobe Experience Platform. Può trattarsi di:*

* *aggiunta a un elenco consentiti*
* *requisiti per l’hash delle e-mail*
* *tutte le specifiche dell&#39;account sul tuo lato*
* *come ottenere una chiave API per connettersi alla piattaforma*

## Connetti *GIOVANE* su Platform utilizzando [!DNL Flow Service] API

L’esercitazione seguente illustra i passaggi necessari per creare un *GIOVANE* connessione di origine e creazione di un flusso di dati per portare *GIOVANE* dati a Platform tramite [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

### Creare una connessione di base {#base-connection}

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del *GIOVANE* credenziali di autenticazione come parte del corpo della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per *GIOVANE*:

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
| `name` | Nome della connessione di base. Assicurati che il nome della connessione di base sia descrittivo, in quanto puoi utilizzarlo per cercare informazioni sulla connessione di base. |
| `description` | Un valore facoltativo che può essere incluso per fornire ulteriori informazioni sulla connessione di base. |
| `connectionSpec.id` | ID della specifica di connessione dell&#39;origine. Questo ID può essere recuperato dopo la registrazione e l&#39;approvazione della sorgente tramite [!DNL Flow Service] API. |
| `auth.specName` | Il tipo di autenticazione utilizzato per autenticare l’origine in Platform. |
| `auth.params.` | Contiene le credenziali necessarie per autenticare l&#39;origine. |

**Risposta**

Una risposta corretta restituisce la nuova connessione di base creata, incluso l&#39;identificatore di connessione univoco (`id`). Questo ID è necessario per esplorare la struttura file e il contenuto della tua sorgente nel passaggio successivo.

```json
{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

### Esplorare la sorgente {#explore}

Utilizzando l’ID di connessione di base generato nel passaggio precedente, puoi esplorare file e directory eseguendo richieste di GET.
Utilizza le seguenti chiamate per trovare il percorso del file in cui desideri inserire [!DNL Platform]:

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

Quando si eseguono richieste di GET per esplorare la struttura e il contenuto del file di origine, è necessario includere i parametri di query elencati nella tabella seguente:


| Parametro | Descrizione |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | ID connessione di base generato nel passaggio precedente. |
| `objectType=rest` | Tipo di oggetto da esplorare. Attualmente, questo valore è sempre impostato su `rest`. |
| `{OBJECT}` | Questo parametro è necessario solo quando si visualizza una directory specifica. Il suo valore rappresenta il percorso della directory che desideri esplorare. |
| `fileType=json` | Il tipo di file da portare in Platform. Attualmente, `json` è l&#39;unico tipo di file supportato. |
| `{PREVIEW}` | Valore booleano che definisce se il contenuto della connessione supporta l’anteprima. |
| `{SOURCE_PARAMS}` | Definisce i parametri del file di origine che si desidera portare in Platform. Per recuperare il tipo di formato accettato per `{SOURCE_PARAMS}`, devi codificare l’intero `list_id` stringa in base64. Nell’esempio seguente: `"list_id": "10c097ca71"` codificato in base64 equivale a `eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=`. |


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

Una risposta corretta restituisce la struttura del file interrogato.

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

### Creazione di una connessione sorgente {#source-connection}

È possibile creare una connessione sorgente effettuando una richiesta di POST al [!DNL Flow Service] API. Una connessione di origine è costituita da un ID connessione, un percorso del file di dati di origine e un ID della specifica di connessione.

**Formato API**

```https
POST /sourceConnections
```

**Richiesta**

La richiesta seguente crea una connessione di origine per *GIOVANE*:

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
| `name` | Nome della connessione di origine. Assicurati che il nome della connessione sorgente sia descrittivo, in quanto puoi utilizzarlo per cercare informazioni sulla connessione sorgente. |
| `description` | Un valore facoltativo che può essere incluso per fornire ulteriori informazioni sulla connessione sorgente. |
| `baseConnectionId` | ID connessione di base di *GIOVANE*. Questo ID è stato generato in un passaggio precedente. |
| `connectionSpec.id` | ID della specifica di connessione corrispondente alla tua origine. |
| `data.format` | Il formato del *GIOVANE* dati da acquisire. Attualmente, l’unico formato di dati supportato è `json`. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della nuova connessione sorgente creata. Questo ID è necessario in un passaggio successivo per creare un flusso di dati.

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

### Creare uno schema XDM di destinazione {#target-schema}

Affinché i dati di origine possano essere utilizzati in Platform, è necessario creare uno schema di destinazione per strutturare i dati di origine in base alle tue esigenze. Lo schema di destinazione viene quindi utilizzato per creare un set di dati di Platform in cui sono contenuti i dati di origine.

È possibile creare uno schema XDM di destinazione effettuando una richiesta POST al [API del Registro di sistema dello schema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Per i passaggi dettagliati su come creare uno schema XDM di destinazione, consulta l’esercitazione su [creazione di uno schema tramite API](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=en#create).

### Creare un set di dati di destinazione {#target-dataset}

È possibile creare un set di dati di destinazione eseguendo una richiesta di POST al [API del servizio catalogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), fornendo l’ID dello schema di destinazione all’interno del payload.

Per i passaggi dettagliati su come creare un set di dati di destinazione, consulta l’esercitazione su [creazione di un set di dati tramite API](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html?lang=en).

### Creare una connessione di destinazione {#target-connection}

Una connessione di destinazione rappresenta la connessione alla destinazione in cui devono essere memorizzati i dati acquisiti. Per creare una connessione di destinazione, è necessario fornire l’ID di specifica di connessione fissa corrispondente al [!DNL Data Lake]. Questo ID è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ora disponi degli identificatori univoci di uno schema di destinazione di un set di dati di destinazione e dell’ID della specifica di connessione di [!DNL Data Lake]. Utilizzando questi identificatori, puoi creare una connessione di destinazione utilizzando [!DNL Flow Service] API per specificare il set di dati che conterrà i dati di origine in entrata.

**Formato API**

```https
POST /targetConnections
```

**Richiesta**

La seguente richiesta crea una connessione di destinazione per *GIOVANE*:

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
| `name` | Nome della connessione di destinazione. Assicurati che il nome della connessione di destinazione sia descrittivo, in quanto puoi utilizzarlo per cercare informazioni sulla connessione di destinazione. |
| `description` | Un valore facoltativo che può essere incluso per fornire ulteriori informazioni sulla connessione di destinazione. |
| `connectionSpec.id` | ID della specifica di connessione corrispondente a [!DNL Data Lake]. Questo ID fisso è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Il formato del *GIOVANE* i dati che desideri inserire in Platform. |
| `params.dataSetId` | ID del set di dati di destinazione recuperato in un passaggio precedente. |


**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco della nuova connessione di destinazione (`id`). Questo ID è necessario nei passaggi successivi.

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### Creare una mappatura {#mapping}

Affinché i dati di origine possano essere acquisiti in un set di dati di destinazione, devono prima essere mappati sullo schema di destinazione a cui aderisce il set di dati di destinazione. A tal fine, esegui una richiesta POST a [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) con mappature dati definite all’interno del payload della richiesta.

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
| `xdmSchema` | ID del [schema XDM di destinazione](#target-schema) generato in un passaggio precedente. |
| `mappings.destinationXdmPath` | Percorso XDM di destinazione in cui viene eseguito il mapping dell&#39;attributo di origine. |
| `mappings.sourceAttribute` | L&#39;attributo di origine che deve essere mappato su un percorso XDM di destinazione. |
| `mappings.identity` | Un valore booleano che indica se il set di mappatura verrà contrassegnato per [!DNL Identity Service]. |

**Risposta**

Una risposta corretta restituisce i dettagli della mappatura appena creata, incluso il relativo identificatore univoco (`id`). Questo valore è necessario in un passaggio successivo per creare un flusso di dati.

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

Ultimo passo verso l&#39;inserimento dei dati *GIOVANE* su Platform viene creato un flusso di dati. A questo punto sono stati preparati i seguenti valori richiesti:

* [ID connessione di origine](#source-connection)
* [ID connessione di destinazione](#target-connection)
* [ID mappatura](#mapping)

Un flusso di dati è responsabile della pianificazione e della raccolta dei dati da un’origine. È possibile creare un flusso di dati eseguendo una richiesta di POST fornendo al contempo i valori precedentemente menzionati all’interno del payload.

Per pianificare un’acquisizione, è innanzitutto necessario impostare il valore dell’ora di inizio in modo che l’ora di inizio sia espressa in secondi. Quindi, è necessario impostare il valore della frequenza su una delle cinque opzioni: `once`, `minute`, `hour`, `day`oppure `week`. Il valore dell’intervallo indica il periodo tra due acquisizioni consecutive, tuttavia la creazione di un’acquisizione una tantum non richiede l’impostazione di un intervallo. Per tutte le altre frequenze, il valore dell&#39;intervallo deve essere impostato su uguale o maggiore di `15`.


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
| `name` | Nome del flusso di dati. Assicurati che il nome del flusso di dati sia descrittivo in quanto puoi utilizzarlo per cercare informazioni sul flusso di dati. |
| `description` | Un valore facoltativo che può essere incluso per fornire ulteriori informazioni sul flusso di dati. |
| `flowSpec.id` | ID delle specifiche di flusso necessario per creare un flusso di dati. Questo ID fisso è: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | Versione corrispondente dell’ID della specifica di flusso. Questo valore predefinito è `1.0`. |
| `sourceConnectionIds` | La [ID connessione di origine](#source-connection) generato in un passaggio precedente. |
| `targetConnectionIds` | La [ID connessione di destinazione](#target-connection) generato in un passaggio precedente. |
| `transformations` | Questa proprietà contiene le varie trasformazioni necessarie per essere applicate ai dati. Questa proprietà è necessaria per portare dati non conformi a XDM su Platform. |
| `transformations.name` | Nome assegnato alla trasformazione. |
| `transformations.params.mappingId` | La [ID mappatura](#mapping) generato in un passaggio precedente. |
| `transformations.params.mappingVersion` | Versione corrispondente dell&#39;ID di mappatura. Questo valore predefinito è `0`. |
| `scheduleParams.startTime` | Questa proprietà contiene informazioni sulla pianificazione dell’acquisizione del flusso di dati. |
| `scheduleParams.frequency` | Frequenza con cui il flusso di dati raccoglie i dati. I valori accettabili includono: `once`, `minute`, `hour`, `day`oppure `week`. |
| `scheduleParams.interval` | L&#39;intervallo indica il periodo tra due esecuzioni di flusso consecutive. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero. L&#39;intervallo non è necessario quando la frequenza è impostata come `once` e deve essere maggiore o uguale a `15` per altri valori di frequenza. |

**Risposta**

Una risposta corretta restituisce l&#39;ID (`id`) del flusso di dati appena creato. Puoi utilizzare questo ID per monitorare, aggiornare o eliminare il flusso di dati.

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

### Monitorare il flusso di dati

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
            "createdAt": 1596656079576,
            "updatedAt": 1596656113526,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
            "sandboxName": "prod",
            "id": "9830305a-985f-47d0-b030-5a985fd7d004",
            "flowId": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
            "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1596656058198,
                    "completedAtUTC": 1596656113306
                },
                "sizeSummary": {
                    "inputBytes": 24012,
                    "outputBytes": 17128
                },
                "recordSummary": {
                    "inputRecordCount": 100,
                    "outputRecordCount": 99,
                    "failedRecordCount": 1
                },
                "fileSummary": {
                    "inputFileCount": 1,
                    "outputFileCount": 1,
                    "activityRefs": [
                        "promotionActivity"
                    ]
                },
                "statusSummary": {
                    "status": "success",
                    "errors": [
                        {
                            "code": "CONNECTOR-2001-500",
                            "message": "Error occurred at promotion activity."
                        }
                    ],
                    "activityRefs": [
                        "promotionActivity"
                    ]
                }
            },
            "activities": [
                {
                    "id": "copyActivity",
                    "updatedAtUTC": 1596656095088,
                    "durationSummary": {
                        "startedAtUTC": 1596656058198,
                        "completedAtUTC": 1596656089650,
                        "extensions": {
                            "windowStart": 1596653708000,
                            "windowEnd": 1596655508000
                        }
                    },
                    "sizeSummary": {
                        "inputBytes": 24012,
                        "outputBytes": 24012
                    },
                    "recordSummary": {},
                    "fileSummary": {
                        "inputFileCount": 1,
                        "outputFileCount": 1
                    },
                    "statusSummary": {
                        "status": "success",
                        "extensions": {
                            "type": "one-time"
                        }
                    },
                    "sourceInfo": [
                        {
                            "id": "c0e18602-f9ea-44f9-a186-02f9ea64f9ac",
                            "type": "SourceConnection",
                            "reference": {
                                "type": "AdfRunId",
                                "ids": [
                                    "8a8eb0cc-e283-4605-ac70-65a5adb1baef"
                                ]
                            }
                        }
                    ]
                },
                {
                    "id": "promotionActivity",
                    "updatedAtUTC": 1596656113485,
                    "durationSummary": {
                        "startedAtUTC": 1596656095333,
                        "completedAtUTC": 1596656113306
                    },
                    "sizeSummary": {
                        "inputBytes": 24012,
                        "outputBytes": 17128
                    },
                    "recordSummary": {
                        "inputRecordCount": 100,
                        "outputRecordCount": 99,
                        "failedRecordCount": 1
                    },
                    "fileSummary": {
                        "inputFileCount": 2,
                        "outputFileCount": 1,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=input_files"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success",
                        "errors": [
                            {
                                "code": "CONNECTOR-2001-500",
                                "message": "Error occurred at promotion activity."
                            }
                        ],
                        "extensions": {
                            "manifest": {
                                "failedRecords": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=row_errors",
                                "sampleErrors": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=row_error_samples.json"
                            },
                            "errors": [
                                {
                                    "code": "INGEST-1212-400",
                                    "message": "Encountered 1 errors in the data. Successfully ingested 99 rows. Review the associated diagnostic files for additional details."
                                },
                                {
                                    "code": "MAPPER-3700-400",
                                    "recordCount": 1,
                                    "message": "Mapper Transform Error"
                                }
                            ]
                        }
                    },
                    "targetInfo": [
                        {
                            "id": "47166b83-01c7-4b65-966b-8301c70b6562",
                            "type": "TargetConnection",
                            "reference": {
                                "type": "Batch",
                                "ids": [
                                    "01EF01X41KJD82Y9ZX6ET54PCZ"
                                ]
                            }
                        }
                    ]
                }
            ]
        }
    ],
    "_links": {}
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `items` | Contiene un singolo payload di metadati associati all’esecuzione di flusso specifica. |
| `metrics` | Definisce le caratteristiche dei dati nell&#39;esecuzione del flusso. |
| `activities` | Definisce la modalità di trasformazione dei dati. |
| `durationSummary` | Definisce l&#39;ora di inizio e di fine dell&#39;esecuzione del flusso. |
| `sizeSummary` | Definisce il volume dei dati in byte. |
| `recordSummary` | Definisce il conteggio dei record dei dati. |
| `fileSummary` | Definisce il conteggio dei file dei dati. |
| `statusSummary` | Definisce se l&#39;esecuzione del flusso è un successo o un errore. |

### Aggiornare il flusso di dati

Per aggiornare la pianificazione, il nome e la descrizione dell’esecuzione del flusso di dati, esegui una richiesta PATCH al [!DNL Flow Service] API fornendo al tempo stesso il tuo ID flusso, la versione e la nuova pianificazione che desideri utilizzare.

>[!IMPORTANT]
>
>La `If-Match` l’intestazione è necessaria quando si effettua una richiesta PATCH. Il valore di questa intestazione è il tag univoco del flusso di dati che si desidera aggiornare.

**Formato API**

```http
PATCH /flows/{FLOW_ID}
```

**Richiesta**

La richiesta seguente aggiorna la pianificazione di esecuzione del flusso, nonché il nome e la descrizione del flusso di dati.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/scheduleParams/frequency",
                "value": "day"
            },
            {
                "op": "replace",
                "path": "/name",
                "value": "New dataflow name"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "Updated dataflow description"
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
    "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

### Elimina il flusso di dati

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
    'https://platform.adobe.io/data/foundation/flowservice/flows/993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto. Puoi confermare l’eliminazione tentando una richiesta di ricerca (GET) al flusso di dati. L’API restituirà un errore HTTP 404 (Non trovato) che indica che il flusso di dati è stato eliminato.

### Aggiorna la connessione

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
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: 1400dd53-0000-0200-0000-5f3f23450000' \
    -d '[
        {
            "op": "replace",
            "path": "/auth/params",
            "value": {
                "username": "salesforce-connector-username",
                "password": "{NEW_PASSWORD}",
                "securityToken": "{NEW_SECURITY_TOKEN}"
            }
        },
        {
            "op": "replace",
            "path": "/name",
            "value": "Test salesforce connection"
        },
        {
            "op": "add",
            "path": "/description",
            "value": "A test salesforce connection"
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
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

### Elimina la connessione

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
    'https://platform.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto.

Puoi confermare l’eliminazione tentando una richiesta di ricerca (GET) alla connessione.
