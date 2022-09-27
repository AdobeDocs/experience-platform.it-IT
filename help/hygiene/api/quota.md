---
title: Endpoint API per la quota
description: L’endpoint /quota nell’API di igiene dati consente di monitorare l’utilizzo dell’igiene dei dati in base ai limiti della quota mensile della tua organizzazione per ogni tipo di lavoro.
source-git-commit: 364ada0c354ddba8a855945f4f806f5600f21416
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 3%

---

# Endpoint di quota

>[!IMPORTANT]
>
>Le funzionalità di igiene dei dati in Adobe Experience Platform sono attualmente disponibili solo per le organizzazioni che hanno acquistato Healthcare Shield.

La `/quota` l’endpoint nell’API di igiene dati consente di monitorare l’utilizzo dell’igiene dei dati in base ai limiti di quota della tua organizzazione per ogni tipo di processo.

Le quote vengono applicate per ciascun tipo di lavoro di igiene dei dati nei seguenti modi:

* Le eliminazioni dal consumatore e gli aggiornamenti dei campi sono limitati a un certo numero di richieste ogni mese.
* Le scadenze del set di dati hanno un limite fisso per il numero di processi contemporaneamente attivi, indipendentemente da quando verranno eseguite le scadenze.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’API di igiene dei dati. Prima di continuare, controlla la [panoramica](./overview.md) per le seguenti informazioni:

* Collegamenti alla relativa documentazione
* Guida alla lettura delle chiamate API di esempio in questo documento
* Informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente chiamate a qualsiasi API di Experience Platform

## Elencare quote {#list}

Puoi visualizzare le informazioni sulla quota della tua organizzazione effettuando una richiesta di GET al `/quota` punto finale.

**Formato API**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUOTA_TYPE}` | Parametro di query facoltativo che specifica il tipo di quota da recuperare. Se no `quotaType` viene fornito il parametro , tutti i valori di quota vengono restituiti nella risposta API. I valori di tipo accettati includono:<ul><li>`expirationDatasetQuota`: Scadenza set di dati</li><li>`deleteIdentityWorkOrderDatasetQuota`: Cancellazioni dal consumo</li><li>`fieldUpdateWorkOrderDatasetQuota`: Aggiornamenti dei campi</li></ul> |

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

Una risposta corretta restituisce i dettagli delle quote di igiene dei dati.

```json
{
  "quotas": [
    {
      "name": "expirationDatasetQuota",
      "description": "The number of concurrently active Expiration Dataset Delete Work Order requests for the organization.",
      "consumed": 3154,
      "quota": 10000
    },
    {
      "name": "deleteIdentityWorkOrderQuota",
      "description": "The number of Consumer Delete Work Order requests for the organization for this month.",
      "consumed": 390,
      "quota": 10000
    }
  ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `quotas` | Elenca le informazioni sulle quote per ogni tipo di processo di igiene dei dati. Ogni oggetto quota contiene le seguenti proprietà:<ul><li>`name`: Tipo di lavoro per l&#39;igiene dei dati:<ul><li>`expirationDatasetQuota`: Scadenza set di dati</li><li>`deleteIdentityWorkOrderDatasetQuota`: Cancellazioni dal consumo</li></ul></li><li>`description`: Descrizione del tipo di processo di igiene dei dati.</li><li>`consumed`: Il numero di processi di questo tipo eseguiti nel periodo mensile corrente.</li><li>`quota`: Limite di quota per questo tipo di processo. Per le eliminazioni consumer e gli aggiornamenti dei campi, questo rappresenta il numero di processi che possono essere eseguiti per ogni periodo mensile. Per le scadenze dei set di dati, questo rappresenta il numero di processi che possono essere contemporaneamente attivi in un dato momento.</li></ul> |

{style=&quot;table-layout:auto&quot;}
