---
keywords: Experience Platform;home;argomenti popolari;trovare sandbox;cercare una sandbox
solution: Experience Platform
title: Cercare una sandbox nell’API
topic-legacy: developer guide
description: Puoi cercare una singola sandbox effettuando una richiesta GET che include la proprietà name della sandbox nel percorso della richiesta.
exl-id: de8d965c-ca58-436e-b5b1-05a492de70f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 2%

---

# Cercare una sandbox nell’API

Puoi cercare un singolo sandbox effettuando una richiesta GET che include la proprietà `name` della sandbox nel percorso della richiesta.

**Formato API**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La proprietà `name` della sandbox che desideri cercare. |

**Richiesta**

La richiesta seguente recupera una sandbox denominata &quot;dev-2&quot;.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli della sandbox, inclusi i relativi `name`, `title`, `state` e `type`.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "creating",
    "type": "development",
    "region": "VA7",
    "isDefault": false,
    "eTag": 1,
    "createdDate": "2019-09-07 10:16:02",
    "lastModifiedDate": "2019-09-07 10:16:02",
    "createdBy": "{USER_ID}",
    "modifiedBy": "{USER_ID}"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della sandbox. Utilizzato a scopo di ricerca nelle chiamate API. |
| `title` | Nome visualizzato della sandbox. |
| `state` | Lo stato di elaborazione corrente della sandbox. Lo stato di una sandbox può essere uno dei seguenti: <ul><li>**creazione**: La sandbox è stata creata, ma viene comunque fornita dal sistema.</li><li>**attivo**: La sandbox viene creata e attiva.</li><li>**non riuscito**: A causa di un errore, il sistema non è in grado di eseguire il provisioning della sandbox ed è disabilitato.</li><li>**eliminato**: La sandbox è stata disabilitata manualmente.</li></ul> |
| `type` | Il tipo di sandbox, &quot;sviluppo&quot; o &quot;produzione&quot;. |
| `isDefault` | Proprietà booleana che indica se questa sandbox è la sandbox predefinita per l’organizzazione. In genere si tratta della sandbox di produzione. |
| `eTag` | Identificatore per una versione specifica della sandbox. Utilizzato per il controllo delle versioni e l’efficienza del caching, questo valore viene aggiornato ogni volta che viene apportata una modifica alla sandbox. |
