---
keywords: Experience Platform;home;argomenti popolari;filtro;filtrare;filtrare dati;filtrare dati;intervallo date
solution: Experience Platform
title: Filtrare i dati del catalogo utilizzando i parametri di query
description: L’API Catalog Service consente di filtrare i dati di risposta tramite l’utilizzo di parametri di query di richiesta. Una parte delle best practice per il catalogo consiste nell’utilizzare i filtri in tutte le chiamate API, in quanto riducono il carico sull’API e contribuiscono a migliorare le prestazioni complessive.
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '2121'
ht-degree: 2%

---

# Filtro [!DNL Catalog] dati tramite parametri di query

Il [!DNL Catalog Service] API consente di filtrare i dati di risposta tramite l’utilizzo di parametri di query di richiesta. Parte delle best practice per [!DNL Catalog] utilizza i filtri in tutte le chiamate API, in quanto riducono il carico sull’API e contribuiscono a migliorare le prestazioni complessive.

Questo documento illustra i metodi più comuni per filtrare [!DNL Catalog] nell&#39;API. È consigliabile fare riferimento a questo documento durante la lettura del [Guida per gli sviluppatori di cataloghi](getting-started.md) per ulteriori informazioni su come interagire con [!DNL Catalog] API. Per informazioni più generali su [!DNL Catalog Service], vedere [[!DNL Catalog] panoramica](../home.md).

## Limita oggetti restituiti

Il `limit` il parametro query limita il numero di oggetti restituiti in una risposta. [!DNL Catalog] le risposte vengono misurate automaticamente in base ai limiti configurati:

* Se un `limit` parametro non specificato, il numero massimo di oggetti per payload di risposta è 20.
* Per le query di set di dati, se `observableSchema` è richiesto utilizzando `properties` parametro di query, il numero massimo di set di dati restituiti è 20.
* Il limite globale per tutte le altre query Catalog è 100 oggetti.
* Non valido `limit` parametri (inclusi `limit=0`) genera risposte di errore a 400 livelli che descrivono intervalli corretti.
* I limiti o gli offset passati come parametri di query hanno la precedenza su quelli passati come intestazioni.

**Formato API**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di [!DNL Catalog] oggetto da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | Numero intero che indica il numero di oggetti da restituire, compreso tra 1 e 100. |

**Richiesta**

La richiesta seguente recupera un elenco di set di dati limitando la risposta a tre oggetti.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di set di dati, limitati al numero indicato dalla `limit` parametro di query.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## Limita proprietà visualizzate

Anche quando si filtra il numero di oggetti restituiti utilizzando `limit` , gli oggetti restituiti possono spesso contenere più informazioni di quelle effettivamente necessarie. Per ridurre ulteriormente il carico sul sistema, è consigliabile filtrare le risposte in modo da includere solo le proprietà necessarie.

Il `properties` Il parametro filtra gli oggetti di risposta in modo da restituire solo un set di proprietà specificate. Il parametro può essere impostato per restituire una o più proprietà.

Il `properties` il parametro accetta solo proprietà dell’oggetto di livello superiore, il che significa che per il seguente oggetto di esempio è possibile applicare filtri per `name`, `description`, e `subItem`, ma NON per `sampleKey`.

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**Formato API**

