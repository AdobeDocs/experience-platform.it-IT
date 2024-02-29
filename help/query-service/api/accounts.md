---
keywords: Experience Platform;home;argomenti popolari;servizio query;guida API;servizio query;account servizio query;account servizio query;
solution: Experience Platform
title: Endpoint API account
description: È possibile creare un account di Query Service per persistente.
role: Developer
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 5%

---

# Endpoint Account

In Adobe Experience Platform Query Service, gli account vengono utilizzati per creare credenziali senza scadenza che è possibile utilizzare con client SQL esterni. È possibile utilizzare `/accounts` endpoint nell’API di Query Service, che consente di creare, recuperare, modificare ed eliminare in modo programmatico gli account di integrazione di Query Service (noto anche come account tecnico).

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte dell’API Query Service. Prima di continuare, controlla [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all’API, incluse le intestazioni richieste e la lettura di esempi di chiamate API.

## Creare un account

Per creare un account di integrazione di Query Service, devi effettuare una richiesta POST al `/accounts` endpoint.

**Formato API**

```http
POST /accounts
```

**Richiesta**

La richiesta seguente creerà un nuovo account di integrazione di Query Service per la tua organizzazione.

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
| `accountName` | **Obbligatorio** Nome dell’account di integrazione di Query Service. |
| `assignedToUser` | **Obbligatorio** L’Adobe ID per cui verrà creato l’account di integrazione di Query Service. |
| `credential` | *(Facoltativo)* Credenziali utilizzate per l&#39;integrazione di Query Service. Se non viene specificato, il sistema genererà automaticamente una credenziale. |
| `description` | *(Facoltativo)* Descrizione dell&#39;account di integrazione di Query Service. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200, con i dettagli dell’account di integrazione di Query Service appena creato. Puoi utilizzare questi dettagli dell’account per collegare Query Service a client esterni.

```json
{
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012",
    "credential": "samplecredential"
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `technicalAccountName` | Nome dell’account di integrazione di Query Service. |
| `technicalAccountId` | ID dell’account di integrazione di Query Service. Questo, insieme al `credential`, compone la password per il tuo account. |
| `credential` | Le credenziali dell’account di integrazione di Query Service. Questo, insieme al `technicalAccountId`, compone la password per il tuo account. |

## Aggiornare un account

Per aggiornare l’account di integrazione di Query Service, effettua una richiesta PUT al `/accounts` endpoint.

**Formato API**

```http
POST /accounts/{ACCOUNT_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{ACCOUNT_ID}` | ID dell’account di integrazione di Query Service che desideri aggiornare. |

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
| `accountName` | *(Facoltativo)* Nome aggiornato per l’account di integrazione di Query Service. |
| `assignedToUser` | *(Facoltativo)* L’Adobe ID aggiornato a cui è collegato l’account di integrazione di Query Service. |
| `credential` | *(Facoltativo)* Credenziali aggiornate per l&#39;account di Query Service. |
| `description` | *(Facoltativo)* Descrizione aggiornata dell’account di integrazione di Query Service. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni sull’account di integrazione di Query Service appena aggiornato.

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

Per recuperare un elenco di tutti gli account di integrazione di Query Service, effettua una richiesta GET al `/accounts` endpoint.

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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco di tutti gli account di integrazione di Query Service.

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

Per eliminare l’account di integrazione di Query Service, effettua una richiesta DELETE al `/accounts` endpoint.

**Formato API**

```http
DELETE /accounts/{ACCOUNT_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{ACCOUNT_ID}` | ID dell’account di integrazione di Query Service che desideri eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un messaggio che informa che l’account è stato eliminato correttamente.

```json
{
    "result": "Success"
}
```
