---
title: Endpoint API per attributi calcolati
description: Scopri come creare, visualizzare, aggiornare ed eliminare gli attributi calcolati utilizzando l’API Profilo cliente in tempo reale.
exl-id: f217891c-574d-4a64-9d04-afc436cf16a9
source-git-commit: 49196473f304585193e87393f8dc5dc37be7e4d9
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 2%

---

# Endpoint API per attributi calcolati

>[!IMPORTANT]
>
>L’accesso all’API è limitato. Per informazioni su come ottenere l’accesso all’API degli attributi calcolati, contatta il supporto Adobe.

Gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento negli attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate in segmentazione, attivazione e personalizzazione. Questa guida include esempi di chiamate API per eseguire operazioni CRUD di base utilizzando l&#39;endpoint `/attributes`.

Per ulteriori informazioni sugli attributi calcolati, leggere la [panoramica sugli attributi calcolati](overview.md).

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39;[API del profilo cliente in tempo reale](https://www.adobe.com/go/profile-apis-en).

Prima di continuare, consulta la [Guida introduttiva all&#39;API del profilo](../api/getting-started.md) per i collegamenti alla documentazione consigliata, una guida alla lettura delle chiamate API di esempio visualizzate in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

Inoltre, consulta la documentazione del seguente servizio:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   - [Guida introduttiva al registro degli schemi](../../xdm/api/getting-started.md#know-your-tenant_id): vengono fornite informazioni su `{TENANT_ID}`, visualizzate nelle risposte in questa guida.

## Recuperare un elenco di attributi calcolati {#list}

Per recuperare un elenco di tutti gli attributi calcolati per l&#39;organizzazione, eseguire una richiesta GET all&#39;endpoint `/attributes`.

**Formato API**

L&#39;endpoint `/attributes` supporta diversi parametri di query per filtrare i risultati. Anche se questi parametri sono facoltativi, si consiglia vivamente di utilizzarli per ridurre i costi comuni quando si elencano le risorse. Se effettui una chiamata a questo endpoint senza parametri, verranno recuperati tutti gli attributi calcolati disponibili per la tua organizzazione. È possibile includere più parametri, separati da e commerciali (`&`).

```http
GET /attributes
GET /attributes?{QUERY_PARAMETERS}
```

I seguenti parametri di query possono essere utilizzati per recuperare un elenco di attributi calcolati:

| Parametro query | Descrizione | Esempio |
| --------------- | ----------- | ------- |
| `limit` | Un parametro che specifica il numero massimo di elementi restituiti come parte della risposta. Il valore minimo di questo parametro è 1 e il valore massimo è 40. Se questo parametro non è incluso, per impostazione predefinita verranno restituiti 20 elementi. | `limit=20` |
| `offset` | Un parametro che specifica il numero di elementi da ignorare prima di restituire gli elementi. | `offset=5` |
| `sortBy` | Parametro che specifica l&#39;ordine in cui vengono ordinati gli elementi restituiti. Le opzioni disponibili sono `name`, `status`, `updateEpoch` e `createEpoch`. È inoltre possibile scegliere se ordinare in ordine crescente o decrescente non includendo o includendo `-` prima dell&#39;opzione di ordinamento. Per impostazione predefinita, gli elementi verranno ordinati per `updateEpoch` in ordine decrescente. | `sortBy=name` |
| `property` | Parametro che consente di filtrare in base a vari campi attributo calcolati. Le proprietà supportate sono `name`, `createEpoch`, `mergeFunction.value`, `updateEpoch` e `status`. Le operazioni supportate dipendono dalla proprietà elencata. <ul><li>`name`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contains(), `NOT_CONTAINS` (=!contains())</li><li>`createEpoch`: `GREATER_THAN_OR_EQUALS` (&lt;=), `LESS_THAN_OR_EQUALS` (>=) </li><li>`mergeFunction.value`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contains(), `NOT_CONTAINS` (=!contains())</li><li>`updateEpoch`: `GREATER_THAN_OR_EQUALS` (&lt;=), `LESS_THAN_OR_EQUALS` (>=)</li><li>`status`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contains(), `NOT_CONTAINS` (=!contains())</li></ul> | `property=updateEpoch>=1683669114845`<br/>`property=name!=testingrelease`<br/>`property=status=contains(new,processing,disabled)` |

**Richiesta**

La richiesta seguente recupera gli ultimi tre attributi calcolati che sono stati aggiornati nell’organizzazione.

+++ Richiesta di esempio per recuperare un elenco di attributi calcolati.

```shell
curl -X GET https://platform.adobe.io/data/core/ca/attributes?limit=3 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco degli ultimi 3 attributi calcolati aggiornati che appartengono alla tua organizzazione e alla sandbox.

+++ Risposta di esempio per recuperare un elenco di attributi calcolati.

```json
{
    "_links": {
        "last": {
            "href": "/attributes?offset=3&limit=1"
        },
        "next": {
            "href": "/attributes?offset=20&limit=20"
        },
        "prev": {
            "href": "/attributes?offset=0&limit=20"
        },
        "self": {
            "href": "/attributes?offset=0&limit=20"
        }
    },
    "computedAttributes": [
        {
            "id": "2e3bf98c-5840-4eb5-98c9-fcd7bde82188",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses19",
            "displayName": "Multiple Filter Clauses 19",
            "description": "Multiple Filter Clauses 19",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": false,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223530322,
            "updateEpoch": 1673043640946,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "d9fbbd3d-049a-4561-b826-adc162511950",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses20",
            "displayName": "Multiple Filter Clauses 20",
            "description": "Multiple Filter Clauses 20",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": true,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[eventType.equals(\"commerce.backofficeOrderPlaced\", false)].topN(timestamp, 1).map({\"timestamp\": timestamp, \"value\": producedBy}).head()"
            },
            "mergeFunction": {
                "value": "MOST_RECENT"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223586455,
            "updateEpoch": 1671223586455,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "afedff07-9d15-4385-b181-49708229d73b",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses18",
            "displayName": "Multiple Filter Clauses 18",
            "description": "Multiple Filter Clauses 18",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "PROCESSED",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "2023-08-27T00:14:55.028",
            "createEpoch": 1671220358902,
            "updateEpoch": 1671220358902,
            "createdBy": "{USER_ID}"
        }
    ],
    "_page": {
        "offset": 0,
        "limit": 20,
        "count": 3,
        "totalCount": 3
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `_links` | Oggetto contenente le informazioni sull&#39;impaginazione necessarie per accedere all&#39;ultima pagina dei risultati, alla pagina successiva dei risultati, alla pagina precedente dei risultati o alla pagina corrente dei risultati. |
| `computedAttributes` | Matrice che contiene gli attributi calcolati in base ai parametri di query. Ulteriori informazioni sull&#39;array degli attributi calcolati sono disponibili nella sezione [recuperare un attributo calcolato specifico](#get). |
| `_page` | Oggetto contenente metadati sui risultati restituiti. Ciò include informazioni sull&#39;offset corrente, il conteggio degli attributi calcolati restituiti, il conteggio totale degli attributi calcolati e il limite degli attributi calcolati restituiti. |

+++

## Creare un attributo calcolato {#create}

Per creare un attributo calcolato, iniziare effettuando una richiesta POST all&#39;endpoint `/attributes` con un corpo della richiesta contenente i dettagli dell&#39;attributo calcolato che si desidera creare.

**Formato API**

```http
POST /attributes
```

**Richiesta**

+++ Richiesta di esempio per creare un nuovo attributo calcolato.

```shell
curl -X POST https://platform.adobe.io/data/core/ca/attributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "testing",
        "displayName": "Sample Display Name",
        "description": "Sample Description",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)].sum(commerce.order.priceTotal)"
        },
        "keepCurrent": false,
        "duration": {
            "count": 4,
            "unit": "DAYS"
        },
        "status": "DRAFT"
      }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Nome del campo attributo calcolato sotto forma di stringa. Il nome dell&#39;attributo calcolato può essere composto solo da caratteri alfanumerici senza spazi o trattini bassi. Questo valore **deve** essere univoco tra tutti gli attributi calcolati. Come best practice, questo nome deve essere una versione di camelCase di `displayName`. |
| `description` | Descrizione dell&#39;attributo calcolato. Questa funzione è particolarmente utile quando sono stati definiti più attributi calcolati, in quanto consente ad altri utenti all’interno dell’organizzazione di determinare l’attributo calcolato corretto da utilizzare. |
| `displayName` | Nome visualizzato dell&#39;attributo calcolato. Questo è il nome che verrà visualizzato quando vengono elencati gli attributi calcolati nell’interfaccia utente di Adobe Experience Platform. |
| `expression` | Oggetto che rappresenta l’espressione di query dell’attributo calcolato che stai tentando di creare. |
| `expression.type` | Tipo dell&#39;espressione. Attualmente, è supportato solo PQL. |
| `expression.format` | Il formato dell’espressione. Attualmente, è supportato solo `pql/text`. |
| `expression.value` | Il valore dell’espressione. |
| `keepCurrent` | Valore booleano che determina se il valore dell’attributo calcolato viene mantenuto aggiornato tramite l’aggiornamento rapido. Attualmente, questo valore deve essere impostato su `false`. |
| `duration` | Oggetto che rappresenta il periodo di lookback per l’attributo calcolato. Il periodo di lookback rappresenta il periodo di tempo trascorso il quale è possibile risalire per calcolare l’attributo calcolato. |
| `duration.count` | Numero che rappresenta la durata del periodo di lookback. I valori possibili dipendono dal valore del campo `duration.unit`. <ul><li>`HOURS`: 1-24</li><li>`DAYS`: 1-7</li><li>`WEEKS`: 1-4</li><li>`MONTHS`: 1-6</li></ul> |
| `duration.unit` | Stringa che rappresenta l’unità di tempo che verrà utilizzata per il periodo di lookback. I valori possibili includono: `HOURS`, `DAYS`, `WEEKS` e `MONTHS`. |
| `status` | Stato dell&#39;attributo calcolato. I valori possibili includono `DRAFT` e `NEW`. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni sull’attributo calcolato appena creato.

+++ Risposta di esempio durante la creazione di un nuovo attributo calcolato.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | ID generato dal sistema dell’attributo calcolato appena creato. |
| `status` | Stato dell&#39;attributo calcolato. Può essere `DRAFT` o `NEW`. |
| `createEpoch` | L’ora di creazione dell’attributo calcolato in secondi. |
| `updateEpoch` | Ora dell&#39;ultimo aggiornamento dell&#39;attributo calcolato, in secondi. |
| `createdBy` | ID dell’utente che ha creato l’attributo calcolato. |

+++

## Recuperare un attributo calcolato specifico {#get}

Per recuperare informazioni dettagliate su un attributo calcolato specifico, eseguire una richiesta GET all&#39;endpoint `/attributes` e fornire l&#39;ID dell&#39;attributo calcolato che si desidera recuperare nel percorso della richiesta.

**Formato API**

```http
GET /attributes/{ATTRIBUTE_ID}
```

**Richiesta**

+++ Richiesta di esempio per recuperare un attributo calcolato specifico.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni dettagliate sull’attributo calcolato specificato.

+++ Una risposta di esempio durante il recupero di un attributo calcolato specifico.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | ID univoco generato dal sistema e di sola lettura, che può essere utilizzato per fare riferimento all’attributo calcolato durante altre operazioni API. |
| `type` | Stringa che indica che l&#39;oggetto restituito è un attributo calcolato. |
| `name` | Nome dell&#39;attributo calcolato. |
| `displayName` | Nome visualizzato dell&#39;attributo calcolato. Questo è il nome che verrà visualizzato quando vengono elencati gli attributi calcolati nell’interfaccia utente di Adobe Experience Platform. |
| `description` | Descrizione dell&#39;attributo calcolato. Questa funzione è particolarmente utile quando sono stati definiti più attributi calcolati, in quanto consente ad altri utenti all’interno dell’organizzazione di determinare l’attributo calcolato corretto da utilizzare. |
| `imsOrgId` | ID dell’organizzazione a cui appartiene l’attributo calcolato. |
| `sandbox` | L’oggetto sandbox contiene i dettagli della sandbox in cui è stato configurato l’attributo calcolato. Queste informazioni sono tratte dall’intestazione sandbox inviata nella richiesta. Per ulteriori informazioni, consulta la [panoramica delle sandbox](../../sandboxes/home.md). |
| `path` | `path` all&#39;attributo calcolato. |
| `keepCurrent` | Valore booleano che determina se il valore dell’attributo calcolato viene mantenuto aggiornato tramite l’aggiornamento rapido. |
| `expression` | Oggetto contenente l&#39;espressione dell&#39;attributo calcolato. |
| `mergeFunction` | Oggetto contenente la funzione di unione per l’attributo calcolato. Questo valore è basato sul parametro di aggregazione corrispondente all&#39;interno dell&#39;espressione dell&#39;attributo calcolato. I valori possibili sono `SUM`, `MIN`, `MAX` e `MOST_RECENT`. |
| `status` | Stato dell&#39;attributo calcolato. Può essere uno dei valori seguenti: `DRAFT`, `NEW`, `INITIALIZING`, `PROCESSING`, `PROCESSED`, `FAILED` o `DISABLED`. |
| `schema` | Oggetto che contiene informazioni sullo schema in cui viene valutata l’espressione. Attualmente, è supportato solo `_xdm.context.profile`. |
| `lastEvaluationTs` | Timestamp che rappresenta l’ultima valutazione dell’attributo calcolato. |
| `createEpoch` | L’ora di creazione dell’attributo calcolato in secondi. |
| `updateEpoch` | Ora dell&#39;ultimo aggiornamento dell&#39;attributo calcolato, in secondi. |
| `createdBy` | ID dell’utente che ha creato l’attributo calcolato. |

+++

## Eliminare un attributo calcolato specifico {#delete}

È possibile eliminare un attributo calcolato specifico effettuando una richiesta DELETE all&#39;endpoint `/attributes` e fornendo l&#39;ID dell&#39;attributo calcolato che si desidera eliminare nel percorso della richiesta.

>[!IMPORTANT]
>
>La richiesta di eliminazione può essere utilizzata solo per eliminare attributi calcolati con stato **bozza** (`DRAFT`). Questo endpoint **non può** essere utilizzato per eliminare attributi calcolati in qualsiasi altro stato.

**Formato API**

```http
DELETE /attributes/{ATTRIBUTE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | Il valore `id` dell&#39;attributo calcolato che si desidera eliminare. |

**Richiesta**

+++ Richiesta di esempio per eliminare un attributo calcolato.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 con i dettagli dell’attributo calcolato eliminato.

+++ Una risposta di esempio durante l’eliminazione di un attributo calcolato.

```json
{
    "id": "03ae581b-5f7b-48da-a9eb-4ef0daf4bc3c",
    "type": "ComputedAttribute",
    "name": "testdemopd2",
    "displayName": "testdemopd2",
    "description": "testdemopd2",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.shipping.shipDate occurs <= 1 days before now) and (timestamp occurs <= 1 days before now)].min(commerce.shipping.shipDate)"
    },
    "mergeFunction": {
        "value": "MIN"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1681365690928,
    "updateEpoch": 1681365690928,
    "createdBy": "{USER_ID}"
}
```

+++

## Aggiornare un attributo calcolato specifico

È possibile aggiornare un attributo calcolato specifico effettuando una richiesta PATCH all&#39;endpoint `/attributes` e fornendo l&#39;ID dell&#39;attributo calcolato che si desidera aggiornare nel percorso della richiesta.

>[!IMPORTANT]
>
>Quando si aggiorna un attributo calcolato, è possibile aggiornare solo i campi seguenti:
>
>- Se lo stato corrente è `NEW`, lo stato può essere modificato solo in `DISABLED`.
>- Se lo stato corrente è `DRAFT`, è possibile modificare i valori dei campi seguenti: `name`, `description`, `keepCurrent`, `expression` e `duration`. È inoltre possibile modificare lo stato da `DRAFT` a `NEW`. Qualsiasi modifica ai campi generati dal sistema, ad esempio `mergeFunction` o `path`, restituirà un errore.
>- Se lo stato corrente è `PROCESSING` o `PROCESSED`, lo stato può essere modificato solo in `DISABLED`.

**Formato API**

```http
PATCH /attributes/{ATTRIBUTE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | Il valore `id` dell&#39;attributo calcolato che si desidera aggiornare. |

**Richiesta**

La richiesta seguente aggiornerà lo stato dell&#39;attributo calcolato da `DRAFT` a `NEW`.

+++ Richiesta di esempio per aggiornare un attributo calcolato.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "description": "Sample Description",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "status": "NEW"
 }'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni sull’attributo calcolato appena aggiornato.

+++ Una risposta di esempio durante l’aggiornamento di un attributo calcolato.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing123",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "NEW",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680071726825,
    "updateEpoch": 1680074429192,
    "createdBy": "{USER_ID}"
}
```

+++

## Passaggi successivi

Ora che hai imparato le nozioni di base sugli attributi calcolati, puoi iniziare a definirli per la tua organizzazione. Per informazioni sull&#39;utilizzo degli attributi calcolati nell&#39;interfaccia utente di Experience Platform, leggere la [guida dell&#39;interfaccia utente degli attributi calcolati](./ui.md).
