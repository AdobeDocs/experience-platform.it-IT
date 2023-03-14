---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;
title: Ritenta esecuzioni flusso di dati non riuscite
description: Questa esercitazione descrive i passaggi per ritentare l’esecuzione di un flusso di dati non riuscito tramite l’API del servizio Flusso
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: a9887535b12b8c4aeb39bb5a6646da88db4f0308
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 3%

---

# Riprova esecuzioni flusso di dati non riuscite

>[!IMPORTANT]
>
>Per le origini batch è disponibile il supporto per ritentare le esecuzioni dei flussi di dati non riuscite. Puoi riprovare solo le esecuzioni del flusso di dati che non sono riuscite.

Questa esercitazione descrive i passaggi per ritentare l’esecuzione di un flusso di dati non riuscito utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../landing/api-guide.md).

## Riprovare un&#39;esecuzione del flusso di dati non riuscita

Per ritentare l’esecuzione di un flusso di dati non riuscito, invia una richiesta POST al `/runs` fornendo l’ID di esecuzione del flusso di dati e il `re-trigger` come parte dei parametri di query.

**Formato API**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| Parametro | Descrizione |
| --- | --- |
| `{RUN_ID}` | ID di esecuzione che corrisponde all’esecuzione del flusso di dati che desideri riprovare. |
| `op` | Operazione che determina l&#39;azione da eseguire. Per ritentare l’esecuzione di un flusso di dati non riuscito, è necessario specificare `re-trigger` come operazione. |

**Richiesta**

La richiesta seguente ritenta l’esecuzione del flusso di dati per l’ID esecuzione `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

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

In caso di esito positivo, la risposta restituisce l’ID di esecuzione di un flusso appena creato e la versione di etag corrispondente.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
