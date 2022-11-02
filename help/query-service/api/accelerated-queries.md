---
title: Endpoint query accelerate
description: Scopri come accedere all’archivio accelerato delle query in modo senza stato per restituire rapidamente i risultati in base ai dati aggregati. Questo documento fornisce un esempio di richiesta e risposta HTTP per l’endpoint query accelerate del servizio query.
source-git-commit: 2a9d40fc783feb78a1d5ad7eb615ceb40097eb89
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 1%

---

# Endpoint di query accelerate

Come parte della SKU di Data Distiller, la [API del servizio query](https://developer.adobe.com/experience-platform-apis/references/query-service/) consente di eseguire query senza stato nell’archivio accelerato. I risultati restituiti sono basati su dati aggregati. La minore latenza dei risultati consente uno scambio più interattivo di informazioni. Le API delle query accelerate vengono utilizzate anche per alimentare [dashboard definiti dall&#39;utente](../../dashboards/user-defined-dashboards.md).

Prima di continuare con questa guida, assicurati di aver letto e compreso il [Guida all’API del servizio query](./getting-started.md) per utilizzare correttamente l’API del servizio query.

## Introduzione

Lo SKU di Data Distiller è necessario per utilizzare l’archivio con accelerazione query. Vedi la [imballaggio](../packages.md), [guardrail](../guardrails.md#query-accelerated-store)e [licenza](../data-distiller/licence-usage.md) documentazione relativa allo SKU di Data Distiller. Se non disponi della SKU di Data Distiller, contatta il tuo rappresentante del servizio clienti Adobe per ulteriori informazioni.

Le sezioni seguenti descrivono le chiamate API necessarie per accedere all’archivio accelerato della query in modo senza stato tramite l’API del servizio query. Ciascuna chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

## Eseguire una query accelerata {#run-accelerated-query}

Effettuare una richiesta POST al `/accelerated-queries` per eseguire una query accelerata. La query è contenuta direttamente nel payload della richiesta o a cui viene fatto riferimento con un ID modello.

**Formato API**

```shell
POST /accelerated-queries
```

### Richiesta

>[!IMPORTANT]
>
>Richieste al `/accelerated-queries` L&#39;endpoint richiede un&#39;istruzione SQL O un ID modello, ma non entrambi. L’invio di entrambi in una richiesta causa un errore.

La seguente richiesta invia una query SQL nel corpo della richiesta all&#39;archivio accelerato.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/acceleated-queries
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

Questa richiesta alternativa invia un ID modello nel corpo della richiesta all&#39;archivio accelerato. L&#39;SQL del modello corrispondente viene utilizzato per eseguire una query sull&#39;archivio accelerato.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/acceleated-queries
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
| `dbName` | Nome del database a cui si sta effettuando una query accelerata. Valore per `dbName` devono assumere il formato di `{SANDBOX_NAME}:{ACCELERATED_STORE_DATABASE}.{ACCELERATED_STORE_SCHEMA}`. Il database fornito deve esistere all&#39;interno dell&#39;archivio accelerato o la richiesta darà luogo a un errore. È inoltre necessario assicurarsi che il `x-sandbox-name` nome dell’intestazione e della sandbox in `dbName` fare riferimento alla stessa sandbox. |
| `sql` | Una stringa di istruzione SQL. La dimensione massima consentita è di 100000 caratteri. |
| `templateId` | Identificatore univoco di una query creata e salvata come modello quando viene effettuata una richiesta di POST al `/templates` punto finale. |
| `name` | Nome descrittivo facoltativo per la query accelerata. |
| `description` | Un commento facoltativo sull’intento della query per aiutare altri utenti a comprenderne lo scopo. La dimensione massima consentita è di 1000 byte. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con lo schema ad hoc creato dalla query.

>[!NOTE]
>
>La risposta seguente è stata troncata per brevità.

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
| `resultsMeta` | Questo oggetto contiene i metadati per ogni colonna restituita nei risultati in modo che gli utenti conoscano il nome e il tipo di ciascuna colonna. |
| `resultsMeta._adhoc` | Schema XDM (Experience Data Model) ad hoc con campi con spazi dei nomi per l’utilizzo solo con un singolo set di dati. |
| `resultsMeta._adhoc.type` | Il tipo di dati dello schema ad hoc. |
| `resultsMeta._adhoc.meta:xdmType` | Si tratta di un valore generato dal sistema per il tipo di campo XDM. Per ulteriori informazioni sui tipi disponibili, consulta la documentazione su [tipi XDM disponibili](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/custom-fields-api.html). |
| `resultsMeta._adhoc.properties` | Si tratta dei nomi di colonna del set di dati interrogato. |
| `resultsMeta._adhoc.results` | Questi sono i nomi di riga del set di dati interrogato. Riflettono ciascuna delle colonne restituite. |

