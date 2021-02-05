---
keywords: Experience Platform ;home;argomenti popolari;Applicazione delle regole;Applicazione basata sulle API;governance dei dati
solution: Experience Platform
title: Endpoint API criteri
topic: developer guide
description: I criteri di utilizzo dei dati sono regole adottate dalla tua organizzazione che descrivono i tipi di azioni di marketing consentite, o da cui sono previste restrizioni, per i dati all'interno  Experience Platform. L'endpoint /policy viene utilizzato per tutte le chiamate API relative alla visualizzazione, alla creazione, all'aggiornamento o all'eliminazione dei criteri di utilizzo dei dati.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 2%

---


# Endpoint criteri

I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing consentite o con cui è consentito eseguire attività sui dati all&#39;interno di [!DNL Experience Platform]. L&#39;endpoint `/policies` in [!DNL Policy Service API] consente di gestire i criteri di utilizzo dei dati a livello di programmazione per l&#39;organizzazione.

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39; [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Prima di continuare, consultare la [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per eseguire correttamente chiamate a qualsiasi API [!DNL Experience Platform].

## Recupera un elenco di criteri {#list}

È possibile elencare tutti i criteri `core` o `custom` effettuando una richiesta di GET rispettivamente a `/policies/core` o `/policies/custom`.

**Formato API**

```http
GET /policies/core
GET /policies/custom
```

**Richiesta**

La seguente richiesta consente di ottenere un elenco di criteri personalizzati definiti dall&#39;organizzazione.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta include un array `children` che elenca i dettagli di ciascun criterio recuperato, inclusi i relativi valori `id`. È possibile utilizzare il campo `id` di un particolare criterio per eseguire le richieste [Search](#lookup), [update](#update) e [delete](#delete) per tale criterio.

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
| `name` | Nome visualizzato per un criterio. |
| `status` | Stato corrente di un criterio. Esistono tre stati possibili: `DRAFT`, `ENABLED` o `DISABLED`. Per impostazione predefinita, solo i criteri `ENABLED` partecipano alla valutazione. Per ulteriori informazioni, vedere la panoramica sulla [valutazione dei criteri](../enforcement/overview.md). |
| `marketingActionRefs` | Un array che elenca gli URI di tutte le azioni di marketing applicabili a un criterio. |
| `description` | Una descrizione facoltativa che fornisce ulteriore contesto al caso di utilizzo del criterio. |
| `deny` | Un oggetto che descrive le etichette di utilizzo dei dati specifiche sulle quali viene limitata l&#39;azione di marketing associata a un criterio. Per ulteriori informazioni su questa proprietà, vedere la sezione relativa alla [creazione di un criterio](#create-policy). |

## Cercare un criterio {#look-up}

Potete cercare un criterio specifico includendo la proprietà `id` di tale criterio nel percorso di una richiesta di GET.

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
| `name` | Nome visualizzato per il criterio. |
| `status` | Stato corrente del criterio. Esistono tre stati possibili: `DRAFT`, `ENABLED` o `DISABLED`. Per impostazione predefinita, solo i criteri `ENABLED` partecipano alla valutazione. Per ulteriori informazioni, vedere la panoramica sulla [valutazione dei criteri](../enforcement/overview.md). |
| `marketingActionRefs` | Un array che elenca gli URI di tutte le azioni di marketing applicabili al criterio. |
| `description` | Una descrizione facoltativa che fornisce ulteriore contesto al caso di utilizzo del criterio. |
| `deny` | Un oggetto che descrive le etichette di utilizzo dei dati specifiche sulle quali l&#39;azione di marketing associata al criterio non viene eseguita. Per ulteriori informazioni su questa proprietà, vedere la sezione relativa alla [creazione di un criterio](#create-policy). |

## Creare un criterio personalizzato {#create-policy}

Nell&#39;API [!DNL Policy Service], un criterio è definito dai seguenti elementi:

* Riferimento a una specifica azione di marketing
* Un&#39;espressione che descrive le etichette di utilizzo dei dati per le quali l&#39;azione di marketing non può essere eseguita

Per soddisfare quest&#39;ultimo requisito, le definizioni dei criteri devono includere un&#39;espressione booleana relativa alla presenza di etichette di utilizzo dei dati. Questa espressione è denominata espressione di criterio.

Le espressioni del criterio vengono fornite sotto forma di proprietà `deny` all&#39;interno di ogni definizione del criterio. Un esempio di semplice oggetto `deny` che verifica solo la presenza di una singola etichetta avrà l&#39;aspetto seguente:

```json
"deny": {
    "label": "C1"
}
```

Tuttavia, molti criteri specificano condizioni più complesse relative alla presenza di etichette di utilizzo dei dati. Per supportare questi casi di utilizzo, è anche possibile includere operazioni booleane per descrivere le espressioni dei criteri. L&#39;oggetto policy espressione deve contenere un&#39;etichetta o un operatore e gli operandi, ma non entrambi. A sua volta, ogni operando è anche un oggetto con espressione di criterio.

Ad esempio, per definire un criterio che impedisca l&#39;esecuzione di un&#39;azione di marketing sui dati in cui sono presenti etichette `C1 OR (C3 AND C7)`, la proprietà `deny` del criterio viene specificata come:

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
| `operator` | Indica la relazione condizionale tra le etichette fornite nell&#39;array di pari livello `operands`. I valori accettati sono: <ul><li>`OR`: L&#39;espressione restituisce true se sono presenti delle etichette nell&#39; `operands` array.</li><li>`AND`: L&#39;espressione restituisce true solo se sono presenti tutte le etichette della  `operands` matrice.</li></ul> |
| `operands` | Un array di oggetti, con ciascun oggetto che rappresenta una singola etichetta o una coppia aggiuntiva di proprietà `operator` e `operands`. La presenza delle etichette e/o delle operazioni in un array `operands` restituisce true o false in base al valore della proprietà di pari livello `operator`. |
| `label` | Nome di un&#39;unica etichetta di utilizzo dati applicata al criterio. |

Potete creare un nuovo criterio personalizzato effettuando una richiesta di POST all&#39;endpoint `/policies/custom`.

**Formato API**

```http
POST /policies/custom
```

**Richiesta**

La richiesta seguente crea un nuovo criterio che impedisce l&#39;esecuzione dell&#39;azione di marketing `exportToThirdParty` sui dati contenenti etichette `C1 OR (C3 AND C7)`.

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
| `name` | Nome visualizzato per il criterio. |
| `status` | Stato corrente del criterio. Esistono tre stati possibili: `DRAFT`, `ENABLED` o `DISABLED`. Per impostazione predefinita, solo i criteri `ENABLED` partecipano alla valutazione. Per ulteriori informazioni, vedere la panoramica sulla [valutazione dei criteri](../enforcement/overview.md). |
| `marketingActionRefs` | Un array che elenca gli URI di tutte le azioni di marketing applicabili al criterio. L&#39;URI di un&#39;azione di marketing è fornito in `_links.self.href` nella risposta per [cercare un&#39;azione di marketing](./marketing-actions.md#look-up). |
| `description` | Una descrizione facoltativa che fornisce ulteriore contesto al caso di utilizzo del criterio. |
| `deny` | L&#39;espressione di criterio che descrive le etichette di utilizzo dei dati specifiche per le azioni di marketing associate al criterio non viene eseguita. |

**Risposta**

Una risposta corretta restituisce i dettagli del criterio appena creato, incluso `id`. Questo valore è di sola lettura e viene assegnato automaticamente alla creazione del criterio.

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
>È possibile aggiornare solo i criteri personalizzati. Se si desidera abilitare o disabilitare i criteri di base, consultare la sezione in [aggiornamento dell&#39;elenco dei criteri di base abilitati](#update-enabled-core).

Potete aggiornare un criterio personalizzato esistente fornendo il relativo ID nel percorso di una richiesta di PUT con un payload che include il modulo aggiornato del criterio nella sua interezza. In altre parole, la richiesta PUT sostanzialmente riscrive il criterio.

>[!NOTE]
>
>Consultate la sezione sull [aggiornamento di una parte di un criterio personalizzato](#patch) se desiderate aggiornare solo uno o più campi per un criterio, anziché sovrascriverlo.

**Formato API**

```http
PUT /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | Il `id` del criterio da aggiornare. |

**Richiesta**

In questo esempio, le condizioni per l&#39;esportazione di dati a terzi sono cambiate e ora è necessario che il criterio creato neghi questa azione di marketing se sono presenti etichette di dati `C1 AND C5`.

La richiesta seguente aggiorna il criterio esistente per includere la nuova espressione del criterio. Notate che, poiché questa richiesta in sostanza riscrive il criterio, tutti i campi devono essere inclusi nel payload, anche se alcuni dei relativi valori non vengono aggiornati.

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
| `name` | Nome visualizzato per il criterio. |
| `status` | Stato corrente del criterio. Esistono tre stati possibili: `DRAFT`, `ENABLED` o `DISABLED`. Per impostazione predefinita, solo i criteri `ENABLED` partecipano alla valutazione. Per ulteriori informazioni, vedere la panoramica sulla [valutazione dei criteri](../enforcement/overview.md). |
| `marketingActionRefs` | Un array che elenca gli URI di tutte le azioni di marketing applicabili al criterio. L&#39;URI di un&#39;azione di marketing è fornito in `_links.self.href` nella risposta per [cercare un&#39;azione di marketing](./marketing-actions.md#look-up). |
| `description` | Una descrizione facoltativa che fornisce ulteriore contesto al caso di utilizzo del criterio. |
| `deny` | L&#39;espressione di criterio che descrive le etichette di utilizzo dei dati specifiche per le azioni di marketing associate al criterio non viene eseguita. Per ulteriori informazioni su questa proprietà, vedere la sezione relativa alla [creazione di un criterio](#create-policy). |

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
>È possibile aggiornare solo i criteri personalizzati. Se si desidera abilitare o disabilitare i criteri di base, consultare la sezione in [aggiornamento dell&#39;elenco dei criteri di base abilitati](#update-enabled-core).

Una parte specifica di un criterio può essere aggiornata utilizzando una richiesta PATCH. A differenza delle richieste PUT che riscrivono il criterio, le richieste PATCH aggiornano solo le proprietà specificate nel corpo della richiesta. Ciò è particolarmente utile quando si desidera abilitare o disabilitare un criterio, in quanto è necessario fornire solo il percorso della proprietà appropriata (`/status`) e il relativo valore (`ENABLED` o `DISABLED`).

>[!NOTE]
>
>I payload per le richieste PATCH seguono la formattazione della patch JSON. Per ulteriori informazioni sulla sintassi accettata, vedere la [Guida di base delle API](../../landing/api-fundamentals.md).

L&#39;API [!DNL Policy Service] supporta le operazioni di patch JSON `add`, `remove` e `replace` e consente di combinare diversi aggiornamenti in una singola chiamata, come illustrato nell&#39;esempio seguente.

**Formato API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | Il `id` del criterio di cui si desidera aggiornare le proprietà. |

**Richiesta**

La richiesta seguente utilizza due operazioni `replace` per cambiare lo stato del criterio da `DRAFT` a `ENABLED` e per aggiornare il campo `description` con una nuova descrizione.

>[!IMPORTANT]
>
>Quando si inviano più operazioni PATCH in un&#39;unica richiesta, queste vengono elaborate nell&#39;ordine in cui appaiono nell&#39;array. Se necessario, accertatevi di inviare le richieste nell&#39;ordine corretto.

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

Potete eliminare un criterio personalizzato includendone `id` nel percorso di una richiesta di DELETE.

>[!WARNING]
>
>Una volta eliminati, i criteri non possono essere recuperati. È consigliabile eseguire [una richiesta di ricerca (GET)](#lookup) prima di visualizzare il criterio e confermare che si tratta del criterio corretto da rimuovere.

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

Potete confermare l&#39;eliminazione tentando di ricercare nuovamente (GET) il criterio. Se il criterio è stato eliminato correttamente, dovreste ricevere un errore HTTP 404 (non trovato).

## Recupera un elenco di criteri di base abilitati {#list-enabled-core}

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

## Aggiornare l&#39;elenco dei criteri di base abilitati {#update-enabled-core}

Per impostazione predefinita, solo i criteri di utilizzo dei dati abilitati partecipano alla valutazione. Eseguendo una richiesta di PUT all&#39;endpoint `/enabledCorePolicies`, puoi aggiornare l&#39;elenco dei criteri di base abilitati per la tua organizzazione utilizzando una singola chiamata.

>[!NOTE]
>
>Solo i criteri di base possono essere attivati o disattivati da questo endpoint. Per abilitare o disabilitare i criteri personalizzati, consultare la sezione relativa all&#39;aggiornamento di una parte di un criterio ](#patch).[

**Formato API**

```http
PUT /enabledCorePolicies
```

**Richiesta**

La richiesta seguente aggiorna l&#39;elenco dei criteri di base abilitati in base agli ID forniti nel payload.

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
| `policyIds` | Elenco degli ID dei criteri di base da abilitare. Eventuali criteri di base non inclusi sono impostati sullo stato `DISABLED` e non parteciperanno alla valutazione. |

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

Una volta definiti nuovi criteri o aggiornati quelli esistenti, puoi utilizzare l&#39;API [!DNL Policy Service] per testare le azioni di marketing in base a etichette o set di dati specifici e verificare se i criteri stanno generando le violazioni come previsto. Per ulteriori informazioni, vedere la guida sugli endpoint di [valutazione criteri](./evaluation.md).