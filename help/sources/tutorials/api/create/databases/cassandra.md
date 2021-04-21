---
keywords: Experience Platform;casa;argomenti popolari;Apache Cassandra;apache cassandra;Cassandra;Cassandra;Cassandra
solution: Experience Platform
title: Creare una connessione sorgente Apache Cassandra utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Apache Cassandra a Adobe Experience Platform utilizzando l’API del servizio di flusso.
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 2%

---


# Creare una connessione sorgente [!DNL Apache Cassandra] utilizzando l&#39;API [!DNL Flow Service]

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti all&#39;interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui è possibile connettere tutte le sorgenti supportate.

Questa esercitazione utilizza l’ API [!DNL Flow Service] per guidarti nei passaggi per la connessione [!DNL Apache Cassandra] (in seguito denominata &quot;Cassandra&quot;) a [!DNL Experience Platform].

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md):  [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a Cassandra utilizzando l’ API [!DNL Flow Service] .

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Cassandra], è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | L&#39;indirizzo IP o il nome host del server [!DNL Cassandra]. |
| `port` | La porta TCP utilizzata dal server [!DNL Cassandra] per ascoltare le connessioni client. La porta predefinita è `9042`. |
| `username` | Nome utente utilizzato per connettersi al server [!DNL Cassandra] per l&#39;autenticazione. |
| `password` | Password per la connessione al server [!DNL Cassandra] per l&#39;autenticazione. |
| `connectionSpec.id` | Identificatore univoco necessario per creare una connessione. L&#39;ID della specifica di connessione per [!DNL Cassandra] è `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

Per ulteriori informazioni su come iniziare, consulta [questo documento Cassandra](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* nome x-sandbox: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* Content-Type: `application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessario un solo connettore per account [!DNL Cassandra] in quanto può essere utilizzato per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```http
POST /connections
```

**Richiesta**

Per creare una connessione [!DNL Cassandra], è necessario fornire l’ID univoco della specifica di connessione come parte della richiesta di POST. L&#39;ID della specifica di connessione per [!DNL Cassandra] è `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cassandra test connection",
        "description": "A test connection for Cassandra",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST},
                    "port": "{PORT}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
            "version": "1.0"
        }
    }'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `auth.params.host` | L&#39;indirizzo IP o il nome host del server [!DNL Cassandra]. |
| `auth.params.port` | La porta TCP utilizzata dal server [!DNL Cassandra] per ascoltare le connessioni client. La porta predefinita è `9042`. |
| `auth.params.username` | Nome utente utilizzato per connettersi al server [!DNL Cassandra] per l&#39;autenticazione. |
| `auth.params.password` | Password per la connessione al server [!DNL Cassandra] per l&#39;autenticazione. |
| `connectionSpec.id` | ID delle specifiche di connessione [!DNL Cassandra]: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso l’identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL Cassandra] utilizzando l&#39;API [!DNL Flow Service] e hai ottenuto il valore ID univoco della connessione. Puoi utilizzare questo ID nell&#39;esercitazione successiva per scoprire come [esplorare i database utilizzando l&#39;API del servizio di flusso](../../explore/database-nosql.md).
