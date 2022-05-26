---
keywords: Experience Platform;home;argomenti comuni;api;controllo degli accessi basato su attributi;controllo degli accessi basato su attributi
solution: Experience Platform
title: Endpoint API per criteri
description: L'endpoint /policy nell'API di controllo accessi basato su attributi consente di gestire i criteri in Adobe Experience Platform a livello di programmazione.
hide: true
hidefromtoc: true
exl-id: 07690f43-fdd9-4254-9324-84e6bd226743
source-git-commit: 19f1e8df8cd8b55ed6b03f80e42810aefd211474
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 3%

---

# Endpoint criteri

>[!IMPORTANT]
>
>Il controllo dell&#39;accesso basato su attributi è attualmente disponibile in una versione limitata per i clienti del settore sanitario negli Stati Uniti. Questa funzionalità sarà disponibile per tutti i clienti Real-time Customer Data Platform una volta rilasciata.

Le politiche sono dichiarazioni che riuniscono gli attributi per stabilire azioni ammissibili e non ammissibili. I criteri possono essere locali o globali e possono sostituire altri criteri. La `/policies` l’endpoint nell’API di controllo accessi basata sugli attributi ti consente di gestire i criteri in modo programmatico, incluse informazioni sulle regole che li governano e sulle rispettive condizioni dell’oggetto.

## Introduzione

