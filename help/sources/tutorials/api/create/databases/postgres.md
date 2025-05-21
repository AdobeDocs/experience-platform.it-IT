---
title: Connettere PostgreSQL Ad Experience Platform Utilizzando L’API Del Servizio Di Flusso
description: Scopri come collegare il tuo database  [!DNL PostgreSQL]  ad Experience Platform utilizzando le API.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: f4200ca71479126e585ac76dd399af4092fdf683
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 3%

---

# Connetti [!DNL PostgreSQL] ad Experience Platform utilizzando l&#39;API [!DNL Flow Service]

Leggere questa guida per scoprire come collegare il database [!DNL PostgreSQL] a Adobe Experience Platform utilizzando [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL PostgreSQL] utilizzando l&#39;API [!DNL Flow Service].

### Utilizzo delle API di Experience Platform

Per informazioni su come effettuare correttamente chiamate alle API di Experience Platform, leggi la guida [guida introduttiva alle API di Experience Platform](../../../../../landing/api-guide.md).

### Raccogli le credenziali richieste

Per ulteriori informazioni sull&#39;autenticazione, leggere la [[!DNL PostgreSQL] panoramica](../../../../connectors/databases/postgres.md).

### Abilita crittografia SSL per la stringa di connessione

È possibile abilitare la crittografia SSL per la stringa di connessione [!DNL PostgreSQL] aggiungendo la stringa di connessione con le proprietà seguenti:

| Proprietà | Descrizione | Esempio |
| --- | --- | --- |
| `EncryptionMethod` | Consente di abilitare la crittografia SSL nei dati [!DNL PostgreSQL]. | <uL><li>`EncryptionMethod=0`(Disabilitato)</li><li>`EncryptionMethod=1`(abilitato)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Convalida il certificato inviato dal database [!DNL PostgreSQL] quando viene applicato `EncryptionMethod`. | <uL><li>`ValidationServerCertificate=0`(Disabilitato)</li><li>`ValidationServerCertificate=1`(abilitato)</li></ul> |

Di seguito è riportato un esempio di stringa di connessione [!DNL PostgreSQL] a cui è stata aggiunta la crittografia SSL: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

## Connetti [!DNL PostgreSQL] ad Experience Platform su Azure {#azure}

Per informazioni su come collegare l&#39;account [!DNL PostgreSQL] ad Experience Platform su Azure, leggere la procedura riportata di seguito.

### Creare una connessione di base {#azure-base}

Una connessione di base mantiene le informazioni tra l’origine e Experience Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID connessione di base, eseguire una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL PostgreSQL] come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticazione basata su chiave account]

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL PostgreSQL] utilizzando l&#39;autenticazione basata su chiave account:

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via connection string",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| ------------- | --------------- |
| `auth.params.connectionString` | Stringa di connessione associata all&#39;account [!DNL PostgreSQL]. Schema della stringa di connessione [!DNL PostgreSQL]: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL PostgreSQL]: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;identificatore univoco (`id`) della connessione di base appena creata.

+++Visualizza esempio di risposta

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

+++

>[!TAB Autenticazione di base]

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL PostgreSQL] utilizzando l&#39;autenticazione di base:

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "3306",
              "database": "postgresql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "Allow"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| ---| --- |
| `auth.params.server` | Il nome o l&#39;indirizzo IP del database [!DNL PostgreSQL]. |
| `auth.params.port` | Numero di porta del server di database. |
| `auth.params.database` | Nome del database [!DNL PostgreSQL]. |
| `auth.params.username` | Il nome utente associato all&#39;autenticazione del database [!DNL PostgreSQL]. |
| `auth.params.password` | La password associata all&#39;autenticazione del database [!DNL PostgreSQL]. |
| `auth.params.sslMode` | Il metodo con cui i dati vengono crittografati durante il trasferimento. I valori disponibili includono: `Disable`, `Allow`, `Prefer`, `Verify Ca` e `Verify Full`. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL PostgreSQL]: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;identificatore univoco (`id`) della connessione di base appena creata.

+++Visualizza esempio di risposta

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

>[!ENDTABS]

## Connetti [!DNL PostgreSQL] ad Experience Platform su Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../../../landing/multi-cloud.md).

Per informazioni su come collegare il database [!DNL PostgreSQL] ad Experience Platform su AWS, leggere la procedura seguente.

### Creare una connessione di base {#aws-base}

Per creare un ID connessione di base, eseguire una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL PostgreSQL] come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL PostgreSQL] per connettersi ad Experience Platform su AWS.

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "3306",
              "database": "postgresql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "false"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| ---| --- |
| `auth.params.server` | Il nome o l&#39;indirizzo IP del database [!DNL PostgreSQL]. |
| `auth.params.port` | Numero di porta del server di database. |
| `auth.params.database` | Nome del database [!DNL PostgreSQL]. |
| `auth.params.username` | Il nome utente associato all&#39;autenticazione del database [!DNL PostgreSQL]. |
| `auth.params.password` | La password associata all&#39;autenticazione del database [!DNL PostgreSQL]. |
| `sslMode` | Valore booleano che controlla se SSL è applicato o meno, a seconda del supporto del server. Il valore predefinito di questa configurazione è `false`. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL PostgreSQL]: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;identificatore univoco (`id`) della connessione di base appena creata.

+++Visualizza esempio di risposta

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

## Passaggi successivi

Dopo aver creato una connessione tra il database [!DNL PostgreSQL] e Experience Platform, è ora possibile procedere con i passaggi successivi e portare i dati di [!DNL PostgreSQL] in Experience Platform. Per ulteriori informazioni, consulta la seguente documentazione:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati del database ad Experience Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/database-nosql.md)
