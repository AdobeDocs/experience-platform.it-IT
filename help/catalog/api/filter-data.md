---
keywords: Experience Platform;home;argomenti popolari;filtro;filtrare;filtrare dati;filtrare dati;intervallo di date
solution: Experience Platform
title: Filtrare i dati del catalogo utilizzando i parametri della query
topic-legacy: developer guide
description: L’API del servizio catalogo consente di filtrare i dati di risposta utilizzando i parametri di query della richiesta. Parte delle best practice per Catalog consiste nell’utilizzare i filtri in tutte le chiamate API, in quanto riducono il carico sull’API e contribuiscono a migliorare le prestazioni complessive.
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2121'
ht-degree: 1%

---

# Filtrare i dati [!DNL Catalog] utilizzando i parametri di query

L’ API [!DNL Catalog Service] consente di filtrare i dati di risposta utilizzando i parametri di query della richiesta. Parte delle best practice per [!DNL Catalog] è l’utilizzo di filtri in tutte le chiamate API, in quanto riducono il carico sull’API e contribuiscono a migliorare le prestazioni complessive.

Questo documento illustra i metodi più comuni per filtrare gli oggetti [!DNL Catalog] nell&#39;API. È consigliabile fare riferimento a questo documento durante la lettura della [Guida per gli sviluppatori del catalogo](getting-started.md) per ulteriori informazioni su come interagire con l&#39;API [!DNL Catalog]. Per informazioni generali su [!DNL Catalog Service], consulta la [[!DNL Catalog] panoramica](../home.md).

## Limitare gli oggetti restituiti

Il parametro di query `limit` vincola il numero di oggetti restituiti in una risposta. [!DNL Catalog] le risposte vengono misurate automaticamente in base ai limiti configurati:

* Se non si specifica un parametro `limit`, il numero massimo di oggetti per payload di risposta è 20.
* Per le query dei set di dati, se `observableSchema` viene richiesto utilizzando il parametro di query `properties`, il numero massimo di set di dati restituiti è 20.
* Il limite globale per tutte le altre query del catalogo è di 100 oggetti.
* I parametri `limit` non validi (incluso `limit=0`) generano risposte di errore a 400 livelli che delineano intervalli appropriati.
* I limiti o gli offset passati come parametri di query hanno la precedenza su quelli passati come intestazioni.

**Formato API**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di oggetto [!DNL Catalog] da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
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

Una risposta corretta restituisce un elenco di set di dati, limitato al numero indicato dal parametro di query `limit` .

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

Anche quando si filtra il numero di oggetti restituiti utilizzando il parametro `limit` , gli oggetti restituiti possono spesso contenere più informazioni di quelle effettivamente necessarie. Per ridurre ulteriormente il carico sul sistema, è consigliabile filtrare le risposte in modo da includere solo le proprietà necessarie.

Il parametro `properties` filtra gli oggetti di risposta per restituire solo un set di proprietà specificate. Il parametro può essere impostato per restituire una o più proprietà.

Il parametro `properties` accetta solo proprietà dell&#39;oggetto di livello principale, il che significa che per il seguente oggetto di esempio è possibile applicare filtri per `name`, `description` e `subItem`, ma NON per `sampleKey`.

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
| `{OBJECT_TYPE}` | Il tipo di oggetto [!DNL Catalog] da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | Nome di un attributo da includere nel corpo della risposta. |
| `{OBJECT_ID}` | Identificatore univoco di un oggetto specifico [!DNL Catalog] da recuperare. |

**Richiesta**

La richiesta seguente recupera un elenco di set di dati. L&#39;elenco separato da virgole dei nomi di proprietà forniti sotto il parametro `properties` indica le proprietà da restituire nella risposta. È incluso anche un parametro `limit` che limita il numero di set di dati restituiti. Se la richiesta non includeva un parametro `limit`, la risposta conterrebbe un massimo di 20 oggetti.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di oggetti [!DNL Catalog] con solo le proprietà richieste visualizzate.

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

Sulla base della risposta di cui sopra, si può dedurre quanto segue:

