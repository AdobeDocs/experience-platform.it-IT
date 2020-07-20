---
keywords: Experience Platform;segmentation;segmentation service;troubleshooting;API;seg;
solution: Adobe Experience Platform
title: Endpoint di ricerca del segmento
topic: guide
translation-type: tm+mt
source-git-commit: b3e6a6f1671a456b2ffa61139247c5799c495d92
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 2%

---


# Endpoint di ricerca del segmento

La ricerca dei segmenti viene utilizzata per cercare i campi contenuti in varie origini dati e restituirli in tempo quasi reale.

Questa guida fornisce informazioni utili per comprendere meglio la ricerca dei segmenti e include chiamate API di esempio per l&#39;esecuzione di azioni di base tramite l&#39;API.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte dell&#39; [!DNL Adobe Experience Platform Segmentation Service] API. Prima di continuare, controllate la guida [](./getting-started.md) introduttiva per informazioni importanti che dovete conoscere per effettuare correttamente le chiamate all&#39;API, comprese le intestazioni richieste e come leggere le chiamate API di esempio.

Oltre alle intestazioni richieste indicate nella sezione introduttiva, tutte le richieste all’endpoint di ricerca dei segmenti richiedono l’intestazione aggiuntiva seguente:

- x-ups-search-version: &quot;1.0&quot;

### Ricerca tra più spazi dei nomi

Questo endpoint di ricerca può essere utilizzato per eseguire ricerche in vari spazi dei nomi, restituendo un elenco dei risultati del conteggio di ricerca. È possibile utilizzare più parametri, separati da e commerciale (&amp;).

**Formato API**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| Parametri | Descrizione |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obbligatorio)** Dove {SCHEMA} rappresenta il valore della classe dello schema associato agli oggetti di ricerca. Al momento, `_xdm.context.segmentdefinition` è supportato solo. |
| `s={SEARCH_TERM}` | *(Facoltativo)* Dove {SEARCH_TERM} rappresenta una query conforme all&#39;implementazione Microsoft della sintassi [di ricerca di](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Se non viene specificato alcun termine di ricerca, `schema.name` verranno restituiti tutti i record associati. Una spiegazione più dettagliata è riportata nell&#39; [appendice](#appendix) del presente documento. |

**Richiesta**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/namespaces?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con le seguenti informazioni.

```json
{
  "namespaces": [
    {
      "namespace": "AAMTraits",
      "displayName": "AAMTraits",
      "count": 45
    },
    {
      "namespace": "AAMSegments",
      "displayName": "AAMSegment",
      "count": 10
    },
    {
      "namespace": "SegmentsAISegments",
      "displayName": "SegmentSAISegment",
      "count": 3
    }
  ],
  "totalCount": 3,
  "status": {
    "message": "Success"
  }
}
```

### Ricerca di singole entità

Questo endpoint di ricerca può essere utilizzato per recuperare un elenco di tutti gli oggetti con indicizzazione full text all&#39;interno dello spazio nomi specificato. È possibile utilizzare più parametri, separati da e commerciale (&amp;).

**Formato API**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parametri | Descrizione |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obbligatorio)** Se {SCHEMA} contiene il valore della classe dello schema associato agli oggetti di ricerca. Al momento, `_xdm.context.segmentdefinition` è supportato solo. |
| `namespace={NAMESPACE}` | **(Obbligatorio)** Dove {NAMESPACE} contiene lo spazio dei nomi in cui eseguire la ricerca. |
| `s={SEARCH_TERM}` | *(Facoltativo)* Dove {SEARCH_TERM} contiene una query conforme all&#39;implementazione di Microsoft della sintassi [di ricerca di](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Se non viene specificato alcun termine di ricerca, `schema.name` verranno restituiti tutti i record associati. Una spiegazione più dettagliata è riportata nell&#39; [appendice](#appendix) del presente documento. |
| `entityId={ENTITY_ID}` | *(Facoltativo)* Limita la ricerca all’interno della cartella designata, specificata con {ENTITY_ID}. |
| `limit={LIMIT}` | *(Facoltativo)* Dove {LIMIT} rappresenta il numero di risultati di ricerca da restituire. Il valore predefinito è 50. |
| `page={PAGE}` | *(Facoltativo)* Dove {PAGE} rappresenta il numero di pagina utilizzato per impaginare i risultati della query cercata. Il numero di pagina inizia a **0**. |


