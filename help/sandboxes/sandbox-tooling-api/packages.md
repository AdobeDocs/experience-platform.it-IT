---
title: Endpoint API per pacchetti di strumenti sandbox
description: L’endpoint /packages nell’API degli strumenti sandbox consente di gestire in modo programmatico i pacchetti in Adobe Experience Platform.
source-git-commit: e4e89c5250885bef177ba0d678629261a361a66d
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 8%

---

# Endpoint &quot;packages&quot;

Gli strumenti sandbox consentono di selezionare diversi artefatti (noti anche come oggetti) ed esportarli in un pacchetto. Un pacchetto può essere costituito da un singolo artefatto o da più artefatti (come set di dati o schemi). Tutti gli artefatti inclusi in un pacchetto devono appartenere alla stessa sandbox.

Il `/packages` l’endpoint nell’API degli strumenti sandbox consente di gestire in modo programmatico i pacchetti nell’organizzazione, inclusa la pubblicazione di un pacchetto e l’importazione di un pacchetto in una sandbox.

## Creare un pacchetto {#create}

Per creare un pacchetto con più artefatti, devi effettuare una richiesta POST al `/packages` fornendo valori per il nome e il tipo di pacchetto.

**Formato API**

```http
POST /packages/
```

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "name": "acme",
      "description": "Acme Business Group",
      "packageType": "PARTIAL",    
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      },
      "expiry": "2023-05-20T20:05:10Z",
      "artifacts": [
        {
          "id": "27115daa-c92b-4f17-a077-d65ffeb0c525",
          "type": "PROFILE_SEGMENT",
          "title": "Acme Profile Segment"
        }      
      ]
  }'
```

| Proprietà | Descrizione | Tipo | Obbligatorio |
| --- | --- | --- | --- |
| `name` | Nome del pacchetto. | Stringa | Sì |
| `description` | Una descrizione per fornire ulteriori informazioni sul pacchetto. | Stringa | No |
| `packageType` | Il tipo di pacchetto è **PARZIALE** per indicare che si stanno includendo artefatti specifici in un pacchetto. | Stringa | SÌ |
| `sourceSandbox` | La sandbox di origine del pacchetto. | Stringa | No |
| `expiry` | Il timestamp che definisce la data di scadenza del pacchetto. Il valore predefinito è 90 giorni dalla data di creazione. Il campo di scadenza della risposta sarà l’ora UTC dell’epoca. | Stringa (formato timestamp UTC) | No |
| `artifacts` | Elenco di artefatti da esportare nel pacchetto. Il `artifacts` il valore deve essere **nulle** o **vuoto**, quando `packageType` è `FULL`. | Array | No |

**Risposta**

In caso di esito positivo, la risposta restituisce il pacchetto appena creato. La risposta include l’ID del pacchetto corrispondente, nonché informazioni sullo stato, sulla scadenza e sull’elenco degli artefatti.

```json
{
    "id": "209f886b00444eac9bb5836fe32e7681",
    "version": 0,
    "createdDate": 1684475012105,
    "modifiedDate": 1684475012105,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "requestId": "devxa54a6b56d04f46119d9e3cc006fcc1cb",
    "userId": "platform_exim",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "cjm-mr",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1684613110000,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## Aggiornare un pacchetto {#update}

Per aggiornare un pacchetto, devi effettuare una richiesta PUT al `/packages` endpoint.

### Aggiungere artefatti a un pacchetto {#add-artifacts}

Per aggiungere artefatti a un pacchetto, è necessario fornire un `id` e includono **AGGIUNGI** per `action`.

**Formato API**

```http
PUT /packages/
```

**Richiesta**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "ADD",
      "expiry": "2023-05-20T20:05:10Z", 
      "artifacts": [
        {
         "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
         "type": "JOURNEY"
        }      
      ]
  }'
