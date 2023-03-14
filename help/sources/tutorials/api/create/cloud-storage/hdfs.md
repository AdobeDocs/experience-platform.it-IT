---
keywords: Experience Platform;home;argomenti comuni;Apache Hadoop Distributed File System;Apache hadoop;hdfs;HDFS
solution: Experience Platform
title: Creare una connessione di base Apache HDFS utilizzando l’API del servizio Flow
type: Tutorial
description: Scopri come collegare un file system distribuito di Hadoop Apache a Adobe Experience Platform utilizzando l’API del servizio Flow.
exl-id: 04fa65db-073c-48e1-b981-425185ae08aa
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 2%

---

# Creare un [!DNL Apache] Connessione di base HDFS tramite [!DNL Flow Service] API

>[!NOTE]
>
>Il connettore Apache HDFS è in versione beta. Consulta la [Panoramica sulle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di connettori con etichetta beta.

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Apache Hadoop Distributed File System] (in seguito denominati &quot;[!DNL HDFS]&quot;) utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL HDFS] utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

| Credenziali | Descrizione |
| ---------- | ----------- |
| `url` | L’URL definisce i parametri di autenticazione necessari per la connessione a [!DNL HDFS] anonimamente. Per ulteriori informazioni su come ottenere questo valore, consulta [questo [!DNL HDFS] documento](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL AdWords] è: `54e221aa-d342-4707-bcff-7a4bceef0001`. |

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL HDFS] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL HDFS]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "HDFS test connection",
        "description": "A test connection for an HDFS source",
        "auth": {
            "specName": "Anonymous Authentication",
            "params": {
                "url": "{URL}"
                }
        },
        "connectionSpec": {
            "id": "54e221aa-d342-4707-bcff-7a4bceef0001",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `auth.params.url` | URL che definisce i parametri di autenticazione necessari per la connessione a [!DNL HDFS] anonimamente |
| `connectionSpec.id` | Il [!DNL HDFS] ID specifica di connessione: `54e221aa-d342-4707-bcff-7a4bceef0001`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "6a6a880a-2b15-4051-aa88-0a2b1570516d",
    "etag": "\"1801bb7d-0000-0200-0000-5ed6ad580000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un’ [!DNL HDFS] connessione tramite [!DNL Flow Service] e hanno ottenuto il valore ID univoco della connessione. Puoi utilizzare questo ID nel prossimo tutorial mentre apprendi come [esplorare un’archiviazione cloud di terze parti utilizzando l’API del servizio Flow](../../explore/cloud-storage.md).
