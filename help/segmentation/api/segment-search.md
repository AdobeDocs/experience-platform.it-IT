---
title: Endpoint API di ricerca segmenti
description: Nell’API del servizio di segmentazione di Adobe Experience Platform, la ricerca dei segmenti viene utilizzata per cercare i campi contenuti in diverse origini dati e restituirli quasi in tempo reale. Questa guida fornisce informazioni utili per comprendere meglio la Ricerca di segmenti e include chiamate API di esempio per eseguire azioni di base utilizzando l’API.
role: Developer
exl-id: bcafbed7-e4ae-49c0-a8ba-7845d8ad663b
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 2%

---

# Endpoint di ricerca del segmento

La ricerca dei segmenti viene utilizzata per cercare i campi contenuti in diverse origini dati e restituirli quasi in tempo reale.

Questa guida fornisce informazioni utili per comprendere meglio la Ricerca di segmenti e include chiamate API di esempio per eseguire azioni di base utilizzando l’API.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte dell&#39;API [!DNL Adobe Experience Platform Segmentation Service]. Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, incluse le intestazioni richieste e la lettura delle chiamate API di esempio.

Oltre alle intestazioni richieste descritte nella sezione guida introduttiva, tutte le richieste all’endpoint di ricerca dei segmenti richiedono la seguente intestazione aggiuntiva:

- x-ups-search-version: &quot;1.0&quot;

### Ricerca in più spazi dei nomi

Questo endpoint di ricerca può essere utilizzato per eseguire ricerche in vari spazi dei nomi, restituendo un elenco di risultati del conteggio delle ricerche. È possibile utilizzare più parametri, separati da e commerciali (&amp;).

**Formato API**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| Elemento “parameters” | Descrizione |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obbligatorio)** Dove {SCHEMA} rappresenta il valore della classe dello schema associato agli oggetti di ricerca. Attualmente, è supportato solo `_xdm.context.segmentdefinition`. |
| `s={SEARCH_TERM}` | *(Facoltativo)* Dove {SEARCH_TERM} rappresenta una query conforme all&#39;implementazione di Microsoft della sintassi di ricerca di [Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Se non viene specificato alcun termine di ricerca, verranno restituiti tutti i record associati a `schema.name`. Una spiegazione più dettagliata è disponibile nell&#39;[appendice](#appendix) di questo documento. |

**Richiesta**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/namespaces?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con le seguenti informazioni.

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

Questo endpoint di ricerca può essere utilizzato per recuperare una lista di tutti gli oggetti indicizzati full-text all’interno dello spazio dei nomi specificato. È possibile utilizzare più parametri, separati da e commerciali (&amp;).

**Formato API**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Elemento “parameters” | Descrizione |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obbligatorio)** Dove {SCHEMA} contiene il valore della classe dello schema associato agli oggetti di ricerca. Attualmente, è supportato solo `_xdm.context.segmentdefinition`. |
| `namespace={NAMESPACE}` | **(Obbligatorio)** Dove {NAMESPACE} contiene lo spazio dei nomi in cui si desidera eseguire la ricerca. |
| `s={SEARCH_TERM}` | *(Facoltativo)* Dove {SEARCH_TERM} contiene una query conforme all&#39;implementazione di Microsoft della [sintassi di ricerca Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Se non viene specificato alcun termine di ricerca, verranno restituiti tutti i record associati a `schema.name`. Una spiegazione più dettagliata è disponibile nell&#39;[appendice](#appendix) di questo documento. |
| `entityId={ENTITY_ID}` | *(Facoltativo)* Limita la ricerca alla cartella specificata, specificata con {ENTITY_ID}. |
| `limit={LIMIT}` | *(Facoltativo)* Dove {LIMIT} rappresenta il numero di risultati di ricerca da restituire. Il valore predefinito è 50. |
| `page={PAGE}` | *(Facoltativo)* Dove {PAGE} rappresenta il numero di pagina utilizzato per impaginare i risultati della query cercata. Il numero di pagina inizia da **0**. |


**Richiesta**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/entities?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 e i risultati corrispondono alla query di ricerca.

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

Questo endpoint di ricerca può essere utilizzato per ottenere informazioni strutturali sull&#39;oggetto di ricerca richiesto.

**Formato API**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Elemento “parameters” | Descrizione |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obbligatorio)** Dove {SCHEMA} contiene il valore della classe dello schema associato agli oggetti di ricerca. Attualmente, è supportato solo `_xdm.context.segmentdefinition`. |
| `namespace={NAMESPACE}` | **(Obbligatorio)** Dove {NAMESPACE} contiene lo spazio dei nomi in cui si desidera eseguire la ricerca. |
| `entityId={ENTITY_ID}` | **(Obbligatorio)** ID dell&#39;oggetto di ricerca di cui si desidera ottenere le informazioni strutturali, specificato con {ENTITY_ID}. |

**Richiesta**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/taxonomy?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments&entityId=porsche11037 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni strutturali dettagliate sull’oggetto di ricerca richiesto.

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

Dopo aver letto questa guida hai acquisito una migliore comprensione del funzionamento della ricerca per segmenti.

## Appendice {#appendix}

