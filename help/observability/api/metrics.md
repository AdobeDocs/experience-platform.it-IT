---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Metriche disponibili
topic: developer guide
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 2%

---


# Endpoint delle metriche

Le metriche di osservabilità forniscono informazioni approfondite sulle statistiche di utilizzo, sulle tendenze storiche e sugli indicatori di prestazioni per diverse funzioni di Adobe Experience Platform. L&#39; `/metrics` endpoint [!DNL Observability Insights API] consente di recuperare i dati delle metriche a livello di programmazione per l&#39;attività dell&#39;organizzazione in [!DNL Platform].

## Introduzione

L&#39;endpoint API utilizzato in questa guida è parte dell&#39; [[!DNL Observability Insights] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml). Prima di continuare, consultate la guida [introduttiva per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente chiamate a qualsiasi](./getting-started.md) [!DNL Experience Platform] API.

## Recuperare le metriche di osservabilità

Potete recuperare le metriche di osservabilità effettuando una richiesta di GET all&#39; `/metrics` endpoint nell&#39; [!DNL Observability Insights] API.

**Formato API**

Quando si utilizza l&#39; `/metrics` endpoint, è necessario fornire almeno un parametro di richiesta della metrica. Altri parametri di query sono facoltativi per filtrare i risultati.

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
| `{ID}` | Identificatore per una particolare [!DNL Platform] risorsa di cui si desidera esporre le metriche. Questo ID può essere facoltativo, obbligatorio o non applicabile a seconda delle metriche utilizzate. Vedi l’ [appendice](#available-metrics) per un elenco delle metriche disponibili, nonché gli ID supportati (obbligatori e facoltativi) per ciascuna metrica. |
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