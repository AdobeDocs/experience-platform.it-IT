---
keywords: Experience Platform;home;argomenti popolari;Data Explorer Azure;Data Explorer Azure;Data Explorer Azure
solution: Experience Platform
title: Creare una connessione alla base di Data Explorer di Azure utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare la Data Explorer di Azure a Adobe Experience Platform utilizzando l’API del servizio di flusso.
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
source-git-commit: 0ca900b77275851076a13dcc4b8b4a9995ddd0be
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 2%

---

# Crea un [!DNL Azure Azure Data Explorer] connessione di base utilizzando [!DNL Flow Service] API

>[!NOTE]
>
>La [!DNL Azure Azure Data Explorer] connettore in versione beta. Consulta la sezione [Panoramica delle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo dei connettori con etichetta beta.

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Azure Data Explorer] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL Azure Data Explorer] utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi con [!DNL Azure Data Explorer], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `endpoint` | Il punto finale del [!DNL Azure Data Explorer] server. |
| `database` | Nome della [!DNL Azure Data Explorer] database. |
| `tenant` | L’ID tenant univoco utilizzato per la connessione a [!DNL Azure Data Explorer] database. |
| `servicePrincipalId` | L&#39;ID univoco dell&#39;entità servizio utilizzato per la connessione al [!DNL Azure Data Explorer] database. |
| `servicePrincipalKey` | Chiave univoca dell&#39;entità del servizio utilizzata per la connessione a [!DNL Azure Data Explorer] database. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Azure Data Explorer] è `0479cc14-7651-4354-b233-7480606c2ac3`. |

Per ulteriori informazioni su come iniziare, consulta questo articolo [[!DNL Azure Data Explorer] documento](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL Azure Data Explorer] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Azure Data Explorer]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Azure Data Explorer connection",
        "description": "A connection for Azure Azure Data Explorer",
        "auth": {
            "specName": "Service Principal Based Authentication",
            "params": {
                    "endpoint": "{ENDPOINT}",
                    "database": "{DATABASE}",
                    "tenant": "{TENANT}",
                    "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                    "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
                }
        },
        "connectionSpec": {
            "id": "0479cc14-7651-4354-b233-7480606c2ac3",
            "version": "1.0"
        }
    }'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `auth.params.endpoint` | Il punto finale del [!DNL Azure Data Explorer] server. |
| `auth.params.database` | Nome della [!DNL Azure Data Explorer] database. |
| `auth.params.tenant` | L’ID tenant univoco utilizzato per la connessione a [!DNL Azure Data Explorer] database. |
| `auth.params.servicePrincipalId` | L&#39;ID univoco dell&#39;entità servizio utilizzato per la connessione al [!DNL Azure Data Explorer] database. |
| `auth.params.servicePrincipalKey` | Chiave univoca dell&#39;entità del servizio utilizzata per la connessione a [!DNL Azure Data Explorer] database. |
| `connectionSpec.id` | La [!DNL Azure Data Explorer] ID specifica di connessione: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL Azure Data Explorer] connessione di base utilizzando [!DNL Flow Service] API. Puoi usare questo ID di connessione di base nelle seguenti esercitazioni:

* [Esplorare la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Creare un flusso di dati per trasferire i dati di database a Platform utilizzando [!DNL Flow Service] API](../../collect/database-nosql.md)
