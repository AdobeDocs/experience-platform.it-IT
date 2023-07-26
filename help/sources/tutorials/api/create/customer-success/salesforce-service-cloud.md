---
keywords: Experience Platform;home;argomenti popolari;Salesforce Service Cloud;salesforce service cloud
solution: Experience Platform
title: Creare una connessione sorgente del cloud di servizi Salesforce utilizzando l’API del servizio Flusso
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a Salesforce Service Cloud utilizzando l’API del servizio Flusso.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 5d28db34edd377269e8710b1741098a08616ae5f
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 2%

---

# Creare un [!DNL Salesforce Service Cloud] connessione sorgente tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Salesforce Service Cloud] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Salesforce Service Cloud] utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi con [!DNL Salesforce Service Cloud], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `username` | Il nome utente per il [!DNL Salesforce Service Cloud] account utente. |
| `password` | La password per [!DNL Salesforce Service Cloud] account. |
| `securityToken` | Token di sicurezza per il [!DNL Salesforce Service Cloud] account. |
| `apiVersion` | (Facoltativo) La versione REST API di [!DNL Salesforce Service Cloud] che si sta utilizzando. Se questo campo viene lasciato vuoto, Experienci Platform utilizzerà automaticamente l’ultima versione disponibile. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Salesforce Service Cloud] è: `b66ab34-8619-49cb-96d1-39b37ede86ea`. |

Per ulteriori informazioni su come iniziare, consulta [questo documento di Salesforce Service Cloud](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL Salesforce Service Cloud] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Salesforce Service Cloud]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for salesforce service cloud",
      "description": "Base connection for salesforce service cloud",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "securityToken": "{SECURITY_TOKEN}"
          }
      },
      "connectionSpec": {
          "id": "b66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `auth.params.username` | Il nome utente associato al tuo [!DNL Salesforce Service Cloud] account. |
| `auth.params.password` | La password associata al tuo [!DNL Salesforce Service Cloud] account. |
| `auth.params.securityToken` | Il token di sicurezza associato al tuo [!DNL Salesforce Service Cloud] account. |
| `connectionSpec.id` | Il [!DNL Salesforce Service Cloud] ID specifica di connessione: `b66ab34-8619-49cb-96d1-39b37ede86ea` |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare il sistema CRM nel passaggio successivo.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una [!DNL Salesforce Service Cloud] connessione di base tramite [!DNL Flow Service] API. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati di successo dei clienti su Platform utilizzando [!DNL Flow Service] API](../../collect/customer-success.md)
