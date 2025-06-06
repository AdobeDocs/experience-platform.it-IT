---
keywords: Experience Platform;home;argomenti popolari;api;Attribute-Based Access Control;attribute-based access control;attribute-based access control
solution: Experience Platform
title: Endpoint API per i ruoli
description: L’endpoint /roles nell’API di controllo dell’accesso basata su attributi consente di gestire in modo programmatico i ruoli in Adobe Experience Platform.
role: Developer
exl-id: 049f7a18-7d06-437b-8ce9-25d7090ba782
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 7%

---

# Endpoint &quot;Roles&quot;

>[!NOTE]
>
>Se viene passato un token utente, l’utente del token deve avere un ruolo &quot;amministratore organizzazione&quot; per l’organizzazione richiesta.

I ruoli definiscono l’accesso di un amministratore, uno specialista o un utente finale alle risorse della tua organizzazione. In un ambiente di controllo degli accessi basato su ruoli, il provisioning degli accessi utente è raggruppato in base a responsabilità e esigenze comuni. Un ruolo dispone di un determinato set di autorizzazioni e i membri dell’organizzazione possono essere assegnati a uno o più ruoli, a seconda dell’ambito di accesso di visualizzazione o scrittura necessario.

L&#39;endpoint `/roles` nell&#39;API di controllo degli accessi basata su attributi consente di gestire in modo programmatico i ruoli dell&#39;organizzazione.

## Introduzione

