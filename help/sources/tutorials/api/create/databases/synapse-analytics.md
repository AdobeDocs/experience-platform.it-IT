---
keywords: Experience Platform;home;argomenti popolari;Synapse;sinapse;Azure synapse Analytics
solution: Experience Platform
title: Creare una connessione di base di Analytics Azure synapse utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Azure synapse Analytics a Adobe Experience Platform utilizzando l’API del servizio di flusso.
exl-id: 8944ac3f-366d-49c8-882f-11cd0ea766e4
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 2%

---

# Crea un [!DNL Azure Synapse Analytics] connessione di base utilizzando [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Azure Synapse Analytics] (in appresso denominato &quot;[!DNL Synapse]&quot;) utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL Synapse] utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi con [!DNL Synapse], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Stringa di connessione utilizzata per la connessione [!DNL Synapse]. La [!DNL Synapse] pattern di stringa di connessione `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Synapse] è: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79` |

Per ulteriori informazioni su come ottenere una stringa di connessione, consulta [documento di sincronizzazione](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure?toc=%2Fazure%2Fsynapse-analytics%2Fsql-data-warehouse%2Ftoc.json&amp;bc=%2Fazure%2Fsynapse-analytics%2Fsql-data-warehouse%2Fbreadcrumb%2Ftoc.json&amp;tabs=azure-powershell).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL Synapse] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Synapse]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for Azure Synapse Analytics",
        "description": "Connection for Azure Synapse Analytics",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        },
        "connectionSpec": {
            "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
            "version": "1.0"
        }
    }'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `auth.params.connectionString` | Stringa di connessione utilizzata per la connessione [!DNL Synapse]. La [!DNL Synapse] pattern di stringa di connessione `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |
| `connectionSpec.id` | La [!DNL Synapse] ID della specifica di connessione: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare il database nell’esercitazione successiva.

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL Synapse] connessione di base utilizzando [!DNL Flow Service] API. Puoi usare questo ID di connessione di base nelle seguenti esercitazioni:

* [Esplorare la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Creare un flusso di dati per trasferire i dati di database a Platform utilizzando [!DNL Flow Service] API](../../collect/database-nosql.md)
