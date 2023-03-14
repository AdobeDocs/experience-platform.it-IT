---
keywords: Experience Platform;home;argomenti popolari;Azure Data Lake Storage Gen2;azure data lake storage;Azure
solution: Experience Platform
title: Creare una connessione di base di Azure Data Lake Storage Gen2 utilizzando l'API del servizio Flusso
type: Tutorial
description: Scopri come collegare Adobe Experience Platform ad Azure Data Lake Storage Gen2 utilizzando l’API del servizio Flusso.
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 2%

---

# Creare un [!DNL Azure Data Lake Storage Gen2] connessione di base tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Azure Data Lake Storage Gen2] (di seguito &quot;ADLS Gen2&quot;) utilizzando il [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per creare correttamente una connessione sorgente ADLS Gen2 utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi ad ADLS Gen2, è necessario specificare i valori per le proprietà di connessione seguenti:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `url` | Endpoint per ADLS Gen2. Il modello di endpoint è: `https://<accountname>.dfs.core.windows.net`. |
| `servicePrincipalId` | ID client dell’applicazione. |
| `servicePrincipalKey` | Chiave dell&#39;applicazione. |
| `tenant` | Informazioni tenant contenenti l&#39;applicazione. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per ADLS Gen2 è: `b3ba5556-48be-44b7-8b85-ff2b69b46dc4`. |

Per ulteriori informazioni su questi valori, consulta [questo documento ADLS Gen2](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` fornendo le credenziali di autenticazione ADLS Gen2 come parte dei parametri di richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per ADLS Gen2:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "adls-gen2",
        "description": "Connection for adls-gen2",
        "auth": {
            "specName": "Basic Authentication for adls-gen2",
            "params": {
                "url": "{URL}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
                "tenant": "{TENANT}"
            }
        },
        "connectionSpec": {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.url` | Endpoint URL per l&#39;account ADLS Gen2. |
| `auth.params.servicePrincipalId` | ID dell&#39;entità servizio dell&#39;account ADLS Gen2. |
| `auth.params.servicePrincipalKey` | La chiave dell&#39;entità servizio del tuo account ADLS Gen2. |
| `auth.params.tenant` | Informazioni sul tenant dell&#39;account ADLS Gen2. |
| `connectionSpec.id` | ID specifica connessione ADLS Gen2: `b3ba5556-48be-44b7-8b85-ff2b69b46dc41`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione ADLS Gen2 utilizzando le API ed è stato ottenuto un ID univoco come parte del corpo della risposta. Puoi usare questo ID connessione per [esplorare gli archivi cloud utilizzando l’API del servizio Flow](../../explore/cloud-storage.md).