L’endpoint API utilizzato in questa guida fa parte dell’API di controllo degli accessi basata su attributi. Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e per le informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recuperare un elenco di ruoli {#list}

Per elencare tutti i ruoli esistenti appartenenti alla tua organizzazione, devi eseguire una richiesta GET all&#39;endpoint `/roles`.

**Formato API**

```http
GET /roles/
```

**Richiesta**

La richiesta seguente recupera un elenco di ruoli appartenenti alla tua organizzazione.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di ruoli dell’organizzazione, incluse informazioni sul rispettivo tipo di ruolo, sui set di autorizzazioni e sugli attributi dell’oggetto.

```json
{
  "roles": [
    {
      "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "name": "Administrator Role",
      "description": "Role for administrator type of responsibilities and access",
      "roleType": "user-defined",
      "permissionSets": [
        "manage-datasets",
        "manage-schemas"
      ],
      "sandboxes": [
        "prod"
      ],
      "subjectAttributes": {
        "labels": [
          "core/S1"
        ]
      },
      "createdBy": "{CREATED_BY}",
      "createdAt": 1648153201825,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1648153201825,
      "etag": null
    }
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "next": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "subjects": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    }
  }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID corrispondente al ruolo. Questo ID viene generato automaticamente. |
| `name` | Il nome del ruolo. |
| `description` | La proprietà description fornisce informazioni aggiuntive sul ruolo. |
| `roleType` | Il tipo designato del ruolo. I valori possibili per il tipo di ruolo sono: `user-defined` e `system-defined`. |
| `permissionSets` | I set di autorizzazioni rappresentano un gruppo di autorizzazioni che un amministratore può applicare a un ruolo. Un amministratore può assegnare set di autorizzazioni a un ruolo, invece di assegnare singole autorizzazioni. In questo modo è possibile creare ruoli personalizzati da un ruolo predefinito contenente un gruppo di autorizzazioni. |
| `sandboxes` | Questa proprietà visualizza all’interno dell’organizzazione le sandbox per le quali è stato eseguito il provisioning per un determinato ruolo. |
| `subjectAttributes` | Attributi che indicano la correlazione tra un soggetto e le risorse Experience Platform a cui hanno accesso. |
| `subjectAttributes.labels` | Visualizza le etichette di utilizzo dei dati applicate al ruolo sottoposto a query. |

## Cercare un ruolo {#lookup}

Per cercare un singolo ruolo, devi eseguire una richiesta GET che includa il `roleId` corrispondente nel percorso della richiesta.

**Formato API**

```http
GET /roles/{ROLE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| {ROLE_ID} | ID del ruolo che si desidera cercare. |

**Richiesta**

La richiesta seguente recupera informazioni per `{ROLE_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli per l’ID ruolo interrogato, incluse informazioni sul tipo di ruolo, sui set di autorizzazioni e sugli attributi dell’oggetto.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID corrispondente al ruolo. Questo ID viene generato automaticamente. |
| `name` | Il nome del ruolo. |
| `description` | La proprietà description fornisce informazioni aggiuntive sul ruolo. |
| `roleType` | Il tipo designato del ruolo. I valori possibili per il tipo di ruolo sono: `user-defined` e `system-defined`. |
| `permissionSets` | I set di autorizzazioni rappresentano un gruppo di autorizzazioni che un amministratore può applicare a un ruolo. Un amministratore può assegnare set di autorizzazioni a un ruolo, invece di assegnare singole autorizzazioni. In questo modo è possibile creare ruoli personalizzati da un ruolo predefinito contenente un gruppo di autorizzazioni. |
| `sandboxes` | Questa proprietà visualizza all’interno dell’organizzazione le sandbox per le quali è stato eseguito il provisioning per un determinato ruolo. |
| `subjectAttributes` | Attributi che indicano la correlazione tra un soggetto e le risorse Experience Platform a cui hanno accesso. |
| `subjectAttributes.labels` | Visualizza le etichette di utilizzo dei dati applicate al ruolo sottoposto a query. |

## Cerca soggetti per ID ruolo

È inoltre possibile recuperare gli oggetti effettuando una richiesta GET all&#39;endpoint `/roles` e fornendo un {ROLE_ID}.

**Formato API**

```http
GET /roles/{ROLE_ID}/subjects
```

| Parametro | Descrizione |
| --- | --- |
| {ROLE_ID} | ID del ruolo associato ai soggetti che si desidera cercare. |

**Richiesta**

La richiesta seguente recupera gli oggetti associati a `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809/subjects \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce i soggetti associati all’ID ruolo richiesto, inclusi l’ID soggetto e il tipo di oggetto corrispondenti.

```json
{
  "items": [
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "PIRJ7WE5T3QT9Z4TCLVH86DE@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "WHPWE00MC26SHZ7AKBFG403D@AdobeID"
      },
  ]
  "_page": {
    "limit": 0,
    "count": 0
  },
  "_links": {
      "self": {
          "href": "/roles/{ROLE_ID}/subjects",
          "templated": false,
          "type": null,
          "method": null
      },
      "page": {
          "href": "/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
          "templated": true,
          "type": null,
          "method": null
      }
  }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `roleId` | ID ruolo associato all&#39;oggetto della query. |
| `subjectType` | Tipo dell&#39;oggetto della query. |
| `subjectId` | ID corrispondente all&#39;oggetto della query. |

## Creare un ruolo {#create}

Per creare un nuovo ruolo, effettuare una richiesta POST all&#39;endpoint `/roles` fornendo i valori per il nome, la descrizione e il tipo di ruolo del ruolo.

**Formato API**

```http
POST /roles/
```

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator Role",
    "description": "Role for administrator type of responsibilities and access",
    "roleType": "user-defined"
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Il nome del ruolo. Assicurati che il nome del ruolo sia descrittivo, in quanto può essere utilizzato per cercare informazioni sul ruolo. |
| `description` | (Facoltativo) Un valore descrittivo che puoi includere per fornire ulteriori informazioni sul tuo ruolo. |
| `roleType` | Il tipo designato del ruolo. I valori possibili per il tipo di ruolo sono: `user-defined` e `system-defined`. |

**Risposta**

In caso di esito positivo, la risposta restituisce il ruolo appena creato, con il relativo ID ruolo corrispondente, nonché informazioni sul tipo di ruolo, sui set di autorizzazioni e sugli attributi dell’oggetto.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID corrispondente al ruolo. Questo ID viene generato automaticamente. |
| `name` | Il nome del ruolo. |
| `description` | La proprietà description fornisce informazioni aggiuntive sul ruolo. |
| `roleType` | Il tipo designato del ruolo. I valori possibili per il tipo di ruolo sono: `user-defined` e `system-defined`. |
| `permissionSets` | I set di autorizzazioni rappresentano un gruppo di autorizzazioni che un amministratore può applicare a un ruolo. Un amministratore può assegnare set di autorizzazioni a un ruolo, invece di assegnare singole autorizzazioni. In questo modo è possibile creare ruoli personalizzati da un ruolo predefinito contenente un gruppo di autorizzazioni. |
| `sandboxes` | Questa proprietà visualizza all’interno dell’organizzazione le sandbox per le quali è stato eseguito il provisioning per un determinato ruolo. |
| `subjectAttributes` | Attributi che indicano la correlazione tra un soggetto e le risorse Experience Platform a cui hanno accesso. |
| `subjectAttributes.labels` | Visualizza le etichette di utilizzo dei dati applicate al ruolo sottoposto a query. |

## Aggiornare un ruolo {#patch}

È possibile aggiornare le proprietà di un ruolo effettuando una richiesta PATCH all&#39;endpoint `/roles` e fornendo l&#39;ID ruolo e i valori corrispondenti per le operazioni che si desidera applicare.

**Formato API**

```http
PATCH /roles/{ROLE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| {ROLE_ID} | ID del ruolo da aggiornare. |

**Richiesta**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "add",
        "path": "/description",
        "value": "Role with permission sets for admin type of access"
      }
    ]
  }'
