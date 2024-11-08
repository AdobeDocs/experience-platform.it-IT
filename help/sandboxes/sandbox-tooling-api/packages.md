---
title: Endpoint API per pacchetti di strumenti sandbox
description: L’endpoint /packages nell’API degli strumenti sandbox consente di gestire in modo programmatico i pacchetti in Adobe Experience Platform.
exl-id: 46efee26-d897-4941-baf4-d5ca0b8311f0
source-git-commit: e029380dd970195d1254ee3ea1cd68ba2574bbd3
workflow-type: tm+mt
source-wordcount: '2543'
ht-degree: 10%

---

# Endpoint &quot;packages&quot;

Gli strumenti sandbox consentono di selezionare diversi artefatti (noti anche come oggetti) ed esportarli in un pacchetto. Un pacchetto può essere costituito da un singolo artefatto o da più artefatti (come set di dati o schemi). Tutti gli artefatti inclusi in un pacchetto devono appartenere alla stessa sandbox.

L&#39;endpoint `/packages` nell&#39;API degli strumenti sandbox consente di gestire in modo programmatico i pacchetti dell&#39;organizzazione, ad esempio la pubblicazione di un pacchetto e l&#39;importazione di un pacchetto in una sandbox.

## Creare un pacchetto {#create}

È possibile creare un pacchetto con più artefatti effettuando una richiesta POST all&#39;endpoint `/packages` e fornendo i valori per il nome e il tipo di pacchetto del pacchetto.

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
| `packageType` | Il tipo di pacchetto è **PARTIAL** per indicare che si stanno includendo artefatti specifici in un pacchetto. | Stringa | SÌ |
| `sourceSandbox` | La sandbox di origine del pacchetto. | Oggetto | No |
| `expiry` | Il timestamp che definisce la data di scadenza del pacchetto. Il valore predefinito è 90 giorni dalla data di creazione. Il campo di scadenza della risposta sarà l’ora UTC dell’epoca. | Stringa (formato timestamp UTC) | No |
| `artifacts` | Elenco di artefatti da esportare nel pacchetto. Il valore `artifacts` deve essere **null** o **empty**, quando `packageType` è `FULL`. | Array | No |

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

È possibile aggiornare un pacchetto effettuando una richiesta PUT all&#39;endpoint `/packages`.

### Aggiungere artefatti a un pacchetto {#add-artifacts}

Per aggiungere artifact a un pacchetto, è necessario specificare `id` e includere **ADD** per `action`.

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
| `action` | Per aggiungere artifact al pacchetto, il valore dell&#39;azione deve essere **ADD**. Questa azione è supportata solo per i tipi di pacchetto **PARTIAL**. | Stringa | Sì |
| `artifacts` | Elenco di artefatti da aggiungere al pacchetto. Non ci sarebbero modifiche al pacchetto se l&#39;elenco è **null** o **empty**. Gli artefatti vengono deduplicati prima di essere aggiunti al pacchetto. Per un elenco completo degli artefatti supportati, consulta la tabella seguente. | Array | No |
| `expiry` | Il timestamp che definisce la data di scadenza del pacchetto. Il valore predefinito è 90 giorni dalla chiamata dell’API di PUT se la scadenza non è specificata nel payload. Il campo di scadenza della risposta sarà l’ora UTC dell’epoca. | Stringa (formato timestamp UTC) | No |

I seguenti tipi di artefatto sono attualmente supportati.

| Artefatto | Piattaforma | Oggetto | Flusso parziale | Sandbox completa |
| --- | --- | --- | --- | --- |
| `JOURNEY` | Adobe Journey Optimizer | Percorsi | Sì | No |
| `ID_NAMESPACE` | Customer Data Platform | Identità | Sì | Sì |
| `REGISTRY_DATATYPE` | Customer Data Platform | Tipo di dati | Sì | Sì |
| `REGISTRY_CLASS` | Customer Data Platform | Classe | Sì | Sì |
| `REGISTRY_MIXIN` | Customer Data Platform | Gruppo di campi | Sì | Sì |
| `REGISTRY_SCHEMA` | Customer Data Platform | Schemi | Sì | Sì |
| `CATALOG_DATASET` | Customer Data Platform | Set di dati | Sì | Sì |
| `DULE_CONSENT_POLICY` | Customer Data Platform | Criteri di consenso e governance | Sì | Sì |
| `PROFILE_SEGMENT` | Customer Data Platform | Tipi di pubblico | Sì | Sì |
| `FLOW` | Customer Data Platform | Flusso di dati origini | Sì | Sì |

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

