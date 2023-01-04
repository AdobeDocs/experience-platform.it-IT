---
keywords: Experience Platform;home;argomenti comuni;governance dei dati;criteri di utilizzo dei dati
solution: Experience Platform
title: Creare un criterio di governance dei dati nell’API
topic-legacy: policies
type: Tutorial
description: Scopri come creare un criterio di governance dei dati utilizzando l’API del servizio criteri.
exl-id: 8483f8a1-efe8-4ebb-b074-e0577e5a81a4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 3%

---

# Creare un criterio di governance dei dati nell’API

La [API del servizio criteri](https://www.adobe.io/experience-platform-apis/references/policy-service/) consente di creare e gestire criteri di governance dei dati per determinare quali azioni di marketing possono essere intraprese rispetto ai dati che contengono determinate etichette di utilizzo dei dati.

Questo documento fornisce un&#39;esercitazione dettagliata per la creazione di un criterio di governance utilizzando [!DNL Policy Service] API.

>[!NOTE]
>
>Per i passaggi su come creare un criterio di controllo degli accessi, consulta `/policies` guida dell&#39;endpoint per [API di controllo accessi](../../access-control/abac/api/policies.md). Per informazioni su come creare un criterio per il consenso, consulta [guida all’interfaccia utente dei criteri](./user-guide.md#consent-policy).

## Introduzione

Questa esercitazione richiede una comprensione approfondita dei seguenti concetti chiave relativi alla creazione e alla valutazione dei criteri:

* [Governance dei dati di Adobe Experience Platform](../home.md): Il quadro [!DNL Platform] applica la conformità per l’utilizzo dei dati.
   * [Etichette di utilizzo dati](../labels/overview.md): Le etichette per l’utilizzo dei dati vengono applicate ai campi di dati XDM, specificando le restrizioni per l’accesso a tali dati.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il quadro standardizzato [!DNL Platform] organizza i dati sulla customer experience.
* [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Prima di avviare questa esercitazione, controlla la [guida per sviluppatori](../api/getting-started.md) per informazioni importanti che devi conoscere al fine di effettuare correttamente le chiamate al [!DNL Policy Service] API, incluse le intestazioni richieste e come leggere le chiamate API di esempio.

## Definire un’azione di marketing {#define-action}

Nel framework per la governance dei dati, un’azione di marketing è un’azione che [!DNL Experience Platform] prende i dati del consumatore, per i quali è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati.

Il primo passaggio nella creazione di un criterio di utilizzo dei dati consiste nel determinare quale azione di marketing verrà valutata dal criterio. Questa operazione può essere eseguita utilizzando una delle seguenti opzioni:

* [Cerca un’azione di marketing esistente](#look-up)
* [Crea una nuova azione di marketing](#create-new)

### Cerca un’azione di marketing esistente {#look-up}

Puoi cercare le azioni di marketing esistenti da valutare in base al criterio effettuando una richiesta di GET a uno dei `/marketingActions` endpoint.

**Formato API**

A seconda che tu stia cercando un’azione di marketing fornita da [!DNL Experience Platform] o un&#39;azione di marketing personalizzata creata dalla tua organizzazione, utilizza `marketingActions/core` o `marketingActions/custom` endpoint, rispettivamente.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Richiesta**

La richiesta seguente utilizza il `marketingActions/custom` endpoint , che recupera un elenco di tutte le azioni di marketing definite dall’organizzazione IMS.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce il numero totale di azioni di marketing trovate (`count`) ed elenca i dettagli delle azioni di marketing stesse all’interno della `children` array.

```json
{
    "_page": {
        "start": "sampleMarketingAction",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/marketingActions/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "sampleMarketingAction",
            "description": "Marketing Action description.",
            "imsOrg": "{ORG_ID}",
            "created": 1550714012088,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714012088,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{ORG_ID}",
            "created": 1550793833224,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550793833224,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `_links.self.href` | Ogni elemento all&#39;interno della `children` contiene un ID URI per l’azione di marketing elencata. |

Quando trovi l’azione di marketing da utilizzare, registra il valore della relativa `href` proprietà. Questo valore viene utilizzato durante il passaggio successivo di [creazione di un criterio](#create-policy).

### Crea una nuova azione di marketing {#create-new}

Puoi creare una nuova azione di marketing effettuando una richiesta di PUT al `/marketingActions/custom/` e fornendo un nome per l’azione di marketing alla fine del percorso della richiesta.

**Formato API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome della nuova azione di marketing che desideri creare. Questo nome agisce come identificatore principale dell’azione di marketing e deve quindi essere univoco. Si consiglia di assegnare all’azione di marketing un nome descrittivo ma conciso. |

**Richiesta**

La richiesta seguente crea una nuova azione di marketing personalizzata denominata &quot;exportToThirdParty&quot;. Tieni presente che `name` nel payload della richiesta è lo stesso nome fornito nel percorso della richiesta.

```shell
curl -X PUT \  
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "exportToThirdParty",
      "description": "Export data to a third party"
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome dell’azione di marketing che desideri creare. Questo nome deve corrispondere al nome fornito nel percorso della richiesta, altrimenti si verificherà un errore 400 (Richiesta non valida). |
| `description` | Descrizione dell’azione di marketing leggibile dall’utente. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e i dettagli dell’azione di marketing appena creata.

```json
{
    "name": "exportToThirdParty",
    "description": "Export data to a third party",
    "imsOrg": "{ORG_ID}",
    "created": 1550713341915,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER",
    "updated": 1550713856390,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
        }
    }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `_links.self.href` | ID URI dell’azione di marketing. |

Registra l&#39;ID URI dell&#39;azione di marketing appena creata, in modo che venga utilizzato nel passaggio successivo della creazione di un criterio.

## Creare un criterio {#create-policy}

La creazione di un nuovo criterio richiede di fornire l’ID URI di un’azione di marketing con un’espressione delle etichette di utilizzo che ne vietano l’azione di marketing.

Questa espressione è denominata espressione di criterio e è un oggetto contenente (A) un&#39;etichetta o (B) un operatore e operandi, ma non entrambi. A sua volta, ogni operando è anche un oggetto espressione di criterio. Ad esempio, una politica relativa all’esportazione di dati verso terzi potrebbe essere vietata se `C1 OR (C3 AND C7)` le etichette sono presenti. Questa espressione viene specificata come:

```json
"deny": {
  "operator": "OR",
  "operands": [
    {
      "label": "C1"
    },
    {
      "operator": "AND",
      "operands": [
        {
          "label": "C3"
        },
        {
          "label": "C7"
        }
      ]
    }
  ]
}
```

>[!NOTE]
>
>Sono supportati solo gli operatori OR e AND .

Dopo aver configurato l’espressione del criterio, puoi creare un nuovo criterio effettuando una richiesta di POST al `/policies/custom` punto finale.

**Formato API**

```http
POST /policies/custom
```

**Richiesta**

La seguente richiesta crea un criterio denominato &quot;Esporta dati a terze parti&quot; fornendo un’azione di marketing e un’espressione di policy nel payload della richiesta.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
      "../marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
      "operator": "OR",
      "operands": [
        {"label": "C1"},
        {
          "operator": "AND",
          "operands": [
            {"label": "C3"},
            {"label": "C7"}
          ]
        }
      ]
    }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `marketingActionRefs` | Una matrice contenente `href` valore di un’azione di marketing, ottenuta [passaggio precedente](#define-action). Anche se nell’esempio precedente è elencata una sola azione di marketing, è possibile fornire più azioni. |
| `deny` | L&#39;oggetto espressione policy. Definisce le etichette di utilizzo e le condizioni che causerebbero il rifiuto dell&#39;azione di marketing a cui si fa riferimento in `marketingActionRefs`. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e i dettagli del criterio appena creato.

```json
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "OR",
        "operands": [
            {
                "label": "C1"
            },
            {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "C7"
                    }
                ]
            }
        ]
    },
    "imsOrg": "{ORG_ID}",
    "created": 1565651746693,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER",
    "updated": 1565651746693,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
    },
    "id": "5d51f322e553c814e67af1a3"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | Valore generato dal sistema di sola lettura che identifica il criterio in modo univoco. |

