---
keywords: ' Experience Platform;home;argomenti popolari;Applicazione delle regole;Applicazione automatica;Applicazione basata sulle API;governance dei dati;test'
solution: Experience Platform
title: Applicazione dei criteri di utilizzo dei dati tramite l'API di Servizio criteri
topic: guide
type: Tutorial
description: Dopo aver creato etichette di utilizzo dei dati per i dati e criteri di utilizzo per le azioni di marketing in base a tali etichette, potete utilizzare l'API Servizio criteri per valutare se un'azione di marketing eseguita su un set di dati o su un gruppo arbitrario di etichette costituisce una violazione dei criteri. Potete quindi configurare i vostri protocolli interni per gestire le violazioni dei criteri in base alla risposta API.
translation-type: tm+mt
source-git-commit: acc4fa59a4808ed9a32c2aaf664039e0d12dc1d8
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 1%

---


# Applicazione dei criteri di utilizzo dei dati tramite l&#39;API [!DNL Policy Service]

Dopo aver creato etichette di utilizzo dei dati per i dati e criteri di utilizzo per le azioni di marketing in base a tali etichette, è possibile utilizzare la [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) per valutare se un&#39;azione di marketing eseguita su un set di dati o su un gruppo arbitrario di etichette costituisce una violazione dei criteri. Potete quindi configurare i vostri protocolli interni per gestire le violazioni dei criteri in base alla risposta API.

>[!NOTE]
>
>Per impostazione predefinita, solo i criteri il cui stato è impostato su `ENABLED` possono partecipare alla valutazione. Per consentire ai criteri `DRAFT` di partecipare alla valutazione, è necessario includere il parametro di query `includeDraft=true` nel percorso della richiesta.

In questo documento sono descritti i passaggi necessari per utilizzare l&#39;API [!DNL Policy Service] per verificare la presenza di violazioni dei criteri in scenari diversi.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei seguenti concetti chiave relativi all&#39;applicazione dei criteri di utilizzo dei dati:

