---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Endpoint API delle metriche
description: Scopri come recuperare le metriche di osservabilità in Experience Platform utilizzando l’API Observability Insights.
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
source-git-commit: 39eda018611d0244eaff908e924afa93dc46e14d
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 4%

---

# Endpoint &quot;metrics&quot;

Le metriche di osservabilità forniscono informazioni approfondite sulle statistiche di utilizzo, le tendenze storiche e gli indicatori di prestazioni per varie funzioni di Adobe Experience Platform. L&#39;endpoint `/metrics` in [!DNL Observability Insights API] consente di recuperare in modo programmatico i dati delle metriche per l&#39;attività dell&#39;organizzazione in [!DNL Platform].

>[!NOTE]
>
>La versione precedente dell’endpoint delle metriche (V1) è stata dichiarata obsoleta. Questo documento si concentra esclusivamente sulla versione corrente (V2). Per informazioni dettagliate sull&#39;endpoint V1 per le implementazioni legacy, consulta il [riferimento API](https://www.adobe.io/experience-platform-apis/references/observability-insights/#operation/retrieveMetricsV1).

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39;[[!DNL Observability Insights] API](https://www.adobe.io/experience-platform-apis/references/observability-insights/). Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API [!DNL Experience Platform].

## Recuperare le metriche di osservabilità

Per recuperare i dati delle metriche, devi eseguire una richiesta POST all&#39;endpoint `/metrics`, specificando le metriche da recuperare nel payload.

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
            "aggregator": "sum"
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
| `start` | La prima data/ora da cui recuperare i dati della metrica. |
| `end` | La data/ora più recente da cui recuperare i dati della metrica. |
| `granularity` | Un campo facoltativo che indica l’intervallo di tempo per cui dividere i dati della metrica. Ad esempio, un valore di `DAY` restituisce le metriche per ogni giorno compreso tra la data `start` e `end`, mentre un valore di `MONTH` raggrupperebbe i risultati delle metriche per mese. |
| `metrics` | Array di oggetti, uno per ogni metrica da recuperare. |
| `name` | Il nome di una metrica riconosciuta da Observability Insights. Per un elenco completo dei nomi delle metriche accettate, vedere l&#39;[appendice](#available-metrics). |
| `filters` | Campo facoltativo che consente di filtrare le metriche per set di dati specifici. Il campo è un array di oggetti (uno per ciascun filtro), con ogni oggetto contenente le seguenti proprietà: <ul><li>`name`: tipo di entità su cui filtrare le metriche. Attualmente, è supportato solo `dataSets`.</li><li>`value`: ID di uno o più set di dati. È possibile fornire più ID di set di dati come una singola stringa, con ogni ID separato da caratteri di barra verticali (`\|`).</li><li>`groupBy`: se impostato su true, indica che il `value` corrispondente rappresenta più set di dati i cui risultati della metrica devono essere restituiti separatamente. Se impostato su false, i risultati delle metriche per tali set di dati sono raggruppati.</li></ul> |
| `aggregator` | Specifica la funzione di aggregazione da utilizzare per raggruppare più record di serie temporali in singoli risultati. Gli aggregatori attualmente supportati sono min, max, sum e avg a seconda della definizione della metrica. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce i punti dati risultanti per le metriche e i filtri specificati nella richiesta.

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
| `metricResponses` | Matrice i cui oggetti rappresentano ciascuna delle metriche specificate nella richiesta. Ogni oggetto contiene informazioni sulla configurazione del filtro e sui dati delle metriche restituiti. |
| `metric` | Il nome di una delle metriche fornite nella richiesta. |
| `filters` | Configurazione del filtro per la metrica specificata. |
| `datapoints` | Matrice i cui oggetti rappresentano i risultati della metrica e dei filtri specificati. Il numero di oggetti nell’array dipende dalle opzioni di filtro fornite nella richiesta. Se non sono stati forniti filtri, l’array conterrà solo un singolo oggetto che rappresenta tutti i set di dati. |
| `groupBy` | Se nella proprietà `filter` per una metrica sono stati specificati più set di dati e l&#39;opzione `groupBy` è stata impostata su true nella richiesta, questo oggetto conterrà l&#39;ID del set di dati a cui si applica la proprietà `dps` corrispondente.<br><br>Se questo oggetto appare vuoto nella risposta, la proprietà `dps` corrispondente si applica a tutti i set di dati forniti nell&#39;array `filters` (o a tutti i set di dati in [!DNL Platform] se non sono stati forniti filtri). |
| `dps` | I dati restituiti per la metrica, il filtro e l’intervallo di tempo specificati. Ogni chiave in questo oggetto rappresenta una marca temporale con un valore corrispondente per la metrica specificata. Il periodo di tempo tra ciascun punto dati dipende dal valore `granularity` specificato nella richiesta. |

{style="table-layout:auto"}

## Appendice

La sezione seguente contiene informazioni aggiuntive sull&#39;utilizzo dell&#39;endpoint `/metrics`.

### Metriche disponibili {#available-metrics}

Nelle tabelle seguenti sono elencate tutte le metriche esposte da [!DNL Observability Insights], suddivise per il servizio [!DNL Platform]. Ogni metrica include una descrizione e un parametro di query dell’ID accettato.

>[!NOTE]
>
>Tutti i parametri di query ID elencati sono facoltativi, se non diversamente specificato.

#### [!DNL Data Ingestion] {#ingestion}

La tabella seguente illustra le metriche per Adobe Experience Platform [!DNL Data Ingestion]. Le metriche in **bold** sono metriche di acquisizione in streaming.

| Metrica Approfondimenti | Descrizione | Parametro query ID |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.size | Dimensione cumulativa di tutti i dati acquisiti per un set di dati per o tutti i set di dati. | ID set di dati |
| timeseries.ingestion.dataset.dailysize | Dimensione dei dati acquisiti su base giornaliera per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.ingestion.dataset.batchfailed.count | Numero di batch non riusciti per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.ingestion.dataset.batchsuccess.count | Numero di batch acquisiti per un set di dati o per tutti. | ID set di dati |
| timeseries.ingestion.dataset.recordsuccess.count | Numero di record acquisiti per un set di dati o per tutti. | ID set di dati |
| **serie temporali.data.collection.validation.category.presence.count** | Numero totale di messaggi di &quot;presenza&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati |
| **serie temporali.data.collection.inlet.total.messages.received** | Numero totale di messaggi ricevuti per un’entrata dati o per tutti gli ingressi dati. | ID ingresso |
| **serie temporali.data.collection.inlet.total.messages.size.received** | Dimensione totale dei dati ricevuti per un’entrata dati o per tutti gli ingressi dati. | ID ingresso |
| **serie temporali.data.collection.inlet.success** | Numero totale di chiamate HTTP riuscite a un’entrata dati o a tutte le entrate dati. | ID ingresso |
| **serie temporali.data.collection.inlet.failure** | Numero totale di chiamate HTTP non riuscite a un’entrata dati o a tutte le entrate dati. | ID ingresso |

{style="table-layout:auto"}

#### [!DNL Identity Service] {#identity}

La tabella seguente illustra le metriche per Adobe Experience Platform [!DNL Identity Service].

| Metrica Approfondimenti | Descrizione | Parametro query ID |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Numero di record scritti nell&#39;origine dati da [!DNL Identity Service], per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.identity.dataset.recordfailed.count | Numero di record non riusciti da [!DNL Identity Service], per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Numero di record di identità ignorati. | ID organizzazione |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Numero di identità univoche memorizzate nel grafico delle identità per la tua organizzazione. | N/D |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Numero di identità univoche memorizzate nel grafico delle identità per uno spazio dei nomi. | ID dello spazio dei nomi (**Obbligatorio**) |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Numero di identità univoche memorizzate nel grafo delle identità per l’organizzazione per una particolare forza del grafo (&quot;sconosciuta&quot;, &quot;debole&quot; o &quot;forte&quot;). | Forza del grafico (**Obbligatorio**) |

{style="table-layout:auto"}

#### [!DNL Real-Time Customer Profile] {#profile}

La tabella seguente illustra le metriche per [!DNL Real-Time Customer Profile].

| Metrica Approfondimenti | Descrizione | Parametro query ID |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Numero di record letti da [!DNL Data Lake] da [!DNL Profile], per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.profiles.dataset.recordsuccess.count | Numero di record scritti nell&#39;origine dati da [!DNL Profile], per un set di dati o per tutti i set di dati. | ID set di dati |
| timeseries.profiles.dataset.batchsuccess.count | Numero di [!DNL Profile] batch acquisiti per un set di dati o per tutti i set di dati. | ID set di dati |

{style="table-layout:auto"}

### Messaggi di errore

Le risposte dall&#39;endpoint `/metrics` possono restituire messaggi di errore in determinate condizioni. Questi messaggi di errore vengono restituiti nel seguente formato:

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
| `title` | Stringa contenente il messaggio di errore e il motivo potenziale per cui si è verificato. |
| `report` | Contiene informazioni contestuali sull’errore, inclusa la sandbox e l’organizzazione utilizzata nell’operazione che l’ha attivato. |

{style="table-layout:auto"}

Nella tabella seguente sono elencati i diversi codici di errore che possono essere restituiti dall’API:

| Codice errore | Titolo | Descrizione |
| --- | --- | --- |
| `INSGHT-1000-400` | Payload di richiesta non valido | Si è verificato un errore nel payload della richiesta. Assicurati di avere la stessa formattazione del payload mostrata [sopra](#v2). Questo errore può essere attivato da uno dei motivi seguenti:<ul><li>Campi obbligatori mancanti come `aggregator`</li><li>Metriche non valide</li><li>La richiesta contiene un aggregatore non valido</li><li>Una data di inizio segue una data di fine</li></ul> |
| `INSGHT-1001-400` | Query delle metriche non riuscita | Si è verificato un errore durante il tentativo di eseguire una query sul database delle metriche a causa di una richiesta non valida o perché la query stessa non è analizzabile. Prima di riprovare, assicurati che la richiesta sia formattata correttamente. |
| `INSGHT-1001-500` | Query delle metriche non riuscita | Si è verificato un errore durante il tentativo di eseguire una query sul database delle metriche a causa di un errore del server. Riprova e, se il problema persiste, contatta l’assistenza Adobe. |
| `INSGHT-1002-500` | Errore di servizio | Impossibile elaborare la richiesta a causa di un errore interno. Riprova e, se il problema persiste, contatta l’assistenza Adobe. |
| `INSGHT-1003-401` | Errore di convalida della sandbox | Impossibile elaborare la richiesta a causa di un errore di convalida della sandbox. Prima di riprovare a eseguire la richiesta, verifica che il nome della sandbox fornito nell&#39;intestazione `x-sandbox-name` rappresenti una sandbox valida e abilitata per la tua organizzazione. |

{style="table-layout:auto"}
