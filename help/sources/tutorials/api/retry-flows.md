---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;
title: Esecuzione del flusso di dati di nuovo non riuscito
description: Questa esercitazione descrive i passaggi su come riprovare l’esecuzione di un flusso di dati non riuscito utilizzando l’API del servizio di flusso
source-git-commit: dfb95f457d7ddb730950159165ed85b2f532f9ab
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 3%

---

# Esecuzione del flusso di dati non riuscita del nuovo tentativo

>[!IMPORTANT]
>
>Il supporto per il nuovo tentativo di esecuzione di un flusso di dati non riuscito è disponibile per le origini batch. È possibile riprovare solo le esecuzioni del flusso di dati che non sono riuscite.

Questa esercitazione descrive i passaggi su come riprovare l&#39;esecuzione di un flusso di dati non riuscito utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../landing/api-guide.md).

## Riprovare a eseguire un flusso di dati non riuscito

Per riprovare l’esecuzione di un flusso di dati non riuscito, invia una richiesta POST al `/runs` l&#39;endpoint fornisce l&#39;ID di esecuzione del flusso di dati e il `re-trigger` come parte dei parametri di query.

**Formato API**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| Parametro | Descrizione |
| --- | --- |
| `{RUN_ID}` | L&#39;ID di esecuzione corrispondente all&#39;esecuzione del flusso di dati che si desidera riprovare. |
| `op` | Operazione che determina l&#39;azione da eseguire. Per riprovare l&#39;esecuzione di un flusso di dati non riuscito, è necessario specificare `re-trigger` come operazione. |

**Richiesta**

La richiesta seguente prova nuovamente l&#39;esecuzione del flusso di dati per l&#39;ID di esecuzione `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs/4fb0418e-1804-45d6-8d56-dd51f05c0baf/action?op=re-trigger' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
```

**Risposta**

Una risposta corretta restituisce un ID di esecuzione di flusso appena creato e la versione di tag corrispondente.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
