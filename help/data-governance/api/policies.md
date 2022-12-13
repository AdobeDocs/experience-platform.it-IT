---
keywords: Experience Platform;home;argomenti popolari;applicazione dei criteri;applicazione basata su API;governance dei dati
solution: Experience Platform
title: Endpoint API per i criteri di governance dei dati
topic-legacy: developer guide
description: I criteri di governance dei dati sono regole adottate dalla tua organizzazione che descrivono il tipo di azioni di marketing che ti è permesso o da cui ti sono limitati nell’eseguire sui dati all’interno di un Experience Platform. L’endpoint /policy viene utilizzato per tutte le chiamate API relative alla visualizzazione, alla creazione, all’aggiornamento o all’eliminazione dei criteri di governance dei dati.
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 3%

---

# Endpoint per criteri di governance dei dati

I criteri di governance dei dati sono regole che descrivono i tipi di azioni di marketing che ti sono consentite o a cui ti è consentito eseguire sui dati all’interno di [!DNL Experience Platform]. La `/policies` punto finale [!DNL Policy Service API] consente di gestire in modo programmatico i criteri di governance dei dati per la tua organizzazione.

>[!IMPORTANT]
>
>I criteri di governance non devono essere confusi con i criteri di controllo degli accessi, che determinano gli attributi di dati specifici a cui possono accedere alcuni utenti di Platform nella tua organizzazione. Fai riferimento a `/policies` guida dell&#39;endpoint per [API di controllo accessi](../../access-control/abac/api/policies.md) per informazioni su come gestire in modo programmatico i criteri di controllo accessi.

## Introduzione

