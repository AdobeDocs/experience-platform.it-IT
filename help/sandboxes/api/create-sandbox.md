---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare una sandbox
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 2%

---


# Creare una sandbox

Potete creare una nuova sandbox effettuando una richiesta di POST all’ `/sandboxes` endpoint.

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
| `title` | Un nome leggibile da un utente utilizzato per la visualizzazione nell&#39;interfaccia utente di Platform. |
| `type` | Il tipo di sandbox da creare. Attualmente solo le sandbox di tipo &quot;development&quot; possono essere create da un&#39;organizzazione. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova sandbox creata, mostrando che `state` è &quot;in fase di creazione&quot;.

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
>Le sandbox impiegano circa 15 minuti per essere fornite dal sistema, dopo di che `state` diventeranno &quot;attive&quot; o &quot;fallite&quot;.
