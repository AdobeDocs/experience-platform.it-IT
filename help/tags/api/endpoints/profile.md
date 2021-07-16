---
title: Endpoint profili
description: Scopri come effettuare chiamate all’endpoint /profiles nell’API Reactor.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 5%

---

# Endpoint profilo

Nell’API di Reactor, un profilo rappresenta un utente Adobe Experience Platform. L’API di Reactor non mantiene il proprio database di utenti e autorizzazioni, ma si basa sugli ID di Adobe gestiti da [IMS (Identity Management System)](https://helpx.adobe.com/it/enterprise/using/identity.html) di Adobe.

Un profilo contiene tutte le informazioni sull’utente connesso, comprese tutte le organizzazioni IMS a cui appartengono, i profili di prodotto a cui appartengono all’interno di ogni organizzazione e i diritti di cui dispongono da ciascun profilo di prodotto.

## Introduzione

L&#39;endpoint utilizzato in questa guida fa parte dell&#39; [API del reattore](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Prima di continuare, controlla la [guida introduttiva](../getting-started.md) per informazioni importanti su come eseguire l&#39;autenticazione nell&#39;API.

## Recupera il profilo corrente {#lookup}

Puoi recuperare i dettagli del profilo attualmente connesso effettuando una richiesta di GET all’endpoint `/profile` .

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
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

Una risposta corretta restituisce i dettagli del profilo.

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

