---
title: Ordinamento e filtraggio delle risposte nell’API del servizio Flusso
description: Questa esercitazione descrive la sintassi per l’ordinamento e il filtraggio utilizzando i parametri di query nell’API del servizio Flusso, inclusi alcuni casi d’uso avanzati.
exl-id: 029c3199-946e-4f89-ba7a-dac50cc40c09
source-git-commit: c7ff379b260edeef03f8b47f932ce9040eef3be2
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 2%

---

# Ordinamento e filtraggio delle risposte nell’API del servizio Flusso

Durante l’esecuzione delle richieste di inserimento nell’elenco (GET) in [API del servizio Flusso](https://www.adobe.io/experience-platform-apis/references/flow-service/), puoi utilizzare i parametri di query per ordinare e filtrare le risposte. Questa guida fornisce un riferimento su come utilizzare questi parametri per diversi casi d’uso.

## Ordinamento

È possibile ordinare le risposte utilizzando un `orderby` parametro query. Le seguenti risorse possono essere ordinate nell’API:

* [Connessioni](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [Connessioni di origine](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [Connessioni di destinazione](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [Flussi](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [Esecuzioni](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

Per utilizzare il parametro, è necessario impostarne il valore sulla proprietà specifica in base alla quale si desidera ordinare (ad esempio, `?orderby=name`). È possibile anteporre al valore un segno più (`+`) per ordine crescente o segno meno (`-`) in ordine decrescente. Se non viene fornito alcun prefisso di ordinamento, l’elenco viene ordinato in ordine crescente per impostazione predefinita.

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

È inoltre possibile combinare un parametro di ordinamento con un parametro di filtro utilizzando il simbolo &quot;e&quot; (`&`).

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## Filtro

Puoi filtrare le risposte utilizzando una `property` parametro con un&#39;espressione chiave-valore. Ad esempio: `?property=id==12345` restituisce solo risorse il cui `id` la proprietà è esattamente uguale a `12345`.

Il filtro può essere applicato in modo generico a qualsiasi proprietà in un’entità, purché sia noto il percorso valido di tale proprietà.

>[!NOTE]
>
>Se una proprietà è nidificata all&#39;interno di un elemento matrice, è necessario aggiungere parentesi quadre (`[]`) all&#39;array nel percorso. Consulta la sezione su [filtraggio in base alle proprietà dell’array](#arrays) ad esempio.

**Restituisce tutte le connessioni di origine in cui il nome della tabella di origine è `lead`:**

```http
GET /sourceConnections?property=params.tableName==lead
```

**Restituisce tutti i flussi per un ID segmento specifico:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### Unione di filtri

Più `property` i filtri possono essere inclusi in una query a condizione che siano separati da caratteri &quot;e&quot; (`&`). Quando si combinano i filtri si assume una relazione AND, il che significa che un’entità deve soddisfare tutti i filtri per essere inclusa nella risposta.

**Restituisce tutti i flussi abilitati per un ID segmento:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### Filtraggio delle proprietà dell’array {#arrays}

Puoi filtrare in base alle proprietà degli elementi all’interno degli array aggiungendo `[]` al nome della proprietà array.

**Flussi di ritorno associati a connessioni di origine specifiche:**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**Flussi di ritorno con una trasformazione contenente un ID di valore selettore specifico:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**Restituire le connessioni di origine che hanno una colonna con un `name` valore:**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**Cerca l’ID di esecuzione del flusso per una destinazione filtrando per ID segmento:**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

Qualsiasi query di filtro può essere aggiunta con `count` parametro di query con valore `true` per restituire il conteggio dei risultati. La risposta API contiene un `count` proprietà il cui valore rappresenta il conteggio del totale degli elementi filtrati. Gli elementi filtrati effettivi non vengono restituiti in questa chiamata.

**Restituisce il conteggio dei flussi abilitati nel sistema:**

```http
GET /flows?property=state==enabled&count=true
```

La risposta alla query precedente sarà simile alla seguente:

```json
{
  "count": 95
}
```

### Proprietà filtrabili per risorsa

A seconda dell’entità Servizio flusso che stai recuperando, è possibile utilizzare proprietà diverse per il filtro. Le tabelle seguenti suddividono i campi a livello principale per ogni risorsa comunemente utilizzata per filtrare i casi d’uso.

**`connectionSpec`**

| Proprietà | Esempio |
| --- | --- |
| `id` | `/connectionSpecs?property=id==736873,9485095` |
| `name` | `/connectionSpecs?property=name==TestConn` |
| `providerId` | `/connectionSpecs?property=providerId==3897933` |
| `attributes.{ATTRIBUTE_NAME}` | `/connectionSpecs?property=attributes.sampleAttribute="abc"` |

{style="table-layout:auto"}

**`flowSpec`**

| Proprietà | Esempio |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style="table-layout:auto"}

**`connection`**

| Proprietà | Esempio |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style="table-layout:auto"}

**`sourceConnection`**

| Proprietà | Esempio |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

**`targetConnection`**

| Proprietà | Esempio |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

**`flow`**

| Proprietà | Esempio |
| --- | --- |
| `id` | `/flows?property=id==736873,9485095` |
| `name` | `/flows?property=name==TestFlow` |
| `description` | `/flows?property=description==Test%20description` |
| `flowSpec.id` | `/flows?property=flowSpec.id==938903,849048` |
| `state` | `/flows?property=state==enabled` |
| `sourceConnectionIds` | `/flows?property=sourceConnectionIds[]==9874984,6980696` |
| `targetConnectionIds` | `/flows?property=targetConnectionIds[]==598590,690666` |

{style="table-layout:auto"}

**`run`**

| Proprietà | Esempio |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style="table-layout:auto"}

## Casi d’uso {#use-cases}

Leggi questa sezione per alcuni esempi specifici su come utilizzare i filtri e l’ordinamento per restituire informazioni su determinati connettori o per assistenza nei problemi di debug. Adobe Se desideri aggiungere altri casi d’uso, utilizza l’ **[!UICONTROL Opzioni di feedback dettagliate]** sulla pagina per inviare una richiesta.

**Filtro per restituire solo le connessioni a una determinata destinazione**

Puoi utilizzare i filtri per restituire connessioni solo a determinate destinazioni. Innanzitutto, esegui una query su `connectionSpecs` endpoint come quello riportato di seguito:

```http
GET /connectionSpecs
```

Quindi, cerca il `connectionSpec` esaminando la `name` parametro. Ad esempio, cerca Amazon Ads, o Pega, o SFTP, e così via in `name` parametro. Il corrispondente `id` è il `connectionSpec` che puoi cercare nella chiamata API successiva.

Ad esempio, filtra le destinazioni per restituire solo le connessioni esistenti alle connessioni Amazon S3:

```http
GET /connections?property=connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**Filtra per restituire flussi di dati solo alle destinazioni**

Quando si esegue una query su `/flows` endpoint, invece di restituire tutti i flussi di dati di origini e destinazioni, puoi utilizzare un filtro per restituire solo i flussi di dati alle destinazioni. A tale scopo, utilizza `isDestinationFlow` come parametro di query, come segue:

```http
GET /flows?property=inheritedAttributes.properties.isDestinationFlow==true
```

**Filtro per restituire flussi di dati solo a una determinata origine o destinazione**

Puoi filtrare i flussi di dati per restituirli solo a una determinata destinazione o da una determinata origine. Ad esempio, filtra le destinazioni per restituire solo le connessioni esistenti alle connessioni Amazon S3:

```http
GET /flows?property=inheritedAttributes.targetConnections[].connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**Filtro per ottenere tutte le esecuzioni di un flusso di dati per un periodo di tempo specifico**

Puoi filtrare le esecuzioni di un flusso di dati per esaminare solo le esecuzioni in un determinato intervallo di tempo, come segue:

```
GET /runs?property=flowId==<flow-id>&property=metrics.durationSummary.startedAtUTC>1593134665781&property=metrics.durationSummary.startedAtUTC<1653134665781
```

**Filtro per restituire solo i flussi di dati non riusciti**

A scopo di debug, puoi filtrare e visualizzare tutti i flussi di dati non riusciti eseguiti per un determinato flusso di dati di origine o di destinazione, come indicato di seguito:

```http
GET /runs?property=flowId==<flow-id>&property=metrics.statusSummary.status==Failed
```

## Passaggi successivi

Questa guida illustra come utilizzare `orderby` e `property` Parametri di query per ordinare e filtrare le risposte nell’API del servizio Flusso. Per guide dettagliate sull’utilizzo dell’API per i flussi di lavoro più comuni in Platform, consulta i tutorial sull’API contenuti in [sorgenti](../../sources/home.md) e [destinazioni](../../destinations/home.md) documentazione.
