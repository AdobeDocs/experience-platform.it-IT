---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Filtra i dati del catalogo utilizzando i parametri di query
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '2033'
ht-degree: 1%

---


# Filtra [!DNL Catalog] i dati utilizzando i parametri di query

L&#39; [!DNL Catalog Service] API consente di filtrare i dati di risposta mediante l&#39;uso di parametri di query di richiesta. Parte delle best practice per [!DNL Catalog] è utilizzare i filtri in tutte le chiamate API, in quanto riducono il carico sull&#39;API e contribuiscono a migliorare le prestazioni complessive.

Questo documento illustra i metodi più comuni per filtrare [!DNL Catalog] gli oggetti nell&#39;API. È consigliabile fare riferimento a questo documento durante la lettura della guida [per gli sviluppatori di](getting-started.md) Catalog per ulteriori informazioni su come interagire con l&#39; [!DNL Catalog] API. Per informazioni generali su [!DNL Catalog Service]questo argomento, consultate la panoramica [](../home.md)Catalogo.

## Limite oggetti restituiti

Il parametro `limit` query vincola il numero di oggetti restituiti in una risposta. [!DNL Catalog] le risposte vengono misurate automaticamente in base ai limiti configurati:

* Se non viene specificato un `limit` parametro, il numero massimo di oggetti per payload di risposta è 20.
* Per le query dataset, se `observableSchema` viene richiesto utilizzando il parametro `properties` query, il numero massimo di dataset restituito è 20.
* Il limite globale per tutte le altre query Catalog è di 100 oggetti.
* I `limit` parametri (inclusi `limit=0`) non validi generano risposte di errore a 400 livelli che delineano intervalli corretti.
* I limiti o gli offset passati come parametri di query hanno la precedenza su quelli passati come intestazioni.

**Formato API**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di [!DNL Catalog] oggetto da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | Un numero intero che indica il numero di oggetti da restituire, compreso tra 1 e 100. |

**Richiesta**

La richiesta seguente recupera un elenco di set di dati limitando la risposta a tre oggetti.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di set di dati, limitato al numero indicato dal parametro della `limit` query.

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

## Limite proprietà visualizzate

Anche quando si filtra il numero di oggetti restituiti utilizzando il `limit` parametro, gli oggetti restituiti possono spesso contenere più informazioni di quelle effettivamente necessarie. Per ridurre ulteriormente il carico sul sistema, è consigliabile filtrare le risposte in modo da includere solo le proprietà necessarie.

Il `properties` parametro filtra gli oggetti di risposta per restituire solo un set di proprietà specificate. Il parametro può essere impostato per restituire una o più proprietà.

Il `properties` parametro accetta solo proprietà dell&#39;oggetto di livello principale, il che significa che per il seguente oggetto di esempio è possibile applicare filtri per `name`, `description`e `subItem`, ma NON per `sampleKey`.

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
| `{OBJECT_TYPE}` | Tipo di [!DNL Catalog] oggetto da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | Il nome di un attributo da includere nel corpo della risposta. |
| `{OBJECT_ID}` | Identificatore univoco di un [!DNL Catalog] oggetto specifico che si sta recuperando. |

**Richiesta**

La richiesta seguente recupera un elenco di set di dati. L&#39;elenco separato da virgole dei nomi delle proprietà forniti sotto il `properties` parametro indica le proprietà da restituire nella risposta. È incluso anche un `limit` parametro, che limita il numero di set di dati restituiti. Se la richiesta non includeva un `limit` parametro, la risposta conterrebbe un massimo di 20 oggetti.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di [!DNL Catalog] oggetti con solo le proprietà richieste visualizzate.

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

In base alla risposta di cui sopra, si può dedurre quanto segue:

* Se a un oggetto mancano le proprietà richieste, verranno mostrate solo le proprietà richieste che non include. (`Dataset1`)
* Se un oggetto non include alcuna delle proprietà richieste, verrà visualizzato come un oggetto vuoto. (`Dataset2`)
* Un dataset può restituire una proprietà richiesta come oggetto vuoto se contiene la proprietà ma non esiste alcun valore. (`Dataset3`)
* In caso contrario, il set di dati visualizzerà il valore completo di tutte le proprietà richieste. (`Dataset4`)