Registra l&#39;ID URI del criterio appena creato, in modo che venga utilizzato nel passaggio successivo per abilitare il criterio.

## Abilitare il criterio

>[!NOTE]
>
>Anche se questo passaggio è facoltativo se desideri lasciare il criterio in `DRAFT` stato: per impostazione predefinita, lo stato di un criterio deve essere impostato su `ENABLED` per partecipare alla valutazione. Consulta la guida su [applicazione delle norme](../enforcement/api-enforcement.md) per informazioni su come fare eccezioni per i criteri in `DRAFT` stato.

Per impostazione predefinita, i criteri con le relative `status` proprietà impostata su `DRAFT` non partecipare alla valutazione. Puoi abilitare il criterio per la valutazione effettuando una richiesta PATCH al `/policies/custom/` e fornisce l&#39;identificatore univoco per il criterio alla fine del percorso della richiesta.

**Formato API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | La `id` valore del criterio che si desidera abilitare. |

**Richiesta**

La seguente richiesta esegue un’operazione PATCH sul `status` proprietà del criterio, modifica del valore da `DRAFT` a `ENABLED`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    {
      "op": "replace",
      "path": "/status",
      "value": "ENABLED"
    }
  ]'
```

| Proprietà | Descrizione |
| --- | --- |
| `op` | Tipo di operazione PATCH da eseguire. Questa richiesta esegue un&#39;operazione di &quot;sostituzione&quot;. |
| `path` | Percorso del campo da aggiornare. Quando si abilita un criterio, il valore deve essere impostato su &quot;/status&quot;. |
| `value` | Il nuovo valore da assegnare alla proprietà specificata in `path`. Questa richiesta imposta il `status` su &quot;ENABLED&quot;. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 (OK) e i dettagli del criterio aggiornato, con i relativi `status` ora impostato su `ENABLED`.

```json
{
    "name": "Export Data to Third Party",
    "status": "ENABLED",
    "marketingActionRefs": [
        "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "OR",
        "operands": [
            {
                "label": "C1"
            },
            {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "C7"
                    }
                ]
            }
        ]
    },
    "imsOrg": "{ORG_ID}",
    "created": 1565651746693,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER}",
    "updated": 1565723012139,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
    },
    "id": "5d51f322e553c814e67af1a3"
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente un criterio di utilizzo dei dati per un’azione di marketing. Ora puoi continuare l’esercitazione su [applicazione dei criteri di utilizzo dei dati](../enforcement/api-enforcement.md) per scoprire come verificare le violazioni dei criteri e gestirle nell&#39;applicazione di esperienza.

Per ulteriori informazioni sulle diverse operazioni disponibili nella [!DNL Policy Service] API, vedi [Guida per gli sviluppatori di Policy Service](../api/getting-started.md). Per informazioni su come applicare i criteri per [!DNL Real-Time Customer Profile] data, consulta l’esercitazione su [applicazione della conformità in materia di utilizzo dei dati per i segmenti di pubblico](../../segmentation/tutorials/governance.md).

Per scoprire come gestire i criteri di utilizzo in [!DNL Experience Platform] interfaccia utente, vedi [guida utente di policy](user-guide.md).