```

| Proprietà | Descrizione | Tipo | Obbligatorio |
| --- | --- | --- | --- |
| `id` | ID del pacchetto da aggiornare. | Stringa | Sì |
| `action` | Per aggiungere artefatti al pacchetto, il valore dell’azione deve essere **AGGIUNGI**. Questa azione è supportata solo **PARZIALE** tipi di pacchetti. | Stringa | Sì |
| `artifacts` | Elenco di artefatti da aggiungere al pacchetto. Non ci sarebbe alcuna modifica al pacchetto se l&#39;elenco è **nulle** o **vuoto**. Gli artefatti vengono deduplicati prima di essere aggiunti al pacchetto. | Array | No |
| `expiry` | Il timestamp che definisce la data di scadenza del pacchetto. Il valore predefinito è 90 giorni dalla chiamata dell’API di PUT se la scadenza non è specificata nel payload. Il campo di scadenza della risposta sarà l’ora UTC dell’epoca. | Stringa (formato timestamp UTC) | No |

**Risposta**

In caso di esito positivo, la risposta restituisce il pacchetto aggiornato. La risposta include l’ID del pacchetto corrispondente, nonché informazioni sullo stato, sulla scadenza e sull’elenco degli artefatti.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 4,
    "createdDate": 1684235842000,
    "modifiedDate": 1684475861366,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1692251861352,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### Eliminare gli artefatti da un pacchetto {#delete-artifacts}

Per eliminare gli artefatti da un pacchetto, è necessario fornire un `id` e includono **DELETE** per `action`.


**Formato API**

```http
PUT /packages/
```

**Richiesta**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "DELETE",
      "artifacts": [
        {
          "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
          "type": "JOURNEY"
        }      
      ]
  }'
```

| Proprietà | Descrizione | Tipo | Obbligatorio |
| --- | --- | --- | --- |
| `id` | ID del pacchetto da aggiornare. | Stringa | Sì |
| `action` | Per eliminare gli artefatti da un pacchetto, il valore dell’azione deve essere **DELETE**. Questa azione è supportata solo **PARZIALE** tipi di pacchetti. | Stringa | Sì |
| `artifacts` | Elenco di artefatti da eliminare dal pacchetto. Non ci sarebbe alcuna modifica al pacchetto se l&#39;elenco è **nulle** o **vuoto**. | Array | No |

**Risposta**

In caso di esito positivo, la risposta restituisce il pacchetto aggiornato. La risposta include l’ID del pacchetto corrispondente, nonché informazioni sullo stato, sulla scadenza e sull’elenco degli artefatti.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 5,
    "createdDate": 1684235842000,
    "modifiedDate": 1684478830416,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },      
    "packageType": "PARTIAL",
    "expiry": 1692254830403,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### Aggiornare i campi di metadati in un pacchetto {#update-metadata}

>[!NOTE]
>
>Il **AGGIORNA** viene utilizzata per aggiornare i campi di metadati del pacchetto e **non può** per aggiungere o eliminare artefatti in un pacchetto.

Per aggiornare i campi di metadati in un pacchetto, devi fornire un `id` e includono **AGGIORNA** per `action`.

**Formato API**

```http
PUT /packages/
```

**Richiesta**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "UPDATE",
      "name": "acme",
      "description": "Acme Business Group",  
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      }
  }'
