---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guida per lo sviluppatore di API profilo cliente in tempo reale
topic: guide
translation-type: tm+mt
source-git-commit: d464a6b4abd843f5f8545bc3aa8000f379a86c6d
workflow-type: tm+mt
source-wordcount: '2052'
ht-degree: 1%

---


# Unisci criteri

 Adobe Experience Platform consente di unire dati provenienti da più origini e combinarli per visualizzare una visione completa di ogni singolo cliente. Quando si uniscono questi dati, i criteri di unione sono le regole utilizzate da Platform per determinare in che modo i dati verranno classificati come priorità e quali dati verranno combinati per creare tale visualizzazione unificata. Utilizzando le API RESTful o l&#39;interfaccia utente, puoi creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la tua organizzazione. Questa guida illustra i passaggi per l&#39;utilizzo dei criteri di unione tramite l&#39;API. Per utilizzare i criteri di unione utilizzando l&#39;interfaccia utente, fare riferimento alla guida [utente dei criteri di](../ui/merge-policies.md)unione.

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39;API [Profilo cliente in tempo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)reale. Prima di continuare, consultate la guida [](getting-started.md) introduttiva per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente chiamate a qualsiasi API Experience Platform .

## Componenti dei criteri di unione {#components-of-merge-policies}

I criteri di unione sono privati per l&#39;organizzazione IMS e consentono di creare criteri diversi per unire gli schemi nel modo desiderato. Qualsiasi API che accede ai dati del profilo richiede un criterio di unione, anche se un valore predefinito verrà utilizzato se non viene fornito in modo esplicito. Platform fornisce un criterio di unione predefinito, oppure è possibile creare un criterio di unione per uno schema specifico e contrassegnarlo come predefinito per l&#39;organizzazione. Ogni organizzazione può avere potenzialmente più criteri di unione per schema, tuttavia ogni schema può avere un solo criterio di unione predefinito. I criteri di unione impostati come predefiniti verranno utilizzati nei casi in cui il nome dello schema è fornito e un criterio di unione è obbligatorio ma non fornito. Quando si imposta un criterio di unione come predefinito, tutti i criteri di unione esistenti precedentemente impostati come predefiniti verranno automaticamente aggiornati in modo da non essere più utilizzati come predefiniti.

### Oggetto criteri di unione completo

L&#39;oggetto criteri di unione completo rappresenta un insieme di preferenze che controllano gli aspetti dell&#39;unione dei frammenti di profilo.

**Oggetto Criteri di unione**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "{SCHEMA_NAME}"
        },
        "version": 1,
        "identityGraph": {
            "type": "{IDENTITY_GRAPH_TYPE}"
        },
        "attributeMerge": {
            "type": "{ATTRIBUTE_MERGE_TYPE}"
        },
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| Proprietà | Descrizione |
|---|---|
| `id` | Identificatore univoco generato dal sistema assegnato al momento della creazione |
| `name` | Nome descrittivo per l&#39;identificazione del criterio di unione nelle viste elenco. |
| `imsOrgId` | ID organizzazione a cui appartiene il criterio di unione |
| `identityGraph` | [Oggetto grafico](#identity-graph) dell&#39;identità che indica il grafico dell&#39;identità da cui verranno ottenute le identità correlate. I frammenti di profilo trovati per tutte le identità correlate verranno uniti. |
| `attributeMerge` | [Oggetto unione](#attribute-merge) attributi che indica il modo in cui il criterio di unione darà priorità ai valori degli attributi di profilo in caso di conflitti di dati. |
| `schema` | L&#39;oggetto [schema](#schema) su cui è possibile utilizzare il criterio di unione. |
| `default` | Valore booleano che indica se il criterio di unione è il valore predefinito per lo schema specificato. |
| `version` | Versione dei criteri di unione gestita da Platform. Questo valore di sola lettura viene incrementato ogni volta che viene aggiornato un criterio di unione. |
| `updateEpoch` | Data dell&#39;ultimo aggiornamento del criterio di unione. |

**Esempio di criteri di unione**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "timestampOrdered"
        },
        "default": true,
        "updateEpoch": 1551660639
    }
