---
title: Creare una connessione Salesforce Service Cloud Source utilizzando l’API Flow Service
description: Scopri come collegare Adobe Experience Platform a Salesforce Service Cloud utilizzando l’API del servizio Flusso.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 7930a869627130a5db34780e64b809cda0c1e5f4
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 3%

---

# Crea una connessione di origine [!DNL Salesforce Service Cloud] utilizzando l&#39;API [!DNL Flow Service]

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Leggi questo tutorial per scoprire come creare una connessione di base per [!DNL Salesforce Service Cloud] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Salesforce Service Cloud] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

L&#39;origine [!DNL Salesforce Service Cloud] supporta l&#39;autenticazione di base e le credenziali client OAuth2.

>[!BEGINTABS]

>[!TAB Autenticazione di base]

Per connettere l&#39;account [!DNL Salesforce Service Cloud] a [!DNL Flow Service] utilizzando l&#39;autenticazione di base, specificare i valori per le credenziali seguenti:

| Credenziali | Descrizione |
| --- | --- |
| `environmentUrl` | URL dell&#39;istanza di origine [!DNL Salesforce Service Cloud]. |
| `username` | Nome utente per l&#39;account utente [!DNL Salesforce Service Cloud]. |
| `password` | Password per l&#39;account utente [!DNL Salesforce Service Cloud]. |
| `securityToken` | Token di sicurezza per l&#39;account utente [!DNL Salesforce Service Cloud]. |
| `apiVersion` | (Facoltativo) Versione REST API dell&#39;istanza [!DNL Salesforce Service Cloud] in uso. Il valore della versione API deve essere formattato con un decimale. Ad esempio, se utilizzi la versione API `52`, devi immettere il valore come `52.0`. Se questo campo viene lasciato vuoto, Experience Platform utilizzerà automaticamente l’ultima versione disponibile. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Salesforce Service Cloud]: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Per ulteriori informazioni su come iniziare, visita [questo documento Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB Credenziali client OAuth 2]

Per connettere l&#39;account [!DNL Salesforce Service Cloud] a [!DNL Flow Service] utilizzando le credenziali client OAuth 2, specificare i valori per le credenziali seguenti:

| Credenziali | Descrizione |
| --- | --- |
| `environmentUrl` | URL dell&#39;istanza di origine [!DNL Salesforce Service Cloud]. |
| `clientId` | L’ID client viene utilizzato insieme al segreto client come parte dell’autenticazione OAuth2. Insieme, l&#39;ID client e il segreto client consentono all&#39;applicazione di funzionare per conto dell&#39;account identificando l&#39;applicazione in [!DNL Salesforce Service Cloud]. |
| `clientSecret` | Il segreto client viene utilizzato insieme all’ID client come parte dell’autenticazione OAuth2. Insieme, l&#39;ID client e il segreto client consentono all&#39;applicazione di funzionare per conto dell&#39;account identificando l&#39;applicazione in [!DNL Salesforce Service Cloud]. |
| `apiVersion` | Versione REST API dell&#39;istanza [!DNL Salesforce Service Cloud] in uso. Il valore della versione API deve essere formattato con un decimale. Ad esempio, se utilizzi la versione API `52`, devi immettere il valore come `52.0`. Se questo campo viene lasciato vuoto, Experience Platform utilizzerà automaticamente l’ultima versione disponibile. Questo valore è obbligatorio per l&#39;autenticazione delle credenziali client OAuth2. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Salesforce Service Cloud]: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Per ulteriori informazioni sull&#39;utilizzo di OAuth per [!DNL Salesforce Service Cloud], leggere la [[!DNL Salesforce Service Cloud] guida sui flussi di autorizzazione OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Salesforce Service Cloud] come parte dei parametri della richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

>[!BEGINTABS]

>[!TAB Autenticazione di base]

La richiesta seguente crea una connessione di base per [!DNL Salesforce Service Cloud] utilizzando l&#39;autenticazione di base:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (basic auth)",
      "description": "Salesforce Service Cloud account for ACME data (basic auth)",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce-service-cloud",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| Parametro | Descrizione |
| ---| --- |
| `auth.params.environmentUrl` | URL dell&#39;istanza [!DNL Salesforce Service Cloud]. |
| `auth.params.username` | Il nome utente associato al tuo account [!DNL Salesforce Service Cloud]. |
| `auth.params.password` | La password associata al tuo account [!DNL Salesforce Service Cloud]. |
| `auth.params.securityToken` | Il token di sicurezza associato al tuo account [!DNL Salesforce Service Cloud]. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Salesforce Service Cloud]: `cb66ab34-8619-49cb-96d1-39b37ede86ea` |

>[!TAB Credenziali client OAuth2]

La richiesta seguente crea una connessione di base per [!DNL Salesforce Service Cloud] utilizzando le credenziali client OAuth 2:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (OAuth2)",
      "description": "Salesforce Service Cloud account for ACME data (OAuth2)",
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "apiVersion": "60.0"
        }
      },
      "connectionSpec": {
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `auth.params.environmentUrl` | URL dell&#39;istanza [!DNL Salesforce Service Cloud]. |
| `auth.params.clientId` | ID client associato all&#39;account [!DNL Salesforce Service Cloud]. |
| `auth.params.clientSecret` | Il segreto client associato al tuo account [!DNL Salesforce Service Cloud]. |
| `auth.params.apiVersion` | Versione REST API dell&#39;istanza [!DNL Salesforce Service Cloud] in uso. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Salesforce Service Cloud]: `cb66ab34-8619-49cb-96d1-39b37ede86ea`. |

>[!ENDTABS]

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione di base appena creata insieme al relativo ID univoco.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL Salesforce Service Cloud] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati di successo dei clienti su Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/customer-success.md)
