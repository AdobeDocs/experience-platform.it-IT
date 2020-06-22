---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criteri
topic: developer guide
translation-type: tm+mt
source-git-commit: ba9d4b31cfc3b7924879a91bd125f72159e55fc4
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 1%

---


# Criteri

I criteri di utilizzo dei dati sono regole adottate dalla tua organizzazione che descrivono i tipi di azioni di marketing che puoi eseguire su dati all&#39;interno  Experience Platform o da cui ti sono limitate.

L&#39; `/policies` endpoint viene utilizzato per tutte le chiamate API relative alla visualizzazione, alla creazione, all&#39;aggiornamento o all&#39;eliminazione dei criteri di utilizzo dei dati.

## Elenca tutti i criteri

Per visualizzare un elenco di criteri, è possibile effettuare una richiesta GET `/policies/core` o `/policies/custom` che restituisca tutti i criteri per il contenitore specificato.

**Formato API**

```http
GET /policies/core
GET /policies/custom
```

**Richiesta**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta include un &quot;conteggio&quot; che mostra il numero totale di criteri all&#39;interno del contenitore specificato, nonché i dettagli di ciascun criterio, inclusi i relativi `id`. Il `id` campo viene utilizzato per eseguire richieste di ricerca per visualizzare criteri specifici, nonché per eseguire operazioni di aggiornamento ed eliminazione.

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
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550701472910,
            "updatedClient": "string",
            "updatedUser": "string",
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
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714340335,
            "updatedClient": "string",
            "updatedUser": "string",
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

## Cercare una politica

Ogni criterio contiene un `id` campo che può essere utilizzato per richiedere i dettagli di un criterio specifico. Se il criterio `id` di un criterio è sconosciuto, può essere trovato utilizzando la richiesta di elenco (GET) per elencare tutti i criteri all&#39;interno di un contenitore (`core` o `custom`) specifico come mostrato nel passaggio precedente.

**Formato API**

```http
GET /policies/core/{id}
GET /policies/custom/{id}
```

**Richiesta**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta contiene i dettagli del criterio, compresi i campi chiave come `id` (il campo deve corrispondere a quello `id` inviato nella richiesta), `name`, `status`e `description`, nonché un collegamento di riferimento all&#39;azione di marketing su cui si basa il criterio (`marketingActionRefs`).

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
    "created": 1550691551888,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550701472910,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Creare un criterio {#create-policy}

La creazione di un criterio richiede l&#39;inclusione di un&#39;azione di marketing con un&#39;espressione delle etichette DULE che vietano tale azione di marketing. Le definizioni dei criteri devono includere una `deny` proprietà, che è un&#39;espressione booleana relativa alla presenza di etichette DULE.

Questa espressione è denominata un oggetto `PolicyExpression` e contiene _un&#39;etichetta_ o __ un operatore e gli operandi, ma non entrambi. A sua volta, ogni operando è anche un `PolicyExpression` oggetto. Ad esempio, un criterio relativo all&#39;esportazione di dati a terzi potrebbe essere vietato se sono presenti `C1 OR (C3 AND C7)` etichette. Questa espressione viene specificata come:

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

**Formato API**

```http
POST /policies/custom
```

**Richiesta**

```SHELL
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

**Risposta**

Se creata correttamente, riceverete uno stato HTTP 201 (Creato) e il corpo della risposta conterrà i dettagli del criterio appena creato, incluso `id`il relativo. Questo valore è di sola lettura e viene assegnato automaticamente alla creazione del criterio.

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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550691551888,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Aggiornare un criterio

Una volta creato, potrebbe essere necessario aggiornare un criterio di utilizzo dei dati. Questo viene fatto attraverso una richiesta PUT al criterio `id` con un payload che include la forma aggiornata del criterio, nella sua interezza. In altre parole, la richiesta PUT consiste essenzialmente nella _riscrittura_ della politica, pertanto l&#39;organismo deve includere tutte le informazioni richieste, come illustrato nell&#39;esempio seguente.

**Formato API**

```http
PUT /policies/custom/{id}
```

**Richiesta**

In questo esempio, le condizioni per l&#39;esportazione di dati a terzi sono cambiate e ora è necessario che il criterio creato neghi questa azione di marketing se sono presenti etichette `C1 AND (C3 OR C7)` dati. Utilizzate la seguente chiamata per aggiornare il criterio esistente.

```SHELL
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
            {
              "operator": "OR",
              "operands": [
                {"label": "C3"},
                {"label": "C7"}
              ]
            }
          ]
        }
      }'
