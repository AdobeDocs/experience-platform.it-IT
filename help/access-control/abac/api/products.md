---
keywords: Experience Platform;home;argomenti comuni;api;controllo degli accessi basato su attributi;controllo degli accessi basato su attributi
solution: Experience Platform
title: Endpoint API per i prodotti
description: L'endpoint /products nell'API di controllo accessi basato su attributi consente di gestire i prodotti in Adobe Experience Platform a livello di programmazione.
exl-id: 44ee9a9d-7a13-4d59-a1a9-97764dbd3763
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 4%

---

# Endpoint prodotti

>[!NOTE]
>
>Se viene passato un token utente, l’utente del token deve avere un ruolo di amministratore organizzazione per l’organizzazione richiesta.

La `/products` l’endpoint nell’API di controllo accessi basato su attributi consente di gestire in modo programmatico i prodotti, nonché le categorie di autorizzazioni e i set di autorizzazioni associati ai prodotti dell’organizzazione.

## Introduzione

L’endpoint API utilizzato in questa guida fa parte dell’API di controllo accessi basata sugli attributi. Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e importanti informazioni sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recupera un elenco di prodotti autorizzati {#list}

È possibile recuperare un elenco di prodotti autorizzati effettuando una richiesta di GET al `/products` punto finale.

**Formato API**

```http
GET /products/
```

**Richiesta**

La richiesta seguente recupera un elenco di prodotti autorizzati appartenenti all’organizzazione.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Risposta**

Una risposta corretta restituisce un elenco di prodotti autorizzati appartenenti all’organizzazione.

```json
{
  "products": [
    {
      "id": "{ID}",
      "name": "Adobe Experience Platform",
      "serviceCode": "{SERVICE_CODE}"
    }
  ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | L&#39;ID corrispondente del prodotto interrogato. |
| `name` | Nome del prodotto interrogato. |
| `serviceCode` | Il codice di servizio corrispondente del prodotto interrogato. |

## Cerca categorie di autorizzazioni per ID prodotto

Puoi cercare le categorie di autorizzazioni per un dato prodotto, effettuando una richiesta di GET al `/products/{PRODUCT_ID}/categories` endpoint durante la specifica dell&#39;ID prodotto.

**Formato API**

```http
GET /products/{PRODUCT_ID}/categories
```

| Parametro | Descrizione |
| --- | --- |
| {PRODUCT_ID} | ID del prodotto associato alle categorie di autorizzazioni che desideri cercare. |

**Richiesta**

La richiesta seguente recupera le categorie di autorizzazioni associate a `{PRODUCT_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/categories \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Risposta**

Una risposta corretta restituisce le categorie di autorizzazioni associate all&#39;ID prodotto interrogato.

```json
{
  "categories": [
    {
        "name": "Profile Management"
    },
    {
        "name": "Data Ingestion"
    },
    {
        "name": "Sandbox Administration"
    },
    {
        "name": "Query Service"
    },
    {
        "name": "Data Management"
    },
    {
        "name": "Identity Management"
    },
    {
        "name": "Data Modeling"
    },
    {
        "name": "Data Science Workspace"
    },
    {
        "name": "Dashboards"
    },
    {
        "name": "Alerts"
    },
    {
        "name": "Data Governance"
    }
  ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `category` | Le categorie di autorizzazioni disponibili all&#39;interno dell&#39;ID prodotto interrogato. |
| `name` | Nome della categoria di autorizzazioni. |

## Cerca i set di autorizzazioni per ID prodotto

Puoi cercare i set di autorizzazioni per un dato prodotto, effettuando una richiesta di GET al `/products/{PRODUCT_ID}/permission-sets` endpoint durante la specifica dell&#39;ID prodotto.

**Formato API**

```http
GET /products/{PRODUCT_ID}/permission-sets
```

| Parametro | Descrizione |
| --- | --- |
| {PRODUCT_ID} | ID del prodotto associato ai set di autorizzazioni da cercare. |

**Richiesta**

La richiesta seguente recupera i set di autorizzazioni associati a `{PRODUCT_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/permission-sets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Risposta**

Una risposta corretta restituisce i set di autorizzazioni associati all’ID prodotto interrogato.

```json
{
  "permission-sets": [
      {
          "id": "manage-schemas",
          "name": "Manage Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
      {
          "id": "view-schemas",
          "name": "View Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
  ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `permission-sets` | I set di autorizzazioni rappresentano un gruppo di autorizzazioni che un amministratore può assegnare a un ruolo. Un amministratore può assegnare set di autorizzazioni a un ruolo, anziché assegnare singole autorizzazioni. Ciò ti consente di creare ruoli personalizzati da un ruolo predefinito che contiene un gruppo di autorizzazioni. |
| `id` | L&#39;ID corrispondente del set di autorizzazioni interrogato. |
| `name` | Nome corrispondente del set di autorizzazioni interrogato. |
| `category` | La categoria di autorizzazioni disponibile. |
| `permissions` | Le autorizzazioni includono la possibilità di visualizzare e/o utilizzare le funzioni di Platform, ad esempio la creazione di sandbox, la definizione di schemi e la gestione dei set di dati. |
| `permissions.resource` | Risorsa o oggetto a cui un soggetto può o non può accedere. Le risorse possono essere file, applicazioni, server o anche API. |
| `permissions.actions` | Azione consentita a un oggetto in relazione a una risorsa interrogata. I valori possibili sono: `view`, `read`, `create`, `edit`e `delete` |
