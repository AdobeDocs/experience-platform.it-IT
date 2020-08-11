---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criteri
topic: developer guide
translation-type: tm+mt
source-git-commit: cb3a17aa08c67c66101cbf3842bf306ebcca0305
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 1%

---


# Finalità della valutazione politica

Una volta create le azioni di marketing e definite le policy, potete utilizzare l&#39; [!DNL Policy Service] API per valutare se eventuali criteri vengono violati da determinate azioni. I vincoli restituiti assumono la forma di un insieme di criteri che verrebbero violati tentando di eseguire un&#39;azione di marketing sui dati specificati contenenti etichette di utilizzo dei dati.

Per impostazione predefinita, solo le politiche il cui stato è impostato per `ENABLED` partecipare alla valutazione. Tuttavia, potete utilizzare il parametro query `?includeDraft=true` per includere `DRAFT` i criteri nella valutazione.

Le richieste di valutazione possono essere effettuate in uno dei tre modi seguenti:

1. Considerate un&#39;azione di marketing e un insieme di etichette di utilizzo dei dati, l&#39;azione viola eventuali criteri?
1. Data un&#39;azione di marketing e uno o più set di dati, l&#39;azione viola eventuali criteri?
1. Considerata un&#39;azione di marketing, uno o più set di dati e un sottoinsieme di uno o più campi all&#39;interno di ciascuno di tali set di dati, l&#39;azione viola eventuali criteri?

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte dell&#39; [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Prima di continuare, consultate la guida [introduttiva per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente chiamate a qualsiasi](./getting-started.md) [!DNL Experience Platform] API.

## Valutazione delle violazioni dei criteri utilizzando le etichette di utilizzo dei dati {#labels}

È possibile valutare le violazioni dei criteri in base alla presenza di un set specifico di etichette di utilizzo dei dati utilizzando il parametro di `duleLabels` query in una richiesta di GET.

**Formato API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Il nome dell&#39;azione di marketing da sottoporre a test rispetto a un set di etichette di utilizzo dei dati. Puoi recuperare un elenco delle azioni di marketing disponibili effettuando una richiesta di [GET all&#39;endpoint](./marketing-actions.md#list)delle azioni di marketing. |
| `{LABELS_LIST}` | Un elenco separato da virgole di nomi di etichette di utilizzo dei dati con cui verificare l&#39;azione di marketing. Ad esempio: `duleLabels=C1,C2,C3`<br><br>I nomi delle etichette seguono la distinzione tra maiuscole e minuscole. Accertatevi di usare le maiuscole e le minuscole corrette per inserirle nel `duleLabels` parametro. |

**Richiesta**

La richiesta di esempio riportata di seguito valuta un&#39;azione di marketing rispetto alle etichette C1 e C3.

>[!IMPORTANT]
>
>Prestate attenzione agli `AND` `OR` operatori e agli operatori nelle espressioni dei criteri. Nell&#39;esempio seguente, se nella richiesta fosse stata visualizzata un&#39;etichetta (`C1` o `C3`) da sola, l&#39;azione di marketing non avrebbe violato tale criterio. Sono necessarie sia etichette (`C1` che `C3`) per restituire la politica violata. Assicurati di valutare attentamente i criteri e di definirne le espressioni con la stessa attenzione.

```sh
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta di successo include un `violatedPolicies` array che contiene i dettagli dei criteri violati a seguito dell&#39;esecuzione dell&#39;azione di marketing sulle etichette fornite. Se non vengono violati i criteri, la `violatedPolicies` matrice sarà vuota.

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

## Valutazione delle violazioni dei criteri tramite set di dati {#datasets}

È possibile valutare le violazioni dei criteri in base a un set di uno o più set di dati da cui è possibile raccogliere le etichette di utilizzo dei dati. Questa operazione viene eseguita eseguendo una richiesta di POST all&#39; `/constraints` endpoint per una specifica azione di marketing e fornendo un elenco di ID di set di dati all&#39;interno del corpo della richiesta.

**Formato API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Il nome dell&#39;azione di marketing da sottoporre a test in base a uno o più set di dati. Puoi recuperare un elenco delle azioni di marketing disponibili effettuando una richiesta di [GET all&#39;endpoint](./marketing-actions.md#list)delle azioni di marketing. |

**Richiesta**

La richiesta seguente esegue l&#39;azione di `crossSiteTargeting` marketing in base a un insieme di tre set di dati per valutare eventuali violazioni dei criteri.

```sh
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
| `entityType` | Il tipo di entità il cui ID è indicato nella `entityId` proprietà di pari livello. Attualmente, l&#39;unico valore accettato è `dataSet`. |
| `entityId` | ID di un set di dati con cui sottoporre a test l&#39;azione di marketing. È possibile ottenere un elenco di set di dati e dei relativi ID effettuando una richiesta di GET all&#39; `/dataSets` endpoint nell&#39; [!DNL Catalog Service] API. Per ulteriori informazioni, vedere la guida sull&#39; [ [!DNL Catalog] elenco degli oggetti](../../catalog/api/list-objects.md) . |