```

**Risposta**

Una richiesta di aggiornamento riuscita restituisce uno stato HTTP 200 (OK) e il corpo della risposta mostra il criterio aggiornato. Il valore `id` deve corrispondere a quello `id` inviato nella richiesta.

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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550701472910,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Aggiornare una parte di un criterio

Una parte specifica di un criterio può essere aggiornata utilizzando una richiesta PATCH. A differenza delle richieste PUT che _riscritgono_ il criterio, PATCH richiede di aggiornare solo il percorso specificato nel corpo della richiesta. Questo è particolarmente utile quando desiderate abilitare o disabilitare un criterio, in quanto dovete inviare solo il percorso specifico che desiderate aggiornare (`/status`) e il relativo valore (`ENABLE` o `DISABLE`).

L&#39;API Policy Service al momento supporta le operazioni PATCH &quot;add&quot;, &quot;replace&quot; e &quot;remove&quot; e consente di combinare diversi aggiornamenti in una singola chiamata aggiungendo ogni oggetto come oggetto all&#39;interno dell&#39;array, come illustrato negli esempi seguenti.

**Formato API**

```http
PATCH /policies/custom/{id}
```

**Richiesta**

In questo esempio, stiamo utilizzando l&#39;operazione &quot;replace&quot; per cambiare lo stato del criterio da &quot;DRAFT&quot; a &quot;ENABLED&quot; e per aggiornare il campo della descrizione con una nuova descrizione. Potremmo anche aggiornare il campo di descrizione utilizzando l&#39;operazione &quot;delete&quot; per rimuovere la descrizione del criterio e quindi utilizzando l&#39;operazione &quot;add&quot; per aggiungere una nuova volta, come segue:

```SHELL
[
    {
        "op": "remove",
        "path": "/description"
    },
    {
        "op": "add",
        "path": "/description",
        "value": "New policy description."
    }
]
```

Quando si inviano più operazioni PATCH in un&#39;unica richiesta, ricordare che verranno elaborate nell&#39;ordine in cui appaiono nell&#39;array, in modo da garantire che le richieste vengano inviate nell&#39;ordine corretto, se necessario.

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

Una richiesta di aggiornamento corretta restituirà uno stato HTTP 200 (OK) e il corpo della risposta mostrerà il criterio aggiornato (&quot;status&quot; è ora &quot;ENABLED&quot; e &quot;description&quot; è stata modificata). Il criterio `id` deve corrispondere a quello `id` inviato nella richiesta.


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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550712163182,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Eliminare un criterio

Se è necessario rimuovere un criterio creato, è possibile farlo emettendo una richiesta DELETE all&#39;interno `id` del criterio che si desidera eliminare. È consigliabile eseguire prima una richiesta di ricerca (GET) per visualizzare il criterio e confermare che si tratta del criterio corretto da rimuovere. **Una volta eliminati, i criteri non possono essere recuperati.**

**Formato API**

```http
DELETE /policies/custom/{id}
```

**Richiesta**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Se il criterio è stato eliminato correttamente, il corpo della risposta sarà vuoto con lo stato HTTP 200 (OK).

È possibile confermare l&#39;eliminazione tentando di cercare nuovamente il criterio (GET). Dovreste ricevere uno stato HTTP 404 (non trovato) insieme a un messaggio di errore &quot;Non trovato&quot; perché il criterio è stato rimosso.
