---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Eliminare una sandbox
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 4%

---


# Eliminare una sandbox

Potete eliminare una sandbox effettuando una richiesta di DELETE che include la sandbox `name` nel percorso della richiesta.

>[!NOTE]
>
>Facendo questa chiamata API, la proprietà della `status` sandbox viene aggiornata in &quot;eliminata&quot; e disattivata. Le richieste di GET possono ancora recuperare i dettagli della sandbox dopo che è stata eliminata.

**Formato API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | Indica `name` la sandbox da eliminare. |

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

Una risposta corretta restituisce i dettagli aggiornati della sandbox, indicando che `state` è &quot;eliminata&quot;.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
