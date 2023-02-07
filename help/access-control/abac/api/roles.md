---
keywords: Experience Platform;home;argomenti comuni;api;controllo degli accessi basato su attributi;controllo degli accessi basato su attributi
solution: Experience Platform
title: Endpoint API ruoli
description: L'endpoint /ruoli nell'API di controllo accessi basato su attributi consente di gestire i ruoli in modo programmatico in Adobe Experience Platform.
exl-id: 049f7a18-7d06-437b-8ce9-25d7090ba782
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '1606'
ht-degree: 4%

---

# Endpoint ruoli

>[!NOTE]
>
>Se viene passato un token utente, l’utente del token deve avere un ruolo di amministratore organizzazione per l’organizzazione richiesta.

I ruoli definiscono l’accesso che un amministratore, uno specialista o un utente finale ha alle risorse dell’organizzazione. In un ambiente di controllo degli accessi basato su ruoli, il provisioning degli accessi utente viene raggruppato attraverso responsabilità e esigenze comuni. Un ruolo dispone di un determinato set di autorizzazioni e i membri dell’organizzazione possono essere assegnati a uno o più ruoli, a seconda dell’ambito di accesso di visualizzazione o scrittura necessario.

La `/roles` l’endpoint nell’API di controllo accessi basata sugli attributi ti consente di gestire i ruoli in modo programmatico all’interno dell’organizzazione.

## Introduzione

