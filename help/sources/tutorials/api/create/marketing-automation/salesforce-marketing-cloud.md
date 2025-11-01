---
title: Connettere Salesforce Marketing Cloud Ad Experience Platform Utilizzando L’API Del Servizio Flusso
description: Scopri come collegare il tuo account Marketing Cloud di Salesforce ad Experience Platform utilizzando le API.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 2%

---

# Connetti [!DNL Salesforce Marketing Cloud] ad Experience Platform utilizzando l&#39;API [!DNL Flow Service]

>[!WARNING]
>
>L&#39;origine [!DNL Salesforce Marketing Cloud] diventerà obsoleta a gennaio 2026. Una nuova fonte verrà rilasciata nel corso di quest&#39;anno come alternativa. Una volta rilasciata la nuova origine, è necessario pianificare la migrazione alla nuova origine creando nuove connessioni account e flussi di dati prima della fine di gennaio 2026.

Leggi questa guida per scoprire come collegare il tuo account [!DNL Salesforce Marketing Cloud] a Adobe Experience Platform utilizzando [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Azure Synapse Analytics] utilizzando l&#39;API [!DNL Flow Service].


### Utilizzo delle API di Experience Platform

Per informazioni su come effettuare correttamente chiamate alle API di Experience Platform, consulta la guida introduttiva [alle API di Experience Platform](../../../../../landing/api-guide.md).

La sezione seguente fornisce informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Salesforce Marketing Cloud] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Per informazioni sull&#39;autenticazione, leggere la [[!DNL Salesforce Marketing Cloud] panoramica autenticazione](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md).

### Utilizzo delle API di Experience Platform

Per informazioni su come effettuare correttamente chiamate alle API di Experience Platform, leggi la guida [guida introduttiva alle API di Experience Platform](../../../../../landing/api-guide.md).

## Connetti [!DNL Salesforce Marketing Cloud] ad Experience Platform il [!DNL Azure]

Per informazioni su come creare una connessione di base e connettere l&#39;account [!DNL Salesforce Marketing Cloud] ad Experience Platform il [!DNL Azure], leggi quanto segue.

### Creare una connessione di base {#azure-base}

>[!IMPORTANT]
>
>L&#39;acquisizione di oggetti personalizzati non è attualmente supportata dall&#39;integrazione di origine [!DNL Salesforce Marketing Cloud].

Una **connessione di base** memorizza le informazioni chiave che collegano il sistema di origine a Adobe Experience Platform. Ciò include:

* Credenziali di autenticazione dell&#39;origine
* Stato corrente della connessione
* Un ID di connessione di base **univoco**

L&#39;**ID connessione di base** ti consente di sfogliare ed esplorare i file dall&#39;origine, identificando gli elementi da acquisire, insieme ai relativi tipi di dati e formati.

Per creare un ID connessione di base, inviare una richiesta POST all&#39;endpoint `/connections`, incluse le credenziali di autenticazione [!DNL Salesforce Marketing Cloud] nei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Salesforce Marketing Cloud].

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
    "name": "Salesforce Marketing Cloud base connection for Azure",
    "description": "Salesforce Marketing Cloud base connection for Azure",
    "auth": {
      "specName": "Client-Id-Secret Based Authentication",
      "params": {
        "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst",
        "clientId": "acme-salesforce-marketing-cloud",
        "clientSecret": "xxxx"
      }
    },
    "connectionSpec": {
      "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
      "version": "1.0"
    }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `auth.params.host` |  |
| `auth.params.clientId` | L&#39;ID client associato all&#39;applicazione [!DNL Salesforce Marketing Cloud]. |
| `auth.params.clientSecret` | Il segreto client associato all&#39;applicazione [!DNL Salesforce Marketing Cloud]. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Salesforce Marketing Cloud]: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

+++

+++Visualizza risposta di esempio

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`).

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

## Connetti [!DNL Salesforce Marketing Cloud] ad Experience Platform su Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../../../landing/multi-cloud.md).

Per informazioni su come collegare il tuo account [!DNL Salesforce Marketing Cloud] ad Experience Platform su AWS, leggi i passaggi seguenti.

### Creare una connessione di base {#aws-base}

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Salesforce Service Cloud] per connettersi ad Experience Platform su AWS.

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
    "name": "Salesforce Marketing Cloud base connection for AWS",
    "description": "Salesforce Marketing Cloud base connection for AWS",
    "auth": {
      "specName": "OAuth2 Client Credential",
      "params": {
        "subdomain": "mc563885gzs27c5t9-63k636ttgm",
        "clientId": "3a1b2c3d4e5f67890123456789abcdef",
        "clientSecret": "xxxx"
      }
    },
    "connectionSpec": {
      "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
      "version": "1.0"
    }
  }'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`).

+++Visualizza esempio di risposta

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


## Crea un flusso di dati per [!DNL Salesforce Marketing Cloud] dati

Dopo aver connesso correttamente l&#39;account [!DNL Salesforce Marketing Cloud], è ora possibile [creare un flusso di dati e acquisire dati dal provider di automazione marketing in Experience Platform](../../collect/marketing-automation.md).