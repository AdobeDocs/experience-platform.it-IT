---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API per criteri di unione
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform consente di unire frammenti di dati provenienti da più sorgenti e di combinarli per ottenere una visualizzazione completa di ciascuno dei singoli clienti. Quando si riuniscono questi dati, i criteri di unione sono le regole utilizzate da Platform per determinare in che modo i dati verranno definiti come prioritari e quali dati verranno combinati per creare una visualizzazione unificata.
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
source-git-commit: 6864e4518b17dc843b3e74c0f9b03ab756d9c581
workflow-type: tm+mt
source-wordcount: '2590'
ht-degree: 1%

---

# Endpoint Criteri di unione

Adobe Experience Platform consente di unire frammenti di dati provenienti da più sorgenti e di combinarli per ottenere una visualizzazione completa di ciascuno dei singoli clienti. Quando si riuniscono questi dati, i criteri di unione sono le regole utilizzate da [!DNL Platform] per determinare in che modo i dati verranno definiti come prioritari e quali dati verranno combinati per creare una visualizzazione unificata.

Ad esempio, se un cliente interagisce con il tuo marchio su più canali, la tua organizzazione avrà più frammenti di profilo relativi al singolo cliente che compaiono in più set di dati. Quando questi frammenti vengono acquisiti in Platform, vengono uniti per creare un singolo profilo per quel cliente. Quando i dati provenienti da più origini sono in conflitto (ad esempio, un frammento elenca il cliente come &quot;singolo&quot;, mentre l’altro elenca il cliente come &quot;sposato&quot;), il criterio di unione determina quali informazioni includere nel profilo dell’utente.

Utilizzando le API RESTful o l&#39;interfaccia utente, è possibile creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la propria organizzazione. Questa guida descrive i passaggi necessari per l’utilizzo delle API per l’unione dei criteri.