Per eliminare gli artifact da un pacchetto, è necessario fornire `id` e includere **DELETE** per `action`.

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
| `action` | Per eliminare gli artifact da un pacchetto, il valore dell&#39;azione deve essere **DELETE**. Questa azione è supportata solo per i tipi di pacchetto **PARTIAL**. | Stringa | Sì |
| `artifacts` | Elenco di artefatti da eliminare dal pacchetto. Non ci sarebbero modifiche al pacchetto se l&#39;elenco è **null** o **empty**. | Array | No |

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
>L&#39;azione **AGGIORNA** viene utilizzata per aggiornare i campi dei metadati del pacchetto e **non può** essere utilizzata per aggiungere/eliminare artifact a un pacchetto.

Per aggiornare i campi di metadati in un pacchetto, è necessario fornire `id` e includere **UPDATE** per `action`.

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
| `action` | Per aggiornare i campi di metadati in un pacchetto, il valore dell&#39;azione deve essere **UPDATE**. Questa azione è supportata solo per i tipi di pacchetto **PARTIAL**. | Stringa | Sì |
| `name` | Nome aggiornato del pacchetto. I nomi di pacchetto duplicati non sono consentiti. | Array | Sì |
| `sourceSandbox` | La sandbox di Source deve appartenere alla stessa organizzazione specificata nell’intestazione della richiesta. | Oggetto | Sì |

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

Per eliminare un pacchetto, effettuare una richiesta DELETE all&#39;endpoint `/packages` e specificare l&#39;ID del pacchetto da eliminare.

**Formato API**

```http
DELETE /packages/{PACKAGE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{PACKAGE_ID}` | ID del pacchetto da eliminare. |

**Richiesta**

La richiesta seguente elimina il pacchetto con ID {PACKAGE_ID}.

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

## Publish un pacchetto {#publish}

Per abilitare l’importazione di un pacchetto in una sandbox, devi pubblicarlo. Effettuare una richiesta di GET all&#39;endpoint `/packages` specificando l&#39;ID del pacchetto da pubblicare.

**Formato API**

```http
GET /packages/{PACKAGE_ID}/export
```

| Parametro | Descrizione |
| --- | --- |
| `{PACKAGE_ID}` | ID del pacchetto da pubblicare. |

**Richiesta**

La richiesta seguente pubblica il pacchetto con ID {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}\export \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| Proprietà | Descrizione | Tipo | Obbligatorio |
| --- | --- | --- | --- |
| `expiryPeriod` | Questo periodo di tempo specificato dall&#39;utente definisce la data di scadenza del pacchetto (in giorni) dal momento in cui il pacchetto è stato pubblicato. Questo valore non deve essere negativo.<br> Se non viene specificato alcun valore, il valore predefinito verrà calcolato come 90 (giorni) dalla data di pubblicazione. | Intero | No |

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

Per cercare un singolo pacchetto, devi eseguire una richiesta GET all&#39;endpoint `/packages` che includa l&#39;ID corrispondente del pacchetto nel percorso della richiesta.

**Formato API**

```http
GET /packages/{PACKAGE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{PACKAGE_ID}` | ID del pacchetto da cercare. |

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

È possibile elencare tutti i pacchetti dell&#39;organizzazione effettuando una richiesta di GET all&#39;endpoint `/packages`.

**Formato API**

```http
GET /packages/?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUERY_PARAMS}` | Parametri di query facoltativi in base ai quali filtrare i risultati. Per ulteriori informazioni, vedere la sezione relativa ai [parametri di query](./appendix.md). |

**Richiesta**

La richiesta seguente recupera le informazioni dei pacchetti in base a {QUERY_PARAMS}.

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
| `{PACKAGE_ID}` | ID del pacchetto da cercare. |

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

I conflitti vengono restituiti nella risposta. La risposta mostra il pacchetto originale più il frammento `alternatives` come un array ordinato per classificazione.

+++Visualizza risposta

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

Dopo aver esaminato i conflitti e fornito le sostituzioni, è possibile inviare un&#39;importazione per un pacchetto effettuando una richiesta POST all&#39;endpoint `/packages`. Il risultato viene fornito come payload, che avvia il processo di importazione per la sandbox di destinazione come specificato nel payload.