```

### Grafico identità {#identity-graph}

[Adobe Experience Platform Identity Service](../../identity-service/home.md) gestisce i grafici di identità utilizzati a livello globale e per ciascuna organizzazione  Experience Platform. L&#39; `identityGraph` attributo del criterio di unione definisce come determinare le identità correlate per un utente.

**oggetto identityGraph**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Se `{IDENTITY_GRAPH_TYPE}` è uno dei seguenti casi:

* **&quot;none&quot;:** Non eseguire alcuna cucitura di identità.
* **&quot;pdg&quot;:** Esegue l&#39;unione delle identità in base al grafico dell&#39;identità privata.

**Esempio`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Unione attributi {#attribute-merge}

Un frammento di profilo è l&#39;informazione di profilo per una sola identità inclusa nell&#39;elenco di identità esistenti per un particolare utente. Quando il tipo di grafico dell&#39;identità utilizzato genera più identità, è possibile che vi siano valori in conflitto per le proprietà del profilo e occorre specificare la priorità. Utilizzando `attributeMerge`, è possibile specificare quali valori del profilo di set di dati dare la priorità in caso di conflitto di unione.

**oggetto attributeMerge**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Se `{ATTRIBUTE_MERGE_TYPE}` è uno dei seguenti casi:

* **&quot;timestampOrdered&quot;**: (impostazione predefinita) Assegna priorità al profilo aggiornato per ultimo in caso di conflitto. Utilizzando questo tipo di unione, l&#39; `data` attributo non è obbligatorio.
* **&quot;dataSetPrecedence&quot;** : Attribuire priorità ai frammenti di profilo in base al set di dati da cui provengono. Questo può essere utilizzato quando le informazioni presenti in un set di dati sono preferite o attendibili rispetto ai dati contenuti in un altro set di dati. Quando si utilizza questo tipo di unione, l&#39; `order` attributo è obbligatorio, in quanto elenca i set di dati in ordine di priorità.
   * **&quot;order&quot;**: Quando si utilizza &quot;dataSetPrecedence&quot;, è necessario fornire un `order` array con un elenco di set di dati. Eventuali set di dati non inclusi nell&#39;elenco non verranno uniti. In altre parole, i set di dati devono essere esplicitamente elencati per essere uniti in un profilo. L&#39; `order` array elenca gli ID dei set di dati in ordine di priorità.

**Esempio di oggetto attributeMerge che utilizza il tipo dataSetPrecedence**

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order" : [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

**Esempio di oggetto attributeMerge con tipo timestampOrdered**

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Schema {#schema}

L&#39;oggetto schema specifica lo schema XDM per il quale viene creato il criterio di unione.

**`schema`object **

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

Se il valore di `name` è il nome della classe XDM su cui si basa lo schema associato al criterio di unione.

**Esempio`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

## Accedere ai criteri di unione {#access-merge-policies}

Utilizzando l&#39;API Profilo cliente in tempo reale, l&#39; `/config/mergePolicies` endpoint consente di eseguire una richiesta di ricerca per visualizzare un criterio di unione specifico in base al relativo ID, oppure di accedere a tutti i criteri di unione nell&#39;organizzazione IMS, filtrati in base a criteri specifici. Potete inoltre utilizzare l&#39; `/config/mergePolicies/bulk-get` endpoint per recuperare più criteri di unione in base ai relativi ID. I passaggi per eseguire ciascuna di queste chiamate sono descritti nelle sezioni seguenti.

### Accesso a un singolo criterio di unione tramite ID

Potete accedere a un singolo criterio di unione utilizzando il relativo ID effettuando una richiesta GET all&#39; `/config/mergePolicies` endpoint e includendo l&#39; `mergePolicyId` elemento nel percorso della richiesta.

**Formato API**

```http
GET /config/mergePolicies/{mergePolicyId}
```

| Parametro | Descrizione |
|---|---|
| `{mergePolicyId}` | Identificatore del criterio di unione che si desidera eliminare. |

**Richiesta**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/10648288-cda5-11e8-a8d5-f2801f1b9fd1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Risposta**

Una risposta corretta restituisce i dettagli del criterio di unione.

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{IMS_ORG}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "pdg"
    },
    "attributeMerge": {
        "type": "timestampOrdered"
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

Per informazioni dettagliate su ciascuno dei singoli elementi che compongono un criterio di unione, vedere la sezione [Componenti di criteri](#components-of-merge-policies) di unione all&#39;inizio del documento.

### Recuperare più criteri di unione in base ai relativi ID

È possibile recuperare più criteri di unione eseguendo una richiesta POST all&#39; `/config/mergePolicies/bulk-get` endpoint e includendo gli ID dei criteri di unione che si desidera recuperare nel corpo della richiesta.

**Formato API**

```http
POST /config/mergePolicies/bulk-get
```

**Richiesta**

Il corpo della richiesta include un array &quot;ids&quot; con singoli oggetti contenenti &quot;id&quot; per ciascun criterio di unione per il quale si desidera recuperare i dettagli.

```shell
curl -X POST \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/bulk-get' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "ids": [
          {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b"
          },
          {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130"
          }
        ]
      }'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 207 (Stato multiplo) e i dettagli dei criteri di unione i cui ID sono stati forniti nella richiesta POST.

