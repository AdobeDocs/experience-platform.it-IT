---
title: Collegare Oracle DB Ad Experience Platform Utilizzando L’API Del Servizio Flusso
description: Scopri come collegare Oracle DB ad Experience Platform utilizzando le API.
exl-id: b1cea714-93ff-425f-8e12-6061da97d094
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 2%

---

# Connetti [!DNL Oracle DB] ad Experience Platform utilizzando l&#39;API [!DNL Flow Service]

Leggi questa guida per scoprire come collegare il tuo account [!DNL Oracle DB] a Adobe Experience Platform utilizzando [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Oracle] utilizzando l&#39;API [!DNL Flow Service].

### Utilizzo delle API di Experience Platform

Per informazioni su come effettuare correttamente chiamate alle API di Experience Platform, consulta la guida introduttiva [alle API di Experience Platform](../../../../../landing/api-guide.md).

### Raccogli le credenziali richieste

Per informazioni sull&#39;autenticazione, leggere la [[!DNL Oracle DB] panoramica](../../../../connectors/databases/oracle.md#prerequisites).

## Connetti [!DNL Oracle DB] ad Experience Platform su Azure {#azure}

Per informazioni su come collegare l&#39;account [!DNL Oracle DB] ad Experience Platform su Azure, leggere la procedura seguente.

### Crea una connessione di base per [!DNL Oracle DB] in Experience Platform su Azure {#azure-base}

Una connessione di base collega l’origine ad Experience Platform, memorizzando i dettagli di autenticazione, lo stato della connessione e un ID univoco. Utilizza questo ID per sfogliare i file sorgente e identificare elementi specifici da acquisire, compresi i relativi tipi di dati e formati.

**Formato API**

```https
POST /connections
```

Per creare un ID connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` e fornire le credenziali di autenticazione [!DNL Oracle DB] come parte dei parametri della richiesta.

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Oracle DB] utilizzando l&#39;autenticazione della stringa di connessione.

+++Visualizza richiesta


```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Oracle DB base connection",
    "description": "A base connection to connect Oracle DB to Experience Platform on Azure",
    "auth": {
      "specName": "ConnectionString",
      "params": {
        "connectionString": "Host={HOST};Port={PORT};Sid={SID};UserId={USERNAME};Password={PASSWORD}"
      }
    },
    "connectionSpec": {
      "id": "d6b52d86-f0f8-475f-89d4-ce54c8527328",
      "version": "1.0"
    }
  }'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `auth.params.connectionString` | Stringa di connessione utilizzata per connettersi a [!DNL Oracle DB]. Schema della stringa di connessione [!DNL Oracle DB]: `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Oracle]: `d6b52d86-f0f8-475f-89d4-ce54c8527328`. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`).

+++Visualizza risposta

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

+++

## Connetti [!DNL Oracle DB] ad Experience Platform su Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../../../landing/multi-cloud.md).

Per informazioni su come collegare il tuo account [!DNL Oracle DB] ad Experience Platform su AWS, leggi i passaggi seguenti.

### Crea una connessione di base per [!DNL Oracle DB] su Experience Platform su AWS {#aws-base}

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Oracle DB] per connettersi ad Experience Platform su AWS.

+++Visualizza richiesta

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle DB on Experience Platform AWS",
      "description": "Oracle DB on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "diy.us-dawkins-1.oraclecloud.com",
              "port": "1521",
              "database": "mcmg_profits_diy.oraclecloud.com",
              "username": "Admin",
              "password": "xxxx",
              "schema": "ADMIN",
              "sslMode": "true"
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
| `auth.params.server` | L&#39;indirizzo IP o il nome host del server [!DNL Oracle DB]. |
| `auth.params.port` | Il numero di porta del server [!DNL Oracle DB]. |
| `auth.params.database` | Nome dell&#39;istanza [!DNL Oracle DB] a cui ci si connette. |
| `auth.params.username` | L&#39;account utente associato all&#39;istanza [!DNL Oracle DB]. |
| `auth.prams.password` | Password corrispondente all&#39;account utente [!DNL Oracle DB]. |
| `auth.params.schema` | Schema contenente gli oggetti di database. |
| `auth.params.sslMode` | Valore booleano che indica se le misure SSL sono applicate o meno. |
| `connectionSpec.id` | ID della specifica di connessione corrispondente all&#39;origine [!DNL Oracle DB]. Questo valore ID è fisso come: `d6b52d86-f0f8-475f-89d4-ce54c8527328.` |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso l&#39;identificatore univoco (`id`) e i corrispondenti. Puoi usare l&#39;ID per [creare la connessione di origine](../../collect/database-nosql.md#create-a-source-connection) e `etag` per [aggiornare l&#39;account](../../update.md).

+++Visualizza risposta

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++


## Crea un flusso di dati per [!DNL Oracle DB] dati

Dopo aver connesso correttamente l&#39;account [!DNL Oracle DB], è ora possibile [creare un flusso di dati e acquisire dati dal database in Experience Platform](../../collect/database-nosql.md).