---
keywords: Experience Platform;casa;argomenti popolari;generico REST;riposo generico
solution: Experience Platform
title: Creare una connessione di base API REST generica utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare l’API REST generica a Adobe Experience Platform utilizzando l’API del servizio di flusso.
exl-id: 6b414868-503e-49d5-8f4a-5b2fc003dab0
source-git-commit: 1f2ae53e5503618b7ac12628923b30c457fd17e2
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 1%

---

# Creare una connessione di base API REST generica utilizzando [!DNL Flow Service] API

>[!NOTE]
>
>La [!DNL Generic REST API] la sorgente è in versione beta. Consulta la sezione [Panoramica delle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo dei connettori con etichetta beta.

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Generic REST API] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi con [!DNL Generic REST API], è necessario fornire credenziali valide per il tipo di autenticazione desiderato. [!DNL Generic REST API] supporta sia il codice di aggiornamento OAuth 2 che l’autenticazione di base. Per informazioni sulle credenziali per i due tipi di autenticazione supportati, vedere le tabelle seguenti.

#### Codice di aggiornamento OAuth 2

| Credenziali | Descrizione |
| --- | --- |
| `host` | L&#39;URL host della sorgente a cui stai effettuando la richiesta. Questo valore è obbligatorio e non può essere bypassato utilizzando `requestParameterOverride`. |
| `authorizationTestUrl` | (Facoltativo) L&#39;URL del test di autorizzazione viene utilizzato per convalidare le credenziali durante la creazione di una connessione di base. Se non viene fornito, le credenziali vengono automaticamente controllate durante il passaggio di creazione della connessione di origine. |
| `clientId` | (Facoltativo) L&#39;ID client associato al tuo account utente. |
| `clientSecret` | (Facoltativo) Il segreto client associato al tuo account utente. |
| `accessToken` | Credenziale di autenticazione principale utilizzata per accedere all’applicazione. Il token di accesso rappresenta l’autorizzazione dell’applicazione per accedere a specifici aspetti dei dati di un utente. Questo valore è obbligatorio e non può essere bypassato utilizzando `requestParameterOverride`. |
| `refreshToken` | (Facoltativo) Token utilizzato per generare un nuovo token di accesso quando il token di accesso è scaduto. |
| `expirationDate` | (Facoltativo) Un valore nascosto che definisce la data di scadenza del token di accesso. |
| `accessTokenUrl` | (Facoltativo) L&#39;endpoint URL utilizzato per recuperare il token di accesso. |
| `requestParameterOverride` | (Facoltativo) Proprietà che consente di specificare i parametri delle credenziali da ignorare. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Generic REST API] è: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

#### Autenticazione di base

| Credenziali | Descrizione |
| --- | --- |
| `host` | L&#39;URL host della sorgente a cui stai effettuando la richiesta. |
| `username` | Nome utente corrispondente al tuo account utente. |
| `password` | Password corrispondente al tuo account utente. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Generic REST API] è: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

[!DNL Generic REST API] supporta sia l’autenticazione di base che il codice di aggiornamento OAuth 2. Per informazioni su come eseguire l’autenticazione con uno dei due tipi di autenticazione, consulta gli esempi seguenti.

### Crea un [!DNL Generic REST API] connessione di base tramite codice di aggiornamento OAuth 2

Per creare un ID di connessione di base utilizzando il codice di aggiornamento OAuth 2, invia una richiesta POST al `/connections` durante la fornitura delle credenziali OAuth 2.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Nome della connessione di base. Assicurati che il nome della connessione di base sia descrittivo, in quanto puoi utilizzarlo per cercare informazioni sulla connessione di base. |
| `description` | (Facoltativo) Proprietà che è possibile includere per fornire ulteriori informazioni sulla connessione di base. |
| `connectionSpec.id` | ID della specifica di connessione associata a [!DNL Generic REST API]. Questo ID fisso è: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | Il tipo di autenticazione utilizzato per autenticare l’origine in Platform. |
| `auth.params.host` | L’URL principale utilizzato per connettersi al [!DNL Generic REST API] sorgente. |
| `auth.params.accessToken` | Il token di accesso corrispondente utilizzato per autenticare l&#39;origine. Questo è necessario per l’autenticazione basata su OAuth. |

**Risposta**

Una risposta corretta restituisce la nuova connessione appena creata, incluso il relativo identificatore di connessione univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
  "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
  "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

### Crea un [!DNL Generic REST API] connessione di base tramite autenticazione di base

Per creare una [!DNL Generic REST API] connessione di base utilizzando l’autenticazione di base, effettuare una richiesta di POST al `/connections` punto finale [!DNL Flow Service] API fornendo le credenziali di autenticazione di base.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Nome della connessione di base. Assicurati che il nome della connessione di base sia descrittivo, in quanto puoi utilizzarlo per cercare informazioni sulla connessione di base. |
| `description` | (Facoltativo) Proprietà che è possibile includere per fornire ulteriori informazioni sulla connessione di base. |
| `connectionSpec.id` | ID della specifica di connessione associata a [!DNL Generic REST API]. Questo ID fisso è: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | Tipo di autenticazione utilizzato per collegare l’origine a Platform. |
| `auth.params.host` | L’URL principale utilizzato per connettersi al [!DNL Generic REST API] sorgente. |
| `auth.params.username` | Il nome utente che corrisponde al tuo [!DNL Generic REST API] sorgente. Questo è necessario per l’autenticazione di base. |
| `auth.params.password` | La password che corrisponde alla tua [!DNL Generic REST API] sorgente. Questo è necessario per l’autenticazione di base. |

**Risposta**

Una risposta corretta restituisce la nuova connessione di base creata, incluso l&#39;identificatore di connessione univoco (`id`). Questo ID è necessario per esplorare la struttura file e il contenuto della tua sorgente nel passaggio successivo.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL Generic REST API] connessione di base utilizzando [!DNL Flow Service] API. Puoi usare questo ID di connessione di base nelle seguenti esercitazioni:

* [Esplorare la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Creare un flusso di dati per trasferire i dati dei protocolli a Platform utilizzando [!DNL Flow Service] API](../../collect/protocols.md)
