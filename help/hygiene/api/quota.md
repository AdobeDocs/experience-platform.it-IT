---
title: Endpoint API quota
description: L’endpoint /quota nell’API di igiene dei dati ti consente di monitorare l’utilizzo dell’igiene dei dati rispetto ai limiti di quota mensili della tua organizzazione per ogni tipo di processo.
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 1c6a5df6473e572cae88a5980fe0db9dfcf9944e
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 2%

---

# Endpoint quota

>[!IMPORTANT]
>
>Le funzionalità di igiene dei dati in Adobe Experience Platform sono attualmente disponibili solo per le organizzazioni che hanno acquistato **Schermo sanitario Adobe** o **Adobe Privacy &amp; Security Shield**.

Il `/quota` L’endpoint nell’API di igiene dei dati consente di monitorare l’utilizzo dell’igiene dei dati rispetto ai limiti di quota della tua organizzazione per ogni tipo di processo.

Le quote vengono applicate per ogni tipo di processo di igiene dei dati nei seguenti modi:

* Le eliminazioni e gli aggiornamenti dei record sono limitati a un determinato numero di richieste al mese.
* Le scadenze dei set di dati hanno un limite fisso per il numero di processi attivi simultaneamente, indipendentemente da quando verranno eseguite.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’API di igiene dei dati. Prima di continuare, controlla [panoramica](./overview.md) per le seguenti informazioni:

* Collegamenti alla documentazione correlata
* Guida alla lettura delle chiamate API di esempio in questo documento
* Informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente chiamate a qualsiasi API Experience Platform

## Elenca quote {#list}

È possibile visualizzare le informazioni sulle quote della propria organizzazione effettuando una richiesta di GET al `/quota` endpoint.

**Formato API**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUOTA_TYPE}` | Parametro di query facoltativo che specifica il tipo di quota da recuperare. In caso negativo `quotaType` Se viene fornito il parametro, tutti i valori di quota vengono restituiti nella risposta API. I valori di tipo accettati includono:<ul><li>`expirationDatasetQuota`: scadenze del set di dati</li><li>`deleteIdentityWorkOrderDatasetQuota`: eliminazioni record</li><li>`fieldUpdateWorkOrderDatasetQuota`: Aggiornamenti record</li></ul> |

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

In caso di esito positivo, la risposta restituisce i dettagli delle quote di igiene dei dati.

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
      "description": "The number of Record Delete Work Order requests for the organization for this month.",
      "consumed": 390,
      "quota": 10000
    }
  ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `quotas` | Elenca le informazioni sulla quota per ogni tipo di processo di igiene dei dati. Ogni oggetto quota contiene le proprietà seguenti:<ul><li>`name`: tipo di processo di igiene dei dati:<ul><li>`expirationDatasetQuota`: scadenze del set di dati</li><li>`deleteIdentityWorkOrderDatasetQuota`: eliminazioni record</li></ul></li><li>`description`: descrizione del tipo di processo di igiene dei dati.</li><li>`consumed`: numero di processi di questo tipo eseguiti nel periodo mensile corrente.</li><li>`quota`: limite di quota per questo tipo di processo. Per le eliminazioni e gli aggiornamenti dei record, rappresenta il numero di processi che è possibile eseguire per ogni periodo mensile. Per le scadenze dei set di dati, rappresenta il numero di processi che possono essere attivi contemporaneamente in un dato momento.</li></ul> |

{style="table-layout:auto"}
