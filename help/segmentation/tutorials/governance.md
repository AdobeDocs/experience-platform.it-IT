---
keywords: Experience Platform;home;argomenti popolari;conformità all’utilizzo dei dati;applicare;applicare la conformità all’utilizzo dei dati;servizio di segmentazione;segmentazione;segmentazione;
solution: Experience Platform
title: Applicare la conformità in materia di utilizzo dei dati per un segmento di pubblico utilizzando le API
topic-legacy: tutorial
type: Tutorial
description: Questa esercitazione descrive i passaggi per applicare la conformità dell’utilizzo dei dati per i segmenti di pubblico Profilo cliente in tempo reale che utilizzano le API.
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 1%

---

# Applicare la conformità in materia di utilizzo dei dati per un segmento di pubblico utilizzando le API

Questa esercitazione descrive i passaggi per applicare la conformità in materia di utilizzo dei dati per i segmenti di pubblico [!DNL Real-time Customer Profile] che utilizzano le API.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di [!DNL Adobe Experience Platform]:

- [[!DNL Real-time Customer Profile]](../../profile/home.md):  [!DNL Real-time Customer Profile] è un archivio di entità di ricerca generico e viene utilizzato per gestire  [!DNL Experience Data Model (XDM)] i dati all’interno di  [!DNL Platform]. Il profilo unisce i dati tra varie risorse di dati aziendali e fornisce l’accesso a tali dati in una presentazione unificata.
   - [Criteri](../../profile/api/merge-policies.md) di unione: Regole utilizzate da  [!DNL Real-time Customer Profile] per determinare quali dati possono essere uniti in una visualizzazione unificata in determinate condizioni. I criteri di unione possono essere configurati a scopo [!DNL Data Governance].
- [[!DNL Segmentation]](../home.md): Come  [!DNL Real-time Customer Profile] divide un grande gruppo di individui contenuti nell’archivio profili in gruppi più piccoli che condividono caratteristiche simili e risponderanno in modo simile alle strategie di marketing.
- [[!DNL Data Governance]](../../data-governance/home.md):  [!DNL Data Governance] fornisce l’infrastruttura per l’etichettatura e l’applicazione dell’utilizzo dei dati, utilizzando i seguenti componenti:
   - [Etichette](../../data-governance/labels/user-guide.md) di utilizzo dati: Etichette utilizzate per descrivere i set di dati e i campi in termini di livello di sensibilità con cui gestire i rispettivi dati.
   - [Criteri](../../data-governance/policies/overview.md) di utilizzo dati: Configurazioni che indicano quali azioni di marketing sono consentite sui dati categorizzati da particolari etichette di utilizzo dei dati.
   - [Applicazione](../../data-governance/enforcement/overview.md) delle regole: Consente di applicare i criteri di utilizzo dei dati e di impedire le operazioni di dati che costituiscono violazioni dei criteri.
