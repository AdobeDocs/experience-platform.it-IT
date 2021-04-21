---
keywords: Experience Platform;home;argomenti popolari;applicazione dei criteri;applicazione basata su API;governance dei dati
solution: Experience Platform
title: Endpoint API per criteri
topic-legacy: developer guide
description: I criteri di utilizzo dei dati sono regole adottate dalla tua organizzazione che descrivono i tipi di azioni di marketing che puoi o da cui ti sono limitate, eseguendo dati all’interno di un Experience Platform. L’endpoint /policy viene utilizzato per tutte le chiamate API relative alla visualizzazione, alla creazione, all’aggiornamento o all’eliminazione dei criteri di utilizzo dei dati.
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 2%

---

# Endpoint criteri

I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing consentite o a cui è stata limitata l’esecuzione di dati all’interno di [!DNL Experience Platform]. L’endpoint `/policies` in [!DNL Policy Service API] ti consente di gestire in modo programmatico i criteri di utilizzo dei dati per la tua organizzazione.

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39; [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Prima di continuare, controlla la [guida introduttiva](getting-started.md) per i collegamenti alla relativa documentazione, una guida per la lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API [!DNL Experience Platform].

## Recupera un elenco di criteri {#list}

È possibile elencare tutti i criteri `core` o `custom` effettuando una richiesta di GET rispettivamente a `/policies/core` o `/policies/custom`.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta include una matrice `children` che elenca i dettagli di ciascun criterio recuperato, inclusi i relativi valori `id`. Puoi utilizzare il campo `id` di un particolare criterio per eseguire le richieste [lookup](#lookup), [update](#update) e [delete](#delete) per tale criterio.

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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
| `status` | Lo stato corrente di un criterio. Sono disponibili tre stati possibili: `DRAFT`, `ENABLED` o `DISABLED`. Per impostazione predefinita, solo i criteri `ENABLED` partecipano alla valutazione. Per ulteriori informazioni, consulta la panoramica sulla [valutazione dei criteri](../enforcement/overview.md) . |
| `marketingActionRefs` | Matrice che elenca gli URI di tutte le azioni di marketing applicabili per un criterio. |
| `description` | Una descrizione facoltativa che fornisce ulteriore contesto al caso d’uso del criterio. |
| `deny` | Un oggetto che descrive le etichette di utilizzo dati specifiche per le quali è stata limitata l&#39;esecuzione dell&#39;azione di marketing associata a un criterio. Per ulteriori informazioni su questa proprietà, consulta la sezione su [creazione di un criterio](#create-policy) . |

## Cerca un criterio {#look-up}

Puoi cercare un criterio specifico includendo la proprietà `id` di tale criterio nel percorso di una richiesta GET.

**Formato API**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | Il `id` del criterio da cercare. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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
| `status` | Stato corrente del criterio. Sono disponibili tre stati possibili: `DRAFT`, `ENABLED` o `DISABLED`. Per impostazione predefinita, solo i criteri `ENABLED` partecipano alla valutazione. Per ulteriori informazioni, consulta la panoramica sulla [valutazione dei criteri](../enforcement/overview.md) . |
| `marketingActionRefs` | Matrice che elenca gli URI di tutte le azioni di marketing applicabili al criterio. |
| `description` | Una descrizione facoltativa che fornisce ulteriore contesto al caso d’uso del criterio. |
| `deny` | Un oggetto che descrive le etichette di utilizzo dei dati specifiche sulle quali l&#39;azione di marketing associata al criterio non viene eseguita. Per ulteriori informazioni su questa proprietà, consulta la sezione su [creazione di un criterio](#create-policy) . |

## Creare un criterio personalizzato {#create-policy}

Nell&#39;API [!DNL Policy Service], un criterio è definito dai seguenti elementi:

* Riferimento a una specifica azione di marketing
* Un&#39;espressione che descrive le etichette di utilizzo dei dati su cui è limitata l&#39;esecuzione dell&#39;azione di marketing

Per soddisfare quest’ultimo requisito, le definizioni dei criteri devono includere un’espressione booleana relativa alla presenza di etichette di utilizzo dei dati. Questa espressione è denominata espressione di criterio.

Le espressioni di criterio vengono fornite sotto forma di proprietà `deny` all&#39;interno di ogni definizione di criterio. Un esempio di un semplice oggetto `deny` che controlla solo la presenza di una singola etichetta ha il seguente aspetto:

```json
"deny": {
    "label": "C1"
}
```

Tuttavia, molti criteri specificano condizioni più complesse relative alla presenza di etichette per l’utilizzo dei dati. Per supportare questi casi d’uso, puoi anche includere le operazioni booleane per descrivere le espressioni dei criteri. L&#39;oggetto espressione policy deve contenere un&#39;etichetta o un operatore e operandi, ma non entrambi. A sua volta, ogni operando è anche un oggetto espressione di criterio.

Ad esempio, per definire un criterio che impedisca l’esecuzione di un’azione di marketing sui dati in cui sono presenti le etichette `C1 OR (C3 AND C7)`, la proprietà `deny` del criterio viene specificata come segue:

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
| `operator` | Indica la relazione condizionale tra le etichette fornite nella matrice di pari livello `operands`. I valori accettati sono: <ul><li>`OR`: L&#39;espressione restituisce true se è presente una delle etichette nell&#39; `operands` array.</li><li>`AND`: L&#39;espressione restituisce true solo se sono presenti tutte le etichette nell&#39; `operands` array.</li></ul> |
| `operands` | Matrice di oggetti, con ogni oggetto che rappresenta una singola etichetta o una coppia aggiuntiva di proprietà `operator` e `operands`. La presenza delle etichette e/o delle operazioni in un array `operands` restituisce true o false in base al valore della proprietà di pari livello `operator`. |
| `label` | Nome di un&#39;etichetta di utilizzo dati singola applicata al criterio. |

Puoi creare un nuovo criterio personalizzato effettuando una richiesta di POST all’endpoint `/policies/custom` .

**Formato API**

```http
POST /policies/custom
```

**Richiesta**

La seguente richiesta crea un nuovo criterio che impedisce l’esecuzione dell’azione di marketing `exportToThirdParty` sui dati contenenti etichette `C1 OR (C3 AND C7)`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `status` | Stato corrente del criterio. Sono disponibili tre stati possibili: `DRAFT`, `ENABLED` o `DISABLED`. Per impostazione predefinita, solo i criteri `ENABLED` partecipano alla valutazione. Per ulteriori informazioni, consulta la panoramica sulla [valutazione dei criteri](../enforcement/overview.md) . |
| `marketingActionRefs` | Matrice che elenca gli URI di tutte le azioni di marketing applicabili al criterio. L’URI per un’azione di marketing viene fornito in `_links.self.href` nella risposta per [cerca un’azione di marketing](./marketing-actions.md#look-up). |
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
    "imsOrg": "{IMS_ORG}",
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
>È possibile aggiornare solo i criteri personalizzati. Per abilitare o disabilitare i criteri di base, consulta la sezione su [aggiornamento dell&#39;elenco dei criteri di base abilitati](#update-enabled-core).

Puoi aggiornare un criterio personalizzato esistente fornendo il relativo ID nel percorso di una richiesta di PUT con un payload che include la versione aggiornata del criterio nella sua interezza. In altre parole, la richiesta di PUT sostanzialmente riscrive il criterio.

>[!NOTE]
>
>Consulta la sezione sull’ [aggiornamento di una parte di un criterio personalizzato](#patch) se desideri aggiornare solo uno o più campi per un criterio, anziché sovrascriverlo.

**Formato API**

```http
PUT /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | Il `id` del criterio da aggiornare. |

**Richiesta**

In questo esempio, le condizioni per l’esportazione di dati in una terza parte sono cambiate e ora è necessario il criterio creato per negare questa azione di marketing se sono presenti etichette di dati `C1 AND C5` .

La richiesta seguente aggiorna il criterio esistente in modo da includere la nuova espressione di criterio. Tieni presente che, poiché questa richiesta essenzialmente riscrive il criterio, tutti i campi devono essere inclusi nel payload, anche se alcuni dei relativi valori non vengono aggiornati.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `status` | Stato corrente del criterio. Sono disponibili tre stati possibili: `DRAFT`, `ENABLED` o `DISABLED`. Per impostazione predefinita, solo i criteri `ENABLED` partecipano alla valutazione. Per ulteriori informazioni, consulta la panoramica sulla [valutazione dei criteri](../enforcement/overview.md) . |
| `marketingActionRefs` | Matrice che elenca gli URI di tutte le azioni di marketing applicabili al criterio. L’URI per un’azione di marketing viene fornito in `_links.self.href` nella risposta per [cerca un’azione di marketing](./marketing-actions.md#look-up). |
| `description` | Una descrizione facoltativa che fornisce ulteriore contesto al caso d’uso del criterio. |
| `deny` | L&#39;espressione di criterio che descrive le etichette di utilizzo dati specifiche per le azioni di marketing associate al criterio non viene eseguita. Per ulteriori informazioni su questa proprietà, consulta la sezione su [creazione di un criterio](#create-policy) . |

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
    "imsOrg": "{IMS_ORG}",
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
>È possibile aggiornare solo i criteri personalizzati. Per abilitare o disabilitare i criteri di base, consulta la sezione su [aggiornamento dell&#39;elenco dei criteri di base abilitati](#update-enabled-core).

Una parte specifica di un criterio può essere aggiornata utilizzando una richiesta di PATCH. A differenza delle richieste PUT che riscrivono il criterio, le richieste PATCH aggiornano solo le proprietà specificate nel corpo della richiesta. Questa funzione è particolarmente utile quando si desidera abilitare o disabilitare un criterio, in quanto è sufficiente fornire il percorso della proprietà appropriata (`/status`) e il relativo valore (`ENABLED` o `DISABLED`).

>[!NOTE]
>
>I payload per le richieste PATCH seguono la formattazione della patch JSON. Per ulteriori informazioni sulla sintassi accettata, consulta la [Guida di base API](../../landing/api-fundamentals.md) .

L’ API [!DNL Policy Service] supporta le operazioni di patch JSON `add`, `remove` e `replace` e consente di combinare diversi aggiornamenti insieme in una singola chiamata, come mostrato nell’esempio seguente.

**Formato API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | Il `id` del criterio di cui si desidera aggiornare le proprietà. |

**Richiesta**

La richiesta seguente utilizza due operazioni `replace` per modificare lo stato del criterio da `DRAFT` a `ENABLED` e per aggiornare il campo `description` con una nuova descrizione.

>[!IMPORTANT]
>
>Quando si inviano più operazioni PATCH in una singola richiesta, queste vengono elaborate nell’ordine in cui compaiono nell’array. Se necessario, assicurati di inviare le richieste nell’ordine corretto.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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

Puoi eliminare un criterio personalizzato includendo il relativo `id` nel percorso di una richiesta DELETE.

>[!WARNING]
>
>Una volta eliminate, le politiche non possono essere recuperate. È consigliabile [eseguire prima una richiesta di ricerca (GET)](#lookup) per visualizzare il criterio e confermare che si tratta del criterio corretto da rimuovere.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 (OK) con un corpo vuoto.

Puoi confermare l’eliminazione tentando di cercare nuovamente (GET) il criterio. Se il criterio è stato eliminato correttamente, riceverai un errore HTTP 404 (Non trovato).

## Recupera un elenco di criteri core abilitati {#list-enabled-core}

Per impostazione predefinita, solo i criteri di utilizzo dei dati abilitati partecipano alla valutazione. È possibile recuperare un elenco dei criteri di base attualmente abilitati dalla propria organizzazione effettuando una richiesta di GET all&#39;endpoint `/enabledCorePolicies`.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce l&#39;elenco dei criteri di base abilitati in un array `policyIds`.

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
  "imsOrg": "{IMS_ORG}",
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

## Aggiorna l&#39;elenco dei criteri di base abilitati {#update-enabled-core}

Per impostazione predefinita, solo i criteri di utilizzo dei dati abilitati partecipano alla valutazione. Effettuando una richiesta di PUT all&#39;endpoint `/enabledCorePolicies`, puoi aggiornare l&#39;elenco dei criteri di base abilitati per la tua organizzazione utilizzando una singola chiamata.

>[!NOTE]
>
>Solo i criteri principali possono essere abilitati o disabilitati da questo endpoint. Per abilitare o disabilitare i criteri personalizzati, consulta la sezione relativa all’ [aggiornamento di una parte di un criterio](#patch).

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Una risposta corretta restituisce l&#39;elenco aggiornato dei criteri di base abilitati in un array `policyIds`.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{IMS_ORG}",
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

Una volta definiti nuovi criteri o aggiornati quelli esistenti, puoi utilizzare l’ [!DNL Policy Service] API per testare le azioni di marketing rispetto a specifiche etichette o set di dati e verificare se i tuoi criteri stanno generando violazioni come previsto. Per ulteriori informazioni, consulta la guida sugli endpoint per la valutazione dei criteri [a1/> .](./evaluation.md)
