---
solution: Experience Platform
title: Applicare la conformità dell’utilizzo dati per un segmento di pubblico utilizzando le API
type: Tutorial
description: Questo tutorial illustra i passaggi necessari per applicare le definizioni dei segmenti di conformità per l’utilizzo dei dati utilizzando le API.
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 2%

---

# Applicare la conformità dell’utilizzo dei dati per una definizione di segmento utilizzando le API

Questo tutorial illustra i passaggi necessari per applicare la conformità all’utilizzo dei dati per le definizioni dei segmenti utilizzando le API.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di [!DNL Adobe Experience Platform]:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): [!DNL Real-Time Customer Profile] è un archivio di entità di ricerca generico e viene utilizzato per gestire [!DNL Experience Data Model (XDM)] dati in [!DNL Platform]. Il profilo unisce i dati tra diverse risorse di dati aziendali e consente di accedere a tali dati in una presentazione unificata.
   - [Criteri di unione](../../profile/api/merge-policies.md): regole utilizzate da [!DNL Real-Time Customer Profile] per determinare quali dati possono essere uniti in una vista unificata in determinate condizioni. I criteri di unione possono essere configurati a scopo di governance dei dati.
- [[!DNL Segmentation]](../home.md): Come [!DNL Real-Time Customer Profile] divide un ampio gruppo di individui contenuti nell’archivio profili in gruppi più piccoli che condividono caratteristiche simili e rispondono in modo simile alle strategie di marketing.
- [Governance dei dati](../../data-governance/home.md): la governance dei dati fornisce l’infrastruttura per l’etichettatura e l’applicazione dell’utilizzo dei dati, utilizzando i seguenti componenti:
   - [Etichette di utilizzo dati](../../data-governance/labels/user-guide.md): etichette utilizzate per descrivere set di dati e campi in termini di livello di sensibilità con cui gestire i rispettivi dati.
   - [Criteri di utilizzo dati](../../data-governance/policies/overview.md): configurazioni che indicano quali azioni di marketing sono consentite nei dati classificati da particolari etichette di utilizzo dei dati.
   - [Applicazione dei criteri](../../data-governance/enforcement/overview.md): consente di applicare i criteri di utilizzo dei dati e di impedire le operazioni sui dati che costituiscono violazioni dei criteri.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per effettuare correttamente chiamate al [!DNL Platform] API.

