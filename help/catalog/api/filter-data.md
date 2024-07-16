---
keywords: Experience Platform;home;argomenti popolari;filtro;filtrare;filtrare dati;filtrare dati;intervallo date
solution: Experience Platform
title: Filtrare i dati del catalogo utilizzando i parametri di query
description: L’API Catalog Service consente di filtrare i dati di risposta tramite l’utilizzo di parametri di query di richiesta. Una parte delle best practice per il catalogo consiste nell’utilizzare i filtri in tutte le chiamate API, in quanto riducono il carico sull’API e contribuiscono a migliorare le prestazioni complessive.
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 75099d39fbdb9488105a9254bbbcca9b12349238
workflow-type: tm+mt
source-wordcount: '2117'
ht-degree: 2%

---

# Filtra i dati di [!DNL Catalog] tramite parametri di query

L&#39;API [!DNL Catalog Service] consente di filtrare i dati di risposta tramite l&#39;utilizzo di parametri di query di richiesta. Parte delle best practice per [!DNL Catalog] consiste nell&#39;utilizzare i filtri in tutte le chiamate API, in quanto riducono il carico sull&#39;API e contribuiscono a migliorare le prestazioni complessive.

Questo documento illustra i metodi più comuni per filtrare gli oggetti [!DNL Catalog] nell&#39;API. È consigliabile fare riferimento a questo documento durante la lettura della [Guida per gli sviluppatori di Catalog](getting-started.md) per ulteriori informazioni su come interagire con l&#39;API [!DNL Catalog]. Per ulteriori informazioni generali su [!DNL Catalog Service], vedere la [[!DNL Catalog] panoramica](../home.md).

## Limita oggetti restituiti

Il parametro di query `limit` limita il numero di oggetti restituiti in una risposta. [!DNL Catalog] risposte vengono misurate automaticamente in base ai limiti configurati:

* Se non si specifica un parametro `limit`, il numero massimo di oggetti per payload di risposta è 20.
* Per le query di set di dati, se `observableSchema` viene richiesto utilizzando il parametro di query `properties`, il numero massimo di set di dati restituiti è 20.
* Il limite globale per tutte le altre query Catalog è 100 oggetti.
* I parametri `limit` non validi (incluso `limit=0`) generano risposte di errore a 400 livelli che delineano intervalli corretti.
* I limiti o gli offset passati come parametri di query hanno la precedenza su quelli passati come intestazioni.

**Formato API**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di oggetto [!DNL Catalog] da recuperare. Gli oggetti validi sono: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
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

In caso di esito positivo, la risposta restituisce un elenco di set di dati, limitati al numero indicato dal parametro di query `limit`.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## Limita proprietà visualizzate

Anche quando si filtra il numero di oggetti restituiti utilizzando il parametro `limit`, gli oggetti restituiti possono spesso contenere più informazioni di quelle effettivamente necessarie. Per ridurre ulteriormente il carico sul sistema, è consigliabile filtrare le risposte in modo da includere solo le proprietà necessarie.

Il parametro `properties` filtra gli oggetti di risposta in modo da restituire solo un insieme di proprietà specificate. Il parametro può essere impostato per restituire una o più proprietà.

