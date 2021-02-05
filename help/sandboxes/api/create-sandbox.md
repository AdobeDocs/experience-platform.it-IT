---
keywords: ' Experience Platform;home;argomenti popolari;Sandbox;sandbox'
solution: Experience Platform
title: Creare una sandbox nell'API
topic: developer guide
description: Potete creare una nuova sandbox effettuando una richiesta di POST all'endpoint `/sandbox`.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 2%

---


# Creare una sandbox nell&#39;API

Potete creare una nuova sandbox effettuando una richiesta di POST all&#39;endpoint `/sandboxes`.

**Formato API**

```http
POST /sandboxes
```

**Richiesta**

La richiesta seguente crea una nuova sandbox di sviluppo denominata &quot;dev-3&quot;.

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
| `name` | Identificatore che verrà utilizzato per accedere alla sandbox nelle richieste future. Questo valore deve essere univoco e la best practice consiste nel renderlo il più descrittivo possibile. Non può contenere spazi o lettere maiuscole. |
| `title` | Un nome leggibile dall&#39;uomo utilizzato per la visualizzazione nell&#39;interfaccia utente della piattaforma. |
| `type` | Il tipo di sandbox da creare. Attualmente solo le sandbox di tipo &quot;development&quot; possono essere create da un&#39;organizzazione. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova sandbox creata, mostrando che la relativa `state` è &quot;creazione&quot;.

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
>Il provisioning delle sandbox richiede circa 15 minuti dal sistema, dopo di che il loro `state` diventerà &quot;attivo&quot; o &quot;non riuscito&quot;.
