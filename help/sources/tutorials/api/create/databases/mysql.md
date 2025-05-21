---
title: Connettere MySQL ad Experience Platform utilizzando l’API del servizio Flusso
description: Scopri come collegare il database MySQL ad Experience Platform utilizzando le API.
exl-id: 273da568-84ed-4a3d-bfea-0f5b33f1551a
source-git-commit: b73ced639100c95f6c62be92d4796a206a688958
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 5%

---

# Connetti [!DNL MySQL] ad Experience Platform utilizzando l&#39;API [!DNL Flow Service]

Leggi questa guida per scoprire come collegare il tuo account [!DNL MySQL] a Adobe Experience Platform utilizzando [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL MySQL] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Per informazioni sull&#39;autenticazione, leggere la [[!DNL MySQL] panoramica](../../../../connectors/databases/mysql.md#prerequisites).

### Utilizzo delle API di Experience Platform

Per informazioni su come effettuare correttamente chiamate alle API di Experience Platform, leggi la guida [guida introduttiva alle API di Experience Platform](../../../../../landing/api-guide.md).

## Connetti [!DNL MySQL] ad Experience Platform su Azure {#azure}

Per informazioni su come collegare l&#39;account [!DNL MySQL] ad Experience Platform su Azure, leggere la procedura seguente.

### Crea una connessione di base per [!DNL MySQL] in Experience Platform su Azure {#azure-base}

Una connessione di base collega l’origine ad Experience Platform, memorizzando i dettagli di autenticazione, lo stato della connessione e un ID univoco. Utilizza questo ID per sfogliare i file sorgente e identificare elementi specifici da acquisire, compresi i relativi tipi di dati e formati.

**Formato API**

```https
POST /connections
```

Per creare un ID connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` e fornire le credenziali di autenticazione [!DNL MySQL] come parte dei parametri della richiesta.

>[!BEGINTABS]

>[!TAB Autenticazione basata su stringa di connessione]

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL MySQL] utilizzando l&#39;autenticazione basata su stringa di connessione.

+++Esempio di richiesta View

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Connection String,
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `auth.params.connectionString` | La stringa di connessione [!DNL MySQL] associata al tuo account. Schema della stringa di connessione [!DNL MySQL]: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL MySQL]: `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`).

+++Visualizza esempio di risposta

```json
{
    "id": "1a444165-3439-4c16-8441-653439dc166a",
    "etag": "\"5b04c219-0000-0200-0000-5e179c8f0000\""
}
```

+++

>[!TAB Autenticazione di base]

**Richiesta**

La richiesta seguente crea una connessione di base per un&#39;origine [!DNL MySQL] utilizzando l&#39;autenticazione di base.

+++Esempio di richiesta View

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Basic Authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "443",
              "database": "mysql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "DISABLED"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `auth.params.server` | Il nome o l&#39;IP del database [!DNL MySQL]. |
| `auth.params.database` | Nome del database. |
| `auth.params.username` | Il nome utente che corrisponde al database. |
| `auth.params.password` | La password che corrisponde al database. |
| `auth.params.sslMode` | Il metodo con cui i dati vengono crittografati durante il trasferimento. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL MySQL]: `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`).

+++Visualizza esempio di risposta

```json
{
    "id": "025d4158-4113-403b-b551-e81724d3880c",
    "etag": "\"ae004437-0000-0200-0000-67ee107e0000\""
}
```

+++

>[!ENDTABS]

## Connetti [!DNL MySQL] ad Experience Platform su Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../../../landing/multi-cloud.md).

Per informazioni su come collegare il tuo account [!DNL MySQL] ad Experience Platform su AWS, leggi i passaggi seguenti.

### Crea una connessione di base per [!DNL MySQL] su Experience Platform su AWS {#aws-base}

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL MySQL] per connettersi ad Experience Platform su AWS.

+++Esempio di richiesta View

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL on Experience Platform AWS",
      "description": "MySQL on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "443",
              "database": "mysql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "false"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `auth.params.server` | Il nome o l&#39;IP del database [!DNL MySQL]. |
| `auth.params.database` | Nome del database. |
| `auth.params.username` | Il nome utente che corrisponde al database. |
| `auth.params.password` | La password che corrisponde al database. |
| `auth.params.sslMode` | Valore booleano che controlla se SSL è applicato o meno, a seconda del supporto del server. Il valore predefinito di questa configurazione è `false`. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL MySQL]: `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`).

+++Visualizza esempio di risposta

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

## Crea un flusso di dati per [!DNL MySQL] dati

Dopo aver connesso correttamente il database [!DNL MySQL], è ora possibile [creare un flusso di dati e acquisire dati dal database in Experience Platform](../../collect/database-nosql.md).