---
title: Endpoint API per eventi di controllo
description: Scopri come recuperare gli eventi di audit in Experience Platform utilizzando l’API Query di audit.
role: Developer
feature: Audits, API
exl-id: c365b6d8-0432-41a5-9a07-44a995f69b7d
source-git-commit: dec895e3ea625fb86d1891bad713185d39c47c81
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 2%

---

# Endpoint “audit_events”

I registri di audit vengono utilizzati per fornire dettagli sull’attività dell’utente per vari servizi e funzionalità. Ogni azione registrata contiene metadati che indicano il tipo di azione, la data e l’ora, l’ID e-mail dell’utente che l’ha eseguita e altri attributi relativi al tipo di azione. L&#39;endpoint `/audit/events` nell&#39;API [!DNL Audit Query] consente di recuperare in modo programmatico i dati evento per l&#39;attività dell&#39;organizzazione in [!DNL Experience Platform].

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39;[[!DNL Audit Query] API](https://developer.adobe.com/experience-platform-apis/references/audit-query/). Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API [!DNL Experience Platform].

## Elencare eventi di audit

È possibile recuperare i dati degli eventi effettuando una richiesta GET all&#39;endpoint `/audit/events`, specificando gli eventi da recuperare nel payload.

**Formato API**

```http
GET /audit/events
```

L&#39;API [!DNL Audit Query] supporta l&#39;utilizzo di parametri di query per la pagina e il filtro dei risultati durante l&#39;elenco degli eventi.

| Parametro | Descrizione |
| --- | --- |
| `limit` | Numero massimo di record da restituire nella risposta. Il valore predefinito `limit` è 50. |
| `start` | Puntatore al primo elemento per i risultati di ricerca restituiti. Per accedere alla pagina successiva dei risultati, questo parametro deve essere incrementato della stessa quantità indicata da un limite. Esempio: per accedere alla pagina successiva dei risultati per una richiesta con limite=50, utilizza il parametro start=50, quindi start=100 per la pagina successiva e così via. |
| `queryId` | Quando si esegue una query sull’endpoint /audit/events, la risposta include una proprietà stringa queryId. Per eseguire la stessa query in una chiamata separata, puoi includere il valore Id come un singolo parametro di query invece di configurare manualmente di nuovo i parametri di ricerca. |

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events?limit=10
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce i punti dati risultanti per le metriche e i filtri specificati nella richiesta.

```json
{
  "_embedded": {
    "events": [
      {
        "id": "6ecc125d-da03-4882-a944-88c707ddc3f7",
        "requestId": "5YGdpTX5PvRrdqCfrCT8p8lWphZPzxl8",
        "permissionResource": "Dataset",
        "permissionType": "WRITE",
        "assetType": "Dataset",
        "action": "Create",
        "status": "Allow",
        "failureCode": "",
        "timestamp": "2025-06-24T16:50:28.318+0000",
        "version": "1.0",
        "imsOrgId": "{ORGANIZATION_ID}",
        "region": "VA7",
        "authId": "e6b46821-e2b4-4729-952f-2e4afd713b31",
        "assetId": "685ad754fb1abe2b263df4b3",
        "assetName": "my-dataset",
        "sandboxName": "prod",
        "sandboxId": "{SANDBOX_ID}",
        "userEmail": "{USER_EMAIL}",
        "userIpAddresses": [
          "130.*.*.*",
          "10.*.*.*"
        ],
        "enhancedEvents": [
          {
            "id": "0ee91e42-ac46-4f35-a01a-f74a1569c404",
            "requestId": "5YGdpTX5PvRrdqCfrCT8p8lWphZPzxl8",
            "permissionResource": "Dataset",
            "permissionType": "Write",
            "assetType": "Dataset",
            "action": "Create",
            "status": "Success",
            "failureCode": "",
            "timestamp": "2025-06-24T16:50:28.883+0000",
            "assetId": "685ad754fb1abe2b263df4b3",
            "assetName": "my-dataset"
          }
        ]
      }
    ]
  },
  "_links": {
    "self": {
      "href": "https://platform.adobe.io/data/foundation/audit/events?property=user%253D%253Ddraghici%2540adobe.com"
    },
    "page": {
      "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=b3JkZXJCeVJ1bGVzPSZwcm9wZXJ0eT11c2VyPT1kcmFnaGljaUBhZG9iZS5jb20mdGltZXN0YW1wSW5kZXg9MTc1MDc4MzgyODMxOCZ0b3RhbEVsZW1lbnRzPTE3&limit=50{&start}",
      "templated": true
    }
  },
  "page": {
    "size": 1,
    "totalElements": 1,
    "totalPages": 1,
    "number": 1
  },
  "queryId": "b3JkZXJCeVJ1bGVzPSZwcm9wZXJ0eT11c2VyPT1kcmFnaGljaUBhZG9iZS5jb20mdGltZXN0YW1wSW5kZXg9MTc1MDc4MzgyODMxOCZ0b3RhbEVsZW1lbnRzPTE3"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `events` | Matrice i cui oggetti rappresentano ciascuno degli eventi specificati nella richiesta. Ogni oggetto contiene informazioni sulla configurazione del filtro e sui dati evento restituiti. |
| `userEmail` | Indirizzo e-mail dell’utente che ha eseguito l’evento. |
| `eventType` | Il tipo di evento. I tipi di eventi includono `Core` e `Enhanced`. |
| `imsOrgId` | ID dell’organizzazione in cui si è verificato l’evento. |
| `permissionResource` | Il prodotto o la funzionalità che ha fornito l’autorizzazione eseguono l’azione. Una risorsa può essere una qualsiasi delle seguenti: <ul><li>`Activation` </li><li>`ActivationAssociation` </li><li>`AnalyticSource` </li><li>`AudienceManagerSource` </li><li>`BizibleSource` </li><li>`CustomerAttributeSource` </li><li>`Dataset` </li><li>`EnterpriseSource` </li><li>`LaunchSource` </li><li>`MarketoSource` </li><li>`ProductProfile` </li><li>`ProfileConfig` </li><li>`Sandbox` </li><li>`Schema` </li><li>`Segment` </li><li>`StreamingSource` </li></ul> |
| `permissionType` | Tipo di autorizzazione coinvolto nell’azione. |
| `assetType` | Tipo di risorsa Experience Platform su cui è stata eseguita l’azione. |
| `assetId` | Identificatore univoco della risorsa Experience Platform su cui è stata eseguita l’azione. |
| `assetName` | Nome della risorsa Experience Platform su cui è stata eseguita l’azione. |
| `action` | Tipo di azione registrata per l’evento. Un’azione può essere una qualsiasi delle seguenti: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `status` | Stato dell’azione. Uno stato può essere uno dei seguenti: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |

{style="table-layout:auto"}
