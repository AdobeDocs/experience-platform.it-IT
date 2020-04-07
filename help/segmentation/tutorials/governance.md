---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Applica la conformità all'utilizzo dei dati per i segmenti di pubblico
topic: tutorial
translation-type: tm+mt
source-git-commit: f5bc9beb59e83b0411d98d901d5055122a124d07

---


# Applicazione della conformità dell&#39;utilizzo dei dati per un segmento di pubblico tramite API

Questa esercitazione descrive i passaggi per imporre la conformità dell&#39;utilizzo dei dati per i segmenti di pubblico Profilo cliente in tempo reale che utilizzano le API.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Profilo](../../profile/home.md)cliente in tempo reale: Profilo cliente in tempo reale è un archivio di entità di ricerca generico e viene utilizzato per gestire i dati Experience Data Model (XDM) all&#39;interno della piattaforma. Il profilo unisce i dati tra diverse risorse di dati aziendali e fornisce l&#39;accesso a tali dati in una presentazione unificata.
   - [Unisci criteri](../../profile/api/merge-policies.md): Regole utilizzate dal profilo cliente in tempo reale per determinare quali dati possono essere uniti in una visualizzazione unificata a determinate condizioni. I criteri di unione possono essere configurati a scopo di governance dei dati.
- [Segmentazione](../home.md): In che modo il profilo cliente in tempo reale divide un ampio gruppo di individui contenuti nello store del profilo in gruppi più piccoli che condividono caratteristiche simili e risponderanno in modo simile alle strategie di marketing.
- [Governance](../../data-governance/home.md)dei dati: La governance dei dati fornisce l&#39;infrastruttura per l&#39;etichettatura e l&#39;applicazione dell&#39;uso dei dati (DULE), utilizzando i seguenti componenti:
   - [Etichette](../../data-governance/labels/user-guide.md)di utilizzo dati: Etichette utilizzate per descrivere insiemi di dati e campi in termini di livello di sensibilità con cui gestire i rispettivi dati.
   - [Criteri](../../data-governance/api/getting-started.md)di utilizzo dei dati: Configurazioni che indicano quali azioni di marketing sono consentite sui dati classificati da particolari etichette di utilizzo dei dati.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente chiamate alle API della piattaforma.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi della piattaforma Experience.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API della piattaforma, dovete prima completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API della piattaforma richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Per ulteriori informazioni sulle sandbox in Piattaforma, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

## Ricerca di un criterio di unione per la definizione di un segmento

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

## Trovare i set di dati di origine dal criterio di unione

I criteri di unione contengono informazioni sui set di dati di origine, che a loro volta contengono etichette DULE. Potete consultare i dettagli di un criterio di unione fornendo l&#39;ID del criterio di unione in una richiesta GET all&#39;API del profilo.

**Formato API**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | ID del criterio di unione ottenuto nel passaggio [](#lookup-a-merge-policy-for-a-segment-definition)precedente. |

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

## Ricerca delle etichette di utilizzo dei dati per i set di dati di origine

Dopo aver raccolto gli ID dei set di dati di origine del criterio di unione, puoi utilizzare questi ID per cercare le etichette di utilizzo dei dati configurate per i set di dati stessi ed eventuali campi di dati specifici in essi contenuti.

La seguente chiamata all’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) Catalog Service recupera le etichette di utilizzo dei dati associate a un singolo dataset fornendo il relativo ID nel percorso della richiesta:

**Formato API**

```http
GET /dataSets/{DATASET_ID}/dule
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{DATASET_ID}` | ID del set di dati di cui si desidera cercare le etichette di utilizzo dei dati. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b95b155419ec801e6eee780/dule \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di etichette di utilizzo dei dati associate al set di dati nel suo insieme ed eventuali specifici campi di dati associati allo schema di origine.

```json
{
    "connection": {},
    "dataset": {
        "identity": [],
        "contract": [
            "C3"
        ],
        "sensitive": [],
        "contracts": [
            "C3"
        ],
        "identifiability": [],
        "specialTypes": []
    },
    "fields": [],
    "schemaFields": [
        {
            "path": "/properties/personalEmail/properties/address",
            "identity": [
                "I1"
            ],
            "contract": [
                "C2",
                "C9"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C9"
            ],
            "identifiability": [
                "I1"
            ],
            "specialTypes": []
        }
    ]
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `dataset` | Un oggetto che contiene le etichette di utilizzo dei dati applicate all&#39;insieme di dati. |
| `schemaFields` | Un array di oggetti che rappresenta specifici campi dello schema a cui sono applicate etichette di utilizzo dei dati. |
| `schemaFields.path` | Percorso del campo dello schema le cui etichette di utilizzo dei dati sono elencate nello stesso oggetto. |

## Filtrare i campi dati

>[!NOTE] Questo passaggio è facoltativo. Se non desideri regolare i dati inclusi nel tuo segmento in base ai risultati ottenuti nel passaggio precedente, ovvero [cercare etichette](#lookup-data-usage-labels-for-the-source-datasets)di utilizzo dei dati, puoi passare al passaggio finale di [valutazione dei dati per le violazioni](#evaluate-data-for-policy-violations)dei criteri.

Se desiderate regolare i dati inclusi nel segmento di pubblico, potete farlo utilizzando uno dei due metodi seguenti:

### Aggiorna il criterio di unione della definizione del segmento

Quando si aggiorna il criterio di unione di una definizione di segmento, vengono regolati i set di dati e i campi che verranno inclusi durante l&#39;esecuzione del processo di segmento. Per ulteriori informazioni, consulta la sezione sull&#39; [aggiornamento di un criterio](../../profile/api/merge-policies.md) di unione esistente nell&#39;esercitazione sulla politica di unione.

### Limita campi dati specifici durante l&#39;esportazione del segmento

Quando si esporta un segmento in un dataset utilizzando l&#39;API Profilo cliente in tempo reale, è possibile filtrare i dati inclusi nell&#39;esportazione utilizzando il `fields` parametro. Tutti i campi di dati aggiunti a questo parametro verranno inclusi nell&#39;esportazione, mentre tutti gli altri campi di dati saranno esclusi.

Considerate un segmento con campi di dati denominati &quot;A&quot;, &quot;B&quot; e &quot;C&quot;. Se si desidera esportare solo il campo &quot;C&quot;, il `fields` parametro conterrà solo il campo &quot;C&quot;. In questo modo, i campi &quot;A&quot; e &quot;B&quot; sarebbero esclusi durante l’esportazione del segmento.

Per ulteriori informazioni, consulta la sezione sull’ [esportazione di un segmento](./evaluate-a-segment.md#export-a-segment) nell’esercitazione sulla segmentazione.

## Valutazione dei dati per le violazioni dei criteri

Dopo aver raccolto le etichette di utilizzo dei dati associate al segmento di pubblico, puoi sottoporre a test queste etichette in base alle azioni di marketing per valutare eventuali violazioni dei criteri di utilizzo dei dati. Per i passaggi dettagliati su come eseguire le valutazioni dei criteri utilizzando l&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)DULE Policy Service, vedete il documento sulla valutazione [dei](../../data-governance/enforcement/overview.md)criteri.

## Passaggi successivi

Seguendo questa esercitazione, hai cercato le etichette di utilizzo dei dati associate a un segmento di pubblico e li hai testati per verificare la presenza di violazioni dei criteri rispetto a determinate azioni di marketing. Per ulteriori informazioni sulla governance dei dati in Experience Platform, consulta la panoramica sulla governance dei [dati](../../data-governance/home.md).