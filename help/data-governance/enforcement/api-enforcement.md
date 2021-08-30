---
keywords: Experience Platform;home;argomenti popolari;applicazione dei criteri;applicazione automatica;applicazione basata su API;governance dei dati;test
solution: Experience Platform
title: Applicare i criteri di utilizzo dei dati utilizzando l’API del servizio criteri
topic-legacy: guide
type: Tutorial
description: Dopo aver creato etichette di utilizzo dei dati per i dati e aver creato criteri di utilizzo per le azioni di marketing rispetto a tali etichette, puoi utilizzare l’API del servizio criteri per valutare se un’azione di marketing eseguita su un set di dati o su un gruppo arbitrario di etichette costituisca una violazione dei criteri. Puoi quindi impostare i tuoi protocolli interni per gestire le violazioni dei criteri in base alla risposta API.
exl-id: 093db807-c49d-4086-a676-1426426b43fd
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 2%

---

# Applica i criteri di utilizzo dei dati utilizzando l&#39;API [!DNL Policy Service]

Dopo aver creato le etichette di utilizzo dei dati per i dati e aver creato i criteri di utilizzo per le azioni di marketing rispetto a tali etichette, puoi utilizzare [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) per valutare se un&#39;azione di marketing eseguita su un set di dati o su un gruppo arbitrario di etichette costituisce una violazione dei criteri. Puoi quindi impostare i tuoi protocolli interni per gestire le violazioni dei criteri in base alla risposta API.

>[!NOTE]
>
>Per impostazione predefinita, solo i criteri il cui stato è impostato su `ENABLED` possono partecipare alla valutazione. Per consentire ai criteri `DRAFT` di partecipare alla valutazione, è necessario includere il parametro query `includeDraft=true` nel percorso della richiesta.

Questo documento fornisce passaggi su come utilizzare l’ API [!DNL Policy Service] per verificare la presenza di violazioni dei criteri in scenari diversi.

## Introduzione

Questa esercitazione richiede una comprensione approfondita dei seguenti concetti chiave coinvolti nell&#39;applicazione dei criteri di utilizzo dei dati:

* [Governance dei dati](../home.md): Il framework in base al quale  [!DNL Platform] viene applicata la conformità per l’utilizzo dei dati.
   * [Etichette](../labels/overview.md) di utilizzo dati: Le etichette di utilizzo dei dati vengono applicate ai set di dati (e/o ai singoli campi all’interno di tali set di dati), specificando le restrizioni relative alla modalità di utilizzo dei dati.
   * [Criteri](../policies/overview.md) di utilizzo dati: I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing consentite o limitate per determinati set di etichette di utilizzo dei dati.
* [Sandbox](../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Prima di avviare questa esercitazione, controlla la [guida per gli sviluppatori](../api/getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’ API [!DNL Policy Service], comprese le intestazioni richieste e come leggere le chiamate API di esempio.

## Valutare utilizzando le etichette e un’azione di marketing

Puoi valutare un criterio testando un’azione di marketing rispetto a un set di etichette di utilizzo dei dati che sarebbero in teoria presenti all’interno di un set di dati. Questo viene fatto utilizzando il parametro di query `duleLabels` , dove le etichette vengono fornite come elenco di valori separati da virgola, come mostrato nell’esempio seguente.

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

La richiesta seguente verifica l’azione di marketing `exportToThirdParty` rispetto alle etichette `C1` e `C3`. Poiché i criteri di utilizzo dei dati creati in precedenza in questa esercitazione definiscono l’etichetta `C1` come una delle condizioni `deny` nella relativa espressione dei criteri, l’azione di marketing deve attivare una violazione dei criteri.

>[!NOTE]
>
>Le etichette di utilizzo dei dati sono sensibili all’uso di maiuscole e minuscole. Le violazioni dei criteri si verificano solo quando le etichette definite nelle relative espressioni dei criteri corrispondono esattamente. In questo esempio, un&#39;etichetta `C1` potrebbe causare una violazione, mentre un&#39;etichetta `c1` no.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce l’URL per l’azione di marketing, le etichette di utilizzo su cui è stata eseguita la verifica e un elenco di tutti i criteri violati a seguito della verifica dell’azione rispetto a tali etichette. In questo esempio, il criterio &quot;Esporta dati in terze parti&quot; viene visualizzato nell&#39;array `violatedPolicies`, a indicare che l&#39;azione di marketing ha attivato la violazione dei criteri prevista.

```json
{
    "timestamp": 1565727821209,
    "clientId": "string",
    "userId": "string",
    "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
| `violatedPolicies` | Una matrice che elenca tutti i criteri violati testando l&#39;azione di marketing (specificata in `marketingActionRef`) rispetto al `duleLabels` fornito. |

## Valutare utilizzando i set di dati

Puoi valutare un criterio di utilizzo dei dati testando un’azione di marketing rispetto a uno o più set di dati da cui è possibile raccogliere le etichette. A tal fine, invia una richiesta POST a `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` e fornisce ID set di dati all’interno del corpo della richiesta, come mostrato nell’esempio seguente.

**Formato API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell’azione di marketing associata al criterio che si sta valutando. |

**Richiesta**

La richiesta seguente verifica l’azione di marketing `exportToThirdParty` rispetto a tre set di dati diversi. Ai set di dati viene fatto riferimento per tipo e ID in una matrice fornita nel payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
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
| `entityMeta.fields` | (Facoltativo) Array di stringhe [JSON Pointer](../../landing/api-fundamentals.md#json-pointer) che fanno riferimento a campi specifici nello schema del set di dati. Se l’array è incluso, solo i campi contenuti nell’array partecipano alla valutazione. Eventuali campi dello schema non inclusi nell’array non parteciperanno alla valutazione.<br><br>Se questo campo non è incluso, tutti i campi all’interno dello schema del set di dati verranno inclusi nella valutazione. |

**Risposta**

Una risposta corretta restituisce l’URL per l’azione di marketing, le etichette di utilizzo raccolte dai set di dati forniti e un elenco di tutti i criteri violati a seguito del test dell’azione rispetto a tali etichette. In questo esempio, il criterio &quot;Esporta dati in terze parti&quot; viene visualizzato nell&#39;array `violatedPolicies`, a indicare che l&#39;azione di marketing ha attivato la violazione dei criteri prevista.

```json
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
| `violatedPolicies` | Una matrice che elenca tutti i criteri violati testando l&#39;azione di marketing (specificata in `marketingActionRef`) rispetto al `duleLabels` fornito. |

## Passaggi successivi

Leggendo questo documento, hai verificato con successo la presenza di violazioni dei criteri durante l’esecuzione di un’azione di marketing su un set di dati o su un set di etichette di utilizzo dei dati. Utilizzando i dati restituiti nelle risposte API, puoi impostare protocolli all’interno dell’applicazione di esperienza per applicare in modo appropriato le violazioni dei criteri quando si verificano.

Per informazioni su come Platform fornisce automaticamente l’applicazione dei criteri per i segmenti attivati, consulta la guida sull’ [applicazione automatica](./auto-enforcement.md).
