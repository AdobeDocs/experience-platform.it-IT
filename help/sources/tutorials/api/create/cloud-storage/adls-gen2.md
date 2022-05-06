---
keywords: Experience Platform;home;argomenti popolari;Azure Data Lake Storage Gen2;archiviazione dati azure;Azure
solution: Experience Platform
title: Creare una connessione di base Azure Data Lake Storage Gen2 utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform ad Azure Data Lake Storage Gen2 utilizzando l’API del servizio di flusso.
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 2%

---

# Crea un [!DNL Azure Data Lake Storage Gen2] connessione di base utilizzando [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Azure Data Lake Storage Gen2] (di seguito &quot;ADLS Gen2&quot;) utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per creare correttamente una connessione di origine ADLS Gen2 utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi a ADLS Gen2, è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `url` | Endpoint per ADLS Gen2. Il pattern dell’endpoint è: `https://<accountname>.dfs.core.windows.net`. |
| `servicePrincipalId` | ID client dell&#39;applicazione. |
| `servicePrincipalKey` | La chiave dell&#39;applicazione. |
| `tenant` | Informazioni sul tenant contenente l&#39;applicazione. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per ADLS Gen2 è: `b3ba5556-48be-44b7-8b85-ff2b69b46dc4`. |

Per ulteriori informazioni su questi valori, consulta [questo documento ADLS Gen2](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` endpoint durante la fornitura delle credenziali di autenticazione ADLS Gen2 come parte dei parametri di richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

La seguente richiesta crea una connessione di base per ADLS Gen2:

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
| `auth.params.servicePrincipalId` | L&#39;ID principale del servizio del tuo account ADLS Gen2. |
| `auth.params.servicePrincipalKey` | Chiave principale del servizio dell&#39;account ADLS Gen2. |
| `auth.params.tenant` | Informazioni sul tenant del tuo account ADLS Gen2. |
| `connectionSpec.id` | ID della specifica di connessione ADLS Gen2: `b3ba5556-48be-44b7-8b85-ff2b69b46dc41`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione di base creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione ADLS Gen2 utilizzando le API e come parte del corpo della risposta è stato ottenuto un ID univoco. Puoi usare questo ID connessione per [esplorare gli archivi cloud utilizzando l’API del servizio di flusso](../../explore/cloud-storage.md).
