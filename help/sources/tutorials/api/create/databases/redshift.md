---
title: Creare una connessione di base Amazon Redshift utilizzando l’API del servizio Flow
description: Scopri come collegare Adobe Experience Platform ad Amazon Redshift utilizzando l’API del servizio Flow.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 5%

---

# Creare una connessione di base [!DNL Amazon Redshift] utilizzando l&#39;API [!DNL Flow Service]

>[!IMPORTANT]
>
>L&#39;origine [!DNL Amazon Redshift] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Amazon Redshift] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Amazon Redshift] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Amazon Redshift], è necessario fornire le seguenti proprietà di connessione:

| **Credenziali** | **Descrizione** |
| -------------- | --------------- |
| `server` | Il server associato al tuo account [!DNL Amazon Redshift]. |
| `port` | Porta TCP utilizzata da un server [!DNL Amazon Redshift] per l&#39;ascolto delle connessioni client. |
| `username` | Il nome utente associato al tuo account [!DNL Amazon Redshift]. |
| `password` | La password associata al tuo account [!DNL Amazon Redshift]. |
| `database` | Database [!DNL Amazon Redshift] a cui si sta effettuando l&#39;accesso. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per [!DNL Amazon Redshift] è `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

Per ulteriori informazioni su come iniziare, consulta questo [[!DNL Amazon Redshift] documento](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

>[!NOTE]
>
>Lo standard di codifica predefinito per [!DNL Redshift] è Unicode. Questo non può essere modificato.

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Amazon Redshift] come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Amazon Redshift]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "amazon-redshift base connection",
      "description": "base connection for amazon-redshift,
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
| ------------- | --------------- |
| `auth.params.server` | Il server [!DNL Amazon Redshift]. |
| `auth.params.port` | Porta TCP utilizzata dal server [!DNL Amazon Redshift] per l&#39;ascolto delle connessioni client. |
| `auth.params.database` | Il database associato al tuo account [!DNL Amazon Redshift]. |
| `auth.params.password` | La password associata al tuo account [!DNL Amazon Redshift]. |
| `auth.params.username` | Il nome utente associato al tuo account [!DNL Amazon Redshift]. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Amazon Redshift]: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL Amazon Redshift] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati del database in Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/database-nosql.md)
