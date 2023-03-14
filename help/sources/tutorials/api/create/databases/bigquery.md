---
keywords: Experience Platform;home;argomenti popolari;bigquery;Google;google;Google BigQuery
solution: Experience Platform
title: Creare una connessione di base BigQuery Google utilizzando l’API del servizio Flow
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a Google BigQuery utilizzando l’API del servizio Flow.
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 2%

---

# Creare un [!DNL Google BigQuery] connessione di base tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Google BigQuery] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Sorgenti](../../../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Google BigQuery] utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi [!DNL Google BigQuery] In Platform, devi fornire i seguenti valori di autenticazione OAuth 2.0:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `project` | ID progetto predefinito [!DNL Google BigQuery] progetto su cui eseguire la query. |
| `clientID` | Valore ID utilizzato per generare il token di aggiornamento. |
| `clientSecret` | Valore segreto utilizzato per generare il token di aggiornamento. |
| `refreshToken` | Il token di aggiornamento ottenuto da [!DNL Google] utilizzato per autorizzare l’accesso a [!DNL Google BigQuery]. |
| `largeResultsDataSetId` | Il predefinito  [!DNL Google BigQuery] ID del set di dati necessario per abilitare il supporto per set di risultati di grandi dimensioni. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Google BigQuery] è: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

Per ulteriori informazioni su questi valori, consulta [[!DNL Google BigQuery] documento](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL Google BigQuery] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Google BigQuery]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection",
        "description": "Google BigQuery connection",
        "auth": {
            "specName": "Basic Authentication",
            "type": "OAuth2.0",
            "params": {
                    "project": "{PROJECT}",
                    "clientId": "{CLIENT_ID},
                    "clientSecret": "{CLIENT_SECRET}",
                    "refreshToken": "{REFRESH_TOKEN}"
                }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `auth.params.project` | ID progetto predefinito [!DNL Google BigQuery] progetto da interrogare. contro. |
| `auth.params.clientId` | Valore ID utilizzato per generare il token di aggiornamento. |
| `auth.params.clientSecret` | Valore client utilizzato per generare il token di aggiornamento. |
| `auth.params.refreshToken` | Il token di aggiornamento ottenuto da [!DNL Google] utilizzato per autorizzare l’accesso a [!DNL Google BigQuery]. |
| `connectionSpec.id` | Il [!DNL Google BigQuery] ID specifica di connessione: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una [!DNL Google BigQuery] connessione di base tramite [!DNL Flow Service] API. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati del database su Platform utilizzando [!DNL Flow Service] API](../../collect/database-nosql.md)
