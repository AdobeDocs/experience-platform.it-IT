---
keywords: Experience Platform;home;argomenti popolari;api;Attribute-Based Access Control;attribute-based access control
solution: Experience Platform
title: Endpoint API prodotti
description: L’endpoint /products nell’API di controllo dell’accesso basato su attributi consente di gestire in modo programmatico i prodotti in Adobe Experience Platform.
role: Developer
exl-id: 44ee9a9d-7a13-4d59-a1a9-97764dbd3763
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 4%

---

# Endpoint prodotti

>[!NOTE]
>
>Se viene passato un token utente, l’utente del token deve avere un ruolo &quot;amministratore organizzazione&quot; per l’organizzazione richiesta.

Il `/products` L’endpoint nell’API di controllo degli accessi basata su attributi consente di gestire in modo programmatico prodotti, categorie di autorizzazioni e set di autorizzazioni associati ai prodotti dell’organizzazione.

## Introduzione

L’endpoint API utilizzato in questa guida fa parte dell’API di controllo degli accessi basata su attributi. Prima di continuare, controlla [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida per la lettura delle chiamate API di esempio di questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experienci Platform.

## Recuperare un elenco di prodotti autorizzati {#list}

Per recuperare un elenco di prodotti autorizzati, devi effettuare una richiesta GET al `/products` endpoint.

**Formato API**

```http
GET /products/
```

**Richiesta**

La richiesta seguente recupera un elenco di prodotti autorizzati appartenenti alla tua organizzazione.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di prodotti autorizzati appartenenti alla tua organizzazione.

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
| `id` | ID corrispondente del prodotto oggetto di query. |
| `name` | Nome del prodotto oggetto della query. |
| `serviceCode` | Il codice del servizio corrispondente del prodotto oggetto della query. |

## Cercare categorie di autorizzazioni per ID prodotto

Per cercare le categorie di autorizzazione per un determinato prodotto, devi effettuare una richiesta GET al `/products/{PRODUCT_ID}/categories` endpoint durante la specifica dell&#39;ID prodotto.

**Formato API**

```http
GET /products/{PRODUCT_ID}/categories
```

| Parametro | Descrizione |
| --- | --- |
| {PRODUCT_ID} | ID del prodotto associato alle categorie di autorizzazioni che desideri cercare. |

**Richiesta**

La richiesta seguente recupera le categorie di autorizzazione associate a `{PRODUCT_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/categories \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce le categorie di autorizzazione associate all’ID prodotto oggetto della query.

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
| `category` | Le categorie di autorizzazione disponibili all’interno dell’ID prodotto oggetto della query. |
| `name` | Nome della categoria di autorizzazioni. |

## Cercare i set di autorizzazioni per ID prodotto

Per cercare i set di autorizzazioni per un determinato prodotto, devi effettuare una richiesta GET al `/products/{PRODUCT_ID}/permission-sets` endpoint durante la specifica dell&#39;ID prodotto.

**Formato API**

```http
GET /products/{PRODUCT_ID}/permission-sets
```

| Parametro | Descrizione |
| --- | --- |
| {PRODUCT_ID} | ID del prodotto associato ai set di autorizzazioni che desideri cercare. |

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

In caso di esito positivo, la risposta restituisce i set di autorizzazioni associati all’ID prodotto oggetto della query.

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
| `permission-sets` | I set di autorizzazioni rappresentano un gruppo di autorizzazioni che un amministratore può applicare a un ruolo. Un amministratore può assegnare set di autorizzazioni a un ruolo, invece di assegnare singole autorizzazioni. In questo modo è possibile creare ruoli personalizzati da un ruolo predefinito contenente un gruppo di autorizzazioni. |
| `id` | ID corrispondente del set di autorizzazioni sottoposto a query. |
| `name` | Nome corrispondente del set di autorizzazioni sottoposto a query. |
| `category` | La categoria di autorizzazioni disponibile. |
| `permissions` | Le autorizzazioni includono la possibilità di visualizzare e/o utilizzare le funzioni di Platform, ad esempio la creazione di sandbox, la definizione di schemi e la gestione di set di dati. |
| `permissions.resource` | La risorsa o l&#39;oggetto a cui un soggetto può o non può accedere. Le risorse possono essere file, applicazioni, server o anche API. |
| `permissions.actions` | Azione consentita a un oggetto per una risorsa su cui è stata eseguita una query. I valori possibili includono: `view`, `read`, `create`, `edit`, e `delete` |
