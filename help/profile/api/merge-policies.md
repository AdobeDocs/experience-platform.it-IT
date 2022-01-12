---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API per criteri di unione
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform consente di unire frammenti di dati provenienti da più sorgenti e di combinarli per ottenere una visualizzazione completa di ciascuno dei singoli clienti. Quando si riuniscono questi dati, i criteri di unione sono le regole utilizzate da Platform per determinare in che modo i dati verranno definiti come prioritari e quali dati verranno combinati per creare una visualizzazione unificata.
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '2472'
ht-degree: 2%

---

# Endpoint Criteri di unione

Adobe Experience Platform consente di unire frammenti di dati provenienti da più sorgenti e di combinarli per ottenere una visualizzazione completa di ciascuno dei singoli clienti. Quando si uniscono questi dati, i criteri di unione sono regole che [!DNL Platform] utilizza per determinare come assegnare una priorità ai dati e quali saranno i dati combinati per creare una visualizzazione unificata.

Ad esempio, se un cliente interagisce con il tuo marchio su più canali, la tua organizzazione avrà più frammenti di profilo relativi al singolo cliente che compaiono in più set di dati. Quando questi frammenti vengono acquisiti in Platform, vengono uniti per creare un singolo profilo per quel cliente. Quando i dati provenienti da più origini sono in conflitto (ad esempio, un frammento elenca il cliente come &quot;singolo&quot;, mentre l’altro elenca il cliente come &quot;sposato&quot;), il criterio di unione determina quali informazioni includere nel profilo dell’utente.

Utilizzando le API RESTful o l&#39;interfaccia utente, è possibile creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la propria organizzazione. Questa guida descrive i passaggi necessari per l’utilizzo delle API per l’unione dei criteri.

Per utilizzare i criteri di unione utilizzando l’interfaccia utente, consulta [guida all’interfaccia utente per i criteri di unione](../merge-policies/ui-guide.md). Per ulteriori informazioni sui criteri di unione in generale e sul loro ruolo all&#39;interno dell&#39;Experience Platform, leggere innanzitutto il [panoramica dei criteri di unione](../merge-policies/overview.md).

## Introduzione