- [Sandbox](../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrai conoscere per effettuare correttamente le chiamate alle API [!DNL Platform] .

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- nome x-sandbox: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la documentazione di panoramica [sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Tipo di contenuto: application/json

## Cercare un criterio di unione per una definizione di segmento {#merge-policy}

Questo flusso di lavoro inizia con l’accesso a un segmento di pubblico noto. I segmenti abilitati per l’uso in [!DNL Real-time Customer Profile] contengono un ID criterio di unione all’interno della relativa definizione del segmento. Questo criterio di unione contiene informazioni sui set di dati da includere nel segmento, che a loro volta contengono eventuali etichette di utilizzo dei dati applicabili.

Utilizzando l’API [!DNL Segmentation], puoi cercare una definizione di segmento in base al relativo ID per trovare i criteri di unione associati.

**Formato API**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | ID della definizione del segmento da cercare. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/24379cae-726a-4987-b7b9-79c32cddb5c1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli della definizione del segmento.

```json
{
    "id": "24379cae-726a-4987-b7b9-79c32cddb5c1",
    "schema": { 
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 90,
    "imsOrgId": "{IMS_ORG}",
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
| `mergePolicyId` | ID del criterio di unione utilizzato per la definizione del segmento. Questo verrà utilizzato nel passaggio successivo. |

## Trovare i set di dati di origine dal criterio di unione {#datasets}

I criteri di unione contengono informazioni sui set di dati di origine, che a loro volta contengono etichette di utilizzo dei dati. Puoi cercare i dettagli di un criterio di unione fornendo l’ID del criterio di unione in una richiesta di GET all’ [!DNL Profile] API. Ulteriori informazioni sui criteri di unione sono disponibili nella [guida per l&#39;endpoint dei criteri di unione](../../profile/api/merge-policies.md).

**Formato API**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | L&#39;ID del criterio di unione ottenuto nel [passaggio precedente](#merge-policy). |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli del criterio di unione.

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{IMS_ORG}",
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
            "order" : ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `schema.name` | Nome dello schema associato al criterio di unione. |
| `attributeMerge.type` | Tipo di configurazione della precedenza dei dati per il criterio di unione. Se il valore è `dataSetPrecedence`, i set di dati associati a questo criterio di unione sono elencati in `attributeMerge > data > order`. Se il valore è `timestampOrdered`, tutti i set di dati associati allo schema a cui si fa riferimento in `schema.name` vengono utilizzati dal criterio di unione. |
| `attributeMerge.data.order` | Se `attributeMerge.type` è `dataSetPrecedence`, questo attributo sarà una matrice contenente gli ID dei set di dati utilizzati da questo criterio di unione. Questi ID vengono utilizzati nel passaggio successivo. |

## Valutare i set di dati per le violazioni dei criteri

>[!NOTE]
>
> Questo passaggio presuppone che tu disponga di almeno un criterio di utilizzo dei dati attivo che impedisce l’esecuzione di azioni di marketing specifiche su dati contenenti determinate etichette. Se non disponi di criteri di utilizzo applicabili per i set di dati in fase di valutazione, segui l&#39; [esercitazione sulla creazione dei criteri](../../data-governance/policies/create.md) per crearne uno prima di continuare con questo passaggio.

Dopo aver ottenuto gli ID dei set di dati di origine dei criteri di unione, puoi utilizzare l’ [API del servizio criteri](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) per valutare tali set di dati rispetto a azioni di marketing specifiche al fine di verificare la presenza di violazioni dei criteri di utilizzo dei dati.

Per valutare i set di dati, devi fornire il nome dell’azione di marketing nel percorso di una richiesta di POST, fornendo allo stesso tempo gli ID dei set di dati all’interno del corpo della richiesta, come mostrato nell’esempio seguente.

**Formato API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell&#39;azione di marketing associata al criterio di utilizzo dei dati per il quale si stanno valutando i set di dati. A seconda che il criterio sia stato definito dall&#39;Adobe o dall&#39;organizzazione, è necessario utilizzare rispettivamente `/marketingActions/core` o `/marketingActions/custom`. |

**Richiesta**

La richiesta seguente verifica l&#39;azione di marketing `exportToThirdParty` rispetto ai set di dati ottenuti nel [passaggio precedente](#datasets). Il payload della richiesta è un array contenente gli ID di ogni set di dati.

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
| `entityType` | Ogni elemento dell’array di payload deve indicare il tipo di entità da definire. Per questo caso d’uso, il valore sarà sempre &quot;dataSet&quot;. |
| `entityID` | Ogni elemento dell’array di payload deve fornire l’ID univoco di un set di dati. |

**Risposta**

Una risposta corretta restituisce l’URI per l’azione di marketing, le etichette di utilizzo dei dati raccolte dai set di dati specificati e un elenco di tutti i criteri di utilizzo dei dati che sono stati violati in seguito al test dell’azione rispetto a tali etichette. In questo esempio, il criterio &quot;Esporta dati in terze parti&quot; viene visualizzato nell&#39;array `violatedPolicies`, a indicare che l&#39;azione di marketing ha attivato una violazione dei criteri.

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
| `duleLabels` | Elenco di etichette di utilizzo dei dati estratte dai set di dati forniti. |
| `discoveredLabels` | Elenco dei set di dati forniti nel payload della richiesta, che mostrano le etichette a livello di set di dati e di campi presenti in ciascuno di essi. |
| `violatedPolicies` | Matrice che elenca tutti i criteri di utilizzo dei dati violati testando l’azione di marketing (specificata in `marketingActionRef`) rispetto al `duleLabels` fornito. |

Utilizzando i dati restituiti nella risposta API, puoi impostare protocolli all’interno dell’applicazione di esperienza per applicare in modo appropriato le violazioni dei criteri quando si verificano.

## Filtrare i campi dati

Se il segmento di pubblico non supera la valutazione, puoi regolare i dati inclusi nel segmento attraverso uno dei due metodi descritti di seguito.

### Aggiornare il criterio di unione della definizione del segmento

L’aggiornamento del criterio di unione di una definizione di segmento regola i set di dati e i campi che verranno inclusi durante l’esecuzione del processo di segmento. Per ulteriori informazioni, consulta la sezione sull’ [aggiornamento di un criterio di unione esistente](../../profile/api/merge-policies.md#update) nell’esercitazione sui criteri di unione delle API .

### Limita campi di dati specifici durante l’esportazione del segmento

Durante l’esportazione di un segmento in un set di dati utilizzando l’ API [!DNL Segmentation] , puoi filtrare i dati inclusi nell’esportazione utilizzando il parametro `fields` . Tutti i campi di dati aggiunti a questo parametro verranno inclusi nell’esportazione, mentre tutti gli altri campi di dati verranno esclusi.

Considera un segmento con campi di dati denominati &quot;A&quot;, &quot;B&quot; e &quot;C&quot;. Se si desidera esportare solo il campo &quot;C&quot;, il parametro `fields` conterrà solo il campo &quot;C&quot;. In questo modo, i campi &quot;A&quot; e &quot;B&quot; verrebbero esclusi durante l’esportazione del segmento.

Per ulteriori informazioni, consulta la sezione sull’ [esportazione di un segmento](./evaluate-a-segment.md#export) nell’esercitazione sulla segmentazione .

## Passaggi successivi

Seguendo questa esercitazione, hai cercato le etichette di utilizzo dei dati associate a un segmento di pubblico e le hai testate per individuare eventuali violazioni dei criteri rispetto a specifiche azioni di marketing. Per ulteriori informazioni su [!DNL Data Governance] in [!DNL Experience Platform], leggere la panoramica relativa a [[!DNL Data Governance]](../../data-governance/home.md).