Il payload accetta anche il nome e la descrizione del processo specificati dall’utente per il processo di importazione. Se il nome e la descrizione specificati dall&#39;utente non sono disponibili, vengono utilizzati il nome e la descrizione del pacchetto per il nome e la descrizione del processo.

**Formato API**

```http
POST /packages/import
```

**Richiesta**

La richiesta seguente recupera i pacchetti da importare. Il payload è una mappa di sostituzioni in cui, se esiste una voce, la chiave è `artifactId` fornita dal pacchetto e l&#39;alternativa è il valore. Se la mappa o il payload è **vuoto**, non vengono eseguite sostituzioni.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/import/ \
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
| `alternatives` | `alternatives` rappresenta il mapping degli artifact sandbox di origine agli artifact sandbox di destinazione esistenti. Poiché sono già presenti, il processo di importazione evita la creazione di questi artefatti nella sandbox di destinazione. | Stringa | No |

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

Elencare tutti gli oggetti dipendenti per gli oggetti esportati in un pacchetto effettuando una richiesta POST all&#39;endpoint `/packages` mentre si specifica l&#39;ID del pacchetto.

**Formato API**

```http
POST /packages/{PACKAGE_ID}/children
```

| Parametro | Descrizione |
| --- | --- |
| `{PACKAGE_ID}` | ID del pacchetto. |

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

Per verificare se si dispone delle autorizzazioni per importare gli artefatti del pacchetto, eseguire una richiesta GET all&#39;endpoint `/packages` specificando l&#39;ID del pacchetto e il nome della sandbox di destinazione.

**Formato API**

```http
GET /packages/preflight/{packageId}?targetSandbox=<sandbox_name
```

| Parametro | Descrizione |
| --- | --- |
| `{PACKAGE_ID}` | ID del pacchetto da importare. |

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

+++Visualizza risposta

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

È possibile elencare i processi di esportazione/importazione correnti effettuando una richiesta GET all&#39;endpoint `/packages`.

**Formato API**

```http
GET /packages/jobs?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUERY_PARAMS}` | Parametri di query facoltativi in base ai quali filtrare i risultati. Per ulteriori informazioni, vedere la sezione relativa ai [parametri di query](./appendix.md). |

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

## Condivisione di pacchetti tra organizzazioni {#org-linking}

L&#39;endpoint `/handshake` nell&#39;API degli strumenti sandbox consente di collaborare con altre organizzazioni per condividere i pacchetti.

### Invio di una richiesta di condivisione {#send-request}

Invia una richiesta a un&#39;organizzazione partner di destinazione per l&#39;approvazione condivisa eseguendo una richiesta POST all&#39;endpoint `/handshake/bulkCreate`. Questa operazione è necessaria prima di poter condividere pacchetti privati.

**Formato API**

```http
POST /handshake/bulkCreate
```

**Richiesta**

La richiesta seguente avvia la condivisione dell’approvazione tra un’organizzazione partner di destinazione e l’organizzazione di origine.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/handshake/bulkCreate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "targetIMSOrgIds":["acme@AdobeOrg"],
      "sourceIMSDetails":{
        "id":"acme@AdobeOrg",
        "name":"acme_org"
      } 
  }' 
```

| Proprietà | Descrizione | Tipo | Obbligatorio |
| --- | --- | --- | --- |
| `targetIMSOrgIds` | Elenco di organizzazioni target a cui inviare la richiesta di condivisione. | Array | Sì |
| `sourceIMSDetails` | Dettagli sull’organizzazione di origine. | Oggetto | Sì |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli relativi alla richiesta di condivisione.

```json
{
    "successfulRequests": {
        "acme@AdobeOrg": {
            "id": "{ID}",
            "version": 0,
            "createdDate": 1724938816798,
            "modifiedDate": 1724938816798,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "sourceIMSOrgId": "{ORG_ID}",
            "targetIMSOrgId": "{TARGET_ID}",
            "sourceRegion": "va6",
            "sourceIMSOrgName": "{SOURCE_NAME}",
            "status": "APPROVAL_PENDING",
            "createdByName": "{CREATED_BY}",
            "modifiedByName": "{MODIFIED_BY}",
            "modifiedByIMSOrgId": "{ORG_ID}",
            "statusHistory": "[{\"actionTakenBy\":\"acme@98ff67fa661fdf6549420b.e\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"INITIATED\",\"actionTimeStamp\":1724938816885}]",
            "linkingId": "{LINKIND_ID}"
        }
    },
    "failedRequests": {}
}
```

### Approvazione delle richieste di condivisione ricevute {#approve-requests}

Approva le richieste di condivisione da parte delle organizzazioni partner di destinazione effettuando una richiesta POST all&#39;endpoint `/handshake/action`. Dopo l’approvazione, le organizzazioni partner di origine possono condividere pacchetti privati.

**Formato API**

```http
POST /handshake/action
```

**Richieste**

La richiesta seguente approva una richiesta di condivisione da parte di un&#39;organizzazione partner di destinazione.

```shell
curl -X POST  \
  https://platform.adobe.io/data/foundation/exim/handshake/action \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "linkingID":"{LINKING_ID}",
      "status":"APPROVED",
      "reason":"Done",
      "targetIMSOrgDetails":{
          "id":"acme@AdobeOrg",
          "name":"acme",
          "region":"va7"
      }
  }'