L’endpoint API utilizzato in questa guida fa parte del [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Prima di continuare, controlla la [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio presenti in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi [!DNL Experience Platform] API.

## Recupera un elenco di criteri {#list}

È possibile elencare tutti `core` o `custom` , richiedendo la GET a `/policies/core` o `/policies/custom`, rispettivamente.

**Formato API**

```http
GET /policies/core
GET /policies/custom
```

**Richiesta**

La richiesta seguente recupera un elenco di criteri personalizzati definiti dall&#39;organizzazione.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta include un `children` array in cui sono elencati i dettagli di ciascun criterio recuperato, inclusi i relativi `id` valori. È possibile utilizzare `id` campo di una particolare politica da eseguire [ricerca](#lookup), [update](#update)e [delete](#delete) richieste di tale politica.

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
| `status` | Lo stato corrente di un criterio. Sono disponibili tre stati possibili: `DRAFT`, `ENABLED`oppure `DISABLED`. Per impostazione predefinita, solo `ENABLED` Le politiche partecipano alla valutazione. Vedi la panoramica su [valutazione politica](../enforcement/overview.md) per ulteriori informazioni. |
| `marketingActionRefs` | Matrice che elenca gli URI di tutte le azioni di marketing applicabili per un criterio. |
| `description` | Una descrizione facoltativa che fornisce ulteriore contesto al caso d’uso del criterio. |
| `deny` | Un oggetto che descrive le etichette di utilizzo dati specifiche per le quali è stata limitata l&#39;esecuzione dell&#39;azione di marketing associata a un criterio. Vedi la sezione su [creazione di un criterio](#create-policy) per ulteriori informazioni su questa proprietà. |

## Cercare una politica {#look-up}

Puoi cercare una politica specifica includendo quella `id` nel percorso di una richiesta GET.

**Formato API**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | La `id` della politica che si desidera cercare. |

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

Una risposta corretta restituisce i dettagli del criterio.

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
| `status` | Stato corrente del criterio. Sono disponibili tre stati possibili: `DRAFT`, `ENABLED`oppure `DISABLED`. Per impostazione predefinita, solo `ENABLED` Le politiche partecipano alla valutazione. Vedi la panoramica su [valutazione politica](../enforcement/overview.md) per ulteriori informazioni. |
| `marketingActionRefs` | Matrice che elenca gli URI di tutte le azioni di marketing applicabili al criterio. |
| `description` | Una descrizione facoltativa che fornisce ulteriore contesto al caso d’uso del criterio. |
| `deny` | Un oggetto che descrive le etichette di utilizzo dei dati specifiche sulle quali l&#39;azione di marketing associata al criterio non viene eseguita. Vedi la sezione su [creazione di un criterio](#create-policy) per ulteriori informazioni su questa proprietà. |

## Creare un criterio personalizzato {#create-policy}

In [!DNL Policy Service] API, un criterio è definito dai seguenti elementi:

* Riferimento a una specifica azione di marketing
* Un&#39;espressione che descrive le etichette di utilizzo dei dati su cui è limitata l&#39;esecuzione dell&#39;azione di marketing

Per soddisfare quest’ultimo requisito, le definizioni dei criteri devono includere un’espressione booleana relativa alla presenza di etichette di utilizzo dei dati. Questa espressione è denominata espressione di criterio.

Le espressioni di criterio vengono fornite sotto forma di `deny` all&#39;interno di ogni definizione di criterio. Esempio di un semplice `deny` un oggetto che controlla solo la presenza di una singola etichetta avrà un aspetto simile al seguente:

```json
"deny": {
    "label": "C1"
}
```

Tuttavia, molti criteri specificano condizioni più complesse relative alla presenza di etichette per l’utilizzo dei dati. Per supportare questi casi d’uso, puoi anche includere le operazioni booleane per descrivere le espressioni dei criteri. L&#39;oggetto espressione policy deve contenere un&#39;etichetta o un operatore e operandi, ma non entrambi. A sua volta, ogni operando è anche un oggetto espressione di criterio.

Ad esempio, per definire un criterio che vieta l’esecuzione di un’azione di marketing sui dati in cui `C1 OR (C3 AND C7)` le etichette sono presenti, le `deny` viene specificata come:

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
| `operator` | Indica la relazione condizionale tra le etichette fornite nel pari livello `operands` array. I valori accettati sono: <ul><li>`OR`: L&#39;espressione restituisce true se una delle etichette nel campo `operands` sono presenti array.</li><li>`AND`: L&#39;espressione viene risolta in true solo se tutte le etichette nel `operands` sono presenti array.</li></ul> |
| `operands` | Matrice di oggetti, con ogni oggetto che rappresenta una singola etichetta o una coppia aggiuntiva `operator` e `operands` proprietà. Presenza delle etichette e/o delle operazioni in un `operands` viene risolto in true o false in base al valore del relativo elemento di pari livello `operator` proprietà. |
| `label` | Nome di un&#39;etichetta di utilizzo dati singola applicata al criterio. |

Puoi creare un nuovo criterio personalizzato effettuando una richiesta di POST al `/policies/custom` punto finale.

**Formato API**

```http
POST /policies/custom
```

**Richiesta**

La seguente richiesta crea un nuovo criterio che limita l’azione di marketing `exportToThirdParty` da eseguire su dati contenenti etichette `C1 OR (C3 AND C7)`.

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
| `status` | Stato corrente del criterio. Sono disponibili tre stati possibili: `DRAFT`, `ENABLED`oppure `DISABLED`. Per impostazione predefinita, solo `ENABLED` Le politiche partecipano alla valutazione. Vedi la panoramica su [valutazione politica](../enforcement/overview.md) per ulteriori informazioni. |
| `marketingActionRefs` | Matrice che elenca gli URI di tutte le azioni di marketing applicabili al criterio. L’URI per un’azione di marketing viene fornito in `_links.self.href` nella risposta per [ricerca di un’azione di marketing](./marketing-actions.md#look-up). |
| `description` | Una descrizione facoltativa che fornisce ulteriore contesto al caso d’uso del criterio. |
| `deny` | L&#39;espressione di criterio che descrive le etichette di utilizzo dati specifiche per le azioni di marketing associate al criterio non viene eseguita. |

**Risposta**

Una risposta corretta restituisce i dettagli del criterio appena creato, incluso il relativo `id`. Questo valore è di sola lettura e viene assegnato automaticamente alla creazione del criterio.

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
>È possibile aggiornare solo i criteri personalizzati. Per abilitare o disabilitare i criteri di base, consulta la sezione [aggiornamento dell&#39;elenco dei criteri di base abilitati](#update-enabled-core).

Puoi aggiornare un criterio personalizzato esistente fornendo il relativo ID nel percorso di una richiesta di PUT con un payload che include la versione aggiornata del criterio nella sua interezza. In altre parole, la richiesta di PUT sostanzialmente riscrive il criterio.

>[!NOTE]
>
>Vedi la sezione su [aggiornamento di una parte di un criterio personalizzato](#patch) se si desidera aggiornare solo uno o più campi per un criterio, anziché sovrascriverlo.

**Formato API**

```http
PUT /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | La `id` del criterio da aggiornare. |

**Richiesta**

In questo esempio, le condizioni per l’esportazione di dati in una terza parte sono cambiate e ora è necessario richiedere il criterio creato per negare questa azione di marketing se `C1 AND C5` sono presenti etichette per i dati.

La richiesta seguente aggiorna il criterio esistente in modo da includere la nuova espressione di criterio. Tieni presente che, poiché questa richiesta essenzialmente riscrive il criterio, tutti i campi devono essere inclusi nel payload, anche se alcuni dei relativi valori non vengono aggiornati.

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
| `status` | Stato corrente del criterio. Sono disponibili tre stati possibili: `DRAFT`, `ENABLED`oppure `DISABLED`. Per impostazione predefinita, solo `ENABLED` Le politiche partecipano alla valutazione. Vedi la panoramica su [valutazione politica](../enforcement/overview.md) per ulteriori informazioni. |
| `marketingActionRefs` | Matrice che elenca gli URI di tutte le azioni di marketing applicabili al criterio. L’URI per un’azione di marketing viene fornito in `_links.self.href` nella risposta per [ricerca di un’azione di marketing](./marketing-actions.md#look-up). |
| `description` | Una descrizione facoltativa che fornisce ulteriore contesto al caso d’uso del criterio. |
| `deny` | L&#39;espressione di criterio che descrive le etichette di utilizzo dati specifiche per le azioni di marketing associate al criterio non viene eseguita. Vedi la sezione su [creazione di un criterio](#create-policy) per ulteriori informazioni su questa proprietà. |

**Risposta**

Una risposta corretta restituisce i dettagli del criterio aggiornato.

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
>È possibile aggiornare solo i criteri personalizzati. Per abilitare o disabilitare i criteri di base, consulta la sezione [aggiornamento dell&#39;elenco dei criteri di base abilitati](#update-enabled-core).

Una parte specifica di un criterio può essere aggiornata utilizzando una richiesta di PATCH. A differenza delle richieste PUT che riscrivono il criterio, le richieste PATCH aggiornano solo le proprietà specificate nel corpo della richiesta. Questa opzione è particolarmente utile quando desideri abilitare o disabilitare un criterio, in quanto devi fornire solo il percorso della proprietà appropriata (`/status`) e il relativo valore (`ENABLED` o `DISABLED`).

>[!NOTE]
>
>I payload per le richieste PATCH seguono la formattazione della patch JSON. Consulta la sezione [Guida di base sulle API](../../landing/api-fundamentals.md) per ulteriori informazioni sulla sintassi accettata.

La [!DNL Policy Service] API supporta le operazioni di patch JSON `add`, `remove`e `replace`, e ti consente di combinare diversi aggiornamenti insieme in una singola chiamata, come mostrato nell’esempio di seguito.

**Formato API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | La `id` del criterio di cui si desidera aggiornare le proprietà. |

**Richiesta**

La richiesta seguente utilizza due `replace` operazioni per modificare lo stato del criterio da `DRAFT` a `ENABLED`e per aggiornare `description` campo con una nuova descrizione.

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

Una risposta corretta restituisce i dettagli del criterio aggiornato.


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

È possibile eliminare un criterio personalizzato includendo i relativi `id` nel percorso di una richiesta DELETE.

>[!WARNING]
>
>Una volta eliminate, le politiche non possono essere recuperate. Si consiglia di [eseguire una richiesta di ricerca (GET)](#lookup) per visualizzare il criterio e confermare che si tratta del criterio corretto da rimuovere.

**Formato API**

```http
DELETE /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | ID del criterio da eliminare. |

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

Una risposta corretta restituisce lo stato HTTP 200 (OK) con un corpo vuoto.

Puoi confermare l’eliminazione tentando di cercare nuovamente (GET) il criterio. Se il criterio è stato eliminato correttamente, riceverai un errore HTTP 404 (Non trovato).

## Recupera un elenco dei criteri di base abilitati {#list-enabled-core}

Per impostazione predefinita, solo i criteri di governance dei dati abilitati partecipano alla valutazione. Puoi recuperare un elenco dei criteri di base attualmente abilitati dalla tua organizzazione effettuando una richiesta di GET al `/enabledCorePolicies` punto finale.

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

Una risposta corretta restituisce l&#39;elenco dei criteri di base abilitati in un `policyIds` array.

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

## Aggiornare l’elenco dei criteri di base abilitati {#update-enabled-core}

Per impostazione predefinita, solo i criteri di governance dei dati abilitati partecipano alla valutazione. Effettuando una richiesta PUT al `/enabledCorePolicies` endpoint, puoi aggiornare l’elenco dei criteri di base abilitati per l’organizzazione utilizzando una singola chiamata .

>[!NOTE]
>
>Solo i criteri principali possono essere abilitati o disabilitati da questo endpoint. Per abilitare o disabilitare i criteri personalizzati, consulta la sezione [aggiornamento di una parte di un criterio](#patch).

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
| `policyIds` | Elenco degli ID dei criteri di base da abilitare. I criteri di base non inclusi sono impostati su `DISABLED` status e non parteciperà alla valutazione. |

**Risposta**

Una risposta corretta restituisce l&#39;elenco aggiornato dei criteri di base abilitati in un `policyIds` array.

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

Una volta definiti nuovi criteri o aggiornati quelli esistenti, puoi utilizzare [!DNL Policy Service] API per testare le azioni di marketing rispetto a specifiche etichette o set di dati e vedere se le tue politiche stanno generando violazioni come previsto. Consulta la guida [endpoint per la valutazione delle politiche](./evaluation.md) per ulteriori informazioni.