**Richiesta**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/entities?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con risultati corrispondenti alla query di ricerca.

```json
{
  "entities": [
    {
       "id": "1012667",
       "base64EncodedSourceId": "RFVGamdydHpEdy01ZTE1ZGJlZGE4YjAxMzE4YWExZWY1MzM1",
       "sourceId": "DUFjgrtzDw-5e15dbeda8b01318aa1ef533",
       "isFolder": true,
       "parentFolderId": "974139",
       "name": "aam-47995 verification (100)"
    },
    {
       "id": "14653311",
       "base64EncodedSourceId": "REVGamduLVgzdy01ZTE2ZjRhNjc1ZDZhMDE4YThhZDM3NmY1",
       "sourceId": "DEFjgn-X3w-5e16f4a675d6a018a8ad376f",
       "isFolder": false,
       "parentFolderId": "324050",
       "name": "AAM - Heavy equipment",
       "description": "AAM - Acme Equipment"
    }
 
 ],
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": 0,
    "pageSize": 10
  },
  "status": {
    "message": "Success"
  }
}
```

### Ottenere informazioni strutturali su un oggetto di ricerca

Questo endpoint di ricerca può essere utilizzato per ottenere le informazioni strutturali sull&#39;oggetto di ricerca richiesto.

**Formato API**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parametri | Descrizione |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obbligatorio)** Se {SCHEMA} contiene il valore della classe dello schema associato agli oggetti di ricerca. Al momento, `_xdm.context.segmentdefinition` è supportato solo. |
| `namespace={NAMESPACE}` | **(Obbligatorio)** Dove {NAMESPACE} contiene lo spazio dei nomi in cui eseguire la ricerca. |
| `entityId={ENTITY_ID}` | **(Obbligatorio)** L&#39;ID dell&#39;oggetto di ricerca di cui si desidera ottenere le informazioni strutturali, specificato con {ENTITY_ID}. |

**Richiesta**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/taxonomy?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments&entityId=porsche11037 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni strutturali dettagliate sull&#39;oggetto di ricerca richiesto.

```json
{
    "taxonomy": [
        {
            "id": "0",
            "base64EncodedSourceId": "RFVGZ01BLTVlNjgzMGZjMzk3YjQ1MThhYWExYTA4Zg2",
            "name": "AAMTraits for Cars",
            "parentFolderId": "root"
        },
        {
            "id": "150561",
            "base64EncodedSourceId": "RFVGamdpRk1BZy01ZTY4MzBmYzM5N2I0NTE4YWFhMWEwOGY1",
            "name": "Fast Cars",
            "parentFolderId": "carTraits"
        },
        {
            "id": "porsche11037",
            "base64EncodedSourceId": "REFGZ01CLTVlNjczMGZjMzk3YjQ1MThhZGIxYTA4Zg==",
            "name": "Porsche",
            "parentFolderId": "redCarsFolderId"
        }
    ],
    "status": {
        "message": "Success"
    }
}
```

## Passaggi successivi

Dopo aver letto questa guida è ora possibile comprendere meglio il funzionamento della ricerca segmenti.

## Appendice {#appendix}

Le sezioni seguenti forniscono informazioni aggiuntive sul funzionamento dei termini di ricerca. Le query di ricerca vengono scritte nel modo seguente: `s={FieldName}:{SearchExpression}`. Per cercare, ad esempio, un segmento denominato AAM o Platform, si utilizza la seguente query di ricerca: `s=segmentName:AAM%20OR%20Platform`.

> !![NOTE] Per le procedure ottimali, l&#39;espressione di ricerca deve essere codificata in HTML, come nell&#39;esempio riportato sopra.

### Campi di ricerca {#search-fields}

Nella tabella seguente sono elencati i campi che è possibile cercare all’interno del parametro della query di ricerca.

| Nome campo | Descrizione |
| ---------- | ----------- |
| folderId | Cartella o cartelle con l’ID cartella della ricerca specificata. |
| folderLocation | Il percorso o i percorsi in cui si trova la cartella della ricerca specificata. |
| parentFolderId | Segmento o cartella con l’ID cartella principale della ricerca specificata. |
| segmentId | Il segmento corrisponde all’ID del segmento della ricerca specificata. |
| segmentName | Il segmento corrisponde al nome del segmento della ricerca specificata. |
| segmentDescription | Il segmento corrisponde alla descrizione del segmento della ricerca specificata. |

