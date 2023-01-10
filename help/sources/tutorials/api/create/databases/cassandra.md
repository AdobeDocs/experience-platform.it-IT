---
keywords: Experience Platform;casa;argomenti popolari;Apache Cassandra;apache cassandra;Cassandra;Cassandra;Cassandra
solution: Experience Platform
title: Creare una connessione sorgente Apache Cassandra utilizzando l’API del servizio di flusso
type: Tutorial
description: Scopri come collegare Apache Cassandra a Adobe Experience Platform utilizzando l’API del servizio di flusso.
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 2%

---


# Crea un [!DNL Apache Cassandra] connessione di origine tramite [!DNL Flow Service] API

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti all&#39;interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui è possibile connettere tutte le sorgenti supportate.

Questa esercitazione utilizza la funzione [!DNL Flow Service] API per seguire i passaggi necessari per la connessione [!DNL Apache Cassandra] (in seguito denominata &quot;Cassandra&quot;) [!DNL Experience Platform].

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi con successo a Cassandra utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi con [!DNL Cassandra], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Indirizzo IP o nome host del [!DNL Cassandra] server. |
| `port` | La porta TCP che [!DNL Cassandra] il server utilizza per ascoltare le connessioni client. La porta predefinita è `9042`. |
| `username` | Il nome utente utilizzato per connettersi al [!DNL Cassandra] server per l&#39;autenticazione. |
| `password` | Password per la connessione al [!DNL Cassandra] server per l&#39;autenticazione. |
| `connectionSpec.id` | Identificatore univoco necessario per creare una connessione. ID della specifica di connessione per [!DNL Cassandra] è `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

Per ulteriori informazioni su come iniziare, consulta [documento Cassandra](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], compresi quelli appartenenti al [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* Content-Type: `application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessario un solo connettore per [!DNL Cassandra] può essere utilizzato per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```http
POST /connections
```

**Richiesta**

Per creare un [!DNL Cassandra] connection, il suo ID univoco della specifica di connessione deve essere fornito come parte della richiesta POST. ID della specifica di connessione per [!DNL Cassandra] è `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

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
| `auth.params.port` | La porta TCP che [!DNL Cassandra] il server utilizza per ascoltare le connessioni client. La porta predefinita è `9042`. |
| `auth.params.username` | Il nome utente utilizzato per connettersi al [!DNL Cassandra] server per l&#39;autenticazione. |
| `auth.params.password` | Password per la connessione al [!DNL Cassandra] server per l&#39;autenticazione. |
| `connectionSpec.id` | La [!DNL Cassandra] ID delle specifiche di connessione: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL Cassandra] connessione tramite [!DNL Flow Service] e hanno ottenuto il valore ID univoco della connessione. Puoi usare questo ID nell&#39;esercitazione successiva per scoprire come [esplorare i database utilizzando l’API del servizio di flusso](../../explore/database-nosql.md).
