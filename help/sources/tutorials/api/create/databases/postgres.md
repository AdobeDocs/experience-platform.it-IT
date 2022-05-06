---
keywords: Experience Platform;home;argomenti popolari;PostgreSQL;postgresql;PSQL;psql
solution: Experience Platform
title: Creare una connessione di base PostgreSQL utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a PostgreSQL utilizzando l’API del servizio di flusso.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 3%

---

# Crea un [!DNL PostgreSQL] connessione di base utilizzando [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL PostgreSQL] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL PostgreSQL] utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi con [!DNL PostgreSQL], è necessario fornire la seguente proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | La stringa di connessione associata alla [!DNL PostgreSQL] conto. La [!DNL PostgreSQL] pattern di stringa di connessione: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL PostgreSQL] è `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

Per ulteriori informazioni su come ottenere una stringa di connessione, consulta questo [[!DNL PostgreSQL] documento](https://www.postgresql.org/docs/9.2/app-psql.html).

#### Abilita crittografia SSL per la stringa di connessione

Puoi abilitare la crittografia SSL per il tuo [!DNL PostgreSQL] stringa di connessione aggiungendo la stringa di connessione con le seguenti proprietà:

| Proprietà | Descrizione | Esempio |
| --- | --- | --- |
| `EncryptionMethod` | Consente di abilitare la crittografia SSL nel [!DNL PostgreSQL] dati. | <uL><li>`EncryptionMethod=0`(Disabilitata)</li><li>`EncryptionMethod=1`(Abilitata)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Convalida il certificato inviato dal tuo [!DNL PostgreSQL] database quando `EncryptionMethod` viene applicata. | <uL><li>`ValidationServerCertificate=0`(Disabilitata)</li><li>`ValidationServerCertificate=1`(Abilitata)</li></ul> |

Di seguito è riportato un esempio di [!DNL PostgreSQL] stringa di connessione aggiunta con crittografia SSL: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL PostgreSQL] credenziali di autenticazione come parte dei parametri della richiesta.

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
| `auth.params.connectionString` | La stringa di connessione associata alla [!DNL PostgreSQL] conto. La [!DNL PostgreSQL] pattern di stringa di connessione: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | La [!DNL PostgreSQL] ID delle specifiche di connessione: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della nuova connessione di base creata. Questo ID è necessario per esplorare il tuo [!DNL PostgreSQL] database nell&#39;esercitazione successiva.

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL PostgreSQL] connessione di base tramite [!DNL Flow Service] API. Puoi usare questo ID di connessione di base nelle seguenti esercitazioni:

* [Esplorare la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Creare un flusso di dati per trasferire i dati di database a Platform utilizzando [!DNL Flow Service] API](../../collect/database-nosql.md)