### Espressione di ricerca {#search-expression}

Nella tabella seguente sono elencate le specifiche del funzionamento delle query di ricerca quando si utilizza l&#39;API di ricerca segmenti.

>!![NOTE] Gli esempi seguenti sono mostrati in un formato non codificato HTML per una maggiore chiarezza. Per le procedure ottimali, l&#39;HTML codifica l&#39;espressione di ricerca.

| Esempio di espressione di ricerca | Descrizione |
| ------------------------- | ----------- |
| foo | Cerca qualsiasi parola. Questo restituisce dei risultati se la parola &quot;foo&quot; è presente in uno qualsiasi dei campi ricercabili. |
| foo AND bar | Una ricerca booleana. Questo restituisce dei risultati se **entrambe** le parole &quot;foo&quot; e &quot;bar&quot; sono presenti in uno dei campi ricercabili. |
| barra per utenti o | Una ricerca booleana. Questo restituisce dei risultati se **la parola &quot;foo&quot; o la parola &quot;bar&quot; si trovano** in uno qualsiasi dei campi ricercabili. |
| barra NON | Una ricerca booleana. Questo restituisce dei risultati se la parola &quot;foo&quot; è trovata ma la parola &quot;bar&quot; non è trovata in nessuno dei campi ricercabili. |
| name: foo AND bar | Una ricerca booleana. Questo restituisce risultati se **entrambe** le parole &quot;foo&quot; e &quot;bar&quot; sono presenti nel campo &quot;name&quot;. |
| run* | Ricerca con caratteri jolly. L&#39;utilizzo di un asterisco (*) corrisponde a 0 o più caratteri, il che significa che restituirà risultati se il contenuto di uno qualsiasi dei campi ricercabili contiene una parola che inizia con &quot;run&quot;. Ad esempio, questo restituisce i risultati se vengono visualizzate le parole &quot;run&quot;, &quot;run&quot;, &quot;runner&quot; o &quot;runt&quot;. |
| cam? | Ricerca con caratteri jolly. Utilizzo di un punto interrogativo (?) rileva solo un carattere, il che significa che restituirà risultati se il contenuto di uno qualsiasi dei campi ricercabili inizia con &quot;cam&quot; e una lettera aggiuntiva. Ad esempio, questo restituisce i risultati se vengono visualizzate le parole &quot;campeggio&quot; o &quot;cams&quot;, ma non restituisce i risultati se vengono visualizzate le parole &quot;camera&quot; o &quot;fuoco&quot;. |
| &quot;ombrello blu&quot; | Una ricerca di frasi. Questo restituisce dei risultati se il contenuto di uno qualsiasi dei campi ricercabili contiene la frase completa &quot;ombrello blu&quot;. |
| blue\~ | Una ricerca sfocata. Facoltativamente, potete inserire un numero compreso tra 0 e 2 dopo la tilde (~) per specificare la distanza di modifica. Ad esempio, &quot;blue\~1&quot; restituisce &quot;blue&quot;, &quot;blues&quot; o &quot;colla&quot;. La ricerca Fuzzy può essere applicata **solo** ai termini, non alle frasi. Tuttavia, è possibile aggiungere piastrelle alla fine di ogni parola di una frase. Così, ad esempio, &quot;campeggio\~ in\~ la\~ estate\~&quot; avrebbe giocato con &quot;campeggio in estate&quot;. |
| &quot;hotel Airport&quot;\~5 | Una ricerca di prossimità. Questo tipo di ricerca viene utilizzato per trovare i termini che si trovano l&#39;uno accanto all&#39;altro in un documento. Ad esempio, la frase `"hotel airport"~5` troverà i termini &quot;hotel&quot; e &quot;aeroporto&quot; entro 5 parole l&#39;una dall&#39;altra in un documento. |
| `/a[0-9]+b$/` | Una ricerca con espressione regolare. Questo tipo di ricerca trova una corrispondenza basata sul contenuto tra le barre &quot;/&quot;, come documentato nella classe RegExp. Ad esempio, per trovare documenti contenenti &quot;motel&quot; o &quot;hotel&quot;, specificare `/[mh]otel/`. Le ricerche di espressioni regolari vengono confrontate con singole parole. |

Per una documentazione più dettagliata sulla sintassi della query, consulta la documentazione [sulla sintassi della query](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene.
