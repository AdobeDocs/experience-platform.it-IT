---
keywords: Experience Platform;home;argomenti popolari;reimpostare sandbox
solution: Experience Platform
title: Reimpostare una sandbox nell’API
topic: guida per sviluppatori
description: Le sandbox di sviluppo dispongono di una funzione di "reimpostazione di fabbrica" che elimina tutte le risorse non predefinite da una sandbox. Puoi reimpostare una sandbox effettuando una richiesta di PUT che include il nome della sandbox nel percorso della richiesta.
translation-type: tm+mt
source-git-commit: ca3de18c093d7b692b582045afea4401d7133b9b
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 3%

---


# Reimpostare una sandbox nell’API

Le sandbox di sviluppo dispongono di una funzione di &quot;reimpostazione di fabbrica&quot; che elimina tutte le risorse non predefinite da una sandbox. Puoi reimpostare una sandbox effettuando una richiesta di PUT che include il `name` della sandbox nel percorso della richiesta.

**Formato API**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La proprietà `name` della sandbox da reimpostare. |

**Richiesta**

La richiesta seguente reimposta una sandbox denominata &quot;dev-2&quot;.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "action": "reset"
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `action` | Questo parametro deve essere fornito nel payload della richiesta con un valore di &quot;reset&quot; per reimpostare la sandbox. |

**Risposta**

Una risposta corretta restituisce i dettagli della sandbox aggiornata, indicando che la relativa `state` è &quot;reimpostazione&quot;.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "dev-2",
    "title": "Development 2",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>Una volta reimpostata la sandbox, il sistema impiega circa 15 minuti per effettuare il provisioning. Una volta eseguito il provisioning, l’ `state` della sandbox diventa &quot;attivo&quot; o &quot;non riuscito&quot;.