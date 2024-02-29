---
keywords: Experience Platform;home;argomenti popolari;Applicazione dei criteri;Applicazione automatica;Imposizione basata su API;governance dei dati
solution: Experience Platform
title: Endpoint API per la valutazione dei criteri
description: Dopo aver creato le azioni di marketing e definito i criteri, è possibile utilizzare l’API del servizio criteri per valutare se alcuni criteri sono violati da determinate azioni. I vincoli restituiti assumono la forma di un set di criteri che verrebbero violati se si tentasse di eseguire un’azione di marketing sui dati specificati contenenti le etichette di utilizzo dei dati.
role: Developer
exl-id: f9903939-268b-492c-aca7-63200bfe4179
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1538'
ht-degree: 2%

---

# Endpoint di valutazione dei criteri

Dopo aver creato le azioni di marketing e definito i criteri di utilizzo dei dati, puoi utilizzare [!DNL Policy Service] API per valutare se alcuni criteri sono violati da determinate azioni. I vincoli restituiti assumono la forma di un set di criteri che verrebbero violati se si tentasse di eseguire un’azione di marketing sui dati specificati contenenti le etichette di utilizzo dei dati.

Per impostazione predefinita, solo i criteri il cui stato è impostato su `ENABLED` partecipare alla valutazione. Tuttavia, puoi utilizzare il parametro di query `?includeDraft=true` da includere `DRAFT` politiche in fase di valutazione.

Le richieste di valutazione possono essere effettuate in uno dei tre modi seguenti:

1. Considerate un’azione di marketing e un set di etichette di utilizzo dei dati, l’azione viola alcuni criteri?
1. Considerata un’azione di marketing e uno o più set di dati, l’azione viola alcuni criteri?
1. Considerata un’azione di marketing, uno o più set di dati e un sottoinsieme di uno o più campi all’interno di ciascuno di tali set di dati, l’azione viola eventuali criteri?

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte del [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Prima di continuare, controlla [guida introduttiva](./getting-started.md) per collegamenti alla documentazione correlata, una guida per la lettura delle chiamate API di esempio di questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a [!DNL Experience Platform] API.

## Valuta le violazioni dei criteri utilizzando le etichette di utilizzo dei dati {#labels}

È possibile valutare le violazioni dei criteri in base alla presenza di un set specifico di etichette di utilizzo dei dati utilizzando `duleLabels` parametro di query in una richiesta GET.

**Formato API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell’azione di marketing da verificare in base a un set di etichette di utilizzo dei dati. Per recuperare un elenco delle azioni di marketing disponibili, devi effettuare una [Richiesta di GET all’endpoint delle azioni di marketing](./marketing-actions.md#list). |
| `{LABELS_LIST}` | Un elenco separato da virgole di nomi di etichette di utilizzo dati su cui verificare l’azione di marketing. Ad esempio: `duleLabels=C1,C2,C3`<br><br>I nomi delle etichette fanno distinzione tra maiuscole e minuscole. Assicurati di usare la maiuscola/minuscola corretta quando li inserisci nell’elenco `duleLabels` parametro. |

**Richiesta**

L’esempio di richiesta seguente valuta un’azione di marketing rispetto alle etichette C1 e C3.

>[!IMPORTANT]
>
>Presta attenzione a `AND` e `OR` nelle espressioni dei criteri. Nell’esempio seguente, se una delle etichette (`C1` o `C3`) era apparso da solo nella richiesta, l’azione di marketing non avrebbe violato questo criterio. Accetta entrambe le etichette (`C1` e `C3`) per restituire la policy violata. Accertati di valutare attentamente le policy e di definirne le espressioni con la stessa attenzione.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta include `violatedPolicies` array, che contiene i dettagli dei criteri violati a seguito dell’esecuzione dell’azione di marketing contro le etichette fornite. Se non vengono violati i criteri, il `violatedPolicies` l’array sarà vuoto.

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "marketingActionRef": "https://platform.adobe.io/marketingActions/custom/sampleMarketingAction",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
            ],
            "description": "NEW content for description.",
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
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714340335,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
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

## Valutare le violazioni dei criteri utilizzando i set di dati {#datasets}

Puoi valutare le violazioni dei criteri in base a un set di uno o più set di dati da cui è possibile raccogliere le etichette di utilizzo dei dati. Questa operazione viene eseguita eseguendo una richiesta POST al `/constraints` endpoint per una specifica azione di marketing che fornisce un elenco di ID di set di dati all’interno del corpo della richiesta.

**Formato API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell’azione di marketing da testare rispetto a uno o più set di dati. Per recuperare un elenco delle azioni di marketing disponibili, devi effettuare una [Richiesta di GET all’endpoint delle azioni di marketing](./marketing-actions.md#list). |

**Richiesta**

La richiesta seguente esegue `crossSiteTargeting` azione di marketing su un set di tre set di dati da valutare per eventuali violazioni dei criteri.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319"
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e"
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f"
        }
      ]'
