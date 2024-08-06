---
title: Creare una connessione di base Salesforce utilizzando l’API del servizio Flow
description: Scopri come collegare Adobe Experience Platform a un account Salesforce utilizzando l’API del servizio Flusso.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 5951b0f549c2fd2723945f8f4089d12f73b92e6c
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 3%

---

# Creare una connessione di base [!DNL Salesforce] utilizzando l&#39;API [!DNL Flow Service]

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Salesforce] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettere correttamente [!DNL Platform] a un account [!DNL Salesforce] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

L&#39;origine [!DNL Salesforce] supporta l&#39;autenticazione di base e le credenziali client OAuth2.

>[!BEGINTABS]

>[!TAB Autenticazione di base]

Per connettere l&#39;account [!DNL Salesforce] a [!DNL Flow Service] utilizzando l&#39;autenticazione di base, specificare i valori per le credenziali seguenti:

| Credenziali | Descrizione |
| --- | --- |
| `environmentUrl` | URL dell&#39;istanza di origine [!DNL Salesforce]. Il formato per `environmentUrl` è `https://[domain].my.salesforce.com`. |
| `username` | Nome utente per l&#39;account utente [!DNL Salesforce]. |
| `password` | Password per l&#39;account utente [!DNL Salesforce]. |
| `securityToken` | Token di sicurezza per l&#39;account utente [!DNL Salesforce]. |
| `apiVersion` | Facoltativo) Versione REST API dell&#39;istanza [!DNL Salesforce] in uso. Il valore della versione API deve essere formattato con un decimale. Ad esempio, se utilizzi la versione API `52`, devi immettere il valore come `52.0`. Se questo campo viene lasciato vuoto, Experience Platform utilizzerà automaticamente l’ultima versione disponibile. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Salesforce]: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Per ulteriori informazioni su come iniziare, visita [questo documento Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB Credenziali client OAuth 2]

Per connettere l&#39;account [!DNL Salesforce] a [!DNL Flow Service] utilizzando le credenziali client OAuth 2, specificare i valori per le credenziali seguenti:

| Credenziali | Descrizione |
| --- | --- |
| `environmentUrl` | URL dell&#39;istanza di origine [!DNL Salesforce]. Il formato per `environmentUrl` è `https://[domain].my.salesforce.com` |
| `clientId` | L’ID client viene utilizzato insieme al segreto client come parte dell’autenticazione OAuth2. Insieme, l&#39;ID client e il segreto client consentono all&#39;applicazione di funzionare per conto dell&#39;account identificando l&#39;applicazione in [!DNL Salesforce]. |
| `clientSecret` | Il segreto client viene utilizzato insieme all’ID client come parte dell’autenticazione OAuth2. Insieme, l&#39;ID client e il segreto client consentono all&#39;applicazione di funzionare per conto dell&#39;account identificando l&#39;applicazione in [!DNL Salesforce]. |
| `apiVersion` | Versione REST API dell&#39;istanza [!DNL Salesforce] in uso. Il valore della versione API deve essere formattato con un decimale. Ad esempio, se utilizzi la versione API `52`, devi immettere il valore come `52.0`. Se questo campo viene lasciato vuoto, Experience Platform utilizzerà automaticamente l’ultima versione disponibile. Questo valore è obbligatorio per l&#39;autenticazione delle credenziali client OAuth2. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Salesforce]: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Per ulteriori informazioni sull&#39;utilizzo di OAuth per [!DNL Salesforce], leggere la [[!DNL Salesforce] guida sui flussi di autorizzazione OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` e fornire le credenziali di autenticazione [!DNL Salesforce] nel corpo della richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

>[!BEGINTABS]

>[!TAB Autenticazione di base]

La richiesta seguente crea una connessione di base per [!DNL Salesforce] utilizzando l&#39;autenticazione di base:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `auth.params.environmentUrl` | URL dell&#39;istanza [!DNL Salesforce]. |
| `auth.params.username` | Il nome utente associato al tuo account [!DNL Salesforce]. |
| `auth.params.password` | La password associata al tuo account [!DNL Salesforce]. |
| `auth.params.securityToken` | Il token di sicurezza associato al tuo account [!DNL Salesforce]. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Salesforce]: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

>[!TAB Credenziali client OAuth 2]

La richiesta seguente crea una connessione di base per [!DNL Salesforce] utilizzando le credenziali client OAuth 2:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using OAuth 2",
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
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `auth.params.environmentUrl` | URL dell&#39;istanza [!DNL Salesforce]. |
| `auth.params.clientId` | ID client associato all&#39;account [!DNL Salesforce]. |
| `auth.params.clientSecret` | Il segreto client associato al tuo account [!DNL Salesforce]. |
| `auth.params.apiVersion` | Versione REST API dell&#39;istanza [!DNL Salesforce] in uso. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Salesforce]: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

>[!ENDTABS]

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione di base appena creata insieme al relativo ID univoco.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL Salesforce] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati CRM in Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/crm.md)
