---
keywords: Experience Platform;home;argomenti popolari;governance dei dati;criteri di utilizzo dei dati
solution: Experience Platform
title: Creare un criterio di governance dei dati nell’API
type: Tutorial
description: Scopri come creare un criterio di governance dei dati utilizzando l’API del servizio criteri.
exl-id: 8483f8a1-efe8-4ebb-b074-e0577e5a81a4
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 3%

---

# Creare un criterio di governance dei dati nell’API

Il [API del servizio criteri](https://www.adobe.io/experience-platform-apis/references/policy-service/) consente di creare e gestire criteri di governance dei dati per determinare quali azioni di marketing possono essere eseguite sui dati che contengono determinate etichette di utilizzo dei dati.

Questo documento fornisce un tutorial dettagliato per la creazione di un criterio di governance utilizzando [!DNL Policy Service] API.

>[!NOTE]
>
>Per informazioni su come creare un criterio di controllo degli accessi, vedere `/policies` guida dell’endpoint per [API di controllo degli accessi](../../access-control/abac/api/policies.md). Per informazioni su come creare un criterio di consenso, consulta la [guida all’interfaccia utente dei criteri](./user-guide.md#consent-policy).

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti concetti chiave coinvolti nella creazione e nella valutazione delle policy:

* [Governance dei dati Adobe Experience Platform](../home.md): framework tramite il quale [!DNL Platform] applica la conformità all’utilizzo dei dati.
   * [Etichette di utilizzo dati](../labels/overview.md): le etichette di utilizzo dei dati vengono applicate ai campi dati XDM, specificando restrizioni sulla modalità di accesso ai dati.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Platform] organizza i dati sull’esperienza del cliente.
* [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Prima di iniziare questo tutorial, controlla [guida per sviluppatori](../api/getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate al [!DNL Policy Service] API, incluse le intestazioni richieste e la modalità di lettura delle chiamate API di esempio.

## Definire un’azione di marketing {#define-action}

Nel framework per la governance dei dati, un’azione di marketing è un’azione che [!DNL Experience Platform] dati richiesti dal consumatore, per i quali è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati.

Il primo passaggio nella creazione di un criterio di utilizzo dei dati consiste nel determinare l’azione di marketing che verrà valutata dal criterio. Questa operazione può essere eseguita utilizzando una delle seguenti opzioni:

* [Cercare un’azione di marketing esistente](#look-up)
* [Creare una nuova azione di marketing](#create-new)

### Cercare un’azione di marketing esistente {#look-up}

Per cercare le azioni di marketing esistenti da valutare in base ai criteri, devi effettuare una richiesta GET a una delle `/marketingActions` endpoint.

**Formato API**

A seconda che tu stia cercando un’azione di marketing fornita da [!DNL Experience Platform] o un’azione di marketing personalizzata creata dalla tua organizzazione, utilizza `marketingActions/core` o `marketingActions/custom` endpoint, rispettivamente.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Richiesta**

La richiesta seguente utilizza `marketingActions/custom` endpoint, che recupera un elenco di tutte le azioni di marketing definite dall’organizzazione IMS.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce il numero totale di azioni di marketing trovate (`count`) ed elenca i dettagli delle azioni di marketing stesse all’interno del `children` array.

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
| `_links.self.href` | Ogni elemento all&#39;interno del `children` l’array contiene un ID URI per l’azione di marketing elencata. |

Quando trovi l’azione di marketing da utilizzare, registra il valore dei relativi `href` proprietà. Questo valore viene utilizzato durante il passaggio successivo di [creazione di una policy](#create-policy).

### Creare una nuova azione di marketing {#create-new}

Per creare una nuova azione di marketing, devi effettuare una richiesta PUT al `/marketingActions/custom/` e fornendo un nome per l’azione di marketing alla fine del percorso della richiesta.

**Formato API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome della nuova azione di marketing da creare. Questo nome funge da identificatore principale dell’azione di marketing e deve quindi essere univoco. Si consiglia di assegnare all’azione di marketing un nome descrittivo ma conciso. |

**Richiesta**

La richiesta seguente crea una nuova azione di marketing personalizzata denominata &quot;exportToThirdParty&quot;. Tieni presente che `name` nel payload della richiesta corrisponde al nome fornito nel percorso della richiesta.

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
| `name` | Nome dell’azione di marketing da creare. Questo nome deve corrispondere al nome fornito nel percorso della richiesta, altrimenti si verificherà un errore 400 (Richiesta non valida). |
| `description` | Una descrizione leggibile dell’azione di marketing. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 (Creato) e i dettagli dell’azione di marketing appena creata.

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

Registra l’ID URI dell’azione di marketing appena creata, in quanto verrà utilizzata nel passaggio successivo della creazione di un criterio.

## Creare un criterio {#create-policy}

Per creare un nuovo criterio è necessario fornire all’ID URI di un’azione di marketing un’espressione delle etichette di utilizzo che impediscono tale azione di marketing.

Questa espressione viene definita espressione di criteri ed è un oggetto contenente (A) un&#39;etichetta oppure (B) un operatore e operandi, ma non entrambi. A sua volta, ogni operando è anche un oggetto espressione di criteri. Ad esempio, una politica relativa all’esportazione di dati a terzi potrebbe essere vietata se `C1 OR (C3 AND C7)` sono presenti etichette. Questa espressione viene specificata come:

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
>Sono supportati solo gli operatori OR e AND.

Dopo aver configurato l’espressione dei criteri, puoi creare un nuovo criterio effettuando una richiesta POST al `/policies/custom` endpoint.

**Formato API**

```http
POST /policies/custom
```

**Richiesta**

La richiesta seguente crea un criterio denominato &quot;Export Data to Third Party&quot; (Esporta dati a terze parti) fornendo un’azione di marketing e un’espressione di criterio nel payload della richiesta.

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
| `marketingActionRefs` | Un array contenente `href` valore di un’azione di marketing, ottenuto nel [passaggio precedente](#define-action). Nell’esempio precedente è elencata una sola azione di marketing, ma è possibile specificare anche più azioni. |
| `deny` | L’oggetto espressione criterio. Definisce le etichette e le condizioni di utilizzo che causerebbero il rifiuto da parte del criterio dell’azione di marketing a cui si fa riferimento in `marketingActionRefs`. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 (Creato) e i dettagli del criterio appena creato.

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
| `id` | Valore di sola lettura generato dal sistema che identifica in modo univoco il criterio. |

Registra l’ID URI del criterio appena creato, in quanto viene utilizzato nel passaggio successivo per abilitare il criterio.

## Abilita il criterio

>[!NOTE]
>
>Questo passaggio è facoltativo se desideri lasciare i criteri in `DRAFT` per impostazione predefinita, lo stato di un criterio deve essere impostato su `ENABLED` per partecipare alla valutazione. Consulta la guida su [applicazione dei criteri](../enforcement/api-enforcement.md) per informazioni su come creare eccezioni per i criteri in `DRAFT` stato.

Per impostazione predefinita, i criteri con `status` proprietà impostata su `DRAFT` non partecipano alla valutazione. Per abilitare il criterio per la valutazione, devi effettuare una richiesta PATCH al `/policies/custom/` e fornendo l’identificatore univoco per il criterio alla fine del percorso della richiesta.

**Formato API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | Il `id` valore del criterio che si desidera abilitare. |

**Richiesta**

La richiesta seguente esegue un’operazione PATCH sul `status` della policy, modificandone il valore da `DRAFT` a `ENABLED`.

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
| `path` | Percorso del campo da aggiornare. Quando si abilita una policy, il valore deve essere impostato su &quot;/status&quot;. |
| `value` | Il nuovo valore da assegnare alla proprietà specificata in `path`. Questa richiesta imposta i `status` su &quot;ENABLED&quot;. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 (OK) e i dettagli del criterio aggiornato, con i relativi `status` ora impostato su `ENABLED`.

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

Seguendo questa esercitazione, hai creato correttamente un criterio di utilizzo dei dati per un’azione di marketing. Ora puoi continuare l’esercitazione su [applicazione dei criteri di utilizzo dei dati](../enforcement/api-enforcement.md) per scoprire come verificare la presenza di violazioni dei criteri e gestirle nell’applicazione experience.

Per ulteriori informazioni sulle diverse operazioni disponibili nella sezione [!DNL Policy Service] API, consulta [Guida per gli sviluppatori di Policy Service](../api/getting-started.md). Per informazioni su come applicare i criteri per [!DNL Real-Time Customer Profile] dati, consulta l’esercitazione su [applicazione della conformità all’utilizzo dei dati per i segmenti di pubblico](../../segmentation/tutorials/governance.md).

Per informazioni su come gestire i criteri di utilizzo in [!DNL Experience Platform] interfaccia utente, consulta [guida utente dei criteri](user-guide.md).