**Risposta**

Una risposta di successo include un `violatedPolicies` array che contiene i dettagli dei criteri violati a seguito dell&#39;esecuzione dell&#39;azione di marketing sui set di dati forniti. Se non vengono violati i criteri, la `violatedPolicies` matrice sarà vuota.

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
| `duleLabels` | L&#39;oggetto response include una `duleLabels` matrice che contiene un elenco consolidato di tutte le etichette trovate all&#39;interno dei set di dati specificati. Questo elenco include etichette a livello di set di dati e di campi su tutti i campi all&#39;interno del set di dati. |
| `discoveredLabels` | La risposta include anche una `discoveredLabels` matrice contenente oggetti per ogni dataset, `datasetLabels` suddivisi in etichette a livello di set di dati e di campi. Ogni etichetta a livello di campo mostra il percorso del campo specifico con tale etichetta. |

## Valutazione delle violazioni dei criteri utilizzando campi set di dati specifici {#fields}

È possibile valutare le violazioni dei criteri in base a un sottoinsieme di campi all&#39;interno di uno o più set di dati, in modo che vengano valutate solo le etichette di utilizzo dei dati applicate a tali campi.

Quando si valutano i criteri utilizzando i campi dataset, tenere presente quanto segue:

* **I nomi dei campi sono con distinzione tra maiuscole e minuscole**: Quando forniscono i campi, devono essere scritti esattamente come appaiono nel set di dati (ad esempio, `firstName` vs `firstname`).
* **Ereditarietà** dell&#39;etichetta del set di dati: I singoli campi di un set di dati ereditano tutte le etichette applicate a livello di set di dati. Se le valutazioni dei criteri non restituiscono come previsto, verificare la presenza di eventuali etichette che potrebbero essere state ereditate dal livello del set di dati fino ai campi, oltre a quelli applicati a livello di campo.

**Formato API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Il nome dell&#39;azione di marketing da sottoporre a test rispetto a un sottoinsieme di campi di set di dati. Puoi recuperare un elenco delle azioni di marketing disponibili effettuando una richiesta di [GET all&#39;endpoint](./marketing-actions.md#list)delle azioni di marketing. |

**Richiesta**

La richiesta seguente esegue il test dell&#39;azione di marketing `crossSiteTargeting` su un set specifico di campi appartenenti a tre set di dati. Il payload è simile a una richiesta di [valutazione che interessa solo i set di dati](#datasets), aggiungendo campi specifici per ogni set di dati da cui raccogliere le etichette.