L’endpoint API utilizzato in questa guida fa parte dell’API di controllo accessi basata sugli attributi. Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e importanti informazioni sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recupera un elenco di ruoli {#list}

Puoi elencare tutti i ruoli esistenti appartenenti all’organizzazione effettuando una richiesta di GET al `/roles` punto finale.

**Formato API**

```http
GET /roles/
```

**Richiesta**

La richiesta seguente recupera un elenco di ruoli appartenenti all’organizzazione.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Risposta**

Una risposta corretta restituisce un elenco di ruoli nell’organizzazione, incluse informazioni sul rispettivo tipo di ruolo, set di autorizzazioni e attributi dell’oggetto.

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
| `id` | L&#39;ID che corrisponde al ruolo . Questo ID viene generato automaticamente. |
| `name` | Nome del ruolo. |
| `description` | La proprietà description fornisce ulteriori informazioni sul ruolo. |
| `roleType` | Tipo designato del ruolo. I valori possibili per il tipo di ruolo sono: `user-defined` e `system-defined`. |
| `permissionSets` | I set di autorizzazioni rappresentano un gruppo di autorizzazioni che un amministratore può assegnare a un ruolo. Un amministratore può assegnare set di autorizzazioni a un ruolo, anziché assegnare singole autorizzazioni. Ciò ti consente di creare ruoli personalizzati da un ruolo predefinito che contiene un gruppo di autorizzazioni. |
| `sandboxes` | Questa proprietà visualizza le sandbox all&#39;interno dell&#39;organizzazione per le quali è stato eseguito il provisioning per un particolare ruolo. |
| `subjectAttributes` | Attributi che indicano la correlazione tra un oggetto e le risorse di Platform a cui hanno accesso. |
| `subjectAttributes.labels` | Visualizza le etichette di utilizzo dei dati applicate al ruolo interrogato. |

## Cercare un ruolo {#lookup}

Puoi cercare un singolo ruolo effettuando una richiesta di GET che include il corrispondente `roleId` nel percorso della richiesta.

**Formato API**

```http
GET /roles/{ROLE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| {ROLE_ID} | ID del ruolo da cercare. |

**Richiesta**

La richiesta seguente recupera le informazioni per `{ROLE_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Risposta**

Una risposta corretta restituisce i dettagli dell’ID ruolo interrogato, incluse informazioni sul tipo di ruolo, i set di autorizzazioni e gli attributi oggetto.

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
| `id` | L&#39;ID che corrisponde al ruolo . Questo ID viene generato automaticamente. |
| `name` | Nome del ruolo. |
| `description` | La proprietà description fornisce ulteriori informazioni sul ruolo. |
| `roleType` | Tipo designato del ruolo. I valori possibili per il tipo di ruolo sono: `user-defined` e `system-defined`. |
| `permissionSets` | I set di autorizzazioni rappresentano un gruppo di autorizzazioni che un amministratore può assegnare a un ruolo. Un amministratore può assegnare set di autorizzazioni a un ruolo, anziché assegnare singole autorizzazioni. Ciò ti consente di creare ruoli personalizzati da un ruolo predefinito che contiene un gruppo di autorizzazioni. |
| `sandboxes` | Questa proprietà visualizza le sandbox all&#39;interno dell&#39;organizzazione per le quali è stato eseguito il provisioning per un particolare ruolo. |
| `subjectAttributes` | Attributi che indicano la correlazione tra un oggetto e le risorse di Platform a cui hanno accesso. |
| `subjectAttributes.labels` | Visualizza le etichette di utilizzo dei dati applicate al ruolo interrogato. |

## Cercare i soggetti per ID ruolo

È inoltre possibile recuperare i soggetti effettuando una richiesta di GET al `/roles` endpoint durante la fornitura di un {ROLE_ID}.

**Formato API**

```http
GET /roles/{ROLE_ID}/subjects
```

| Parametro | Descrizione |
| --- | --- |
| {ROLE_ID} | ID del ruolo associato ai soggetti da cercare. |

**Richiesta**

La richiesta seguente recupera gli argomenti associati a `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809/subjects \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Risposta**

Una risposta corretta restituisce i soggetti associati all’ID ruolo interrogato, inclusi l’ID oggetto e il tipo di oggetto corrispondenti.

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
| `roleId` | L&#39;ID del ruolo associato all&#39;oggetto interrogato. |
| `subjectType` | Tipo dell&#39;oggetto interrogato. |
| `subjectId` | L&#39;ID che corrisponde all&#39;oggetto interrogato. |

## Creare un ruolo {#create}

Per creare un nuovo ruolo, invia una richiesta POST al gruppo `/roles` endpoint fornendo i valori per il nome, la descrizione e il tipo di ruolo del ruolo.

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
| `name` | Nome del ruolo. Assicurati che il nome del tuo ruolo sia descrittivo in quanto puoi usarlo per cercare informazioni sul tuo ruolo. |
| `description` | (Facoltativo) Un valore descrittivo che può essere incluso per fornire ulteriori informazioni sul ruolo. |
| `roleType` | Tipo designato del ruolo. I valori possibili per il tipo di ruolo sono: `user-defined` e `system-defined`. |

**Risposta**

Una risposta corretta restituisce il ruolo appena creato, con l’ID del ruolo corrispondente, nonché informazioni sul tipo di ruolo, i set di autorizzazioni e gli attributi dell’oggetto.

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
| `id` | L&#39;ID che corrisponde al ruolo . Questo ID viene generato automaticamente. |
| `name` | Nome del ruolo. |
| `description` | La proprietà description fornisce ulteriori informazioni sul ruolo. |
| `roleType` | Tipo designato del ruolo. I valori possibili per il tipo di ruolo sono: `user-defined` e `system-defined`. |
| `permissionSets` | I set di autorizzazioni rappresentano un gruppo di autorizzazioni che un amministratore può assegnare a un ruolo. Un amministratore può assegnare set di autorizzazioni a un ruolo, anziché assegnare singole autorizzazioni. Ciò ti consente di creare ruoli personalizzati da un ruolo predefinito che contiene un gruppo di autorizzazioni. |
| `sandboxes` | Questa proprietà visualizza le sandbox all&#39;interno dell&#39;organizzazione per le quali è stato eseguito il provisioning per un particolare ruolo. |
| `subjectAttributes` | Attributi che indicano la correlazione tra un oggetto e le risorse di Platform a cui hanno accesso. |
| `subjectAttributes.labels` | Visualizza le etichette di utilizzo dei dati applicate al ruolo interrogato. |

## Aggiornare un ruolo {#patch}

Puoi aggiornare le proprietà di un ruolo effettuando una richiesta di PATCH al `/roles` durante la fornitura dell&#39;ID ruolo e dei valori corrispondenti per le operazioni che si desidera applicare.

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
| `op` | La chiamata dell’operazione utilizzata per definire l’azione necessaria per aggiornare il ruolo. Le operazioni includono: `add`, `replace`e `remove`. |
| `path` | Percorso del parametro da aggiornare. |
| `value` | Il nuovo valore con cui si desidera aggiornare il parametro. |

**Risposta**

Una risposta corretta restituisce il ruolo aggiornato, inclusi nuovi valori per le proprietà che hai scelto di aggiornare.

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
| `id` | L&#39;ID che corrisponde al ruolo . Questo ID viene generato automaticamente. |
| `name` | Nome del ruolo. |
| `description` | La proprietà description fornisce ulteriori informazioni sul ruolo. |
| `roleType` | Tipo designato del ruolo. I valori possibili per il tipo di ruolo sono: `user-defined` e `system-defined`. |
| `permissionSets` | I set di autorizzazioni rappresentano un gruppo di autorizzazioni che un amministratore può assegnare a un ruolo. Un amministratore può assegnare set di autorizzazioni a un ruolo, anziché assegnare singole autorizzazioni. Ciò ti consente di creare ruoli personalizzati da un ruolo predefinito che contiene un gruppo di autorizzazioni. |
| `sandboxes` | Questa proprietà visualizza le sandbox all&#39;interno dell&#39;organizzazione per le quali è stato eseguito il provisioning per un particolare ruolo. |
| `subjectAttributes` | Attributi che indicano la correlazione tra un oggetto e le risorse di Platform a cui hanno accesso. |
| `subjectAttributes.labels` | Visualizza le etichette di utilizzo dei dati applicate al ruolo interrogato. |

## Aggiornare un ruolo per ID ruolo {#put}

È possibile aggiornare un ruolo effettuando una richiesta di PUT al `/roles` e specifica l&#39;ID ruolo corrispondente al ruolo da aggiornare.

**Formato API**

```http
PUT /roles/{ROLE_ID}
```

**Richiesta**

La seguente richiesta aggiorna nome, descrizione e tipo di ruolo per l’ID ruolo: `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

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
| `roleType` | Tipo designato del ruolo. I valori possibili per il tipo di ruolo sono: `user-defined` e `system-defined`. |

**Risposta**

Se il ruolo viene aggiornato correttamente, vengono restituiti nuovi valori per nome, descrizione e tipo di ruolo.

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
| `id` | L&#39;ID che corrisponde al ruolo . Questo ID viene generato automaticamente. |
| `name` | Nome del ruolo. |
| `description` | La proprietà description fornisce ulteriori informazioni sul ruolo. |
| `roleType` | Tipo designato del ruolo. I valori possibili per il tipo di ruolo sono: `user-defined` e `system-defined`. |
| `permissionSets` | I set di autorizzazioni rappresentano un gruppo di autorizzazioni che un amministratore può assegnare a un ruolo. Un amministratore può assegnare set di autorizzazioni a un ruolo, anziché assegnare singole autorizzazioni. Ciò ti consente di creare ruoli personalizzati da un ruolo predefinito che contiene un gruppo di autorizzazioni. |
| `sandboxes` | Questa proprietà visualizza le sandbox all&#39;interno dell&#39;organizzazione per le quali è stato eseguito il provisioning per un particolare ruolo. |
| `subjectAttributes` | Attributi che indicano la correlazione tra un oggetto e le risorse di Platform a cui hanno accesso. |
| `subjectAttributes.labels` | Visualizza le etichette di utilizzo dei dati applicate al ruolo interrogato. |

## Aggiorna oggetto per ID ruolo

Per aggiornare gli argomenti associati a un ruolo, invia una richiesta PATCH al `/roles` endpoint durante la fornitura dell&#39;ID ruolo dei soggetti che si desidera aggiornare.

**Formato API**

```http
PATCH /roles/{ROLE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| {ROLE_ID} | ID del ruolo associato ai soggetti da aggiornare. |

**Richiesta**

La seguente richiesta aggiorna gli argomenti associati a `{ROLE_ID}`.

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
        "path": "/subjects",
        "value": "New subjects"
      }
    ]
  }'
```

| Operazioni | Descrizione |
| --- | --- |
| `op` | La chiamata dell’operazione utilizzata per definire l’azione necessaria per aggiornare il ruolo. Le operazioni includono: `add`, `replace`e `remove`. |
| `path` | Percorso del parametro da aggiornare. |
| `value` | Il nuovo valore con cui si desidera aggiornare il parametro. |

**Risposta**

Una risposta corretta restituisce i soggetti aggiornati associati all’ID ruolo interrogato.

```json
{
  "subjects": [
    {
      "subjectId": "string",
      "subjectType": "user"
    }
  ],
  "_page": {
    "limit": 0,
    "count": 0
  },
  "_links": {
    "next": {
      "href": "string",
      "templated": true
    },
    "page": {
      "href": "string",
      "templated": true
    }
  }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `subjectId` | ID di un oggetto. |
| `subjectType` | Il tipo di oggetto. |

## Eliminare un ruolo {#delete}

Per eliminare un ruolo, invia una richiesta DELETE al `/roles` endpoint durante la specificazione dell&#39;ID del ruolo da eliminare.

**Formato API**

```http
DELETE /roles/{ROLE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| {ROLE_ID} | ID del ruolo da eliminare. |

**Richiesta**

La richiesta seguente elimina il ruolo con l’ID di `{ROLE_ID}`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto.

Puoi confermare l’eliminazione tentando una richiesta di ricerca (GET) al ruolo . Riceverai uno stato HTTP 404 (Non trovato) perché il ruolo è stato rimosso dall’amministrazione.
