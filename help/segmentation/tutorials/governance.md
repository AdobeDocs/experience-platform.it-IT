---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Applica la conformità all'utilizzo dei dati per i segmenti di pubblico
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1372'
ht-degree: 1%

---


# Applicazione della conformità dell&#39;utilizzo dei dati per un segmento di pubblico tramite API

Questa esercitazione descrive i passaggi per imporre la conformità dell&#39;utilizzo dei dati per i segmenti di pubblico Profilo cliente in tempo reale che utilizzano le API.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei seguenti componenti del  Adobe Experience Platform:

- [Profilo](../../profile/home.md)cliente in tempo reale: Il profilo cliente in tempo reale è un archivio di entità di ricerca generico e viene utilizzato per gestire i dati del modello dati esperienza (XDM) in Platform. Il profilo unisce i dati tra diverse risorse di dati aziendali e fornisce l&#39;accesso a tali dati in una presentazione unificata.
   - [Unisci criteri](../../profile/api/merge-policies.md): Regole utilizzate dal profilo cliente in tempo reale per determinare quali dati possono essere uniti in una visualizzazione unificata a determinate condizioni. I criteri di unione possono essere configurati a scopo di governance dei dati.
- [Segmentazione](../home.md): In che modo il profilo cliente in tempo reale divide un ampio gruppo di individui contenuti nello store del profilo in gruppi più piccoli che condividono caratteristiche simili e risponderanno in modo simile alle strategie di marketing.
- [Governance](../../data-governance/home.md)dei dati: La governance dei dati fornisce l&#39;infrastruttura per l&#39;etichettatura e l&#39;applicazione dell&#39;uso dei dati (DULE), utilizzando i seguenti componenti:
   - [Etichette](../../data-governance/labels/user-guide.md)di utilizzo dati: Etichette utilizzate per descrivere insiemi di dati e campi in termini di livello di sensibilità con cui gestire i rispettivi dati.
   - [Criteri](../../data-governance/policies/overview.md)di utilizzo dei dati: Configurazioni che indicano quali azioni di marketing sono consentite sui dati classificati da particolari etichette di utilizzo dei dati.
   - [Applicazione](../../data-governance/enforcement/overview.md)delle regole: Consente di applicare criteri di utilizzo dei dati e di impedire le operazioni di dati che costituiscono violazioni dei criteri.
- [Sandbox](../../sandboxes/home.md):  Experience Platform fornisce sandbox virtuali che dividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente chiamate alle API Platform.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi di  Experience Platform.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API Platform, è prima necessario completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API Experience Platform, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in  Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API Platform richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Platform, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

## Cercare un criterio di unione per la definizione di un segmento {#merge-policy}

Questo flusso di lavoro inizia con l&#39;accesso a un segmento di pubblico noto. I segmenti abilitati per l’uso in Profilo cliente in tempo reale contengono un ID criterio di unione all’interno della definizione del segmento. Questo criterio di unione contiene informazioni sui set di dati da includere nel segmento, che a loro volta contengono eventuali etichette di utilizzo dei dati applicabili.

Utilizzando l&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)Segmentazione, puoi cercare una definizione di segmento in base al relativo ID per trovare il criterio di unione associato.

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

I criteri di unione contengono informazioni sui set di dati di origine, che a loro volta contengono etichette di utilizzo dei dati. Potete consultare i dettagli di un criterio di unione fornendo l&#39;ID del criterio di unione in una richiesta GET all&#39;API del profilo.

**Formato API**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | ID del criterio di unione ottenuto nel passaggio [](#merge-policy)precedente. |

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

## Valutazione dei set di dati per le violazioni dei criteri

>[!NOTE]
>
> Questo passaggio presuppone che sia presente almeno un criterio di utilizzo dei dati attivo che impedisca l&#39;esecuzione di azioni di marketing specifiche su dati contenenti determinate etichette. Se non si dispone di criteri di utilizzo applicabili per i set di dati in fase di valutazione, seguire l&#39;esercitazione [sulla creazione dei](../../data-governance/policies/create.md) criteri per crearne uno prima di continuare con questo passaggio.

Dopo aver ottenuto gli ID dei set di dati di origine del criterio di unione, puoi utilizzare l&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) DULE Policy Service per valutare tali set di dati in base ad azioni di marketing specifiche, al fine di verificare la presenza di violazioni dei criteri di utilizzo dei dati.