Il parametro `properties` può accettare qualsiasi proprietà oggetto di livello. È possibile estrarre `sampleKey` tramite `?properties=subItem.sampleKey`.

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
| `{OBJECT_TYPE}` | Tipo di oggetto [!DNL Catalog] da recuperare. Gli oggetti validi sono: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY}` | Nome di un attributo da includere nel corpo della risposta. |
| `{OBJECT_ID}` | Identificatore univoco di un oggetto [!DNL Catalog] specifico da recuperare. |

**Richiesta**

La richiesta seguente recupera un elenco di set di dati. L&#39;elenco separato da virgole dei nomi di proprietà forniti sotto il parametro `properties` indica le proprietà da restituire nella risposta. È incluso anche un parametro `limit`, che limita il numero di set di dati restituiti. Se la richiesta non include un parametro `limit`, la risposta conterrà un massimo di 20 oggetti.

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
>Nella proprietà `schemaRef` per ogni set di dati, il numero di versione indica la versione secondaria più recente dello schema. Per ulteriori informazioni, consulta la sezione sul controllo delle versioni dello schema [1} nella guida dell&#39;API XDM.](../../xdm/api/getting-started.md#versioning)

## Indice di offset iniziale dell&#39;elenco di risposte

Il parametro di query `start` determina l&#39;offset dell&#39;elenco di risposte in avanti in base a un numero specificato, utilizzando la numerazione basata su zero. Ad esempio, `start=2` distanzierebbe la risposta per iniziare dal terzo oggetto elencato.

Se il parametro `start` non è associato a un parametro `limit`, il numero massimo di oggetti restituiti è 20.

**Formato API**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di oggetto Catalog da recuperare. Gli oggetti validi sono: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OFFSET}` | Numero intero che indica il numero di oggetti in base ai quali eseguire l&#39;offset della risposta. |

**Richiesta**

La richiesta seguente recupera un elenco di set di dati, eseguendo l&#39;offset rispetto al quinto oggetto (`start=4`) e limitando la risposta a due set di dati restituiti (`limit=2`).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta include un oggetto JSON contenente due elementi di livello principale (`limit=2`), uno per ogni set di dati e i relativi dettagli (i dettagli sono stati sintetizzati nell&#39;esempio). La risposta viene spostata di quattro (`start=4`), il che significa che i set di dati visualizzati sono il numero cinque e sei in ordine cronologico.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## Filtra per tag

Alcuni oggetti Catalog supportano l&#39;utilizzo di un attributo `tags`. I tag possono allegare informazioni a un oggetto e quindi essere utilizzati in un secondo momento per recuperarlo. La scelta dei tag da utilizzare e la relativa modalità di applicazione dipendono dai processi organizzativi.

Esistono alcune limitazioni da considerare quando si utilizzano i tag:

* Gli unici oggetti Catalog che attualmente supportano i tag sono set di dati, batch e connessioni.
* I nomi dei tag sono univoci per la tua organizzazione.
* I processi Adobe possono sfruttare i tag per determinati comportamenti. I nomi di questi tag hanno il prefisso &quot;adobe&quot; come standard. Pertanto, è necessario evitare questa convenzione quando si dichiarano i nomi dei tag.
* I seguenti nomi di tag sono riservati per l&#39;utilizzo in [!DNL Experience Platform] e pertanto non possono essere dichiarati come nomi di tag per l&#39;organizzazione:
   * `unifiedProfile`: questo nome di tag è riservato per i set di dati da acquisire da [[!DNL Real-Time Customer Profile]](../../profile/home.md).
   * `unifiedIdentity`: questo nome di tag è riservato per i set di dati da acquisire da [[!DNL Identity Service]](../../identity-service/home.md).

Di seguito è riportato un esempio di set di dati contenente una proprietà `tags`. I tag all’interno di tale proprietà assumono la forma di coppie chiave-valore, con ogni valore di tag visualizzato come un array contenente una singola stringa:

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

Il parametro supporta i caratteri jolly (`*`) per i valori dei tag. Ad esempio, una stringa di ricerca di `test*` restituisce qualsiasi oggetto in cui il valore del tag inizia con &quot;test&quot;. Una stringa di ricerca costituita esclusivamente da un carattere jolly può essere utilizzata per filtrare gli oggetti in base al fatto che contengano o meno un tag specifico, indipendentemente dal relativo valore.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di oggetto [!DNL Catalog] da recuperare. Gli oggetti validi sono: <ul><li>`batches`</li><li>`dataSets`</li></ul> |
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

In caso di esito positivo, la risposta restituisce un elenco di set di dati contenenti `sampleTag` con il valore &quot;123456&quot; E `secondTag` con qualsiasi valore. A meno che non venga specificato anche un limite, la risposta contiene un massimo di 20 oggetti.

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
    }
}
```

## Filtra per intervallo di date

Alcuni endpoint nell&#39;API [!DNL Catalog] dispongono di parametri di query che consentono query con intervalli, il più delle volte nel caso di date.

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
    }
}
```

