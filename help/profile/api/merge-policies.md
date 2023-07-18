---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API per i criteri di unione
type: Documentation
description: Adobe Experience Platform consente di unire frammenti di dati provenienti da più origini e di combinarli in modo da ottenere una visualizzazione completa di ciascuno dei singoli clienti. Quando si riuniscono questi dati, i criteri di unione sono le regole utilizzate da Platform per determinare come i dati avranno priorità e quali saranno combinati per creare una vista unificata.
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '2467'
ht-degree: 2%

---

# Endpoint &quot;merge policies&quot;

Adobe Experience Platform consente di unire frammenti di dati provenienti da più origini e di combinarli in modo da ottenere una visualizzazione completa di ciascuno dei singoli clienti. Quando si riuniscono questi dati, i criteri di unione sono le regole che [!DNL Platform] utilizza per determinare come assegnare la priorità ai dati e quali dati verranno combinati per creare una vista unificata.

Ad esempio, se un cliente interagisce con il tuo marchio su più canali, la tua organizzazione avrà più frammenti di profilo relativi a quel singolo cliente che appaiono in più set di dati. Quando questi frammenti vengono acquisiti in Platform, vengono uniti per creare un unico profilo per quel cliente. Quando i dati provenienti da più origini sono in conflitto (ad esempio, un frammento elenca il cliente come &quot;singolo&quot; mentre l’altro lo elenca come &quot;sposato&quot;), il criterio di unione determina quali informazioni includere nel profilo dell’individuo.

Utilizzando le API RESTful o l’interfaccia utente di, puoi creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la tua organizzazione. Questa guida descrive i passaggi necessari per lavorare con i criteri di unione utilizzando l’API.

Per utilizzare i criteri di unione tramite l’interfaccia utente, consulta [guida dell’interfaccia utente per i criteri di unione](../merge-policies/ui-guide.md). Per ulteriori informazioni sui criteri di unione in generale e sul loro ruolo nell’Experience Platform, leggi [panoramica dei criteri di unione](../merge-policies/overview.md).

## Introduzione

