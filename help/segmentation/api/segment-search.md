---
keywords: Experience Platform;segmentazione;servizio di segmentazione;risoluzione dei problemi;API;seg;segmento;Segmento;ricerca;ricerca di segmenti;
title: Endpoint API per la ricerca dei segmenti
topic-legacy: guide
description: Nell’API del servizio di segmentazione di Adobe Experience Platform, la ricerca dei segmenti viene utilizzata per cercare i campi contenuti in diverse origini di dati e per restituirli in tempo quasi reale. Questa guida fornisce informazioni utili per comprendere meglio la funzione di ricerca dei segmenti e include chiamate API di esempio per l’esecuzione di azioni di base tramite l’API.
exl-id: bcafbed7-e4ae-49c0-a8ba-7845d8ad663b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 2%

---

# Endpoint di ricerca per segmenti

La ricerca dei segmenti viene utilizzata per cercare i campi contenuti nelle varie origini dati e per restituirli in tempo quasi reale.

Questa guida fornisce informazioni utili per comprendere meglio la funzione di ricerca dei segmenti e include chiamate API di esempio per l’esecuzione di azioni di base tramite l’API.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte dell’ API [!DNL Adobe Experience Platform Segmentation Service] . Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all&#39;API, comprese le intestazioni richieste e come leggere le chiamate API di esempio.

Oltre alle intestazioni richieste descritte nella sezione guida introduttiva, tutte le richieste all’endpoint di ricerca segmenti richiedono la seguente intestazione aggiuntiva:

- x-ups-search-version: &quot;1,0&quot;

### Ricerca in più spazi dei nomi

Questo endpoint di ricerca può essere utilizzato per la ricerca in vari namespace, restituendo un elenco di risultati del conteggio di ricerca. È possibile utilizzare più parametri, separati da e commerciale (&amp;).

**Formato API**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| Parametri | Descrizione |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obbligatorio)** Dove {SCHEMA} rappresenta il valore della classe dello schema associato agli oggetti di ricerca. Attualmente, è supportato solo `_xdm.context.segmentdefinition`. |
| `s={SEARCH_TERM}` | *(Facoltativo)* Dove {SEARCH_TERM} rappresenta una query conforme all&#39;implementazione di Microsoft della sintassi di ricerca di  [Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Se non viene specificato alcun termine di ricerca, verranno restituiti tutti i record associati a `schema.name`. Una spiegazione più dettagliata è disponibile nell&#39; [appendice](#appendix) del presente documento. |

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

Questo endpoint di ricerca può essere utilizzato per recuperare un elenco di tutti gli oggetti full text indicizzati all’interno dello spazio dei nomi specificato. È possibile utilizzare più parametri, separati da e commerciale (&amp;).

**Formato API**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parametri | Descrizione |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obbligatorio)** Se {SCHEMA} contiene il valore della classe dello schema associato agli oggetti di ricerca. Attualmente, è supportato solo `_xdm.context.segmentdefinition`. |
| `namespace={NAMESPACE}` | **(Obbligatorio)** Dove {NAMESPACE} contiene lo spazio dei nomi in cui si desidera eseguire la ricerca. |
| `s={SEARCH_TERM}` | *(Facoltativo)* Dove {SEARCH_TERM} contiene una query conforme all&#39;implementazione di Microsoft della sintassi di ricerca di  [Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Se non viene specificato alcun termine di ricerca, verranno restituiti tutti i record associati a `schema.name`. Una spiegazione più dettagliata è disponibile nell&#39; [appendice](#appendix) del presente documento. |
| `entityId={ENTITY_ID}` | *(Facoltativo)* Limita la ricerca all&#39;interno della cartella designata, specificata con {ENTITY_ID}. |
| `limit={LIMIT}` | *(Facoltativo)* Dove {LIMIT} rappresenta il numero di risultati di ricerca da restituire. Il valore predefinito è 50. |
| `page={PAGE}` | *(Facoltativo)* Dove {PAGE} rappresenta il numero di pagina utilizzato per impaginare i risultati della query cercata. Il numero della pagina inizia da **0**. |


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
| `schema.name={SCHEMA}` | **(Obbligatorio)** Se {SCHEMA} contiene il valore della classe dello schema associato agli oggetti di ricerca. Attualmente, è supportato solo `_xdm.context.segmentdefinition`. |
| `namespace={NAMESPACE}` | **(Obbligatorio)** Dove {NAMESPACE} contiene lo spazio dei nomi in cui si desidera eseguire la ricerca. |
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

Dopo aver letto questa guida hai ora una migliore comprensione del funzionamento della ricerca dei segmenti.

## Appendice {#appendix}

Le sezioni seguenti forniscono informazioni aggiuntive sul funzionamento dei termini di ricerca. Le query di ricerca vengono scritte nel modo seguente: `s={FieldName}:{SearchExpression}`. Ad esempio, per cercare un segmento denominato AAM o [!DNL Platform], utilizza la seguente query di ricerca: `s=segmentName:AAM%20OR%20Platform`.

