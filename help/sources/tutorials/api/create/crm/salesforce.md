---
title: Connettere Salesforce Ad Experience Platform Utilizzando L’API Del Servizio Flusso
description: Scopri come collegare Adobe Experience Platform a un account Salesforce utilizzando l’API del servizio Flow.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: eab6303a3b420d4622185316922d242a4ce8a12d
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 3%

---

# Connetti [!DNL Salesforce] ad Experience Platform utilizzando l&#39;API [!DNL Flow Service]

Leggi questa guida per scoprire come collegare l&#39;account di origine [!DNL Salesforce] a Adobe Experience Platform utilizzando [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Experience Platform].
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Experience Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Experience Platform

Per informazioni su come effettuare correttamente chiamate alle API di Experience Platform, consulta la guida introduttiva [alle API di Experience Platform](../../../../../landing/api-guide.md).

## Connetti [!DNL Salesforce] ad Experience Platform il [!DNL Azure] {#azure}

Per informazioni su come collegare l&#39;origine [!DNL Salesforce] ad Experience Platform, leggere la procedura seguente il [!DNL Azure].

### Raccogli le credenziali richieste

>[!WARNING]
>
>L&#39;autenticazione di base per l&#39;origine [!DNL Salesforce] diventerà obsoleta a gennaio 2026. È necessario passare all&#39;autenticazione delle credenziali client OAuth 2 per continuare a utilizzare l&#39;origine e l&#39;acquisizione dei dati dall&#39;account [!DNL Salesforce] in Experience Platform.

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

Per ulteriori informazioni su come iniziare, visita [questo documento di Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB Credenziali client OAuth 2]

Per connettere l&#39;account [!DNL Salesforce] a [!DNL Flow Service] utilizzando le credenziali client OAuth 2, specificare i valori per le credenziali seguenti:

| Credenziali | Descrizione |
| --- | --- |
| `environmentUrl` | URL dell&#39;istanza di origine [!DNL Salesforce]. Il formato per `environmentUrl` è `https://[domain].my.salesforce.com` |
| `clientId` | L’ID client viene utilizzato insieme al segreto client come parte dell’autenticazione OAuth2. Insieme, l&#39;ID client e il segreto client consentono all&#39;applicazione di funzionare per conto dell&#39;account identificando l&#39;applicazione in [!DNL Salesforce]. |
| `clientSecret` | Il segreto client viene utilizzato insieme all’ID client come parte dell’autenticazione OAuth2. Insieme, l&#39;ID client e il segreto client consentono all&#39;applicazione di funzionare per conto dell&#39;account identificando l&#39;applicazione in [!DNL Salesforce]. |
| `apiVersion` | Versione REST API dell&#39;istanza [!DNL Salesforce] in uso. Il valore della versione API deve essere formattato con un decimale. Ad esempio, se utilizzi la versione API `52`, devi immettere il valore come `52.0`. Se questo campo viene lasciato vuoto, Experience Platform utilizzerà automaticamente l’ultima versione disponibile. Questo valore è obbligatorio per l&#39;autenticazione delle credenziali client OAuth2. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Salesforce]: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Per ulteriori informazioni sull&#39;utilizzo di OAuth per [!DNL Salesforce], leggere la [[!DNL Salesforce] guida sui flussi di autorizzazione OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5).

>[!ENDTABS]

### Crea una connessione di base per [!DNL Salesforce] in Experience Platform su [!DNL Azure]

Una connessione di base mantiene le informazioni tra l’origine e Experience Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare una connessione di base e connettere l&#39;account [!DNL Salesforce] ad Experience Platform il [!DNL Azure], effettuare una richiesta POST all&#39;endpoint `/connections` e fornire le credenziali di autenticazione [!DNL Salesforce] nel corpo della richiesta.

**Formato API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticazione di base]

+++Richiesta

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

+++

+++Risposta

In caso di esito positivo, la risposta restituisce la connessione di base appena creata insieme al relativo ID univoco.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

>[!TAB Credenziali client OAuth 2]

+++Richiesta

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

+++


+++Risposta

In caso di esito positivo, la risposta restituisce la connessione di base appena creata insieme al relativo ID univoco.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

>[!ENDTABS]

## Connetti [!DNL Salesforce] ad Experience Platform su Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../../../landing/multi-cloud.md).

Per informazioni su come collegare l&#39;origine [!DNL Salesforce] ad Experience Platform su AWS, leggere i passaggi seguenti.

### Prerequisiti