```sh
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
| `entityType` | Il tipo di entità il cui ID è indicato nella `entityId` proprietà di pari livello. Attualmente, l&#39;unico valore accettato è `dataSet`. |
| `entityId` | ID di un set di dati i cui campi devono essere valutati in base all&#39;azione di marketing. È possibile ottenere un elenco di set di dati e dei relativi ID effettuando una richiesta di GET all&#39; `/dataSets` endpoint nell&#39; [!DNL Catalog Service] API. Per ulteriori informazioni, vedere la guida sull&#39; [ [!DNL Catalog] elenco degli oggetti](../../catalog/api/list-objects.md) . |
| `entityMeta.fields` | Un array di percorsi per campi specifici all&#39;interno dello schema del set di dati, fornito sotto forma di stringhe JSON Pointer. Per informazioni dettagliate sulla sintassi accettata per queste stringhe, consulta la sezione relativa al puntatore [](../../landing/api-fundamentals.md#json-pointer) JSON nella guida di base delle API. |

**Risposta**

Una risposta di successo include un `violatedPolicies` array che contiene i dettagli dei criteri violati a seguito dell&#39;esecuzione dell&#39;azione di marketing nei campi del set di dati forniti. Se non vengono violati i criteri, la `violatedPolicies` matrice sarà vuota.

Confrontando la risposta di esempio riportata di seguito con la [risposta che include solo set di dati](#datasets), si noti che l&#39;elenco delle etichette raccolte è più breve. Anche `discoveredLabels` per ogni set di dati sono stati ridotti, in quanto includono solo i campi specificati nel corpo della richiesta. Inoltre, il criterio precedentemente violato `Targeting Ads or Content` richiede la presentazione di entrambe `C4 AND C6` le etichette e non è più violato come indicato dall&#39;array vuoto `violatedPolicies` .

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

## Valutazione dei criteri in blocco {#bulk}

L&#39; `/bulk-eval` endpoint consente di eseguire più processi di valutazione in una singola chiamata API.

**Formato API**

```http
POST /bulk-eval
```

**Richiesta**

Il payload di una richiesta di valutazione di massa deve essere un array di oggetti; uno per ogni processo di valutazione da eseguire. Per i processi che valutano in base a insiemi di dati e campi, è necessario fornire un `entityList` array. Per i processi che valutano in base alle etichette di utilizzo dei dati, è necessario fornire una `labels` matrice.

>[!WARNING]
>
>Se un qualsiasi processo di valutazione elencato contiene sia un `entityList` array che un `labels` array, si verificherà un errore. Se desideri valutare la stessa azione di marketing in base a set di dati ed etichette, devi includere processi di valutazione separati per tale azione di marketing.

```sh
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
| `evalRef` | URI dell&#39;azione di marketing da sottoporre a test per etichette o set di dati per violazioni dei criteri. |
| `includeDraft` | Per impostazione predefinita, solo i criteri abilitati partecipano alla valutazione. Se `includeDraft` è impostato su `true`, parteciperanno anche le politiche in `DRAFT` stato. |
| `labels` | Un array di etichette di utilizzo dei dati con cui sottoporre a test l&#39;azione di marketing.<br><br>**IMPORTANTE **: Quando si utilizza questa proprietà, NON è necessario includere una`entityList`proprietà nello stesso oggetto. Per valutare la stessa azione di marketing utilizzando insiemi di dati e/o campi, è necessario includere nel payload della richiesta un oggetto separato che contenga un`entityList`array. |
| `entityList` | Un array di set di dati e (facoltativamente) campi specifici all&#39;interno di tali set di dati per sottoporre a test l&#39;azione di marketing.<br><br>**IMPORTANTE **: Quando si utilizza questa proprietà, NON è necessario includere una`labels`proprietà nello stesso oggetto. Per valutare la stessa azione di marketing utilizzando etichette di utilizzo dati specifiche, è necessario includere un oggetto separato nel payload della richiesta che contenga un`labels`array. |
| `entityType` | Il tipo di entità con cui sottoporre a test l&#39;azione di marketing. Al momento, `dataSet` è supportato solo. |
| `entityId` | ID di un set di dati con cui sottoporre a test l&#39;azione di marketing. |
| `entityMeta.fields` | (Facoltativo) Un elenco di campi specifici all&#39;interno del dataset per verificare l&#39;azione di marketing rispetto a. |

**Risposta**

Una risposta di successo restituisce un array di risultati di valutazione; uno per ogni processo di valutazione dei criteri inviato nella richiesta.

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

## Valutazione delle politiche [!DNL Real-time Customer Profile]

L&#39; [!DNL Policy Service] API può essere utilizzata anche per verificare la presenza di violazioni dei criteri che implicano l&#39;uso di [!DNL Real-time Customer Profile] segmenti. Per ulteriori informazioni, consulta l’esercitazione sull’ [imposizione della conformità per l’utilizzo dei dati per i segmenti](../../segmentation/tutorials/governance.md) di pubblico.