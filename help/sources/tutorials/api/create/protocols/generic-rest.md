---
keywords: Experience Platform;home;argomenti popolari;REST generico;resto generico
solution: Experience Platform
title: Creare una connessione di base API REST generica utilizzando l’API del servizio Flow
type: Tutorial
description: Scopri come collegare l’API REST generica a Adobe Experience Platform utilizzando l’API del servizio Flow.
exl-id: 6b414868-503e-49d5-8f4a-5b2fc003dab0
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 3%

---

# Creare una connessione di base API REST generica utilizzando l&#39;API [!DNL Flow Service]

>[!NOTE]
>
>L&#39;origine [!DNL Generic REST API] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica origini](../../../../home.md#terms-and-conditions).

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Generic REST API] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

### Raccogli le credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Generic REST API], è necessario fornire credenziali valide per il tipo di autenticazione scelto. [!DNL Generic REST API] supporta sia il codice di aggiornamento OAuth 2 che l&#39;autenticazione di base. Per informazioni sulle credenziali per i due tipi di autenticazione supportati, vedere le tabelle seguenti.

#### Codice di aggiornamento OAuth 2

| Credenziali | Descrizione |
| --- | --- |
| `host` | L’URL host dell’origine a cui stai effettuando la richiesta. Questo valore è obbligatorio e non può essere ignorato utilizzando `requestParameterOverride`. |
| `authorizationTestUrl` | (Facoltativo) L’URL del test di autorizzazione viene utilizzato per convalidare le credenziali durante la creazione di una connessione di base. Se non vengono fornite, le credenziali vengono controllate automaticamente durante il passaggio di creazione della connessione di origine. |
| `clientId` | (Facoltativo) L’ID client associato al tuo account utente. |
| `clientSecret` | (Facoltativo) Il segreto client associato al tuo account utente. |
| `accessToken` | Credenziali di autenticazione primarie utilizzate per accedere all&#39;applicazione. Il token di accesso rappresenta l’autorizzazione dell’applicazione ad accedere ad aspetti particolari dei dati di un utente. Questo valore è obbligatorio e non può essere ignorato utilizzando `requestParameterOverride`. |
| `refreshToken` | (Facoltativo) Token utilizzato per generare un nuovo token di accesso, se il token di accesso è scaduto. |
| `expirationDate` | (Facoltativo) Un valore nascosto che definisce la data di scadenza del token di accesso. |
| `accessTokenUrl` | (Facoltativo) L’endpoint URL utilizzato per recuperare il token di accesso. |
| `requestParameterOverride` | (Facoltativo) Proprietà che consente di specificare i parametri delle credenziali da ignorare. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Generic REST API]: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

#### Autenticazione di base

| Credenziali | Descrizione |
| --- | --- |
| `host` | L’URL host dell’origine a cui stai effettuando la richiesta. |
| `username` | Il nome utente che corrisponde al tuo account utente. |
| `password` | La password che corrisponde al tuo account utente. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Generic REST API]: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

[!DNL Generic REST API] supporta sia l&#39;autenticazione di base che il codice di aggiornamento OAuth 2. Per istruzioni su come eseguire l’autenticazione con uno dei tipi di autenticazione, consulta gli esempi seguenti.

### Crea una connessione di base [!DNL Generic REST API] utilizzando il codice di aggiornamento OAuth 2

Per creare un ID di connessione di base utilizzando il codice di aggiornamento OAuth 2, effettua una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali OAuth 2.

**Formato API**

```http
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Generic REST API]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Generic REST API base connection with OAuth 2 refresh code",
      "description": "Generic REST API base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "host": "{HOST}",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `name` | Nome della connessione di base. Verificare che il nome della connessione di base sia descrittivo, in quanto è possibile utilizzarlo per cercare informazioni sulla connessione di base. |
| `description` | (Facoltativo) Proprietà che è possibile includere per fornire ulteriori informazioni sulla connessione di base. |
| `connectionSpec.id` | ID della specifica di connessione associato a [!DNL Generic REST API]. ID corretto: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | Tipo di autenticazione utilizzato per autenticare l’origine in Platform. |
| `auth.params.host` | URL principale utilizzato per connettersi all&#39;origine [!DNL Generic REST API]. |
| `auth.params.accessToken` | Il token di accesso corrispondente utilizzato per autenticare l’origine. Questo è richiesto per l’autenticazione basata su OAuth. |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso l&#39;identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
  "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
  "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

### Crea una connessione di base [!DNL Generic REST API] utilizzando l&#39;autenticazione di base

Per creare una connessione di base [!DNL Generic REST API] utilizzando l&#39;autenticazione di base, eseguire una richiesta POST all&#39;endpoint `/connections` dell&#39;API [!DNL Flow Service] fornendo le credenziali di autenticazione di base.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Generic REST API]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Generic REST API base connection with basic authentication",
      "description": "Generic REST API base connection with basic authentication",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della connessione di base. Verificare che il nome della connessione di base sia descrittivo, in quanto è possibile utilizzarlo per cercare informazioni sulla connessione di base. |
| `description` | (Facoltativo) Proprietà che è possibile includere per fornire ulteriori informazioni sulla connessione di base. |
| `connectionSpec.id` | ID della specifica di connessione associato a [!DNL Generic REST API]. ID corretto: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | Tipo di autenticazione utilizzato per connettere l’origine a Platform. |
| `auth.params.host` | URL principale utilizzato per connettersi all&#39;origine [!DNL Generic REST API]. |
| `auth.params.username` | Il nome utente che corrisponde all&#39;origine [!DNL Generic REST API]. Questa opzione è necessaria per l’autenticazione di base. |
| `auth.params.password` | Password corrispondente all&#39;origine [!DNL Generic REST API]. Questa opzione è necessaria per l’autenticazione di base. |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione di base appena creata, incluso il relativo identificatore univoco di connessione (`id`). Questo ID è necessario per esplorare la struttura e il contenuto del file sorgente nel passaggio successivo.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL Generic REST API] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati dei protocolli in Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/protocols.md)
