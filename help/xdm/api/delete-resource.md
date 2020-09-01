---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;delete
solution: Experience Platform
title: Elimina una risorsa
describe: It may occasionally be necessary to remove resource from the Schema Registry. Only resources that you create in the tenant container may be deleted. This is done by performing a DELETE request using the $id of the resource you wish to delete.
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 7%

---


# Elimina una risorsa

Può essere talvolta necessario rimuovere (DELETE) una risorsa dal [!DNL Schema Registry]. È possibile eliminare solo le risorse create nel contenitore tenant. Questa operazione viene eseguita eseguendo una richiesta DELETE utilizzando l&#39; `$id` elemento della risorsa che si desidera eliminare.

**Formato API**

```http
DELETE /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{RESOURCE_TYPE}` | Il tipo di risorsa da eliminare dal [!DNL Schema Library]. I tipi validi sono `datatypes`, `mixins`, `schemas`e `classes`. |
| `{RESOURCE_ID}` | URI con codifica URL `$id` o `meta:altId` della risorsa. |

**Richiesta**

Le richieste di DELETE non richiedono l&#39;opzione Accetta intestazioni.

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fmixins%2F4fbd5368aa67f0e74d5838f67694c867 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto.

È possibile confermare l&#39;eliminazione provando una richiesta di ricerca (GET) alla risorsa. Dovrete includere un&#39;intestazione Accetto nella richiesta, ma dovreste ricevere uno stato HTTP 404 (Non trovato) perché la risorsa è stata rimossa dal [!DNL Schema Registry].