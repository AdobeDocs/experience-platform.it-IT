---
keywords: Experience Platform;home;argomenti popolari;conformità all’utilizzo dei dati;applicare;applicare la conformità all’utilizzo dei dati;servizio di segmentazione;segmentazione;segmentazione;
solution: Experience Platform
title: Applicare la conformità in materia di utilizzo dei dati per un segmento di pubblico utilizzando le API
topic-legacy: tutorial
type: Tutorial
description: Questa esercitazione descrive i passaggi per applicare la conformità dell’utilizzo dei dati per i segmenti di pubblico Profilo cliente in tempo reale che utilizzano le API.
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1368'
ht-degree: 2%

---

# Applicare la conformità in materia di utilizzo dei dati per un segmento di pubblico utilizzando le API

Questa esercitazione descrive i passaggi per applicare la conformità in materia di utilizzo dei dati per [!DNL Real-time Customer Profile] segmenti di pubblico utilizzando le API.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di [!DNL Adobe Experience Platform]:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): [!DNL Real-time Customer Profile] è un archivio di entità di ricerca generico e viene utilizzato per gestire [!DNL Experience Data Model (XDM)] dati [!DNL Platform]. Il profilo unisce i dati tra varie risorse di dati aziendali e fornisce l’accesso a tali dati in una presentazione unificata.
   - [Unisci criteri](../../profile/api/merge-policies.md): Regole utilizzate da [!DNL Real-time Customer Profile] per determinare quali dati possono essere uniti in una visualizzazione unificata in determinate condizioni. I criteri di unione possono essere configurati a scopo di governance dei dati.
- [[!DNL Segmentation]](../home.md): Come [!DNL Real-time Customer Profile] divide un ampio gruppo di utenti contenuti nell’archivio profili in gruppi più piccoli che condividono caratteristiche simili e risponderanno in modo simile alle strategie di marketing.
- [Governance dei dati](../../data-governance/home.md): La governance dei dati fornisce l’infrastruttura per l’etichettatura e l’applicazione dell’utilizzo dei dati, utilizzando i seguenti componenti:
   - [Etichette di utilizzo dati](../../data-governance/labels/user-guide.md): Etichette utilizzate per descrivere i set di dati e i campi in termini di livello di sensibilità con cui gestire i rispettivi dati.
   - [Criteri di utilizzo dei dati](../../data-governance/policies/overview.md): Configurazioni che indicano quali azioni di marketing sono consentite sui dati categorizzati da particolari etichette di utilizzo dei dati.
   - [Applicazione delle politiche](../../data-governance/enforcement/overview.md): Consente di applicare i criteri di utilizzo dei dati e di impedire le operazioni di dati che costituiscono violazioni dei criteri.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente le chiamate al [!DNL Platform] API.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione panoramica su sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Tipo di contenuto: application/json

## Cercare un criterio di unione per una definizione di segmento {#merge-policy}

Questo flusso di lavoro inizia con l’accesso a un segmento di pubblico noto. Segmenti abilitati per l’uso in [!DNL Real-time Customer Profile] contengono un ID criterio di unione nella relativa definizione del segmento. Questo criterio di unione contiene informazioni sui set di dati da includere nel segmento, che a loro volta contengono eventuali etichette di utilizzo dei dati applicabili.

Utilizzo della [!DNL Segmentation] API, puoi cercare una definizione di segmento in base al relativo ID per trovare i criteri di unione associati.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `mergePolicyId` | ID del criterio di unione utilizzato per la definizione del segmento. Questo verrà utilizzato nel passaggio successivo. |

## Trovare i set di dati di origine dal criterio di unione {#datasets}

I criteri di unione contengono informazioni sui set di dati di origine, che a loro volta contengono etichette di utilizzo dei dati. È possibile cercare i dettagli di un criterio di unione fornendo l&#39;ID del criterio di unione in una richiesta di GET al [!DNL Profile] API. Ulteriori informazioni sui criteri di unione sono disponibili nella sezione [guida all’endpoint dei criteri di unione](../../profile/api/merge-policies.md).