```

| Proprietà | Descrizione | Tipo | Obbligatorio |
| --- | --- | --- | --- |
| `id` | ID del pacchetto da aggiornare. | Stringa | Sì |
| `action` | Per aggiornare i campi di metadati in un pacchetto, il valore dell’azione deve essere **AGGIORNA**. Questa azione è supportata solo **PARZIALE** tipi di pacchetti. | Stringa | Sì |
| `name` | Nome aggiornato del pacchetto. I nomi di pacchetto duplicati non sono consentiti. | Array | Sì |
| `sourceSandbox` | La sandbox di origine deve appartenere alla stessa organizzazione specificata nell’intestazione della richiesta. | Stringa | Sì |

**Risposta**

In caso di esito positivo, la risposta restituisce il pacchetto aggiornato. La risposta include l’ID del pacchetto corrispondente, nonché informazioni su descrizione, stato, scadenza ed elenco degli artefatti.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 6,
    "createdDate": 1684235842000,
    "modifiedDate": 1684479094129,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",    
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "packageType": "PARTIAL",
    "expiry": 1692255094127,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## Eliminare un pacchetto {#delete}

Per eliminare un pacchetto, effettua una richiesta DELETE al `/packages` e specificare l&#39;ID del pacchetto da eliminare.

**Formato API**

```http
DELETE /packages/{PACKAGE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| {PACKAGE_ID} | ID del pacchetto da eliminare. |

**Richiesta**

La seguente richiesta elimina il pacchetto con l’ID {PACKAGE_ID}.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce un motivo che mostra l’ID pacchetto eliminato.

```json
{
    "reason": "Package d30e0424a37b46ada6a5cf37f47a86ff deleted"
}
```

## Pubblicare un pacchetto {#publish}

Per abilitare l’importazione di un pacchetto in una sandbox, devi pubblicarlo. Effettuare una richiesta di GET al `/packages` endpoint durante la specifica dell’ID del pacchetto da pubblicare.

**Formato API**

```http
GET /packages/{PACKAGE_ID}/export
```

| Parametro | Descrizione |
| --- | --- |
| {PACKAGE_ID} | ID del pacchetto da pubblicare. |

**Richiesta**

La richiesta seguente pubblica il pacchetto con l’ID {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}\export \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| Proprietà | Descrizione | Tipo | Obbligatorio |
| --- | --- | --- | --- |
| `expiryPeriod` | Questo periodo di tempo specificato dall&#39;utente definisce la data di scadenza del pacchetto (in giorni) dal momento in cui il pacchetto è stato pubblicato. Questo valore non deve essere negativo.<br> Se non viene specificato alcun valore, il valore predefinito sarà calcolato come 90 (giorni) dalla data di pubblicazione. | Intero | No |

**Risposta**

In caso di esito positivo, la risposta restituisce il pacchetto pubblicato.

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285"
}
```

## Cercare un pacchetto {#look-up-package}

Per cercare un singolo pacchetto, devi effettuare una richiesta GET al `/packages` endpoint che include l’ID corrispondente del pacchetto nel percorso della richiesta.

**Formato API**

```http
GET /packages/{PACKAGE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| {PACKAGE_ID} | ID del pacchetto da cercare. |

**Richiesta**

La richiesta seguente recupera informazioni per {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli per l’ID pacchetto richiesto. La risposta include il nome, la descrizione, la data di pubblicazione e la data di scadenza, la sandbox di origine del pacchetto e un elenco di artefatti.

```json
{
    "id": "8f585fad94d042cd82dbcba594108a41",
    "version": 2,
    "createdDate": 1685597784000,
    "modifiedDate": 1685597810000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
    "packageType": "PARTIAL",
    "expiry": 1693373810000,
    "publishDate": 1685597810000,
    "status": "PUBLISHED",
    "artifactsList": [
        {
            "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ],
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    }
}
```

## Elencare pacchetti {#list-packages}

Puoi elencare tutti i pacchetti nella tua organizzazione effettuando una richiesta GET al `/packages` endpoint.

**Formato API**

```http
GET /packages/?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| {QUERY_PARAMS} | Parametri di query facoltativi in base ai quali filtrare i risultati. Consulta la sezione su [parametri di query](./appendix.md) per ulteriori informazioni. |

**Richiesta**

La richiesta seguente recupera le informazioni dei pacchetti in base al {QUERY_PARAMS}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/?property=status==DRAFT,PUBLISHED&property=createdDate>=2023-05-11T18:29:59.999Z&property=createdDate<=2023-05-16T18:29:59.999Z&start=0&orderby=-createdDate&limit=20 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di pacchetti appartenenti all’organizzazione, inclusi dettagli quali nome, stato, scadenza ed elenco di artefatti.

```json
{
    "totalElements": 109,
    "currentPage": 0,
    "totalPages": 6,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "8f585fad94d042cd82dbcba594108a41",
            "version": 2,
            "createdDate": 1685597784000,
            "modifiedDate": 1685597810000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "c875b077162b40409c1327b16da99c1b",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693373810000,
            "publishDate": 1685597810000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                },
                {
                    "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        },
        {
            "id": "0d7e427ce4cb4dc1b78e30ef61b125c1",
            "version": 2,
            "createdDate": 1685555213000,
            "modifiedDate": 1685555275000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "7d7d8bbe3c7c4a8ea701cc5e42c57aeb",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693331275000,
            "publishDate": 1685555275000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "626a9669a9f5b818db270e95",
                    "type": "CATALOG_DATASET",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        }
    ]
}
```

## Importare un pacchetto {#import}

Questo endpoint viene utilizzato per recuperare gli oggetti in conflitto nella sandbox di destinazione specificata. Gli oggetti in conflitto rappresentano oggetti simili già presenti nella sandbox di destinazione.

**Formato API**

```http
GET /packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName
```

| Parametro | Descrizione |
| --- | --- |
| {PACKAGE_ID} | ID del pacchetto da cercare. |

**Richiesta**

La richiesta seguente importa {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

I conflitti vengono restituiti nella risposta. La risposta mostra il pacchetto originale più il `alternatives` frammento come array ordinato per classificazione.

Visualizza risposta+++

```json
[
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
            "type": "REGISTRY_SCHEMA",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/176f33f6a8ff6542de1256f8dc01cce4be1b3a68fd5f5bc5",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686403052050"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/1b37c3403e4e12c7aa46ea9dfe380a9f2b72d4da9db62b46",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686218766627"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_SCHEMA::https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
    },
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
            "type": "REGISTRY_CLASS",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/1dd81d61cdaa89a89382d0a424db77494475bd1db3105feb",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686564843736"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/classes/2511fb5396a630b2cd3d5d9e9b69d42ce66a4289db8ac917",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686408152916"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_CLASS::https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
    },
    {
        "artifact": {
            "id": "4d4c874ec3344d64bf8b3160e60ac78b",
            "type": "MAPPING_SET",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: 4d4c874ec3344d64bf8b3160e60ac78b"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "6b49c959d77c48e9904f7616fe2e7848",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "7b363da9e6704afb9716f57193d5246f",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "93ca0b4f437c4eaf9f1986408679e965",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::MAPPING_SET::4d4c874ec3344d64bf8b3160e60ac78b"
    }
]
```

+++

## Inviare un’importazione {#submit-import}

>[!NOTE]
>
>Per la risoluzione dei conflitti è fondamentale che l’artefatto alternativo esista già nella sandbox di destinazione.

È possibile inviare un&#39;importazione per un pacchetto dopo aver esaminato i conflitti e fornito le sostituzioni effettuando una richiesta POST al `/packages` endpoint. Il risultato viene fornito come payload, che avvia il processo di importazione per la sandbox di destinazione come specificato nel payload.

Il payload accetta anche il nome e la descrizione del processo specificati dall’utente per il processo di importazione. Se il nome e la descrizione specificati dall&#39;utente non sono disponibili, vengono utilizzati il nome e la descrizione del pacchetto per il nome e la descrizione del processo.

**Formato API**

```http
POST /packages/import
```

**Richiesta**

La richiesta seguente recupera il pacchetto utilizzando {PACKAGE_ID} fornite. Il payload è una mappa di sostituzioni in cui, se è presente una voce, la chiave è `artifactId` fornite dal pacchetto, e l’alternativa è il valore. Se la mappa o il payload è **vuoto**, non vengono eseguite sostituzioni.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
       "id": "09484a599f5f4a5faa43986643964615",
       "name": "acme",
       "description": "Acme Business Group",
       "destinationSandbox": {
         "name": "cjm-mr",
         "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
     },
     "alternatives": {
       "https://ns.adobe.com/cjmstage/schemas/ac33bbd22eb4ad6656e1c7e12e9f520261fb39fd28a902a9": {
         "id": "https://ns.adobe.com/cjmstage/schemas/a3b935344685afad4e52c753161cf673ec23d4fb1b3e9ce",
         "type": "REGISTRY_SCHEMA"
       }
     }
  }'
```

