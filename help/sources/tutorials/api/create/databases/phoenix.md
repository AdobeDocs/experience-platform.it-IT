---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore Phoenix tramite l'API di servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 1%

---


# Creare un [!DNL Phoenix] connettore utilizzando l&#39; [!DNL Flow Service] API

>[!NOTE]
>Il [!DNL Phoenix] connettore è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti diverse all&#39;interno  Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39; [!DNL Flow Service] API per illustrare i passaggi necessari per connettere un [!DNL Phoenix] database a [!DNL Experience Platform].

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti del  Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrete conoscere per collegarvi correttamente [!DNL Phoenix] utilizzando l&#39; [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] connettersi con [!DNL Phoenix], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Indirizzo IP o nome host del [!DNL Phoenix] server. |
| `username` | Nome utente utilizzato per accedere al [!DNL Phoenix] server. |
| `password` | La password corrispondente all&#39;utente. |
| `port` | La porta TCP utilizzata dal [!DNL Phoenix] server per ascoltare le connessioni client. Se vi collegate a [!DNL Azure] HDInsights, specificate la porta 443. |
| `httpPath` | URL parziale corrispondente al [!DNL Phoenix] server. Specificate /hbasephoenix0 se utilizzate il cluster [!DNL Azure] HDInsights. |
| `enableSsl` | Un valore booleano. Specifica se le connessioni al server sono crittografate utilizzando SSL. |
| `connectionSpec.id` | Identificatore univoco necessario per creare una connessione. L&#39;ID della specifica di connessione per [!DNL Phoenix] è: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Per ulteriori informazioni su come iniziare, consulta [questo documento](https://python-phoenixdb.readthedocs.io/en/latest/api.html)Phoenix.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../../../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti al gruppo [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* Content-Type: `application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione per [!DNL Phoenix] account, in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```http
POST /connections
```

**Richiesta**

Per creare una [!DNL Phoenix] connessione, è necessario fornire l&#39;ID univoco della specifica di connessione come parte della richiesta POST. L&#39;ID della specifica di connessione per [!DNL Phoenix] è `102706fb-a5cd-42ee-afe0-bc42f017ff43`.

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
| `auth.params.host` | Host del [!DNL Phoenix] server. |
| `auth.params.username` | Nome utente associato alla [!DNL Phoenix] connessione. |
| `auth.params.password` | La password associata alla [!DNL Phoenix] connessione. |
| `auth.params.port` | La porta TCP per la [!DNL Phoenix] connessione. |
| `auth.params.httpPath` | Percorso http parziale per la [!DNL Phoenix] connessione. |
| `auth.params.enableSsl` | Valore booleano che specifica se le connessioni al server sono crittografate utilizzando SSL. |
| `connectionSpec.id` | ID specifica [!DNL Phoenix] connessione: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell&#39;esercitazione successiva.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una [!DNL Phoenix] connessione utilizzando l&#39; [!DNL Flow Service] API e hai ottenuto il valore ID univoco della connessione. Puoi usare questo ID nell’esercitazione successiva per imparare a [esplorare i database utilizzando l’API](../../explore/database-nosql.md)del servizio di flusso.