---
keywords: Experience Platform;home;popular topics;update sandbox
solution: Experience Platform
title: Aggiornare una sandbox
topic: developer guide
description: Potete aggiornare uno o più campi in una sandbox effettuando una richiesta di PATCH che includa il nome della sandbox nel percorso della richiesta e la proprietà da aggiornare nel payload della richiesta.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 3%

---


# Aggiornare una sandbox

Potete aggiornare uno o più campi in una sandbox effettuando una richiesta di PATCH che includa la sandbox `name` nel percorso della richiesta e la proprietà da aggiornare nel payload della richiesta.

>[!NOTE]
>
>Al momento è possibile aggiornare solo la `title` proprietà di una sandbox.

**Formato API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La `name` proprietà della sandbox da aggiornare. |

**Richiesta**

La richiesta seguente aggiorna la `title` proprietà della sandbox denominata &quot;dev-2&quot;.

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
