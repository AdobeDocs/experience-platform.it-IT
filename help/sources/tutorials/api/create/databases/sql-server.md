---
keywords: Experience Platform;home;argomenti comuni;Microsoft SQL;microsoft sql;sql server;SQL server
solution: Experience Platform
title: Creare una connessione di base di SQL Server utilizzando l'API del servizio di flusso
type: Tutorial
description: Scopri come connettere Adobe Experience Platform a Microsoft SQL Server utilizzando l’API del servizio Flusso.
exl-id: 00455a61-c8c1-42f4-a962-fc16f7370cbd
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 2%

---

# Creare un [!DNL Microsoft] Connessione di base di SQL Server tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Microsoft SQL Server] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Microsoft SQL Server] utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per connettersi a [!DNL Microsoft SQL Server], è necessario fornire la seguente proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | La stringa di connessione associata al tuo [!DNL Microsoft SQL Server] account. Il [!DNL Microsoft SQL Server] modello di stringa di connessione: `Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Microsoft SQL Server] è `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

Per ulteriori informazioni su come ottenere una stringa di connessione, consulta questa [[!DNL Microsoft SQL Server] documento](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL Microsoft SQL Server] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Microsoft SQL Server]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Base connection for sql-server",
        "description": "Base connection for sql-server",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};"
            }
        },
        "connectionSpec": {
            "id": "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
            "version": "1.0"
    }'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `auth.params.connectionString` | La stringa di connessione associata al tuo [!DNL Microsoft SQL Server] account. Il [!DNL Microsoft SQL Server] modello di stringa di connessione: `Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`. |
| `connectionSpec.id` | Il [!DNL Microsoft SQL Server] ID specifica di connessione: `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare il database nell’esercitazione successiva.

```json
{
    "id": "0b8224e4-0de8-4293-8224-e40de80293c6",
    "etag": "\"5802c519-0000-0200-0000-5e4d89520000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un’ [!DNL Microsoft SQL Server] connessione di base tramite [!DNL Flow Service] API. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati del database su Platform utilizzando [!DNL Flow Service] API](../../collect/database-nosql.md)