## Ordina per proprietà

Il parametro di query `orderBy` consente di ordinare (ordinare) i dati di risposta in base a un valore di proprietà specificato. Questo parametro richiede una &quot;direction&quot; (`asc` per crescente o `desc` per decrescente), seguita da due punti (`:`) e quindi da una proprietà in base alla quale ordinare i risultati. Se non viene specificata una direzione, la direzione predefinita è crescente.

È possibile specificare più proprietà di ordinamento in un elenco separato da virgole. Se la prima proprietà di ordinamento produce più oggetti che contengono lo stesso valore per tale proprietà, la seconda proprietà di ordinamento viene quindi utilizzata per ordinare ulteriormente gli oggetti corrispondenti.

Considerare ad esempio la seguente query: `orderBy=name,desc:created`. I risultati vengono ordinati in ordine crescente in base alla prima proprietà di ordinamento, `name`. Nei casi in cui più record condividono la stessa proprietà `name`, i record corrispondenti vengono quindi ordinati in base alla seconda proprietà di ordinamento, `created`. Se nessun record restituito condivide lo stesso `name`, la proprietà `created` non viene considerata nell&#39;ordinamento.


**Formato API**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di oggetto Catalog da recuperare. Gli oggetti validi sono: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | Nome di una proprietà in base alla quale ordinare i risultati. |

**Richiesta**

La richiesta seguente recupera un elenco di set di dati ordinati in base alla relativa proprietà `name`. Se uno qualsiasi dei set di dati condivide lo stesso `name`, tali set di dati verranno a loro volta ordinati in ordine decrescente in base alla proprietà `updated`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta contiene un elenco di [!DNL Catalog] oggetti ordinati in base al parametro `orderBy`. A meno che non venga specificato anche un limite, la risposta contiene un massimo di 20 oggetti.

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
    }
}
```

## Filtra per proprietà

[!DNL Catalog] fornisce due metodi di filtraggio per proprietà, descritti in dettaglio nelle sezioni seguenti:

* [Utilizzo di filtri semplici](#using-simple-filters): consente di filtrare in base alla corrispondenza di una proprietà specifica con un valore specifico.
* [Utilizzo del parametro della proprietà](#using-the-property-parameter): utilizzare espressioni condizionali per filtrare in base all&#39;esistenza di una proprietà oppure se il valore di una proprietà corrisponde, si avvicina o si confronta con un altro valore specificato o con un&#39;espressione regolare.

### Utilizzo di filtri semplici {#using-simple-filters}

I filtri semplici ti consentono di filtrare le risposte in base a valori di proprietà specifici. Un filtro semplice assume la forma di `{PROPERTY_NAME}={VALUE}`.

Ad esempio, la query `name=exampleName` restituisce solo oggetti la cui proprietà `name` contiene il valore &quot;exampleName&quot;. La query `name=!exampleName` restituisce invece solo oggetti la cui proprietà `name` è **not** &quot;exampleName&quot;.

Inoltre, i filtri semplici supportano la possibilità di eseguire query per più valori per una singola proprietà. Quando vengono forniti più valori, la risposta restituisce oggetti la cui proprietà corrisponde a **any** dei valori nell&#39;elenco specificato. È possibile invertire una query con più valori inserendo un carattere `!` come prefisso nell&#39;elenco e restituendo solo gli oggetti il cui valore di proprietà è **not** nell&#39;elenco specificato (ad esempio, `name=!exampleName,anotherName`).

**Formato API**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di oggetto [!DNL Catalog] da recuperare. Gli oggetti validi sono: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | Nome della proprietà di cui si desidera filtrare il valore. |
| `{VALUE}` | Valore di proprietà che determina quali risultati includere (o escludere, a seconda della query). |

**Richiesta**

La richiesta seguente recupera un elenco di set di dati, filtrati per includere solo i set di dati la cui proprietà `name` ha il valore &quot;exampleName&quot; o &quot;otherName&quot;.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta contiene un elenco di set di dati, esclusi i set di dati il cui `name` è &quot;exampleName&quot; o &quot;otherName&quot;. A meno che non venga specificato anche un limite, la risposta contiene un massimo di 20 oggetti.

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
    }
}
```

