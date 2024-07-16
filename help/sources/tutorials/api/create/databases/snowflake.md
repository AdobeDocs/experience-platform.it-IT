---
title: Creare una connessione di base al Snowflake utilizzando l’API del servizio Flusso
description: Scopri come collegare Adobe Experience Platform al Snowflake utilizzando l’API del servizio Flusso.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 2%

---

# Creare una connessione di base [!DNL Snowflake] utilizzando l&#39;API [!DNL Flow Service]

>[!IMPORTANT]
>
>L&#39;origine [!DNL Snowflake] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Utilizzare il seguente tutorial per scoprire come creare una connessione di base per [!DNL Snowflake] utilizzando [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

La sezione seguente fornisce informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Snowflake] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Per autenticare l&#39;origine [!DNL Snowflake], è necessario fornire i valori per le seguenti proprietà delle credenziali.

>[!BEGINTABS]

>[!TAB Autenticazione chiave account]

| Credenziali | Descrizione |
| ---------- | ----------- |
| `account` | Un nome di account identifica in modo univoco un account all’interno dell’organizzazione. In questo caso, è necessario identificare in modo univoco un account tra diverse [!DNL Snowflake] organizzazioni. A questo scopo, devi anteporre il nome della tua organizzazione al nome dell’account. Esempio: `orgname-account_name`. Per ulteriori informazioni sui nomi di account, leggere la documentazione di [!DNL Snowflake] su [identificatori di account](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | Il data warehouse [!DNL Snowflake] gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni data warehouse [!DNL Snowflake] è indipendente l&#39;uno dall&#39;altro e deve essere accessibile singolarmente quando si trasferiscono i dati a Platform. |
| `database` | Il database [!DNL Snowflake] contiene i dati che si desidera inserire nella piattaforma. |
| `username` | Nome utente per l&#39;account [!DNL Snowflake]. |
| `password` | Password per l&#39;account utente [!DNL Snowflake]. |
| `role` | Ruolo di controllo di accesso predefinito da utilizzare nella sessione [!DNL Snowflake]. Il ruolo deve essere esistente e già assegnato all&#39;utente specificato. Il ruolo predefinito è `PUBLIC`. |
| `connectionString` | Stringa di connessione utilizzata per connettersi all&#39;istanza [!DNL Snowflake]. Il modello di stringa di connessione per [!DNL Snowflake] è `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Autenticazione coppia di chiavi]

Per utilizzare l&#39;autenticazione con coppia di chiavi, è necessario generare una coppia di chiavi RSA a 2048 bit e quindi fornire i seguenti valori durante la creazione di un account per l&#39;origine [!DNL Snowflake].

| Credenziali | Descrizione |
| --- | --- |
| `account` | Un nome di account identifica in modo univoco un account all’interno dell’organizzazione. In questo caso, è necessario identificare in modo univoco un account tra diverse [!DNL Snowflake] organizzazioni. A questo scopo, devi anteporre il nome della tua organizzazione al nome dell’account. Esempio: `orgname-account_name`. Per ulteriori informazioni sui nomi di account, leggere la documentazione di [!DNL Snowflake] su [identificatori di account](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Il nome utente dell&#39;account [!DNL Snowflake]. |
| `privateKey` | La chiave privata con codifica [!DNL Base64-] del tuo account [!DNL Snowflake]. Puoi generare chiavi private crittografate o non crittografate. Se utilizzi una chiave privata crittografata, devi anche fornire una passphrase di chiave privata durante l’autenticazione in base a Experience Platform. |
| `privateKeyPassphrase` | La passphrase per chiave privata è un ulteriore livello di sicurezza da utilizzare per l&#39;autenticazione con una chiave privata crittografata. Se si utilizza una chiave privata non crittografata, non è necessario fornire la passphrase. |
| `database` | Il database [!DNL Snowflake] che contiene i dati da acquisire per l&#39;Experience Platform. |
| `warehouse` | Il data warehouse [!DNL Snowflake] gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni data warehouse [!DNL Snowflake] è indipendente l&#39;uno dall&#39;altro e deve essere accessibile singolarmente quando si trasferiscono i dati all&#39;Experience Platform. |

Per ulteriori informazioni su questi valori, fare riferimento alla [[!DNL Snowflake] guida all&#39;autenticazione con coppia di chiavi](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

>[!NOTE]
>
>È necessario impostare il flag `PREVENT_UNLOAD_TO_INLINE_URL` su `FALSE` per consentire lo scaricamento dei dati dal database [!DNL Snowflake] su Experience Platform.

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Snowflake] come parte del corpo della richiesta.

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

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso l&#39;identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

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
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
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

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso l&#39;identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!ENDTABS]

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL Snowflake] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati del database in Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/database-nosql.md)
