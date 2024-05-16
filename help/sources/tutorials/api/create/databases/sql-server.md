---
title: Creare una connessione di base di Microsoft SQL Server utilizzando l'API del servizio di flusso
type: Tutorial
description: Scopri come connettere Adobe Experience Platform a Microsoft SQL Server utilizzando l’API del servizio Flusso.
exl-id: 00455a61-c8c1-42f4-a962-fc16f7370cbd
source-git-commit: 1828dd76e9ff317f97e9651331df3e49e44efff5
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 5%

---

# Creare un [!DNL Microsoft] Connessione di base di SQL Server tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Leggi questa esercitazione per scoprire come creare una connessione di base per [!DNL Microsoft SQL Server] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experienci Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Microsoft SQL Server] utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste {#gather-required-credentials}

Per connettersi a [!DNL Microsoft SQL Server], è necessario fornire la seguente proprietà di connessione:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| `connectionString` | La stringa di connessione associata al tuo [!DNL Microsoft SQL Server] account. Il modello di stringa di connessione dipende dall&#39;utilizzo del nome del server o dell&#39;istanza per l&#39;origine dati:<ul><li>Stringa di connessione che utilizza il nome del server: `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>Stringa di connessione che utilizza il nome dell’istanza:`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |
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
              "connectionString": "Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword"
          }
      },
      "connectionSpec": {
          "id": "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
          "version": "1.0"
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `auth.params.connectionString` | La stringa di connessione associata al tuo [!DNL Microsoft SQL Server] account. Leggi la sezione su [raccolta delle credenziali richieste](#gather-required-credentials) per ulteriori informazioni. |
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