```json
{ 
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "none"
            },
            "attributeMerge": {
                "type": "timestampOrdered"
            },
            "default": true,
            "updateEpoch": 1552086578
        },
        "42d4a596-b1c6-46c0-994e-ca5ef1f85130": {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "pdg"
            },
            "attributeMerge": {
                "type": "dataSetPrecedence",
                "order": [
                    "5b76f86b85d0e00000be5c8b",
                    "5b76f8d787a6af01e2ceda18"
                ]
            },
            "default": false,
            "updateEpoch": 1576099719
        }
    }
}
```

Per informazioni dettagliate su ciascuno dei singoli elementi che compongono un criterio di unione, vedere la sezione [Componenti di criteri](#components-of-merge-policies) di unione all&#39;inizio del documento.

### Elenca più criteri di unione

È possibile elencare più criteri di unione all&#39;interno dell&#39;organizzazione IMS inviando una richiesta GET all&#39; `/config/mergePolicies` endpoint e utilizzando parametri di query facoltativi per filtrare, ordinare e impaginare la risposta. È possibile includere più parametri, separati da e commerciale (&amp;). Effettuando una chiamata a questo endpoint senza parametri, tutti i criteri di unione disponibili per l&#39;organizzazione verranno recuperati.

**Formato API**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Parametro | Descrizione |
|---|---|
| `default` | Valore booleano che filtra i risultati in base al fatto che i criteri di unione siano o meno i valori predefiniti per una classe di schema. |
| `limit` | Specifica il limite delle dimensioni di pagina per controllare il numero di risultati inclusi in una pagina. Valore predefinito: 20 |
| `orderBy` | Specifica il campo in base al quale ordinare i risultati come in `orderBy=name` o `orderBy=+name` ordinare per nome in ordine crescente o `orderBy=-name`, per l&#39;ordinamento decrescente. Omettendo questo valore si ottiene l&#39;ordinamento predefinito di `name` crescente. |
| `schema.name` | Nome dello schema per il quale recuperare i criteri di unione disponibili. |
| `identityGraph.type` | Filtra i risultati in base al tipo di grafico dell&#39;identità. I valori possibili includono &quot;none&quot; e &quot;pdg&quot; (grafico privato). |
| `attributeMerge.type` | Filtra i risultati in base al tipo di unione degli attributi utilizzato. I valori possibili includono &quot;timestampOrdered&quot; e &quot;dataSetPrecedence&quot;. |
| `start` | Offset pagina - specifica l&#39;ID iniziale per i dati da recuperare. Valore predefinito: 0 |
| `version` | Specificate questo valore se desiderate utilizzare una versione specifica del criterio di unione. Per impostazione predefinita, verrà utilizzata la versione più recente. |

Per ulteriori informazioni sui `schema.name`componenti `identityGraph.type`e `attributeMerge.type`, consultare la sezione relativa ai [componenti dei criteri](#components-of-merge-policies) di unione fornita in precedenza in questa guida.


**Richiesta**

Nella richiesta seguente sono elencati tutti i criteri di unione per uno schema specifico:

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Risposta**

Una risposta corretta restituisce un elenco impaginato di criteri di unione che soddisfano i criteri specificati dai parametri di query inviati nella richiesta.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "none"
            },
            "attributeMerge": {
                "type": "timestampOrdered"
            },
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "pdg"
            },
            "attributeMerge": {
                "type": "dataSetPrecedence",
                "order": [
                    "5b76f86b85d0e00000be5c8b",
                    "5b76f8d787a6af01e2ceda18"
                ]
            },
            "default": false,
            "updateEpoch": 1576099719
        }
    ],
    "_links": {
        "next": {
            "href": "@/mergePolicies?start=K1JJRDpFaWc5QUpZWHY1c2JBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQldBQkVBQVBnaFFQLzM4VUIvL2tKQi8rLysvMUpBLzMrMi8wRkFmLzR4UUwvL0VrRC85em4zRTBEcmNmYi92Kzh4UUwvL05rQVgzRi8rMStqNS80WHQwN2NhUUVzQUFBUUFleGpLQ1JnVXRVcEFCQUFFQVBBRA==&orderBy=&limit=2"
        }
    }
}
```

| Proprietà | Descrizione |
|---|---|
| `_links.next.href` | Indirizzo URI per la pagina successiva di risultati. Utilizzate questo URI come parametro di richiesta per un’altra chiamata API allo stesso endpoint per visualizzare la pagina. Se non esiste una pagina successiva, questo valore sarà una stringa vuota. |

## Creare un criterio di unione

Potete creare un nuovo criterio di unione per la vostra organizzazione effettuando una richiesta POST all&#39; `/config/mergePolicies` endpoint.

**Formato API**

```http
POST /config/mergePolicies
```

**Richiesta** La richiesta seguente crea un nuovo criterio di unione, configurato dai valori attributo forniti nel payload:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph" : {
        "type": "none"
    },
    "attributeMerge" : {
        "type":"dataSetPrecedence",
        "order" : [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "default": true
}'
```