### Utilizzo del parametro `property` {#using-the-property-parameter}

Il parametro di query `property` offre maggiore flessibilità per i filtri basati su proprietà rispetto ai filtri semplici. Oltre a filtrare in base al valore specifico di una proprietà, il parametro `property` può utilizzare altri operatori di confronto, ad esempio &quot;più di&quot; (`>`) e &quot;meno di&quot; (`<`), nonché espressioni regolari per filtrare in base ai valori di proprietà. Può anche filtrare in base all’esistenza o meno di una proprietà, indipendentemente dal suo valore.

Il parametro `property` può accettare qualsiasi proprietà oggetto di livello. `sampleKey` può essere utilizzato per filtrare utilizzando `?properties=subItem.sampleKey`.

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
| `{OBJECT_TYPE}` | Tipo di oggetto [!DNL Catalog] da recuperare. Gli oggetti validi sono: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{CONDITION}` | Espressione condizionale che indica la proprietà per la quale eseguire la query e come deve essere valutato il relativo valore. Di seguito sono riportati alcuni esempi. |

Il valore del parametro `property` supporta diversi tipi di espressioni condizionali. La tabella seguente illustra la sintassi di base delle espressioni supportate:

| Simbolo/i | Descrizione | Esempio |
| --- | --- | --- |
| (Nessuno) | Se si imposta il nome della proprietà senza operatore, verranno restituiti solo gli oggetti in cui la proprietà esiste, indipendentemente dal relativo valore. | `property=name` |
| ! | Se si aggiunge il prefisso &quot;`!`&quot; al valore di un parametro `property`, verranno restituiti solo gli oggetti in cui la proprietà **non** esiste. | `property=!name` |
| ~ | Restituisce solo oggetti i cui valori di proprietà (stringa) corrispondono a un&#39;espressione regolare fornita dopo il simbolo di tilde (`~`). | `property=name~^example` |
| == | Restituisce solo oggetti i cui valori di proprietà corrispondono esattamente alla stringa fornita dopo il simbolo di doppio uguale (`==`). | `property=name==exampleName` |
| != | Restituisce solo oggetti i cui valori di proprietà non corrispondono alla stringa **not** fornita dopo il simbolo not-equals (`!=`). | `property=name!=exampleName` |
| &lt; | Restituisce solo oggetti i cui valori di proprietà sono inferiori (ma non uguali) a una quantità dichiarata. | `property=version<1.0.0` |
| &lt;= | Restituisce solo oggetti i cui valori di proprietà sono inferiori o uguali a una quantità specificata. | `property=version<=1.0.0` |
| > | Restituisce solo oggetti i cui valori di proprietà sono maggiori (ma non uguali) di una quantità dichiarata. | `property=version>1.0.0` |
| >= | Restituisce solo oggetti i cui valori di proprietà sono maggiori o uguali a una quantità specificata. | `property=version>=1.0.0` |

>[!NOTE]
>
>La proprietà `name` supporta l&#39;utilizzo di un carattere jolly `*`, come stringa di ricerca intera o come parte di essa. I caratteri jolly corrispondono a caratteri vuoti, pertanto la stringa di ricerca `te*st` corrisponderà al valore &quot;test&quot;. Gli asterischi hanno escape raddoppiandoli (`**`). Un doppio asterisco in una stringa di ricerca rappresenta un singolo asterisco come stringa letterale.

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
    }
}
```

## Combinare più filtri

Utilizzando una e commerciale (`&`), è possibile combinare più filtri in una singola richiesta. Quando vengono aggiunte condizioni aggiuntive a una richiesta, si presume una relazione AND.

**Formato API**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
