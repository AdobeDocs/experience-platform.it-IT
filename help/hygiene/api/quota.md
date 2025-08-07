---
title: Endpoint API quota
description: L’endpoint /quota nell’API di igiene dei dati consente di monitorare l’utilizzo di Advanced Data Lifecycle Management rispetto ai limiti di quota mensili dell’organizzazione per ogni tipo di processo.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 2c2907c5ed38ce4c87b1b73f96e1a0e64586cb97
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 2%

---

# Endpoint quota

Utilizza l&#39;endpoint `/quota` nell&#39;API di igiene dei dati per verificare l&#39;utilizzo corrente e i limiti della tua organizzazione. I contingenti variano in base alle autorizzazioni, ad esempio Privacy e scudo di sicurezza o Healthcare Shield.

Monitorare il consumo corrente delle quote per garantire la conformità ai limiti organizzativi per ogni tipo di processo.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’API di igiene dei dati. Prima di continuare, esaminare la [panoramica](./overview.md) per le seguenti informazioni:

* Collegamenti alla documentazione correlata
* Come leggere le chiamate API di esempio
* Intestazioni richieste per le chiamate API di Experience Platform

## Quote e timeline di elaborazione {#quotas}

Le richieste di cancellazione dei record sono soggette a quote e aspettative a livello di servizio in base al diritto alla licenza. Questi limiti si applicano sia alle richieste di eliminazione basate su API che su interfaccia utente.

>[!TIP]
>
>In questo documento viene illustrato come eseguire query sull&#39;utilizzo in base ai limiti basati sui diritti. Per una descrizione completa dei livelli di quota, dei diritti di eliminazione dei record e del comportamento di SLA, vedere i documenti [Eliminazione record basata sull&#39;interfaccia utente](../ui/record-delete.md#quotas) o [Eliminazione record basata su API](./workorder.md#quotas).

## Elenca quote {#list}

È possibile visualizzare le informazioni sulle quote della propria organizzazione effettuando una richiesta GET all&#39;endpoint `/quota`.

**Formato API**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

>[!NOTE]
>
>Il consumo delle quote viene ripristinato ogni giorno e ogni mese il 1° di ogni mese alle 00:00 GMT.
>
>Solo le richieste accettate vengono conteggiate per la quota. Gli ordini di lavorazione rifiutati non riducono la quota.

| Parametro | Descrizione |
| --- | --- |
| `{QUOTA_TYPE}` | Parametro di query facoltativo che specifica il tipo di quota da recuperare. Se non viene fornito alcun parametro `quotaType`, nella risposta API vengono restituiti tutti i valori di quota. I valori accettati includono:<ul><li>`datasetExpirationQuota`: il numero di scadenze del set di dati attivo e la tolleranza totale.</li><li>`dailyConsumerDeleteIdentitiesQuota`: numero di record eliminati oggi e quota giornaliera.</li><li>`monthlyConsumerDeleteIdentitiesQuota`: numero di record eliminati questo mese e quota mensile.</li></ul> |

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
      "description": "The number of concurrently active dataset-expiration delete operations in all work order requests for the organization.",
      "consumed": 11,
      "quota": 75
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization for today.",
      "consumed": 314,
      "quota": 700000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization this month.",
      "consumed": 2764,
      "quota": 12000000
    }
  ]
}
```

| Proprietà | Descrizione |
| -------- | ------- |
| `quotas` | Elenca le informazioni sulla quota per ogni tipo di processo del ciclo di vita dei dati. Ogni oggetto quota contiene le proprietà seguenti:<ul><li>`name`</li><li>`description`</li><li>`consumed`</li><li>`quota`</li></ul> |
| `name` | Identificatore del tipo di quota. |
| `description` | Descrizione dei limiti di quota. |
| `consumed` | Quantità di quota attualmente utilizzata. La quantità consumata viene ripristinata il 1° del mese alle 00:00 GMT e 00:00 GMT per la quota giornaliera. |
| `quota` | L&#39;assegnazione massima di questo tipo di quota per l&#39;organizzazione. |
