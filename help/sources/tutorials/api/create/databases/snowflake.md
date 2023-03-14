---
keywords: Experience Platform;home;argomenti popolari;Snowflake;snowflake
solution: Experience Platform
title: Creare una connessione di base al Snowflake utilizzando l’API del servizio Flusso
type: Tutorial
description: Scopri come collegare Adobe Experience Platform al Snowflake utilizzando l’API del servizio Flusso.
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 2%

---

# Creare un [!DNL Snowflake] connessione di base tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Snowflake] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

La sezione seguente fornisce informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Snowflake] utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi con [!DNL Snowflake], è necessario fornire le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| --- | --- |
| `account` | Il nome completo dell&#39;account associato al [!DNL Snowflake] account. Un sistema completo [!DNL Snowflake] il nome account include il nome account, l’area geografica e la piattaforma cloud. Ad esempio, `cj12345.east-us-2.azure`. Per ulteriori informazioni sui nomi degli account, consulta questa [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| `warehouse` | Il [!DNL Snowflake] warehouse gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni [!DNL Snowflake] il data warehouse è indipendente l’uno dall’altro e deve essere accessibile singolarmente quando si trasferiscono i dati su Platform. |
| `database` | Il [!DNL Snowflake] Il database contiene i dati che desideri inserire in Platform. |
| `username` | Nome utente per [!DNL Snowflake] account. |
| `password` | La password per [!DNL Snowflake] account utente. |
| `connectionString` | Stringa di connessione utilizzata per la connessione al [!DNL Snowflake] dell&#39;istanza. Schema della stringa di connessione per [!DNL Snowflake] è `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Snowflake] è `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

Per ulteriori informazioni su come iniziare, consulta questa [[!DNL Snowflake] documento](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL Snowflake] credenziali di autenticazione come parte del corpo della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

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
          "specName": "ConnectionString,
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

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso il relativo identificatore univoco di connessione (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Seguendo questa esercitazione, hai creato una [!DNL Snowflake] connessione di base tramite [!DNL Flow Service] API. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati del database su Platform utilizzando [!DNL Flow Service] API](../../collect/database-nosql.md)
