---
keywords: Experience Platform;home;argomenti popolari;Apache hive;hive;Hive
solution: Experience Platform
title: Creare un hive Apache sulla connessione di base Azure HDInsights utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Apache Hive su Azure HDInsights a Adobe Experience Platform utilizzando l’API del servizio di flusso.
exl-id: e1469a29-6f61-47ba-995e-39f06ee4a4a4
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 2%

---

# Crea un [!DNL Apache Hive] su [!DNL Azure HDInsights] connessione di base utilizzando [!DNL Flow Service] API

>[!NOTE]
>
>La [!DNL Apache Hive] su [!DNL Azure HDInsights] connettore in versione beta. Consulta la sezione [Panoramica delle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo dei connettori con etichetta beta.

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Apache Hive] su [!DNL Azure HDInsights] (in appresso denominato &quot;[!DNL Hive]&quot;) utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL Hive] utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi con [!DNL Hive], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Indirizzo IP o nome host del [!DNL Hive] server. |
| `username` | Nome utente utilizzato per accedere [!DNL Hive] server. |
| `password` | La password corrispondente all&#39;utente. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Hive] è: `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |

Per ulteriori informazioni su come iniziare, consulta [documento Hive](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL Hive] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Hive]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Apache Hive test connection",
        "description": "A test connection for Apache Hive",
        "auth": {
            "specName": "HDInsights Basic Authentication",
            "params": {
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
            "version": "1.0"
        }
    }'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `auth.params.connectionString` | La stringa di connessione associata alla [!DNL Hive] conto. |
| `connectionSpec.id` | La [!DNL Hive] ID specifica di connessione: `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "9f6e4311-e032-4c00-ae43-11e032bc00c7",
    "etag": "\"f4004fb7-0000-0200-0000-5e865c1e0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL Apache Hive] su [!DNL Azure HDInsights] connessione di base utilizzando [!DNL Flow Service] API. Puoi usare questo ID di connessione di base nelle seguenti esercitazioni:

* [Esplorare la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Creare un flusso di dati per trasferire i dati di database a Platform utilizzando [!DNL Flow Service] API](../../collect/database-nosql.md)
