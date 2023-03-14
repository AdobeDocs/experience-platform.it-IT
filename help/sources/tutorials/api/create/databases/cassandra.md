---
keywords: Experience Platform;home;argomenti popolari;Apache Cassandra;apache cassandra;Cassandra;cassandra
solution: Experience Platform
title: Creare una connessione sorgente Apache Cassandra utilizzando l’API del servizio Flusso
type: Tutorial
description: Scopri come collegare Apache Cassandra a Adobe Experience Platform utilizzando l’API del servizio Flow.
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 2%

---


# Creare un [!DNL Apache Cassandra] connessione sorgente tramite [!DNL Flow Service] API

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da diverse origini all’interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui tutte le sorgenti supportate sono collegabili.

Questa esercitazione utilizza [!DNL Flow Service] API per illustrare i passaggi per la connessione [!DNL Apache Cassandra] (in seguito denominata &quot;Cassandra&quot;) [!DNL Experience Platform].

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a Cassandra utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi con [!DNL Cassandra], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Indirizzo IP o nome host del [!DNL Cassandra] server. |
| `port` | La porta TCP che [!DNL Cassandra] il server utilizza per l&#39;ascolto delle connessioni client. La porta predefinita è `9042`. |
| `username` | Il nome utente utilizzato per connettersi al [!DNL Cassandra] server per l&#39;autenticazione. |
| `password` | Password per la connessione al [!DNL Cassandra] server per l&#39;autenticazione. |
| `connectionSpec.id` | L’identificatore univoco necessario per creare una connessione. ID della specifica di connessione per [!DNL Cassandra] è `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

Per ulteriori informazioni su come iniziare, consulta [questo documento Cassandra](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### Lettura delle chiamate API di esempio

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nel [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori per le intestazioni richieste

Per effettuare chiamate a [!DNL Platform] , devi prima completare le [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* Autorizzazione: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], compresi quelli appartenenti al [!DNL Flow Service], sono isolate in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* Content-Type: `application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È richiesto un solo connettore per ogni [!DNL Cassandra] in quanto può essere utilizzato per creare più connettori di origine per l’inserimento di dati diversi.

**Formato API**

```http
POST /connections
```

**Richiesta**

Per creare un [!DNL Cassandra] connessione, l’ID univoco della specifica di connessione deve essere fornito come parte della richiesta POST. ID della specifica di connessione per [!DNL Cassandra] è `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

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
| `auth.params.host` | Indirizzo IP o nome host del [!DNL Cassandra] server. |
| `auth.params.port` | La porta TCP che [!DNL Cassandra] il server utilizza per l&#39;ascolto delle connessioni client. La porta predefinita è `9042`. |
| `auth.params.username` | Il nome utente utilizzato per connettersi al [!DNL Cassandra] server per l&#39;autenticazione. |
| `auth.params.password` | Password per la connessione al [!DNL Cassandra] server per l&#39;autenticazione. |
| `connectionSpec.id` | Il [!DNL Cassandra] ID specifica di connessione: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una [!DNL Cassandra] connessione tramite [!DNL Flow Service] e hanno ottenuto il valore ID univoco della connessione. Puoi utilizzare questo ID nel prossimo tutorial mentre apprendi come [esplorare i database utilizzando l’API del servizio Flow](../../explore/database-nosql.md).
