---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' informazioni sull''osservabilità del Adobe Experience Platform'
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 2%

---


# Panoramica sull&#39;osservabilità  Adobe Experience Platform

Observability Insights è una RESTful API che consente di esporre le metriche di osservabilità chiave nel  Adobe Experience Platform. Queste metriche forniscono informazioni approfondite sulle statistiche di [!DNL Platform] utilizzo, sui controlli dello stato dei [!DNL Platform] servizi, sulle tendenze storiche e sugli indicatori di prestazioni per diverse [!DNL Platform] funzionalità.

Questo documento illustra una chiamata di esempio all&#39;API Observability Insights. Per un elenco completo degli endpoint di osservabilità, fare riferimento al riferimento [API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml)Observability Insights.

## Introduzione

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione. Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione [sulla panoramica della](../sandboxes/home.md)sandbox.

* x-sandbox-name: `{SANDBOX_NAME}`

## Recuperare le metriche di osservabilità

Potete recuperare le metriche di osservabilità effettuando una richiesta GET all&#39; `/metrics` endpoint nell&#39;API Observability Insights.

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
| `{ID}` | Identificatore per una particolare [!DNL Platform] risorsa di cui si desidera esporre le metriche. Questo ID può essere facoltativo, obbligatorio o non applicabile a seconda delle metriche utilizzate. Per un elenco delle metriche disponibili, nonché degli ID supportati (obbligatori e facoltativi) per ciascuna metrica, consultate il documento di riferimento sulle metriche [](metrics.md)disponibili. |
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

## Passaggi successivi

Questo documento fornisce una panoramica dell&#39;API Observability Insights. Consultate il documento sulle metriche [](metrics.md) disponibili per un elenco completo delle metriche utilizzabili nell&#39;API.