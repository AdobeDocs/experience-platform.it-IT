---
keywords: Experience Platform;home;argomenti popolari;api;Attribute-Based Access Control;attribute-based access control
solution: Experience Platform
title: Endpoint API per i criteri di controllo degli accessi
description: L’endpoint /policies nell’API di controllo dell’accesso basato su attributi consente di gestire in modo programmatico i criteri in Adobe Experience Platform.
exl-id: 07690f43-fdd9-4254-9324-84e6bd226743
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 3%

---

# Endpoint &quot;access control policies&quot;

>[!NOTE]
>
>Se viene passato un token utente, l’utente del token deve avere un ruolo &quot;amministratore organizzazione&quot; per l’organizzazione richiesta.

I criteri di controllo degli accessi sono istruzioni che riuniscono attributi per stabilire azioni consentite e inammissibili. Questi criteri possono essere locali o globali e possono ignorare altri criteri. Il `/policies` L’endpoint nell’API di controllo degli accessi basato su attributi consente di gestire in modo programmatico i criteri, incluse le informazioni sulle regole che li governano e sulle rispettive condizioni dell’oggetto.

>[!IMPORTANT]
>
>Questo endpoint non deve essere confuso con `/policies` endpoint nella [API del servizio criteri](../../../data-governance/api/policies.md), utilizzato per gestire i criteri di utilizzo dei dati.

## Introduzione