Per informazioni su come configurare l&#39;account [!DNL Salesforce] per connettersi ad Experience Platform su AWS, leggere la [[!DNL Salesforce] panoramica](../../../../connectors/crm/salesforce.md#aws).

### Crea una connessione di base per [!DNL Salesforce] su Experience Platform su AWS

Per creare una connessione di base e connettere l&#39;account [!DNL Salesforce] ad Experience Platform su AWS, effettuare una richiesta POST all&#39;endpoint `/connections` e fornire i valori appropriati per le credenziali.

**Formato API**

```http
POST /connections
```

**Richiesta**

+++Seleziona per visualizzare la richiesta

La richiesta seguente crea una connessione di base per l&#39;origine [!DNL Salesforce] in Experience Platform su AWS.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account on AWS",
      "description": "ACME Salesforce account on AWS",
      "auth": {
          "specName": "OAuth2 JWT Token Credential",
          "params":
            "jwtToken": "{JWT_TOKEN},
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "instanceUrl": "https://acme-enterprise-3126.my.salesforce.com"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

Per informazioni su come recuperare [!DNL Salesforce] `jwtToken`, leggere la guida in [come configurare un&#39;origine [!DNL Salesforce] per la connessione ad Experience Platform su AWS](../../../../connectors/crm/salesforce.md#aws).

+++

**Risposta**

+++Seleziona per visualizzare la risposta

In caso di esito positivo, la risposta restituisce la connessione di base appena creata insieme al relativo ID univoco.

```json
{
    "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

### Verifica lo stato della connessione

Per verificare lo stato della connessione, effettuare una richiesta GET all&#39;endpoint `/connections` e fornire l&#39;ID connessione di base generato nel passaggio di creazione.

**Formato API**

```http
GET /connections
```

**Richiesta**

+++Seleziona per visualizzare la richiesta

La richiesta seguente recupera le informazioni per l&#39;ID connessione di base: `3e908d3f-c390-482b-9f44-43d3d4f2eb82`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/3e908d3f-c390-482b-9f44-43d3d4f2eb82' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
```

+++

**Risposta**

>[!BEGINTABS]

>[!TAB Inizializzazione in corso]

+++Seleziona per visualizzare l’esempio di risposta

Nella risposta seguente vengono visualizzate le informazioni per l&#39;ID connessione di base: `3e908d3f-c390-482b-9f44-43d3d4f2eb82` mentre si trova nello stato `initializing`.

```json
{
  "items": [
    {
      "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
      "createdAt": 1736506325115,
      "updatedAt": 1736506325717,
      "createdBy": "acme@techacct.adobe.com",
      "updatedBy": "acme@techacct.adobe.com",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "JWT Token Auth Authentication E2E-1736506322",
      "description": "Base Connection for salesforce E2E",
      "connectionSpec": {
        "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
        "version": "1.0"
      },
      "state": "initializing",
      "auth": {
        "specName": "OAuth2 JWT Token Credential",
        "params": {
          "jwtToken": "{JWT_TOKEN}",
          "clientId": "{CLIENT_ID}",
          "clientSecret": "{CLIENT_SECRET}",
          "instanceUrl": "https://acme-enterprise-3126.my.salesforce.com"
        }
      }
    }
  }
]
```

+++

>[!TAB Abilitato]

+++Seleziona per visualizzare l’esempio di risposta

Nella risposta seguente vengono visualizzate le informazioni per l&#39;ID connessione di base: `3e908d3f-c390-482b-9f44-43d3d4f2eb82` mentre si trova nello stato `enabled`.

```json
{
  "items": [
      {
        "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
        "createdAt": 1736506325115,
        "updatedAt": 1736506413299,
        "createdBy": "acme@techacct.adobe.com",
        "updatedBy": "acme@AdobeID",
        "createdClient": "{CREATED_CLIENT}",
        "updatedClient": "acme",
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "imsOrgId": "{ORG_ID}",
        "name": "JWT Token Auth Authentication E2E-1736506322",
        "description": "Base Connection for salesforce E2E",
        "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
        },
        "state": "enabled",
        "auth": {
          "specName": "OAuth2 JWT Token Credential",
          "params": {
            "jwtToken": "{JWT_TOKEN}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}",
            "instanceUrl": "https://adb8-dev-ed.develop.my.salesforce.com",
            "orgId": "00DdL000001iPRxUAM"
          }
        },
        "version": "\"6d27f305-40be-41c3-97d4-a701827c34df\"",
        "etag": "\"6d27f305-40be-41c3-97d4-a701827c34df\""
    }
  ]
}
```

+++

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL Salesforce] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati CRM in Experience Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/crm.md)
