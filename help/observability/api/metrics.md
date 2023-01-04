---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Endpoint API per le metriche
topic-legacy: developer guide
description: Scopri come recuperare le metriche di osservabilità in Experience Platform utilizzando l’API Observability Insights .
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 3%

---

# Endpoint metriche

Le metriche di osservabilità forniscono informazioni approfondite sulle statistiche di utilizzo, sulle tendenze della cronologia e sugli indicatori di prestazioni per varie funzioni di Adobe Experience Platform. La `/metrics` punto finale [!DNL Observability Insights API] consente di recuperare in modo programmatico i dati delle metriche per l’attività dell’organizzazione in [!DNL Platform].

>[!NOTE]
>
>La versione precedente dell’endpoint delle metriche (V1) è stata dichiarata obsoleta. Questo documento si concentra esclusivamente sulla versione corrente (V2). Per informazioni dettagliate sull’endpoint V1 per le implementazioni legacy, consulta [Riferimento API](https://www.adobe.io/experience-platform-apis/references/observability-insights/#operation/retrieveMetricsV1).

## Introduzione

L’endpoint API utilizzato in questa guida fa parte del [[!DNL Observability Insights] API](https://www.adobe.io/experience-platform-apis/references/observability-insights/). Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio presenti in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi [!DNL Experience Platform] API.

## Recupera metriche di osservabilità

Puoi recuperare i dati delle metriche effettuando una richiesta di POST al `/metrics` endpoint, specificando le metriche da recuperare nel payload.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `start` | La data/ora più recente da cui recuperare i dati delle metriche. |
| `end` | Data/ora più recente da cui recuperare i dati delle metriche. |
| `granularity` | Un campo facoltativo che indica l’intervallo di tempo per il quale dividere i dati delle metriche. Ad esempio, un valore di `DAY` restituisce le metriche per ogni giorno compreso tra `start` e `end` data, mentre un valore `MONTH` raggrupperebbe invece i risultati delle metriche per mese. Quando si utilizza questo campo, un `downsample` è inoltre necessario fornire la proprietà per indicare la funzione di aggregazione tramite la quale raggruppare i dati. |
| `metrics` | Matrice di oggetti, una per ogni metrica che si desidera recuperare. |
| `name` | Nome di una metrica riconosciuta da Observability Insights. Consulta la sezione [appendice](#available-metrics) per un elenco completo dei nomi delle metriche accettate. |
| `filters` | Un campo facoltativo che consente di filtrare le metriche in base a set di dati specifici. Il campo è una matrice di oggetti (uno per ogni filtro), con ogni oggetto contenente le seguenti proprietà: <ul><li>`name`: Il tipo di entità su cui filtrare le metriche. Attualmente, solo `dataSets` è supportato.</li><li>`value`: ID di uno o più set di dati. È possibile fornire più ID di set di dati come una singola stringa, con ogni ID separato da caratteri a barre verticali (`\|`).</li><li>`groupBy`: Quando è impostato su true, indica che il corrispondente `value` rappresenta più set di dati i cui risultati delle metriche devono essere restituiti separatamente. Se è impostato su false, i risultati delle metriche per tali set di dati sono raggruppati.</li></ul> |
| `aggregator` | Specifica la funzione di aggregazione da utilizzare per raggruppare più record serie temporali in singoli risultati. Per informazioni dettagliate sugli aggregati disponibili, consulta la sezione [Documentazione OpenTSDB](https://docs.w3cub.com/opentsdb/user_guide/query/aggregators). |
| `downsample` | Un campo facoltativo che consente di specificare una funzione di aggregazione per ridurre la frequenza di campionamento dei dati metrici ordinando i campi in intervalli (o &quot;bucket&quot;). L&#39;intervallo per il sottocampionamento è determinato dalla `granularity` proprietà. Per informazioni dettagliate sul downcampionamento, consulta la [Documentazione OpenTSDB](https://docs.w3cub.com/opentsdb/user_guide/query/aggregators). |

{style=&quot;table-layout:auto&quot;}

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
| `metricResponses` | Matrice i cui oggetti rappresentano ciascuna delle metriche specificate nella richiesta. Ogni oggetto contiene informazioni sulla configurazione del filtro e sui dati della metrica restituiti. |
| `metric` | Nome di una delle metriche fornite nella richiesta. |
| `filters` | La configurazione del filtro per la metrica specificata. |
| `datapoints` | Matrice i cui oggetti rappresentano i risultati della metrica e i filtri specificati. Il numero di oggetti nell’array dipende dalle opzioni di filtro fornite nella richiesta. Se non sono stati forniti filtri, la matrice conterrà solo un singolo oggetto che rappresenta tutti i set di dati. |
| `groupBy` | Se sono stati specificati più set di dati in `filter` per una metrica e `groupBy` è stata impostata su true nella richiesta, questo oggetto conterrà l&#39;ID del set di dati corrispondente `dps` si applica a.<br><br>Se l&#39;oggetto viene visualizzato vuoto nella risposta, il valore corrispondente `dps` si applica a tutti i set di dati forniti nella `filters` array (o tutti i set di dati in [!DNL Platform] se non sono stati forniti filtri). |
| `dps` | I dati restituiti per la metrica, il filtro e l’intervallo di tempo specificato. Ogni chiave in questo oggetto rappresenta una marca temporale con un valore corrispondente per la metrica specificata. Il periodo di tempo tra ciascun punto di dati dipende dal `granularity` valore specificato nella richiesta. |

{style=&quot;table-layout:auto&quot;}

## Appendice

La sezione seguente contiene informazioni aggiuntive sull’utilizzo delle `/metrics` punto finale.

### Metriche disponibili {#available-metrics}

Nelle tabelle seguenti sono elencate tutte le metriche esposte da [!DNL Observability Insights], suddivisi per [!DNL Platform] servizio. Ogni metrica include una descrizione e un parametro di query ID accettato.

>[!NOTE]
>
>Tutti i parametri di query ID elencati sono facoltativi, se non diversamente specificato.

#### [!DNL Data Ingestion] {#ingestion}

La tabella seguente delinea le metriche per Adobe Experience Platform [!DNL Data Ingestion]. Metriche in **audace** sono metriche di acquisizione in streaming.

| Metrica Approfondimenti | Descrizione | Parametro query ID |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.size | Dimensione cumulativa di tutti i dati acquisiti per un set di dati per o per tutti i set di dati. | ID set di dati |
| timeseries.ingestion.dataset.dailysize | Dimensione dei dati acquisiti su base giornaliera per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.ingestion.dataset.batchfailed.count | Numero di batch non riusciti per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.ingestion.dataset.batchsuccess.count | Numero di batch acquisiti per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.ingestion.dataset.recordsuccess.count | Numero di record acquisiti per un set di dati o per tutti i set di dati. | ID set di dati |
| **timeseries.data.collection.validation.category.presence.count** | Numero totale di messaggi &quot;presenza&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati |
| **timeseries.data.collection.inlet.total.messages.receive** | Numero totale di messaggi ricevuti per un’entrata dati o per tutte le entrate dati. | ID ingresso |
| **timeseries.data.collection.inlet.total.messages.size.receive** | Dimensione totale dei dati ricevuti per un’entrata dati o per tutte le entrate dati. | ID ingresso |
| **timeseries.data.collection.inlet.success** | Numero totale di chiamate HTTP riuscite a una singola entrata dati o a tutte le entrate dati. | ID ingresso |
| **timeseries.data.collection.inlet.failed** | Numero totale di chiamate HTTP non riuscite a una singola entrata dati o a tutte le entrate dati. | ID ingresso |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Identity Service] {#identity}

La tabella seguente delinea le metriche per Adobe Experience Platform [!DNL Identity Service].

| Metrica Approfondimenti | Descrizione | Parametro query ID |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Numero di record scritti nella relativa origine dati da [!DNL Identity Service], per un set di dati o tutti i set di dati. | ID set di dati |
| timeseries.identity.dataset.recordfailed.count | Numero di record non riusciti da [!DNL Identity Service], per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Numero di record di identità non riusciti da uno spazio dei nomi. | ID dello spazio dei nomi (**Obbligatorio**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Numero di record di identità ignorati da uno spazio dei nomi. | ID dello spazio dei nomi (**Obbligatorio**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Numero di identità univoche memorizzate nel grafico delle identità per la tua organizzazione IMS. | N/D |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Numero di identità univoche memorizzate nel grafico delle identità per uno spazio dei nomi. | ID dello spazio dei nomi (**Obbligatorio**) |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Numero di identità univoche memorizzate nel grafico delle identità per la tua organizzazione IMS per una particolare forza grafico (&quot;sconosciuto&quot;, &quot;debole&quot; o &quot;forte&quot;). | Forza del grafico (**Obbligatorio**) |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Real-Time Customer Profile] {#profile}

La tabella seguente delinea le metriche per [!DNL Real-Time Customer Profile].

| Metrica Approfondimenti | Descrizione | Parametro query ID |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Numero di record letti dal [!DNL Data Lake] da [!DNL Profile], per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.profiles.dataset.recordsuccess.count | Numero di record scritti nella relativa origine dati da [!DNL Profile], per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.profiles.dataset.batchsuccess.count | Numero di [!DNL Profile] batch acquisiti per un set di dati o per tutti i set di dati. | ID set di dati |

{style=&quot;table-layout:auto&quot;}

### Messaggi di errore

Risposte da `/metrics` l’endpoint può restituire messaggi di errore in determinate condizioni. Questi messaggi di errore vengono restituiti nel seguente formato:

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{ORG_ID}"
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
| `title` | Una stringa contenente il messaggio di errore e il motivo potenziale per cui si è verificato. |
| `report` | Contiene informazioni contestuali sull’errore, tra cui la sandbox e l’organizzazione IMS utilizzata nell’operazione che l’ha attivato. |

{style=&quot;table-layout:auto&quot;}

Nella tabella seguente sono elencati i diversi codici di errore che possono essere restituiti dall’API:

| Codice di errore | Title | Descrizione |
| --- | --- | --- |
| `INSGHT-1000-400` | Payload della richiesta non valido | Errore nel payload della richiesta. Assicurati di corrispondere esattamente alla formattazione del payload come mostrato [sopra](#v2). Uno dei possibili motivi può attivare questo errore:<ul><li>Campi obbligatori mancanti, ad esempio `aggregator`</li><li>Metriche non valide</li><li>La richiesta contiene un aggregatore non valido</li><li>Una data di inizio ha luogo dopo una data di fine</li></ul> |
| `INSGHT-1001-400` | Query metriche non riuscita | Errore durante il tentativo di eseguire query sul database delle metriche a causa di una richiesta errata o dell&#39;annullamento della parsabilità della query stessa. Assicurati che la richiesta sia formattata correttamente prima di riprovare. |
| `INSGHT-1001-500` | Query metriche non riuscita | Errore durante il tentativo di eseguire query sul database delle metriche a causa di un errore del server. Riprovare la richiesta e, se il problema persiste, contattare il supporto Adobe. |
| `INSGHT-1002-500` | Errore del servizio | Impossibile elaborare la richiesta a causa di un errore interno. Riprovare la richiesta e, se il problema persiste, contattare il supporto Adobe. |
| `INSGHT-1003-401` | Errore di convalida sandbox | Impossibile elaborare la richiesta a causa di un errore di convalida sandbox. Assicurati che il nome della sandbox fornito nella `x-sandbox-name` header rappresenta una sandbox valida e abilitata per la tua organizzazione IMS prima di riprovare. |

{style=&quot;table-layout:auto&quot;}
