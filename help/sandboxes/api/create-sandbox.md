---
keywords: Experience Platform;home;argomenti popolari;Sandbox;sandbox
solution: Experience Platform
title: Creare una sandbox nell’API
topic-legacy: developer guide
description: Puoi creare una nuova sandbox effettuando una richiesta di POST all’endpoint `/sandbox`.
exl-id: 676c5de8-2c3a-4612-9dd8-93e01cafe90e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 2%

---

# Creare una sandbox nell’API

Puoi creare una nuova sandbox effettuando una richiesta POST all’endpoint `/sandboxes` .

**Formato API**

```http
POST /sandboxes
```

**Richiesta**

La seguente richiesta crea una nuova sandbox di sviluppo denominata &quot;dev-3&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Identificatore che verrà utilizzato per accedere alla sandbox nelle richieste future. Questo valore deve essere univoco e la best practice prevede di renderlo il più descrittivo possibile. Non può contenere spazi o lettere maiuscole. |
| `title` | Un nome leggibile dall’utente utilizzato a scopo di visualizzazione nell’interfaccia utente di Platform. |
| `type` | Tipo di sandbox da creare. Attualmente solo le sandbox di tipo &quot;sviluppo&quot; possono essere create da un’organizzazione. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova sandbox creata, indicando che la relativa `state` è &quot;creazione&quot;.

```json
{
    "name": "dev-3",
    "title": "Development 3",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>Il provisioning delle sandbox da parte del sistema richiede circa 15 minuti, dopodiché le `state` diventeranno &quot;attive&quot; o &quot;non riuscite&quot;.
