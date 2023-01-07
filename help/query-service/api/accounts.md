---
keywords: Experience Platform;home;argomenti popolari;servizio query;guida API;servizio query;account del servizio query;account del servizio query;
solution: Experience Platform
title: Endpoint API account
description: Puoi creare un account del servizio query per persistente .
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 5%

---

# Endpoint account

In Adobe Experience Platform Query Service, gli account vengono utilizzati per creare credenziali non in scadenza che è possibile utilizzare con client SQL esterni. È possibile utilizzare `/accounts` endpoint nell’API del servizio query, che consente di creare, recuperare, modificare ed eliminare programmaticamente gli account di integrazione del servizio query (noto anche come account tecnico).

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte dell’API del servizio query. Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, comprese le intestazioni richieste e come leggere le chiamate API di esempio.

## Creare un account

Puoi creare un account di integrazione del servizio Query effettuando una richiesta di POST al `/accounts` punto finale.

**Formato API**

```http
POST /accounts
```

**Richiesta**

La seguente richiesta creerà un nuovo account di integrazione del servizio query per la tua organizzazione IMS.

```shell
curl -X POST https://platform.adobe.io/data/foundation/queryauth/accounts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
{
    "accountName": "sampleName",
    "assignedToUser": "sample@example.com",
    "credential": "samplecredential",
    "description": "Sample description"
}'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `accountName` | **Obbligatorio** Nome dell’account di integrazione del servizio query. |
| `assignedToUser` | **Obbligatorio** Adobe ID per il quale verrà creato l’account di integrazione del servizio query. |
| `credential` | *(Facoltativo)* Credenziale utilizzata per l’integrazione del servizio query. Se non viene specificato, verrà automaticamente generata una credenziale. |
| `description` | *(Facoltativo)* Descrizione dell’account di integrazione del servizio query. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200, con i dettagli dell’account di integrazione di Query Service appena creato. Puoi utilizzare questi dettagli account per collegare Query Service a client esterni.

```json
{
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012",
    "credential": "samplecredential"
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `technicalAccountName` | Nome dell’account di integrazione del servizio query. |
| `technicalAccountId` | ID dell’account di integrazione del servizio query. Questo, insieme al `credential`, compone la password per il tuo account. |
| `credential` | Credenziale dell’account di integrazione del servizio query. Questo, insieme al `technicalAccountId`, compone la password per il tuo account. |

## Aggiornare un account

È possibile aggiornare l’account di integrazione del servizio Query effettuando una richiesta di PUT al `/accounts` punto finale.

**Formato API**

```http
POST /accounts/{ACCOUNT_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{ACCOUNT_ID}` | ID dell’account di integrazione del servizio query che si desidera aggiornare. |

**Richiesta**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
     "accountName": "Updated account name",
     "assignedToUser": "sampleuser2@adobe.com",
     "credential": "UpdatedCredential",
     "description": "Updated description"
 }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `accountName` | *(Facoltativo)* Nome aggiornato per l’account di integrazione del servizio query. |
| `assignedToUser` | *(Facoltativo)* L’Adobe ID aggiornato a cui è collegato l’account di integrazione del servizio query. |
| `credential` | *(Facoltativo)* Credenziale aggiornata per l’account del servizio query. |
| `description` | *(Facoltativo)* Descrizione aggiornata dell’account di integrazione del servizio query. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con le informazioni sul tuo account di integrazione di Query Service appena aggiornato.

```json
{
    "accountName": "Updated account name",
    "assignedToUser": "sampleuser2@adobe.com",
    "created": "2021-06-16T16:44:42.073Z",
    "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "credential": "UpdatedCredential",
    "description": "Updated description",
    "lastUpdated": "2021-08-03T23:47:46.588Z",
    "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012"
}
```

## Elenca tutti gli account

È possibile recuperare un elenco di tutti gli account di integrazione di Query Service effettuando una richiesta di GET al `/accounts` punto finale.

**Formato API**

```http
GET /accounts
```

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/foundation/queryauth/accounts \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un elenco di tutti gli account di integrazione di Query Service.

```json
{
    "accounts": [
        {
            "lastUpdated": "2021-06-16T18:07:49.581Z",
            "accountName": "Use for XQL testing of account creation",
            "description": "Local test",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "ADC7EB19-63B4-4B9F-A192-EBE3CD0C034E@TECHACCT.ADOBE.COM",
            "technicalAccountId": "38645A7360CA3DF30A49400F",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T18:07:49.581Z",
            "active": true
        },
        {
            "lastUpdated": "2021-06-16T16:44:42.073Z",
            "accountName": "Use for XQL testing of account creation",
            "description": " ",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "66E91FDD-4733-45E2-A312-D87580CFA55D@TECHACCT.ADOBE.COM",
            "technicalAccountId": "392202E060CA2A770A49420A",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T16:44:42.073Z",
            "active": true
        }
    ],
    "_page": {
        "count": 2,
        "next": "2021-06-16T16:44:42.073Z",
        "orderby": "-created",
        "property": "active==true",
        "start": "2021-06-16T18:07:49.581Z"
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T16:44:42.073Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T18:07:49.581Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

## Eliminare un account

Puoi eliminare l’account di integrazione del servizio query effettuando una richiesta di DELETE al `/accounts` punto finale.

**Formato API**

```http
DELETE /accounts/{ACCOUNT_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{ACCOUNT_ID}` | ID dell’account di integrazione del servizio query da eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un messaggio che indica che l’account è stato eliminato correttamente.

```json
{
    "result": "Success"
}
```