L’endpoint API utilizzato in questa guida fa parte del [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Prima di continuare, controlla [guida introduttiva](getting-started.md) per collegamenti alla documentazione correlata, una guida per la lettura delle chiamate API di esempio di questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a [!DNL Experience Platform] API.

## Componenti dei criteri di unione {#components-of-merge-policies}

I criteri di unione sono privati per la tua organizzazione e ti consentono di creare diversi criteri per unire gli schemi nei modi specifici necessari. Qualsiasi API che accede a [!DNL Profile] i dati richiedono un criterio di unione, anche se verrà utilizzato un criterio predefinito, se non specificato in modo esplicito. [!DNL Platform] fornisce alle organizzazioni un criterio di unione predefinito, oppure puoi creare un criterio di unione per una classe di schema Experience Data Model (XDM) specifica e contrassegnarlo come predefinito per la tua organizzazione.

Anche se è possibile che ogni organizzazione disponga di più criteri di unione per classe di schema, ogni classe può disporre di un solo criterio di unione predefinito. Qualsiasi criterio di unione impostato come predefinito verrà utilizzato nei casi in cui viene fornito il nome della classe di schema e viene richiesto un criterio di unione, ma non viene fornito.

>[!NOTE]
>
>Quando si imposta un nuovo criterio di unione come predefinito, tutti i criteri di unione esistenti precedentemente impostati come predefinito verranno aggiornati automaticamente in modo da non essere più utilizzati come predefiniti.

Per garantire che tutti i consumatori di profili utilizzino la stessa vista sugli spigoli, i criteri di unione possono essere contrassegnati come attivi sugli spigoli. Per attivare un pubblico in Edge (contrassegnato come pubblico Edge), è necessario legarlo a un criterio di unione contrassegnato come attivo in Edge. Se un pubblico è **non** associato a un criterio di unione contrassegnato come attivo su edge, il pubblico non verrà contrassegnato come attivo su edge e verrà contrassegnato come pubblico in streaming.

Inoltre, ogni organizzazione può disporre solo di **uno** criterio di unione attivo su edge. Se un criterio di unione è attivo su Edge, può essere utilizzato per altri sistemi su Edge, ad esempio Profilo Edge, Segmentazione Edge e Destinazioni su Edge.

### Completa oggetto criterio di unione

L’oggetto criterio di unione completo rappresenta un insieme di preferenze che controllano gli aspetti dell’unione di frammenti di profilo.

**Oggetto criterio di unione**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{ORG_ID}",
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
| `name` | Nome intuitivo con cui è possibile identificare il criterio di unione nelle visualizzazioni elenco. |
| `imsOrgId` | ID organizzazione a cui appartiene il criterio di unione |
| `schema.name` | Parte del [`schema`](#schema) oggetto, il `name` contiene la classe di schema XDM a cui si riferisce il criterio di unione. Per ulteriori informazioni su schemi e classi, leggere [Documentazione XDM](../../xdm/home.md). |
| `version` | [!DNL Platform] versione mantenuta del criterio di unione. Questo valore di sola lettura viene incrementato ogni volta che un criterio di unione viene aggiornato. |
| `identityGraph` | [Grafo identità](#identity-graph) oggetto che indica il grafico delle identità da cui verranno ottenute le identità correlate. I frammenti di profilo trovati per tutte le identità correlate verranno uniti. |
| `attributeMerge` | [Unione attributi](#attribute-merge) oggetto che indica il modo in cui il criterio di unione assegnerà la priorità agli attributi del profilo in caso di conflitti di dati. |
| `isActiveOnEdge` | Valore booleano che indica se questo criterio di unione può essere utilizzato su Edge. Per impostazione predefinita, questo valore è `false`. |
| `default` | Valore booleano che indica se questo criterio di unione è il valore predefinito per lo schema specificato. |
| `updateEpoch` | Data dell’ultimo aggiornamento del criterio di unione. |

**Esempio di criterio di unione**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{ORG_ID}",
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

### Grafico delle identità {#identity-graph}

[Servizio Adobe Experience Platform Identity](../../identity-service/home.md) gestisce i grafici di identità utilizzati a livello globale e per ogni organizzazione su [!DNL Experience Platform]. Il `identityGraph` L’attributo del criterio di unione definisce come determinare le identità correlate per un utente.

**oggetto identityGraph**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Dove `{IDENTITY_GRAPH_TYPE}` è uno dei seguenti:

* **&quot;none&quot;:** Non eseguire alcuna unione di identità.
* **&quot;pdg&quot;** Esegui l’unione delle identità in base al grafico delle identità private.

**Esempio`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Unione attributi {#attribute-merge}

Un frammento di profilo è costituito dalle informazioni di profilo relative a una sola identità presente nell’elenco delle identità esistenti per un determinato utente. Quando il tipo di grafo delle identità utilizzato determina più di un’identità, è possibile che si verifichino conflitti tra gli attributi del profilo ed è necessario specificare la priorità. Utilizzo di `attributeMerge`, è possibile specificare gli attributi di profilo da assegnare come priorità in caso di conflitto di unione tra set di dati di tipo Valore chiave (dati record).

**attributeMerge, oggetto**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Dove `{ATTRIBUTE_MERGE_TYPE}` è uno dei seguenti:

* **`timestampOrdered`**: (impostazione predefinita) assegna priorità al profilo aggiornato per ultimo. Utilizzando questo tipo di unione, `data` attributo non obbligatorio.
* **`dataSetPrecedence`**: dai priorità ai frammenti di profilo in base al set di dati da cui provengono. Questo può essere utilizzato quando le informazioni presenti in un set di dati sono preferite o attendibili rispetto ai dati in un altro set di dati. Quando si utilizza questo tipo di unione, la `order` L’attributo è obbligatorio, in quanto elenca i set di dati in ordine di priorità.
   * **`order`**: quando si utilizza &quot;dataSetPrecedence&quot;, viene `order` è necessario fornire un array con un elenco di set di dati. Eventuali set di dati non inclusi nell’elenco non verranno uniti. In altre parole, i set di dati devono essere elencati in modo esplicito per essere uniti in un profilo. Il `order` array elenca gli ID dei set di dati in ordine di priorità.

#### Esempio `attributeMerge` oggetto tramite `dataSetPrecedence` tipo

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

#### Esempio `attributeMerge` oggetto tramite `timestampOrdered` tipo

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Schema {#schema}

L’oggetto schema specifica la classe di schema Experience Data Model (XDM) per la quale viene creato questo criterio di unione.

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

Per ulteriori informazioni su XDM e sull’utilizzo degli schemi in Experience Platform, leggi [Panoramica del sistema XDM](../../xdm/home.md).

## Accedere ai criteri di unione {#access-merge-policies}

Utilizzo di [!DNL Real-Time Customer Profile] API, `/config/mergePolicies` endpoint consente di eseguire una richiesta di ricerca per visualizzare un criterio di unione specifico in base al relativo ID o accedere a tutti i criteri di unione dell’organizzazione, filtrati in base a criteri specifici. È inoltre possibile utilizzare `/config/mergePolicies/bulk-get` per recuperare più criteri di unione in base ai relativi ID. I passaggi per eseguire ciascuna di queste chiamate sono descritti nelle sezioni seguenti.

### Accedere a un singolo criterio di unione per ID

Per accedere a un singolo criterio di unione in base al relativo ID, devi effettuare una richiesta di GET al `/config/mergePolicies` e che include `mergePolicyId` nel percorso della richiesta.

**Formato API**

```http
GET /config/mergePolicies/{mergePolicyId}
```

| Parametro | Descrizione |
|---|---|
| `{mergePolicyId}` | Identificatore del criterio di unione da eliminare. |

**Richiesta**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/10648288-cda5-11e8-a8d5-f2801f1b9fd1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del criterio di unione.

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{ORG_ID}",
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

Consulta la [componenti dei criteri di unione](#components-of-merge-policies) all’inizio del presente documento per i dettagli su ciascuno dei singoli elementi che compongono un criterio di unione.

### Recuperare più criteri di unione in base ai relativi ID

Per recuperare più criteri di unione, devi effettuare una richiesta POST al `/config/mergePolicies/bulk-get` e includendo gli ID dei criteri di unione che desideri recuperare nel corpo della richiesta.

**Formato API**

```http
POST /config/mergePolicies/bulk-get
```

**Richiesta**

Il corpo della richiesta include un array &quot;ids&quot; con singoli oggetti contenenti l’&quot;id&quot; per ogni criterio di unione per il quale desideri recuperare i dettagli.

```shell
curl -X POST \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/bulk-get' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

In caso di esito positivo, la risposta restituisce lo stato HTTP 207 (più stati) e i dettagli dei criteri di unione i cui ID sono stati forniti nella richiesta POST.

```json
{ 
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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

Consulta la [componenti dei criteri di unione](#components-of-merge-policies) all’inizio del presente documento per i dettagli su ciascuno dei singoli elementi che compongono un criterio di unione.

### Elencare più criteri di unione per criterio

È possibile elencare più criteri di unione all’interno dell’organizzazione inviando una richiesta di GET al `/config/mergePolicies` endpoint e utilizzo di parametri di query facoltativi per filtrare, ordinare e impaginare la risposta. È possibile includere più parametri, separati dal simbolo &amp;. Effettuando una chiamata a questo endpoint senza parametri, verranno recuperati tutti i criteri di unione disponibili per la tua organizzazione.

**Formato API**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Parametro | Descrizione |
|---|---|
| `default` | Valore booleano che filtra i risultati a seconda che i criteri di unione siano o meno l’impostazione predefinita per una classe di schema. |
| `limit` | Specifica il limite di dimensioni della pagina per controllare il numero di risultati inclusi in una pagina. Valore predefinito: 20 |
| `orderBy` | Specifica il campo in base al quale ordinare i risultati come in `orderBy=name` o `orderBy=+name` per ordinare in base al nome in ordine crescente, oppure `orderBy=-name`, per ordinare in ordine decrescente. Se si omette questo valore, viene applicato l’ordinamento predefinito `name` in ordine crescente. |
| `isActiveOnEdge` | Valori booleani che filtrano i risultati a seconda che i criteri di unione siano attivi o meno sul server Edge. |
| `schema.name` | Nome dello schema per il quale recuperare i criteri di unione disponibili. |
| `identityGraph.type` | Filtra i risultati per tipo di grafo delle identità. I valori possibili includono &quot;none&quot; (nessuno) e &quot;pdg&quot; (Private graph). |
| `attributeMerge.type` | Filtra i risultati in base al tipo di unione degli attributi utilizzato. I valori possibili includono &quot;timestampOrdered&quot; e &quot;dataSetPrecedence&quot;. |
| `start` | Offset pagina: specifica l’ID iniziale dei dati da recuperare. Valore predefinito: 0 |
| `version` | Specificare questa opzione se si desidera utilizzare una versione specifica del criterio di unione. Per impostazione predefinita, viene utilizzata la versione più recente. |

Per ulteriori informazioni su `schema.name`, `identityGraph.type`, e `attributeMerge.type`, fare riferimento a [componenti dei criteri di unione](#components-of-merge-policies) fornite in precedenza in questa guida.


**Richiesta**

La richiesta seguente elenca tutti i criteri di unione per un determinato schema:

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco impaginato di criteri di unione che soddisfano i criteri specificati dai parametri di query inviati nella richiesta.

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
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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
| `_links.next.href` | Un indirizzo URI per la pagina di risultati successiva. Utilizza questo URI come parametro della richiesta per un’altra chiamata API allo stesso endpoint per visualizzare la pagina. Se non esiste alcuna pagina successiva, questo valore sarà una stringa vuota. |

## Creare un criterio di unione

Per creare un nuovo criterio di unione per l’organizzazione, effettua una richiesta POST al `/config/mergePolicies` endpoint.

**Formato API**

```http
POST /config/mergePolicies
```

**Richiesta**
La richiesta seguente crea un nuovo criterio di unione, configurato dai valori di attributo forniti nel payload:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | Nome descrittivo con cui è possibile identificare il criterio di unione nelle visualizzazioni elenco. |
| `identityGraph.type` | Tipo di grafo delle identità da cui ottenere le identità correlate da unire. Valori possibili: &quot;none&quot; (nessuno) o &quot;pdg&quot; (Private graph). |
| `attributeMerge` | Il modo in cui assegnare la priorità ai valori degli attributi di profilo in caso di conflitti di dati. |
| `schema` | La classe dello schema XDM associata al criterio di unione. |
| `isActiveOnEdge` | Specifica se il criterio di unione è attivo sul server Edge. |
| `default` | Specifica se questo criterio di unione è il valore predefinito dello schema. |

Consulta la sezione [componenti dei criteri di unione](#components-of-merge-policies) per ulteriori informazioni.

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del criterio di unione appena creato.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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

Consulta la [componenti dei criteri di unione](#components-of-merge-policies) all’inizio del presente documento per i dettagli su ciascuno dei singoli elementi che compongono un criterio di unione.

## Aggiornare un criterio di unione {#update}

È possibile modificare un criterio di unione esistente modificando singoli attributi (PATCH) o sovrascrivendo l’intero criterio di unione con nuovi attributi (PUT). Di seguito sono riportati alcuni esempi di ciascuno di essi.

### Modificare singoli campi dei criteri di unione

È possibile modificare singoli campi per un criterio di unione effettuando una richiesta PATCH al `/config/mergePolicies/{mergePolicyId}` endpoint:

**Formato API**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Parametro | Descrizione |
|---|---|
| `{mergePolicyId}` | Identificatore del criterio di unione da eliminare. |

**Richiesta**

La richiesta seguente aggiorna un criterio di unione specificato modificando il valore del relativo `default` proprietà a `true`:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | Specifica l&#39;operazione da eseguire. Esempi di altre operazioni PATCH sono disponibili nella sezione [Documentazione delle patch JSON](https://datatracker.ietf.org/doc/html/rfc6902) |
| `path` | Percorso del campo da aggiornare. I valori accettati sono: &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot;, &quot;/isActiveOnEdge&quot; |
| `value` | Il valore su cui impostare il campo specificato. |

Consulta la sezione [componenti dei criteri di unione](#components-of-merge-policies) per ulteriori informazioni.


**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del criterio di unione appena aggiornato.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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

### Sovrascrivere un criterio di unione

Un altro modo per modificare un criterio di unione consiste nell’utilizzare una richiesta PUT, che sovrascrive l’intero criterio di unione.

**Formato API**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| Parametro | Descrizione |
|---|---|
| `{mergePolicyId}` | Identificatore del criterio di unione da sovrascrivere. |

**Richiesta**

La richiesta seguente sovrascrive il criterio di unione specificato, sostituendo i valori degli attributi con quelli forniti nel payload. Poiché questa richiesta sostituisce completamente un criterio di unione esistente, è necessario fornire tutti gli stessi campi richiesti durante la definizione originale del criterio di unione. Tuttavia, questa volta si forniscono valori aggiornati per i campi che si desidera modificare.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{ORG_ID}",
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
| `name` | Nome descrittivo con cui è possibile identificare il criterio di unione nelle visualizzazioni elenco. |
| `identityGraph` | Grafo di identità da cui ottenere le identità correlate da unire. |
| `attributeMerge` | Il modo in cui assegnare la priorità ai valori degli attributi di profilo in caso di conflitti di dati. |
| `schema` | La classe dello schema XDM associata al criterio di unione. |
| `isActiveOnEdge` | Specifica se il criterio di unione è attivo sul server Edge. |
| `default` | Specifica se questo criterio di unione è il valore predefinito dello schema. |

Consulta la sezione [componenti dei criteri di unione](#components-of-merge-policies) per ulteriori informazioni.

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del criterio di unione aggiornato.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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

È possibile eliminare un criterio di unione effettuando una richiesta DELETE al `/config/mergePolicies` e includendo l’ID del criterio di unione da eliminare nel percorso della richiesta.

>[!NOTE]
>
>Se il criterio di unione ha `isActiveOnEdge` impostato su true, il criterio di unione **non può** essere soppressa. Utilizza il [PATCH](#edit-individual-merge-policy-fields) o [PUT](#overwrite-a-merge-policy) endpoint per aggiornare il criterio di unione prima di eliminarlo.

**Formato API**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| Parametro | Descrizione |
|---|---|
| `{mergePolicyId}` | Identificatore del criterio di unione da eliminare. |

**Richiesta**

La richiesta seguente elimina un criterio di unione.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

In caso di esito positivo, la richiesta di eliminazione restituisce lo stato HTTP 200 (OK) e un corpo di risposta vuoto. Per confermare che l’eliminazione è avvenuta correttamente, puoi eseguire una richiesta di GET per visualizzare il criterio di unione in base al relativo ID. Se il criterio di unione è stato eliminato, verrà visualizzato un errore Stato HTTP 404 (Non trovato).

## Passaggi successivi

Ora che sai come creare e configurare i criteri di unione per la tua organizzazione, puoi utilizzarli per regolare la visualizzazione dei profili dei clienti in Platform e per creare tipi di pubblico dal tuo [!DNL Real-Time Customer Profile] dati.

Consulta la sezione [Documentazione del servizio di segmentazione di Adobe Experience Platform](../../segmentation/home.md) per iniziare a definire e utilizzare i tipi di pubblico.
