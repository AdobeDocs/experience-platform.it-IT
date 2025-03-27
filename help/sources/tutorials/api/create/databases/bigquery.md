---
title: Connettere Google BigQuery Ad Experience Platform Utilizzando L’API Del Servizio Flusso
description: Scopri come collegare Adobe Experience Platform a Google BigQuery utilizzando l’API del servizio Flow.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: 1900a8c6a3f3119c8b9049b12f5660cc9fd181a2
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 2%

---

# Connetti [!DNL Google BigQuery] ad Experience Platform utilizzando l&#39;API [!DNL Flow Service]

>[!IMPORTANT]
>
>L&#39;origine [!DNL Google BigQuery] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-Time Customer Data Platform Ultimate.

Leggere questa guida per scoprire come collegare il database [!DNL Google BigQuery] a Adobe Experience Platform utilizzando [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

### Raccogli le credenziali richieste

Per i passaggi dettagliati sul recupero delle credenziali di [!DNL Google BigQuery], leggere la [[!DNL Google BigQuery] guida all&#39;autenticazione](../../../../connectors/databases/bigquery.md#prerequisites).

## Connetti [!DNL Google BigQuery] ad Experience Platform su Azure {#azure}

Per informazioni su come collegare l&#39;origine [!DNL Google BigQuery] ad Experience Platform su Azure, leggere la procedura seguente.

### Crea una connessione di base per [!DNL Google BigQuery] in Experience Platform su Azure {#azure-base}

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID connessione di base, eseguire una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Google BigQuery] come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Usa autenticazione di base]

+++Richiesta

La richiesta seguente crea una connessione di base per [!DNL Google BigQuery] utilizzando l&#39;autenticazione di base.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection with basic authentication",
        "description": "Google BigQuery connection with basic authentication",
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
| `auth.params.project` | ID del progetto predefinito [!DNL Google BigQuery] da interrogare. contro. |
| `auth.params.clientId` | Valore ID utilizzato per generare il token di aggiornamento. |
| `auth.params.clientSecret` | Valore client utilizzato per generare il token di aggiornamento. |
| `auth.params.refreshToken` | Il token di aggiornamento ottenuto da [!DNL Google] utilizzato per autorizzare l&#39;accesso a [!DNL Google BigQuery]. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Google BigQuery]: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

>[!TAB Usa autenticazione servizio]


+++Richiesta

La richiesta seguente crea una connessione di base per [!DNL Google BigQuery] utilizzando l&#39;autenticazione del servizio:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google BigQuery base connection with service account",
      "description": "Google BigQuery connection with service account",
      "auth": {
          "specName": "Service Authentication",
          "params": {
                  "projectId": "{PROJECT_ID}",
                  "keyFileContent": "{KEY_FILE_CONTENT},
                  "largeResultsDataSetId": "{LARGE_RESULTS_DATASET_ID}"
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
| `auth.params.projectId` | ID del progetto predefinito [!DNL Google BigQuery] da interrogare. contro. |
| `auth.params.keyFileContent` | File di chiave utilizzato per autenticare l&#39;account del servizio. È necessario codificare il contenuto del file chiave in [!DNL Base64]. |
| `auth.params.largeResultsDataSetId` | (Facoltativo) L&#39;ID del set di dati [!DNL Google BigQuery] precreato necessario per abilitare il supporto per set di risultati di grandi dimensioni. |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

>[!ENDTABS]

## Connetti [!DNL Google BigQuery] ad Experience Platform su Amazon Web Services (AWS) {#aws}

Per informazioni su come collegare il database [!DNL Google BigQuery] ad Experience Platform su AWS, leggere la procedura seguente.

### Crea una connessione di base per [!DNL Google BigQuery] su Experience Platform su AWS

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../../../landing/multi-cloud.md).

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per connettere [!DNL Google BigQuery] ad Experience Platform su AWS.

+++Seleziona per visualizzare l’esempio

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google BigQuery base connection on AWS",
      "description": "Google BigQuery base connection on AWS",
      "auth": {
          "specName": "Service Authentication",
          "params": {
                  "projectId": "{PROJECT_ID}",
                  "keyFileContent": "{KEY_FILE_CONTENT},
                  "datasetId": "{DATASET_ID}"
      },
      "connectionSpec": {
          "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `auth.params.projectId` | ID del progetto predefinito [!DNL Google BigQuery] da interrogare. contro. |
| `auth.params.keyFileContent` | File di chiave utilizzato per autenticare l&#39;account del servizio. È necessario codificare il contenuto del file chiave in [!DNL Base64]. |
| `auth.params.datasetId` | ID del set di dati corrispondente all&#39;origine [!DNL Google BigQuery]. Questo ID rappresenta dove si trovano le tabelle di dati. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare lo spazio di archiviazione nella prossima esercitazione.

+++Seleziona per visualizzare l’esempio

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL Google BigQuery] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati del database in Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/database-nosql.md)
