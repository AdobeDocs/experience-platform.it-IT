---
keywords: Experience Platform;home;argomenti popolari;Applicazione delle policy;applicazione basata su API;governance dei dati
solution: Experience Platform
title: Endpoint API per i criteri di governance dei dati
description: I criteri di governance dei dati sono regole adottate dall’organizzazione che descrivono i tipi di azioni di marketing che possono essere eseguiti o meno sui dati di Experienci Platform. L’endpoint /policies viene utilizzato per tutte le chiamate API relative alla visualizzazione, alla creazione, all’aggiornamento o all’eliminazione dei criteri di governance dei dati.
role: Developer
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 3%

---

# Endpoint &quot;data governance policies&quot;

I criteri di governance dei dati sono regole che descrivono i tipi di azioni di marketing che possono essere eseguiti o meno sui dati in [!DNL Experience Platform]. Il `/policies` endpoint nella [!DNL Policy Service API] consente di gestire in modo programmatico i criteri di governance dei dati per la tua organizzazione.

>[!IMPORTANT]
>
>I criteri di governance non devono essere confusi con i criteri di controllo dell’accesso, che determinano gli attributi di dati specifici a cui possono accedere alcuni utenti di Platform nella tua organizzazione. Consulta la sezione `/policies` guida dell’endpoint per [API di controllo degli accessi](../../access-control/abac/api/policies.md) per informazioni dettagliate su come gestire in modo programmatico i criteri di controllo degli accessi.

## Introduzione

