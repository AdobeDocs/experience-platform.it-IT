---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore Couchbase utilizzando l'API del servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 2%

---


# Creare un [!DNL Couchbase] connettore utilizzando l&#39; [!DNL Flow Service] API

>[!NOTE]
>Il [!DNL Couchbase] connettore è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti diverse per  Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l’API del servizio di flusso per guidarvi nei passaggi [!DNL Couchbase] a cui connettervi [!DNL Experience Platform].

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti del  Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrete conoscere per collegarvi correttamente [!DNL Couchbase] utilizzando l&#39; [!DNL Flow Service] API.

### Raccogli credenziali richieste

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Stringa di connessione utilizzata per connettersi all&#39; [!DNL Couchbase] istanza. Il pattern della stringa di connessione per [!DNL Couchbase] è `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Per ulteriori informazioni sull&#39;acquisizione di una stringa di connessione, vedere [questo documento](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview)Couchbase. |
| `connectionSpec.id` | Identificatore necessario per creare una connessione. L&#39;ID della specifica di connessione fissa per [!DNL Couchbase] è `1fe283f6-9bec-11ea-bb37-0242ac130002`. |

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../../../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* Content-Type: `application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessario un solo connettore per [!DNL Couchbase] account, in quanto può essere utilizzato per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```http
POST /connections
```

**Richiesta**

La richiesta seguente crea una nuova [!DNL Couchbase] connessione, configurata dalle proprietà fornite nel payload:.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Couchbase test connection",
        "description": "A test connection for a Couchbase source",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                    "connectionString": "Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];"
                }
        },
        "connectionSpec": {
            "id": "1fe283f6-9bec-11ea-bb37-0242ac130002",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `auth.params.connectionString` | Stringa di connessione utilizzata per connettersi a un [!DNL Couchbase] account. Il pattern della stringa di connessione è: `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. |
| `connectionSpec.id` | ID specifica [!DNL Couchbase] di connessione: `1fe283f6-9bec-11ea-bb37-0242ac130002`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell&#39;esercitazione successiva.

```json
{
    "id": "54997109-07b5-40b7-9971-0907b5a0b75a",
    "etag": "\"280168f5-0000-0200-0000-5ed72b230000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una [!DNL Couchbase] connessione utilizzando l&#39; [!DNL Flow Service] API e hai ottenuto il valore ID univoco della connessione. Puoi usare questo ID nell’esercitazione successiva per imparare a [esplorare i database utilizzando l’API](../../explore/database-nosql.md)del servizio di flusso.
