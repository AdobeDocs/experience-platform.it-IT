---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criteri
topic: developer guide
translation-type: tm+mt
source-git-commit: 1a835c6c20c70bf03d956c601e2704b68d4f90fa
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---


# Valutazione politica

Una volta create le azioni di marketing e definite le policy, potete utilizzare l&#39;API del servizio criteri per valutare se eventuali criteri vengono violati da determinate azioni. I vincoli restituiti assumono la forma di un insieme di criteri che verrebbero violati tentando di eseguire un&#39;azione di marketing sui dati specificati contenenti etichette di utilizzo dei dati.

Per impostazione predefinita, **solo i criteri il cui stato è impostato su &quot;ENABLED&quot; partecipano alla valutazione**, tuttavia è possibile utilizzare il parametro query `?includeDraft=true` per includere i criteri &quot;DRAFT&quot; nella valutazione.

Le richieste di valutazione possono essere effettuate in uno dei tre modi seguenti:

1. Considerata una serie di etichette di utilizzo dei dati e un&#39;azione di marketing, l&#39;azione viola eventuali criteri?
1. Considerati uno o più set di dati e un&#39;azione di marketing, l&#39;azione viola eventuali criteri?
1. Dati uno o più set di dati e un sottoinsieme di uno o più campi all&#39;interno di ciascuno di tali set di dati, l&#39;azione viola eventuali criteri?

## Valutare i criteri utilizzando le etichette di utilizzo dei dati e un&#39;azione di marketing

La valutazione delle violazioni dei criteri in base alla presenza di etichette di utilizzo dei dati richiede di specificare il set di etichette che saranno presenti sui dati durante la richiesta. Questo avviene tramite l&#39;uso di parametri di query, dove le etichette di utilizzo dei dati vengono fornite come un elenco di valori separati da virgola, come illustrato nell&#39;esempio seguente.

**Formato API**

```http
GET /marketingActions/core/{marketingActionName}/constraints?duleLabels={value1},{value2}
GET /marketingActions/custom/{marketingActionName}/constraints?duleLabels={value1},{value2}
```

**Richiesta**

La richiesta di esempio riportata di seguito valuta un&#39;azione di marketing rispetto alle etichette C1 e C3. Durante la valutazione dei criteri utilizzando le etichette di utilizzo dei dati, tenere presente quanto segue:
* **Le etichette di utilizzo dei dati sono con distinzione tra maiuscole e minuscole.** La richiesta di cui sopra restituisce un criterio violato, mentre la stessa richiesta viene effettuata utilizzando etichette in lettere minuscole (ad es. `"c1,c3"`, `"C1,c3"`, `"c1,C3"`) no.
* **Prestate attenzione agli`AND``OR`operatori e agli operatori nelle espressioni dei criteri.** In questo esempio, se l&#39;etichetta (`C1` o `C3`) fosse apparsa da sola nella richiesta, l&#39;azione di marketing non avrebbe violato questo criterio. Sono necessarie entrambe le etichette (`C1 AND C3`) per restituire la politica violata. Assicurati di valutare attentamente i criteri e di definirne le espressioni con la stessa attenzione.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

L&#39;oggetto response include un `duleLabels` array che deve corrispondere alle etichette inviate nella richiesta. Se l&#39;esecuzione dell&#39;azione di marketing specificata rispetto alle etichette di utilizzo dei dati viola un criterio, l&#39; `violatedPolicies` array conterrà i dettagli del criterio o dei criteri interessati. Se non vengono violati i criteri, l&#39; `violatedPolicies` array appare vuoto (`[]`).

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

## Valutazione dei criteri tramite set di dati e un&#39;azione di marketing

È inoltre possibile valutare le violazioni dei criteri specificando l&#39;ID di uno o più set di dati da cui è possibile raccogliere le etichette di utilizzo dei dati. Questa operazione viene eseguita eseguendo una richiesta POST all&#39;endpoint principale o personalizzato per un&#39;azione di marketing e specificando gli ID di set di dati all&#39;interno del corpo della richiesta, come mostrato di seguito. `/constraints`

**Formato API**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**Richiesta**