Per valutare i set di dati, è necessario fornire il nome dell&#39;azione di marketing nel percorso di una richiesta POST, fornendo al contempo gli ID dei set di dati all&#39;interno del corpo della richiesta, come illustrato nell&#39;esempio seguente.

**Formato API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell&#39;azione di marketing associata al criterio di utilizzo dei dati per il quale si stanno valutando i set di dati. A seconda che il criterio sia stato definito da Adobe o dalla vostra organizzazione, dovete utilizzare `/marketingActions/core` o `/marketingActions/custom`, rispettivamente. |

**Richiesta**

La richiesta seguente verifica l&#39;azione di `exportToThirdParty` marketing rispetto ai set di dati ottenuti nel passaggio [](#datasets)precedente. Il payload della richiesta è un array contenente gli ID di ogni dataset.

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
| `entityType` | Ogni elemento nell&#39;array di payload deve indicare il tipo di entità da definire. In questo caso d’uso, il valore sarà sempre &quot;dataSet&quot;. |
| `entityID` | Ogni elemento nell&#39;array di payload deve fornire l&#39;ID univoco per un dataset. |

**Risposta**

Una risposta corretta restituisce l’URI per l’azione di marketing, le etichette di utilizzo dei dati raccolte dai set di dati forniti e un elenco di eventuali criteri di utilizzo dei dati violati a seguito del test dell’azione rispetto a tali etichette. In questo esempio, il criterio &quot;Esporta dati in terze parti&quot; viene visualizzato nell&#39; `violatedPolicies` array, a indicare che l&#39;azione di marketing ha generato una violazione del criterio.

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
| `discoveredLabels` | Un elenco dei set di dati forniti nel payload della richiesta, in cui sono visualizzate le etichette a livello di set di dati e di campi presenti in ciascuno di essi. |
| `violatedPolicies` | Un array che elenca tutti i criteri di utilizzo dei dati violati eseguendo il test dell&#39;azione di marketing (specificata in `marketingActionRef`) rispetto a quella fornita `duleLabels`. |

Utilizzando i dati restituiti nella risposta API, potete impostare protocolli all&#39;interno dell&#39;applicazione dell&#39;esperienza per applicare correttamente le violazioni dei criteri quando si verificano.

## Filtrare i campi dati

Se il segmento di pubblico non supera la valutazione, puoi regolare i dati inclusi nel segmento tramite uno dei due metodi descritti di seguito.

### Aggiorna il criterio di unione della definizione del segmento

Quando si aggiorna il criterio di unione di una definizione di segmento, vengono regolati i set di dati e i campi che verranno inclusi durante l&#39;esecuzione del processo di segmento. Per ulteriori informazioni, consulta la sezione sull&#39; [aggiornamento di un criterio](../../profile/api/merge-policies.md#update) di unione esistente nell&#39;esercitazione per l&#39;unione delle API.

### Limita campi dati specifici durante l&#39;esportazione del segmento

Quando si esporta un segmento in un dataset utilizzando l&#39;API Profilo cliente in tempo reale, è possibile filtrare i dati inclusi nell&#39;esportazione utilizzando il `fields` parametro. Tutti i campi di dati aggiunti a questo parametro verranno inclusi nell&#39;esportazione, mentre tutti gli altri campi di dati saranno esclusi.

Considerate un segmento con campi di dati denominati &quot;A&quot;, &quot;B&quot; e &quot;C&quot;. Se si desidera esportare solo il campo &quot;C&quot;, il `fields` parametro conterrà solo il campo &quot;C&quot;. In questo modo, i campi &quot;A&quot; e &quot;B&quot; sarebbero esclusi durante l’esportazione del segmento.

Per ulteriori informazioni, consulta la sezione sull’ [esportazione di un segmento](./evaluate-a-segment.md#export) nell’esercitazione sulla segmentazione.

## Passaggi successivi

Seguendo questa esercitazione, hai cercato le etichette di utilizzo dei dati associate a un segmento di pubblico e li hai testati per verificare la presenza di violazioni dei criteri rispetto a determinate azioni di marketing. Per ulteriori informazioni sulla governance dei dati in  Experience Platform, consulta la panoramica sulla governance dei [dati](../../data-governance/home.md).
