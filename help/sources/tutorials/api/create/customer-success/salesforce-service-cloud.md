---
title: Creare una connessione sorgente del cloud di servizi Salesforce utilizzando l’API del servizio Flusso
description: Scopri come collegare Adobe Experience Platform a Salesforce Service Cloud utilizzando l’API del servizio Flusso.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 7930a869627130a5db34780e64b809cda0c1e5f4
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 3%

---

# Creare un [!DNL Salesforce Service Cloud] connessione sorgente tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Leggi questa esercitazione per scoprire come creare una connessione di base per [!DNL Salesforce Service Cloud] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): Experience Platform consente di acquisire dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): Experienci Platform fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Salesforce Service Cloud] utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Il [!DNL Salesforce Service Cloud] L&#39;origine supporta l&#39;autenticazione di base e le credenziali client OAuth2.

>[!BEGINTABS]

>[!TAB Autenticazione di base]

Per collegare [!DNL Salesforce Service Cloud] account a [!DNL Flow Service] utilizzando l’autenticazione di base, fornisci i valori per le seguenti credenziali:

| Credenziali | Descrizione |
| --- | --- |
| `environmentUrl` | L’URL del [!DNL Salesforce Service Cloud] istanza di origine. |
| `username` | Nome utente per [!DNL Salesforce Service Cloud] account utente. |
| `password` | La password per [!DNL Salesforce Service Cloud] account utente. |
| `securityToken` | Token di sicurezza per [!DNL Salesforce Service Cloud] account utente. |
| `apiVersion` | (Facoltativo) La versione REST API di [!DNL Salesforce Service Cloud] che si sta utilizzando. Il valore della versione API deve essere formattato con un decimale. Ad esempio, se utilizzi la versione API `52`, è necessario immettere il valore come `52.0`. Se questo campo viene lasciato vuoto, Experienci Platform utilizzerà automaticamente l’ultima versione disponibile. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Salesforce Service Cloud] è: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Per ulteriori informazioni su come iniziare, visita [questo documento Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB Credenziali client OAuth 2]

Per collegare [!DNL Salesforce Service Cloud] account a [!DNL Flow Service] utilizzando le credenziali client OAuth 2, fornisci i valori per le seguenti credenziali:

| Credenziali | Descrizione |
| --- | --- |
| `environmentUrl` | L’URL del [!DNL Salesforce Service Cloud] istanza di origine. |
| `clientId` | L’ID client viene utilizzato insieme al segreto client come parte dell’autenticazione OAuth2. Insieme, l’ID client e il segreto client consentono all’applicazione di funzionare per conto del tuo account identificando l’applicazione in [!DNL Salesforce Service Cloud]. |
| `clientSecret` | Il segreto client viene utilizzato insieme all’ID client come parte dell’autenticazione OAuth2. Insieme, l’ID client e il segreto client consentono all’applicazione di funzionare per conto del tuo account identificando l’applicazione in [!DNL Salesforce Service Cloud]. |
| `apiVersion` | Versione REST API di [!DNL Salesforce Service Cloud] che si sta utilizzando. Il valore della versione API deve essere formattato con un decimale. Ad esempio, se utilizzi la versione API `52`, è necessario immettere il valore come `52.0`. Se questo campo viene lasciato vuoto, Experienci Platform utilizzerà automaticamente l’ultima versione disponibile. Questo valore è obbligatorio per l&#39;autenticazione delle credenziali client OAuth2. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Salesforce Service Cloud] è: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Per ulteriori informazioni sull’utilizzo di OAuth per [!DNL Salesforce Service Cloud], leggi [[!DNL Salesforce Service Cloud] guida ai flussi di autorizzazione OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

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

>[!BEGINTABS]

>[!TAB Autenticazione di base]

La richiesta seguente crea una connessione di base per [!DNL Salesforce Service Cloud] utilizzo dell&#39;autenticazione di base:

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
| `auth.params.environmentUrl` | L’URL del tuo [!DNL Salesforce Service Cloud] dell&#39;istanza. |
| `auth.params.username` | Il nome utente associato al tuo [!DNL Salesforce Service Cloud] account. |
| `auth.params.password` | La password associata al tuo [!DNL Salesforce Service Cloud] account. |
| `auth.params.securityToken` | Il token di sicurezza associato al tuo [!DNL Salesforce Service Cloud] account. |
| `connectionSpec.id` | Il [!DNL Salesforce Service Cloud] ID specifica di connessione: `cb66ab34-8619-49cb-96d1-39b37ede86ea` |

>[!TAB Credenziali client OAuth2]

La richiesta seguente crea una connessione di base per [!DNL Salesforce Service Cloud] utilizzo delle credenziali client OAuth 2:

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
| `auth.params.environmentUrl` | L’URL del tuo [!DNL Salesforce Service Cloud] dell&#39;istanza. |
| `auth.params.clientId` | L’ID client associato al tuo [!DNL Salesforce Service Cloud] account. |
| `auth.params.clientSecret` | Il segreto client associato al tuo [!DNL Salesforce Service Cloud] account. |
| `auth.params.apiVersion` | Versione REST API di [!DNL Salesforce Service Cloud] che si sta utilizzando. |
| `connectionSpec.id` | Il [!DNL Salesforce Service Cloud] ID specifica di connessione: `cb66ab34-8619-49cb-96d1-39b37ede86ea`. |

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

Seguendo questa esercitazione, hai creato una [!DNL Salesforce Service Cloud] connessione di base tramite [!DNL Flow Service] API. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati di successo dei clienti su Platform utilizzando [!DNL Flow Service] API](../../collect/customer-success.md)
