---
title: Endpoint API esportazione eventi di controllo
description: Scopri come esportare eventi di controllo in Experience Platform utilizzando l’API Audit Query.
source-git-commit: 5b3459711f41430977f9d7b06f8b35801739207c
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# Esportare un elenco di eventi di controllo

Puoi recuperare i dati degli eventi effettuando una richiesta GET al `/audit/export` endpoint, specificando gli eventi da recuperare nel payload.

**Formato API**

```http
GET /audit/export
```

| Parametro | Descrizione |
| --------- | ----------- |
| `timestamp` | Quando si filtra per marca temporale, è consigliabile utilizzare un intervallo utilizzando gli operatori > e &lt; anziché un valore esatto. <br/>Esempio: ?property=timestamp&lt;2020-02-08T02:46:48.610862Z&amp;property=timestamp>2020-01-01T02:46:48,610862Z. |
| `status` | Lo stato dell’azione. Uno stato può essere uno dei seguenti: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |
| `action` | Il tipo di azione registrata per l&#39;evento. Un’azione può essere una delle seguenti: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `user` | Utente che ha eseguito l’evento. |
| `assetType` | Il tipo di risorsa Platform su cui è stata eseguita l’azione. |

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**Risposta**

I risultati vengono generati in un file CSV da esportare. Una risposta corretta restituisce HTTP 307 senza corpo di risposta. Nella sezione `Location` intestazione di risposta.
