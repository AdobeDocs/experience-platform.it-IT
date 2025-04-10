---
title: Collegare MariaDB Ad Experience Platform Utilizzando L’API Del Servizio Flusso
description: Scopri come collegare il tuo account MariaDB ad Experience Platform utilizzando le API.
exl-id: 9b7ff394-ca55-4ab4-99ef-85c80b04a6df
source-git-commit: d5d47f9ca3c01424660fe33f8310586a70a32875
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 3%

---

# Connetti [!DNL MariaDB] ad Experience Platform utilizzando l&#39;API [!DNL Flow Service]

Leggi questa guida per scoprire come collegare il tuo account [!DNL MariaDB] a Adobe Experience Platform utilizzando [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL MariaDB] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Per informazioni sull&#39;autenticazione, leggere la [[!DNL MariaDB] panoramica](../../../../connectors/databases/mariadb.md#prerequisites).

### Utilizzo delle API di Experience Platform

Per informazioni su come effettuare correttamente chiamate alle API di Experience Platform, leggi la guida [guida introduttiva alle API di Experience Platform](../../../../../landing/api-guide.md).

## Connetti [!DNL MariaDB] ad Experience Platform su Azure {#azure}

Per informazioni su come collegare l&#39;account [!DNL MariaDB] ad Experience Platform su Azure, leggere la procedura seguente.

### Crea una connessione di base per [!DNL MariaDB] in Experience Platform su Azure {#azure-base}

Una connessione di base mantiene le informazioni tra l’origine e Experience Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

**Formato API**

```https
POST /connections
```

Per creare un ID connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` e fornire le credenziali di autenticazione appropriate per l&#39;account [!DNL MariaDB].

>[!BEGINTABS]

>[!TAB Autenticazione basata su stringa di connessione]

**Richiesta**

La richiesta seguente crea una connessione di base per un&#39;origine [!DNL MariaDB] utilizzando l&#39;autenticazione basata su stringa di connessione.

Esempio di richiesta +++View

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/connections' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d '{
    "name": "MariaDB connection",
    "description": "MariaDB connection",
    "auth": {
        "specName": "Connection String Based Authentication",
        "params": {
            "connectionString": "Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
        }
    },
    "connectionSpec": {
        "id": "3000eb99-cd47-43f3-827c-43caf170f015",
        "version": "1.0"
    }
}'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.connectionString` | Stringa di connessione associata all&#39;autenticazione [!DNL MariaDB]. Schema della stringa di connessione [!DNL MariaDB]: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL MariaDB]: `3000eb99-cd47-43f3-827c-43caf170f015`. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`).

+++Visualizza esempio di risposta

```json
{
    "id": "be3a2d71-1fb6-4fea-ba2d-711fb61fea50",
    "etag": "\"02002624-0000-0200-0000-5e41f7040000\""
}
```

+++

>[!TAB Autenticazione di base]

**Richiesta**

La richiesta seguente crea una connessione di base per un&#39;origine [!DNL MariaDB] utilizzando l&#39;autenticazione di base.

Esempio di richiesta +++View

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MariaDB on Experience Platform using basic auth",
      "description": "MariaDB on Experience Platform using basic auth",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSLMODE}"
          }
      },
      "connectionSpec": {
          "id": "3000eb99-cd47-43f3-827c-43caf170f015",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `auth.params.server` | Il nome o l&#39;IP del database [!DNL MariaDB]. |
| `auth.params.database` | Nome del database. |
| `auth.params.username` | Il nome utente che corrisponde al database. |
| `auth.params.password` | La password che corrisponde al database. |
| `auth.params.sslMode` | Il metodo con cui i dati vengono crittografati durante il trasferimento. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL MariaDB]: `3000eb99-cd47-43f3-827c-43caf170f015`. |

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

>[!ENDTABS]

## Connetti [!DNL MariaDB] ad Experience Platform su Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../../../landing/multi-cloud.md).

Per informazioni su come collegare il tuo account [!DNL MariaDB] ad Experience Platform su AWS, leggi i passaggi seguenti.

### Crea una connessione di base per [!DNL MariaDB] su Experience Platform su AWS {#aws-base}

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL MariaDB] per connettersi ad Experience Platform su AWS.

Esempio di richiesta +++View

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MariaDB on Experience Platform AWS",
      "description": "MariaDB on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSLMODE}"
          }
      },
      "connectionSpec": {
          "id": "3000eb99-cd47-43f3-827c-43caf170f015",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `auth.params.server` | Il nome o l&#39;IP del database [!DNL MariaDB]. |
| `auth.params.database` | Nome del database. |
| `auth.params.username` | Il nome utente che corrisponde al database. |
| `auth.params.password` | La password che corrisponde al database. |
| `auth.params.sslMode` | Il metodo con cui i dati vengono crittografati durante il trasferimento. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL MariaDB]: `3000eb99-cd47-43f3-827c-43caf170f015`. |

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


## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL MariaDB] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati del database ad Experience Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/database-nosql.md)
