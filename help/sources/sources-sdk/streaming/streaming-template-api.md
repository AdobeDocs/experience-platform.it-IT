---
title: Modello self-service della documentazione per l’API SDK per streaming
description: Scopri come portare i dati in streaming da un’origine a Adobe Experience Platform utilizzando l’API del servizio di flusso.
hide: true
hidefromtoc: true
source-git-commit: 7744fef9751212a40f8f20df52812d38130c42fc
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 1%

---

# Creare una connessione sorgente e un flusso di dati per lo streaming *GIOVANE* i dati che utilizzano [!DNL Flow Service] API

*Passando al modello, sostituisci o elimina tutti i paragrafi in corsivo (a partire da questo).*

*Per iniziare, aggiorna i metadati (titolo e descrizione) nella parte superiore della pagina. Ignora tutte le istanze di DNL in questa pagina. Questo è un tag che aiuta i nostri processi di traduzione automatica a tradurre correttamente la pagina nelle diverse lingue supportate. Dopo l’invio verranno aggiunti dei tag alla documentazione.*

## Panoramica

*Fornisci una breve panoramica della tua azienda, compreso il valore che fornisce ai clienti. Includi un collegamento alla home page della documentazione del prodotto per ulteriori informazioni.*

>[!IMPORTANT]
>
>Questa pagina della documentazione è stata creata da *GIOVANE* squadra. Per qualsiasi richiesta di informazioni o di aggiornamento, contattali direttamente all&#39;indirizzo *Inserire un collegamento o un indirizzo e-mail dove è possibile ottenere gli aggiornamenti*.

## Prerequisiti

*Aggiungi in questa sezione informazioni su qualsiasi cosa i clienti devono sapere prima di iniziare a configurare l’origine nell’interfaccia utente di Adobe Experience Platform. Può trattarsi di:*

* *aggiunta a un elenco consentiti*
* *requisiti per l’hash delle e-mail*
* *tutte le specifiche dell&#39;account sul tuo lato*
* *come ottenere una chiave API per connettersi alla piattaforma*

### Raccogli credenziali richieste

Per connettersi *GIOVANE* ad Experience Platform, è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| *credenziale uno* | *Aggiungi una breve descrizione alla credenziale di autenticazione della tua sorgente qui* | *Aggiungi un esempio della credenziale di autenticazione della tua origine qui* |
| *credenziale due* | *Aggiungi una breve descrizione alla credenziale di autenticazione della tua sorgente qui* | *Aggiungi un esempio della credenziale di autenticazione della tua origine qui* |
| *credenziale tre* | *Aggiungi una breve descrizione alla credenziale di autenticazione della tua sorgente qui* | *Aggiungi un esempio della credenziale di autenticazione della tua origine qui* |

Per ulteriori informazioni su queste credenziali, consulta la sezione *GIOVANE* documentazione sull’autenticazione. *Aggiungi un collegamento alla documentazione sull’autenticazione della piattaforma qui*.

### Integrare *GIOVANE* con il tuo gancio

*L&#39;SDK per lo streaming richiede che la tua origine sia in grado di supportare i webhook al fine di comunicare con Experience Platform. In questa sezione, devi fornire i passaggi che gli utenti dovranno seguire per integrare YOURSOURCE con un webhook.*

## Connetti *GIOVANE* su Platform utilizzando [!DNL Flow Service] API

