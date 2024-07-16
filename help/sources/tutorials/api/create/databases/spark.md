---
keywords: Experience Platform;home;argomenti popolari;Apache Spark;apache spark;Azure HDInsights
solution: Experience Platform
title: Creare uno Spark Apache sulla connessione di base Azure HDInsights utilizzando l’API del servizio di flusso
type: Tutorial
description: Scopri come collegare Apache Spark su Azure HDInsights a Adobe Experience Platform utilizzando l’API del servizio Flusso.
exl-id: 1f7ca86e-32f4-45f7-92c2-f87c5c0c4ea4
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 5%

---

# Crea una connessione di base [!DNL Apache Spark] su [!DNL Azure] HDInsights utilizzando l&#39;API [!DNL Flow Service]

>[!NOTE]
>
>[!DNL Apache Spark] sul connettore [!DNL Azure HDInsights] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica origini](../../../../home.md#terms-and-conditions).

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Apache Spark] su [!DNL Azure HDInsights] (di seguito &quot;[!DNL Spark]&quot;) utilizzando l&#39;API [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Spark] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Spark], è necessario fornire i valori per le proprietà di connessione seguenti:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Indirizzo IP o nome host del server [!DNL Spark]. |
| `username` | Nome utente utilizzato per accedere al server [!DNL Spark]. |
| `password` | La password corrispondente all’utente. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Spark]: `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |

Per ulteriori informazioni su come iniziare, fare riferimento a [questo documento Spark](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Spark] come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Spark]:


```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Spark test connection",
        "description": "A Spark test connection",
        "auth": {
            "specName": "HDInsights Basic Authentication",
        "params": {
            "host":  "{HOST}",
            "username": "{USERNAME}",
            "password":"{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
            "version": "1.0"
        }
    }'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `auth.params.host` | Host del server [!DNL Spark]. |
| `auth.params.username` | Il nome utente associato alla connessione [!DNL Spark]. |
| `auth.params.password` | La password associata alla connessione [!DNL Spark]. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Spark]: `6a8d82bc-1caf-45d1-908d-cadabc9d63a6`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "a45f2f58-e3a2-46ba-9f2f-58e3a2b6baf2",
    "etag": "\"900009d6-0000-0200-0000-5e8500010000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL Spark] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati del database in Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/database-nosql.md)
