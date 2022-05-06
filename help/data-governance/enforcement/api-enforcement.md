---
keywords: Experience Platform;home;argomenti popolari;applicazione dei criteri;applicazione automatica;applicazione basata su API;governance dei dati;test
solution: Experience Platform
title: Applicare i criteri di utilizzo dei dati utilizzando l’API del servizio criteri
topic-legacy: guide
type: Tutorial
description: Dopo aver creato etichette di utilizzo dei dati per i dati e aver creato criteri di utilizzo per le azioni di marketing rispetto a tali etichette, puoi utilizzare l’API del servizio criteri per valutare se un’azione di marketing eseguita su un set di dati o su un gruppo arbitrario di etichette costituisca una violazione dei criteri. Puoi quindi impostare i tuoi protocolli interni per gestire le violazioni dei criteri in base alla risposta API.
exl-id: 093db807-c49d-4086-a676-1426426b43fd
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 2%

---

# Applica i criteri di utilizzo dei dati utilizzando [!DNL Policy Service] API

Dopo aver creato le etichette di utilizzo dei dati per i dati e aver creato i criteri di utilizzo per le azioni di marketing rispetto a tali etichette, puoi utilizzare la funzione [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) valutare se un’azione di marketing eseguita su un set di dati o su un gruppo arbitrario di etichette costituisce una violazione dei criteri. Puoi quindi impostare i tuoi protocolli interni per gestire le violazioni dei criteri in base alla risposta API.

>[!NOTE]
>
>Per impostazione predefinita, solo i criteri il cui stato è impostato su `ENABLED` può partecipare alla valutazione. Consentire `DRAFT` Criteri per partecipare alla valutazione, è necessario includere il parametro query `includeDraft=true` nel percorso della richiesta.

In questo documento sono descritti i passaggi da seguire per utilizzare il [!DNL Policy Service] API per verificare la presenza di violazioni dei criteri in scenari diversi.

## Introduzione

Questa esercitazione richiede una comprensione approfondita dei seguenti concetti chiave coinvolti nell&#39;applicazione dei criteri di utilizzo dei dati:

* [Governance dei dati](../home.md): Il quadro [!DNL Platform] applica la conformità per l’utilizzo dei dati.
   * [Etichette di utilizzo dati](../labels/overview.md): Le etichette di utilizzo dei dati vengono applicate ai set di dati (e/o ai singoli campi all’interno di tali set di dati), specificando le restrizioni relative alla modalità di utilizzo dei dati.
   * [Criteri di utilizzo dei dati](../policies/overview.md): I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing consentite o limitate per determinati set di etichette di utilizzo dei dati.
