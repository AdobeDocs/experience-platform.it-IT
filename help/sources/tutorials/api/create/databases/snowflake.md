---
title: Connettere Snowflake ad Experience Platform utilizzando l’API del servizio Flow
description: Scopri come collegare Adobe Experience Platform a Snowflake utilizzando l’API del servizio Flusso.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 0476c42924bf0163380e650141fad8e50b98d4cf
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 4%

---

# Connetti [!DNL Snowflake] ad Experience Platform utilizzando l&#39;API [!DNL Flow Service]

>[!IMPORTANT]
>
>L&#39;origine [!DNL Snowflake] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-Time Customer Data Platform Ultimate.

Leggi questa guida per scoprire come collegare l&#39;account di origine [!DNL Snowflake] a Adobe Experience Platform utilizzando [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Experience Platform].
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Experience Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Experience Platform

Per informazioni su come effettuare correttamente chiamate alle API di Experience Platform, consulta la guida introduttiva [alle API di Experience Platform](../../../../../landing/api-guide.md).

La sezione seguente fornisce informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Snowflake] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Per informazioni sull&#39;autenticazione, leggere la [[!DNL Snowflake] panoramica](../../../../connectors/databases/snowflake.md#prerequisites).

## Connetti [!DNL Snowflake] ad Experience Platform su Azure {#azure}

>[!WARNING]
>
>L&#39;autenticazione di base (o l&#39;autenticazione della chiave dell&#39;account) per l&#39;origine [!DNL Snowflake] diventerà obsoleta a novembre 2025. Devi passare all’autenticazione basata su coppia di chiavi per continuare a utilizzare l’origine e ad acquisire i dati dal database ad Experience Platform. Per ulteriori informazioni sulla deprecazione, leggere la [[!DNL Snowflake] guida alle best practice per ridurre i rischi di compromissione delle credenziali](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/).

Per informazioni su come collegare l&#39;origine [!DNL Snowflake] ad Experience Platform su Azure, leggere la procedura seguente.

>[!NOTE]
>
>Impostare il flag `PREVENT_UNLOAD_TO_INLINE_URL` su `FALSE` per consentire lo scaricamento dei dati dal database [!DNL Snowflake] in Experience Platform.

### Crea una connessione di base per [!DNL Snowflake] in Experience Platform su Azure {#azure-base}

Una connessione di base mantiene le informazioni tra l’origine e Experience Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, eseguire una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Snowflake] come parte del corpo della richiesta.

**Formato API**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB StringaConnessione]

+++Richiesta

La richiesta seguente crea una connessione di base per [!DNL Snowflake]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "Snowflake base connection",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}"
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.connectionString` | Stringa di connessione utilizzata per connettersi all&#39;istanza [!DNL Snowflake]. Il modello di stringa di connessione per [!DNL Snowflake] è `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Snowflake]: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso l&#39;identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


>[!TAB Autenticazione coppia di chiavi con chiave privata crittografata]

+++Richiesta

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "privateKeyPassphrase": "abcd1234",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.account` | Il nome dell&#39;account [!DNL Snowflake]. |
| `auth.params.username` | Il nome utente associato al tuo account [!DNL Snowflake]. |
| `auth.params.database` | Il database [!DNL Snowflake] da cui verranno estratti i dati. |
| `auth.params.privateKey` | La chiave privata crittografata con codifica [!DNL Base64-] dell&#39;account [!DNL Snowflake]. |
| `auth.params.privateKeyPassphrase` | La passphrase che corrisponde alla chiave privata. |
| `auth.params.warehouse` | Il data warehouse [!DNL Snowflake] in uso. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Snowflake]: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`).

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!TAB Autenticazione coppia di chiavi con chiave privata non crittografata]

+++Richiesta

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with unencrypted private key",
      "description": "Snowflake base connection with unencrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.account` | Il nome dell&#39;account [!DNL Snowflake]. |
| `auth.params.username` | Il nome utente associato al tuo account [!DNL Snowflake]. |
| `auth.params.database` | Il database [!DNL Snowflake] da cui verranno estratti i dati. |
| `auth.params.privateKey` | Chiave privata non crittografata con codifica [!DNL Base64-] dell&#39;account [!DNL Snowflake]. |
| `auth.params.warehouse` | Il data warehouse [!DNL Snowflake] in uso. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Snowflake]: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`).

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!ENDTABS]

## Connetti [!DNL Snowflake] ad Experience Platform su Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../../../landing/multi-cloud.md).

Per informazioni su come collegare l&#39;origine [!DNL Snowflake] ad Experience Platform su AWS, leggere i passaggi seguenti.

### Crea una connessione di base per [!DNL Snowflake] su Experience Platform in AWS {#aws-base}

**Formato API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticazione di base]

La richiesta seguente crea una connessione di base per [!DNL Snowflake] per acquisire dati in Experience Platform su AWS:

+++Richiesta

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection for Experience Platform on AWS",
      "description": "Snowflake base connection for Experience Platform on AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme.snowflakecomputing.com",
              "port": "443",
              "username": "acme-cj123",
              "password": "{PASSWORD}",
              "database": "ACME_DB",
              "warehouse": "COMPUTE_WH",
              "schema": "{SCHEMA}"
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `auth.params.host` | L&#39;URL host al quale il tuo account [!DNL Snowflake] si connette. |
| `auth.params.port` | Numero di porta utilizzato da [!DNL Snowflake] per la connessione a un server tramite Internet. |
| `auth.params.username` | Il nome utente associato al tuo account [!DNL Snowflake]. |
| `auth.params.database` | Il database [!DNL Snowflake] da cui verranno estratti i dati. |
| `auth.params.password` | La password associata al tuo account [!DNL Snowflake]. |
| `auth.params.warehouse` | Il data warehouse [!DNL Snowflake] in uso. |
| `auth.params.schema` | Il nome dello schema associato al database [!DNL Snowflake]. È necessario assicurarsi che anche l&#39;utente a cui si desidera concedere l&#39;accesso al database abbia accesso a questo schema. |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`).

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++

>[!TAB Autenticazione coppia di chiavi con chiave privata non crittografata]

+++Richiesta

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with unencrypted private key",
      "description": "Snowflake base connection with unencrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.account` | Il nome dell&#39;account [!DNL Snowflake]. |
| `auth.params.username` | Il nome utente associato al tuo account [!DNL Snowflake]. |
| `auth.params.database` | Il database [!DNL Snowflake] da cui verranno estratti i dati. |
| `auth.params.privateKey` | Chiave privata non crittografata con codifica [!DNL Base64-] dell&#39;account [!DNL Snowflake]. |
| `auth.params.warehouse` | Il data warehouse [!DNL Snowflake] in uso. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Snowflake]: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++


+++Risposta

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`).

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++

>[!ENDTABS]

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL Snowflake] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] &#x200B;](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati del database ad Experience Platform utilizzando l&#39;API  [!DNL Flow Service] &#x200B;](../../collect/database-nosql.md)
