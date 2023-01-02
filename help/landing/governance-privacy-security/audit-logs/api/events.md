---
title: Endpoint API per gli eventi di controllo
description: Scopri come recuperare gli eventi di controllo in Experience Platform utilizzando l’API Audit Query.
exl-id: c365b6d8-0432-41a5-9a07-44a995f69b7d
source-git-commit: c7887391481def872c40dd6ed1193bf562b9d0cf
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 10%

---

# Endpoint “audit_events”

I registri di controllo vengono utilizzati per fornire dettagli sull’attività dell’utente per vari servizi e funzionalità. Ogni azione registrata contiene metadati che indicano il tipo di azione, la data e l’ora, l’ID e-mail dell’utente che l’ha eseguita ed eventuali attributi aggiuntivi relativi al tipo di azione. La `/audit/events` punto finale [!DNL Audit Query] L’API ti consente di recuperare in modo programmatico i dati evento per l’attività dell’organizzazione in [!DNL Platform].

## Introduzione

L’endpoint API utilizzato in questa guida fa parte del [[!DNL Audit Query] API](https://developer.adobe.com/experience-platform-apis/references/audit-query/). Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio presenti in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi [!DNL Experience Platform] API.

## Elencare eventi di controllo

Puoi recuperare i dati degli eventi effettuando una richiesta GET al `/audit/events` endpoint, specificando gli eventi da recuperare nel payload.

**Formato API**

```http
GET /audit/events
```

La [!DNL Audit Query] L’API supporta l’utilizzo di parametri di query per la pagina e filtrare i risultati durante l’elenco degli eventi.

| Parametro | Descrizione |
| --- | --- |
| `limit` | Il numero massimo di record da restituire nella risposta. Il valore predefinito `limit` è 50. |
| `start` | Puntatore al primo elemento per i risultati di ricerca restituiti. Per accedere alla pagina successiva dei risultati, questo parametro deve incrementare della stessa quantità indicata dal limite. Esempio: Per accedere alla pagina successiva di risultati per una richiesta con limit=50, utilizza il parametro start=50, quindi start=100 per la pagina successiva e così via. |
| `queryId` | Quando si effettua una query sull&#39;endpoint /audit/events, la risposta include una proprietà della stringa queryId. Per eseguire la stessa query in una chiamata separata, puoi includere il valore ID come parametro di query singolo invece di configurare nuovamente manualmente i parametri di ricerca. |

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

Una risposta corretta restituisce i punti dati risultanti per le metriche e i filtri specificati nella richiesta.

```json
{
   "_embedded": {
     "customerAuditLogList": [
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "32b72208-3035-4bc6-b434-39e34401a864",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "5NphpgUQdQnjTWOcS9DSMs2wD1EUMlYG",
         "authId": "96715f98-d100-4575-8491-ebbcea654eb9",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T21:58:09.745+0000"
       },
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "a178736a-8fa1-47da-bac5-b0d9e741e414",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "7AlGIAhWvaEzYWHLzvuf26AAFAkqSyKg",
         "authId": "60fc1077-4aef-4e1f-a5ff-f64183e060f4",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T21:28:00.301+0000"
       },
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "ccfe8c77-9b93-481d-a561-0b2edf3b77dc",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "hArqS4CAa8wfRPnKuxV4yaA82atxwzYu",
         "authId": "80b7d887-9338-4cd5-9d79-2483b03f0160",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T20:58:07.750+0000"
       }
     ]    
   },
   "_links": {
     "self": {
       "href": "https://platform.adobe.io/data/foundation/audit/events?limit=10&start=0&property=type%253D%253Dcore"
     },
     "next": {
       "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2&start=10&limit=10"
     },
     "page": {
       "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2&limit=10{&start}",
       "templated": true
     }
  },
  "page": {
    "size": 10,
    "totalElements": 3,
    "totalPages": 1,
    "number": 1
  },
  "queryId": "cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `customerAuditLogList` | Matrice i cui oggetti rappresentano ciascuno degli eventi specificati nella richiesta. Ogni oggetto contiene informazioni sulla configurazione del filtro e sui dati dell&#39;evento restituiti. |
| `userEmail` | L’e-mail dell’utente che ha eseguito l’evento. |
| `eventType` | Il tipo di evento. I tipi di eventi includono `Core` e `Enhanced`. |
| `imsOrgId` | L&#39;ID dell&#39;organizzazione in cui si è verificato l&#39;evento. |
| `permissionResource` | Il prodotto o la funzionalità che ha fornito l&#39;autorizzazione esegue l&#39;azione. Una risorsa può essere una delle seguenti: <ul><li>`Activation` </li><li>`ActivationAssociation` </li><li>`AnalyticSource` </li><li>`AudienceManagerSource` </li><li>`BizibleSource` </li><li>`CustomerAttributeSource` </li><li>`Dataset` </li><li>`EnterpriseSource` </li><li>`LaunchSource` </li><li>`MarketoSource` </li><li>`ProductProfile` </li><li>`ProfileConfig` </li><li>`Sandbox` </li><li>`Schema` </li><li>`Segment` </li><li>`StreamingSource` </li></ul> |
| `permissionType` | Il tipo di autorizzazione coinvolto nell&#39;azione. |
| `assetType` | Il tipo di risorsa Platform su cui è stata eseguita l’azione. |
| `assetId` | Identificatore univoco per la risorsa Platform su cui è stata eseguita l&#39;azione. |
| `assetName` | Nome della risorsa Platform su cui è stata eseguita l’azione. |
| `action` | Il tipo di azione registrata per l&#39;evento. Un’azione può essere una delle seguenti: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `status` | Lo stato dell’azione. Uno stato può essere uno dei seguenti: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |

{style=&quot;table-layout:auto&quot;}
