---
title: Collegare AWS Redshift Ad Experience Platform Utilizzando L’API Del Servizio Flow
description: Scopri come collegare Adobe Experience Platform ad AWS Redshift utilizzando l’API del servizio Flow.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: dd9aee1ac887637d4761188d6dbcf55ad5bde407
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 4%

---

# Connetti [!DNL AWS Redshift] ad Experience Platform utilizzando l&#39;API [!DNL Flow Service]

>[!IMPORTANT]
>
>L&#39;origine [!DNL AWS Redshift] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-Time Customer Data Platform Ultimate.

Leggi questa guida per scoprire come collegare l&#39;account di origine [!DNL AWS Redshift] a Adobe Experience Platform utilizzando [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Connetti [!DNL AWS Redshift] ad Experience Platform su Azure {#azure}

Per informazioni su come collegare l&#39;origine [!DNL AWS Redshift] ad Experience Platform su Azure, leggere la procedura seguente.

### Raccogli le credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL AWS Redshift], è necessario fornire le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| `server` | Il nome del server dell&#39;istanza [!DNL AWS Redshift]. |
| `port` | Porta TCP utilizzata da un server [!DNL AWS Redshift] per l&#39;ascolto delle connessioni client. |
| `username` | Il nome utente associato al tuo account [!DNL AWS Redshift]. |
| `password` | Password corrispondente all&#39;account utente. |
| `database` | Database [!DNL AWS Redshift] da cui recuperare i dati. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per [!DNL AWS Redshift] è `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

Per ulteriori informazioni su come iniziare, consulta questo [[!DNL AWS Redshift] documento](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html).

### Crea una connessione di base per [!DNL AWS Redshift] in Experience Platform su Azure [#azure-base]

>[!NOTE]
>
>Lo standard di codifica predefinito per [!DNL Redshift] è Unicode. Questo non può essere modificato.

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID connessione di base, eseguire una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL AWS Redshift] come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

+++Seleziona per visualizzare l’esempio

La richiesta seguente crea una connessione di base per [!DNL AWS Redshift]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "AWS-redshift base connection",
      "description": "base connection for AWS-redshift,
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT},
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `auth.params.server` | Il nome del server dell&#39;istanza [!DNL AWS Redshift]. |
| `auth.params.port` | Porta TCP utilizzata da un server [!DNL AWS Redshift] per l&#39;ascolto delle connessioni client. |
| `auth.params.username` | Il nome utente associato al tuo account [!DNL AWS Redshift]. |
| `auth.params.password` | Password corrispondente all&#39;account utente. |
| `auth.params.database` | Database [!DNL AWS Redshift] da cui recuperare i dati. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL AWS Redshift]: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

+++

**Risposta**

+++Seleziona per visualizzare l’esempio

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

+++

## Connetti [!DNL AWS Redshift] ad Experience Platform su AWS Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su AWS Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../../../landing/multi-cloud.md).

Per informazioni su come collegare l&#39;origine [!DNL AWS Redshift] ad Experience Platform su AWS, leggere i passaggi seguenti.

### Crea una connessione di base per [!DNL AWS Redshift] su Experience Platform su AWS {#aws-base}

**Formato API**

```http
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL AWS Redshift]:

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
      "name": "AWS Redshift base connection for Experience Platform on AWS",
      "description": "AWS Redshift base connection for Experience Platform on AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "5439",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}",
              "schema": "{SCHEMA}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `auth.params.server` | Il nome del server dell&#39;istanza [!DNL AWS Redshift]. |
| `auth.params.port` | Porta TCP utilizzata da un server [!DNL AWS Redshift] per l&#39;ascolto delle connessioni client. |
| `auth.params.username` | Il nome utente associato al tuo account [!DNL AWS Redshift]. |
| `auth.params.password` | Password corrispondente all&#39;account utente. |
| `auth.params.database` | Database [!DNL AWS Redshift] da cui recuperare i dati. |
| `auth.params.schema` | Il nome dello schema associato al database [!DNL AWS Redshift]. È necessario assicurarsi che anche l&#39;utente a cui si desidera concedere l&#39;accesso al database abbia accesso a questo schema. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL AWS Redshift]: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare lo spazio di archiviazione nella prossima esercitazione.

+++Seleziona per visualizzare l’esempio

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++


## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL AWS Redshift] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati del database in Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/database-nosql.md)