L’endpoint API utilizzato in questa guida fa parte del [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Prima di continuare, controlla [guida introduttiva](getting-started.md) per collegamenti alla documentazione correlata, una guida per la lettura delle chiamate API di esempio di questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a [!DNL Experience Platform] API.

## Recuperare un elenco di criteri {#list}

Puoi elencare tutti `core` o `custom` criteri effettuando una richiesta GET a `/policies/core` o `/policies/custom`, rispettivamente.

**Formato API**

```http
GET /policies/core
GET /policies/custom
```

**Richiesta**

La richiesta seguente recupera un elenco di criteri personalizzati definiti dall’organizzazione.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta include `children` array che elenca i dettagli di ogni criterio recuperato, inclusi i relativi `id` valori. È possibile utilizzare `id` campo di una particolare policy da eseguire [ricerca](#lookup), [aggiorna](#update), e [eliminare](#delete) richieste per tale criterio.

```JSON
{
    "_page": {
        "start": "5c6dacdf685a4913dc48937c",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/policies/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "Export Data to Third Party",
            "status": "DRAFT",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "OR",
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
            "created": 1550691551888,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550701472910,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
                }
            },
            "id": "5c6dacdf685a4913dc48937c"
        },
        {
            "name": "Combine Data",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
            ],
            "description": "Data that meets these conditions cannot be combined.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "I1"
                    }
                ]
            },
            "imsOrg": "{ORG_ID}",
            "created": 1550703519823,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550714340335,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb9f5c404513dc2dc454"
                }
            },
            "id": "5c6ddb9f5c404513dc2dc454"
        }
    ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `_page.count` | Numero totale di criteri recuperati. |
| `name` | Nome visualizzato di un criterio. |
| `status` | Stato corrente di un criterio. Esistono tre stati possibili: `DRAFT`, `ENABLED`, o `DISABLED`. Per impostazione predefinita, solo `ENABLED` Le politiche partecipano alla valutazione. Consulta la panoramica su [valutazione dei criteri](../enforcement/overview.md) per ulteriori informazioni. |
| `marketingActionRefs` | Array che elenca gli URI di tutte le azioni di marketing applicabili a un criterio. |
| `description` | Descrizione facoltativa che fornisce ulteriore contesto al caso d’uso del criterio. |
| `deny` | Oggetto che descrive le etichette di utilizzo dei dati specifiche su cui l’azione di marketing associata a un criterio non può essere eseguita. Consulta la sezione su [creazione di una policy](#create-policy) per ulteriori informazioni su questa proprietà. |

## Cercare un criterio {#look-up}

Per cercare un criterio specifico, includi i `id` nel percorso di una richiesta GET.

**Formato API**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | Il `id` della policy che desideri cercare. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del criterio.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "operator": "OR",
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
    "created": 1550703519823,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550714340335,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome visualizzato del criterio. |
| `status` | Stato corrente del criterio. Esistono tre stati possibili: `DRAFT`, `ENABLED`, o `DISABLED`. Per impostazione predefinita, solo `ENABLED` Le politiche partecipano alla valutazione. Consulta la panoramica su [valutazione dei criteri](../enforcement/overview.md) per ulteriori informazioni. |
| `marketingActionRefs` | Array che elenca gli URI di tutte le azioni di marketing applicabili per il criterio. |
| `description` | Descrizione facoltativa che fornisce ulteriore contesto al caso d’uso del criterio. |
| `deny` | Oggetto che descrive le etichette di utilizzo dei dati specifiche su cui l’azione di marketing associata al criterio non può essere eseguita. Consulta la sezione su [creazione di una policy](#create-policy) per ulteriori informazioni su questa proprietà. |

## Creare un criterio personalizzato {#create-policy}

In [!DNL Policy Service] API, un criterio è definito dai seguenti elementi:

* Riferimento a una specifica azione di marketing
* Espressione che descrive le etichette di utilizzo dei dati per le quali l’azione di marketing non può essere eseguita

Per soddisfare quest’ultimo requisito, le definizioni dei criteri devono includere un’espressione booleana relativa alla presenza di etichette di utilizzo dei dati. Questa espressione viene definita espressione di criteri.

Le espressioni dei criteri sono fornite sotto forma di `deny` all&#39;interno di ogni definizione di criterio. Un esempio di semplice `deny` l&#39;oggetto che controlla solo la presenza di una singola etichetta sarà simile al seguente:

```json
"deny": {
    "label": "C1"
}
```

Tuttavia, molti criteri specificano condizioni più complesse per quanto riguarda la presenza di etichette di utilizzo dei dati. Per supportare questi casi d’uso, puoi anche includere operazioni booleane per descrivere le espressioni dei criteri. L’oggetto espressione dei criteri deve contenere un’etichetta o un operatore e operandi, ma non entrambi. A sua volta, ogni operando è anche un oggetto espressione di criteri.

Ad esempio, per definire un criterio che vieta l’esecuzione di un’azione di marketing su dati in cui `C1 OR (C3 AND C7)` sono presenti le etichette, le `deny` la proprietà viene specificata come:

```JSON
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
```

| Proprietà | Descrizione |
| --- | --- |
| `operator` | Indica la relazione condizionale tra le etichette fornite nel pari livello `operands` array. I valori accettati sono: <ul><li>`OR`: l’espressione restituisce true se una qualsiasi delle etichette in `operands` sono presenti.</li><li>`AND`: l’espressione restituisce true solo se tutte le etichette in `operands` sono presenti.</li></ul> |
| `operands` | Matrice di oggetti, in cui ogni oggetto rappresenta una singola etichetta o una coppia aggiuntiva di `operator` e `operands` proprietà. La presenza delle etichette e/o delle operazioni in un `operands` l’array viene risolto in true o false in base al valore del relativo pari livello `operator` proprietà. |
| `label` | Nome di una singola etichetta di utilizzo dati che si applica al criterio. |

Per creare un nuovo criterio personalizzato, devi effettuare una richiesta POST al `/policies/custom` endpoint.

**Formato API**

```http
POST /policies/custom
```

**Richiesta**

La richiesta seguente crea un nuovo criterio che limita l’azione di marketing `exportToThirdParty` da eseguire sui dati contenenti etichette `C1 OR (C3 AND C7)`.

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
          "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
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
| `name` | Nome visualizzato del criterio. |
| `status` | Stato corrente del criterio. Esistono tre stati possibili: `DRAFT`, `ENABLED`, o `DISABLED`. Per impostazione predefinita, solo `ENABLED` Le politiche partecipano alla valutazione. Consulta la panoramica su [valutazione dei criteri](../enforcement/overview.md) per ulteriori informazioni. |
| `marketingActionRefs` | Array che elenca gli URI di tutte le azioni di marketing applicabili per il criterio. L’URI per un’azione di marketing viene fornito in `_links.self.href` nella risposta per [ricerca di un’azione di marketing](./marketing-actions.md#look-up). |
| `description` | Descrizione facoltativa che fornisce ulteriore contesto al caso d’uso del criterio. |
| `deny` | L’espressione dei criteri che descrive le etichette di utilizzo dei dati specifiche per le quali l’azione di marketing associata al criterio non può essere eseguita. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del criterio appena creato, inclusi i relativi `id`. Questo valore è di sola lettura e viene assegnato automaticamente al momento della creazione del criterio.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
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
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550691551888,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Aggiornare un criterio personalizzato {#update}

>[!IMPORTANT]
>
>Puoi aggiornare solo i criteri personalizzati. Se desideri abilitare o disabilitare i criteri di base, consulta la sezione su [aggiornamento dell’elenco dei criteri di base abilitati](#update-enabled-core).

Per aggiornare un criterio personalizzato esistente, devi fornire il relativo ID nel percorso di una richiesta PUT con un payload che includa l’intero modulo aggiornato del criterio. In altre parole, la richiesta PUT riscrive essenzialmente il criterio.

>[!NOTE]
>
>Consulta la sezione su [aggiornamento di una parte di una policy personalizzata](#patch) se desideri solo aggiornare uno o più campi per un criterio, anziché sovrascriverlo.

**Formato API**

```http
PUT /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | Il `id` del criterio che desideri aggiornare. |

**Richiesta**

In questo esempio, le condizioni per l’esportazione di dati a terze parti sono cambiate e ora è necessario utilizzare il criterio creato per rifiutare questa azione di marketing se `C1 AND C5` le etichette dati sono presenti.

La richiesta seguente aggiorna il criterio esistente in modo da includere la nuova espressione del criterio. Poiché questa richiesta riscrive essenzialmente il criterio, tutti i campi devono essere inclusi nel payload, anche se alcuni dei loro valori non vengono aggiornati.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
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
          "operator": "AND",
          "operands": [
            {"label": "C1"},
            {"label": "C5"}
          ]
        }
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome visualizzato del criterio. |
| `status` | Stato corrente del criterio. Esistono tre stati possibili: `DRAFT`, `ENABLED`, o `DISABLED`. Per impostazione predefinita, solo `ENABLED` Le politiche partecipano alla valutazione. Consulta la panoramica su [valutazione dei criteri](../enforcement/overview.md) per ulteriori informazioni. |
| `marketingActionRefs` | Array che elenca gli URI di tutte le azioni di marketing applicabili per il criterio. L’URI per un’azione di marketing viene fornito in `_links.self.href` nella risposta per [ricerca di un’azione di marketing](./marketing-actions.md#look-up). |
| `description` | Descrizione facoltativa che fornisce ulteriore contesto al caso d’uso del criterio. |
| `deny` | L’espressione dei criteri che descrive le etichette di utilizzo dei dati specifiche per le quali l’azione di marketing associata al criterio non può essere eseguita. Consulta la sezione su [creazione di una policy](#create-policy) per ulteriori informazioni su questa proprietà. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del criterio aggiornato.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/core/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "label": "C5"
            }
        ]
    },
    "imsOrg": "{ORG_ID}",
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550701472910,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Aggiornare una parte di un criterio personalizzato {#patch}

>[!IMPORTANT]
>
>Puoi aggiornare solo i criteri personalizzati. Se desideri abilitare o disabilitare i criteri di base, consulta la sezione su [aggiornamento dell’elenco dei criteri di base abilitati](#update-enabled-core).

È possibile aggiornare una parte specifica di un criterio utilizzando una richiesta PATCH. A differenza delle richieste PUT che riscrivono il criterio, le richieste PATCH aggiornano solo le proprietà specificate nel corpo della richiesta. Questa funzione è particolarmente utile quando si desidera abilitare o disabilitare una policy, in quanto è necessario fornire solo il percorso della proprietà appropriata (`/status`) e il relativo valore (`ENABLED` o `DISABLED`).

>[!NOTE]
>
>I payload per le richieste PATCH seguono la formattazione Patch JSON. Consulta la [Guida di base sulle API](../../landing/api-fundamentals.md) per ulteriori informazioni sulla sintassi accettata.

Il [!DNL Policy Service] API supporta le operazioni Patch JSON `add`, `remove`, e `replace`, e consente di combinare diversi aggiornamenti in una singola chiamata, come mostrato nell’esempio seguente.

**Formato API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | Il `id` del criterio di cui desideri aggiornare le proprietà. |

**Richiesta**

La richiesta seguente utilizza due `replace` operazioni da cui modificare lo stato dei criteri `DRAFT` a `ENABLED`, e per aggiornare `description` con una nuova descrizione.

>[!IMPORTANT]
>
>Quando si inviano più operazioni PATCH in una singola richiesta, queste vengono elaborate nell’ordine in cui compaiono nell’array. Se necessario, assicurati di inviare le richieste nell’ordine corretto.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' [
          {
            "op": "replace",
            "path": "/status",
            "value": "ENABLED"
          },
          {
            "op": "replace",
            "path": "/description",
            "value": "New policy description."
          }
        ]'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del criterio aggiornato.


```JSON
{
    "name": "Export Data to Third Party",
    "status": "ENABLED",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "New policy description.",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "operator": "OR",
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
    "created": 1550703519823,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550712163182,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Eliminare un criterio personalizzato {#delete}

Per eliminare un criterio personalizzato, devi includere `id` nel percorso di una richiesta DELETE.

>[!WARNING]
>
>Una volta eliminati, i criteri non possono essere recuperati. Si consiglia di [eseguire una richiesta di ricerca (GET)](#lookup) per prima cosa, visualizzare il criterio e confermarne la correttezza.

**Formato API**

```http
DELETE /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | ID del criterio che desideri eliminare. |

**Richiesta**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 (OK) con un corpo vuoto.

Per confermare l’eliminazione, prova a cercare (GET) nuovamente il criterio. Se il criterio è stato eliminato correttamente, dovrebbe essere visualizzato un errore HTTP 404 (Non trovato).

## Recuperare un elenco di criteri di base abilitati {#list-enabled-core}

Per impostazione predefinita, solo i criteri di governance dei dati abilitati partecipano alla valutazione. Per recuperare un elenco dei criteri di base attualmente abilitati dalla tua organizzazione, effettua una richiesta GET al `/enabledCorePolicies` endpoint.

**Formato API**

```http
GET /enabledCorePolicies
```

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce l’elenco dei criteri di base abilitati in una `policyIds` array.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0003",
    "corepolicy_0004",
    "corepolicy_0005",
    "corepolicy_0006",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{ORG_ID}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## Aggiorna l’elenco dei criteri di base abilitati {#update-enabled-core}

Per impostazione predefinita, solo i criteri di governance dei dati abilitati partecipano alla valutazione. Effettuando una richiesta PUT al `/enabledCorePolicies` endpoint, puoi aggiornare l’elenco dei criteri di base abilitati per la tua organizzazione utilizzando una singola chiamata.

>[!NOTE]
>
>Solo i criteri di base possono essere abilitati o disabilitati da questo endpoint. Per abilitare o disabilitare i criteri personalizzati, consulta la sezione su [aggiornamento di una parte di una policy](#patch).

**Formato API**

```http
PUT /enabledCorePolicies
```

**Richiesta**

La richiesta seguente aggiorna l’elenco dei criteri di base abilitati in base agli ID forniti nel payload.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "policyIds": [
          "corepolicy_0001",
          "corepolicy_0002",
          "corepolicy_0007",
          "corepolicy_0008"
        ]
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `policyIds` | Elenco degli ID dei criteri di base da abilitare. Tutti i criteri di base non inclusi sono impostati su `DISABLED` e non parteciperà alla valutazione. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’elenco aggiornato dei criteri di base abilitati in una `policyIds` array.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{ORG_ID}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1595876052649,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## Passaggi successivi

Dopo aver definito nuovi criteri o aggiornato quelli esistenti, puoi utilizzare [!DNL Policy Service] API per testare le azioni di marketing rispetto a etichette o set di dati specifici e per verificare se i criteri generano violazioni come previsto. Consulta la guida sulla [endpoint di valutazione dei criteri](./evaluation.md) per ulteriori informazioni.
