---
keywords: Experience Platform;home;argomenti popolari;aggiornare sandbox
solution: Experience Platform
title: Aggiornare una sandbox nell’API
topic: guida per sviluppatori
description: Puoi aggiornare uno o più campi in una sandbox effettuando una richiesta di PATCH che include il nome della sandbox nel percorso della richiesta e la proprietà da aggiornare nel payload della richiesta.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 2%

---


# Aggiornare una sandbox nell’API

È possibile aggiornare uno o più campi in una sandbox effettuando una richiesta di PATCH che include il `name` della sandbox nel percorso della richiesta e la proprietà da aggiornare nel payload della richiesta.

>[!NOTE]
>
>Attualmente è possibile aggiornare solo la proprietà `title` di una sandbox.

**Formato API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La proprietà `name` della sandbox che desideri aggiornare. |

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

Una risposta corretta restituisce lo stato HTTP 200 (OK) con i dettagli della sandbox appena aggiornata.

```json
{
    "name": "dev-2",
    "title": "Development B",
    "state": "active",
    "type": "development",
    "region": "VA7"
}
```
