---
title: Collegare Azure Synapse Analytics Ad Experience Platform Utilizzando L’API Del Servizio Flusso
description: Scopri come collegare il tuo account Azure Synapse Analytics ad Experience Platform utilizzando le API.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 8944ac3f-366d-49c8-882f-11cd0ea766e4
source-git-commit: b8497ede7f90717ed23bcd10b7abe51de18e08a5
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 3%

---

# Connetti [!DNL Azure Synapse Analytics] ad Experience Platform utilizzando l&#39;API [!DNL Flow Service]

>[!IMPORTANT]
>
>L&#39;origine [!DNL Azure Synapse Analytics] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-Time Customer Data Platform Ultimate.

Leggi questa guida per scoprire come collegare il tuo account [!DNL Azure Synapse Analytics] a Adobe Experience Platform utilizzando [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Azure Synapse Analytics] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Per informazioni sull&#39;autenticazione, leggere la [[!DNL Azure Synapse Analytics] panoramica](../../../../connectors/databases/synapse-analytics.md#prerequisites).

### Utilizzo delle API di Experience Platform

Per informazioni su come effettuare correttamente chiamate alle API di Experience Platform, consulta la guida introduttiva [alle API di Experience Platform](../../../../../landing/api-guide.md).

## Connetti [!DNL Azure Synapse Analytics] ad Experience Platform

Per informazioni su come creare una connessione di base e connettere l&#39;account [!DNL Azure Synapse Analytics] ad Experience Platform, leggere quanto segue.

### Creare una connessione di base

Una **connessione di base** memorizza le informazioni chiave che collegano il sistema di origine a Adobe Experience Platform. Ciò include:

* Credenziali di autenticazione dell&#39;origine
* Stato corrente della connessione
* Un ID di connessione di base **univoco**

L&#39;**ID connessione di base** ti consente di sfogliare ed esplorare i file dall&#39;origine, identificando gli elementi da acquisire, insieme ai relativi tipi di dati e formati.

Per creare un ID connessione di base, inviare una richiesta POST all&#39;endpoint `/connections`, incluse le credenziali di autenticazione [!DNL Azure Synapse Analytics] nei parametri della richiesta.

**Formato API**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticazione basata su stringa di connessione]

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Azure Synapse Analytics] utilizzando l&#39;autenticazione basata su stringa di connessione.

+++Visualizza richiesta di esempio

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
| `auth.params.connectionString` | Stringa di connessione utilizzata per connettersi a [!DNL Azure Synapse Analytics]. Il modello di stringa di connessione [!DNL Azure Synapse Analytics] è `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Azure Synapse Analytics]: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`).

+++Visualizza risposta di esempio

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!TAB Autenticazione basata su chiave dell&#39;entità servizio]

La richiesta seguente crea una connessione di base per [!DNL Azure Synapse Analytics] utilizzando l&#39;autenticazione basata sulla chiave dell&#39;entità servizio.

**Richiesta**

+++Visualizza richiesta di esempio

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
      "specName": "Service Principal Key Based Authentication",
      "params": {
        "server": "yourworkspace.sql.azuresynapse.net",
        "database": "SalesDW",
        "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
        "servicePrincipalId": "e7b8c1f2-1234-4c9a-9f3e-abcdef123456",
        "servicePrincipalKey": "~XyZ1234abcDEF5678..."
      }
    },
    "connectionSpec": {
      "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
      "version": "1.0"
    }
  }'
```

| Credenziali | Descrizione |
| --- | --- |
| `auth.params.server` | Il nome di dominio completo dell&#39;endpoint SQL [!DNL Azure Synapse Analytics]. |
| `auth.params.database` | Il nome del database specifico nell&#39;area di lavoro [!DNL Azure Synapse Analytics]. |
| `auth.params.tenant` | L&#39;ID tenant [!DNL Azure Active Directory] associato alla sottoscrizione [!DNL Azure]. |
| `auth.params.servicePrincipalId` | ID client di un&#39;applicazione [!DNL Azure Active Directory]. |
| `auth.params.servicePrincipalKey` | Il segreto client o la password associati all&#39;entità servizio. |
| `connectSpec.id` | ID della specifica di connessione di [!DNL Azure Synapse Analytics]. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`).

+++Visualizza risposta di esempio

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL Azure Synapse Analytics] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] &#x200B;](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati del database ad Experience Platform utilizzando l&#39;API  [!DNL Flow Service] &#x200B;](../../collect/database-nosql.md)