```http
GET /{OBJECT_TYPE}?properties={PROPERTY}
GET /{OBJECT_TYPE}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di [!DNL Catalog] oggetto da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | Nome di un attributo da includere nel corpo della risposta. |
| `{OBJECT_ID}` | L’identificatore univoco di uno specifico [!DNL Catalog] oggetto da recuperare. |

**Richiesta**

La richiesta seguente recupera un elenco di set di dati. L’elenco separato da virgole dei nomi di proprietà forniti sotto il `properties` Il parametro indica le proprietà da restituire nella risposta. A `limit` È incluso anche il parametro, che limita il numero di set di dati restituiti. Se la richiesta non includeva `limit` , la risposta conterrebbe un massimo di 20 oggetti.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di [!DNL Catalog] oggetti con solo le proprietà richieste visualizzate.

```json
{
    "Dataset1": {
        "name": "Dataset 1",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/bc82c518380478b59a95c63e0f843121",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "Dataset2": {},
    "Dataset3": {
        "name": {},
    },
    "Dataset4": {
        "name": "Dataset 4",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

In base alla risposta precedente, si può dedurre quanto segue:

* Se a un oggetto mancano le proprietà richieste, verranno visualizzate solo le proprietà richieste incluse. (`Dataset1`)
* Se un oggetto non include le proprietà richieste, verrà visualizzato come un oggetto vuoto. (`Dataset2`)
* Un set di dati può restituire una proprietà richiesta come oggetto vuoto se contiene la proprietà ma non esiste alcun valore. (`Dataset3`)
* In caso contrario, nel set di dati verrà visualizzato il valore completo di tutte le proprietà richieste. (`Dataset4`)

>[!NOTE]
>
>In `schemaRef` per ogni set di dati, il numero di versione indica la versione secondaria più recente dello schema. Consulta la sezione su [controllo delle versioni dello schema](../../xdm/api/getting-started.md#versioning) per ulteriori informazioni, consulta la guida dell’API XDM.

## Indice di offset iniziale dell&#39;elenco di risposte

Il `start` il parametro query sposta l’elenco di risposte in avanti di un numero specificato, utilizzando la numerazione basata su zero. Ad esempio: `start=2` determina l’offset della risposta per iniziare dal terzo oggetto elencato.

Se il `start` il parametro non è associato a un `limit` , il numero massimo di oggetti restituiti è 20.

**Formato API**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di oggetto Catalog da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | Numero intero che indica il numero di oggetti in base ai quali eseguire l&#39;offset della risposta. |

**Richiesta**

La richiesta seguente recupera un elenco di set di dati, effettuando l’offset rispetto al quinto oggetto (`start=4`) e limitazione della risposta a due set di dati restituiti (`limit=2`).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta include un oggetto JSON contenente due elementi di livello principale (`limit=2`), uno per ogni set di dati e i relativi dettagli (i dettagli sono stati sintetizzati nell’esempio). La risposta viene spostata di quattro (`start=4`), il che significa che i set di dati mostrati sono numero cinque e sei in ordine cronologico.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## Filtra per tag

Alcuni oggetti Catalog supportano l&#39;utilizzo di `tags` attributo. I tag possono allegare informazioni a un oggetto e quindi essere utilizzati in un secondo momento per recuperarlo. La scelta dei tag da utilizzare e la relativa modalità di applicazione dipendono dai processi organizzativi.

Esistono alcune limitazioni da considerare quando si utilizzano i tag:

* Gli unici oggetti Catalog che attualmente supportano i tag sono set di dati, batch e connessioni.
* I nomi dei tag sono univoci per la tua organizzazione IMS.
* I processi Adobe possono sfruttare i tag per determinati comportamenti. I nomi di questi tag hanno il prefisso &quot;adobe&quot; come standard. Pertanto, è necessario evitare questa convenzione quando si dichiarano i nomi dei tag.
* I seguenti nomi di tag sono riservati per l’utilizzo in [!DNL Experience Platform], e pertanto non può essere dichiarato come nome tag per la tua organizzazione:
   * `unifiedProfile`: questo nome di tag è riservato per i set di dati da acquisire tramite [[!DNL Real-Time Customer Profile]](../../profile/home.md).
   * `unifiedIdentity`: questo nome di tag è riservato per i set di dati da acquisire tramite [[!DNL Identity Service]](../../identity-service/home.md).

Di seguito è riportato un esempio di set di dati che contiene `tags` proprietà. I tag all’interno di tale proprietà assumono la forma di coppie chiave-valore, con ogni valore di tag visualizzato come un array contenente una singola stringa:

```json
{
    "5be1f2ecc73c1714ceba66e2": {
        "imsOrg": "{ORG_ID}",
        "tags": {
            "sampleTag": [
                "123456"
            ],
            "secondTag": [
                "sample_tag_value"
            ]
        },
        "name": "Sample Dataset",
        "description": "Same dataset containing sample data.",
        "dule": {
            "identity": [
                "I1"
            ]
        },
        "statsCache": {},
        "state": "DRAFT",
        "lastBatchId": "ca12b29612bf4052872edad59573703c",
        "lastBatchStatus": "success",
        "lastSuccessfulBatch": "ca12b29612bf4052872edad59573703c",
        "namespace": "{NAMESPACE}",
        "createdUser": "{CREATED_USER}",
        "createdClient": "{CREATED_CLIENT}",
        "updatedUser": "{UPDATED_USER}",
        "version": "1.0.0",
        "created": 1541534444286,
        "updated": 1541534444286
    }
}
```

**Formato API**

Valori per `tags` il parametro assume la forma di coppie chiave-valore, utilizzando il formato `{TAG_NAME}:{TAG_VALUE}`. È possibile fornire più coppie chiave-valore sotto forma di elenco separato da virgole. Quando vengono forniti più tag, si presume una relazione AND.

Il parametro supporta i caratteri jolly (`*`) per i valori dei tag. Ad esempio, una stringa di ricerca di `test*` restituisce qualsiasi oggetto in cui il valore del tag inizia con &quot;test&quot;. Una stringa di ricerca costituita esclusivamente da un carattere jolly può essere utilizzata per filtrare gli oggetti in base al fatto che contengano o meno un tag specifico, indipendentemente dal relativo valore.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di [!DNL Catalog] oggetto da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | Nome del tag in base al quale filtrare. |
| `{TAG_VALUE}` | Valore del tag in base al quale filtrare. Supporta caratteri jolly (`*`). |

**Richiesta**

La seguente richiesta recupera un elenco di set di dati, filtrando per un tag con un valore specifico E con il secondo tag presente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di set di dati contenenti `sampleTag` con valore &quot;123456&quot;, E `secondTag` con qualsiasi valore. A meno che non venga specificato anche un limite, la risposta contiene un massimo di 20 oggetti.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 1",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "Example tag value"
                ]
            },
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 2",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "A different tag value"
                ],
                "anotherTag": [
                    "2.0"
                ]
            },
            "dule": {},
            "statsCache": {}
    }
}
```

## Filtra per intervallo di date

Alcuni endpoint nella [!DNL Catalog] Le API dispongono di parametri di query che consentono query con intervallo, il più delle volte nel caso di date.

**Formato API**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| Parametro | Descrizione |
| --- | --- |
| `{TIMESTAMP }` | Un numero intero datetime in tempo epoca Unix. |

**Richiesta**

La richiesta seguente recupera un elenco di batch creati durante il mese di aprile 2019.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta contiene un elenco di [!DNL Catalog] oggetti che rientrano nell&#39;intervallo di date specificato. A meno che non venga specificato anche un limite, la risposta contiene un massimo di 20 oggetti.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 1",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 2",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Ordina per proprietà

Il `orderBy` il parametro query consente di ordinare (ordinare) i dati di risposta in base a un valore di proprietà specificato. Questo parametro richiede una &quot;direzione&quot; (`asc` per crescente o `desc` per decrescente), seguito da due punti (`:`) e quindi una proprietà in base alla quale ordinare i risultati. Se non viene specificata una direzione, la direzione predefinita è crescente.

È possibile specificare più proprietà di ordinamento in un elenco separato da virgole. Se la prima proprietà di ordinamento produce più oggetti che contengono lo stesso valore per tale proprietà, la seconda proprietà di ordinamento viene quindi utilizzata per ordinare ulteriormente gli oggetti corrispondenti.

Ad esempio, considera la seguente query: `orderBy=name,desc:created`. I risultati vengono ordinati in ordine crescente in base alla prima proprietà di ordinamento, `name`. Nei casi in cui più record condividono lo stesso `name` questi record corrispondenti vengono quindi ordinati in base alla seconda proprietà di ordinamento, `created`. Se nessun record restituito condivide lo stesso `name`, il `created` La proprietà non viene considerata nell’ordinamento.


**Formato API**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di oggetto Catalog da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | Nome di una proprietà in base alla quale ordinare i risultati. |

**Richiesta**

La richiesta seguente recupera un elenco di set di dati ordinati in base ai `name` proprietà. Se uno qualsiasi dei set di dati condivide lo stesso `name`, questi set di dati saranno a loro volta ordinati in base al loro `updated` proprietà in ordine decrescente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta contiene un elenco di [!DNL Catalog] oggetti ordinati in base al `orderBy` parametro. A meno che non venga specificato anche un limite, la risposta contiene un massimo di 20 oggetti.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "0405",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{ORG_ID}",
            "name": "AAM Dataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "AAM Dataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Filtra per proprietà

[!DNL Catalog] In sono disponibili due metodi per filtrare in base alla proprietà, descritti in dettaglio nelle sezioni seguenti:

* [Utilizzo di filtri semplici](#using-simple-filters): filtra in base alla corrispondenza tra una proprietà specifica e un valore specifico.
* [Utilizzo del parametro proprietà](#using-the-property-parameter): utilizza espressioni condizionali per filtrare in base all’esistenza di una proprietà o se il valore di una proprietà corrisponde, si avvicina o si confronta con un altro valore o espressione regolare specificato.

### Utilizzo di filtri semplici {#using-simple-filters}

I filtri semplici ti consentono di filtrare le risposte in base a valori di proprietà specifici. Un filtro semplice assume la forma di `{PROPERTY_NAME}={VALUE}`.

Ad esempio, la query `name=exampleName` restituisce solo oggetti con `name` contiene un valore &quot;exampleName&quot;. Al contrario, la query `name=!exampleName` restituisce solo oggetti con `name` la proprietà è **non** &quot;exampleName&quot;.

Inoltre, i filtri semplici supportano la possibilità di eseguire query per più valori per una singola proprietà. Quando vengono forniti più valori, la risposta restituisce oggetti le cui proprietà corrispondono a **qualsiasi** dei valori nell’elenco fornito. È possibile invertire una query con più valori inserendo un prefisso `!` nell&#39;elenco, restituendo solo gli oggetti il cui valore di proprietà è **non** nell’elenco fornito (ad esempio, `name=!exampleName,anotherName`).

**Formato API**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di [!DNL Catalog] oggetto da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | Nome della proprietà di cui si desidera filtrare il valore. |
| `{VALUE}` | Valore di proprietà che determina quali risultati includere (o escludere, a seconda della query). |

**Richiesta**

La seguente richiesta recupera un elenco di set di dati, filtrati per includere solo i set di dati con `name` ha un valore &quot;exampleName&quot; o &quot;otherName&quot;.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta contiene un elenco di set di dati, escludendo tutti i set di dati il cui `name` è &quot;exampleName&quot; o &quot;otherName&quot;. A meno che non venga specificato anche un limite, la risposta contiene un massimo di 20 oggetti.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "exampleName",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{ORG_ID}",
            "name": "anotherName",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

### Utilizzo di `property` parametro {#using-the-property-parameter}

Il `property` Il parametro query offre maggiore flessibilità per il filtro basato su proprietà rispetto ai filtri semplici. Oltre a filtrare in base al valore specifico di una proprietà, il `property` Il parametro può utilizzare altri operatori di confronto, ad esempio &quot;more-than&quot; (`>`) e &quot;less-than&quot; (`<`) ed espressioni regolari per filtrare in base ai valori delle proprietà. Può anche filtrare in base all’esistenza o meno di una proprietà, indipendentemente dal suo valore.

Il `property` il parametro accetta solo proprietà dell&#39;oggetto di primo livello, il che significa che per l&#39;oggetto di esempio seguente è possibile filtrare in base alla proprietà per `name`, `description`, e `subItem`, ma NON per `sampleKey`.

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**Formato API**

```http
GET /{OBJECT_TYPE}?property={CONDITION}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di [!DNL Catalog] oggetto da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | Espressione condizionale che indica la proprietà per la quale eseguire la query e come deve essere valutato il relativo valore. Di seguito sono riportati alcuni esempi. |