L’esercitazione seguente illustra i passaggi necessari per creare un *GIOVANE* connessione di origine e creazione di un flusso di dati per portare *GIOVANE* dati a Platform tramite [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

### Creazione di una connessione sorgente {#source-connection}

Per creare una connessione sorgente per la sorgente di streaming, invia una richiesta POST al `/sourceConnections` punto finale [!DNL Flow Service] mentre fornisci un nome per la connessione, l’ID della specifica di connessione della sorgente e il formato dei dati.

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
      "name": "Streaming Source Connection for a Streaming SDK source",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Streaming Source Connection for a Streaming SDK source",
      "connectionSpec": {
          "id": "e77fd9d2-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      }
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della connessione di origine. Assicurati che il nome della connessione sorgente sia descrittivo, in quanto puoi utilizzarlo per cercare informazioni sulla connessione sorgente. |
| `description` | Un valore facoltativo che può essere incluso per fornire ulteriori informazioni sulla connessione sorgente. |
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

Una connessione di destinazione rappresenta la connessione alla destinazione in cui devono essere memorizzati i dati acquisiti. Per creare una connessione di destinazione, è necessario fornire l’ID di specifica di connessione fissa corrispondente al data lake. Questo ID è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ora disponi degli identificatori univoci di uno schema di destinazione di un set di dati di destinazione e dell’ID delle specifiche di connessione al data lake. Utilizzando questi identificatori, puoi creare una connessione di destinazione utilizzando [!DNL Flow Service] API per specificare il set di dati che conterrà i dati di origine in entrata.

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
      "name": "Streaming Target Connection for a Streaming SDK source",
      "description": "Streaming Target Connection for a Streaming SDK source",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "{TARGET_XDM_SCHEMA}",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "{TARGET_DATASET}"
      }
  }'