```

| Proprietà | Descrizione |
| --- | --- |
| `entityType` | Tipo di entità il cui ID è indicato nell&#39;elemento di pari livello `entityId` proprietà. Attualmente, l’unico valore accettato è `dataSet`. |
| `entityId` | L’ID di un set di dati su cui testare l’azione di marketing. È possibile ottenere un elenco di set di dati e i relativi ID corrispondenti effettuando una richiesta GET al `/dataSets` endpoint nella [!DNL Catalog Service] API. Consulta la guida su [elenco [!DNL Catalog] oggetti](../../catalog/api/list-objects.md) per ulteriori informazioni. |

**Risposta**

Una risposta corretta include `violatedPolicies` array, che contiene i dettagli dei criteri violati in seguito all’esecuzione dell’azione di marketing sui set di dati forniti. Se non vengono violati i criteri, il `violatedPolicies` l’array sarà vuoto.

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
    "duleLabels": [
        "C1",
        "C2",
        "C4",
        "C5",
        "C6"
    ],
    "discoveredLabels": [
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C6"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C4",
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/identityMap"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/journeyAI"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/createdByBatchID"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C1"
                        ],
                        "path": "/properties/identityMap"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/createdByBatchID"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": [
        {
            "name": "Targeting Ads or Content",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
            ],
            "description": "Data cannot be used for targeting any ads or content, either on-site or cross-site.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C4"
                    },
                    {
                        "label": "C6"
                    }
                ]
            },
            "imsOrg": "{ORG_ID}",
            "created": 1551141210463,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1551146178603,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/policies/custom/5c74895a74744d13dc2d87cc"
                }
            },
            "id": "5c74895a74744d13dc2d87cc"
        }
    ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `duleLabels` | L’oggetto di risposta include una `duleLabels` array contenente un elenco consolidato di tutte le etichette presenti all’interno dei set di dati specificati. Questo elenco include etichette a livello di set di dati e di campo su tutti i campi all’interno del set di dati. |
| `discoveredLabels` | La risposta include anche un `discoveredLabels` array contenente oggetti per ogni set di dati, con visualizzazione `datasetLabels` suddiviso in etichette a livello di set di dati e di campo. Ogni etichetta a livello di campo mostra il percorso del campo specifico con tale etichetta. |

## Valutare le violazioni dei criteri utilizzando campi di set di dati specifici {#fields}

È possibile valutare le violazioni dei criteri in base a un sottoinsieme di campi all’interno di uno o più set di dati, in modo che vengano valutate solo le etichette di utilizzo dei dati applicate a tali campi.

Quando valuti i criteri utilizzando i campi del set di dati, tieni presente quanto segue:

* **I nomi dei campi fanno distinzione tra maiuscole e minuscole**: quando fornisci i campi, questi devono essere scritti esattamente come sono visualizzati nel set di dati (ad esempio, `firstName` vs `firstname`).
* **Ereditarietà etichetta set di dati**: i singoli campi in un set di dati ereditano le etichette applicate a livello di set di dati. Se le valutazioni dei criteri non restituiscono come previsto, assicurati di verificare eventuali etichette ereditate dal livello del set di dati ai campi, oltre a quelle applicate a livello di campo.

**Formato API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell’azione di marketing da testare in base a un sottoinsieme di campi del set di dati. Per recuperare un elenco delle azioni di marketing disponibili, devi effettuare una [Richiesta di GET all’endpoint delle azioni di marketing](./marketing-actions.md#list). |

**Richiesta**

La richiesta seguente verifica l’azione di marketing `crossSiteTargeting` su un set specifico di campi appartenenti a tre set di dati. Il payload è simile a un [richiesta di valutazione riguardante solo set di dati](#datasets), aggiungendo campi specifici per ogni set di dati da cui raccogliere le etichette.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/faxPhone"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/geoUnit"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "entityMeta": {
                "fields": [
                    "/properties/faxPhone"
                ]
            }
        }
      ]'
```