Il valore della proprietà `property` Il parametro supporta diversi tipi di espressioni condizionali. La tabella seguente illustra la sintassi di base delle espressioni supportate:

| Simbolo/i | Descrizione | Esempio |
| --- | --- | --- |
| (Nessuna) | Se si imposta il nome della proprietà senza operatore, verranno restituiti solo gli oggetti in cui la proprietà esiste, indipendentemente dal relativo valore. | `property=name` |
| ! | Prefisso di &quot;`!`&quot; al valore di un `property` Il parametro restituisce solo oggetti in cui la proprietà **non** esiste. | `property=!name` |
| ~ | Restituisce solo oggetti i cui valori di proprietà (stringa) corrispondono a un&#39;espressione regolare fornita dopo la tilde (`~`). | `property=name~^example` |
| == | Restituisce solo oggetti i cui valori di proprietà corrispondono esattamente alla stringa fornita dopo il simbolo di uguale a doppio (`==`). | `property=name==exampleName` |
| != | Restituisce solo gli oggetti i cui valori di proprietà eseguono **non** stringa di corrispondenza fornita dopo il simbolo non è uguale a (`!=`). | `property=name!=exampleName` |
| &lt; | Restituisce solo oggetti i cui valori di proprietà sono inferiori (ma non uguali) a una quantità dichiarata. | `property=version<1.0.0` |
| &lt;= | Restituisce solo oggetti i cui valori di proprietà sono inferiori o uguali a una quantità specificata. | `property=version<=1.0.0` |
| > | Restituisce solo oggetti i cui valori di proprietà sono maggiori (ma non uguali) di una quantità dichiarata. | `property=version>1.0.0` |
| >= | Restituisce solo oggetti i cui valori di proprietà sono maggiori o uguali a una quantità specificata. | `property=version>=1.0.0` |

>[!NOTE]
>
>Il `name` supporta l&#39;utilizzo di un carattere jolly `*`, come stringa di ricerca intera o come parte di essa. I caratteri jolly corrispondono a caratteri vuoti, in modo che la stringa di ricerca `te*st` corrisponderà al valore &quot;test&quot;. Gli asterischi vengono evitati raddoppiandoli (`**`). Un doppio asterisco in una stringa di ricerca rappresenta un singolo asterisco come stringa letterale.

**Richiesta**

La seguente richiesta restituirà tutti i set di dati con un numero di versione maggiore di 1.0.3.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta contiene un elenco di set di dati i cui numeri di versione sono maggiori di 1.0.3. A meno che non venga specificato anche un limite, la risposta contiene un massimo di 20 oggetti.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.1.2",
            "imsOrg": "{ORG_ID}",
            "name": "sampleDataset",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.6",
            "imsOrg": "{ORG_ID}",
            "name": "exampleDataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.4",
            "imsOrg": "{ORG_ID}",
            "name": "anotherDataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Combinare più filtri

Utilizzo di una e commerciale (`&`), puoi combinare più filtri in una singola richiesta. Quando vengono aggiunte condizioni aggiuntive a una richiesta, si presume una relazione AND.

**Formato API**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