Per utilizzare i criteri di unione utilizzando l&#39;interfaccia utente, fare riferimento alla [guida all&#39;interfaccia utente dei criteri di unione](../merge-policies/ui-guide.md). Per ulteriori informazioni sui criteri di unione in generale e sul loro ruolo all&#39;interno dell&#39;Experience Platform, leggere la [panoramica dei criteri di unione](../merge-policies/overview.md).

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte del [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Prima di continuare, controlla la [guida introduttiva](getting-started.md) per i collegamenti alla relativa documentazione, una guida per la lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API [!DNL Experience Platform].

## Componenti dei criteri di unione {#components-of-merge-policies}

I criteri di unione sono privati dell’organizzazione IMS e consentono di creare diversi criteri per unire gli schemi nei modi specifici necessari. Qualsiasi API che accede ai dati [!DNL Profile] richiede un criterio di unione, anche se un valore predefinito verrà utilizzato se non viene fornito esplicitamente. [!DNL Platform] fornisce alle organizzazioni un criterio di unione predefinito oppure è possibile creare un criterio di unione per una classe di schema XDM (Experience Data Model) specifica e contrassegnarlo come predefinito per la propria organizzazione.

Sebbene ogni organizzazione possa avere potenzialmente più criteri di unione per classe di schema, ogni classe può avere un solo criterio di unione predefinito. I criteri di unione impostati come predefiniti verranno utilizzati nei casi in cui viene fornito il nome della classe dello schema e viene richiesto un criterio di unione, ma non viene fornito.

>[!NOTE]
>
>Quando si imposta come impostazione predefinita un nuovo criterio di unione, tutti i criteri di unione esistenti precedentemente impostati come predefiniti verranno automaticamente aggiornati in modo da non essere più utilizzati come impostazione predefinita.

### Oggetto criterio di unione completo

L&#39;oggetto criteri di unione completo rappresenta un insieme di preferenze che controllano gli aspetti dell&#39;unione dei frammenti di profilo.

**Oggetto Criteri di unione**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "{SCHEMA_CLASS_NAME}"
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
| `name` | Nome descrittivo in base al quale i criteri di unione possono essere identificati nelle viste elenco. |
| `imsOrgId` | ID organizzazione a cui appartiene il criterio di unione |
| `identityGraph` | [Oggetto ](#identity-graph) grafico di identità che indica il grafico di identità da cui verranno ottenute le identità correlate. I frammenti di profilo trovati per tutte le identità correlate verranno uniti. |
| `attributeMerge` | [Oggetto ](#attribute-merge) unione attributi che indica il modo in cui il criterio di unione darà priorità agli attributi del profilo in caso di conflitti di dati. |
| `schema.name` | Parte dell&#39;oggetto [`schema`](#schema) , il campo `name` contiene la classe dello schema XDM a cui si riferisce il criterio di unione. Per ulteriori informazioni sugli schemi e le classi, leggere la [documentazione XDM](../../xdm/home.md). |
| `default` | Valore booleano che indica se il criterio di unione è il valore predefinito per lo schema specificato. |
| `version` | [!DNL Platform] versione aggiornata dei criteri di unione. Questo valore di sola lettura viene incrementato ogni volta che un criterio di unione viene aggiornato. |
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

### Grafico di identità {#identity-graph}

[Adobe Experience Platform Identity ](../../identity-service/home.md) Service gestisce i grafici di identità utilizzati a livello globale e per ogni organizzazione in  [!DNL Experience Platform]. L&#39;attributo `identityGraph` del criterio di unione definisce come determinare le identità correlate per un utente.

**oggetto identityGraph**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Dove `{IDENTITY_GRAPH_TYPE}` è uno dei seguenti:

* **&quot;none&quot;:** non eseguire alcuna unione di identità.
* **&quot;pdg&quot;:** esegui la combinazione di identità in base al grafico di identità privata.

**Esempio`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Unione attributi {#attribute-merge}

Un frammento di profilo è l’informazione di profilo per una sola identità inclusa nell’elenco di identità esistenti per un particolare utente. Quando il tipo di grafico di identità utilizzato genera più di un&#39;identità, è possibile che vi siano attributi di profilo in conflitto e deve essere specificata la priorità. Utilizzando `attributeMerge`, puoi specificare quali attributi di profilo dare la priorità in caso di un conflitto di unione tra i set di dati di tipo Valore chiave (dati record).

**oggetto attributeMerge**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Dove `{ATTRIBUTE_MERGE_TYPE}` è uno dei seguenti:

* **`timestampOrdered`**: (Impostazione predefinita) Assegna priorità al profilo aggiornato per ultimo. Utilizzando questo tipo di unione, l&#39;attributo `data` non è obbligatorio. `timestampOrdered` supporta anche le marche temporali personalizzate che avranno la precedenza quando si uniscono frammenti di profilo all’interno o tra set di dati. Per ulteriori informazioni, consulta la sezione Appendice su [uso di marche temporali personalizzate](#custom-timestamps).
* **`dataSetPrecedence`** : Assegna priorità ai frammenti di profilo in base al set di dati da cui provengono. Questo può essere utilizzato quando le informazioni presenti in un set di dati sono preferite o attendibili rispetto ai dati di un altro set di dati. Quando si utilizza questo tipo di unione, l’attributo `order` è obbligatorio in quanto elenca i set di dati in ordine di priorità.
   * **`order`**: Quando si utilizza &quot;dataSetPrecedence&quot;, è necessario fornire un  `order` array con un elenco di set di dati. Eventuali set di dati non inclusi nell’elenco non verranno uniti. In altre parole, i set di dati devono essere elencati in modo esplicito per essere uniti in un profilo. La matrice `order` elenca gli ID dei set di dati in ordine di priorità.

#### Esempio di oggetto `attributeMerge` che utilizza il tipo `dataSetPrecedence`

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

#### Esempio di oggetto `attributeMerge` che utilizza il tipo `timestampOrdered`

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Schema {#schema}

L&#39;oggetto schema specifica la classe di schema Experience Data Model (XDM) per la quale viene creato il criterio di unione.

**`schema`oggetto**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

Dove il valore di `name` è il nome della classe XDM su cui si basa lo schema associato al criterio di unione.

**Esempio`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

Per ulteriori informazioni su XDM e sull&#39;utilizzo degli schemi in Experience Platform, inizia leggendo la [Panoramica del sistema XDM](../../xdm/home.md).

## Accedere ai criteri di unione {#access-merge-policies}

Utilizzando l’API [!DNL Real-time Customer Profile], l’endpoint `/config/mergePolicies` consente di eseguire una richiesta di ricerca per visualizzare un criterio di unione specifico per il relativo ID o per accedere a tutti i criteri di unione nell’organizzazione IMS, filtrati in base a criteri specifici. È inoltre possibile utilizzare l&#39;endpoint `/config/mergePolicies/bulk-get` per recuperare più criteri di unione in base ai relativi ID. I passaggi per eseguire ciascuna di queste chiamate sono descritti nelle sezioni seguenti.

### Accedere a un criterio di unione singolo per ID

Puoi accedere a un singolo criterio di unione dal relativo ID effettuando una richiesta di GET all’ endpoint `/config/mergePolicies` e includendo `mergePolicyId` nel percorso della richiesta.

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

Per informazioni dettagliate su ciascuno dei singoli elementi che compongono un criterio di unione, vedere la sezione [componenti dei criteri di unione](#components-of-merge-policies) all&#39;inizio del documento.

### Recupera più criteri di unione in base ai relativi ID

È possibile recuperare più criteri di unione effettuando una richiesta POST all&#39;endpoint `/config/mergePolicies/bulk-get` e includendo gli ID dei criteri di unione che si desidera recuperare nel corpo della richiesta.

**Formato API**

```http
POST /config/mergePolicies/bulk-get
```

**Richiesta**

Il corpo della richiesta include una matrice &quot;id&quot; con singoli oggetti contenenti l&#39;&quot;id&quot; per ogni criterio di unione per il quale si desidera recuperare i dettagli.

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

Una risposta corretta restituisce lo stato HTTP 207 (stato multiplo) e i dettagli dei criteri di unione i cui ID sono stati forniti nella richiesta di POST.

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

Per informazioni dettagliate su ciascuno dei singoli elementi che compongono un criterio di unione, vedere la sezione [componenti dei criteri di unione](#components-of-merge-policies) all&#39;inizio del documento.

### Elencare più criteri di unione in base ai criteri

È possibile elencare più criteri di unione all’interno dell’organizzazione IMS inviando una richiesta di GET all’endpoint `/config/mergePolicies` e utilizzando parametri di query facoltativi per filtrare, ordinare e impaginare la risposta. È possibile includere più parametri, separati da e commerciale (&amp;). Effettuare una chiamata a questo endpoint senza parametri recupererà tutti i criteri di unione disponibili per la tua organizzazione.

**Formato API**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Parametro | Descrizione |
|---|---|
| `default` | Valore booleano che filtra i risultati in base al fatto che i criteri di unione siano o meno i valori predefiniti per una classe di schema. |
| `limit` | Specifica il limite di dimensioni della pagina per controllare il numero di risultati inclusi in una pagina. Valore predefinito: 20 |
| `orderBy` | Specifica il campo in base al quale ordinare i risultati come in `orderBy=name` o `orderBy=+name` per ordinarli in ordine crescente o `orderBy=-name` in ordine decrescente. Omettendo questo valore si ottiene l’ordinamento predefinito di `name` in ordine crescente. |
| `schema.name` | Nome dello schema per il quale recuperare i criteri di unione disponibili. |
| `identityGraph.type` | Filtra i risultati in base al tipo di grafico delle identità. I valori possibili includono &quot;none&quot; e &quot;pdg&quot; (grafico privato). |
| `attributeMerge.type` | Filtra i risultati in base al tipo di unione degli attributi utilizzato. I valori possibili includono &quot;timestampOrdered&quot; e &quot;dataSetPrecedence&quot;. |
| `start` | Offset pagina - specifica l’ID iniziale per i dati da recuperare. Valore predefinito: 0 |
| `version` | Specificare questa opzione se si desidera utilizzare una versione specifica del criterio di unione. Per impostazione predefinita, verrà utilizzata la versione più recente. |

Per ulteriori informazioni su `schema.name`, `identityGraph.type` e `attributeMerge.type`, consulta la sezione [componenti dei criteri di unione](#components-of-merge-policies) fornita in precedenza in questa guida.


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
| `_links.next.href` | Indirizzo URI per la pagina successiva di risultati. Utilizza questo URI come parametro di richiesta per un’altra chiamata API allo stesso endpoint per visualizzare la pagina. Se non esiste una pagina successiva, questo valore sarà una stringa vuota. |

## Creare un criterio di unione

È possibile creare un nuovo criterio di unione per la propria organizzazione effettuando una richiesta di POST all&#39;endpoint `/config/mergePolicies`.

**Formato API**

```http
POST /config/mergePolicies
```

****
RequestLa richiesta seguente crea un nuovo criterio di unione, configurato dai valori degli attributi forniti nel payload:

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
| `name` | Un nome descrittivo in base al quale è possibile identificare il criterio di unione nelle viste a elenco. |
| `identityGraph.type` | Il tipo di grafico delle identità da cui ottenere le identità correlate da unire. Valori possibili: &quot;none&quot; o &quot;pdg&quot; (grafico privato). |
| `attributeMerge` | Modalità con cui assegnare la priorità ai valori degli attributi del profilo in caso di conflitti di dati. |
| `schema` | Classe dello schema XDM associata al criterio di unione. |
| `default` | Specifica se il criterio di unione è il valore predefinito per lo schema. |

Per ulteriori informazioni, consulta la sezione [componenti dei criteri di unione](#components-of-merge-policies) .

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

Per informazioni dettagliate su ciascuno dei singoli elementi che compongono un criterio di unione, vedere la sezione [componenti dei criteri di unione](#components-of-merge-policies) all&#39;inizio del documento.

## Aggiornare un criterio di unione {#update}

È possibile modificare un criterio di unione esistente modificando singoli attributi (PATCH) o sovrascrivendo l&#39;intero criterio di unione con nuovi attributi (PUT). Di seguito sono riportati alcuni esempi di ciascuno di essi.

### Modifica di singoli campi dei criteri di unione

È possibile modificare singoli campi per un criterio di unione effettuando una richiesta di PATCH all&#39;endpoint `/config/mergePolicies/{mergePolicyId}`:

**Formato API**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Parametro | Descrizione |
|---|---|
| `{mergePolicyId}` | Identificatore del criterio di unione che si desidera eliminare. |

**Richiesta**

La richiesta seguente aggiorna un criterio di unione specificato modificando il valore della relativa proprietà `default` in `true`:

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
| `op` | Specifica l&#39;operazione da eseguire. Esempi di altre operazioni PATCH sono disponibili nella documentazione [JSON Patch](http://jsonpatch.com) |
| `path` | Percorso del campo da aggiornare. I valori accettati sono: &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot; |
| `value` | Valore su cui impostare il campo specificato. |

Per ulteriori informazioni, consulta la sezione [componenti dei criteri di unione](#components-of-merge-policies) .


**Risposta**

Una risposta corretta restituisce i dettagli del criterio di unione appena aggiornato.

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

La richiesta seguente sovrascrive il criterio di unione specificato, sostituendo i relativi valori attributo con quelli forniti nel payload. Poiché questa richiesta sostituisce completamente un criterio di unione esistente, è necessario fornire tutti gli stessi campi richiesti durante la definizione originale del criterio di unione. Tuttavia, questa volta vengono forniti valori aggiornati per i campi che si desidera modificare.

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
| `name` | Un nome descrittivo in base al quale è possibile identificare il criterio di unione nelle viste a elenco. |
| `identityGraph` | Il grafico delle identità da cui ottenere le identità correlate da unire. |
| `attributeMerge` | Modalità con cui assegnare la priorità ai valori degli attributi del profilo in caso di conflitti di dati. |
| `schema` | Classe dello schema XDM associata al criterio di unione. |
| `default` | Specifica se il criterio di unione è il valore predefinito per lo schema. |

Per ulteriori informazioni, consulta la sezione [componenti dei criteri di unione](#components-of-merge-policies) .


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

È possibile eliminare un criterio di unione effettuando una richiesta DELETE all&#39;endpoint `/config/mergePolicies` e includendo l&#39;ID del criterio di unione che si desidera eliminare nel percorso della richiesta.

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

Una richiesta di eliminazione corretta restituisce lo stato HTTP 200 (OK) e un corpo di risposta vuoto. Per confermare che l&#39;eliminazione è avvenuta correttamente, è possibile eseguire una richiesta GET per visualizzare il criterio di unione in base al relativo ID. Se il criterio di unione è stato eliminato, verrà visualizzato un errore di stato HTTP 404 (Non trovato).

## Passaggi successivi

Ora che sai come creare e configurare criteri di unione per la tua organizzazione, puoi utilizzarli per regolare la visualizzazione dei profili dei clienti all’interno di Platform e per creare segmenti di pubblico dai dati [!DNL Real-time Customer Profile]. Per iniziare a definire e lavorare con i segmenti, consulta la [documentazione del servizio di segmentazione Adobe Experience Platform](../../segmentation/home.md) .

## Appendice

Questa sezione fornisce informazioni supplementari relative all&#39;utilizzo dei criteri di unione.

### Utilizzo di marche temporali personalizzate {#custom-timestamps}

Man mano che i record vengono acquisiti in Experience Platform, una marca temporale di sistema viene ottenuta al momento dell’acquisizione e aggiunta al record. Quando `timestampOrdered` è selezionato come tipo `attributeMerge` per un criterio di unione, i profili vengono uniti in base alla marca temporale del sistema. In altre parole, l’unione viene eseguita in base alla marca temporale per quando il record è stato acquisito in Platform.

Talvolta possono verificarsi casi d’uso, ad esempio il backfill dei dati o la verifica dell’ordine corretto degli eventi se i record vengono acquisiti in modo non ordinato, dove è necessario fornire una marca temporale personalizzata e far rispettare alla policy di unione la marca temporale personalizzata anziché la marca temporale di sistema.

Per utilizzare una marca temporale personalizzata, è necessario aggiungere allo schema del profilo il [[!DNL External Source System Audit Details] gruppo di campi dello schema](#field-group-details). Una volta aggiunta, la marca temporale personalizzata può essere compilata utilizzando il campo `xdm:lastUpdatedDate` . Quando un record viene acquisito con il campo `xdm:lastUpdatedDate` popolato, Experience Platform lo utilizzerà per unire record o frammenti di profilo all’interno e tra set di dati. Se `xdm:lastUpdatedDate` non è presente o non è popolato, Platform continuerà a utilizzare la marca temporale del sistema.

>[!NOTE]
>
>È necessario assicurarsi che la marca temporale `xdm:lastUpdatedDate` sia compilata quando si invia un PATCH sullo stesso record.

Per istruzioni dettagliate sull’utilizzo degli schemi tramite l’API del Registro di sistema dello schema, tra cui come aggiungere gruppi di campi agli schemi, visita l’ [esercitazione per creare uno schema utilizzando l’API](../../xdm/tutorials/create-schema-api.md).

Per utilizzare le marche temporali personalizzate utilizzando l&#39;interfaccia utente, consulta la sezione su [uso delle marche temporali personalizzate](../merge-policies/overview.md#custom-timestamps) nella [panoramica dei criteri di unione](../merge-policies/overview.md).

#### [!DNL External Source System Audit Details] dettagli gruppo di campi  {#field-group-details}

L’esempio seguente mostra i campi compilati correttamente nel gruppo di campi [!DNL External Source System Audit Details] . Il gruppo di campi completo JSON può essere visualizzato anche nel repository [public Experience Data Model (XDM)](https://github.com/adobe/xdm/blob/master/components/mixins/shared/external-source-system-audit-details.schema.json) su GitHub.

```json
{
  "xdm:createdBy": "{CREATED_BY}",
  "xdm:createdDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastUpdatedBy": "{LAST_UPDATED_BY}",
  "xdm:lastUpdatedDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastActivityDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastReferencedDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastViewedDate": "2018-01-02T15:52:25+00:00"
 }
```
