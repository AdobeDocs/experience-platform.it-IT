---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Reimpostare una sandbox
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 4%

---


# Reimpostare una sandbox

Le sandbox di sviluppo dispongono di una funzione di &quot;reimpostazione della fabbrica&quot; che elimina tutte le risorse non predefinite da una sandbox. Potete ripristinare una sandbox effettuando una richiesta di PUT che include la sandbox `name` nel percorso della richiesta.

**Formato API**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La `name` proprietà della sandbox da reimpostare. |

**Richiesta**

La richiesta seguente reimposta una sandbox denominata &quot;dev-2&quot;.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "action": "reset"
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `action` | Questo parametro deve essere fornito nel payload della richiesta con il valore &quot;reset&quot; per ripristinare la sandbox. |

**Risposta**

Una risposta corretta restituisce i dettagli della sandbox aggiornata, mostrando che `state` è &quot;resettata&quot;.

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
>Una volta ripristinata la sandbox, il provisioning da parte del sistema richiede circa 15 minuti. Una volta eseguito il provisioning, il sandbox `state` diventa &quot;attivo&quot; o &quot;non riuscito&quot;.