### Lettura delle chiamate API di esempio

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nel [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori per le intestazioni richieste

Per effettuare chiamate a [!DNL Platform] , devi prima completare le [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolati in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedere [documentazione di panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Content-Type: application/json

## Cercare un criterio di unione per una definizione di segmento {#merge-policy}

Questo flusso di lavoro inizia con l’accesso a una definizione di segmento nota. Definizioni di segmenti abilitate per l’utilizzo in [!DNL Real-Time Customer Profile] contengono un ID del criterio di unione nella loro definizione del segmento. Questo criterio di unione contiene informazioni sui set di dati da includere nella definizione del segmento, che a sua volta contengono eventuali etichette di utilizzo dei dati applicabili.

Utilizzo di [!DNL Segmentation] API, puoi cercare una definizione di segmento in base al relativo ID per trovare il relativo criterio di unione associato.

**Formato API**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | ID della definizione del segmento che desideri cercare. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/24379cae-726a-4987-b7b9-79c32cddb5c1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della definizione del segmento.

```json
{
    "id": "24379cae-726a-4987-b7b9-79c32cddb5c1",
    "schema": { 
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 90,
    "imsOrgId": "{ORG_ID}",
    "name": "Cart abandons in CA",
    "description": "",
    "expression": {
        "type": "PQL", 
        "format": "pql/text", 
        "value": "homeAddress.countryISO = 'US'"
    },
    "mergePolicyId": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1556094486000,
    "updateEpoch": 1556094486000,
    "updateTime": 1556094486000
  }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `mergePolicyId` | ID del criterio di unione utilizzato per la definizione del segmento. Verrà utilizzato nel passaggio successivo. |

## Trovare i set di dati di origine dal criterio di unione {#datasets}

I criteri di unione contengono informazioni sui relativi set di dati di origine, che a loro volta contengono etichette di utilizzo dei dati. Per cercare i dettagli di un criterio di unione, devi fornire l’ID del criterio di unione in una richiesta GET al [!DNL Profile] API. Ulteriori informazioni sui criteri di unione sono disponibili nella sezione [guida dell’endpoint &quot;merge policies&quot;](../../profile/api/merge-policies.md).

**Formato API**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | L’ID del criterio di unione ottenuto nella [passaggio precedente](#merge-policy). |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del criterio di unione.

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{ORG_ID}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence", 
        "data": {
            "order": ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `schema.name` | Nome dello schema associato al criterio di unione. |
| `attributeMerge.type` | Tipo di configurazione della precedenza dei dati per il criterio di unione. Se il valore è `dataSetPrecedence`, i set di dati associati a questo criterio di unione sono elencati in `attributeMerge > data > order`. Se il valore è `timestampOrdered`, quindi tutti i set di dati associati allo schema di riferimento in `schema.name` sono utilizzati dal criterio di unione. |
| `attributeMerge.data.order` | Se il `attributeMerge.type` è `dataSetPrecedence`, questo attributo sarà un array contenente gli ID dei set di dati utilizzati da questo criterio di unione. Questi ID vengono utilizzati nel passaggio successivo. |

## Valuta i set di dati per le violazioni dei criteri

>[!NOTE]
>
> Questo passaggio presuppone che tu disponga di almeno un criterio di utilizzo dei dati attivo che impedisca l’esecuzione di specifiche azioni di marketing sui dati contenenti determinate etichette. Se non disponi di criteri di utilizzo applicabili per i set di dati valutati, segui la [tutorial sulla creazione dei criteri](../../data-governance/policies/create.md) per crearne uno prima di continuare con questo passaggio.

Dopo aver ottenuto gli ID dei set di dati di origine del criterio di unione, puoi utilizzare [API del servizio criteri](https://www.adobe.io/experience-platform-apis/references/policy-service/) valutare tali set di dati rispetto a specifiche azioni di marketing al fine di verificare la presenza di violazioni dei criteri di utilizzo dei dati.

Per valutare i set di dati, devi fornire il nome dell’azione di marketing nel percorso di una richiesta POST, fornendo al contempo gli ID dei set di dati nel corpo della richiesta, come mostrato nell’esempio di seguito.

**Formato API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell’azione di marketing associata ai criteri di utilizzo dei dati in base ai quali vengono valutati i set di dati. A seconda che il criterio sia stato definito da Adobe o dalla tua organizzazione, devi utilizzare `/marketingActions/core` o `/marketingActions/custom`, rispettivamente. |

**Richiesta**

La richiesta seguente verifica `exportToThirdParty` azione di marketing contro i set di dati ottenuti nel [passaggio precedente](#datasets). Il payload della richiesta è un array contenente gli ID di ciascun set di dati.

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
      "entityId": "5b95b155419ec801e6eee780"
    },
    {
      "entityType": "dataSet",
      "entityId": "5b7c86968f7b6501e21ba9df"
    }
  ]'
```

| Proprietà | Descrizione |
| --- | --- |
| `entityType` | Ogni elemento nella matrice del payload deve indicare il tipo di entità da definire. Per questo caso d’uso, il valore sarà sempre &quot;dataSet&quot;. |
| `entityID` | Ogni elemento nell’array di payload deve fornire l’ID univoco per un set di dati. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’URI per l’azione di marketing, le etichette di utilizzo dei dati raccolte dai set di dati forniti e un elenco di eventuali criteri di utilizzo dei dati violati a seguito del test dell’azione su tali etichette. In questo esempio, il criterio &quot;Export Data to Third Party&quot; (Esporta dati a terze parti) è illustrato nella `violatedPolicies` array, che indica che l’azione di marketing ha attivato una violazione dei criteri.

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
    "C5"
  ],
  "discoveredLabels": [
    {
      "entityType": "dataSet",
      "entityId": "5b95b155419ec801e6eee780",
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
      "entityId": "5b7c86968f7b6501e21ba9df",
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
| `duleLabels` | Elenco di etichette di utilizzo dei dati estratte dai set di dati forniti. |
| `discoveredLabels` | Elenco dei set di dati forniti nel payload della richiesta, con le etichette a livello di set di dati e di campo presenti in ognuno di essi. |
| `violatedPolicies` | Un array che elenca tutti i criteri di utilizzo dei dati violati dal test dell’azione di marketing (specificata in `marketingActionRef`) rispetto al fornito `duleLabels`. |

Utilizzando i dati restituiti nella risposta API, puoi impostare i protocolli all’interno dell’applicazione Experience per applicare in modo appropriato le violazioni dei criteri quando si verificano.

## Filtrare i campi dati

Se la definizione del segmento non supera la valutazione, puoi regolare i dati inclusi nella definizione del segmento tramite uno dei due metodi descritti di seguito.

### Aggiornare il criterio di unione della definizione del segmento

L’aggiornamento del criterio di unione di una definizione di segmento adeguerà i set di dati e i campi che verranno inclusi durante l’esecuzione del processo di segmentazione. Consulta la sezione su [aggiornamento di un criterio di unione esistente](../../profile/api/merge-policies.md#update) per ulteriori informazioni, consulta l’esercitazione sui criteri di unione API.

### Limita campi di dati specifici durante l’esportazione della definizione del segmento

Quando si esporta una definizione di segmento in un set di dati utilizzando [!DNL Segmentation] API, puoi filtrare i dati inclusi nell’esportazione utilizzando il `fields` parametro. Tutti i campi dati aggiunti a questo parametro verranno inclusi nell’esportazione, mentre tutti gli altri campi dati verranno esclusi.

Considera una definizione di segmento con campi di dati denominati &quot;A&quot;, &quot;B&quot; e &quot;C&quot;. Se desideri esportare solo il campo &quot;C&quot;, il campo `fields` Il parametro conterrebbe solo il campo &quot;C&quot;. In questo modo, i campi &quot;A&quot; e &quot;B&quot; verrebbero esclusi durante l’esportazione della definizione del segmento.

Consulta la sezione su [esportazione di una definizione di segmento](./evaluate-a-segment.md#export) per ulteriori informazioni, consulta l’esercitazione sulla segmentazione.

## Passaggi successivi

Seguendo questa esercitazione, hai cercato le etichette di utilizzo dei dati associate a una definizione di segmento e le hai testate per verificare la presenza di violazioni dei criteri rispetto a specifiche azioni di marketing. Per ulteriori informazioni sulla governance dei dati in [!DNL Experience Platform], leggi la panoramica per [Governance dei dati](../../data-governance/home.md).
