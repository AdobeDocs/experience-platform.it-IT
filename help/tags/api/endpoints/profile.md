---
title: Endpoint “profiles”
description: Scopri come effettuare chiamate all’endpoint /profiles nell’API di Reactor.
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 97%

---

# Endpoint “profile”

Nell’API di Reactor, un profilo rappresenta un utente di Adobe Experience Platform. L’API di Reactor non mantiene il proprio database di utenti e autorizzazioni, ma si basa sugli Adobe ID gestiti da [Adobe IMS (Identity Management System)](https://helpx.adobe.com/it/enterprise/using/identity.html).

Un profilo contiene tutte le informazioni sull’utente connesso, comprese tutte le organizzazioni IMS a cui appartengono, i profili di prodotto a cui appartengono all’interno di ogni organizzazione e i diritti di cui dispongono da ciascun profilo di prodotto.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’[API di Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Prima di continuare, consulta la [guida introduttiva](../getting-started.md) per informazioni importanti su come eseguire l’autenticazione nell’API.

## Recuperare il profilo corrente {#lookup}

Per recuperare i dettagli del profilo attualmente connesso, effettua una richiesta GET all’endpoint `/profile`.

**Formato API**

```http
GET /profile
```

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del profilo.

```json
{
  "data": {
    "id": "UR0bd696624e844d6ba5bfc248ba1eca11",
    "type": "users",
    "attributes": {
      "active_org": "{IMS_ORG_1}",
      "expires_in": 0,
      "display_name": "John Smith",
      "job_function": null,
      "email": "jsmith@example.com",
      "organizations": {
        "{IMS_ORG_1}": {
          "name": "Example IMS Org A",
          "admin": true,
          "active": true,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_audiencemanager_int",
            "dma_tartan",
            "dma_dtm",
            "dma_reactor",
            "dma_auditor"
          ],
          "tenant_id": "{TENANT_ID_1}"
        },
        "{IMS_ORG_2}": {
          "name": "Example IMS Org B",
          "admin": false,
          "active": false,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_reactor",
            "dma_auditor",
            "dma_tartan"
          ],
          "tenant_id": "{TENANT_ID_2}"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/profile"
    },
    "meta": {
      "rights": [
        "manage_companies"
      ]
    }
  }
}
```