```

| Operazioni | Descrizione |
| --- | --- |
| `op` | Chiamata di operazione utilizzata per definire l&#39;azione necessaria per aggiornare il ruolo. Le operazioni includono: `add`, `replace` e `remove`. |
| `path` | Percorso del parametro da aggiornare. |
| `value` | Il nuovo valore con cui desideri aggiornare il parametro. |

**Risposta**

In caso di esito positivo, la risposta restituisce il ruolo aggiornato, inclusi i nuovi valori per le proprietà che hai scelto di aggiornare.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role with permission sets for admin type of access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID corrispondente al ruolo. Questo ID viene generato automaticamente. |
| `name` | Il nome del ruolo. |
| `description` | La proprietà description fornisce informazioni aggiuntive sul ruolo. |
| `roleType` | Il tipo designato del ruolo. I valori possibili per il tipo di ruolo sono: `user-defined` e `system-defined`. |
| `permissionSets` | I set di autorizzazioni rappresentano un gruppo di autorizzazioni che un amministratore può applicare a un ruolo. Un amministratore può assegnare set di autorizzazioni a un ruolo, invece di assegnare singole autorizzazioni. In questo modo è possibile creare ruoli personalizzati da un ruolo predefinito contenente un gruppo di autorizzazioni. |
| `sandboxes` | Questa proprietà visualizza all’interno dell’organizzazione le sandbox per le quali è stato eseguito il provisioning per un determinato ruolo. |
| `subjectAttributes` | Attributi che indicano la correlazione tra un soggetto e le risorse Experience Platform a cui hanno accesso. |
| `subjectAttributes.labels` | Visualizza le etichette di utilizzo dei dati applicate al ruolo sottoposto a query. |

## Aggiornare un ruolo per ID ruolo {#put}

È possibile aggiornare un ruolo effettuando una richiesta PUT all&#39;endpoint `/roles` e specificando l&#39;ID ruolo corrispondente al ruolo da aggiornare.

**Formato API**

```http
PUT /roles/{ROLE_ID}
```

**Richiesta**

La richiesta seguente aggiorna il nome, la descrizione e il tipo di ruolo per l&#39;ID ruolo: `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator role for ACME",
    "description": "New administrator role for ACME",
    "roleType": "user-defined"
  }'
