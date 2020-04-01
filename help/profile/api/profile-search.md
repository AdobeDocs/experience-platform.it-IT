---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guida per lo sviluppatore di API profilo cliente in tempo reale
topic: guide
translation-type: tm+mt
source-git-commit: 95e002c60389ca7e4c1dcf32bbcf6f552cd55d95

---


# Ricerca profilo

La ricerca del profilo viene utilizzata per cercare e indicizzare i campi configurabili contenuti in varie origini dati e restituirli in tempo quasi reale.

Questa guida fornisce informazioni utili per comprendere meglio la ricerca dei profili e include chiamate API di esempio per l&#39;esecuzione di azioni di base tramite l&#39;API.

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte dell&#39;API Profilo cliente in tempo reale. Prima di continuare, consulta la guida [per lo sviluppatore del profilo cliente in tempo](getting-started.md)reale.

In particolare, la sezione [](getting-started.md) introduttiva della guida per gli sviluppatori di profili include collegamenti a argomenti correlati, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni richieste necessarie per eseguire correttamente chiamate a qualsiasi API della piattaforma Experience.

### Ottieni risultati di ricerca

L’endpoint di ricerca può essere utilizzato per ottenere risultati di ricerca basati sui valori del `schema.name` parametro richiesto e su ulteriori parametri di query facoltativi. È possibile utilizzare più parametri, separati da e commerciale (&amp;).

**Formato API**

```http
GET /search?{QUERY_PARAMETERS}
```

| Parametro | Descrizione |
|---|---|
| `schema.name` | **Obbligatorio.** Il nome della classe dello schema contenente il contenuto per il quale eseguire la ricerca, scritto in formato notazione punto. Al momento, `schema.name=_xdm.context.segmentdefinition` è supportato solo. |
| `limit` | Numero di risultati di ricerca da restituire. Il valore predefinito è 50. |
| `page` | Numero di pagina utilizzato per impaginare i risultati della query cercata. |
| `s` | Query conforme all&#39;implementazione Microsoft della sintassi [di ricerca di](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Se non viene specificato alcun termine di ricerca, `schema.name` verranno restituiti tutti i record associati. Una spiegazione più dettagliata è disponibile nella sezione Parametri [di](#search-parameters) ricerca di questo documento. |
| `namespace` | Identifica i dati effettivi da cercare nella classe dello schema specificata nel `schema.name` parametro. |
| `organization.type` | Determina il contenuto della risposta. Il formato del contenuto restituito dipende dai valori utilizzati in `schema.name`. Ad `_xdm.context.segmentdefinition`esempio, i valori validi sono `hierarchy` o `hierarchyinfo`. |
| `organization.id` | **Obbligatorio se`organization.type`è specificato.** Fornisce la gerarchia dell&#39;organizzazione specificata quando viene utilizzata con la gerarchia `organization.type` . |

**Richiesta**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un array di oggetti che soddisfano i criteri di ricerca. In questo esempio, poiché il `schema.name` parametro era `_xdm.context.segmentdefinition`, viene restituito un elenco di definizioni di segmento.

```json
{
  "aam-hierarchy": {
    "_xdm.context.segmentdefinition": [
      {
        "isFolder": true,
        "id": "100023",
        "name": "Segment Definition 1",
        "description": "Sample description.",
        "parentFolderId": "99970"
      },
      {
        "isFolder": false,
        "id": "1000028",
        "name": "Segment Definition 2",
        "description": "Sample description.",
        "parentFolderId": "103584"
      }
    ]
  },
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": "1",
    "pageSize": 2,
    "limit": 2
  }
}
```

### Creare richieste di provisioning

Potete creare richieste di provisioning per abilitare la ricerca del profilo sugli schemi effettuando una richiesta POST all&#39; `/search/provisioning/component/init` endpoint.

**Richiesta**

>[!CAUTION]
>Questa richiesta POST non contiene un payload e pertanto non richiede un&#39;intestazione Content-Type. Inoltre, non esiste un&#39;intestazione sandbox perché tutti i dati vengono inviati in una sandbox globale.

```shell
curl -X POST \
    https://platform.adobe.io/data/core/ups/search/provisioning/component/init \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' 
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e il messaggio seguente:

```plaintext
The request has been fulfilled and resulted in a new resource being created.
```

### Gestione delle richieste di configurazione

L&#39;endpoint di configurazione può essere utilizzato per impostare indici, indici e connessioni di origine dati corretti per una nuova organizzazione IMS. Per gestire le richieste di configurazione sono necessarie due proprietà: `databaseName` e `containerName`.

`databaseName` rappresenta il nome del database del profilo per l&#39;organizzazione che verrà configurata.

`containerName` rappresenta il nome del contenitore popolato da un connettore dati, che è ciò che viene letto durante la configurazione. Nella richiesta POST sono disponibili due valori per `containerName`, uno o entrambi:
- `_xdm.content.segmentdefinition`
- `_experience.audiencemanager.segmentfolder`

### Creare una richiesta di configurazione

La seguente chiamata API genera l’origine dati, l’indicizzatore e l’indice richiesti in base ai parametri forniti nel payload della richiesta.

**Formato API**

```http
POST /search/configure
```

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) e un messaggio in testo normale.

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

### Eliminare una richiesta di configurazione

La seguente chiamata API rimuove le voci di indice corrispondenti ed elimina l’indicizzatore e l’origine dati in base ai parametri forniti nel payload della richiesta.

>[!NOTE]
>L&#39;indice stesso non verrà eliminato, in quanto è una risorsa condivisa.

**Formato API**

```http
DELETE /search/configure
```

**Richiesta**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) e un messaggio in testo normale.

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

## Passaggi successivi

Dopo aver letto questa guida hai ora una migliore comprensione del funzionamento della ricerca in tempo reale sul profilo cliente. Per maggiori informazioni sul profilo cliente in tempo reale, consulta la panoramica [sul profilo cliente in tempo](../home.md)reale. Per ulteriori informazioni sulla segmentazione, consulta la panoramica sulla [segmentazione](../../segmentation/home.md).

## Appendice {#appendix}

### Parametri di ricerca {#search-parameters}

La tabella seguente elenca le specifiche di funzionamento del parametro di ricerca quando si utilizza l&#39;API di ricerca.

| Query di ricerca | Descrizione |
|------------ | -----------|
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