* Se a un oggetto mancano le proprietà richieste, verranno mostrate solo le proprietà richieste che include. (`Dataset1`)
* Se un oggetto non include alcuna delle proprietà richieste, verrà visualizzato come un oggetto vuoto. (`Dataset2`)
* Un set di dati può restituire una proprietà richiesta come oggetto vuoto se contiene la proprietà ma non è presente alcun valore. (`Dataset3`)
* In caso contrario, il set di dati visualizzerà il valore completo di tutte le proprietà richieste. (`Dataset4`)

>[!NOTE]
>
>Nella proprietà `schemaRef` di ogni set di dati, il numero di versione indica la versione secondaria più recente dello schema. Per ulteriori informazioni, consulta la sezione sul [controllo delle versioni dello schema](../../xdm/api/getting-started.md#versioning) nella guida API XDM .

## Offset indice iniziale dell&#39;elenco di risposte

Il parametro di query `start` consente di spostare l&#39;elenco di risposte in avanti di un numero specificato, utilizzando una numerazione basata su zero. Ad esempio, `start=2` compensa la risposta per iniziare sul terzo oggetto elencato.

Se il parametro `start` non è associato a un parametro `limit`, il numero massimo di oggetti restituiti è 20.

**Formato API**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di oggetto Catalog da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | Un numero intero che indica il numero di oggetti per cui eseguire l&#39;offset della risposta. |

**Richiesta**

La richiesta seguente recupera un elenco di set di dati, eseguendo l’offset al quinto oggetto (`start=4`) e limitando la risposta a due set di dati restituiti (`limit=2`).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta include un oggetto JSON contenente due elementi di primo livello (`limit=2`), uno per ogni set di dati e i relativi dettagli (i dettagli sono stati condensati nell’esempio). La risposta viene spostata di quattro (`start=4`), il che significa che i set di dati mostrati sono i numeri cinque e sei cronologicamente.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## Filtrare per tag

Alcuni oggetti Catalog supportano l’utilizzo di un attributo `tags` . I tag possono allegare informazioni a un oggetto e quindi essere utilizzati in un secondo momento per recuperare tale oggetto. La scelta dei tag da utilizzare e di come applicarli dipende dai processi organizzativi in uso.

Ci sono alcune limitazioni da considerare quando si utilizzano i tag:

* Gli unici oggetti Catalog che attualmente supportano i tag sono set di dati, batch e connessioni.
* I nomi dei tag sono univoci per la tua organizzazione IMS.
* I processi di Adobe possono sfruttare i tag per determinati comportamenti. I nomi di questi tag hanno il prefisso &quot;adobe&quot; come standard. Pertanto, evita questa convenzione quando si dichiarano i nomi dei tag.
* I seguenti nomi di tag sono riservati per l’uso in [!DNL Experience Platform] e non possono pertanto essere dichiarati come nome di tag per la tua organizzazione:
   * `unifiedProfile`: Questo nome di tag è riservato ai set di dati da acquisire da  [[!DNL Real-time Customer Profile]](../../profile/home.md).
   * `unifiedIdentity`: Questo nome di tag è riservato ai set di dati da acquisire da  [[!DNL Identity Service]](../../identity-service/home.md).

Di seguito è riportato un esempio di un set di dati contenente una proprietà `tags` . I tag all&#39;interno di tale proprietà si presentano sotto forma di coppie chiave-valore, con ogni valore di tag che viene visualizzato come una matrice contenente una singola stringa:

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

I valori per il parametro `tags` assumono la forma di coppie chiave-valore, utilizzando il formato `{TAG_NAME}:{TAG_VALUE}`. È possibile fornire più coppie chiave-valore sotto forma di elenco separato da virgole. Quando vengono forniti più tag, si presume una relazione AND.

Il parametro supporta i caratteri jolly (`*`) per i valori dei tag. Ad esempio, una stringa di ricerca di `test*` restituisce qualsiasi oggetto in cui il valore del tag inizia con &quot;test&quot;. È possibile utilizzare una stringa di ricerca costituita esclusivamente da un carattere jolly per filtrare gli oggetti in base al fatto che contengano o meno un tag specifico, indipendentemente dal relativo valore.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di oggetto [!DNL Catalog] da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | Nome del tag da filtrare. |
| `{TAG_VALUE}` | Il valore del tag per cui filtrare. Supporta i caratteri jolly (`*`). |

**Richiesta**

La richiesta seguente recupera un elenco di set di dati, filtrando per un tag con un valore specifico E il secondo tag presente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di set di dati contenenti `sampleTag` con un valore pari a &quot;123456&quot;, AND `secondTag` con qualsiasi valore. A meno che non venga specificato un limite, la risposta contiene un massimo di 20 oggetti.

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

Alcuni endpoint nell’ API [!DNL Catalog] dispongono di parametri di query che consentono query con intervalli, più spesso nel caso di date.

**Formato API**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| Parametro | Descrizione |
| --- | --- |
| `{TIMESTAMP }` | Un numero intero datetime in tempo Unix Epoch. |

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

Una risposta corretta contiene un elenco di oggetti [!DNL Catalog] che rientrano nell’intervallo di date specificato. A meno che non venga specificato un limite, la risposta contiene un massimo di 20 oggetti.

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

## Ordina per proprietà

Il parametro di query `orderBy` consente di ordinare i dati di risposta in base a un valore di proprietà specificato. Questo parametro richiede una &quot;direzione&quot; (`asc` per crescente o `desc` per decrescente), seguita da un due punti (`:`) e quindi da una proprietà per ordinare i risultati in base a. Se non viene specificata una direzione, la direzione predefinita è crescente.

È possibile fornire più proprietà di ordinamento in un elenco separato da virgole. Se la prima proprietà di ordinamento produce più oggetti che contengono lo stesso valore per tale proprietà, la seconda proprietà di ordinamento viene quindi utilizzata per ordinare ulteriormente gli oggetti corrispondenti.

Ad esempio, considera la seguente query: `orderBy=name,desc:created`. I risultati vengono ordinati in ordine crescente in base alla prima proprietà di ordinamento, `name`. Nei casi in cui più record condividono la stessa proprietà `name`, i record corrispondenti vengono quindi ordinati in base alla seconda proprietà di ordinamento, `created`. Se nessun record restituito condivide lo stesso `name`, la proprietà `created` non viene applicata all&#39;ordinamento.


**Formato API**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di oggetto Catalog da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | Nome di una proprietà per cui ordinare i risultati. |

**Richiesta**

La richiesta seguente recupera un elenco di set di dati ordinati in base alla relativa proprietà `name` . Se un set di dati condivide lo stesso `name`, questi verranno a loro volta ordinati dalla proprietà `updated` in ordine decrescente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta contiene un elenco di oggetti [!DNL Catalog] ordinati in base al parametro `orderBy` . A meno che non venga specificato un limite, la risposta contiene un massimo di 20 oggetti.

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

[!DNL Catalog] fornisce due metodi di filtraggio per proprietà, descritti più avanti nelle sezioni seguenti:

* [Utilizzo di filtri](#using-simple-filters) semplici: Filtra per stabilire se una proprietà specifica corrisponde a un valore specifico.
* [Utilizzando il parametro](#using-the-property-parameter) della proprietà: Utilizza le espressioni condizionali per filtrare in base all&#39;esistenza di una proprietà o se il valore di una proprietà corrisponde, si avvicina o si confronta con un altro valore specificato o con un&#39;espressione regolare.

### Utilizzo di filtri semplici {#using-simple-filters}

I filtri semplici consentono di filtrare le risposte in base a valori di proprietà specifici. Un filtro semplice assume la forma di `{PROPERTY_NAME}={VALUE}`.

Ad esempio, la query `name=exampleName` restituisce solo oggetti la cui proprietà `name` contiene un valore di &quot;exampleName&quot;. Al contrario, la query `name=!exampleName` restituisce solo oggetti la cui proprietà `name` è **not** &quot;exampleName&quot;.

Inoltre, i filtri semplici supportano la possibilità di eseguire query per più valori per una singola proprietà. Quando vengono forniti più valori, la risposta restituisce oggetti la cui proprietà corrisponde a **any** dei valori nell&#39;elenco fornito. È possibile invertire una query con più valori prefissando un carattere `!` nell’elenco, restituendo solo oggetti il cui valore di proprietà è **not** nell’elenco fornito (ad esempio, `name=!exampleName,anotherName`).

**Formato API**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di oggetto [!DNL Catalog] da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | Nome della proprietà per la quale si desidera filtrare il valore. |
| `{VALUE}` | Un valore di proprietà che determina i risultati da includere (o escludere, a seconda della query). |

**Richiesta**

La richiesta seguente recupera un elenco di set di dati, filtrati per includere solo i set di dati la cui proprietà `name` ha un valore di &quot;exampleName&quot; o &quot;otherName&quot;.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta contiene un elenco di set di dati, escludendo qualsiasi set di dati il cui `name` è &quot;exampleName&quot; o &quot;otherName&quot;. A meno che non venga specificato un limite, la risposta contiene un massimo di 20 oggetti.

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

### Utilizzo del parametro `property` {#using-the-property-parameter}

Il parametro di query `property` offre maggiore flessibilità per il filtro basato sulle proprietà rispetto ai filtri semplici. Oltre a filtrare in base al fatto che una proprietà abbia un valore specifico, il parametro `property` può utilizzare altri operatori di confronto (come &quot;più di&quot; (`>`) e &quot;meno di&quot; (`<`)), nonché espressioni regolari per filtrare in base ai valori delle proprietà. Può anche filtrare in base all&#39;esistenza o meno di una proprietà, indipendentemente dal suo valore.

Il parametro `property` accetta solo proprietà dell&#39;oggetto di livello superiore, il che significa che per il seguente oggetto di esempio è possibile filtrare per proprietà per `name`, `description` e `subItem`, ma NON per `sampleKey`.

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
| `{OBJECT_TYPE}` | Il tipo di oggetto [!DNL Catalog] da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | Un&#39;espressione condizionale che indica la proprietà da richiedere e la modalità di valutazione del relativo valore. Di seguito sono riportati alcuni esempi. |

Il valore del parametro `property` supporta diversi tipi di espressioni condizionali. La tabella seguente illustra la sintassi di base per le espressioni supportate:

| Simbolo/i | Descrizione | Esempio |
| --- | --- | --- |
| (Nessuna) | Se si imposta il nome della proprietà senza alcun operatore, vengono restituiti solo gli oggetti in cui esiste la proprietà, indipendentemente dal relativo valore. | `property=name` |
| ! | Premendo un parametro &quot;`!`&quot; al valore di un parametro `property` vengono restituiti solo gli oggetti in cui la proprietà non esiste **non**. | `property=!name` |
| ~ | Restituisce solo oggetti i cui valori di proprietà (stringa) corrispondono a un&#39;espressione regolare fornita dopo il simbolo tilde (`~`). | `property=name~^example` |
| == | Restituisce solo oggetti i cui valori di proprietà corrispondono esattamente alla stringa fornita dopo il simbolo a doppio uguale (`==`). | `property=name==exampleName` |
| != | Restituisce solo gli oggetti i cui valori di proprietà non corrispondono alla stringa fornita dopo il simbolo non uguale a (`!=`).**** | `property=name!=exampleName` |
| &lt;> | Restituisce solo oggetti i cui valori di proprietà sono inferiori (ma non uguali) a un valore specificato. | `property=version<1.0.0` |
| &lt;> | Restituisce solo oggetti i cui valori di proprietà sono inferiori o uguali a un valore specificato. | `property=version<=1.0.0` |
| > | Restituisce solo oggetti i cui valori di proprietà sono maggiori di (ma non uguali) un valore specificato. | `property=version>1.0.0` |
| >= | Restituisce solo oggetti i cui valori di proprietà sono maggiori di (o uguali a) un valore specificato. | `property=version>=1.0.0` |

>[!NOTE]
>
>La proprietà `name` supporta l&#39;utilizzo di un carattere jolly `*`, sia come stringa di ricerca intera che come parte di essa. I caratteri jolly corrispondono a caratteri vuoti, in modo che la stringa di ricerca `te*st` corrisponda al valore &quot;test&quot;. Gli asterischi vengono escape raddoppiandoli (`**`). Un doppio asterisco in una stringa di ricerca rappresenta un singolo asterisco come stringa letterale.

**Richiesta**

La seguente richiesta restituirà tutti i set di dati con un numero di versione maggiore di 1.0.3.

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

Utilizzando una e commerciale (`&`), puoi combinare più filtri in una singola richiesta. Quando vengono aggiunte condizioni aggiuntive a una richiesta, si presume una relazione AND.

**Formato API**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
