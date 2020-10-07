---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Metriche disponibili
topic: developer guide
translation-type: tm+mt
source-git-commit: ae6f220cdec54851fb78b7ba8a8eb19f2d06b684
workflow-type: tm+mt
source-wordcount: '2007'
ht-degree: 2%

---


# Endpoint delle metriche

Le metriche di osservabilità forniscono informazioni approfondite sulle statistiche di utilizzo, sulle tendenze storiche e sugli indicatori di prestazioni per diverse funzioni di Adobe Experience Platform. L&#39; `/metrics` endpoint [!DNL Observability Insights API] consente di recuperare i dati delle metriche a livello di programmazione per l&#39;attività dell&#39;organizzazione in [!DNL Platform].

## Introduzione

L&#39;endpoint API utilizzato in questa guida è parte dell&#39; [[!DNL Observability Insights] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml). Prima di continuare, consultate la guida [introduttiva per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente chiamate a qualsiasi](./getting-started.md) [!DNL Experience Platform] API.

## Recuperare le metriche di osservabilità

Esistono due metodi supportati per recuperare i dati delle metriche utilizzando l&#39;API:

* [Versione 1](#v1): Specificate le metriche utilizzando i parametri di query.
* [Versione 2](#v2): Specificate e applicate i filtri alle metriche utilizzando un payload JSON.

### Versione 1 {#v1}

Puoi recuperare i dati delle metriche effettuando una richiesta di GET all&#39; `/metrics` endpoint, specificando le metriche mediante l&#39;uso di parametri di query.

**Formato API**

Nel `metric` parametro deve essere specificata almeno una metrica. Altri parametri di query sono facoltativi per filtrare i risultati.

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| Parametro | Descrizione |
| --- | --- |
| `{METRIC}` | La metrica da esporre. Quando combini più metriche in una singola chiamata, devi usare una e commerciale (`&`) per separare le singole metriche. Ad esempio, `metric={METRIC_1}&metric={METRIC_2}`. |
| `{ID}` | Identificatore per una particolare [!DNL Platform] risorsa di cui si desidera esporre le metriche. Questo ID può essere facoltativo, obbligatorio o non applicabile a seconda delle metriche utilizzate. Vedi l&#39; [appendice](#available-metrics) per un elenco delle metriche disponibili, inclusi gli ID supportati (obbligatori e facoltativi) per ciascuna metrica. |
| `{DATE_RANGE}` | L&#39;intervallo di date per le metriche da esporre, in formato ISO 8601 (ad esempio, `2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`). |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics?metric=timeseries.ingestion.dataset.size&metric=timeseries.ingestion.dataset.recordsuccess.count&id=5cf8ab4ec48aba145214abeb&dateRange=2018-10-01T07:00:00.000Z/2019-06-06T07:00:00.000Z \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di oggetti, ciascuno contenente una marca temporale all&#39;interno dei valori forniti `dateRange` e corrispondenti per le metriche specificate nel percorso della richiesta. Se il percorso `id` di richiesta include una [!DNL Platform] risorsa, i risultati verranno applicati solo a tale risorsa. Se `id` viene omesso, i risultati verranno applicati a tutte le risorse applicabili all&#39;interno dell&#39;organizzazione IMS.

```json
{
  "id": "5cf8ab4ec48aba145214abeb",
  "imsOrgId": "{IMS_ORG}",
  "timeseries": {
    "granularity": "MONTH",
    "items": [
      {
        "timestamp": "2019-06-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 1125,
          "timeseries.ingestion.dataset.size": 32320
        }
      },
      {
        "timestamp": "2019-05-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 1003,
          "timeseries.ingestion.dataset.size": 31409
        }
      },
      {
        "timestamp": "2019-04-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 740,
          "timeseries.ingestion.dataset.size": 25809
        }
      },
      {
        "timestamp": "2019-03-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 740,
          "timeseries.ingestion.dataset.size": 25809
        }
      },
      {
        "timestamp": "2019-02-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 390,
          "timeseries.ingestion.dataset.size": 16801
        }
      }
    ],
    "_page": null,
    "_links": null
  },
  "stats": {}
}
```

### Versione 2 {#v2}

Puoi recuperare i dati delle metriche effettuando una richiesta di POST all&#39; `/metrics` endpoint, specificando le metriche che desideri recuperare nel payload.

**Formato API**

```http
POST /metrics
```

**Richiesta**

```sh
curl -X POST \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "start": "2020-07-14T00:00:00.000Z",
        "end": "2020-07-22T00:00:00.000Z",
        "granularity": "day",
        "metrics": [
          {
            "name": "timeseries.ingestion.dataset.recordsuccess.count",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
                "groupBy": true
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          },
          {
            "name": "timeseries.ingestion.dataset.dailysize",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5eddb21420f516191b7a8dad",
                "groupBy": false
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          }
        ]
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `start` | Data/ora meno recente da cui recuperare i dati delle metriche. |
| `end` | Data/ora più recente da cui recuperare i dati delle metriche. |
| `granularity` | Un campo facoltativo che indica un intervallo di tempo per il quale dividere i dati delle metriche. Ad esempio, un valore di `DAY` restituisce le metriche per ogni giorno compreso tra `start` e `end` la data, mentre un valore di `MONTH` restituisce i risultati delle metriche raggruppati per mese. Quando si utilizza questo campo, è necessario fornire anche una `downsample` proprietà corrispondente per indicare la funzione di aggregazione tramite la quale raggruppare i dati. |
| `metrics` | Un array di oggetti, uno per ogni metrica da recuperare. |
| `name` | Il nome di una metrica riconosciuta da Observability Insights. Vedi l&#39; [appendice](#available-metrics) per un elenco completo dei nomi delle metriche accettate. |
| `filters` | Campo facoltativo che consente di filtrare le metriche in base a specifici set di dati. Il campo è un array di oggetti (uno per ciascun filtro), con ogni oggetto contenente le seguenti proprietà: <ul><li>`name`: Il tipo di entità con cui filtrare le metriche. Al momento, `dataSets` è supportato solo.</li><li>`value`: ID di uno o più set di dati. Più ID di set di dati possono essere forniti come una singola stringa, con ciascun ID separato da caratteri a barre verticali (`|`).</li><li>`groupBy`: Se impostato su true, indica che il corrispondente `value` rappresenta più set di dati i cui risultati della metrica devono essere restituiti separatamente. Se impostato su false, i risultati delle metriche per tali set di dati vengono raggruppati.</li></ul> |
| `aggregator` | Specifica la funzione di aggregazione da utilizzare per raggruppare più record serie temporali in singoli risultati. Per informazioni dettagliate sugli aggregatori disponibili, consulta la documentazione [](http://opentsdb.net/docs/build/html/user_guide/query/aggregators.html)OpenTSDB. |
| `downsample` | Campo facoltativo che consente di specificare una funzione di aggregazione per ridurre la frequenza di campionamento dei dati delle metriche ordinando i campi in intervalli (o &quot;secchi&quot;). L&#39;intervallo per il downsampling è determinato dalla `granularity` proprietà. Per informazioni dettagliate sul downsampling, consultate la documentazione [](http://opentsdb.net/docs/build/html/user_guide/query/downsampling.html)OpenTSDB. |

**Risposta**

Una risposta corretta restituisce i punti dati risultanti per le metriche e i filtri specificati nella richiesta.

```json
{
  "metricResponses": [
    {
      "metric": "timeseries.ingestion.dataset.recordsuccess.count",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
          "groupBy": true
        }
      ],
      "datapoints": [
        {
          "groupBy": {
            "dataSetId": "5edcfb2fbb642119194c7d94"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        },
        {
          "groupBy": {
            "dataSetId": "5eddb21420f516191b7a8dad"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        }
      ],
      "granularity": "DAY"
    },
    {
      "metric": "timeseries.ingestion.dataset.dailysize",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5eddb21420f516191b7a8dad",
          "groupBy": false
        }
      ],
      "datapoints": [
        {
          "groupBy": {},
          "dps": {
            "2020-07-14T00:00:00Z": 38455.0,
            "2020-07-15T00:00:00Z": 40213.0,
            "2020-07-16T00:00:00Z": 31476.0,
            "2020-07-17T00:00:00Z": 43705.0,
            "2020-07-18T00:00:00Z": 33227.0,
            "2020-07-19T00:00:00Z": 34977.0,
            "2020-07-20T00:00:00Z": 36735.0,
            "2020-07-21T00:00:00Z": 36737.0,
            "2020-07-22T00:00:00Z": 43715.0
          }
        }
      ],
      "granularity": "DAY"
    }
  ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `metricResponses` | Un array i cui oggetti rappresentano ciascuna delle metriche specificate nella richiesta. Ciascun oggetto contiene informazioni sulla configurazione del filtro e i dati delle metriche restituiti. |
| `metric` | Nome di una delle metriche fornite nella richiesta. |
| `filters` | La configurazione del filtro per la metrica specificata. |
| `datapoints` | Un array i cui oggetti rappresentano i risultati della metrica e dei filtri specificati. Il numero di oggetti nell&#39;array dipende dalle opzioni di filtro fornite nella richiesta. Se non sono stati forniti filtri, l&#39;array conterrà solo un singolo oggetto che rappresenta tutti i dataset. |
| `groupBy` | Se sono stati specificati più set di dati nella `filter` proprietà di una metrica e l&#39; `groupBy` opzione è stata impostata su true nella richiesta, questo oggetto conterrà l&#39;ID del set di dati a cui si applica la `dps` proprietà corrispondente.<br><br>Se l&#39;oggetto appare vuoto nella risposta, la `dps` proprietà corrispondente si applica a tutti i set di dati forniti nell&#39; `filters` array (o a tutti i set di dati in [!DNL Platform] assenza di filtri). |
| `dps` | I dati restituiti per la metrica, il filtro e l&#39;intervallo di tempo specificati. Ogni chiave in questo oggetto rappresenta una marca temporale con un valore corrispondente per la metrica specificata. Il periodo di tempo tra ciascun punto di dati dipende dal `granularity` valore specificato nella richiesta. |

## Appendice

La sezione seguente contiene informazioni aggiuntive sull’utilizzo dell’ `/metrics` endpoint.

### Metriche disponibili {#available-metrics}

Le tabelle seguenti elencano tutte le metriche esposte da [!DNL Observability Insights], suddivise per [!DNL Platform] servizio. Ogni metrica include una descrizione e il parametro di query ID accettato.

>[!NOTE]
>
>Tutti i parametri di query ID elencati sono facoltativi, salvo diversa indicazione.

#### [!DNL Data Ingestion] {#ingestion}

La tabella seguente delinea le metriche per Adobe Experience Platform [!DNL Data Ingestion]. Le metriche in **grassetto** sono metriche di assimilazione in streaming.

| Metrica Insights | Descrizione | Parametro query ID |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Numero totale di set di dati creati. | N/D |
| timeseries.ingestion.dataset.size | Dimensione cumulativa di tutti i dati acquisiti per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.ingestion.dataset.dailysize | Dimensione dei dati acquisiti su base giornaliera per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.ingestion.dataset.batchfailed.count | Numero di batch non riusciti per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.ingestion.dataset.batchsuccess.count | Numero di batch acquisiti per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.ingestion.dataset.recordsuccess.count | Numero di record acquisiti per un set di dati o per tutti i set di dati. | ID set di dati |
| **timeseries.data.collection.validation.total.messages.rate** | Numero totale di messaggi per un set di dati o per tutti i set di dati. | ID set di dati |
| **timeseries.data.collection.validation.valid.messages.rate** | Numero totale di messaggi validi per un set di dati o per tutti i set di dati. | ID set di dati |
| **timeseries.data.collection.validation.Invalid.messages.rate** | Numero totale di messaggi non validi per un set di dati o per tutti i set di dati. | ID set di dati |
| **timeseries.data.collection.validation.category.type.count** | Numero totale di messaggi &quot;tipo&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati |
| **timeseries.data.collection.validation.category.range.count** | Numero totale di messaggi &quot;intervallo&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati |
| **timeseries.data.collection.validation.category.format.count** | Numero totale di messaggi &quot;formato&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati |
| **timeseries.data.collection.validation.category.pattern.count** | Numero totale di messaggi &quot;pattern&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati |
| **timeseries.data.collection.validation.category.presence.count** | Numero totale di messaggi di &quot;presenza&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati |
| **timeseries.data.collection.validation.category.enum.count** | Numero totale di messaggi &quot;enum&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati |
| **timeseries.data.collection.validation.category.unlassificati.count** | Numero totale di messaggi &quot;non classificati&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati |
| **timeseries.data.collection.validation.category.unknown.count** | Numero totale di messaggi &quot;sconosciuti&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati |
| **timeseries.data.collection.inlet.total.messages.Received** | Numero totale di messaggi ricevuti per una entrata dati o per tutte le ingressi di dati. | ID ingresso |
| **timeseries.data.collection.inlet.total.messages.size.Received** | Dimensione totale dei dati ricevuti per una entrata dati o per tutte le ingressi di dati. | ID ingresso |
| **timeseries.data.collection.inlet.success** | Numero totale di chiamate HTTP riuscite a un&#39;entrata dati o a tutte le insenature dati. | ID ingresso |
| **timeseries.data.collection.inlet.failure** | Numero totale di chiamate HTTP non riuscite a una entrata dati o a tutte le insenature dati. | ID ingresso |

#### [!DNL Identity Service] {#identity}

La tabella seguente delinea le metriche per Adobe Experience Platform [!DNL Identity Service].

| Metrica Insights | Descrizione | Parametro query ID |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Numero di record scritti nella propria origine dati da [!DNL Identity Service], per un set di dati o tutti i set di dati. | ID set di dati |
| timeseries.identity.dataset.recordfailed.count | Numero di record non riusciti da [!DNL Identity Service], per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Numero di record di identità acquisiti correttamente per uno spazio dei nomi. | ID spazio nomi (**obbligatorio**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Numero di record di identità non riuscito da uno spazio dei nomi. | ID spazio nomi (**obbligatorio**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Numero di record di identità ignorati da uno spazio dei nomi. | ID spazio nomi (**obbligatorio**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Numero di identità univoche memorizzate nel grafico dell&#39;identità per l&#39;organizzazione IMS. | N/D |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Numero di identità univoche memorizzate nel grafico dell&#39;identità per uno spazio dei nomi. | ID spazio nomi (**obbligatorio**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Numero di identità univoche del grafico memorizzate nel grafico di identità per l&#39;organizzazione IMS. | N/D |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Numero di identità univoche memorizzate nel grafico dell&#39;identità per l&#39;organizzazione IMS per una particolare intensità del grafico (&quot;sconosciuto&quot;, &quot;debole&quot; o &quot;forte&quot;). | Forza del grafico (**richiesta**) |

#### [!DNL Privacy Service] {#privacy}

La tabella seguente delinea le metriche per Adobe Experience Platform [!DNL Privacy Service].

| Metrica Insights | Descrizione | Parametro query ID |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Numero totale di posti di lavoro creati dal GDPR. | ENV (**obbligatorio**) |
| timeseries.gdpr.jobs.completedjobs.count | Numero totale di processi completati dal GDPR. | ENV (**obbligatorio**) |
| timeseries.gdpr.jobs.errorjobs.count | Numero totale di processi di errore da GDPR. | ENV (**obbligatorio**) |

#### [!DNL Query Service] {#query}

La tabella seguente delinea le metriche per Adobe Experience Platform [!DNL Query Service].

| Metrica Insights | Descrizione | Parametro query ID |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Numero totale di query pianificate non ricorrenti. | N/D |
| timeseries.queryservice.query.scheduledrecurring.count | Numero totale di query programmate ricorrenti. | N/D |
| timeseries.queryservice.query.batchquery.count | Numero totale di query batch eseguite. | N/D |
| timeseries.queryservice.query.scheduledquery.count | Numero totale di query pianificate eseguite. | N/D |
| timeseries.queryservice.query.interactivequery.count | Numero totale di query interattive eseguite. | N/D |
| timeseries.queryservice.query.batchfrompsqlquery.count | Numero totale di query batch eseguite da PSQL. | N/D |

#### [!DNL Real-time Customer Profile] {#profile}

La tabella seguente delinea le metriche per [!DNL Real-time Customer Profile].

| Metrica Insights | Descrizione | Parametro query ID |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Numero di record letti dal [!DNL Data Lake] modulo [!DNL Profile], per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.profiles.dataset.recordsuccess.count | Numero di record scritti nella propria origine dati da [!DNL Profile], per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.profiles.dataset.recordfailed.count | Numero di record non riusciti da [!DNL Profile], per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.profiles.dataset.batchsuccess.count | Numero di [!DNL Profile] batch acquisiti per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.profiles.dataset.batchfailed.count | Numero di [!DNL Profile] batch non riusciti per un set di dati o per tutti i set di dati. | ID set di dati |
| platform.ups.ingest.streaming.request.m1_rate | Tasso richieste in arrivo. | Organizzazione IMS (**richiesta**) |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Tasso di successo dell&#39;ingestione. | Organizzazione IMS (**richiesta**) |
| platform.ups.ingest.streaming.records.created.m15_rate | Frequenza dei nuovi record acquisiti per un set di dati. | ID set di dati (**obbligatorio**) |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Frequenza dei record con marca temporale fuori ordine per la creazione di richieste per un dataset. | ID set di dati (**obbligatorio**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Timestamp dell&#39;ultima richiesta di creazione record per un dataset. | ID set di dati (**obbligatorio**) |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Frequenza dei record con marca temporale fuori ordine per la richiesta di aggiornamento per un dataset. | ID set di dati (**obbligatorio**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Timestamp per l&#39;ultima richiesta di aggiornamento record per un dataset. | ID set di dati (**obbligatorio**) |
| platform.ups.ingest.streaming.record.size.m1_rate | Dimensione media del record. | Organizzazione IMS (**richiesta**) |
| platform.ups.ingest.streaming.records.updated.m15_rate | Frequenza delle richieste di aggiornamento per i record acquisiti per un set di dati. | ID set di dati (**obbligatorio**) |

### Messaggi di errore

Le risposte dall&#39; `/metrics` endpoint possono restituire messaggi di errore a determinate condizioni. Questi messaggi di errore vengono restituiti nel formato seguente:

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{IMS_ORG}"
        },
        "additionalContext": null
    },
    "error-chain": [
        {
            "serviceId": "INSGHT",
            "errorCode": "INSGHT-1000-400",
            "invokingServiceId": "INSGHT",
            "unixTimeStampMs": 1602095177129
        }
    ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `title` | Una stringa contenente il messaggio di errore e il motivo potenziale per cui potrebbe essersi verificato. |
| `report` | Contiene informazioni contestuali sull&#39;errore, inclusa la sandbox e l&#39;organizzazione IMS utilizzata nell&#39;operazione che l&#39;ha attivata. |

Nella tabella seguente sono elencati i diversi codici di errore che possono essere restituiti dall&#39;API:

| Codice errore | Title | Descrizione |
| --- | --- | --- |
| `INSGHT-1000-400` | Payload di richiesta non valido | Si è verificato un errore nel payload della richiesta. Assicurarsi di avere la stessa formattazione del payload come illustrato [sopra](#v2). Uno dei possibili motivi può attivare questo errore:<ul><li>Campi obbligatori mancanti, ad esempio `aggregator`</li><li>Metriche non valide</li><li>La richiesta contiene un aggregatore non valido</li><li>Una data di inizio ha luogo dopo una data di fine</li></ul> |
| `INSGHT-1001-400` | Query metriche non riuscita | Si è verificato un errore durante il tentativo di eseguire una query sul database delle metriche a causa di una richiesta non valida o della query stessa non analizzabile. Prima di riprovare, verificate che la richiesta sia formattata correttamente. |
| `INSGHT-1001-500` | Query metriche non riuscita | Si è verificato un errore durante il tentativo di query al database delle metriche a causa di un errore del server. Riprovare la richiesta e, se il problema persiste, contattare  supporto del Adobe. |
| `INSGHT-1002-500` | Errore del servizio | Impossibile elaborare la richiesta a causa di un errore interno. Riprovare la richiesta e, se il problema persiste, contattare  supporto del Adobe. |
| `INSGHT-1003-401` | Errore di convalida sandbox | Impossibile elaborare la richiesta a causa di un errore di convalida sandbox. Prima di riprovare, verificate che il nome della sandbox fornito nell’ `x-sandbox-name` intestazione rappresenti una sandbox valida e abilitata per l’organizzazione IMS. |
