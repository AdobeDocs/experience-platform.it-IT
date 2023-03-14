---
keywords: Experience Platform;home;argomenti popolari;Azure Data Explorer;Azure Data Explorer;Azure Data Explorer
solution: Experience Platform
title: Creazione di una connessione di base Azure Data Explorer tramite l'API del servizio di flusso
type: Tutorial
description: Scopri come collegare Azure Data Explorer a Adobe Experience Platform utilizzando l’API del servizio Flusso.
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 2%

---

# Creare un [!DNL Azure Azure Data Explorer] connessione di base tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Azure Data Explorer] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Azure Data Explorer] utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi con [!DNL Azure Data Explorer], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `endpoint` | Endpoint del [!DNL Azure Data Explorer] server. |
| `database` | Il nome del [!DNL Azure Data Explorer] database. |
| `tenant` | L’ID tenant univoco utilizzato per connettersi al [!DNL Azure Data Explorer] database. |
| `servicePrincipalId` | ID univoco dell&#39;entità servizio utilizzato per connettersi al [!DNL Azure Data Explorer] database. |
| `servicePrincipalKey` | Chiave dell&#39;entità servizio univoca utilizzata per la connessione a [!DNL Azure Data Explorer] database. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Azure Data Explorer] è `0479cc14-7651-4354-b233-7480606c2ac3`. |

Per ulteriori informazioni su come iniziare, consulta questa [[!DNL Azure Data Explorer] documento](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL Azure Data Explorer] credenziali di autenticazione come parte dei parametri della richiesta.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.endpoint` | Endpoint del [!DNL Azure Data Explorer] server. |
| `auth.params.database` | Il nome del [!DNL Azure Data Explorer] database. |
| `auth.params.tenant` | L’ID tenant univoco utilizzato per connettersi al [!DNL Azure Data Explorer] database. |
| `auth.params.servicePrincipalId` | ID univoco dell&#39;entità servizio utilizzato per connettersi al [!DNL Azure Data Explorer] database. |
| `auth.params.servicePrincipalKey` | Chiave dell&#39;entità servizio univoca utilizzata per la connessione a [!DNL Azure Data Explorer] database. |
| `connectionSpec.id` | Il [!DNL Azure Data Explorer] ID specifica di connessione: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un’ [!DNL Azure Data Explorer] connessione di base tramite [!DNL Flow Service] API. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati del database su Platform utilizzando [!DNL Flow Service] API](../../collect/database-nosql.md)
