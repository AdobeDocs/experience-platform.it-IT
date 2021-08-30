---
keywords: Experience Platform;home;argomenti popolari;applicazione dei criteri;applicazione automatica;applicazione basata su API;governance dei dati
solution: Experience Platform
title: Endpoint API per la valutazione dei criteri
topic-legacy: developer guide
description: Una volta create le azioni di marketing e definiti i criteri, puoi utilizzare l’API del servizio criteri per valutare se alcuni criteri sono violati da determinate azioni. I vincoli restituiti assumono la forma di un insieme di criteri che verrebbero violati tentando l'azione di marketing sui dati specificati contenenti etichette di utilizzo dei dati.
exl-id: f9903939-268b-492c-aca7-63200bfe4179
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 2%

---

# Endpoint di valutazione delle politiche

Una volta create le azioni di marketing e definite le policy, puoi utilizzare l’ [!DNL Policy Service] API per valutare se eventuali criteri sono violati da determinate azioni. I vincoli restituiti assumono la forma di un insieme di criteri che verrebbero violati tentando l&#39;azione di marketing sui dati specificati contenenti etichette di utilizzo dei dati.

Per impostazione predefinita, solo i criteri il cui stato è impostato su `ENABLED` partecipano alla valutazione. Tuttavia, puoi utilizzare il parametro di query `?includeDraft=true` per includere i criteri `DRAFT` nella valutazione.

Le richieste di valutazione possono essere effettuate in uno dei tre modi seguenti:

1. Dato un’azione di marketing e un set di etichette di utilizzo dei dati, l’azione viola eventuali criteri?
1. In presenza di un’azione di marketing e di uno o più set di dati, l’azione viola eventuali criteri?
1. Dato un’azione di marketing, uno o più set di dati e un sottoinsieme di uno o più campi all’interno di ciascuno di tali set di dati, l’azione viola eventuali criteri?

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte di [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla relativa documentazione, una guida per la lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API [!DNL Experience Platform].

## Valutare le violazioni dei criteri utilizzando le etichette di utilizzo dei dati {#labels}

Puoi valutare le violazioni dei criteri in base alla presenza di un set specifico di etichette di utilizzo dei dati utilizzando il parametro di query `duleLabels` in una richiesta di GET.

**Formato API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell’azione di marketing da sottoporre a test rispetto a un set di etichette di utilizzo dei dati. Puoi recuperare un elenco delle azioni di marketing disponibili effettuando una richiesta [GET all&#39;endpoint delle azioni di marketing](./marketing-actions.md#list). |
| `{LABELS_LIST}` | Un elenco separato da virgole di nomi di etichette di utilizzo dei dati su cui eseguire il test dell’azione di marketing. Ad esempio: `duleLabels=C1,C2,C3`<br><br>I nomi delle etichette sono sensibili all&#39;uso di maiuscole e minuscole. Assicurati di utilizzare le maiuscole/minuscole corrette quando le inserisci nel parametro `duleLabels` . |

**Richiesta**

La richiesta di esempio seguente valuta un’azione di marketing rispetto alle etichette C1 e C3.

>[!IMPORTANT]
>
>Tieni presente gli operatori `AND` e `OR` nelle espressioni dei criteri. Nell’esempio seguente, se nella richiesta fosse stata visualizzata solo l’etichetta (`C1` o `C3`), l’azione di marketing non avrebbe violato questo criterio. Per restituire i criteri violati sono necessarie entrambe le etichette (`C1` e `C3`). Assicurati di valutare attentamente i criteri e di definirli con la stessa attenzione.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta include una matrice `violatedPolicies` che contiene i dettagli dei criteri violati a seguito dell&#39;esecuzione dell&#39;azione di marketing sulle etichette fornite. Se non vengono violati i criteri, la matrice `violatedPolicies` sarà vuota.

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

Puoi valutare le violazioni dei criteri in base a un set di uno o più set di dati da cui è possibile raccogliere le etichette di utilizzo dei dati. A questo scopo, esegui una richiesta POST all’ endpoint `/constraints` per una specifica azione di marketing e fornisci un elenco di ID di set di dati all’interno del corpo della richiesta.

**Formato API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell’azione di marketing da sottoporre a test per uno o più set di dati. Puoi recuperare un elenco delle azioni di marketing disponibili effettuando una richiesta [GET all&#39;endpoint delle azioni di marketing](./marketing-actions.md#list). |

**Richiesta**

La seguente richiesta esegue l&#39;azione di marketing `crossSiteTargeting` rispetto a un set di tre set di dati per valutare eventuali violazioni dei criteri.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `entityType` | Il tipo di entità il cui ID è indicato nella proprietà di pari livello `entityId`. Attualmente, l’unico valore accettato è `dataSet`. |
| `entityId` | ID di un set di dati su cui eseguire il test dell’azione di marketing. È possibile ottenere un elenco di set di dati e dei relativi ID effettuando una richiesta di GET all’ endpoint `/dataSets` nell’ API [!DNL Catalog Service] . Per ulteriori informazioni, consulta la guida sull’ [elenco [!DNL Catalog] oggetti](../../catalog/api/list-objects.md) . |

**Risposta**

Una risposta corretta include una matrice `violatedPolicies` che contiene i dettagli dei criteri violati a seguito dell&#39;esecuzione dell&#39;azione di marketing sui set di dati specificati. Se non vengono violati i criteri, la matrice `violatedPolicies` sarà vuota.

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
| `duleLabels` | L&#39;oggetto response include una matrice `duleLabels` che contiene un elenco consolidato di tutte le etichette presenti nei set di dati specificati. Questo elenco include etichette a livello di set di dati e di campo su tutti i campi all’interno del set di dati. |
| `discoveredLabels` | La risposta include anche un array `discoveredLabels` contenente oggetti per ogni set di dati, che mostra `datasetLabels` suddivisi in etichette a livello di set di dati e di campi. Ogni etichetta a livello di campo mostra il percorso del campo specifico con tale etichetta. |

## Valutare le violazioni dei criteri utilizzando campi di set di dati specifici {#fields}

È possibile valutare le violazioni dei criteri in base a un sottoinsieme di campi all’interno di uno o più set di dati, in modo che vengano valutate solo le etichette di utilizzo dei dati applicate a tali campi.

Quando si valutano i criteri utilizzando i campi set di dati, tenere presente quanto segue:

* **I nomi dei campi fanno distinzione tra maiuscole e minuscole**: Quando forniscono i campi, devono essere scritti esattamente come compaiono nel set di dati (ad esempio,  `firstName` vs  `firstname`).
* **Ereditarietà** etichetta set di dati: I singoli campi in un set di dati ereditano tutte le etichette applicate a livello di set di dati. Se le valutazioni dei criteri non restituiscono come previsto, assicurati di verificare la presenza di eventuali etichette ereditate dal livello del set di dati fino ai campi, oltre a quelle applicate a livello di campo.

**Formato API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell’azione di marketing da testare su un sottoinsieme di campi di set di dati. Puoi recuperare un elenco delle azioni di marketing disponibili effettuando una richiesta [GET all&#39;endpoint delle azioni di marketing](./marketing-actions.md#list). |

**Richiesta**

La richiesta seguente verifica l’azione di marketing `crossSiteTargeting` su un set specifico di campi appartenenti a tre set di dati. Il payload è simile a una richiesta di valutazione [che coinvolge solo set di dati](#datasets), aggiungendo campi specifici per ogni set di dati da cui raccogliere le etichette.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `entityType` | Il tipo di entità il cui ID è indicato nella proprietà di pari livello `entityId`. Attualmente, l’unico valore accettato è `dataSet`. |
| `entityId` | ID di un set di dati i cui campi devono essere valutati rispetto all’azione di marketing. È possibile ottenere un elenco di set di dati e dei relativi ID effettuando una richiesta di GET all’ endpoint `/dataSets` nell’ API [!DNL Catalog Service] . Per ulteriori informazioni, consulta la guida sull’ [elenco [!DNL Catalog] oggetti](../../catalog/api/list-objects.md) . |
| `entityMeta.fields` | Matrice di percorsi per campi specifici all’interno dello schema del set di dati, fornita sotto forma di stringhe JSON Pointer. Per informazioni dettagliate sulla sintassi accettata per queste stringhe, consulta la sezione su [JSON Pointer](../../landing/api-fundamentals.md#json-pointer) nella guida Principi di base delle API . |

**Risposta**

Una risposta corretta include una matrice `violatedPolicies` che contiene i dettagli dei criteri violati in seguito all’esecuzione dell’azione di marketing sui campi del set di dati forniti. Se non vengono violati i criteri, la matrice `violatedPolicies` sarà vuota.

Confrontando la risposta di esempio riportata di seguito alla risposta [che coinvolge solo i set di dati](#datasets), l&#39;elenco delle etichette raccolte è più breve. Sono stati ridotti anche i `discoveredLabels` per ogni set di dati, in quanto includono solo i campi specificati nel corpo della richiesta. Inoltre, il criterio precedentemente violato `Targeting Ads or Content` richiede la presenza di entrambe le etichette `C4 AND C6` e non viene più violato come indicato dalla matrice vuota `violatedPolicies`.

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
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

## Valutare le politiche in blocco {#bulk}

L’endpoint `/bulk-eval` ti consente di eseguire più processi di valutazione in una singola chiamata API.

**Formato API**

```http
POST /bulk-eval
```

**Richiesta**

Il payload di una richiesta di valutazione in blocco deve essere un array di oggetti; uno per ogni processo di valutazione da eseguire. Per i processi che valutano in base ai set di dati e ai campi, è necessario fornire una matrice `entityList`. Per i processi che valutano in base alle etichette di utilizzo dei dati, è necessario fornire una matrice `labels`.

>[!WARNING]
>
>Se un processo di valutazione elencato contiene sia una matrice `entityList` che `labels`, si verifica un errore. Se desideri valutare la stessa azione di marketing in base sia ai set di dati che alle etichette, devi includere processi di valutazione separati per quell’azione di marketing.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/bulk-eval \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `evalRef` | URI dell’azione di marketing da testare su etichette o set di dati per violazioni dei criteri. |
| `includeDraft` | Per impostazione predefinita, solo le politiche abilitate partecipano alla valutazione. Se `includeDraft` è impostato su `true`, parteciperanno anche i criteri in stato `DRAFT`. |
| `labels` | Matrice di etichette di utilizzo dei dati su cui eseguire il test dell’azione di marketing.<br><br>**IMPORTANTE**: Quando si utilizza questa proprietà, NON è necessario includere una  `entityList` proprietà nello stesso oggetto. Per valutare la stessa azione di marketing utilizzando set di dati e/o campi, è necessario includere un oggetto separato nel payload della richiesta che contiene una matrice `entityList`. |
| `entityList` | Matrice di set di dati e (facoltativamente) campi specifici all’interno di tali set di dati per verificare l’azione di marketing rispetto a .<br><br>**IMPORTANTE**: Quando si utilizza questa proprietà, NON è necessario includere una  `labels` proprietà nello stesso oggetto. Per valutare la stessa azione di marketing utilizzando etichette di utilizzo dati specifiche, è necessario includere un oggetto separato nel payload della richiesta che contiene un array `labels`. |
| `entityType` | Il tipo di entità su cui eseguire il test dell’azione di marketing. Attualmente, è supportato solo `dataSet`. |
| `entityId` | ID di un set di dati su cui eseguire il test dell’azione di marketing. |
| `entityMeta.fields` | (Facoltativo) Un elenco di campi specifici all’interno del set di dati su cui eseguire il test dell’azione di marketing. |

**Risposta**

Una risposta corretta restituisce una serie di risultati di valutazione; uno per ogni processo di valutazione dei criteri inviato nella richiesta.

```json
[
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{IMS_ORG}",
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
      "imsOrg": "{IMS_ORG}",
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
          "imsOrg": "{IMS_ORG}",
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

## Valutazione dei criteri per [!DNL Real-time Customer Profile]

L’ API [!DNL Policy Service] può essere utilizzata anche per verificare la presenza di violazioni dei criteri che coinvolgono l’utilizzo di segmenti [!DNL Real-time Customer Profile]. Per ulteriori informazioni, consulta l’esercitazione sull’ [applicazione della conformità in materia di utilizzo dei dati per i segmenti di pubblico](../../segmentation/tutorials/governance.md) .