Le sezioni seguenti forniscono informazioni aggiuntive sul funzionamento dei termini di ricerca. Le query di ricerca sono scritte nel modo seguente: `s={FieldName}:{SearchExpression}`. Ad esempio, per cercare una definizione di segmento denominata AAM o [!DNL Platform], è necessario utilizzare la seguente query di ricerca: `s=segmentName:AAM%20OR%20Platform`.

>  Per le best practice, l&#39;espressione di ricerca deve essere codificata come HTML, come nell&#39;esempio precedente.

### Cerca campo {#search-fields}

Nella tabella seguente sono elencati i campi in cui è possibile eseguire ricerche nel parametro della query di ricerca.

| Nome campo | Descrizione |
| ---------- | ----------- |
| folderId | Cartella o cartelle con l&#39;ID cartella della ricerca specificata. |
| folderLocation | Il percorso o i percorsi in cui si trova la cartella della ricerca specificata. |
| parentFolderId | La definizione del segmento o la cartella che ha l’ID della cartella principale della ricerca specificata. |
| segmentId | La definizione del segmento che corrisponde all’ID del segmento della ricerca specificata. |
| segmentName | La definizione del segmento che corrisponde al nome del segmento della ricerca specificata. |
| segmentDescription | La definizione del segmento che corrisponde alla descrizione del segmento della ricerca specificata. |

### Espressione di ricerca {#search-expression}

Nella tabella seguente sono elencate le specifiche del funzionamento delle query di ricerca quando si utilizza l’API di ricerca dei segmenti.

>  Gli esempi seguenti vengono visualizzati in un formato non codificato da HTML per una maggiore chiarezza. Per best practice, HTML codifica l’espressione di ricerca.

| Espressione di ricerca di esempio | Descrizione |
| ------------------------- | ----------- |
| foo | Cerca qualsiasi parola. Questo restituirà i risultati se la parola &quot;foo&quot; si trova in uno qualsiasi dei campi ricercabili. |
| bar Foo AND | Una ricerca booleana. Questo restituirà risultati se **entrambi** le parole &quot;foo&quot; e &quot;bar&quot; si trovano in uno qualsiasi dei campi ricercabili. |
| barra o foo | Una ricerca booleana. Questo restituirà risultati se **o** la parola &quot;foo&quot; o la parola &quot;bar&quot; si trovano in uno qualsiasi dei campi ricercabili. |
| foo NOT bar | Una ricerca booleana. Questo restituirà i risultati se la parola &quot;foo&quot; viene trovata ma la parola &quot;bar&quot; non è trovata in nessuno dei campi ricercabili. |
| nome: foo AND bar | Una ricerca booleana. Questo restituirà i risultati se **entrambi** le parole &quot;foo&quot; e &quot;bar&quot; si trovano nel campo &quot;name&quot;. |
| esecuzione* | Ricerca con caratteri jolly. L’asterisco (*) corrisponde a 0 o più caratteri, il che significa che restituirà risultati se il contenuto di uno dei campi ricercabili contiene una parola che inizia con &quot;esegui&quot;. Ad esempio, questo restituirà i risultati se vengono visualizzate le parole &quot;run&quot;, &quot;running&quot;, &quot;runner&quot; o &quot;runt&quot;. |
| Camma? | Ricerca con caratteri jolly. Utilizzo di un punto interrogativo (?) corrisponde esattamente a un carattere, il che significa che restituirà risultati se il contenuto di uno qualsiasi dei campi ricercabili inizia con &quot;cam&quot; e una lettera aggiuntiva. Ad esempio, questo restituirà i risultati se vengono visualizzate le parole &quot;camp&quot; o &quot;cams&quot;, ma non i risultati se vengono visualizzate le parole &quot;camera&quot; o &quot;campfire&quot;. |
| &quot;ombrello blu&quot; | Ricerca di frasi. Questo restituirà i risultati se il contenuto di uno qualsiasi dei campi ricercabili contiene la frase completa &quot;ombrello blu&quot;. |
| blu\~ | Una ricerca confusa. In alternativa, è possibile inserire un numero compreso tra 0 e 2 dopo la tilde (~) per specificare la distanza di modifica. Ad esempio, &quot;blue\~1&quot; restituirà &quot;blue&quot;, &quot;blues&quot; o &quot;glue&quot;. La ricerca fuzzy può essere applicata **solo** ai termini, non alle frasi. Tuttavia, è possibile aggiungere le tessere alla fine di ogni parola di una frase. Ad esempio, &quot;camping\~ in\~ the\~ summer\~&quot; corrisponderebbe a &quot;camping in estate&quot;. |
| &quot;aeroporto dell&#39;hotel&quot;\~5 | Una ricerca di prossimità. Questo tipo di ricerca viene utilizzato per trovare termini vicini tra loro in un documento. Ad esempio, la frase `"hotel airport"~5` troverà i termini &quot;hotel&quot; e &quot;aeroporto&quot; entro 5 parole l&#39;uno dall&#39;altro in un documento. |
| `/a[0-9]+b$/` | Ricerca di espressioni regolari. Questo tipo di ricerca trova una corrispondenza basata sul contenuto tra barre &quot;/&quot;, come documentato nella classe RegExp. Ad esempio, per trovare documenti contenenti &quot;motel&quot; o &quot;hotel&quot;, specificare `/[mh]otel/`. Le ricerche di espressioni regolari vengono associate a singole parole. |

Per una documentazione più dettagliata sulla sintassi della query, leggere la [documentazione sulla sintassi della query Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax).
