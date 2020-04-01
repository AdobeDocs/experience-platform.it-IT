---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Elimina una risorsa
topic: developer guide
translation-type: tm+mt
source-git-commit: d9ab2b1226b051be43f8fc0dd222bc075caed6f0

---


# Elimina una risorsa

Può essere talvolta necessario rimuovere (ELIMINARE) una risorsa dal Registro di sistema dello schema. È possibile eliminare solo le risorse create nel contenitore tenant. A questo scopo, è necessario eseguire una richiesta DELETE utilizzando l&#39; `$id` elemento della risorsa che si desidera eliminare.

**Formato API**

```http
DELETE /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{RESOURCE_TYPE}` | Il tipo di risorsa da eliminare dalla libreria Schema. I tipi validi sono `datatypes`, `mixins`, `schemas`e `classes`. |
| `{RESOURCE_ID}` | URI con codifica URL `$id` o `meta:altId` della risorsa. |

**Richiesta**

Le richieste DELETE non richiedono l’opzione Accetta intestazioni.

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

È possibile confermare l&#39;eliminazione provando una richiesta di ricerca (GET) alla risorsa. Sarà necessario includere un&#39;intestazione Accetto nella richiesta, ma dovrebbe ricevere uno stato HTTP 404 (Non trovato) perché la risorsa è stata rimossa dal Registro di sistema dello schema.