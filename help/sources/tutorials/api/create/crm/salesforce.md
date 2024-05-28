---
title: Creare una connessione di base Salesforce utilizzando l’API del servizio Flow
description: Scopri come collegare Adobe Experience Platform a un account Salesforce utilizzando l’API del servizio Flusso.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 7d450ba3357389a2934f187e4838e534d698dd4a
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 3%

---

# Creare un [!DNL Salesforce] connessione di base tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Salesforce] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente [!DNL Platform] a un [!DNL Salesforce] account che utilizza [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Il [!DNL Salesforce] L&#39;origine supporta l&#39;autenticazione di base e le credenziali client OAuth2.

>[!BEGINTABS]

>[!TAB Autenticazione di base]

Per collegare [!DNL Salesforce] account a [!DNL Flow Service] utilizzando l’autenticazione di base, fornisci i valori per le seguenti credenziali:

| Credenziali | Descrizione |
| --- | --- |
| `environmentUrl` | L’URL del [!DNL Salesforce] istanza di origine. |
| `username` | Nome utente per [!DNL Salesforce] account utente. |
| `password` | La password per [!DNL Salesforce] account utente. |
| `securityToken` | Token di sicurezza per [!DNL Salesforce] account utente. |
| `apiVersion` | Facoltativo) La versione REST API di [!DNL Salesforce] che si sta utilizzando. Il valore della versione API deve essere formattato con un decimale. Ad esempio, se utilizzi la versione API `52`, è necessario immettere il valore come `52.0`. Se questo campo viene lasciato vuoto, Experienci Platform utilizzerà automaticamente l’ultima versione disponibile. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Salesforce] è: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Per ulteriori informazioni su come iniziare, visita [questo documento Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB Credenziali client OAuth 2]

Per collegare [!DNL Salesforce] account a [!DNL Flow Service] utilizzando le credenziali client OAuth 2, fornisci i valori per le seguenti credenziali:

| Credenziali | Descrizione |
| --- | --- |
| `environmentUrl` | L’URL del [!DNL Salesforce] istanza di origine. |
| `clientId` | L’ID client viene utilizzato insieme al segreto client come parte dell’autenticazione OAuth2. Insieme, l’ID client e il segreto client consentono all’applicazione di funzionare per conto del tuo account identificando l’applicazione in [!DNL Salesforce]. |
| `clientSecret` | Il segreto client viene utilizzato insieme all’ID client come parte dell’autenticazione OAuth2. Insieme, l’ID client e il segreto client consentono all’applicazione di funzionare per conto del tuo account identificando l’applicazione in [!DNL Salesforce]. |
| `apiVersion` | Versione REST API di [!DNL Salesforce] che si sta utilizzando. Il valore della versione API deve essere formattato con un decimale. Ad esempio, se utilizzi la versione API `52`, è necessario immettere il valore come `52.0`. Se questo campo viene lasciato vuoto, Experienci Platform utilizzerà automaticamente l’ultima versione disponibile. Questo valore è obbligatorio per l&#39;autenticazione delle credenziali client OAuth2. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Salesforce] è: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Per ulteriori informazioni sull’utilizzo di OAuth per [!DNL Salesforce], leggi [[!DNL Salesforce] guida ai flussi di autorizzazione OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` e fornire il [!DNL Salesforce] credenziali di autenticazione nel corpo della richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

>[!BEGINTABS]

>[!TAB Autenticazione di base]

La richiesta seguente crea una connessione di base per [!DNL Salesforce] utilizzo dell&#39;autenticazione di base:

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
| `auth.params.environmentUrl` | L’URL del tuo [!DNL Salesforce] dell&#39;istanza. |
| `auth.params.username` | Il nome utente associato al tuo [!DNL Salesforce] account. |
| `auth.params.password` | La password associata al tuo [!DNL Salesforce] account. |
| `auth.params.securityToken` | Il token di sicurezza associato al tuo [!DNL Salesforce] account. |
| `connectionSpec.id` | Il [!DNL Salesforce] ID specifica di connessione: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

>[!TAB Credenziali client OAuth 2]

La richiesta seguente crea una connessione di base per [!DNL Salesforce] utilizzo delle credenziali client OAuth 2:

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
| `auth.params.environmentUrl` | L’URL del tuo [!DNL Salesforce] dell&#39;istanza. |
| `auth.params.clientId` | L’ID client associato al tuo [!DNL Salesforce] account. |
| `auth.params.clientSecret` | Il segreto client associato al tuo [!DNL Salesforce] account. |
| `auth.params.apiVersion` | Versione REST API di [!DNL Salesforce] che si sta utilizzando. |
| `connectionSpec.id` | Il [!DNL Salesforce] ID specifica di connessione: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

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

Seguendo questa esercitazione, hai creato una [!DNL Salesforce] connessione di base tramite [!DNL Flow Service] API. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati CRM in Platform utilizzando [!DNL Flow Service] API](../../collect/crm.md)
