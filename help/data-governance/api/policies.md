---
keywords: Experience Platform;home;argomenti popolari;Applicazione delle policy;applicazione basata su API;governance dei dati
solution: Experience Platform
title: Endpoint API per i criteri di governance dei dati
description: I criteri di governance dei dati sono regole adottate dall’organizzazione che descrivono i tipi di azioni di marketing che possono essere eseguiti o meno sui dati di Experience Platform. L’endpoint /policies viene utilizzato per tutte le chiamate API relative alla visualizzazione, alla creazione, all’aggiornamento o all’eliminazione dei criteri di governance dei dati.
role: Developer
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 3%

---

# Endpoint &quot;data governance policies&quot;

I criteri di governance dei dati sono regole che descrivono i tipi di azioni di marketing che possono essere eseguiti o meno sui dati in [!DNL Experience Platform]. L&#39;endpoint `/policies` in [!DNL Policy Service API] consente di gestire in modo programmatico i criteri di governance dei dati per l&#39;organizzazione.

>[!IMPORTANT]
>
>I criteri di governance non devono essere confusi con i criteri di controllo dell’accesso, che determinano gli attributi di dati specifici a cui possono accedere alcuni utenti di Platform nella tua organizzazione. Per informazioni dettagliate su come gestire in modo programmatico i criteri di controllo di accesso, consultare la guida dell&#39;endpoint `/policies` per [Access Control API](../../access-control/abac/api/policies.md).

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39;[[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Prima di continuare, consulta la [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API [!DNL Experience Platform].

## Recuperare un elenco di criteri {#list}

È possibile elencare tutti i criteri `core` o `custom` effettuando una richiesta di GET rispettivamente a `/policies/core` o `/policies/custom`.

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

Una risposta corretta include un array `children` che elenca i dettagli di ogni criterio recuperato, inclusi i relativi valori `id`. È possibile utilizzare il campo `id` di un determinato criterio per eseguire [ricerche](#lookup), [aggiornamenti](#update) e [eliminazioni](#delete) richieste per tale criterio.

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
| `status` | Stato corrente di un criterio. Sono possibili tre stati: `DRAFT`, `ENABLED` o `DISABLED`. Per impostazione predefinita, solo `ENABLED` criteri partecipano alla valutazione. Per ulteriori informazioni, vedere la panoramica sulla [valutazione dei criteri](../enforcement/overview.md). |
| `marketingActionRefs` | Array che elenca gli URI di tutte le azioni di marketing applicabili a un criterio. |
| `description` | Descrizione facoltativa che fornisce ulteriore contesto al caso d’uso del criterio. |
| `deny` | Oggetto che descrive le etichette di utilizzo dei dati specifiche su cui l’azione di marketing associata a un criterio non può essere eseguita. Per ulteriori informazioni su questa proprietà, vedere la sezione relativa alla [creazione di un criterio](#create-policy). |

## Cercare un criterio {#look-up}

Per cercare un criterio specifico, devi includere la proprietà `id` del criterio nel percorso di una richiesta GET.

**Formato API**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | `id` del criterio che si desidera cercare. |

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
| `status` | Stato corrente del criterio. Sono possibili tre stati: `DRAFT`, `ENABLED` o `DISABLED`. Per impostazione predefinita, solo `ENABLED` criteri partecipano alla valutazione. Per ulteriori informazioni, vedere la panoramica sulla [valutazione dei criteri](../enforcement/overview.md). |
| `marketingActionRefs` | Array che elenca gli URI di tutte le azioni di marketing applicabili per il criterio. |
| `description` | Descrizione facoltativa che fornisce ulteriore contesto al caso d’uso del criterio. |
| `deny` | Oggetto che descrive le etichette di utilizzo dei dati specifiche su cui l’azione di marketing associata al criterio non può essere eseguita. Per ulteriori informazioni su questa proprietà, vedere la sezione relativa alla [creazione di un criterio](#create-policy). |

## Creare un criterio personalizzato {#create-policy}

Nell&#39;API [!DNL Policy Service], un criterio è definito dai seguenti elementi:

* Riferimento a una specifica azione di marketing
* Espressione che descrive le etichette di utilizzo dei dati per le quali l’azione di marketing non può essere eseguita

Per soddisfare quest’ultimo requisito, le definizioni dei criteri devono includere un’espressione booleana relativa alla presenza di etichette di utilizzo dei dati. Questa espressione viene definita espressione di criteri.

Le espressioni dei criteri vengono fornite sotto forma di una proprietà `deny` all&#39;interno di ogni definizione dei criteri. Un esempio di un semplice oggetto `deny` che controlla solo la presenza di una singola etichetta avrà l&#39;aspetto seguente:

```json
"deny": {
    "label": "C1"
}
```

Tuttavia, molti criteri specificano condizioni più complesse per quanto riguarda la presenza di etichette di utilizzo dei dati. Per supportare questi casi d’uso, puoi anche includere operazioni booleane per descrivere le espressioni dei criteri. L’oggetto espressione dei criteri deve contenere un’etichetta o un operatore e operandi, ma non entrambi. A sua volta, ogni operando è anche un oggetto espressione di criteri.

Ad esempio, per definire un criterio che impedisca l&#39;esecuzione di un&#39;azione di marketing su dati in cui sono presenti `C1 OR (C3 AND C7)` etichette, la proprietà `deny` del criterio verrà specificata come:

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
| `operator` | Indica la relazione condizionale tra le etichette fornite nell&#39;array `operands` di pari livello. I valori accettati sono: <ul><li>`OR`: l&#39;espressione viene risolta in true se sono presenti etichette nell&#39;array `operands`.</li><li>`AND`: l&#39;espressione viene risolta in true solo se sono presenti tutte le etichette nell&#39;array `operands`.</li></ul> |
| `operands` | Matrice di oggetti, in cui ogni oggetto rappresenta una singola etichetta o una coppia aggiuntiva di proprietà `operator` e `operands`. La presenza di etichette e/o operazioni in un array `operands` viene risolta come true o false in base al valore della proprietà `operator` di pari livello. |
| `label` | Nome di una singola etichetta di utilizzo dati che si applica al criterio. |

È possibile creare un nuovo criterio personalizzato effettuando una richiesta POST all&#39;endpoint `/policies/custom`.

**Formato API**

```http
POST /policies/custom
```

**Richiesta**

La richiesta seguente crea un nuovo criterio che impedisce l&#39;esecuzione dell&#39;azione di marketing `exportToThirdParty` su dati contenenti etichette `C1 OR (C3 AND C7)`.

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
| `status` | Stato corrente del criterio. Sono possibili tre stati: `DRAFT`, `ENABLED` o `DISABLED`. Per impostazione predefinita, solo `ENABLED` criteri partecipano alla valutazione. Per ulteriori informazioni, vedere la panoramica sulla [valutazione dei criteri](../enforcement/overview.md). |
| `marketingActionRefs` | Array che elenca gli URI di tutte le azioni di marketing applicabili per il criterio. L&#39;URI per un&#39;azione di marketing viene fornito in `_links.self.href` nella risposta per [la ricerca di un&#39;azione di marketing](./marketing-actions.md#look-up). |
| `description` | Descrizione facoltativa che fornisce ulteriore contesto al caso d’uso del criterio. |
| `deny` | L’espressione dei criteri che descrive le etichette di utilizzo dei dati specifiche per le quali l’azione di marketing associata al criterio non può essere eseguita. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del criterio appena creato, incluso `id`. Questo valore è di sola lettura e viene assegnato automaticamente al momento della creazione del criterio.

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
>Puoi aggiornare solo i criteri personalizzati. Se desideri abilitare o disabilitare i criteri di base, consulta la sezione su [aggiornamento dell&#39;elenco dei criteri di base abilitati](#update-enabled-core).

Per aggiornare un criterio personalizzato esistente, devi fornire il relativo ID nel percorso di una richiesta PUT con un payload che includa l’intero modulo aggiornato del criterio. In altre parole, la richiesta PUT riscrive essenzialmente il criterio.

>[!NOTE]
>
>Vedere la sezione relativa all&#39;aggiornamento di una parte di un criterio personalizzato](#patch) se si desidera aggiornare solo uno o più campi per un criterio, anziché sovrascriverlo.[

**Formato API**

```http
PUT /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | `id` del criterio che si desidera aggiornare. |

**Richiesta**

In questo esempio, le condizioni per l&#39;esportazione di dati a terze parti sono cambiate e ora è necessario il criterio creato per rifiutare questa azione di marketing se sono presenti `C1 AND C5` etichette dati.

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
| `status` | Stato corrente del criterio. Sono possibili tre stati: `DRAFT`, `ENABLED` o `DISABLED`. Per impostazione predefinita, solo `ENABLED` criteri partecipano alla valutazione. Per ulteriori informazioni, vedere la panoramica sulla [valutazione dei criteri](../enforcement/overview.md). |
| `marketingActionRefs` | Array che elenca gli URI di tutte le azioni di marketing applicabili per il criterio. L&#39;URI per un&#39;azione di marketing viene fornito in `_links.self.href` nella risposta per [la ricerca di un&#39;azione di marketing](./marketing-actions.md#look-up). |
| `description` | Descrizione facoltativa che fornisce ulteriore contesto al caso d’uso del criterio. |
| `deny` | L’espressione dei criteri che descrive le etichette di utilizzo dei dati specifiche per le quali l’azione di marketing associata al criterio non può essere eseguita. Per ulteriori informazioni su questa proprietà, vedere la sezione relativa alla [creazione di un criterio](#create-policy). |

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
>Puoi aggiornare solo i criteri personalizzati. Se desideri abilitare o disabilitare i criteri di base, consulta la sezione su [aggiornamento dell&#39;elenco dei criteri di base abilitati](#update-enabled-core).

È possibile aggiornare una parte specifica di un criterio utilizzando una richiesta PATCH. A differenza delle richieste PUT che riscrivono il criterio, le richieste PATCH aggiornano solo le proprietà specificate nel corpo della richiesta. Questa funzione risulta particolarmente utile quando si desidera abilitare o disabilitare un criterio, in quanto è necessario fornire solo il percorso della proprietà appropriata (`/status`) e il relativo valore (`ENABLED` o `DISABLED`).

>[!NOTE]
>
>I payload per le richieste PATCH seguono la formattazione Patch JSON. Per ulteriori informazioni sulla sintassi accettata, consulta la [guida sui concetti fondamentali dell&#39;API](../../landing/api-fundamentals.md).

L&#39;API [!DNL Policy Service] supporta le operazioni Patch JSON `add`, `remove` e `replace` e consente di combinare diversi aggiornamenti in un&#39;unica chiamata, come illustrato nell&#39;esempio seguente.

**Formato API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | `id` del criterio di cui si desidera aggiornare le proprietà. |

**Richiesta**

La richiesta seguente utilizza due operazioni `replace` per modificare lo stato dei criteri da `DRAFT` a `ENABLED` e per aggiornare il campo `description` con una nuova descrizione.

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
>Una volta eliminati, i criteri non possono essere recuperati. È consigliabile [eseguire una richiesta di ricerca (GET)](#lookup) prima di visualizzare il criterio e confermare che si tratta del criterio corretto da rimuovere.

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

Per impostazione predefinita, solo i criteri di governance dei dati abilitati partecipano alla valutazione. Per recuperare un elenco dei criteri di base attualmente abilitati dall&#39;organizzazione, eseguire una richiesta GET all&#39;endpoint `/enabledCorePolicies`.

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

In caso di esito positivo, la risposta restituisce l’elenco dei criteri di base abilitati in un array `policyIds`.

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

Per impostazione predefinita, solo i criteri di governance dei dati abilitati partecipano alla valutazione. Effettuando una richiesta PUT all&#39;endpoint `/enabledCorePolicies`, puoi aggiornare l&#39;elenco dei criteri di base abilitati per la tua organizzazione utilizzando una singola chiamata.

>[!NOTE]
>
>Solo i criteri di base possono essere abilitati o disabilitati da questo endpoint. Per abilitare o disabilitare i criteri personalizzati, vedere la sezione relativa all&#39;aggiornamento di una parte di un criterio](#patch) in [.

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
| `policyIds` | Elenco degli ID dei criteri di base da abilitare. Tutti i criteri di base non inclusi sono impostati sullo stato `DISABLED` e non parteciperanno alla valutazione. |

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;elenco aggiornato dei criteri di base abilitati in un array `policyIds`.

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

Dopo aver definito nuovi criteri o aggiornato quelli esistenti, è possibile utilizzare l&#39;API [!DNL Policy Service] per testare le azioni di marketing rispetto a etichette o set di dati specifici e verificare se i criteri generano violazioni come previsto. Per ulteriori informazioni, consulta la guida sugli [endpoint di valutazione dei criteri](./evaluation.md).
