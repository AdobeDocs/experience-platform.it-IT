---
title: Creare una connessione di base Phoenix utilizzando l’API del servizio Flow
description: Scopri come collegare un database Phoenix a Adobe Experience Platform utilizzando l’API del servizio Flow.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: efffd6ce1ed541ce20ee6500e42165465f2fa6a0
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 2%

---

# Creare un [!DNL Phoenix] connessione di base tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial descrive come creare una connessione di base e collegare [!DNL Phoenix] account a Adobe Experience Platform utilizzando [!DNL Flow Service] API.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Sorgenti](../../../../home.md): Experienci Platform consente di acquisire dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experienci Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experienci Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Experienci Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Phoenix] utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per connettersi è necessario fornire le seguenti credenziali di autenticazione [!DNL Phoenix] da Experience Platform.

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Indirizzo IP o nome host del [!DNL Phoenix] server. |
| `username` | Nome utente utilizzato per accedere a [!DNL Phoenix] Server. |
| `password` | La password corrispondente all’utente. |
| `port` | La porta TCP che [!DNL Phoenix] il server utilizza per l&#39;ascolto delle connessioni client. Se ci si connette a [!DNL Azure HDInsights], quindi specificare la porta come 443. Se questo parametro non viene specificato, il valore predefinito è 8765. |
| `httpPath` | L’URL parziale corrispondente al [!DNL Phoenix] server. Specifica /hbasephoenix0 se si utilizza [!DNL Azure] Cluster HDInsight. |
| `enableSsl` | Valore booleano. Specifica se le connessioni al server sono crittografate tramite SSL. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Phoenix] è: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Per ulteriori informazioni su come iniziare, consulta [questo documento Phoenix](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare una connessione di base, effettuare una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL Phoenix] credenziali di autenticazione nel corpo della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Phoenix]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Phoenix test connection",
      "description": "Phoenix test connection",
      "auth": {
          "specName": "Basic Authentication",
      "params": {
          "host":  "{HOST}",
          "username": "{USERNAME}",
          "password":"{PASSWORD}",
          "port": {PORT},
          "httpPath": "{PATH}",
          "enableSsl": {SSL}
          }
      },
      "connectionSpec": {
          "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `auth.params.host` | L’host del [!DNL Phoenix] server. |
| `auth.params.username` | Il nome utente associato al tuo [!DNL Phoenix] connessione. |
| `auth.params.password` | La password associata al tuo [!DNL Phoenix] connessione. |
| `auth.params.port` | La porta TCP per [!DNL Phoenix] connessione. |
| `auth.params.httpPath` | Percorso http parziale per [!DNL Phoenix] connessione. |
| `auth.params.enableSsl` | Il valore booleano che specifica se le connessioni al server sono crittografate utilizzando SSL. |
| `connectionSpec.id` | Il [!DNL Phoenix] ID specifica di connessione: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una [!DNL Phoenix] connessione di base tramite [!DNL Flow Service] API. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati del database su Platform utilizzando [!DNL Flow Service] API](../../collect/database-nosql.md)