> !![NOTE] Per le best practice, l’espressione di ricerca deve essere codificata in HTML, come nell’esempio precedente.

### Campi di ricerca {#search-fields}

Nella tabella seguente sono elencati i campi che è possibile cercare all’interno del parametro di query di ricerca.

| Nome campo | Descrizione |
| ---------- | ----------- |
| folderId | Cartella o cartelle con l&#39;ID cartella della ricerca specificata. |
| folderLocation | La posizione o le posizioni in cui si trova la cartella della ricerca specificata. |
| parentFolderId | Il segmento o la cartella con l’ID della cartella principale della ricerca specificata. |
| segmentId | Il segmento corrisponde all’ID del segmento della ricerca specificata. |
| segmentName | Il segmento corrisponde al nome del segmento della ricerca specificata. |
| segmentDescription | Il segmento corrisponde alla descrizione del segmento della ricerca specificata. |

### Espressione di ricerca {#search-expression}

Nella tabella seguente sono elencate le specifiche del funzionamento delle query di ricerca quando si utilizza l’API di ricerca segmenti.

>!![NOTE] Gli esempi seguenti sono visualizzati in un formato non HTML codificato per una maggiore chiarezza. Per le best practice, l’HTML codifica l’espressione di ricerca.

| Espressione di ricerca di esempio | Descrizione |
| ------------------------- | ----------- |
| foo | Cerca qualsiasi parola. Se la parola &quot;foo&quot; si trova in uno qualsiasi dei campi ricercabili, verranno restituiti i risultati. |
| bar e piedi | Una ricerca booleana. Questo restituisce i risultati se **sia** le parole &quot;foo&quot; che &quot;bar&quot; si trovano in uno qualsiasi dei campi ricercabili. |
| barra dei piedi O | Una ricerca booleana. Questo restituirà risultati se **o** la parola &quot;foo&quot; o la parola &quot;bar&quot; si trovano in uno qualsiasi dei campi ricercabili. |
| barra NON | Una ricerca booleana. Questo restituisce i risultati se la parola &quot;foo&quot; è trovata ma la parola &quot;bar&quot; non è trovata in nessuno dei campi ricercabili. |
| nome: bar e piedi | Una ricerca booleana. Questo restituisce i risultati se **entrambe** le parole &quot;foo&quot; e &quot;bar&quot; si trovano nel campo &quot;name&quot;. |
| run* | Ricerca con carattere jolly. L’utilizzo di un asterisco (*) corrisponde a 0 o più caratteri, ovvero restituisce risultati se il contenuto di uno dei campi ricercabili contiene una parola che inizia con &quot;run&quot;. Ad esempio, questo restituirà i risultati se compaiono le parole &quot;run&quot;, &quot;running&quot;, &quot;runner&quot; o &quot;runt&quot;. |
| cam? | Ricerca con carattere jolly. Utilizzando un punto interrogativo (?) rileva esattamente un solo carattere, il che significa che restituirà risultati se il contenuto di uno qualsiasi dei campi ricercabili inizia con &quot;cam&quot; e una lettera aggiuntiva. Ad esempio, questo restituisce i risultati se compaiono le parole &quot;camp&quot; o &quot;cams&quot;, ma non restituisce i risultati se compaiono le parole &quot;camera&quot; o &quot;campfire&quot;. |
| &quot;ombrello blu&quot; | Ricerca di frasi. Questo restituisce i risultati se il contenuto di uno qualsiasi dei campi ricercabili contiene la frase completa &quot;ombrello blu&quot;. |
| blu\~ | Una ricerca sfocata. Facoltativamente, è possibile inserire un numero compreso tra 0 e 2 dopo la tilde (~) per specificare la distanza di modifica. Ad esempio, &quot;blue\~1&quot; restituirà &quot;blue&quot;, &quot;blues&quot; o &quot;colla&quot;. La ricerca fuzzy può **solo** essere applicata a termini e non a frasi. Tuttavia, è possibile aggiungere riquadri alla fine di ogni parola in una frase. Così, per esempio, &quot;campeggio\~ in\~ the\~ estate\~&quot; avrebbe una partita su &quot;campeggio in estate&quot;. |
| &quot;hotel airport&quot;\~5 | Una ricerca di prossimità. Questo tipo di ricerca viene utilizzato per trovare termini vicini tra loro in un documento. Ad esempio, la frase `"hotel airport"~5` troverà i termini &quot;hotel&quot; e &quot;aeroporto&quot; entro 5 parole l&#39;uno dall&#39;altro in un documento. |
| `/a[0-9]+b$/` | Una ricerca con espressione regolare. Questo tipo di ricerca trova una corrispondenza basata sul contenuto tra barre &quot;/&quot;, come documentato nella classe RegExp. Ad esempio, per trovare i documenti contenenti &quot;motel&quot; o &quot;hotel&quot;, specificare `/[mh]otel/`. Le ricerche con espressione regolare vengono confrontate con parole singole. |

Per una documentazione più dettagliata sulla sintassi della query, leggi la [documentazione relativa alla sintassi della query Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax).
