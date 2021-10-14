---
title: Ordinamento e filtraggio delle risposte nell’API del servizio di flusso
description: Questa esercitazione descrive la sintassi per l’ordinamento e il filtraggio utilizzando i parametri di query nell’API del servizio di flusso, inclusi alcuni casi d’uso avanzati.
source-git-commit: ccca81357bd7d7083abd3f395aa547c85ebf65fd
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 6%

---

# Ordinamento e filtraggio delle risposte nell’API del servizio di flusso

Quando esegui richieste di inserimento nell&#39;elenco (GET) nell&#39; [API del servizio di flusso](https://www.adobe.io/experience-platform-apis/references/flow-service/), puoi utilizzare i parametri di query per ordinare e filtrare le risposte. Questa guida fornisce un riferimento su come utilizzare questi parametri per diversi casi d’uso.

## Ordinamento

Puoi ordinare le risposte utilizzando un parametro di query `orderby`. Le risorse seguenti possono essere ordinate nell’API:

* [Connessioni](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [Connessioni di origine](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [Connessioni di destinazione](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [Flussi](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [Esegue](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

Per utilizzare il parametro , è necessario impostarne il valore sulla proprietà specifica per la quale si desidera eseguire l’ordinamento (ad esempio, `?orderby=name`). È possibile anteporre il valore con un segno più (`+`) per l&#39;ordine crescente o il segno meno (`-`) per l&#39;ordine decrescente. Se non viene fornito alcun prefisso di ordinamento, l’elenco viene ordinato in ordine crescente per impostazione predefinita.

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

È inoltre possibile combinare un parametro di ordinamento con un parametro di filtro utilizzando un simbolo &quot;e&quot; (`&`).

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## Filtro

Puoi filtrare le risposte utilizzando un parametro `property` con un&#39;espressione chiave-valore. Ad esempio, `?property=id==12345` restituisce solo risorse la cui proprietà `id` è uguale esattamente a `12345`.

Il filtro può essere applicato genericamente su qualsiasi proprietà di un&#39;entità, purché sia noto il percorso valido di tale proprietà.

>[!NOTE]
>
>Se una proprietà è nidificata all&#39;interno di un elemento array, è necessario aggiungere parentesi quadre (`[]`) all&#39;array nel percorso. Per esempi, consulta la sezione sul filtro [sulle proprietà dell&#39;array](#arrays) .

**Restituisce tutte le connessioni di origine in cui il nome della tabella di origine è  `lead`:**

```http
GET /sourceConnections?property=params.tableName==lead
```

**Restituisce tutti i flussi per un ID segmento specifico:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### Combinazione di filtri

È possibile includere più filtri `property` in una query purché siano separati da caratteri &quot;e&quot; (`&`). Si presume una relazione AND quando si combinano i filtri, il che significa che un’entità deve soddisfare tutti i filtri affinché sia inclusa nella risposta.

**Restituisce tutti i flussi abilitati per un ID segmento:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### Filtro sulle proprietà della matrice {#arrays}

È possibile filtrare in base alle proprietà degli elementi all&#39;interno degli array aggiungendo `[]` al nome della proprietà array.

**Restituire i flussi associati a specifiche connessioni di origine:**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**Restituisce i flussi che hanno una trasformazione contenente un ID valore di selettore specifico:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**Restituisce le connessioni di origine con una colonna con un  `name` valore specifico:**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**Cerca l’ID di esecuzione del flusso per una destinazione filtrando l’ID del segmento:**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

È possibile aggiungere qualsiasi query di filtro con il parametro di query `count` con un valore `true` per restituire il conteggio dei risultati. La risposta API contiene una proprietà `count` il cui valore rappresenta il conteggio del totale degli elementi filtrati. Gli elementi filtrati effettivi non vengono restituiti in questa chiamata.

**Restituisce il conteggio dei flussi abilitati nel sistema:**

```http
GET /flows?property=state==enabled&count=true
```

La risposta alla query di cui sopra sarà simile alla seguente:

```json
{
  "count": 95
}
```

### Proprietà filtrabili per risorsa

A seconda dell’entità del servizio di flusso che si sta recuperando, è possibile utilizzare proprietà diverse per il filtraggio. Le tabelle seguenti suddividono i campi a livello principale per ogni risorsa comunemente utilizzata nei casi di utilizzo dei filtri.

**`connectionSpec`**

| Proprietà | Esempio |
| --- | --- |
| `id` | `/connectionSpecs?property=id==736873,9485095` |
| `name` | `/connectionSpecs?property=name==TestConn` |
| `providerId` | `/connectionSpecs?property=providerId==3897933` |
| `attributes.{ATTRIBUTE_NAME}` | `/connectionSpecs?property=attributes.sampleAttribute="abc"` |

{style=&quot;table-layout:auto&quot;}

**`flowSpec`**

| Proprietà | Esempio |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style=&quot;table-layout:auto&quot;}

**`connection`**

| Proprietà | Esempio |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style=&quot;table-layout:auto&quot;}

**`sourceConnection`**

| Proprietà | Esempio |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style=&quot;table-layout:auto&quot;}

**`targetConnection`**

| Proprietà | Esempio |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style=&quot;table-layout:auto&quot;}

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

{style=&quot;table-layout:auto&quot;}

**`run`**

| Proprietà | Esempio |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style=&quot;table-layout:auto&quot;}

## Passaggi successivi

Questa guida illustra come utilizzare i parametri di query `orderby` e `property` per ordinare e filtrare le risposte nell’API del servizio di flusso. Per guide dettagliate su come utilizzare l’API per i flussi di lavoro comuni in Platform, consulta le esercitazioni API contenute nella documentazione [origini](../../sources/home.md) e [destinazioni](../../destinations/home.md) .