| Proprietà | Descrizione |
|---|---|
| `name` | Un nome descrittivo mediante il quale è possibile identificare il criterio di unione nelle viste elenco. |
| `identityGraph.type` | Il tipo di grafico dell&#39;identità da cui ottenere le identità correlate da unire. Valori possibili: &quot;none&quot; o &quot;pdg&quot; (grafico privato). |
| `attributeMerge` | Modalità con cui assegnare la priorità ai valori degli attributi di profilo in caso di conflitti di dati. |
| `schema` | La classe dello schema XDM associata al criterio di unione. |
| `default` | Specifica se il criterio di unione è il valore predefinito per lo schema. |

Per ulteriori informazioni, fare riferimento alla sezione [Componenti dei criteri](#components-of-merge-policies) di unione.

**Risposta**

Una risposta corretta restituisce i dettagli del criterio di unione appena creato.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

Per informazioni dettagliate su ciascuno dei singoli elementi che compongono un criterio di unione, vedere la sezione [Componenti di criteri](#components-of-merge-policies) di unione all&#39;inizio del documento.

## Aggiornare un criterio di unione {#update}

È possibile modificare un criterio di unione esistente modificando singoli attributi (PATCH) o sovrascrivendo l&#39;intero criterio di unione con nuovi attributi (PUT). Di seguito sono riportati alcuni esempi.

### Modificare singoli campi dei criteri di unione

È possibile modificare singoli campi per un criterio di unione eseguendo una richiesta PATCH all&#39; `/config/mergePolicies/{mergePolicyId}` endpoint:

**Formato API**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Parametro | Descrizione |
|---|---|
| `{mergePolicyId}` | Identificatore del criterio di unione che si desidera eliminare. |

**Richiesta**

La richiesta seguente aggiorna uno specifico criterio di unione modificando il valore della `default` proprietà in `true`:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "op": "add",
    "path": "/default",
    "value": "true"
  }'
```

| Proprietà | Descrizione |
|---|---|
| `op` | Specifica l&#39;operazione da eseguire. Esempi di altre operazioni PATCH sono disponibili nella documentazione relativa alla patch [JSON](http://jsonpatch.com) |
| `path` | Percorso del campo da aggiornare. I valori accettati sono: &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot; |
| `value` | Il valore su cui impostare il campo specificato. |

Per ulteriori informazioni, fare riferimento alla sezione [Componenti dei criteri](#components-of-merge-policies) di unione.


**Risposta**

Una risposta corretta restituisce i dettagli del criterio di unione aggiornato di recente.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

### Sovrascrivi criterio di unione

Un altro modo per modificare un criterio di unione consiste nell&#39;utilizzare una richiesta PUT, che sovrascrive l&#39;intero criterio di unione.

**Formato API**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| Parametro | Descrizione |
|---|---|
| `{mergePolicyId}` | Identificatore del criterio di unione che si desidera sovrascrivere. |

**Richiesta**

La richiesta seguente sovrascrive il criterio di unione specificato, sostituendo i relativi valori attributo con quelli forniti nel payload. Poiché questa richiesta sostituisce completamente un criterio di unione esistente, è necessario fornire tutti gli stessi campi che erano necessari per la definizione originale del criterio di unione. Tuttavia, questa volta vengono forniti valori aggiornati per i campi che si desidera modificare.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "dataSetPrecedence",
            "order": [
                "5b76f86b85d0e00000be5c8b",
                "5b76f8d787a6af01e2ceda18"
            ]
        },
        "default": true,
        "updateEpoch": 1551898378
    }'
```

| Proprietà | Descrizione |
|---|---|
| `name` | Un nome descrittivo mediante il quale è possibile identificare il criterio di unione nelle viste elenco. |
| `identityGraph` | Grafico identità da cui ottenere le identità correlate da unire. |
| `attributeMerge` | Modalità con cui assegnare la priorità ai valori degli attributi di profilo in caso di conflitti di dati. |
| `schema` | La classe dello schema XDM associata al criterio di unione. |
| `default` | Specifica se il criterio di unione è il valore predefinito per lo schema. |

Per ulteriori informazioni, fare riferimento alla sezione [Componenti dei criteri](#components-of-merge-policies) di unione.


**Risposta**

Una risposta corretta restituisce i dettagli del criterio di unione aggiornato.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

## Eliminare un criterio di unione

È possibile eliminare un criterio di unione eseguendo una richiesta di DELETE all&#39; `/config/mergePolicies` endpoint e includendo l&#39;ID del criterio di unione che si desidera eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| Parametro | Descrizione |
|---|---|
| `{mergePolicyId}` | Identificatore del criterio di unione che si desidera eliminare. |

**Richiesta**

La richiesta seguente elimina un criterio di unione.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una richiesta di eliminazione riuscita restituisce lo stato HTTP 200 (OK) e un corpo di risposta vuoto. Per confermare che l&#39;eliminazione è avvenuta correttamente, potete eseguire una richiesta GET per visualizzare il criterio di unione in base al relativo ID. Se il criterio di unione è stato eliminato, si riceverà un errore HTTP Status 404 (Non trovato).

## Passaggi successivi

Ora che sai come creare e configurare criteri di unione per la tua organizzazione IMS, puoi utilizzarli per creare segmenti di pubblico dai dati del profilo cliente in tempo reale. Per iniziare a definire e utilizzare i segmenti, consulta la documentazione [del servizio di segmentazione del Adobe Experience Platform](../../segmentation/home.md) .