**Formato API**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | ID del criterio di unione ottenuto nel [passaggio precedente](#merge-policy). |

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

Una risposta corretta restituisce i dettagli del criterio di unione.

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
| `attributeMerge.type` | Tipo di configurazione della precedenza dei dati per il criterio di unione. Se il valore è `dataSetPrecedence`, i set di dati associati a questo criterio di unione sono elencati in `attributeMerge > data > order`. Se il valore è `timestampOrdered`, quindi tutti i set di dati associati allo schema a cui si fa riferimento in `schema.name` vengono utilizzati dal criterio di unione. |
| `attributeMerge.data.order` | Se la `attributeMerge.type` è `dataSetPrecedence`, questo attributo sarà una matrice contenente gli ID dei set di dati utilizzati da questo criterio di unione. Questi ID vengono utilizzati nel passaggio successivo. |

## Valutare i set di dati per le violazioni dei criteri

>[!NOTE]
>
> Questo passaggio presuppone che tu disponga di almeno un criterio di utilizzo dei dati attivo che impedisce l’esecuzione di azioni di marketing specifiche su dati contenenti determinate etichette. Se non disponi di criteri di utilizzo applicabili per i set di dati in fase di valutazione, segui la [esercitazione sulla creazione dei criteri](../../data-governance/policies/create.md) per crearne uno prima di continuare con questo passaggio.

Una volta ottenuti gli ID dei set di dati di origine dei criteri di unione, puoi utilizzare [API del servizio criteri](https://www.adobe.io/experience-platform-apis/references/policy-service/) valutare tali set di dati rispetto a azioni di marketing specifiche al fine di verificare la presenza di violazioni dei criteri di utilizzo dei dati.

Per valutare i set di dati, devi fornire il nome dell’azione di marketing nel percorso di una richiesta di POST, fornendo allo stesso tempo gli ID dei set di dati all’interno del corpo della richiesta, come mostrato nell’esempio seguente.

**Formato API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell&#39;azione di marketing associata al criterio di utilizzo dei dati per il quale si stanno valutando i set di dati. A seconda che il criterio sia stato definito da Adobe o dalla tua organizzazione, devi utilizzare `/marketingActions/core` o `/marketingActions/custom`, rispettivamente. |

**Richiesta**

La seguente richiesta verifica il `exportToThirdParty` azione di marketing rispetto ai set di dati ottenuti in [passaggio precedente](#datasets). Il payload della richiesta è un array contenente gli ID di ogni set di dati.

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
| `entityType` | Ogni elemento dell’array di payload deve indicare il tipo di entità da definire. Per questo caso d’uso, il valore sarà sempre &quot;dataSet&quot;. |
| `entityID` | Ogni elemento dell’array di payload deve fornire l’ID univoco di un set di dati. |

**Risposta**

Una risposta corretta restituisce l’URI per l’azione di marketing, le etichette di utilizzo dei dati raccolte dai set di dati specificati e un elenco di tutti i criteri di utilizzo dei dati che sono stati violati in seguito al test dell’azione rispetto a tali etichette. In questo esempio, il criterio &quot;Esporta dati in terze parti&quot; è visualizzato in `violatedPolicies` , che indica che l&#39;azione di marketing ha attivato una violazione dei criteri.

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
| `discoveredLabels` | Elenco dei set di dati forniti nel payload della richiesta, che mostrano le etichette a livello di set di dati e di campi presenti in ciascuno di essi. |
| `violatedPolicies` | Una matrice in cui sono elencati tutti i criteri di utilizzo dei dati che sono stati violati testando l’azione di marketing (specificati in `marketingActionRef`) contro i `duleLabels`. |

Utilizzando i dati restituiti nella risposta API, puoi impostare protocolli all’interno dell’applicazione di esperienza per applicare in modo appropriato le violazioni dei criteri quando si verificano.

## Filtrare i campi dati

Se il segmento di pubblico non supera la valutazione, puoi regolare i dati inclusi nel segmento attraverso uno dei due metodi descritti di seguito.

### Aggiornare il criterio di unione della definizione del segmento

L’aggiornamento del criterio di unione di una definizione di segmento regola i set di dati e i campi che verranno inclusi durante l’esecuzione del processo di segmento. Vedi la sezione su [aggiornamento di un criterio di unione esistente](../../profile/api/merge-policies.md#update) per ulteriori informazioni, consulta l’esercitazione sui criteri di unione delle API .

### Limita campi di dati specifici durante l’esportazione del segmento

Quando si esporta un segmento in un set di dati utilizzando [!DNL Segmentation] API, puoi filtrare i dati inclusi nell’esportazione utilizzando l’ `fields` parametro . Tutti i campi di dati aggiunti a questo parametro verranno inclusi nell’esportazione, mentre tutti gli altri campi di dati verranno esclusi.

Considera un segmento con campi di dati denominati &quot;A&quot;, &quot;B&quot; e &quot;C&quot;. Se si desidera esportare solo il campo &quot;C&quot;, allora il `fields` Il parametro conterrà solo il campo &quot;C&quot;. In questo modo, i campi &quot;A&quot; e &quot;B&quot; verrebbero esclusi durante l’esportazione del segmento.

Vedi la sezione su [esportazione di un segmento](./evaluate-a-segment.md#export) nell’esercitazione sulla segmentazione per ulteriori informazioni.

## Passaggi successivi

Seguendo questa esercitazione, hai cercato le etichette di utilizzo dei dati associate a un segmento di pubblico e le hai testate per verificare la presenza di violazioni dei criteri rispetto a specifiche azioni di marketing. Per ulteriori informazioni sulla governance dei dati in [!DNL Experience Platform], leggere la panoramica di [Governance dei dati](../../data-governance/home.md).
