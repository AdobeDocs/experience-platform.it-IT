---
title: Collegare I Database Ad Experience Platform Utilizzando L’API Del Servizio Flusso
description: Scopri come collegare i database ad Experience Platform utilizzando le API.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
exl-id: c3974bab-8e67-49a1-b1a5-d453cf7bfd1d
source-git-commit: 96e395e3b3d977d7eb04c400f6fd290977bf1101
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 3%

---

# Connetti [!DNL Databricks] ad Experience Platform utilizzando l&#39;API [!DNL Flow Service]

>[!AVAILABILITY]
>
>* L&#39;origine [!DNL Databricks] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-Time CDP Ultimate.
>
>* L&#39;origine [!DNL Databricks] è in versione beta. Leggi i [termini e condizioni](../../../../home.md#terms-and-conditions) nella panoramica delle origini per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta.

Leggi questa guida per scoprire come collegare il tuo account [!DNL Databricks] a Adobe Experience Platform utilizzando [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzare le API di Experience Platform

Leggi la guida su [come iniziare a utilizzare le API di Experience Platform](../../../../../landing/api-guide.md) per informazioni su come effettuare correttamente chiamate alle API di Experience Platform.

### Configurare l’impostazione dei prerequisiti

Leggi la [[!DNL Databricks] panoramica](../../../../connectors/databases/databricks.md) per scoprire le configurazioni dei prerequisiti che devono essere completate prima di poter connettere il tuo account ad Experience Platform.

### Raccogli le credenziali richieste

Specificare i valori per le credenziali seguenti per connettere [!DNL Databricks] ad Experience Platform.

| Credenziali | Descrizione |
| --- | --- |
| `domain` | URL dell&#39;area di lavoro [!DNL Databricks]. Ad esempio, `https://adb-1234567890123456.7.azuredatabricks.net`. |
| `clusterId` | ID del cluster in [!DNL Databricks]. Questo cluster deve essere già un cluster esistente e deve essere un cluster interattivo. |
| `accessToken` | Il token di accesso che autentica l&#39;account [!DNL Databricks]. È possibile generare il token di accesso utilizzando l&#39;area di lavoro [!DNL Databricks]. |
| `database` | Il nome del database nel delta lake. |
| `connectionSpec.Id` | L&#39;ID della specifica di connessione restituisce le proprietà del connettore di origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Databricks]: `e9d7ec6b-0873-4e57-ad21-b3a7c65e310b`. |

Per ulteriori informazioni, consulta la [[!DNL Databricks] panoramica](../../../../connectors/databases/databricks.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Experience Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` e fornire le credenziali di autenticazione appropriate per l&#39;account [!DNL Databricks].

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per un&#39;origine [!DNL Databricks] utilizzando l&#39;autenticazione del token di accesso.

+++Visualizza esempio di richiesta

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/connections' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d '{
    "name": "Databricks connection to Experience Platform",
    "description": "A Databricks base connection to Experience Platform",
    "auth": {
        "specName": "Access Token Authentication",
        "params": {
          "domain": "https://adb-1234567890123456.7.azuredatabricks.net",
          "clusterId": "xxxx",
          "accessToken": "xxxx",
          "database": "acme-db"
        }
    },
    "connectionSpec": {
        "id": "e9d7ec6b-0873-4e57-ad21-b3a7c65e310b",
        "version": "1.0"
    }
}'
```

| Proprietà | Descrizione |
| --- | --- |
| `auth.params.domain` | URL dell&#39;area di lavoro [!DNL Databricks]. |
| `auth.params.clusterId` | ID del cluster in [!DNL Databricks]. Questo cluster deve essere già esistente e deve essere un cluster interattivo |
| `auth.params.accessToken` | Il token di accesso che autentica l&#39;account [!DNL Databricks]. |
| `auth.params.database` | Il nome del database nel delta lake. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Databricks]. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso l’ID connessione di base.

+++Visualizza esempio di risposta

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione tra l&#39;account [!DNL Databricks] e Experience Platform. Puoi utilizzare l’ID connessione di base appena generato nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati del database ad Experience Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/database-nosql.md)
