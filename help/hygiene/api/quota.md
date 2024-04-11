---
title: Endpoint API quota
description: L’endpoint /quota nell’API di igiene dei dati consente di monitorare l’utilizzo di Advanced Data Lifecycle Management rispetto ai limiti di quota mensili dell’organizzazione per ogni tipo di processo.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 48a83e2b615fc9116a93611a5e6a8e7f78cb4dee
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 2%

---

# Endpoint quota

Il `/quota` L’endpoint nell’API di igiene dei dati consente di monitorare l’utilizzo di Advanced Data Lifecycle Management rispetto ai limiti di quota della tua organizzazione per ogni tipo di processo.

Le quote vengono applicate per ogni tipo di processo del ciclo di vita dei dati nei seguenti modi:

* Le eliminazioni e gli aggiornamenti dei record sono limitati a un determinato numero di richieste al mese.
* Le scadenze dei set di dati hanno un limite fisso per il numero di processi attivi simultaneamente, indipendentemente da quando verranno eseguite.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’API di igiene dei dati. Prima di continuare, controlla [panoramica](./overview.md) per le seguenti informazioni:

* Collegamenti alla documentazione correlata
* Guida alla lettura delle chiamate API di esempio in questo documento
* Informazioni importanti sulle intestazioni necessarie per effettuare chiamate a qualsiasi API Experienci Platform

## Elenca quote {#list}

È possibile visualizzare le informazioni sulle quote della propria organizzazione effettuando una richiesta di GET al `/quota` endpoint.

**Formato API**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUOTA_TYPE}` | Parametro di query facoltativo che specifica il tipo di quota da recuperare. In caso negativo `quotaType` Se viene fornito il parametro, tutti i valori di quota vengono restituiti nella risposta API. I valori di tipo accettati includono:<ul><li>`datasetExpirationQuota`: questo oggetto mostra il numero di scadenze dei set di dati attivi simultaneamente per l’organizzazione e la tolleranza totale di scadenze. </li><li>`dailyConsumerDeleteIdentitiesQuota`: questo oggetto mostra il numero totale di richieste di cancellazione dei record effettuate dall’organizzazione oggi e la quota giornaliera totale.<br>Nota: vengono conteggiate solo le richieste accettate. Se un ordine di lavoro viene rifiutato perché non supera la convalida, le eliminazioni di identità non vengono conteggiate in base alla quota.</li><li>`monthlyConsumerDeleteIdentitiesQuota`: questo oggetto mostra il numero totale di richieste di cancellazione dei record effettuate dall’organizzazione questo mese e l’indennità mensile totale.</li><li>`monthlyUpdatedFieldIdentitiesQuota`: questo oggetto mostra il numero totale di richieste di aggiornamenti dei record effettuate dall’organizzazione questo mese e l’indennità mensile totale.</li></ul> |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/quota \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli delle quote del ciclo di vita dei dati.

```json
{
  "quotas": [
    {
      "name": "datasetExpirationQuota",
      "description": "The number of concurrently active Expiration Dataset Delete in all workorder requests for the organization.",
      "consumed": 12,
      "quota": 50
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for today.",
      "consumed": 0,
      "quota": 600000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for this month.",
      "consumed": 841,
      "quota": 600000
    },
    {
      "name": "monthlyUpdatedFieldIdentitiesQuota",
      "description": "The consumed number of updated identities in all workorder requests for the organization for this month.",
      "consumed": 0,
      "quota": 0
    }
  ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `quotas` | Elenca le informazioni sulla quota per ogni tipo di processo del ciclo di vita dei dati. Ogni oggetto quota contiene le proprietà seguenti:<ul><li>`name`: tipo di processo del ciclo di vita dei dati:<ul><li>`expirationDatasetQuota`: scadenze del set di dati</li><li>`deleteIdentityWorkOrderDatasetQuota`: eliminazioni record</li></ul></li><li>`description`: descrizione del tipo di processo del ciclo di vita dei dati.</li><li>`consumed`: numero di processi di questo tipo eseguiti nel periodo corrente. Il nome dell&#39;oggetto indica il periodo di quota.</li><li>`quota`: l’assegnazione per questo tipo di mansione per la tua organizzazione. Per le eliminazioni e gli aggiornamenti dei record, la quota rappresenta il numero di processi che è possibile eseguire per ogni periodo mensile. Per le scadenze dei set di dati, la quota rappresenta il numero di processi che possono essere attivi contemporaneamente in un dato momento.</li></ul> |

{style="table-layout:auto"}
