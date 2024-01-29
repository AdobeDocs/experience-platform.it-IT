---
title: Creare una connessione di base al Snowflake utilizzando l’API del servizio Flusso
description: Scopri come collegare Adobe Experience Platform al Snowflake utilizzando l’API del servizio Flusso.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 3%

---

# Creare un [!DNL Snowflake] connessione di base tramite [!DNL Flow Service] API

>[!IMPORTANT]
>
>Il [!DNL Snowflake] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Utilizza il seguente tutorial per scoprire come creare una connessione di base per [!DNL Snowflake] utilizzando [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

La sezione seguente fornisce informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Snowflake] utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per autenticare le credenziali, è necessario fornire i valori per le seguenti proprietà [!DNL Snowflake] sorgente.

>[!BEGINTABS]

>[!TAB Autenticazione chiave account]

| Credenziali | Descrizione |
| ---------- | ----------- |
| `account` | Un nome di account identifica in modo univoco un account all’interno dell’organizzazione. In questo caso, devi identificare in modo univoco un account tra diversi [!DNL Snowflake] organizzazioni. A questo scopo, devi anteporre il nome della tua organizzazione al nome dell’account. Ad esempio: `orgname-account_name`. Per ulteriori informazioni sui nomi degli account, leggere [!DNL Snowflake] documentazione su [identificatori dell’account](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | Il [!DNL Snowflake] warehouse gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni [!DNL Snowflake] il data warehouse è indipendente l’uno dall’altro e deve essere accessibile singolarmente quando si trasferiscono i dati su Platform. |
| `database` | Il [!DNL Snowflake] Il database contiene i dati che desideri inserire in Platform. |
| `username` | Nome utente per [!DNL Snowflake] account. |
| `password` | La password per [!DNL Snowflake] account utente. |
| `role` | Ruolo di controllo di accesso predefinito da utilizzare nel [!DNL Snowflake] sessione. Il ruolo deve essere esistente e già assegnato all&#39;utente specificato. Il ruolo predefinito è `PUBLIC`. |
| `connectionString` | Stringa di connessione utilizzata per la connessione al [!DNL Snowflake] dell&#39;istanza. Schema della stringa di connessione per [!DNL Snowflake] è `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Autenticazione coppia di chiavi]

Per utilizzare l&#39;autenticazione con coppia di chiavi, è necessario generare una coppia di chiavi RSA a 2048 bit e quindi fornire i seguenti valori durante la creazione di un account per [!DNL Snowflake] sorgente.

| Credenziali | Descrizione |
| --- | --- |
| `account` | Un nome di account identifica in modo univoco un account all’interno dell’organizzazione. In questo caso, devi identificare in modo univoco un account tra diversi [!DNL Snowflake] organizzazioni. A questo scopo, devi anteporre il nome della tua organizzazione al nome dell’account. Ad esempio: `orgname-account_name`. Per ulteriori informazioni sui nomi degli account, leggere [!DNL Snowflake] documentazione su [identificatori dell’account](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Il nome utente del [!DNL Snowflake] account. |
| `privateKey` | Il [!DNL Base64-]chiave privata codificata del tuo [!DNL Snowflake] account. Puoi generare chiavi private crittografate o non crittografate. Se utilizzi una chiave privata crittografata, devi anche fornire una passphrase di chiave privata durante l’autenticazione in base a Experienci Platform. |
| `privateKeyPassphrase` | La passphrase per chiave privata è un ulteriore livello di sicurezza da utilizzare per l&#39;autenticazione con una chiave privata crittografata. Se si utilizza una chiave privata non crittografata, non è necessario fornire la passphrase. |
| `database` | Il [!DNL Snowflake] database contenente i dati da acquisire in Experienci Platform. |
| `warehouse` | Il [!DNL Snowflake] warehouse gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni [!DNL Snowflake] warehouse è indipendente l&#39;uno dall&#39;altro e deve essere accessibile singolarmente quando si trasferiscono i dati ad Experienci Platform. |

Per ulteriori informazioni su questi valori, fare riferimento al [[!DNL Snowflake] guida all’autenticazione con coppia di chiavi](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

>[!NOTE]
>
>È necessario impostare `PREVENT_UNLOAD_TO_INLINE_URL` contrassegna per `FALSE` per consentire lo scaricamento dei dati dal [!DNL Snowflake] database di cui eseguire l&#39;Experience Platform.

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL Snowflake] credenziali di autenticazione come parte del corpo della richiesta.

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
| `auth.params.connectionString` | Stringa di connessione utilizzata per la connessione al [!DNL Snowflake] dell&#39;istanza. Schema della stringa di connessione per [!DNL Snowflake] è `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | Il [!DNL Snowflake] ID specifica di connessione: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso il relativo identificatore univoco di connessione (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

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
| `auth.params.account` | Il nome del tuo [!DNL Snowflake] account. |
| `auth.params.username` | Il nome utente associato al tuo [!DNL Snowflake] account. |
| `auth.params.database` | Il [!DNL Snowflake] database da cui verranno estratti i dati. |
| `auth.params.privateKey` | Il [!DNL Base64-]chiave privata crittografata codificata del tuo [!DNL Snowflake] account. |
| `auth.params.privateKeyPassphrase` | La passphrase che corrisponde alla chiave privata. |
| `auth.params.warehouse` | Il [!DNL Snowflake] data warehouse in uso. |
| `connectionSpec.id` | Il [!DNL Snowflake] ID specifica di connessione: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso il relativo identificatore univoco di connessione (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

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
| `auth.params.account` | Il nome del tuo [!DNL Snowflake] account. |
| `auth.params.username` | Il nome utente associato al tuo [!DNL Snowflake] account. |
| `auth.params.database` | Il [!DNL Snowflake] database da cui verranno estratti i dati. |
| `auth.params.privateKey` | Il [!DNL Base64-]chiave privata non crittografata codificata del tuo [!DNL Snowflake] account. |
| `auth.params.warehouse` | Il [!DNL Snowflake] data warehouse in uso. |
| `connectionSpec.id` | Il [!DNL Snowflake] ID specifica di connessione: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso il relativo identificatore univoco di connessione (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!ENDTABS]

Seguendo questa esercitazione, hai creato una [!DNL Snowflake] connessione di base tramite [!DNL Flow Service] API. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati del database su Platform utilizzando [!DNL Flow Service] API](../../collect/database-nosql.md)
