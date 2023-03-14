---
keywords: Experience Platform;home;argomenti popolari;Applicazione dei criteri;Imposizione automatica;Imposizione basata su API;governance dei dati;testing
solution: Experience Platform
title: Imporre i criteri di utilizzo dei dati utilizzando l’API del servizio criteri
type: Tutorial
description: Dopo aver creato le etichette di utilizzo dei dati per i dati e aver creato i criteri di utilizzo per le azioni di marketing su tali etichette, è possibile utilizzare l’API Servizio criteri per valutare se un’azione di marketing eseguita su un set di dati o su un gruppo arbitrario di etichette costituisce una violazione dei criteri. Puoi quindi configurare i tuoi protocolli interni per gestire le violazioni dei criteri in base alla risposta API.
exl-id: 093db807-c49d-4086-a676-1426426b43fd
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 2%

---

# Imponi criteri di utilizzo dati utilizzando [!DNL Policy Service] API

Dopo aver creato le etichette di utilizzo dei dati per i dati e aver creato i criteri di utilizzo per le azioni di marketing su tali etichette, puoi utilizzare [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) per valutare se un’azione di marketing eseguita su un set di dati o su un gruppo arbitrario di etichette costituisce una violazione dei criteri. Puoi quindi configurare i tuoi protocolli interni per gestire le violazioni dei criteri in base alla risposta API.

>[!NOTE]
>
>Per impostazione predefinita, solo i criteri il cui stato è impostato su `ENABLED` possono partecipare alla valutazione. Per consentire `DRAFT` criteri per partecipare alla valutazione, è necessario includere il parametro query `includeDraft=true` nel percorso della richiesta.

Questo documento descrive come utilizzare [!DNL Policy Service] API per verificare la presenza di violazioni dei criteri in scenari diversi.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti concetti chiave coinvolti nell’applicazione dei criteri di utilizzo dei dati:

* [Governance dei dati](../home.md): framework tramite il quale [!DNL Platform] applica la conformità all’utilizzo dei dati.
   * [Etichette di utilizzo dati](../labels/overview.md): le etichette di utilizzo dei dati vengono applicate ai set di dati (e/o ai singoli campi all’interno di tali set di dati), specificando restrizioni per l’utilizzo di tali dati.
   * [Criteri di utilizzo dati](../policies/overview.md): i criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing consentite o limitate per determinati set di etichette di utilizzo dei dati.
* [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Prima di iniziare questo tutorial, controlla [guida per sviluppatori](../api/getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate al [!DNL Policy Service] API, incluse le intestazioni richieste e la modalità di lettura delle chiamate API di esempio.

## Valutare utilizzando etichette e un’azione di marketing

Puoi valutare un criterio testando un’azione di marketing rispetto a un set di etichette di utilizzo dei dati che sarebbe ipoteticamente presente all’interno di un set di dati. Ciò avviene mediante l&#39;utilizzo di `duleLabels` parametro query, in cui le etichette vengono fornite come elenco di valori separati da virgole, come illustrato nell’esempio seguente.

**Formato API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell’azione di marketing associata ai criteri di utilizzo dei dati che stai valutando. |
| `{LABEL_1}` | Un’etichetta di utilizzo dei dati per testare l’azione di marketing su. È necessario fornire almeno un&#39;etichetta. Quando si forniscono più etichette, queste devono essere separate da virgole. |

**Richiesta**

La richiesta seguente verifica `exportToThirdParty` azione di marketing contro le etichette `C1` e `C3`. Poiché i criteri di utilizzo dei dati creati in precedenza in questa esercitazione definiscono `C1` etichetta come una delle `deny` nelle relative espressioni di criteri, l’azione di marketing deve attivare una violazione di criteri.

>[!NOTE]
>
>Le etichette di utilizzo dei dati fanno distinzione tra maiuscole e minuscole. Le violazioni dei criteri si verificano solo quando le etichette definite nelle relative espressioni dei criteri vengono associate esattamente. In questo esempio, un `C1` attiverebbe una violazione, mentre un `c1` L&#39;etichetta no.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce l’URL per l’azione di marketing, le etichette di utilizzo su cui è stata testata e un elenco di eventuali criteri violati a seguito del test dell’azione su tali etichette. In questo esempio, il criterio &quot;Export Data to Third Party&quot; (Esporta dati a terze parti) è illustrato nella `violatedPolicies` array, che indica che l’azione di marketing ha attivato la violazione dei criteri prevista.

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
| `violatedPolicies` | Un array che elenca tutti i criteri violati durante il test dell’azione di marketing (specificata in `marketingActionRef`) rispetto al fornito `duleLabels`. |

## Valuta utilizzando i set di dati

Puoi valutare un criterio di utilizzo dei dati testando un’azione di marketing rispetto a uno o più set di dati da cui è possibile raccogliere le etichette. A tale scopo, effettua una richiesta POST a `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` e fornendo ID di set di dati all’interno del corpo della richiesta, come mostrato nell’esempio di seguito.

**Formato API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell’azione di marketing associata al criterio che stai valutando. |

**Richiesta**

La richiesta seguente verifica `exportToThirdParty` azione di marketing su tre set di dati diversi. Si fa riferimento ai set di dati per tipo e ID in un array fornito nel payload.

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
| `entityType` | Ogni elemento nella matrice del payload deve indicare il tipo di entità da definire. Per questo caso d’uso, il valore sarà sempre &quot;dataSet&quot;. |
| `entityId` | Ogni elemento nell’array di payload deve fornire l’ID univoco per un set di dati. |
| `entityMeta.fields` | (Facoltativo) Array di [Puntatore JSON](../../landing/api-fundamentals.md#json-pointer) stringhe, con riferimento a campi specifici nello schema del set di dati. Se questo array è incluso, solo i campi contenuti nell’array partecipano alla valutazione. Eventuali campi dello schema non inclusi nell’array non parteciperanno alla valutazione.<br><br>Se questo campo non è incluso, nella valutazione verranno inclusi tutti i campi all’interno dello schema del set di dati. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’URL per l’azione di marketing, le etichette di utilizzo raccolte dai set di dati forniti e un elenco di eventuali criteri violati a seguito del test dell’azione su tali etichette. In questo esempio, il criterio &quot;Export Data to Third Party&quot; (Esporta dati a terze parti) è illustrato nella `violatedPolicies` array, che indica che l’azione di marketing ha attivato la violazione dei criteri prevista.

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
| `discoveredLabels` | Elenco dei set di dati forniti nel payload della richiesta, con le etichette a livello di set di dati e di campo presenti in ognuno di essi. |
| `violatedPolicies` | Un array che elenca tutti i criteri violati durante il test dell’azione di marketing (specificata in `marketingActionRef`) rispetto al fornito `duleLabels`. |

## Passaggi successivi

Dopo aver letto questo documento, hai verificato la presenza di violazioni dei criteri durante l’esecuzione di un’azione di marketing su un set di dati o su un set di etichette di utilizzo dei dati. Utilizzando i dati restituiti nelle risposte API, puoi impostare i protocolli all’interno dell’applicazione Experience per applicare in modo appropriato le violazioni dei criteri quando si verificano.

Per informazioni sul modo in cui Platform fornisce automaticamente l’applicazione dei criteri per i segmenti attivati, consulta la guida su [applicazione automatica](./auto-enforcement.md).
