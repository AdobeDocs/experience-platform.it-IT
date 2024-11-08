---
title: Creare una connessione di base Phoenix utilizzando l’API del servizio Flow
description: Scopri come collegare un database Phoenix a Adobe Experience Platform utilizzando l’API del servizio Flow.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# Creare una connessione di base [!DNL Phoenix] utilizzando l&#39;API [!DNL Flow Service]

>[!WARNING]
>
>L&#39;origine [!DNL Phoenix] diventerà obsoleta alla fine di maggio 2025.

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base e connettere l&#39;account [!DNL Phoenix] a Adobe Experience Platform utilizzando l&#39;API [!DNL Flow Service].

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Phoenix] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Per connettere l&#39;account [!DNL Phoenix] a Experience Platform, è necessario fornire le credenziali di autenticazione seguenti.

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Indirizzo IP o nome host del server [!DNL Phoenix]. |
| `username` | Nome utente utilizzato per accedere al server [!DNL Phoenix]. |
| `password` | La password corrispondente all’utente. |
| `port` | Porta TCP utilizzata dal server [!DNL Phoenix] per l&#39;ascolto delle connessioni client. Se ci si connette a [!DNL Azure HDInsights], specificare la porta come 443. Se questo parametro non viene specificato, il valore predefinito è 8765. |
| `httpPath` | URL parziale corrispondente al server [!DNL Phoenix]. Specificare /hbasephoenix0 se si utilizza il cluster HDInsights [!DNL Azure]. |
| `enableSsl` | Valore booleano. Specifica se le connessioni al server sono crittografate tramite SSL. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Phoenix]: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Per ulteriori informazioni su come iniziare, fare riferimento a [questo documento Phoenix](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare una connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Phoenix] nel corpo della richiesta.

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
| `auth.params.host` | Host del server [!DNL Phoenix]. |
| `auth.params.username` | Il nome utente associato alla connessione [!DNL Phoenix]. |
| `auth.params.password` | La password associata alla connessione [!DNL Phoenix]. |
| `auth.params.port` | Porta TCP per la connessione [!DNL Phoenix]. |
| `auth.params.httpPath` | Percorso HTTP parziale per la connessione [!DNL Phoenix]. |
| `auth.params.enableSsl` | Il valore booleano che specifica se le connessioni al server sono crittografate utilizzando SSL. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Phoenix]: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL Phoenix] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati del database in Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/database-nosql.md)