L’endpoint API utilizzato in questa guida fa parte dell’API di controllo degli accessi basata su attributi. Prima di continuare, controlla [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida per la lettura delle chiamate API di esempio di questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recuperare un elenco di criteri {#list}

Effettuare una richiesta di GET al `/policies` per elencare tutti i criteri esistenti nell’organizzazione.

**Formato API**

```http
GET /policies
```

**Richiesta**

La richiesta seguente recupera un elenco di criteri esistenti.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di criteri esistenti.

```json
{
  {
      "id": "7019068e-a3a0-48ce-b56b-008109470592",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652892767559,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652895736367,
      "name": "schema-field",
      "description": "schema-field",
      "status": "inactive",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/xql/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.read",
                  "com.adobe.action.write",
                  "com.adobe.action.view"
              ]
          },
          {
              "effect": "Permit",
              "resource": "/orgs/{IMS_ORG}/sandboxes/*/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.delete"
              ]
          },
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/delete-sandbox-adfengine-test-8/segments/*",
              "condition": "{\"!\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}",
              "actions": [
                  "com.adobe.action.write"
              ]
          }
      ],
      "_etag": "\"0300593f-0000-0200-0000-62852ff80000\""
  },
  {
      "id": "13138ef6-c007-495d-837f-0a248867e219",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652859368555,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652890780206,
      "name": "Documentation-Copy",
      "description": "xyz",
      "status": "active",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Permit",
              "resource": "orgs/{IMS_ORG}/sandboxes/ro-sand/schemas/*/schema-fields/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"and\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          },
          {
              "effect": "Deny",
              "resource": "orgs/{IMS_ORG}/sandboxes/*/segments/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          }
      ],
      "_etag": "\"0300d43c-0000-0200-0000-62851c9c0000\""
  },
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID corrispondente a un criterio. Questo identificatore è generato automaticamente e può essere utilizzato per cercare, aggiornare ed eliminare un criterio. |
| `imsOrgId` | Organizzazione in cui è accessibile il criterio sottoposto a query. |
| `createdBy` | ID dell’utente che ha creato il criterio. |
| `createdAt` | L’ora in cui è stato creato il criterio. Il `createdAt` viene visualizzata nella marca temporale dell’epoca unix. |
| `modifiedBy` | ID dell’ultimo utente che ha aggiornato il criterio. |
| `modifiedAt` | L’ora dell’ultimo aggiornamento del criterio. Il `modifiedAt` viene visualizzata nella marca temporale dell’epoca unix. |
| `name` | Nome del criterio. |
| `description` | (Facoltativo) Proprietà che può essere aggiunta per fornire ulteriori informazioni su un particolare criterio. |
| `status` | Stato corrente di un criterio. Questa proprietà definisce se un criterio è attualmente `active` o `inactive`. |
| `subjectCondition` | Le condizioni applicate a un soggetto. Un oggetto è un utente con determinati attributi che richiede l’accesso a una risorsa per eseguire un’azione. In questo caso, `subjectCondition` sono condizioni di tipo query applicate agli attributi dell’oggetto. |
| `rules` | L’insieme di regole che definiscono un criterio. Le regole definiscono quali combinazioni di attributi sono autorizzate affinché il soggetto esegua correttamente un’azione sulla risorsa. |
| `rules.effect` | L’effetto che risulta dopo aver considerato i valori per `action`, `condition` e `resource`. I valori possibili includono: `permit`, `deny`, o `indeterminate`. |
| `rules.resource` | La risorsa o l&#39;oggetto a cui un soggetto può o non può accedere.  Le risorse possono essere file, applicazioni, server o anche API. |
| `rules.condition` | Condizioni applicate a una risorsa. Ad esempio, se una risorsa è uno schema, a uno schema possono essere applicate determinate etichette che contribuiscono a determinare se un’azione contro tale schema è consentita o meno. |
| `rules.action` | Azione consentita a un oggetto per una risorsa su cui è stata eseguita una query. I valori possibili includono: `read`, `create`, `edit`, e `delete`. |

## Cerca i dettagli dei criteri per ID {#lookup}

Effettuare una richiesta di GET al `/policies` mentre si fornisce un ID policy nel percorso della richiesta per recuperare informazioni su quel singolo criterio.

**Formato API**

```http
GET /policies/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| {POLICY_ID} | ID del criterio che desideri recuperare. |

**Richiesta**

La richiesta seguente recupera informazioni su un singolo criterio.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/13138ef6-c007-495d-837f-0a248867e219 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Risposta**

In caso di esito positivo, la richiesta restituisce informazioni sull’ID del criterio richiesto.

```json
{
    "id": "13138ef6-c007-495d-837f-0a248867e219",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652859368555,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652890780206,
    "name": "Documentation-Copy",
    "description": "xyz",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "orgs/{IMS_ORG}/sandboxes/ro-sand/schemas/*/schema-fields/*",
            "condition": "{\"!\":[{\"or\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"and\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        },
        {
            "effect": "Deny",
            "resource": "orgs/{IMS_ORG}/sandboxes/*/segments/*",
            "condition": "{\"!\":[{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": "\"0300d43c-0000-0200-0000-62851c9c0000\""
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID corrispondente a un criterio. Questo identificatore è generato automaticamente e può essere utilizzato per cercare, aggiornare ed eliminare un criterio. |
| `imsOrgId` | Organizzazione in cui è accessibile il criterio sottoposto a query. |
| `createdBy` | ID dell’utente che ha creato il criterio. |
| `createdAt` | L’ora in cui è stato creato il criterio. Il `createdAt` viene visualizzata nella marca temporale dell’epoca unix. |
| `modifiedBy` | ID dell’ultimo utente che ha aggiornato il criterio. |
| `modifiedAt` | L’ora dell’ultimo aggiornamento del criterio. Il `modifiedAt` viene visualizzata nella marca temporale dell’epoca unix. |
| `name` | Nome del criterio. |
| `description` | (Facoltativo) Proprietà che può essere aggiunta per fornire ulteriori informazioni su un particolare criterio. |
| `status` | Stato corrente di un criterio. Questa proprietà definisce se un criterio è attualmente `active` o `inactive`. |
| `subjectCondition` | Le condizioni applicate a un soggetto. Un oggetto è un utente con determinati attributi che richiede l’accesso a una risorsa per eseguire un’azione. In questo caso, `subjectCondition` sono condizioni di tipo query applicate agli attributi dell’oggetto. |
| `rules` | L’insieme di regole che definiscono un criterio. Le regole definiscono quali combinazioni di attributi sono autorizzate affinché il soggetto esegua correttamente un’azione sulla risorsa. |
| `rules.effect` | L’effetto che risulta dopo aver considerato i valori per `action`, `condition` e `resource`. I valori possibili includono: `permit`, `deny`, o `indeterminate`. |
| `rules.resource` | La risorsa o l&#39;oggetto a cui un soggetto può o non può accedere.  Le risorse possono essere file, applicazioni, server o anche API. |
| `rules.condition` | Condizioni applicate a una risorsa. Ad esempio, se una risorsa è uno schema, a uno schema possono essere applicate determinate etichette che contribuiscono a determinare se un’azione contro tale schema è consentita o meno. |
| `rules.action` | Azione consentita a un oggetto per una risorsa su cui è stata eseguita una query. I valori possibili includono: `read`, `create`, `edit`, e `delete`. |


## Creare un criterio {#create}

Per creare un nuovo criterio, effettua una richiesta POST al `/policies` endpoint.

**Formato API**

```http
POST /policies
```

**Richiesta**

La richiesta seguente crea un nuovo criterio denominato: `acme-integration-policy`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "name": "acme-integration-policy",
      "description": "Policy for ACME",
      "imsOrgId": "{IMS_ORG}",
      "rules": [
        {
          "effect": "Permit",
          "resource": "/orgs/{IMS_ORG}/sandboxes/*",
          "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
          "actions": [
            "read"
          ]
        }
      ]
    }'
```

| Parametro | Descrizione |
| --- | --- |
| `name` | Nome del criterio. |
| `description` | (Facoltativo) Proprietà che può essere aggiunta per fornire ulteriori informazioni su un particolare criterio. |
| `imsOrgId` | L’organizzazione che contiene il criterio. |
| `rules` | L’insieme di regole che definiscono un criterio. Le regole definiscono quali combinazioni di attributi sono autorizzate affinché il soggetto esegua correttamente un’azione sulla risorsa. |
| `rules.effect` | L’effetto che risulta dopo aver considerato i valori per `action`, `condition` e `resource`. I valori possibili includono: `permit`, `deny`, o `indeterminate`. |
| `rules.resource` | La risorsa o l&#39;oggetto a cui un soggetto può o non può accedere.  Le risorse possono essere file, applicazioni, server o anche API. |
| `rules.condition` | Condizioni applicate a una risorsa. Ad esempio, se una risorsa è uno schema, a uno schema possono essere applicate determinate etichette che contribuiscono a determinare se un’azione contro tale schema è consentita o meno. |
| `rules.action` | Azione consentita a un oggetto per una risorsa su cui è stata eseguita una query. I valori possibili includono: `read`, `create`, `edit`, e `delete`. |

**Risposta**

In caso di esito positivo, la richiesta restituisce il criterio appena creato, compreso l’ID univoco e le regole associate.

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988384458,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Policy for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "read"
            ]
        }
    ],
    "_etag": null
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID corrispondente a un criterio. Questo identificatore è generato automaticamente e può essere utilizzato per cercare, aggiornare ed eliminare un criterio. |
| `name` | Nome di un criterio. |
| `rules` | L’insieme di regole che definiscono un criterio. Le regole definiscono quali combinazioni di attributi sono autorizzate affinché il soggetto esegua correttamente un’azione sulla risorsa. |
| `rules.effect` | L’effetto che risulta dopo aver considerato i valori per `action`, `condition` e `resource`. I valori possibili includono: `permit`, `deny`, o `indeterminate`. |
| `rules.resource` | La risorsa o l&#39;oggetto a cui un soggetto può o non può accedere.  Le risorse possono essere file, applicazioni, server o anche API. |
| `rules.condition` | Condizioni applicate a una risorsa. Ad esempio, se una risorsa è uno schema, a uno schema possono essere applicate determinate etichette che contribuiscono a determinare se un’azione contro tale schema è consentita o meno. |
| `rules.action` | Azione consentita a un oggetto per una risorsa su cui è stata eseguita una query. I valori possibili includono: `read`, `create`, `edit`, e `delete`. |


