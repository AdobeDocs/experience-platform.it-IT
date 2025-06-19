---
title: Endpoint API quota
description: L’endpoint /quota nell’API di igiene dei dati consente di monitorare l’utilizzo di Advanced Data Lifecycle Management rispetto ai limiti di quota mensili dell’organizzazione per ogni tipo di processo.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 4d34ae1885f8c4b05c7bb4ff9de9c0c0e26154bd
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 2%

---

# Endpoint quota

L&#39;endpoint `/quota` nell&#39;API di igiene dei dati consente di monitorare l&#39;utilizzo di Advanced Data Lifecycle Management rispetto ai limiti di quota dell&#39;organizzazione per ogni tipo di processo.

L’utilizzo delle quote viene monitorato per ogni tipo di processo del ciclo di vita dei dati. I limiti di quota effettivi dipendono dai diritti dell&#39;organizzazione e possono essere rivisti periodicamente. Le scadenze dei set di dati sono soggette a un limite rigido sul numero di processi attivi simultaneamente.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’API di igiene dei dati. Prima di continuare, esaminare la [panoramica](./overview.md) per le seguenti informazioni:

* Collegamenti alla documentazione correlata
* Guida alla lettura delle chiamate API di esempio in questo documento
* Informazioni importanti sulle intestazioni necessarie per effettuare chiamate a qualsiasi API di Experience Platform

## Quote e timeline di elaborazione {#quotas}

Le richieste di cancellazione dei record sono soggette a quote e aspettative a livello di servizio in base al diritto alla licenza. Questi limiti si applicano sia alle richieste di eliminazione basate su API che su interfaccia utente.

>[!TIP]
> 
>In questo documento viene illustrato come eseguire query sull&#39;utilizzo in base ai limiti basati sui diritti. Per una descrizione completa dei livelli di quota, dei diritti di eliminazione dei record e del comportamento di SLA, vedere i documenti [Eliminazione record basata sull&#39;interfaccia utente](../ui/record-delete.md#quotas) o[Eliminazione record basata su API](./workorder.md#quotas).

## Elenca quote {#list}

È possibile visualizzare le informazioni sulle quote della propria organizzazione effettuando una richiesta GET all&#39;endpoint `/quota`.

**Formato API**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUOTA_TYPE}` | Parametro di query facoltativo che specifica il tipo di quota da recuperare. Se non viene fornito alcun parametro `quotaType`, nella risposta API vengono restituiti tutti i valori di quota. I valori di tipo accettati includono:<ul><li>`datasetExpirationQuota`: questo oggetto mostra il numero di scadenze di set di dati attivi simultaneamente per l&#39;organizzazione e la tolleranza totale di scadenze. </li><li>`dailyConsumerDeleteIdentitiesQuota`: questo oggetto mostra il numero totale di richieste di eliminazione record effettuate dall&#39;organizzazione oggi e la quota giornaliera totale.<br>Nota: vengono conteggiate solo le richieste accettate. Se un ordine di lavoro viene rifiutato perché non supera la convalida, le eliminazioni di identità non vengono conteggiate in base alla quota.</li><li>`monthlyConsumerDeleteIdentitiesQuota`: questo oggetto mostra il numero totale di richieste di eliminazione dei record effettuate dall&#39;organizzazione questo mese e l&#39;indennità mensile totale.</li><li>`monthlyUpdatedFieldIdentitiesQuota`: questo oggetto mostra il numero totale di richieste di aggiornamenti dei record effettuate dall&#39;organizzazione questo mese e l&#39;indennità mensile totale.</li></ul> |

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
      "quota": 1000000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for this month.",
      "consumed": 841,
      "quota": 2000000
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
| -------- | ------- |
| `quotas` | Elenca le informazioni sulla quota per ogni tipo di processo del ciclo di vita dei dati. Ogni oggetto quota contiene le proprietà seguenti:<ul><li>`name`: tipo di processo del ciclo di vita dei dati:<ul><li>`expirationDatasetQuota`: scadenze set di dati</li><li>`deleteIdentityWorkOrderDatasetQuota`: eliminazioni record</li></ul></li><li>`description`: descrizione del tipo di processo del ciclo di vita dei dati.</li><li>`consumed`: numero di processi di questo tipo eseguiti nel periodo corrente. Il nome dell&#39;oggetto indica il periodo di quota.</li><li>`quota`: l&#39;assegnazione per questo tipo di processo per la tua organizzazione. Per le eliminazioni e gli aggiornamenti dei record, la quota rappresenta il numero di processi che è possibile eseguire per ogni periodo mensile. Per le scadenze dei set di dati, la quota rappresenta il numero di processi che possono essere attivi contemporaneamente in un dato momento.</li></ul> |
