---
keywords: Experience Platform;home;argomenti popolari;eliminare sandbox
solution: Experience Platform
title: Eliminare una sandbox nell’API
topic: guida per sviluppatori
description: Puoi eliminare una sandbox effettuando una richiesta di DELETE che include il nome della sandbox nel percorso della richiesta.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 3%

---


# Eliminare una sandbox nell’API

È possibile eliminare una sandbox effettuando una richiesta di DELETE che include nel percorso della richiesta la versione `name` della sandbox.

>[!NOTE]
>
>L’esecuzione di questa chiamata API aggiorna la proprietà della sandbox `status` su &quot;eliminata&quot; e la disattiva. Le richieste GET possono ancora recuperare i dettagli della sandbox dopo che è stata eliminata.

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

Una risposta corretta restituisce i dettagli aggiornati della sandbox, indicando che la relativa `state` è &quot;eliminata&quot;.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