* [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Prima di avviare questa esercitazione, controlla la [guida per sviluppatori](../api/getting-started.md) per informazioni importanti che devi conoscere al fine di effettuare correttamente le chiamate al [!DNL Policy Service] API, incluse le intestazioni richieste e come leggere le chiamate API di esempio.

## Valutare utilizzando le etichette e un’azione di marketing

Puoi valutare un criterio testando un’azione di marketing rispetto a un set di etichette di utilizzo dei dati che sarebbero in teoria presenti all’interno di un set di dati. Questo viene fatto attraverso l&#39;uso del `duleLabels` parametro query, in cui le etichette vengono fornite come elenco di valori separati da virgole, come mostrato nell’esempio seguente.

**Formato API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell’azione di marketing associata al criterio di utilizzo dei dati che si sta valutando. |
| `{LABEL_1}` | Un’etichetta di utilizzo dei dati su cui eseguire il test dell’azione di marketing. Deve essere fornita almeno un&#39;etichetta. Quando si forniscono più etichette, queste devono essere separate da virgole. |

**Richiesta**

La seguente richiesta verifica il `exportToThirdParty` azione di marketing contro le etichette `C1` e `C3`. Poiché il criterio di utilizzo dei dati creato in precedenza in questa esercitazione definisce il `C1` etichetta come una delle `deny` condizioni nella relativa espressione dei criteri, l&#39;azione di marketing deve attivare una violazione dei criteri.

>[!NOTE]
>
>Le etichette di utilizzo dei dati sono sensibili all’uso di maiuscole e minuscole. Le violazioni dei criteri si verificano solo quando le etichette definite nelle relative espressioni dei criteri corrispondono esattamente. In questo esempio, un `C1` l&#39;etichetta potrebbe causare una violazione, mentre un `c1` l&#39;etichetta non lo farebbe.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce l’URL per l’azione di marketing, le etichette di utilizzo su cui è stata eseguita la verifica e un elenco di tutti i criteri violati a seguito della verifica dell’azione rispetto a tali etichette. In questo esempio, il criterio &quot;Esporta dati in terze parti&quot; è visualizzato in `violatedPolicies` array, che indica che l&#39;azione di marketing ha attivato la violazione dei criteri prevista.

```json
{
    "timestamp": 1565727821209,
    "clientId": "string",
    "userId": "string",
    "imsOrg": "{ORG_ID}",
    "marketingActionRef": "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
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
            "created": 1565651746693,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER",
            "updated": 1565723012139,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
                }
            },
            "id": "5d51f322e553c814e67af1a3"
        }
    ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `violatedPolicies` | Una matrice che elenca tutti i criteri violati testando l’azione di marketing (specificato in `marketingActionRef`) contro i `duleLabels`. |

## Valutare utilizzando i set di dati

Puoi valutare un criterio di utilizzo dei dati testando un’azione di marketing rispetto a uno o più set di dati da cui è possibile raccogliere le etichette. A questo scopo, invia una richiesta POST a `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` e fornisce ID di set di dati all’interno del corpo della richiesta, come mostrato nell’esempio seguente.

**Formato API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell’azione di marketing associata al criterio che si sta valutando. |

**Richiesta**

La seguente richiesta verifica il `exportToThirdParty` azione di marketing rispetto a tre set di dati diversi. Ai set di dati viene fatto riferimento per tipo e ID in una matrice fornita nel payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
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
      "entityId": "5cc1fb685410ef14b748c55f",
      "entityMeta": {
          "fields": [
              "/properties/personalEmail/properties/address",
              "/properties/person/properties/name/properties/fullName"
          ]
      }
    }
  ]'
```

| Proprietà | Descrizione |
| --- | --- |
| `entityType` | Ogni elemento dell’array di payload deve indicare il tipo di entità da definire. Per questo caso d’uso, il valore sarà sempre &quot;dataSet&quot;. |
| `entityId` | Ogni elemento dell’array di payload deve fornire l’ID univoco di un set di dati. |
| `entityMeta.fields` | (Facoltativo) Matrice di [Puntatore JSON](../../landing/api-fundamentals.md#json-pointer) stringhe che fanno riferimento a campi specifici nello schema del set di dati. Se l’array è incluso, solo i campi contenuti nell’array partecipano alla valutazione. Eventuali campi dello schema non inclusi nell’array non parteciperanno alla valutazione.<br><br>Se questo campo non è incluso, tutti i campi all’interno dello schema del set di dati verranno inclusi nella valutazione. |

**Risposta**

Una risposta corretta restituisce l’URL per l’azione di marketing, le etichette di utilizzo raccolte dai set di dati forniti e un elenco di tutti i criteri violati a seguito del test dell’azione rispetto a tali etichette. In questo esempio, il criterio &quot;Esporta dati in terze parti&quot; è visualizzato in `violatedPolicies` array, che indica che l&#39;azione di marketing ha attivato la violazione dei criteri prevista.

```json
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
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
                        "path": "/properties/personalEmail/properties/address",
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/person/properties/name/properties/fullName"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
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
            "created": 1565651746693,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER",
            "updated": 1565723012139,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
                }
            },
            "id": "5d51f322e553c814e67af1a3"
        }
    ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `duleLabels` | Elenco di etichette di utilizzo dei dati estratte dai set di dati forniti nel payload della richiesta. |
| `discoveredLabels` | Elenco dei set di dati forniti nel payload della richiesta, che mostrano le etichette a livello di set di dati e di campi presenti in ciascuno di essi. |
| `violatedPolicies` | Una matrice che elenca tutti i criteri violati testando l’azione di marketing (specificato in `marketingActionRef`) contro i `duleLabels`. |

## Passaggi successivi

Leggendo questo documento, hai verificato con successo la presenza di violazioni dei criteri durante l’esecuzione di un’azione di marketing su un set di dati o su un set di etichette di utilizzo dei dati. Utilizzando i dati restituiti nelle risposte API, puoi impostare protocolli all’interno dell’applicazione di esperienza per applicare in modo appropriato le violazioni dei criteri quando si verificano.

Per informazioni su come Platform fornisce automaticamente l’applicazione dei criteri per i segmenti attivati, consulta la guida su [applicazione automatica](./auto-enforcement.md).