L’endpoint API utilizzato in questa guida fa parte dell’API di controllo accessi basata sugli attributi. Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e importanti informazioni sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recupera un elenco di criteri {#list}

Effettua una richiesta di GET al `/policies` per elencare tutti i criteri esistenti nell&#39;organizzazione.

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

Una risposta corretta restituisce un elenco dei criteri esistenti.

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
| `id` | L&#39;ID che corrisponde a un criterio. Questo identificatore è generato automaticamente e può essere utilizzato per cercare, aggiornare ed eliminare un criterio. |
| `imsOrgId` | Organizzazione in cui il criterio interrogato è accessibile. |
| `createdBy` | ID dell&#39;utente che ha creato il criterio. |
| `createdAt` | Data e ora di creazione del criterio. La `createdAt` La proprietà viene visualizzata in marca temporale univoca. |
| `modifiedBy` | ID dell’utente che ha aggiornato il criterio per l’ultima volta. |
| `modifiedAt` | Data e ora dell&#39;ultimo aggiornamento del criterio. La `modifiedAt` La proprietà viene visualizzata in marca temporale univoca. |
| `name` | Nome del criterio. |
| `description` | (Facoltativo) Proprietà che può essere aggiunta per fornire ulteriori informazioni su un particolare criterio. |
| `status` | Lo stato corrente di un criterio. Questa proprietà definisce se un criterio è attualmente `active` o `inactive`. |
| `subjectCondition` | Le condizioni applicate a un soggetto. Un oggetto è un utente con determinati attributi che richiedono l’accesso a una risorsa per eseguire un’azione. In questo caso, `subjectCondition` sono condizioni simili alle query applicate agli attributi oggetto. |
| `rules` | Set di regole che definiscono un criterio. Le regole definiscono quali combinazioni di attributi sono autorizzate affinché l’oggetto esegua correttamente un’azione sulla risorsa. |
| `rules.effect` | L&#39;effetto che si ottiene dopo aver considerato i valori per `action`, `condition` e `resource`. I valori possibili sono: `permit`, `deny`oppure `indeterminate`. |
| `rules.resource` | Risorsa o oggetto a cui un soggetto può o non può accedere.  Le risorse possono essere file, applicazioni, server o anche API. |
| `rules.condition` | Condizioni applicate a una risorsa. Ad esempio, se una risorsa è uno schema, a uno schema possono essere applicate determinate etichette che contribuiscono a determinare se un&#39;azione eseguita in relazione a tale schema è consentita o non consentita. |
| `rules.action` | Azione consentita a un oggetto in relazione a una risorsa interrogata. I valori possibili sono: `read`, `create`, `edit`e `delete`. |

## Cerca i dettagli dei criteri per ID {#lookup}

Effettua una richiesta di GET al `/policies` endpoint durante la fornitura di un ID criterio nel percorso della richiesta per recuperare informazioni su quel singolo criterio.

**Formato API**

```http
GET /policies/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| {POLICY_ID} | ID del criterio da recuperare. |

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

Una richiesta corretta restituisce informazioni sull&#39;ID criterio interrogato.

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
| `id` | L&#39;ID che corrisponde a un criterio. Questo identificatore è generato automaticamente e può essere utilizzato per cercare, aggiornare ed eliminare un criterio. |
| `imsOrgId` | Organizzazione in cui il criterio interrogato è accessibile. |
| `createdBy` | ID dell&#39;utente che ha creato il criterio. |
| `createdAt` | Data e ora di creazione del criterio. La `createdAt` La proprietà viene visualizzata in marca temporale univoca. |
| `modifiedBy` | ID dell’utente che ha aggiornato il criterio per l’ultima volta. |
| `modifiedAt` | Data e ora dell&#39;ultimo aggiornamento del criterio. La `modifiedAt` La proprietà viene visualizzata in marca temporale univoca. |
| `name` | Nome del criterio. |
| `description` | (Facoltativo) Proprietà che può essere aggiunta per fornire ulteriori informazioni su un particolare criterio. |
| `status` | Lo stato corrente di un criterio. Questa proprietà definisce se un criterio è attualmente `active` o `inactive`. |
| `subjectCondition` | Le condizioni applicate a un soggetto. Un oggetto è un utente con determinati attributi che richiedono l’accesso a una risorsa per eseguire un’azione. In questo caso, `subjectCondition` sono condizioni simili alle query applicate agli attributi oggetto. |
| `rules` | Set di regole che definiscono un criterio. Le regole definiscono quali combinazioni di attributi sono autorizzate affinché l’oggetto esegua correttamente un’azione sulla risorsa. |
| `rules.effect` | L&#39;effetto che si ottiene dopo aver considerato i valori per `action`, `condition` e `resource`. I valori possibili sono: `permit`, `deny`oppure `indeterminate`. |
| `rules.resource` | Risorsa o oggetto a cui un soggetto può o non può accedere.  Le risorse possono essere file, applicazioni, server o anche API. |
| `rules.condition` | Condizioni applicate a una risorsa. Ad esempio, se una risorsa è uno schema, a uno schema possono essere applicate determinate etichette che contribuiscono a determinare se un&#39;azione eseguita in relazione a tale schema è consentita o non consentita. |
| `rules.action` | Azione consentita a un oggetto in relazione a una risorsa interrogata. I valori possibili sono: `read`, `create`, `edit`e `delete`. |


## Creare un criterio {#create}

Per creare un nuovo criterio, invia una richiesta POST al `/policies` punto finale.

**Formato API**

```http
POST /policies
```

**Richiesta**

Nella richiesta seguente viene creato un nuovo criterio denominato: `acme-integration-policy`.

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
| `imsOrgId` | Organizzazione che contiene il criterio. |
| `rules` | Set di regole che definiscono un criterio. Le regole definiscono quali combinazioni di attributi sono autorizzate affinché l’oggetto esegua correttamente un’azione sulla risorsa. |
| `rules.effect` | L&#39;effetto che si ottiene dopo aver considerato i valori per `action`, `condition` e `resource`. I valori possibili sono: `permit`, `deny`oppure `indeterminate`. |
| `rules.resource` | Risorsa o oggetto a cui un soggetto può o non può accedere.  Le risorse possono essere file, applicazioni, server o anche API. |
| `rules.condition` | Condizioni applicate a una risorsa. Ad esempio, se una risorsa è uno schema, a uno schema possono essere applicate determinate etichette che contribuiscono a determinare se un&#39;azione eseguita in relazione a tale schema è consentita o non consentita. |
| `rules.action` | Azione consentita a un oggetto in relazione a una risorsa interrogata. I valori possibili sono: `read`, `create`, `edit`e `delete`. |

**Risposta**

Una richiesta corretta restituisce il criterio appena creato, incluso l’ID del criterio univoco e le regole associate.

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
| `id` | L&#39;ID che corrisponde a un criterio. Questo identificatore è generato automaticamente e può essere utilizzato per cercare, aggiornare ed eliminare un criterio. |
| `name` | Nome di un criterio. |
| `rules` | Set di regole che definiscono un criterio. Le regole definiscono quali combinazioni di attributi sono autorizzate affinché l’oggetto esegua correttamente un’azione sulla risorsa. |
| `rules.effect` | L&#39;effetto che si ottiene dopo aver considerato i valori per `action`, `condition` e `resource`. I valori possibili sono: `permit`, `deny`oppure `indeterminate`. |
| `rules.resource` | Risorsa o oggetto a cui un soggetto può o non può accedere.  Le risorse possono essere file, applicazioni, server o anche API. |
| `rules.condition` | Condizioni applicate a una risorsa. Ad esempio, se una risorsa è uno schema, a uno schema possono essere applicate determinate etichette che contribuiscono a determinare se un&#39;azione eseguita in relazione a tale schema è consentita o non consentita. |
| `rules.action` | Azione consentita a un oggetto in relazione a una risorsa interrogata. I valori possibili sono: `read`, `create`, `edit`e `delete`. |


## Aggiornare un criterio per ID criterio {#put}

Per aggiornare le regole di un singolo criterio, invia una richiesta PUT al `/policies` durante la fornitura dell&#39;ID del criterio che si desidera aggiornare nel percorso della richiesta.

**Formato API**

```http
PUT /policies/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| {POLICY_ID} | ID del criterio da aggiornare. |

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

Una risposta corretta restituisce il criterio aggiornato.

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

Per aggiornare le proprietà di un singolo criterio, invia una richiesta PATCH al `/policies` durante la fornitura dell&#39;ID del criterio che si desidera aggiornare nel percorso della richiesta.

**Formato API**

```http
PATCH /policies/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| {POLICY_ID} | ID del criterio da aggiornare. |

**Richiesta**

La seguente richiesta sostituisce il valore di `/description` in ID criterio `c3863937-5d40-448d-a7be-416e538f955e`.

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
| `op` | La chiamata dell’operazione utilizzata per definire l’azione necessaria per aggiornare il ruolo. Le operazioni includono: `add`, `replace`e `remove`. |
| `path` | Percorso del parametro da aggiornare. |
| `value` | Il nuovo valore con cui si desidera aggiornare il parametro. |

**Risposta**

Una risposta corretta restituisce l’ID dei criteri interrogati con la descrizione aggiornata.

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

Per eliminare un criterio, invia una richiesta DELETE al `/policies` endpoint durante la fornitura dell&#39;ID del criterio da eliminare.

**Formato API**

```http
DELETE /policies/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| {POLICY_ID} | ID del criterio da eliminare. |

**Richiesta**

La seguente richiesta elimina il criterio con l’ID di `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto.

Puoi confermare l’eliminazione tentando una richiesta di ricerca (GET) al criterio. Riceverai uno stato HTTP 404 (Non trovato) perché il criterio è stato rimosso dall’amministrazione.
