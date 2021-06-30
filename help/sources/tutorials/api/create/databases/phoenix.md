---
keywords: Experience Platform;casa;argomenti popolari;Phoenix;fenice
solution: Experience Platform
title: Creare una connessione Phoenix Base utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare un database Phoenix a Adobe Experience Platform utilizzando l’API del servizio di flusso.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: 5fb5f0ce8bd03ba037c6901305ba17f8939eb9ce
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 1%

---

# Creare una connessione di base [!DNL Phoenix] utilizzando l&#39;API [!DNL Flow Service]

>[!NOTE]
>
>Il connettore [!DNL Phoenix] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions) .

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti all&#39;interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui è possibile connettere tutte le sorgenti supportate.

Questa esercitazione utilizza l’ API [!DNL Flow Service] per seguire i passaggi necessari per collegare un database [!DNL Phoenix] a [!DNL Experience Platform].

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md):  [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL Phoenix] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Phoenix], è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | L&#39;indirizzo IP o il nome host del server [!DNL Phoenix]. |
| `username` | Nome utente utilizzato per accedere al server [!DNL Phoenix]. |
| `password` | La password corrispondente all&#39;utente. |
| `port` | La porta TCP utilizzata dal server [!DNL Phoenix] per ascoltare le connessioni client. Se ti connetti a [!DNL Azure] HDInsights, specifica la porta come 443. |
| `httpPath` | L&#39;URL parziale corrispondente al server [!DNL Phoenix] . Specificare /hbasephoenix0 se si utilizza il cluster [!DNL Azure] HDInsights. |
| `enableSsl` | Un valore booleano. Specifica se le connessioni al server sono crittografate utilizzando SSL. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per [!DNL Phoenix] è: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Per ulteriori informazioni su come iniziare, consulta [questo documento Phoenix](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md) .

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Phoenix] come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La seguente richiesta crea una connessione di base per [!DNL Phoenix]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Phoenix test connection",
        "description": "Phoenix test connection",
        "auth": {
            "specName": "Basic Authentication",
        "params": {
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}",
            "port" : {PORT},
            "httpPath" : "{PATH}",
            "enableSsl" : {SSL}
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
| `auth.params.username` | Nome utente associato alla connessione [!DNL Phoenix]. |
| `auth.params.password` | Password associata alla connessione [!DNL Phoenix]. |
| `auth.params.port` | La porta TCP per la connessione [!DNL Phoenix]. |
| `auth.params.httpPath` | Il percorso http parziale per la connessione [!DNL Phoenix]. |
| `auth.params.enableSsl` | Valore booleano che specifica se le connessioni al server sono crittografate utilizzando SSL. |
| `connectionSpec.id` | ID delle specifiche di connessione [!DNL Phoenix]: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso l’identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL Phoenix] utilizzando l&#39;API [!DNL Flow Service] e hai ottenuto il valore ID univoco della connessione. Puoi utilizzare questo ID nell&#39;esercitazione successiva per scoprire come [esplorare i database utilizzando l&#39;API del servizio di flusso](../../explore/database-nosql.md).
