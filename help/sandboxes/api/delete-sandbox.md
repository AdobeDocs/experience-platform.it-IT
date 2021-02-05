---
keywords: Experience Platform ;home;argomenti più comuni;eliminare sandbox
solution: Experience Platform
title: Eliminare una sandbox nell'API
topic: developer guide
description: Potete eliminare una sandbox effettuando una richiesta di DELETE che include il nome della sandbox nel percorso della richiesta.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 3%

---


# Eliminare una sandbox nell&#39;API

Potete eliminare una sandbox effettuando una richiesta di DELETE che include nel percorso della richiesta l&#39;elemento `name` della sandbox.

>[!NOTE]
>
>Facendo questa chiamata API, la proprietà `status` della sandbox viene aggiornata in &quot;eliminata&quot; e disattivata. Le richieste di GET possono ancora recuperare i dettagli della sandbox dopo che è stata eliminata.

**Formato API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La `name` della sandbox da eliminare. |

**Richiesta**

La richiesta seguente elimina una sandbox denominata &quot;dev-2&quot;.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli aggiornati della sandbox, indicando che la `state` è &quot;eliminata&quot;.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
