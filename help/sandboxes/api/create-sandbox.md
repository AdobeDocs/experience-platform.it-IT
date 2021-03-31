---
keywords: Experience Platform;home;argomenti popolari;Sandbox;sandbox
solution: Experience Platform
title: Creare una sandbox nell’API
topic: guida per sviluppatori
description: Puoi creare una nuova sandbox effettuando una richiesta di POST all’endpoint `/sandbox`.
translation-type: tm+mt
source-git-commit: ee2fb54ba59f22a1ace56a6afd78277baba5271e
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 2%

---


# Creare una sandbox nell’API

Puoi creare una sandbox di sviluppo o produzione effettuando una richiesta POST all’endpoint `/sandboxes` .

## Creare una sandbox di sviluppo

Per creare una sandbox di sviluppo, invia una richiesta POST all’endpoint `/sandboxes` e fornisci il valore `development` per la proprietà `type`.

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
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Identificatore che verrà utilizzato per accedere alla sandbox nelle richieste future. Questo valore deve essere univoco e la best practice prevede di renderlo il più descrittivo possibile. Questo valore non può contenere spazi o caratteri speciali. |
| `title` | Un nome leggibile dall’utente utilizzato a scopo di visualizzazione nell’interfaccia utente di Platform. |
| `type` | Tipo di sandbox da creare. Il valore della proprietà `type` può essere di sviluppo o di produzione. |

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

## Creare una sandbox di produzione

>[!NOTE]
>
>La funzione Sandbox di produzione multipla è in versione beta.

Per creare una sandbox di produzione, invia una richiesta POST all’endpoint `/sandboxes` e fornisci il valore `production` per la proprietà `type`.

**Formato API**

```http
POST /sandboxes
```

**Richiesta**

La seguente richiesta crea una nuova sandbox di produzione denominata &quot;test-prod-sandbox&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "test-prod-sandbox",
    "title": "Test Production Sandbox",
    "type": "production"
}'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Identificatore che verrà utilizzato per accedere alla sandbox nelle richieste future. Questo valore deve essere univoco e la best practice prevede di renderlo il più descrittivo possibile. Questo valore non può contenere spazi o caratteri speciali. |
| `title` | Un nome leggibile dall’utente utilizzato a scopo di visualizzazione nell’interfaccia utente di Platform. |
| `type` | Tipo di sandbox da creare. Il valore della proprietà `type` può essere di sviluppo o di produzione. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova sandbox creata, indicando che la relativa `state` è &quot;creazione&quot;.

```json
{
    "name": "test-production-sandbox",
    "title": "Test Production Sandbox",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```