| Proprietà | Descrizione | Tipo | Obbligatorio |
| --- | --- | --- | --- |
| `id` | ID del pacchetto. | Stringa | Sì |
| `alternatives` | `alternatives` rappresenta il mapping degli artefatti sandbox di origine agli artefatti sandbox di destinazione esistenti. Poiché sono già presenti, il processo di importazione evita la creazione di questi artefatti nella sandbox di destinazione. | Stringa | No |

**Risposta**

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "destinationSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285"
}
```

## Elenca tutti gli oggetti dipendenti {#dependent-objects}

Elencare tutti gli oggetti dipendenti per gli oggetti esportati in un pacchetto effettuando una richiesta POST al `/packages` endpoint durante la specifica dell’ID del pacchetto.

**Formato API**

```http
POST /packages/{PACKAGE_ID}/children
```

| Parametro | Descrizione |
| --- | --- |
| {PACKAGE_ID} | ID del pacchetto. |

**Richiesta**

La richiesta seguente elenca tutti gli oggetti dipendenti per {PACKAGE_ID}.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d'[
      {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "type": "REGISTRY_SCHEMA"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "type": "REGISTRY_CLASS"
      }
  ]'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di elementi figlio per gli oggetti.

```json
[
    {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "title": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
                "type": "REGISTRY_SCHEMA"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
        "type": "REGISTRY_SCHEMA",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
                "type": "REGISTRY_CLASS"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
        "type": "REGISTRY_CLASS",
        "children": []
    }
]
```

## Controlla le autorizzazioni basate sul ruolo per importare tutti gli artefatti del pacchetto {#role-based-permissions}

Per verificare se si dispone delle autorizzazioni necessarie per importare gli artefatti del pacchetto, effettuare una richiesta GET al `/packages` endpoint durante la specifica dell’ID del pacchetto e del nome della sandbox di destinazione.

**Formato API**

```http
GET /packages/preflight/{packageId}?targetSandbox=<sandbox_name
```

| Parametro | Descrizione |
| --- | --- |
| {PACKAGE_ID} | ID del pacchetto da importare. |

**Richiesta**

La richiesta seguente verifica le autorizzazioni per {PACKAGE_ID} e sandbox.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/preflight/{PACKAGE_ID}?targetSandbox=<sandbox_name> \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce le autorizzazioni per le risorse per la sandbox di destinazione, incluso un elenco di autorizzazioni richieste, autorizzazioni mancanti, tipo di artefatto e una decisione su come consentire o meno la creazione.

Visualizza risposta+++

```json
{
  "packageID": "b7bda68eb1214c86824f1d7204616e51",
  "targetSandboxName": "acme-sandbox",
  "permissionResponse": [
    {
      "artifactID": "4aca57b6-8b83-450b-a460-e8a07ca79a44",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "Schema",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "Segment",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Composition",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Query",
            "resourcePermissions": [
              "write"
            ]
          },
          {
            "palmResourceType": "SegmentDashboard",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": []
      },
      "artifactType": "PROFILE_SEGMENT",
      "creationAllowed": true
    },
    {
      "artifactID": "36bb82bc-a00d-4d6b-a598-227d43e027c1",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": [
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "artifactType": "PROFILE_MERGE",
      "creationAllowed": false
    }
  ]
}
```

+++

## Elencare processi di esportazione/importazione {#list-jobs}

È possibile elencare i processi di esportazione/importazione correnti effettuando una richiesta di GET al `/packages` endpoint.

**Formato API**

```http
GET /packages/jobs?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| {QUERY_PARAMS} | Parametri di query facoltativi in base ai quali filtrare i risultati. Consulta la sezione su [parametri di query](./appendix.md) per ulteriori informazioni. |

**Richiesta**

La richiesta seguente elenca tutti i processi di importazione riusciti.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/jobs?property=requestType==IMPORT&property=jobStatus==SUCCESS&orderby=createdDate&start=0&limit=5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce tutti i processi di importazione riusciti.

```json
{
    "totalElements": 42,
    "currentPage": 0,
    "totalPages": 9,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "3c1b92cf47a246d7bfbe6fd507c5d543",
            "name": "acme",
            "updated": 1685973675401,
            "created": 1685973675401,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "ead59d21405f4184a94dd786a1bf040d",
            "name": "acme1",
            "updated": 1685986367198,
            "created": 1685986367198,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "85ddaa3c2f6c475088167cde7a9d4326",
            "name": "acme2",
            "updated": 1686147692568,
            "created": 1686147692568,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "c49a4fcb31954cbd828ece1da096c8f5",
            "name": "acme3",
            "updated": 1686148007586,
            "created": 1686148007586,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "a3669315baed4cf2af49bf9ce90b8158",
            "name": "acme4",
            "updated": 1686148651910,
            "created": 1686148651910,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        }
    ]
}
```