| Proprietà | Descrizione |
| --- | --- |
| `entityType` | Tipo di entità il cui ID è indicato nell&#39;elemento di pari livello `entityId` proprietà. Attualmente, l’unico valore accettato è `dataSet`. |
| `entityId` | ID di un set di dati i cui campi devono essere valutati in base all’azione di marketing. È possibile ottenere un elenco di set di dati e i relativi ID corrispondenti effettuando una richiesta GET al `/dataSets` endpoint nella [!DNL Catalog Service] API. Consulta la guida su [elenco [!DNL Catalog] oggetti](../../catalog/api/list-objects.md) per ulteriori informazioni. |
| `entityMeta.fields` | Matrice di percorsi per campi specifici all’interno dello schema del set di dati, fornita sotto forma di stringhe puntatore JSON. Consulta la sezione su [Puntatore JSON](../../landing/api-fundamentals.md#json-pointer) per informazioni dettagliate sulla sintassi accettata per queste stringhe, consulta la guida sui concetti di base delle API. |

**Risposta**

Una risposta corretta include `violatedPolicies` array, che contiene i dettagli dei criteri violati in seguito all’esecuzione dell’azione di marketing sui campi del set di dati forniti. Se non vengono violati i criteri, il `violatedPolicies` l’array sarà vuoto.

Confronto della risposta di esempio seguente con [risposta che coinvolge solo set di dati](#datasets), tieni presente che l’elenco delle etichette raccolte è più breve. Il `discoveredLabels` per ogni set di dati sono stati ridotti anche, in quanto includono solo i campi specificati nel corpo della richiesta. Inoltre, la politica violata in precedenza `Targeting Ads or Content` richiede entrambi `C4 AND C6` le etichette da presentare, e non viene quindi più violato come indicato dal vuoto `violatedPolicies` array.

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
    "duleLabels": [
        "C2",
        "C5",
        "C6"
    ],
    "discoveredLabels": [
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C6"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": []
}
```

## Valutare i criteri in blocco {#bulk}

Il `/bulk-eval` L’endpoint consente di eseguire più processi di valutazione in una singola chiamata API.

**Formato API**

```http
POST /bulk-eval
```

**Richiesta**

Il payload di una richiesta di valutazione in blocco deve essere un array di oggetti, uno per ogni processo di valutazione da eseguire. Per i processi che eseguono la valutazione in base a set di dati e campi, è necessario specificare `entityList` è necessario specificare un array. Per i processi che vengono valutati in base alle etichette di utilizzo dei dati, è necessario specificare `labels` è necessario specificare un array.

>[!WARNING]
>
>Se un processo di valutazione elencato contiene sia `entityList` e un `labels` , si verificherà un errore. Se desideri valutare la stessa azione di marketing in base a set di dati ed etichette, devi includere processi di valutazione separati per tale azione di marketing.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/bulk-eval \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "labels": [
            "C1",
            "C2",
            "C3"
          ]
        },
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "entityList": [
            {
              "entityType": "dataSet",
              "entityId": "5b67f4dd9f6e710000ea9da4",
              "entityMeta": {
                "fields": [
                  "address"
                ]
              }
            }
          ]
        }
      ]'
```

| Proprietà | Descrizione |
| --- | --- |
| `evalRef` | URI dell’azione di marketing da testare in base a etichette o set di dati per individuare eventuali violazioni dei criteri. |
| `includeDraft` | Per impostazione predefinita, solo i criteri abilitati partecipano alla valutazione. Se `includeDraft` è impostato su `true`, criteri in `DRAFT` parteciperà anche lo status. |
| `labels` | Array di etichette di utilizzo dei dati per testare l’azione di marketing su.<br><br>**IMPORTANTE**: quando si utilizza questa proprietà, viene `entityList` non deve essere inclusa nello stesso oggetto. Per valutare la stessa azione di marketing utilizzando set di dati e/o campi, è necessario includere un oggetto separato nel payload della richiesta che contiene `entityList` array. |
| `entityList` | Un array di set di dati e (facoltativamente) campi specifici all’interno di tali set di dati per testare l’azione di marketing su.<br><br>**IMPORTANTE**: quando si utilizza questa proprietà, viene `labels` non deve essere inclusa nello stesso oggetto. Per valutare la stessa azione di marketing utilizzando etichette di utilizzo dei dati specifiche, è necessario includere un oggetto separato nel payload della richiesta che contiene `labels` array. |
| `entityType` | Tipo di entità su cui testare l’azione di marketing. Attualmente, solo `dataSet` è supportato. |
| `entityId` | L’ID di un set di dati su cui testare l’azione di marketing. |
| `entityMeta.fields` | (Facoltativo) Un elenco di campi specifici all’interno del set di dati per testare l’azione di marketing. |

**Risposta**

In caso di esito positivo, la risposta restituisce un array di risultati di valutazione, uno per ogni processo di valutazione dei criteri inviato nella richiesta.

```json
[
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{ORG_ID}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2",
        "C3"
      ],
      "violatedPolicies": []
    }
  },
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{ORG_ID}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2"
      ],
      "discoveredLabels": [
        {
          "entityType": "dataset",
          "entityId": "5b67f4dd9f6e710000ea9da4",
          "dataSetLabels": {
            "connection": {
              "labels": [

              ]
            },
            "dataset": {
              "labels": [
                "C1",
                "C2"
              ]
            },
            "fields": []
          }
        }
      ],
      "violatedPolicies": [
        {
          "name": "Email Policy",
          "status": "DRAFT",
          "marketingActionRefs": [
            "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting"
          ],
          "description": "Conditions under which we won't send marketing-based email",
          "deny": {
            "label": "C1",
            "operator": "AND",
            "operands": [
              {
                "label": "C1"
              },
              {
                "label": "C3"
              }
            ]
          },
          "id": "76131228-7654-11e8-adc0-fa7ae01bbebc",
          "imsOrg": "{ORG_ID}",
          "created": 1529696681413,
          "createdClient": "{CLIENT_ID}",
          "createdUser": "{USER_ID}",
          "updated": 1529697651972,
          "updatedClient": "{CLIENT_ID}",
          "updatedUser": "{USER_ID}",
          "_links": {
            "self": {
              "href": "./76131228-7654-11e8-adc0-fa7ae01bbebc"
            }
          }
        }
      ]
    }
  }
]
```

## Valutazione dei criteri per [!DNL Real-Time Customer Profile]

Il [!DNL Policy Service] L’API può essere utilizzata anche per verificare la presenza di violazioni della politica che comportano l’utilizzo di [!DNL Real-Time Customer Profile] segmenti. Guarda il tutorial su [applicazione della conformità all’utilizzo dei dati per i segmenti di pubblico](../../segmentation/tutorials/governance.md) per ulteriori informazioni.