## Offset indice iniziale dell&#39;elenco di risposte

Il parametro `start` query consente di scostare l’elenco di risposte in avanti di un numero specificato, utilizzando la numerazione basata su zero. Ad esempio, `start=2` scosterebbe la risposta per iniziare sul terzo oggetto elencato.

Se il `start` parametro non è associato a un `limit` parametro, il numero massimo di oggetti restituiti è 20.

**Formato API**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di oggetto Catalog da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | Un numero intero che indica il numero di oggetti da cui scostare la risposta. |

**Richiesta**

La richiesta seguente recupera un elenco di set di dati, eseguendo l&#39;offset al quinto oggetto (`start=4`) e limitando la risposta a due set di dati restituiti (`limit=2`).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta include un oggetto JSON contenente due elementi di primo livello (`limit=2`), uno per ogni set di dati e i relativi dettagli (i dettagli sono stati sintetizzati nell&#39;esempio). La risposta viene modificata di quattro (`start=4`), ossia i set di dati mostrati sono i numeri cinque e sei in ordine cronologico.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## Filtrare per tag

Alcuni oggetti Catalog supportano l&#39;utilizzo di un `tags` attributo. I tag possono allegare informazioni a un oggetto e successivamente essere utilizzati per recuperarlo. La scelta dei tag da utilizzare e di come applicarli dipende dai processi aziendali.

L&#39;uso dei tag presenta alcune limitazioni:

* Gli unici oggetti Catalog che al momento supportano i tag sono insiemi di dati, batch e connessioni.
* I nomi dei tag sono univoci per l’organizzazione IMS.
*  processi di Adobe possono utilizzare i tag per determinati comportamenti. I nomi di questi tag hanno il prefisso &quot;adobe&quot; come standard. Pertanto, è consigliabile evitare questa convenzione quando si dichiarano i nomi dei tag.
* I seguenti nomi di tag sono riservati all’uso in tutta [!DNL Experience Platform]l’organizzazione e pertanto non possono essere dichiarati come nome di tag:
   * `unifiedProfile`: Questo nome di tag è riservato ai set di dati da cui eseguire l&#39;assimilazione [!DNL Real-time Customer Profile](../../profile/home.md).
   * `unifiedIdentity`: Questo nome di tag è riservato ai set di dati da cui eseguire l&#39;assimilazione [!DNL Identity Service](../../identity-service/home.md).

Di seguito è riportato un esempio di un set di dati contenente una `tags` proprietà. I tag all&#39;interno di tale proprietà si presentano sotto forma di coppie chiave-valore, con ciascun valore di tag che viene visualizzato come una matrice contenente una singola stringa:

```json
{
    "5be1f2ecc73c1714ceba66e2": {
        "imsOrg": "{IMS_ORG}",
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

I valori per il `tags` parametro assumono la forma di coppie chiave-valore, utilizzando il formato `{TAG_NAME}:{TAG_VALUE}`. Più coppie chiave-valore possono essere fornite sotto forma di elenco separato da virgole. Quando vengono forniti più tag, si assume una relazione AND.

Il parametro supporta i caratteri jolly (`*`) per i valori dei tag. Ad esempio, una stringa di ricerca `test*` restituisce qualsiasi oggetto in cui il valore del tag inizia con &quot;test&quot;. Una stringa di ricerca costituita esclusivamente da un carattere jolly può essere utilizzata per filtrare gli oggetti in base al fatto che contengano o meno un tag specifico, indipendentemente dal suo valore.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di [!DNL Catalog] oggetto da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | Nome del tag per il quale filtrare. |
| `{TAG_VALUE}` | Il valore del tag da filtrare per. Supporta i caratteri jolly (`*`). |

**Richiesta**

La richiesta seguente recupera un elenco di set di dati, filtrando per un tag con un valore specifico e per il secondo tag presente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di set di dati contenenti `sampleTag` il valore &quot;123456&quot;, AND `secondTag` con qualsiasi valore. A meno che non venga specificato un limite, la risposta contiene un massimo di 20 oggetti.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

Alcuni endpoint nell&#39; [!DNL Catalog] API dispongono di parametri di query che consentono query con intervallo, più spesso nel caso di date.

**Formato API**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| Parametro | Descrizione |
| --- | --- |
| `{TIMESTAMP }` | Un numero intero datetime nell&#39;ora Unix Epoch. |

**Richiesta**

La richiesta seguente recupera un elenco di batch creati durante il mese di aprile 2019.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta contiene un elenco di [!DNL Catalog] oggetti che rientrano nell&#39;intervallo di date specificato. A meno che non venga specificato un limite, la risposta contiene un massimo di 20 oggetti.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

## Ordina per, proprietà

Il parametro `orderBy` query consente di ordinare i dati delle risposte in base a un valore di proprietà specificato. Questo parametro richiede una &quot;direzione&quot; (`asc` per crescente o `desc` decrescente), seguita da due punti (`:`) e quindi da una proprietà per ordinare i risultati. Se non viene specificata una direzione, la direzione predefinita è crescente.

Più proprietà di ordinamento possono essere fornite in un elenco separato da virgole. Se la prima proprietà di ordinamento produce più oggetti che contengono lo stesso valore per tale proprietà, la seconda proprietà di ordinamento viene utilizzata per ordinare ulteriormente gli oggetti corrispondenti.

Ad esempio, si consideri la seguente query: `orderBy=name,desc:created`. I risultati vengono ordinati in ordine crescente in base alla prima proprietà di ordinamento, `name`. Nei casi in cui più record condividono la stessa `name` proprietà, questi record corrispondenti vengono quindi ordinati in base alla seconda proprietà di ordinamento, `created`. Se nessun record restituito condivide lo stesso `name`, la `created` proprietà non viene applicata all&#39;ordinamento.


**Formato API**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di oggetto Catalog da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | Nome di una proprietà per cui ordinare i risultati. |

**Richiesta**

La richiesta seguente recupera un elenco di set di dati ordinati in base alla relativa `name` proprietà. Se un set di dati condivide lo stesso `name`, questi verranno a loro volta ordinati dalla `updated` proprietà in ordine decrescente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta contiene un elenco di [!DNL Catalog] oggetti ordinati in base al `orderBy` parametro. A meno che non venga specificato un limite, la risposta contiene un massimo di 20 oggetti.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

[!DNL Catalog] sono disponibili due metodi di filtraggio per proprietà, descritti in dettaglio nelle sezioni seguenti:

* [Utilizzo di filtri](#using-simple-filters)semplici: Filtrare per stabilire se una specifica proprietà corrisponde a un valore specifico.
* [Utilizzo del parametro](#using-the-property-parameter)della proprietà: Utilizzare espressioni condizionali per filtrare in base all&#39;esistenza di una proprietà o se il valore di una proprietà corrisponde, si avvicina o si confronta con un altro valore o un&#39;espressione regolare specificata.

### Utilizzo di filtri semplici {#using-simple-filters}

I filtri semplici consentono di filtrare le risposte in base a valori di proprietà specifici. Un filtro semplice assume la forma di `{PROPERTY_NAME}={VALUE}`.

Ad esempio, la query `name=exampleName` restituisce solo oggetti la cui `name` proprietà contiene il valore &quot;exampleName&quot;. Per contro, la query `name=!exampleName` restituisce solo oggetti la cui `name` proprietà **non** è &quot;exampleName&quot;.

Inoltre, i filtri semplici supportano la possibilità di richiedere più valori per una singola proprietà. Quando vengono forniti più valori, la risposta restituisce oggetti la cui proprietà corrisponde a **uno qualsiasi** dei valori nell&#39;elenco fornito. Per invertire una query con più valori, è possibile anteporre un `!` carattere all&#39;elenco e restituire solo gli oggetti il cui valore di proprietà **non** è incluso nell&#39;elenco fornito (ad esempio, `name=!exampleName,anotherName`).

**Formato API**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di [!DNL Catalog] oggetto da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | Nome della proprietà di cui si desidera filtrare il valore. |
| `{VALUE}` | Un valore di proprietà che determina i risultati da includere (o escludere, a seconda della query). |

**Richiesta**

La richiesta seguente recupera un elenco di set di dati, filtrati per includere solo set di dati la cui `name` proprietà ha un valore &quot;exampleName&quot; o &quot;anotherName&quot;.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta contiene un elenco di set di dati, ad esclusione di qualsiasi set di dati `name` con nome &quot;exampleName&quot; o &quot;anotherName&quot;. A meno che non venga specificato un limite, la risposta contiene un massimo di 20 oggetti.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

### Utilizzo del `property` parametro {#using-the-property-parameter}

Il parametro `property` query offre maggiore flessibilità per il filtraggio basato sulle proprietà rispetto ai filtri semplici. Oltre al filtraggio basato sul fatto che una proprietà abbia un valore specifico, il `property` parametro può utilizzare altri operatori di confronto (come &quot;più di&quot; (`>`) e &quot;meno di&quot; (`<`)), nonché espressioni regolari per filtrare in base ai valori delle proprietà. Può inoltre filtrare in base all&#39;esistenza o meno di una proprietà, indipendentemente dal suo valore.

Il `property` parametro accetta solo proprietà dell&#39;oggetto di livello principale, il che significa che per il seguente oggetto di esempio è possibile filtrare per proprietà per `name`, `description`e `subItem`, ma NON per `sampleKey`.

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
| `{OBJECT_TYPE}` | Tipo di [!DNL Catalog] oggetto da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | Un&#39;espressione condizionale che indica per quale proprietà eseguire la query e come valutare il relativo valore. Di seguito sono riportati alcuni esempi. |

Il valore del `property` parametro supporta diversi tipi di espressioni condizionali. La tabella seguente delinea la sintassi di base per le espressioni supportate:

| Simboli | Descrizione | Esempio |
| --- | --- | --- |
| (Nessuna) | Se si imposta il nome della proprietà senza alcun operatore, vengono restituiti solo gli oggetti in cui esiste la proprietà, indipendentemente dal relativo valore. | `property=name` |
| ! | Se si antepone &quot;`!`&quot; al valore di un `property` parametro, vengono restituiti solo gli oggetti in cui la proprietà **non** esiste. | `property=!name` |
| ~ | Restituisce solo oggetti i cui valori di proprietà (stringa) corrispondono a un&#39;espressione regolare fornita dopo il simbolo tilde (`~`). | `property=name~^example` |
| == | Restituisce solo oggetti i cui valori di proprietà corrispondono esattamente alla stringa fornita dopo il simbolo a doppia uguale (`==`). | `property=name==exampleName` |
| != | Restituisce solo oggetti i cui valori di proprietà **non** corrispondono alla stringa fornita dopo il simbolo non uguale a (`!=`). | `property=name!=exampleName` |
| &lt; | Restituisce solo oggetti i cui valori di proprietà sono inferiori (ma non uguali) a un importo specificato. | `property=version<1.0.0` |
| &lt;= | Restituisce solo oggetti i cui valori di proprietà sono inferiori o uguali a un valore specificato. | `property=version<=1.0.0` |
| > | Restituisce solo oggetti i cui valori di proprietà sono maggiori di (ma non uguali a) un valore specificato. | `property=version>1.0.0` |
| >= | Restituisce solo oggetti i cui valori di proprietà sono maggiori di (o uguali a) un valore specificato. | `property=version>=1.0.0` |

>[!NOTE]
>
>La `name` proprietà supporta l&#39;uso di un carattere jolly `*`, come intera stringa di ricerca o come parte di essa. I caratteri jolly corrispondono a caratteri vuoti, in modo che la stringa di ricerca `te*st` corrisponda al valore &quot;test&quot;. Gli asterischi vengono evasi raddoppiandoli (`**`). Un doppio asterisco in una stringa di ricerca rappresenta un singolo asterisco come stringa letterale.

**Richiesta**

Nella richiesta seguente verranno restituiti tutti i set di dati con un numero di versione maggiore di 1.0.3.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta contiene un elenco di set di dati con numeri di versione superiori a 1.0.3. A meno che non venga specificato un limite, la risposta contiene un massimo di 20 oggetti.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.1.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

Utilizzando una e commerciale (`&`), potete combinare più filtri in una singola richiesta. Quando a una richiesta vengono aggiunte condizioni aggiuntive, viene considerata una relazione AND.

**Formato API**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