Il corpo della richiesta contiene un array con un oggetto per ciascun ID dataset. Dal momento che state inviando un corpo di richiesta, il &quot;Content-Type: l&#39;intestazione della richiesta application/json&quot; è obbligatoria, come illustrato nell&#39;esempio seguente.

```SHELL
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

**Risposta**

L&#39;oggetto response include una `duleLabels` matrice che contiene un elenco consolidato di tutte le etichette trovate all&#39;interno dei set di dati specificati. Questo elenco include etichette a livello di set di dati e di campi su tutti i campi all&#39;interno del set di dati.

La risposta include anche una `discoveredLabels` matrice contenente oggetti per ogni dataset, `datasetLabels` suddivisi in etichette a livello di set di dati e di campi. Ogni etichetta a livello di campo mostra il percorso del campo specifico con tale etichetta.

Se l&#39;azione di marketing specificata viola un criterio che include `duleLabels` i set di dati, la `violatedPolicies` matrice conterrà i dettagli del criterio o dei criteri interessati. Se non vengono violati i criteri, l&#39; `violatedPolicies` array appare vuoto (`[]`).

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

## Valutare i criteri utilizzando set di dati, campi e un&#39;azione di marketing

Oltre a fornire uno o più ID di set di dati, è possibile specificare anche un sottoinsieme di campi all’interno di ciascun set di dati, a indicare che devono essere valutate solo le etichette di utilizzo dei dati in tali campi. Simile alla richiesta POST che interessa solo i set di dati, questa richiesta aggiunge al corpo della richiesta campi specifici per ogni set di dati.

Quando si valutano i criteri utilizzando i campi dataset, tenere presente quanto segue:

* **I nomi dei campi sono con distinzione tra maiuscole e minuscole.** Quando forniscono i campi, devono essere scritti esattamente come appaiono nel set di dati (ad esempio, `firstName` vs `firstname`).
* **Ereditarietà dell&#39;etichetta del set di dati.** le etichette di utilizzo dei dati possono essere applicate a più livelli e vengono ereditate verso il basso. Se le valutazioni dei criteri non restituiscono il risultato desiderato, verificare le etichette ereditate dai set di dati fino ai campi oltre a quelli applicati a livello di campo.

**Formato API**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**Richiesta**

Il corpo della richiesta contiene un array con un oggetto per ciascun ID set di dati e il sottoinsieme di campi all&#39;interno di tale set di dati da utilizzare per la valutazione. Dal momento che state inviando un corpo di richiesta, il &quot;Content-Type: l&#39;intestazione della richiesta application/json&quot; è obbligatoria, come illustrato nell&#39;esempio seguente.

```SHELL
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

**Risposta**

L&#39;oggetto response include un `duleLabels` array che contiene l&#39;elenco consolidato di etichette trovate nei campi specificati. Tenere presente che include anche le etichette dei set di dati, in quanto vengono ereditate fino ai campi.

Se un criterio viene violato eseguendo l&#39;azione di marketing specificata sui dati nei campi forniti, la `violatedPolicies` matrice conterrà i dettagli del criterio o dei criteri interessati. Se non vengono violati i criteri, l&#39; `violatedPolicies` array appare vuoto (`[]`).

Nella risposta seguente, l&#39;elenco di `duleLabels` è ora più breve, così come `discoveredLabels` per ogni set di dati, in quanto include solo i campi specificati nel corpo della richiesta. Noterete inoltre che il criterio precedentemente violato, &quot;Targeting Ads or Content&quot; (Annunci di targeting o contenuto) ha richiesto entrambe `C4 AND C6` le etichette, pertanto non viene più violato e l&#39; `violatedPolicies` array appare vuoto.

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

## Valutazione delle politiche [!DNL Real-time Customer Profile]

L&#39; [!DNL Policy Service] API può essere utilizzata anche per verificare la presenza di violazioni dei criteri che implicano l&#39;uso di [!DNL Real-time Customer Profile] segmenti. Per ulteriori informazioni, consulta l’esercitazione sull’ [imposizione della conformità per l’utilizzo dei dati per i segmenti](../../segmentation/tutorials/governance.md) di pubblico.