L’endpoint API utilizzato in questa guida fa parte del [[!DNL Real-time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Prima di continuare, controlla la [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio presenti in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi [!DNL Experience Platform] API.

## Componenti dei criteri di unione {#components-of-merge-policies}

I criteri di unione sono privati dell’organizzazione IMS e consentono di creare diversi criteri per unire gli schemi nei modi specifici necessari. Qualsiasi API che accede a [!DNL Profile] i dati richiedono un criterio di unione, anche se viene utilizzato un valore predefinito se non viene fornito in modo esplicito. [!DNL Platform] fornisce alle organizzazioni un criterio di unione predefinito oppure è possibile creare un criterio di unione per una classe di schema XDM (Experience Data Model) specifica e contrassegnarlo come predefinito per la propria organizzazione.

Sebbene ogni organizzazione possa avere potenzialmente più criteri di unione per classe di schema, ogni classe può avere un solo criterio di unione predefinito. I criteri di unione impostati come predefiniti verranno utilizzati nei casi in cui viene fornito il nome della classe dello schema e viene richiesto un criterio di unione, ma non viene fornito.

>[!NOTE]
>
>Quando si imposta come impostazione predefinita un nuovo criterio di unione, tutti i criteri di unione esistenti precedentemente impostati come predefiniti verranno automaticamente aggiornati in modo da non essere più utilizzati come impostazione predefinita.

Per garantire che tutti i consumatori di profili lavorino con la stessa vista sui bordi, i criteri di unione possono essere contrassegnati come attivi sui bordi. Affinché un segmento possa essere attivato sul bordo (contrassegnato come segmento edge), deve essere associato a un criterio di unione contrassegnato come attivo sul bordo. Se un segmento è **not** associato a un criterio di unione contrassegnato come attivo sul bordo, il segmento non sarà contrassegnato come attivo sul bordo e sarà contrassegnato come segmento in streaming.

Inoltre, ogni organizzazione IMS può avere solo **uno** criterio di unione attivo sul bordo. Se un criterio di unione è attivo su Edge, può essere utilizzato per altri sistemi su Edge, ad esempio Profilo Edge, Segmentazione Edge e Destinazioni su Edge.

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
        "isActiveOnEdge": "{BOOLEAN}",
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| Proprietà | Descrizione |
|---|---|
| `id` | Identificatore univoco generato dal sistema assegnato al momento della creazione |
| `name` | Nome descrittivo in base al quale i criteri di unione possono essere identificati nelle viste elenco. |
| `imsOrgId` | ID organizzazione a cui appartiene il criterio di unione |
| `schema.name` | Parte del [`schema`](#schema) l&#39;oggetto `name` Il campo contiene la classe dello schema XDM a cui si riferisce il criterio di unione. Per ulteriori informazioni su schemi e classi, leggere il [Documentazione di XDM](../../xdm/home.md). |
| `version` | [!DNL Platform] versione aggiornata dei criteri di unione. Questo valore di sola lettura viene incrementato ogni volta che un criterio di unione viene aggiornato. |
| `identityGraph` | [Grafico di identità](#identity-graph) oggetto che indica il grafico di identità da cui verranno ottenute le identità correlate. I frammenti di profilo trovati per tutte le identità correlate verranno uniti. |
| `attributeMerge` | [Unione attributi](#attribute-merge) oggetto che indica il modo in cui il criterio di unione darà priorità agli attributi del profilo in caso di conflitti di dati. |
| `isActiveOnEdge` | Valore booleano che indica se questo criterio di unione può essere utilizzato sul bordo. Per impostazione predefinita, questo valore è `false`. |
| `default` | Valore booleano che indica se il criterio di unione è il valore predefinito per lo schema specificato. |
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
        "isActiveOnEdge": false,
        "default": true,
        "updateEpoch": 1551660639
    }
```

### Grafico di identità {#identity-graph}

[Servizio Adobe Experience Platform Identity](../../identity-service/home.md) gestisce i grafici di identità utilizzati a livello globale e per ogni organizzazione in [!DNL Experience Platform]. La `identityGraph` l&#39;attributo del criterio di unione definisce come determinare le identità correlate per un utente.

**oggetto identityGraph**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Dove `{IDENTITY_GRAPH_TYPE}` è uno dei seguenti:

* **&quot;none&quot;:** Non eseguire alcuna unione di identità.
* **&quot;pdg&quot;:** Eseguire unione di identità in base al grafico di identità privata.

**Esempio`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Unione attributi {#attribute-merge}

Un frammento di profilo è l’informazione di profilo per una sola identità inclusa nell’elenco di identità esistenti per un particolare utente. Quando il tipo di grafico di identità utilizzato genera più di un&#39;identità, è possibile che vi siano attributi di profilo in conflitto e deve essere specificata la priorità. Utilizzo `attributeMerge`, è possibile specificare gli attributi di profilo da assegnare alla priorità in caso di un conflitto di unione tra i set di dati di tipo Valore chiave (dati record).

**oggetto attributeMerge**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Dove `{ATTRIBUTE_MERGE_TYPE}` è uno dei seguenti:

* **`timestampOrdered`**: (Impostazione predefinita) Assegna priorità al profilo aggiornato per ultimo. Utilizzando questo tipo di unione, la `data` attributo non obbligatorio.
* **`dataSetPrecedence`**: Assegna priorità ai frammenti di profilo in base al set di dati da cui provengono. Questo può essere utilizzato quando le informazioni presenti in un set di dati sono preferite o attendibili rispetto ai dati di un altro set di dati. Quando si utilizza questo tipo di unione, la `order` attributo obbligatorio, in quanto elenca i set di dati in ordine di priorità.
   * **`order`**: Quando si utilizza &quot;dataSetPrecedence&quot;, un `order` deve essere fornito con un elenco di set di dati. Eventuali set di dati non inclusi nell’elenco non verranno uniti. In altre parole, i set di dati devono essere elencati in modo esplicito per essere uniti in un profilo. La `order` array elenca gli ID dei set di dati in ordine di priorità.

#### Esempio `attributeMerge` oggetto che utilizza `dataSetPrecedence` type

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

#### Esempio `attributeMerge` oggetto che utilizza `timestampOrdered` type

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

Se il valore di `name` è il nome della classe XDM su cui si basa lo schema associato al criterio di unione.

**Esempio`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

Per ulteriori informazioni su XDM e sull’utilizzo degli schemi in Experience Platform, inizia leggendo il [Panoramica del sistema XDM](../../xdm/home.md).

## Accedere ai criteri di unione {#access-merge-policies}

Utilizzo della [!DNL Real-time Customer Profile] API, `/config/mergePolicies` L’endpoint ti consente di eseguire una richiesta di ricerca per visualizzare un criterio di unione specifico in base al relativo ID o per accedere a tutti i criteri di unione nell’organizzazione IMS, filtrati in base a criteri specifici. È inoltre possibile utilizzare `/config/mergePolicies/bulk-get` per recuperare più criteri di unione in base ai relativi ID. I passaggi per eseguire ciascuna di queste chiamate sono descritti nelle sezioni seguenti.

### Accedere a un criterio di unione singolo per ID

Puoi accedere a un singolo criterio di unione dal relativo ID effettuando una richiesta di GET al `/config/mergePolicies` l&#39;endpoint e `mergePolicyId` nel percorso della richiesta.

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
    "isActiveOnEdge": "false",
    "default": false,
    "updateEpoch": 1551127597
}
```

Consulta la sezione [componenti dei criteri di unione](#components-of-merge-policies) sezione all&#39;inizio del documento per i dettagli su ciascuno dei singoli elementi che compongono un criterio di unione.

### Recupera più criteri di unione in base ai relativi ID

È possibile recuperare più criteri di unione effettuando una richiesta di POST al `/config/mergePolicies/bulk-get` endpoint e ID dei criteri di unione che si desidera recuperare nel corpo della richiesta.

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
            "isActiveOnEdge": true,
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
            "isActiveOnEdge": false,
            "default": false,
            "updateEpoch": 1576099719
        }
    }
}
```

Consulta la sezione [componenti dei criteri di unione](#components-of-merge-policies) sezione all&#39;inizio del documento per i dettagli su ciascuno dei singoli elementi che compongono un criterio di unione.

### Elencare più criteri di unione in base ai criteri

È possibile elencare più criteri di unione all’interno dell’organizzazione IMS inviando una richiesta di GET a `/config/mergePolicies` e utilizzando parametri di query facoltativi per filtrare, ordinare e impaginare la risposta. È possibile includere più parametri, separati da e commerciale (&amp;). Effettuare una chiamata a questo endpoint senza parametri recupererà tutti i criteri di unione disponibili per la tua organizzazione.

**Formato API**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Parametro | Descrizione |
|---|---|
| `default` | Valore booleano che filtra i risultati in base al fatto che i criteri di unione siano o meno i valori predefiniti per una classe di schema. |
| `limit` | Specifica il limite di dimensioni della pagina per controllare il numero di risultati inclusi in una pagina. Valore predefinito: 20 |
| `orderBy` | Specifica il campo in base al quale ordinare i risultati come in `orderBy=name` o `orderBy=+name` ordinare in ordine crescente per nome, oppure `orderBy=-name`, in ordine decrescente. Se si omette questo valore, viene eseguito l’ordinamento predefinito di `name` in ordine crescente. |
| `isActiveOnEdge` | Valori booleani che filtrano i risultati a seconda che i criteri di unione siano attivi o meno sul bordo. |
| `schema.name` | Nome dello schema per il quale recuperare i criteri di unione disponibili. |
| `identityGraph.type` | Filtra i risultati in base al tipo di grafico delle identità. I valori possibili includono &quot;none&quot; e &quot;pdg&quot; (grafico privato). |
| `attributeMerge.type` | Filtra i risultati in base al tipo di unione degli attributi utilizzato. I valori possibili includono &quot;timestampOrdered&quot; e &quot;dataSetPrecedence&quot;. |
| `start` | Offset pagina - specifica l’ID iniziale per i dati da recuperare. Valore predefinito: 0 |
| `version` | Specificare questa opzione se si desidera utilizzare una versione specifica del criterio di unione. Per impostazione predefinita, verrà utilizzata la versione più recente. |

Per ulteriori informazioni su `schema.name`, `identityGraph.type`e `attributeMerge.type`, fare riferimento alla [componenti dei criteri di unione](#components-of-merge-policies) sezione fornita in precedenza in questa guida.


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
            "isActiveOnEdge": true,
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
            "isActiveOnEdge": false,
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

È possibile creare un nuovo criterio di unione per la propria organizzazione effettuando una richiesta di POST al `/config/mergePolicies` punto finale.

**Formato API**

```http
POST /config/mergePolicies
```

**Richiesta**
La richiesta seguente crea un nuovo criterio di unione, configurato dai valori degli attributi forniti nel payload:

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
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "isActiveOnEdge": true,
    "default": true
}'
```

| Proprietà | Descrizione |
|---|---|
| `name` | Un nome descrittivo in base al quale è possibile identificare il criterio di unione nelle viste a elenco. |
| `identityGraph.type` | Il tipo di grafico delle identità da cui ottenere le identità correlate da unire. Valori possibili: &quot;none&quot; o &quot;pdg&quot; (grafico privato). |
| `attributeMerge` | Modalità con cui assegnare la priorità ai valori degli attributi del profilo in caso di conflitti di dati. |
| `schema` | Classe dello schema XDM associata al criterio di unione. |
| `isActiveOnEdge` | Specifica se il criterio di unione è attivo sul bordo. |
| `default` | Specifica se il criterio di unione è il valore predefinito per lo schema. |

Fai riferimento a [componenti dei criteri di unione](#components-of-merge-policies) per ulteriori informazioni.

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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

Consulta la sezione [componenti dei criteri di unione](#components-of-merge-policies) sezione all&#39;inizio del documento per i dettagli su ciascuno dei singoli elementi che compongono un criterio di unione.

## Aggiornare un criterio di unione {#update}

È possibile modificare un criterio di unione esistente modificando singoli attributi (PATCH) o sovrascrivendo l&#39;intero criterio di unione con nuovi attributi (PUT). Di seguito sono riportati alcuni esempi di ciascuno di essi.

### Modifica di singoli campi dei criteri di unione

È possibile modificare singoli campi di un criterio di unione effettuando una richiesta di PATCH al `/config/mergePolicies/{mergePolicyId}` punto finale:

**Formato API**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Parametro | Descrizione |
|---|---|
| `{mergePolicyId}` | Identificatore del criterio di unione che si desidera eliminare. |

**Richiesta**

La richiesta seguente aggiorna un criterio di unione specificato modificando il valore del relativo `default` proprietà di `true`:

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
| `op` | Specifica l&#39;operazione da eseguire. Alcuni esempi di altre operazioni di PATCH sono disponibili nella sezione [Documentazione sulle patch JSON](https://datatracker.ietf.org/doc/html/rfc6902) |
| `path` | Percorso del campo da aggiornare. I valori accettati sono: &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot;, &quot;/isActiveOnEdge&quot; |
| `value` | Valore su cui impostare il campo specificato. |

Fai riferimento a [componenti dei criteri di unione](#components-of-merge-policies) per ulteriori informazioni.


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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

### Sovrascrivi criterio di unione

Un altro modo per modificare un criterio di unione consiste nell’utilizzare una richiesta PUT, che sovrascrive l’intero criterio di unione.

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
        "isActiveOnEdge": true,
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
| `isActiveOnEdge` | Specifica se il criterio di unione è attivo sul bordo. |
| `default` | Specifica se il criterio di unione è il valore predefinito per lo schema. |

Fai riferimento a [componenti dei criteri di unione](#components-of-merge-policies) per ulteriori informazioni.

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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

## Eliminare un criterio di unione

È possibile eliminare un criterio di unione effettuando una richiesta di DELETE al `/config/mergePolicies` e l&#39;ID del criterio di unione che si desidera eliminare nel percorso della richiesta.

>[!NOTE]
>
>Se il criterio di unione è `isActiveOnEdge` impostato su true, il criterio di unione **impossibile** essere soppressa. Utilizza [PATCH](#edit-individual-merge-policy-fields) o [PUT](#overwrite-a-merge-policy) endpoint per aggiornare il criterio di unione prima di eliminarlo.

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

Ora che sai come creare e configurare criteri di unione per la tua organizzazione, puoi utilizzarli per regolare la visualizzazione dei profili dei clienti all’interno di Platform e per creare segmenti di pubblico dai tuoi [!DNL Real-time Customer Profile] dati.

Vedi la [Documentazione del servizio di segmentazione Adobe Experience Platform](../../segmentation/home.md) per iniziare a definire e lavorare con i segmenti.
