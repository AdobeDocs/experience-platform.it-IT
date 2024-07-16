---
title: Ordinamento e filtraggio delle risposte nell’API del servizio Flusso
description: Questa esercitazione descrive la sintassi per l’ordinamento e il filtraggio utilizzando i parametri di query nell’API del servizio Flusso, inclusi alcuni casi d’uso avanzati.
exl-id: 029c3199-946e-4f89-ba7a-dac50cc40c09
source-git-commit: c7ff379b260edeef03f8b47f932ce9040eef3be2
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 2%

---

# Ordinamento e filtraggio delle risposte nell’API del servizio Flusso

Quando si eseguono richieste di elenco (GET) nell&#39;API [Flow Service](https://www.adobe.io/experience-platform-apis/references/flow-service/), è possibile utilizzare i parametri di query per ordinare e filtrare le risposte. Questa guida fornisce un riferimento su come utilizzare questi parametri per diversi casi d’uso.

## Ordinamento

È possibile ordinare le risposte utilizzando un parametro di query `orderby`. Le seguenti risorse possono essere ordinate nell’API:

* [Connessioni](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [connessioni Source](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [Connessioni di destinazione](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [Flussi](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [Esecuzioni](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

Per utilizzare il parametro, è necessario impostarne il valore sulla proprietà specifica in base alla quale si desidera ordinare (ad esempio, `?orderby=name`). È possibile anteporre al valore un segno più (`+`) per l&#39;ordine crescente o un segno meno (`-`) per l&#39;ordine decrescente. Se non viene fornito alcun prefisso di ordinamento, l’elenco viene ordinato in ordine crescente per impostazione predefinita.

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

È inoltre possibile combinare un parametro di ordinamento con un parametro di filtro utilizzando il simbolo &quot;and&quot; (`&`).

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## Filtro

È possibile filtrare le risposte utilizzando un parametro `property` con un&#39;espressione chiave-valore. Ad esempio, `?property=id==12345` restituisce solo le risorse la cui proprietà `id` è esattamente uguale a `12345`.

Il filtro può essere applicato in modo generico a qualsiasi proprietà in un’entità, purché sia noto il percorso valido di tale proprietà.

>[!NOTE]
>
>Se una proprietà è nidificata all&#39;interno di un elemento di matrice, è necessario aggiungere parentesi quadre (`[]`) alla matrice nel percorso. Per esempi, consulta la sezione sul filtro [per le proprietà dell&#39;array](#arrays).

**Restituire tutte le connessioni di origine in cui il nome della tabella di origine è `lead`:**

```http
GET /sourceConnections?property=params.tableName==lead
```

**Restituisci tutti i flussi per un ID segmento specifico:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### Unione di filtri

È possibile includere più filtri `property` in una query purché siano separati da caratteri &quot;e&quot; (`&`). Quando si combinano i filtri si assume una relazione AND, il che significa che un’entità deve soddisfare tutti i filtri per essere inclusa nella risposta.

**Restituisci tutti i flussi abilitati per un ID segmento:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### Filtraggio delle proprietà dell’array {#arrays}

È possibile filtrare in base alle proprietà degli elementi all&#39;interno degli array aggiungendo `[]` al nome della proprietà dell&#39;array.

**Flussi di ritorno associati a connessioni di origine specifiche:**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**Flussi di ritorno con una trasformazione contenente un ID di valore selettore specifico:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**Restituire le connessioni di origine con una colonna con un valore `name` specifico:**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**Cercare l&#39;ID esecuzione flusso per una destinazione filtrando l&#39;ID segmento:**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

Qualsiasi query di filtro può essere aggiunta con il parametro di query `count` con un valore di `true` per restituire il conteggio dei risultati. La risposta API contiene una proprietà `count` il cui valore rappresenta il numero totale di elementi filtrati. Gli elementi filtrati effettivi non vengono restituiti in questa chiamata.

**Restituisce il numero di flussi abilitati nel sistema:**

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

Leggi questa sezione per alcuni esempi specifici su come utilizzare i filtri e l’ordinamento per restituire informazioni su determinati connettori o per assistenza nei problemi di debug. Adobe Se ci sono altri casi d&#39;uso che desideri aggiungere, utilizza le **[!UICONTROL opzioni di feedback dettagliate]** nella pagina per inviare una richiesta.

**Filtro per restituire solo le connessioni a una determinata destinazione**

Puoi utilizzare i filtri per restituire connessioni solo a determinate destinazioni. Innanzitutto, esegui una query sull&#39;endpoint `connectionSpecs` come segue:

```http
GET /connectionSpecs
```

Quindi, cercare `connectionSpec` desiderato esaminando il parametro `name`. Ad esempio, cerca Amazon Ads, Pega, o SFTP e così via nel parametro `name`. Il `id` corrispondente è il `connectionSpec` in base al quale è possibile eseguire una ricerca nella chiamata API successiva.

Ad esempio, filtra le destinazioni per restituire solo le connessioni esistenti alle connessioni Amazon S3:

```http
GET /connections?property=connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**Filtro per restituire flussi di dati solo alle destinazioni**

Quando si esegue una query sull&#39;endpoint `/flows`, invece di restituire tutti i flussi di dati di origine e destinazione, è possibile utilizzare un filtro per restituire solo i flussi di dati alle destinazioni. A tale scopo, utilizzare `isDestinationFlow` come parametro di query, come riportato di seguito:

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

**Filtro per restituire solo flussi di dati non riusciti**

A scopo di debug, puoi filtrare e visualizzare tutti i flussi di dati non riusciti eseguiti per un determinato flusso di dati di origine o di destinazione, come indicato di seguito:

```http
GET /runs?property=flowId==<flow-id>&property=metrics.statusSummary.status==Failed
```

## Passaggi successivi

Questa guida illustra come utilizzare i parametri di query `orderby` e `property` per ordinare e filtrare le risposte nell&#39;API del servizio Flusso. Per guide dettagliate sull&#39;utilizzo dell&#39;API per i flussi di lavoro comuni in Platform, consulta i tutorial sull&#39;API contenuti nella documentazione di [sources](../../sources/home.md) e [destinations](../../destinations/home.md).