* [Governance](../home.md) dei dati: Il framework in base al quale  [!DNL Platform] viene applicata la conformità all&#39;utilizzo dei dati.
   * [Etichette](../labels/overview.md) di utilizzo dati: Le etichette di utilizzo dei dati vengono applicate ai set di dati (e/o ai singoli campi all&#39;interno di tali set di dati), specificando le restrizioni relative alla modalità di utilizzo dei dati.
   * [Criteri](../policies/overview.md) di utilizzo dei dati: I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing consentite o limitate per certi set di etichette di utilizzo dei dati.
* [Sandbox](../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Prima di avviare questa esercitazione, consultare la [guida allo sviluppo](../api/getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate all&#39;API [!DNL Policy Service], incluse le intestazioni richieste e come leggere le chiamate API di esempio.

## Valutare utilizzando etichette e un&#39;azione di marketing

È possibile valutare un criterio eseguendo il test di un&#39;azione di marketing rispetto a un insieme di etichette di utilizzo dei dati che potrebbero essere presenti all&#39;interno di un dataset. Ciò avviene tramite l&#39;uso del parametro di query `duleLabels`, dove le etichette vengono fornite come un elenco di valori separati da virgola, come illustrato nell&#39;esempio seguente.

**Formato API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell&#39;azione di marketing associata al criterio di utilizzo dei dati che si sta valutando. |
| `{LABEL_1}` | Etichetta di utilizzo dei dati per sottoporre a test l&#39;azione di marketing. Deve essere fornita almeno un&#39;etichetta. Quando si forniscono più etichette, queste devono essere separate da virgole. |

**Richiesta**

La richiesta seguente verifica l&#39;azione di marketing `exportToThirdParty` rispetto alle etichette `C1` e `C3`. Poiché il criterio di utilizzo dei dati creato in precedenza in questa esercitazione definisce l&#39;etichetta `C1` come una delle `deny` condizioni nell&#39;espressione del criterio, l&#39;azione di marketing deve attivare una violazione del criterio.

>[!NOTE]
>
>Le etichette di utilizzo dei dati sono sensibili alle maiuscole/minuscole. Le violazioni dei criteri si verificano solo se le etichette definite nelle relative espressioni dei criteri corrispondono esattamente. In questo esempio, un&#39;etichetta `C1` attiverebbe una violazione, mentre un&#39;etichetta `c1` non lo farebbe.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce l&#39;URL dell&#39;azione di marketing, le etichette di utilizzo su cui è stata eseguita la verifica e un elenco di eventuali criteri violati a seguito del test dell&#39;azione rispetto a tali etichette. In questo esempio, il criterio &quot;Esporta dati in terze parti&quot; è visualizzato nell&#39;array `violatedPolicies`, a indicare che l&#39;azione di marketing ha attivato la violazione prevista del criterio.

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
| `violatedPolicies` | Un array che elenca tutti i criteri violati eseguendo il test dell&#39;azione di marketing (specificata in `marketingActionRef`) rispetto al `duleLabels` fornito. |

## Valutare utilizzando i dataset

È possibile valutare un criterio di utilizzo dei dati eseguendo il test di un&#39;azione di marketing in base a uno o più set di dati da cui è possibile raccogliere le etichette. A questo scopo, è necessario effettuare una richiesta di POST a `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` e fornire gli ID del set di dati all&#39;interno del corpo della richiesta, come illustrato nell&#39;esempio seguente.

**Formato API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell&#39;azione di marketing associata al criterio che si sta valutando. |

**Richiesta**

La richiesta seguente verifica l&#39;azione di marketing `exportToThirdParty` rispetto a tre set di dati diversi. Ai set di dati si fa riferimento per tipo e ID in un array fornito nel payload.

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
| `entityType` | Ogni elemento nell&#39;array di payload deve indicare il tipo di entità da definire. In questo caso d’uso, il valore sarà sempre &quot;dataSet&quot;. |
| `entityId` | Ogni elemento nell&#39;array di payload deve fornire l&#39;ID univoco per un dataset. |
| `entityMeta.fields` | (Facoltativo) Un array di stringhe [JSON Pointer](../../landing/api-fundamentals.md#json-pointer) che fanno riferimento a campi specifici nello schema del set di dati. Se questa matrice è inclusa, solo i campi contenuti nell&#39;array partecipano alla valutazione. Eventuali campi dello schema non inclusi nell&#39;array non parteciperanno alla valutazione.<br><br>Se questo campo non è incluso, tutti i campi all&#39;interno dello schema del set di dati saranno inclusi nella valutazione. |

**Risposta**

Una risposta corretta restituisce l&#39;URL dell&#39;azione di marketing, le etichette di utilizzo raccolte dai set di dati forniti e un elenco di eventuali criteri violati a seguito del test dell&#39;azione rispetto a tali etichette. In questo esempio, il criterio &quot;Esporta dati in terze parti&quot; è visualizzato nell&#39;array `violatedPolicies`, a indicare che l&#39;azione di marketing ha attivato la violazione prevista del criterio.

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
| `discoveredLabels` | Un elenco dei set di dati forniti nel payload della richiesta, in cui sono visualizzate le etichette a livello di set di dati e di campi presenti in ciascuno di essi. |
| `violatedPolicies` | Un array che elenca tutti i criteri violati eseguendo il test dell&#39;azione di marketing (specificata in `marketingActionRef`) rispetto al `duleLabels` fornito. |

## Passaggi successivi

Leggendo questo documento, hai verificato con successo la presenza di violazioni dei criteri durante l&#39;esecuzione di un&#39;azione di marketing su un dataset o un set di etichette di utilizzo dei dati. Utilizzando i dati restituiti nelle risposte API, potete impostare protocolli all&#39;interno dell&#39;applicazione dell&#39;esperienza per applicare correttamente le violazioni dei criteri quando si verificano.

Per informazioni su come la piattaforma fornisce automaticamente l&#39;applicazione dei criteri per i segmenti attivati, consultate la guida sull&#39; [imposizione automatica](./auto-enforcement.md).