## Aggiornare un criterio per ID criterio {#put}

Per aggiornare le regole di un singolo criterio, effettua una richiesta PUT al `/policies` endpoint, fornendo l’ID del criterio da aggiornare nel percorso della richiesta.

**Formato API**

```http
PUT /policies/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| {POLICY_ID} | ID del criterio che desideri aggiornare. |

**Richiesta**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/8cf487d7-3642-4243-a8ea-213d72f694b9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
      "imsOrgId": "{IMS_ORG}",
      "name": "test-2",
      "rules": [
      {
        "effect": "Deny",
        "resource": "/orgs/{IMS_ORG}/sandboxes/*",
        "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
        "actions": [
          "read"
        ]
      }
    ]
  }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce il criterio aggiornato.

```json
{
    "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988866647,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652989297287,
    "name": "test-2",
    "description": null,
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Deny",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "read"
            ]
        }
    ],
    "_etag": null
}
```

## Aggiornare le proprietà dei criteri {#patch}

Per aggiornare le proprietà di un singolo criterio, effettua una richiesta PATCH al `/policies` endpoint, fornendo l’ID del criterio da aggiornare nel percorso della richiesta.

**Formato API**

```http
PATCH /policies/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| {POLICY_ID} | ID del criterio che desideri aggiornare. |

**Richiesta**

La seguente richiesta sostituisce il valore di `/description` in ID policy `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "replace",
        "path": "/description",
        "value": "Pre-set policy to be applied for ACME"
      }
    ]
  }'
```

| Operazioni | Descrizione |
| --- | --- |
| `op` | Chiamata di operazione utilizzata per definire l&#39;azione necessaria per aggiornare il ruolo. Le operazioni includono: `add`, `replace`, e `remove`. |
| `path` | Percorso del parametro da aggiornare. |
| `value` | Il nuovo valore con cui desideri aggiornare il parametro. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID del criterio su cui è stata eseguita la query con una descrizione aggiornata.

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "acp_accessControlService",
    "createdAt": 1652988384458,
    "modifiedBy": "acp_accessControlService",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Pre-set policy to be applied for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "read"
            ]
        }
    ],
    "_etag": null
}
```

## Eliminare un criterio {#delete}

Per eliminare un criterio, effettua una richiesta DELETE al `/policies` mentre fornisci l’ID del criterio da eliminare.

**Formato API**

```http
DELETE /policies/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| {POLICY_ID} | ID del criterio che desideri eliminare. |

**Richiesta**

La richiesta seguente elimina il criterio con l’ID di `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto) e un corpo vuoto.

Puoi confermare l’eliminazione tentando una richiesta di ricerca (GET) nel criterio. Riceverai lo stato HTTP 404 (Non trovato) perché il criterio è stato rimosso dall’amministrazione.
