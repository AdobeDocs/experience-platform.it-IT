---
keywords: Experience Platform;home;argomenti popolari;PostgreSQL;postgresql;PSQL;psql
solution: Experience Platform
title: Creare una connessione di base PostgreSQL utilizzando l’API del servizio Flusso
type: Tutorial
description: Scopri come connettere Adobe Experience Platform a PostgreSQL utilizzando l’API del servizio Flusso.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 3%

---

# Creare un [!DNL PostgreSQL] connessione di base tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL PostgreSQL] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL PostgreSQL] utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi con [!DNL PostgreSQL], è necessario fornire la seguente proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | La stringa di connessione associata al tuo [!DNL PostgreSQL] account. Il [!DNL PostgreSQL] modello di stringa di connessione: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL PostgreSQL] è `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

Per ulteriori informazioni su come ottenere una stringa di connessione, consulta questa [[!DNL PostgreSQL] documento](https://www.postgresql.org/docs/9.2/app-psql.html).

#### Abilita crittografia SSL per la stringa di connessione

Puoi abilitare la crittografia SSL per il tuo [!DNL PostgreSQL] stringa di connessione aggiungendo la stringa di connessione con le seguenti proprietà:

| Proprietà | Descrizione | Esempio |
| --- | --- | --- |
| `EncryptionMethod` | Consente di abilitare la crittografia SSL sul [!DNL PostgreSQL] dati. | <uL><li>`EncryptionMethod=0`(Disabilitata)</li><li>`EncryptionMethod=1`(Abilitata)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Convalida il certificato inviato dal [!DNL PostgreSQL] database quando `EncryptionMethod` viene applicata. | <uL><li>`ValidationServerCertificate=0`(Disabilitata)</li><li>`ValidationServerCertificate=1`(Abilitata)</li></ul> |

Di seguito è riportato un esempio di [!DNL PostgreSQL] stringa di connessione aggiunta con crittografia SSL: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL PostgreSQL] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL PostgreSQL]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test connection for PostgreSQL",
        "description": "Test connection for PostgreSQL",
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
| `auth.params.connectionString` | La stringa di connessione associata al tuo [!DNL PostgreSQL] account. Il [!DNL PostgreSQL] modello di stringa di connessione: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Il [!DNL PostgreSQL] ID delle specifiche di connessione: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’identificatore univoco (`id`) della connessione di base appena creata. Questo ID è necessario per esplorare il tuo [!DNL PostgreSQL] database nell&#39;esercitazione successiva.

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una [!DNL PostgreSQL] connessione di base tramite [!DNL Flow Service] API. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati del database su Platform utilizzando [!DNL Flow Service] API](../../collect/database-nosql.md)
