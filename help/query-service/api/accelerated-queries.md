---
title: Endpoint "Accelerated Queries"
description: Scopri come accedere alle query dell’archivio accelerato in modo stateless per restituire rapidamente risultati basati su dati aggregati. Questo documento fornisce un esempio di richiesta HTTP e di risposta per l’endpoint Query Service con query accelerate.
role: Developer
exl-id: 29ea4d25-9c46-4b29-a6d7-45ac33dcb0fb
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# Endpoint &quot;accelerated queries&quot;

Come parte dello SKU di Data Distiller, l&#39;[API servizio query](https://developer.adobe.com/experience-platform-apis/references/query-service/) consente di eseguire query senza stato nell&#39;archivio accelerato. I risultati restituiti si basano su dati aggregati. La latenza ridotta dei risultati consente uno scambio di informazioni più interattivo. Le API per query accelerate vengono utilizzate anche per alimentare [dashboard definiti dall&#39;utente](../../dashboards/standard-dashboards.md).

Prima di continuare con questa guida, assicurati di aver letto e compreso la [guida API di Query Service](./getting-started.md) per utilizzare correttamente l&#39;API di Query Service.

## Introduzione

Per utilizzare l’archivio con accelerazione delle query è necessario lo SKU di Data Distiller. Consulta la documentazione [package](../packaging.md) e [guardrail](../guardrails.md#query-accelerated-store) e [licensing](../data-distiller/license-usage.md) relativa allo SKU di Data Distiller. Se non disponi dello SKU di Data Distiller, contatta il rappresentante dell’assistenza clienti Adobe per ulteriori informazioni.

Le sezioni seguenti descrivono le chiamate API necessarie per accedere all’archivio accelerato delle query in modo senza stato tramite l’API Query Service. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

## Eseguire una query accelerata {#run-accelerated-query}

Eseguire una richiesta POST all&#39;endpoint `/accelerated-queries` per eseguire una query accelerata. La query è contenuta direttamente nel payload della richiesta oppure è referenziata con un ID modello.

**Formato API**

```shell
POST /accelerated-queries
```

### Richiesta

>[!IMPORTANT]
>
>Le richieste all&#39;endpoint `/accelerated-queries` richiedono un&#39;istruzione SQL OPPURE un ID modello, ma non entrambi. L’invio di entrambi in una richiesta causa un errore.

La richiesta seguente invia una query SQL nel corpo della richiesta all&#39;archivio accelerato.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/accelerated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "sql": "SELECT * FROM accounts;",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

Questa richiesta alternativa invia un ID modello nel corpo della richiesta all’archivio accelerato. L&#39;istruzione SQL del modello corrispondente viene utilizzata per eseguire una query sull&#39;archivio accelerato.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/accelerated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "templateId": "5d8228e7-4200-e3de-11e9-7f27416c5f0d",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

| Proprietà | Descrizione |
|---|---|
| `dbName` | Nome del database a cui si sta eseguendo una query accelerata. Il valore per `dbName` deve assumere il formato di `{SANDBOX_NAME}:{ACCELERATED_STORE_DATABASE}.{ACCELERATED_STORE_SCHEMA}`. Il database fornito deve esistere nell’archivio accelerato, altrimenti la richiesta genererà un errore. È inoltre necessario assicurarsi che l&#39;intestazione e il nome della sandbox `x-sandbox-name` in `dbName` facciano riferimento alla stessa sandbox. |
| `sql` | Stringa di istruzione SQL. La dimensione massima consentita è di 1000000 caratteri. |
| `templateId` | Identificatore univoco di una query creata e salvata come modello quando viene effettuata una richiesta POST all&#39;endpoint `/templates`. |
| `name` | Nome descrittivo facoltativo per la query accelerata. |
| `description` | Commento facoltativo sull’intento della query per aiutare altri utenti a comprenderne lo scopo. La dimensione massima consentita è 1000 byte. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con lo schema ad hoc creato dalla query.

>[!NOTE]
>
>La seguente risposta è stata troncata per brevità.

```json
{
  "queryId": "315a0a66-0fbb-4810-bc30-484cea5e0f1e",
  "resultsMeta": {
    "_adhoc": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
                "Units": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_name_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_code": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_name": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_aggregation_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Value": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Year": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_category": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_ANZSIC06": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                }
            }
        }
    },
  "results": [
     {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H26",
            "Variable_name": "Fixed tangible assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "282",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H27",
            "Variable_name": "Additions to fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "35",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H28",
            "Variable_name": "Disposals of fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "9",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        ...
    ],
  "request": {
    "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
    "sql": "SELECT * FROM accounts;",
    "name": "Sample Accelerated Query",
    "description": "A sample of an accelerated query."
  }
}
```

| Proprietà | Descrizione |
|---|---|
| `queryId` | Il valore ID della query creata. |
| `resultsMeta` | Questo oggetto contiene i metadati per ogni colonna restituita nei risultati, in modo che gli utenti possano conoscere il nome e il tipo di ogni colonna. |
| `resultsMeta._adhoc` | Schema ad hoc Experience Data Model (XDM) con campi denominati in modo che possano essere utilizzati solo da un singolo set di dati. |
| `resultsMeta._adhoc.type` | Il tipo di dati dello schema ad hoc. |
| `resultsMeta._adhoc.meta:xdmType` | Si tratta di un valore generato dal sistema per il tipo di campo XDM. Per ulteriori informazioni sui tipi disponibili, consulta la documentazione sui [tipi XDM disponibili](../../xdm/tutorials/custom-fields-api.md). |
| `resultsMeta._adhoc.properties` | Si tratta dei nomi delle colonne del set di dati sottoposto a query. |
| `resultsMeta._adhoc.results` | Questi sono i nomi delle righe del set di dati sottoposto a query. Riflettono ciascuna delle colonne restituite. |
