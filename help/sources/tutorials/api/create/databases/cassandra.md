---
keywords: Experience Platform;home;argomenti popolari;Apache Cassandra;apache cassandra;Cassandra;cassandra
solution: Experience Platform
title: Creare una connessione Apache Cassandra Source utilizzando l’API del servizio Flow
type: Tutorial
description: Scopri come collegare Apache Cassandra a Adobe Experience Platform utilizzando l’API del servizio Flow.
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 11%

---


# Creare una connessione di origine [!DNL Apache Cassandra] utilizzando l&#39;API [!DNL Flow Service]

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da diverse origini all&#39;interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui tutte le sorgenti supportate sono collegabili.

Questo tutorial utilizza l&#39;API [!DNL Flow Service] per illustrare i passaggi necessari per connettere [!DNL Apache Cassandra] (di seguito &quot;Cassandra&quot;) a [!DNL Experience Platform].

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a Cassandra utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Cassandra], è necessario fornire i valori per le proprietà di connessione seguenti:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Indirizzo IP o nome host del server [!DNL Cassandra]. |
| `port` | Porta TCP utilizzata dal server [!DNL Cassandra] per l&#39;ascolto delle connessioni client. La porta predefinita è `9042`. |
| `username` | Nome utente utilizzato per connettersi al server [!DNL Cassandra] per l&#39;autenticazione. |
| `password` | Password per la connessione al server [!DNL Cassandra] per l&#39;autenticazione. |
| `connectionSpec.id` | L’identificatore univoco necessario per creare una connessione. L&#39;ID della specifica di connessione per [!DNL Cassandra] è `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

Per ulteriori informazioni su come iniziare, fare riferimento a [questo documento Cassandra](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### Lettura delle chiamate API di esempio

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

* Autorizzazione: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* Tipo di contenuto: `application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessario un solo connettore per account [!DNL Cassandra], in quanto può essere utilizzato per creare più connettori di origine per l&#39;inserimento di dati diversi.

**Formato API**

```http
POST /connections
```

**Richiesta**

Per creare una connessione [!DNL Cassandra], è necessario fornire l&#39;ID univoco della specifica di connessione come parte della richiesta POST. L&#39;ID della specifica di connessione per [!DNL Cassandra] è `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.host` | Indirizzo IP o nome host del server [!DNL Cassandra]. |
| `auth.params.port` | Porta TCP utilizzata dal server [!DNL Cassandra] per l&#39;ascolto delle connessioni client. La porta predefinita è `9042`. |
| `auth.params.username` | Nome utente utilizzato per connettersi al server [!DNL Cassandra] per l&#39;autenticazione. |
| `auth.params.password` | Password per la connessione al server [!DNL Cassandra] per l&#39;autenticazione. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Cassandra]: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL Cassandra] utilizzando l&#39;API [!DNL Flow Service] e hai ottenuto il valore ID univoco della connessione. È possibile utilizzare questo ID nell&#39;esercitazione successiva mentre si apprende come [esplorare i database utilizzando l&#39;API del servizio Flusso](../../explore/database-nosql.md).