```

| Proprietà | Descrizione | Tipo | Obbligatorio |
| --- | --- | --- | --- |
| `linkingID` | ID della richiesta di condivisione a cui stai rispondendo. | Stringa | Sì |
| `status` | Azione eseguita sulla richiesta di condivisione. | Stringa | Sì |
| `reason` | Motivo dell&#39;azione. | Stringa | Sì |
| `targetIMSOrgDetails` | Dettagli sull&#39;organizzazione di destinazione in cui il valore ID deve essere il **ID** dell&#39;organizzazione di destinazione, il valore nome deve essere il **NAME** delle organizzazioni di destinazione e il valore regione deve essere le organizzazioni di destinazione **REGION**. | Oggetto | Sì |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli relativi alla richiesta di condivisione approvata.

```json
{
    "id": "{ID}",
    "version": 1,
    "createdDate": 1726737474000,
    "modifiedDate": 1726737541731,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceIMSOrgId": "{ORG_ID}",
    "targetIMSOrgId": "{TARGET_ID}",
    "sourceRegion": "va7",
    "targetRegion": "va7",
    "sourceOrgName": "{SOURCE_ORG}",
    "targetOrgName": "{TARGET_ORG}",
    "status": "APPROVED",
    "createdByName": "{CREATED_BY}",
    "modifiedByIMSOrgId": "{MODIFIED_BY}",
    "statusHistory": "[{\"actionTakenBy\":\"{ACTION_BY}\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"acme@AdobeOrg\",\"action\":\"INITIATED\",\"actionTimeStamp\":1726737474450,\"reason\":null},{\"actionTakenBy\":null,\"actionTakenByName\":null,\"actionTakenByImsOrgID\":\"745F37C35E4B776E0A49421B@AdobeOrg\",\"action\":\"APPROVED\",\"actionTimeStamp\":1726737541818,\"reason\":\"Done\"}]",
    "linkingId": "{LINKING_ID}"
}
```

### Elencare richieste di condivisione in uscita/in arrivo {#outgoing-and-incoming-requests}

Elencare le richieste di condivisione in uscita e in ingresso effettuando una richiesta GET all&#39;endpoint `handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING`.

**Formato API**

```http
POST handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING
```

| Parametro | Valori accettati/predefiniti |
| --- | --- |
| `property` | Specifica la proprietà in base alla quale filtrare, ad esempio lo stato. I valori accettabili per lo stato sono: `APPROVED`, `REJECTED` e `IN_PROGRESS`. |
| `start` | Il valore predefinito di inizio è `0`. |
| `limit` | Il valore predefinito del limite è `20`. |
| `orderBy` | Ordina i record in ordine crescente o decrescente. |
| `requestType` | Accetta `INCOMING` o `OUTGOING`. |

**Richiesta**

La richiesta seguente restituisce un elenco di tutte le richieste di condivisione in uscita e in ingresso.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id:{ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco delle richieste di condivisione in uscita e in entrata e i relativi dettagli.

```json
{
    "totalElements": 1,
    "currentPage": 0,
    "totalPages": 1,
    "hasPreviousPage": false,
    "hasNextPage": false,
    "data": [
        {
            "id": "{ID}",
            "version": 1,
            "createdDate": 1724929446000,
            "modifiedDate": 1724929617000,
            "modifiedBy": "{MODIFIED_BY}",
            "sourceIMSOrgId": "{ORG_ID}",
            "targetIMSOrgId": "{TARGET_ID}",
            "sourceRegion": "va7",
            "targetRegion": "va6",
             "sourceOrgName": "{SOURCE_ORG}",
            "targetOrgName": "{TARGET_ORG}",
            "status": "APPROVED",
            "createdByName": "{CREATED_BY}",
            "modifiedByName": "{MODIFIED_BY}",
            "modifiedByIMSOrgId": "{MODIFIED_BY}",
            "statusHistory": "[{\"actionTakenBy\":\"{ACTION_BY}\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"INITIATED\",\"actionTimeStamp\":1724929442467,\"reason\":null},{\"actionTakenBy\":null,\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"APPROVED\",\"actionTimeStamp\":1724929617531,\"reason\":\"Done\"}]",
            "linkingId": "{LINKING_ID}"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

## Trasferisci pacchetti

Utilizza l&#39;endpoint `/transfer` nell&#39;API degli strumenti sandbox per recuperare e creare nuove richieste di condivisione dei pacchetti.

### Nuova richiesta di condivisione {#share-request}

Recupera il pacchetto di un&#39;organizzazione di origine pubblicata e condividilo con un&#39;organizzazione di destinazione effettuando una richiesta POST all&#39;endpoint `/transfer` e fornendo al contempo l&#39;ID del pacchetto e l&#39;ID dell&#39;organizzazione di destinazione.

**Formato API**

```http
POST /transfer
```

**Richiesta**

La richiesta seguente recupera un pacchetto di organizzazioni di origine e lo condivide con un’organizzazione di destinazione.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/transfer/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "packageId": "{PACKAGE_ID}",
      "targets": [
          {
              "imsOrgId": "{TARGET_IMS_ORG}"
          }
      ]
  }'
```

| Proprietà | Descrizione | Tipo | Obbligatorio |
| --- | --- | --- | --- |
| `packageId` | ID del pacchetto che desideri condividere. | Stringa | Sì |
| `targets` | Elenco di organizzazioni con cui condividere il pacchetto. | Array | Sì |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del pacchetto richiesto e il relativo stato di condivisione.

```json
[
    {
        "id": "{ID}",
        "version": 0,
        "createdDate": 1726480559313,
        "modifiedDate": 1726480559313,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceIMSOrgId": "{ORG_ID}",
        "targetIMSOrgId": "{TARGET_ID}",
        "packageId": "{PACKAGE_ID}",
        "status": "PENDING",
        "initiatedBy": "acme@3ec9197a65a86f34494221.e",
        "transferDetails": {
            "messages": [
                "Fetched Package",
                "Fetched Manifest"
            ],
            "additionalMetadata": null
        },
        "requestType": "PRIVATE"
    }
]
```

### Recuperare una richiesta di condivisione per ID {#fetch-transfer-by-id}

Recupera i dettagli di una richiesta di condivisione effettuando una richiesta GET all&#39;endpoint `/transfer/{TRANSFER_ID}` e fornendo l&#39;ID di trasferimento.

**Formato API**

```http
GET /transfer/{TRANSFER_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{TRANSFER_ID}` | ID del trasferimento che desideri recuperare. |

**Richiesta**

La richiesta seguente recupera un trasferimento con ID {TRANSFER_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/0c843180a64c445ca1beece339abc04b \
  -H 'x-api-key: {API__KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli di una richiesta di condivisione.

```json
{
    "id": "{ID}",
    "sourceIMSOrgId": "{ORG_ID}",
    "sourceOrgName": "{SOURCE_ORG}",
    "targetIMSOrgId": "{TARGET_ID}",
    "targetOrgName": "{TARGET_ORG}",
    "packageId": "{PACKAGE_ID}",
    "packageName": "{PACKAGE_NAME}",
    "status": "COMPLETED",
    "initiatedBy": "{INITIATED_BY}",
    "createdDate": 1724442856000,
    "transferDetails": {
        "messages": [
            "Fetched Package",
            "Fetched Manifest",
            "Tenant Identified",
            "Fetched Sandbox Id",
            "Fetched Blob Files",
            "Message Published to Kafka",
            "Completed Transfer"
        ],
        "additionalMetadata": null
    },
    "requestType": "PRIVATE"
}
```

### Recupera elenco condivisioni {#transfers-list}

Recupera un elenco di richieste di trasferimento effettuando una richiesta GET all&#39;endpoint `/transfer/list?{QUERY_PARAMETERS}`, modificando i parametri di query in base alle esigenze.

**Formato API**

```http
GET `/transfer/list?{QUERY_PARAMETERS}`
```

| Parametro | Valori accettati/predefiniti |
| --- | --- |
| `property` | Specifica la proprietà in base alla quale filtrare, ad esempio lo stato. I valori accettabili per lo stato sono: `COMPLETED`, `PENDING`, `IN_PROGRESS`, `FAILED`. |
| `start` | Il valore predefinito di inizio è `0`. |
| `limit` | Il valore predefinito del limite è `20`. |
| `orderBy` | L&#39;ordinamento accetta solo il campo `createdDate`. |

**Richiesta**

La richiesta seguente recupera un elenco di richieste di trasferimento dai parametri di ricerca forniti.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/list?property=status==COMPLETED&start=0&limit=2&orderBy=-createdDate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di tutte le richieste di trasferimento dai parametri di ricerca forniti.

```json
{
    "totalElements": 43,
    "currentPage": 0,
    "totalPages": 22,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_ORG}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "{PACKAGE_NAME}",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1726129077000,
            "createdDate": 1726129062000,
            "transferDetails": {
                "messages": [
                    "Fetched Package",
                    "Fetched Manifest",
                    "Tenant Identified",
                    "Fetched Sandbox Id",
                    "Fetched Blob Files",
                    "Message Published to Kafka",
                    "Completed Transfer",
                    "Finished with status: COMPLETED"
                ],
                "additionalMetadata": null
            },
            "requestType": "PRIVATE"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_ORG}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "{PACKAGE_NAME}",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1726066046000,
            "createdDate": 1726065936000,
            "transferDetails": {
                "messages": [
                    "Fetched Package",
                    "Fetched Manifest",
                    "Tenant Identified",
                    "Fetched Sandbox Id",
                    "Fetched Blob Files",
                    "Message Published to Kafka",
                    "Completed Transfer",
                    "Finished with status: COMPLETED"
                ],
                "additionalMetadata": null
            },
            "requestType": "PRIVATE"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

### Aggiornamento della disponibilità del pacchetto da privato a pubblico {#update-availability}

Modificare un pacchetto da privato a pubblico effettuando una richiesta GET all&#39;endpoint `/packages/update`. Per impostazione predefinita, viene creato un pacchetto con disponibilità privata.

**Formato API**

```http
GET `/packages/update`
```

**Richiesta**

La richiesta seguente modifica la disponibilità dei pacchetti da privato a pubblico.

```shell
curl -X GET \
  http://platform.adobe.io/data/foundation/exim/packages/update \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
      "id":"{ID}",
      "action":"UPDATE",
      "packageVisibility":"PUBLIC"
  }'
```

| Proprietà | Descrizione | Tipo | Obbligatorio |
| --- | --- | --- | --- |
| `id` | ID del pacchetto da aggiornare. | Stringa | Sì |
| `action` | Per aggiornare la visibilità al pubblico, il valore dell&#39;azione deve essere **UPDATE**. | Stringa | Sì |
| `packageVisbility` | Per aggiornare la visibilità, il valore packageVisibility deve essere **PUBLIC**. | Stringa | Sì |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli su un pacchetto e la relativa visibilità.

```json
{
    "id": "{ID}",
    "version": 7,
    "createdDate": 1729624618000,
    "modifiedDate": 1729658596340,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "name": "acme",
    "imsOrgId": "{ORG_ID}",
    "packageType": "PARTIAL",
    "expiry": 1737434596325,
    "status": "PUBLISH_FAILED",
    "packageVisibility": "PUBLIC",
    "artifactsList": [
        {
            "id": "{ID}",
            "type": "PROFILE_SEGMENT",
            "found": false,
            "count": 0,
            "title": "Acme Profile Segment"
        }
    ],
    "schemaMapping": {},
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    }
}
```

### Richiesta di importazione di un pacchetto pubblico {#pull-public-package}

Importa un pacchetto da un&#39;organizzazione di origine con disponibilità pubblica effettuando una richiesta POST all&#39;endpoint `/transfer/pullRequest`.

**Formato API**

```http
POST /transfer/pullRequest
```

**Richiesta**

La seguente richiesta importa un pacchetto e ne imposta la disponibilità su public.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/transfer/pullRequest \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "imsOrgId": "{ORG_ID}",
      "packageId": "{PACKAGE_ID}"
  }'
```

| Proprietà | Descrizione | Tipo | Obbligatorio |
| --- | --- | --- | --- |
| `imsOrgId` | L’ID dall’organizzazione di origine del pacchetto. | Stringa | Sì |
| `packageId` | ID del pacchetto da importare. | Stringa | Sì |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli sul pacchetto pubblico importato.

```json
{
    "id": "{ID}",
    "version": 0,
    "createdDate": 1729658890425,
    "modifiedDate": 1729658890425,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceIMSOrgId": "{ORG_ID}",
    "targetIMSOrgId": "{TARGET_ID}",
    "packageId": "{PACKAGE_ID}",
    "status": "PENDING",
    "initiatedBy": "{INITIATED_BY}",
    "pipelineMessageId": "{MESSAGE_ID}",
    "requestType": "PUBLIC"
}
```

### Elencare pacchetti pubblici {#list-public-packages}

Recupera un elenco di pacchetti con visibilità pubblica effettuando una richiesta GET all&#39;endpoint `/transfer/list?{QUERY_PARAMS}`.

**Formato API**

```http
GET /transfer/list?{QUERY_PARAMS}
```

| Parametro | Valori accettati/predefiniti |
| --- | --- |
| `property` | Specifica la proprietà in base alla quale filtrare, ad esempio lo stato. I valori accettabili per lo stato sono: `COMPLETED` e `FAILED`. |
| `start` | Il valore predefinito di inizio è `0`. |
| `limit` | Il valore predefinito del limite è `20`. |
| `orderBy` | L&#39;ordinamento accetta solo il campo `createdDate`. |
| `requestType` | Accetta `PUBLIC` o `PRIVATE`. |

**Richiesta**

La richiesta seguente recupera un elenco di pacchetti con disponibilità pubblica.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/list?property=status%3D%3DCOMPLETED%2CFAILED&requestType=PUBLIC&orderby=-createdDate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di pacchetti pubblici e i relativi dettagli.

+++Visualizza risposta

```json
{
    "totalElements": 14,
    "currentPage": 0,
    "totalPages": 1,
    "hasPreviousPage": false,
    "hasNextPage": false,
    "data": [
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public package demo",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729359318000,
            "createdDate": 1729359316000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public package demo",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729359284000,
            "createdDate": 1729359283000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Test Private Flow Final",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284462000,
            "createdDate": 1729275962000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOUCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Fest",
            "status": "FAILED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284104000,
            "createdDate": 1729253854000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284667000,
            "createdDate": 1729253421000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284957000,
            "createdDate": 1729253143000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284562000,
            "createdDate": 1729252975000,
            "requestType": "PUBLIC"
        },
        {
               "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Private Package Test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284262000,
            "createdDate": 1729229755000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Demo Package 1016",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284784000,
            "createdDate": 1729208888000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284934000,
            "createdDate": 1729153097000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284912000,
            "createdDate": 1729153043000,
            "requestType": "PUBLIC"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

+++

## Copia payload del pacchetto (#package-payload)

È possibile copiare il payload di un pacchetto pubblico effettuando una richiesta GET all&#39;endpoint `/packages/payload` che include l&#39;ID corrispondente del pacchetto nel percorso della richiesta.

**Formato API**

```http
GET /packages/payload/{PACKAGE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{PACKAGE_ID}` | ID del pacchetto da copiare. |

**Richiesta**

La richiesta seguente recupera il payload di un pacchetto con l&#39;ID di {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/payload/{PACKAGE_ID} \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "imsOrgId": "{ORG_ID}",
      "packageId": "{PACKAGE_ID}"
  }'
```

| Proprietà | Descrizione | Tipo | Obbligatorio |
| --- | --- | --- | --- |
| `imsOrdId` | ID dell’organizzazione a cui appartiene il pacchetto. | Stringa | Sì |
| `packageId` | ID del pacchetto di cui stai richiedendo il payload. | Stringa | Sì |

**Risposta**

In caso di esito positivo, la risposta restituisce il payload del pacchetto.

```json
{
    "imsOrgId": "{ORG_ID}",
    "packageId": "{PACKAGE_ID}"
}
```