```


| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Nome della connessione di destinazione. Assicurati che il nome della connessione di destinazione sia descrittivo, in quanto puoi utilizzarlo per cercare informazioni sulla connessione di destinazione. |
| `description` | Un valore facoltativo che può essere incluso per fornire ulteriori informazioni sulla connessione di destinazione. |
| `connectionSpec.id` | ID della specifica di connessione corrispondente al data lake. Questo ID fisso è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
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
  'https://platform.adobe.io/data/foundation/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "{TARGET_XDM_SCHEMA}",
      "xdmVersion": "1.0",
      "mappings": [
          {
              "destinationXdmPath": "person.name.firstName",
              "sourceAttribute": "firstName",
              "identity": false,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.lastName",
              "sourceAttribute": "lastName",
              "identity": false,
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
      "name": "Streaming Dataflow for a Streaming SDK source",
      "description": "Streaming Dataflow for a Streaming SDK source",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
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
          "mappingVersion": 0
        }
      }
    ]
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome del flusso di dati. Assicurati che il nome del flusso di dati sia descrittivo in quanto puoi utilizzarlo per cercare informazioni sul flusso di dati. |
| `description` | Un valore facoltativo che può essere incluso per fornire ulteriori informazioni sul flusso di dati. |
| `flowSpec.id` | ID delle specifiche di flusso necessario per creare un flusso di dati. Questo ID fisso è: `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | Versione corrispondente dell’ID della specifica di flusso. Questo valore predefinito è `1.0`. |
| `sourceConnectionIds` | La [ID connessione di origine](#source-connection) generato in un passaggio precedente. |
| `targetConnectionIds` | La [ID connessione di destinazione](#target-connection) generato in un passaggio precedente. |
| `transformations` | Questa proprietà contiene le varie trasformazioni necessarie per essere applicate ai dati. Questa proprietà è necessaria per portare dati non conformi a XDM su Platform. |
| `transformations.name` | Nome assegnato alla trasformazione. |
| `transformations.params.mappingId` | La [ID mappatura](#mapping) generato in un passaggio precedente. |
| `transformations.params.mappingVersion` | Versione corrispondente dell&#39;ID di mappatura. Questo valore predefinito è `0`. |

**Risposta**

Una risposta corretta restituisce l&#39;ID (`id`) del flusso di dati appena creato. Puoi utilizzare questo ID per monitorare, aggiornare o eliminare il flusso di dati.

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

### Ottieni l&#39;URL dell&#39;endpoint di streaming

Con il flusso di dati creato, ora puoi recuperare l’URL dell’endpoint di streaming. Utilizzerai questo URL dell’endpoint per abbonare la tua sorgente a un webhook, consentendo alla tua sorgente di comunicare con l’Experience Platform.

Per recuperare l’URL dell’endpoint di streaming, effettua una richiesta GET al `/flows` e fornisci l&#39;ID del flusso di dati.

**Formato API**

```http
GET /flows/{FLOW_ID}
```

**Richiesta**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce informazioni sul flusso di dati, incluso l’URL dell’endpoint, contrassegnato come `inletUrl`.

```json
{
  "items": [
    {
      "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
      "createdAt": 1669238699119,
      "updatedAt": 1669238699119,
      "createdBy": "acme@AdobeID",
      "updatedBy": "acme@AdobeID",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "Streaming Dataflow for a Streaming SDK source",
      "description": "Streaming Dataflow for a Streaming SDK source",
      "flowSpec": {
        "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
        "version": "1.0"
      },
      "state": "enabled",
      "version": "\"a1011225-0000-0200-0000-63c78ae60000\"",
      "etag": "\"a1011225-0000-0200-0000-63c78ae60000\"",
      "sourceConnectionIds": [
        "246d052c-da4a-494a-937f-a0d17b1c6cf5"
      ],
      "targetConnectionIds": [
        "7c96c827-3ffd-460c-a573-e9558f72f263"
      ],
      "inheritedAttributes": {
        "properties": {
          "isSourceFlow": true
        },
        "sourceConnections": [
          {
            "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
            "connectionSpec": {
              "id": "bdb5b792-451b-42de-acf8-15f3195821de",
              "version": "1.0"
            }
          }
        ],
        "targetConnections": [
          {
            "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
            "connectionSpec": {
              "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
              "version": "1.0"
            }
          }
        ]
      },
      "options": {
        "errorDiagnosticsEnabled": true,
        "inletUrl": "https://dcs-int.adobedc.net/collection/ab65636c31778fb0455c439ffb48a5433a34d443f4c83c4b5beda9c5688797c5"
      },
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingVersion": 0,
            "mappingId": "bf5286a9c1ad4266baca76ba3adc9366"
          }
        }
      ],
      "runs": "/runs?property=flowId==e1514b79-f031-43b4-aab5-381a42f86ad4",
      "providerRefId": "c9809ab5-71e0-4c7f-887b-61c95e4e20b5",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "enable"
      }
    }
  ]
}
```

## Appendice

La sezione seguente fornisce informazioni sui passaggi necessari per monitorare, aggiornare ed eliminare il flusso di dati.

### Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni sulle esecuzioni del flusso, lo stato di completamento e gli errori. Per esempi completi sulle API, consulta la guida su [monitoraggio dei flussi di dati sorgente tramite API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### Aggiornare il flusso di dati

Aggiorna i dettagli del flusso di dati, ad esempio il nome e la descrizione, nonché la pianificazione di esecuzione e i set di mappature associati effettuando una richiesta di PATCH al `/flows` punto finale [!DNL Flow Service] , fornendo al tempo stesso l’ID del flusso di dati. Quando effettui una richiesta di PATCH, devi fornire l’univoco del flusso di dati `etag` in `If-Match` intestazione. Per esempi completi sulle API, consulta la guida su [aggiornamento dei flussi di dati di origini tramite API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### Aggiorna il tuo account

Aggiorna il nome, la descrizione e le credenziali dell&#39;account di origine effettuando una richiesta PATCH al [!DNL Flow Service] API fornendo l&#39;ID di connessione di base come parametro di query. Quando effettui una richiesta di PATCH, devi fornire l’account sorgente univoco `etag` in `If-Match` intestazione. Per esempi completi sulle API, consulta la guida su [aggiornamento dell’account sorgente tramite API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### Elimina il flusso di dati

Elimina il flusso di dati eseguendo una richiesta DELETE al [!DNL Flow Service] API fornendo l’ID del flusso di dati che desideri eliminare come parte del parametro di query. Per esempi completi sulle API, consulta la guida su [eliminazione dei flussi di dati tramite API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### Elimina l&#39;account

Elimina il tuo account eseguendo una richiesta DELETE al [!DNL Flow Service] API fornendo l’ID di connessione di base dell’account da eliminare. Per esempi completi sulle API, consulta la guida su [eliminazione dell’account sorgente tramite API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).