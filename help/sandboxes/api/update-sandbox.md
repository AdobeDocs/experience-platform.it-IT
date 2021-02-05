---
keywords: ' Experience Platform;home;argomenti popolari;aggiornare la sandbox'
solution: Experience Platform
title: Aggiornare una sandbox nell'API
topic: developer guide
description: Potete aggiornare uno o più campi in una sandbox effettuando una richiesta di PATCH che includa il nome della sandbox nel percorso della richiesta e la proprietà da aggiornare nel payload della richiesta.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---


# Aggiornare una sandbox nell&#39;API

Potete aggiornare uno o più campi in una sandbox effettuando una richiesta di PATCH che includa la `name` sandbox nel percorso della richiesta e la proprietà da aggiornare nel payload della richiesta.

>[!NOTE]
>
>Al momento è possibile aggiornare solo la proprietà `title` di una sandbox.

**Formato API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La proprietà `name` della sandbox da aggiornare. |

**Richiesta**

La richiesta seguente aggiorna la proprietà `title` della sandbox denominata &quot;dev-2&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "title": "Development B"
  }'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 (OK) con i dettagli della nuova sandbox aggiornata.

```json
{
    "name": "dev-2",
    "title": "Development B",
    "state": "active",
    "type": "development",
    "region": "VA7"
}
```
