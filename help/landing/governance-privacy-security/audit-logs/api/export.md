---
title: Endpoint API esportazione eventi di controllo
description: Scopri come esportare gli eventi di audit in Experience Platform utilizzando l’API Query di audit.
exl-id: 76c5de76-e391-4258-afd8-ddb2c8a9443f
source-git-commit: c7887391481def872c40dd6ed1193bf562b9d0cf
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 6%

---

# Esportare un elenco di eventi di audit

Per recuperare i dati degli eventi, devi effettuare una richiesta GET al `/audit/export` endpoint, specificando gli eventi da recuperare nel payload.

**Formato API**

```http
GET /audit/export
```

| Parametro | Descrizione |
| --------- | ----------- |
| `timestamp` | Quando si filtra per marca temporale, è consigliabile utilizzare un intervallo utilizzando gli operatori > e &lt; anziché un valore esatto. <br/>Esempio: `?property=timestamp<2020-02-08T02:46:48.610862Z&property=timestamp>2020-01-01T02:46:48.610862Z`. |
| `status` | Stato dell’azione. Uno stato può essere uno dei seguenti: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul><br/>Esempio: `?property=status==Deny`. |
| `action` | Tipo di azione registrata per l’evento. Un’azione può essere una qualsiasi delle seguenti: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`Remove` </li><li>`Reset` </li><li>`Segment Activate` </li><li>`Segment remove` </li><li>`Update` </li></ul> Esempio: `?property=action==Create`. |
| `user` | Utente che ha eseguito l&#39;evento. |
| `assetType` | Tipo di risorsa Platform su cui è stata eseguita l’azione. <br/>Esempio: `?property=assetType==<an asset type>`. |

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

I risultati vengono generati in un file CSV per l’esportazione. In caso di esito positivo, la risposta restituisce HTTP 307 senza corpo di risposta. Un collegamento al file di esportazione è disponibile nella sezione `Location` intestazione di risposta.