```

| Parametro | Descrizione |
| --- | --- |
| `name` | Nome aggiornato di un ruolo. |
| `description` | Descrizione aggiornata di un ruolo. |
| `roleType` | Il tipo designato del ruolo. I valori possibili per il tipo di ruolo sono: `user-defined` e `system-defined`. |

**Risposta**

In caso di esito positivo, la risposta restituisce il ruolo aggiornato, inclusi i nuovi valori per il nome, la descrizione e il tipo di ruolo.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator role for ACME",
  "description": "New administrator role for ACME",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID corrispondente al ruolo. Questo ID viene generato automaticamente. |
| `name` | Il nome del ruolo. |
| `description` | La proprietà description fornisce informazioni aggiuntive sul ruolo. |
| `roleType` | Il tipo designato del ruolo. I valori possibili per il tipo di ruolo sono: `user-defined` e `system-defined`. |
| `permissionSets` | I set di autorizzazioni rappresentano un gruppo di autorizzazioni che un amministratore può applicare a un ruolo. Un amministratore può assegnare set di autorizzazioni a un ruolo, invece di assegnare singole autorizzazioni. In questo modo è possibile creare ruoli personalizzati da un ruolo predefinito contenente un gruppo di autorizzazioni. |
| `sandboxes` | Questa proprietà visualizza all’interno dell’organizzazione le sandbox per le quali è stato eseguito il provisioning per un determinato ruolo. |
| `subjectAttributes` | Attributi che indicano la correlazione tra un soggetto e le risorse Experience Platform a cui hanno accesso. |
| `subjectAttributes.labels` | Visualizza le etichette di utilizzo dei dati applicate al ruolo sottoposto a query. |

## Aggiorna oggetto per ID ruolo

Per aggiornare i soggetti associati a un ruolo, effettuare una richiesta PATCH all&#39;endpoint `/roles` fornendo l&#39;ID ruolo dei soggetti da aggiornare.

**Formato API**

```http
PATCH /roles/{ROLE_ID}/subjects
```

| Parametro | Descrizione |
| --- | --- |
| {ROLE_ID} | ID del ruolo associato ai soggetti da aggiornare. |

**Richiesta**

La richiesta seguente aggiorna gli oggetti associati a `{ROLE_ID}`.

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/access-control/administration/roles/<ROLE_ID>/subjects' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "op": "add",
        "path": "/user",
        "value": "{USER ID}"
    }
]' 
```

| Operazioni | Descrizione |
| --- | --- |
| `op` | Chiamata di operazione utilizzata per definire l&#39;azione necessaria per aggiornare il ruolo. Le operazioni includono: `add`, `replace` e `remove`. |
| `path` | Percorso del parametro da aggiornare. |
| `value` | Il nuovo valore con cui desideri aggiornare il parametro. |

**Risposta**

In caso di esito positivo, la risposta restituisce il ruolo aggiornato, inclusi i nuovi valori per i soggetti.

```json
{
  "subjects": [
    [
      {
        "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID",
        "subjectType": "user"
      }
    ]
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/{ROLE_ID}/subjects",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
      "templated": true
    }
  }
}
```

## Eliminare una mansione {#delete}

Per eliminare un ruolo, effettuare una richiesta DELETE all&#39;endpoint `/roles` specificando l&#39;ID del ruolo che si desidera eliminare.

**Formato API**

```http
DELETE /roles/{ROLE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| {ROLE_ID} | ID del ruolo che si desidera eliminare. |

**Richiesta**

La richiesta seguente elimina il ruolo con ID `{ROLE_ID}`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto) e un corpo vuoto.

Puoi confermare l’eliminazione tentando una richiesta di ricerca (GET) al ruolo. Riceverai lo stato HTTP 404 (Non trovato) perché il ruolo è stato rimosso dall’amministrazione.

## Aggiungi credenziali API {#apicredential}

Per aggiungere una credenziale API, effettuare una richiesta PATCH all&#39;endpoint `/roles` fornendo l&#39;ID ruolo dei soggetti.

**Formato API**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/access-control/administration/roles/<ROLE_ID>/subjects' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "op": "add",
        "path": "/api-integration",
        "value": "{TECHNICAL ACCOUNT ID}"
    }
]'   
```

| Operazioni | Descrizione |
| --- | --- |
| `op` | Chiamata di operazione utilizzata per definire l&#39;azione necessaria per aggiornare il ruolo. Le operazioni includono: `add`, `replace` e `remove`. |
| `path` | Percorso del parametro da aggiungere. |
| `value` | Il valore con cui desideri aggiungere il parametro. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto) e un corpo vuoto.
