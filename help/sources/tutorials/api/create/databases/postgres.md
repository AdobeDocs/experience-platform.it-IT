---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore PostgreSQL utilizzando l'API del servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 2%

---


# Creare un [!DNL PostgreSQL] connettore utilizzando l&#39; [!DNL Flow Service] API

>[!NOTE]
>Il [!DNL PostgreSQL] connettore è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti diverse all&#39;interno  Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39; [!DNL Flow Service] API per guidarvi attraverso i passaggi necessari per la connessione [!DNL Experience Platform] a [!DNL PostgreSQL] (di seguito &quot;PSQL&quot;).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti del  Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a PSQL tramite l&#39; [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] connettersi a PSQL, è necessario fornire la seguente proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Stringa di connessione associata all&#39;account PSQL. Il pattern della stringa di connessione PSQL è: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | ID utilizzato per generare una connessione. L&#39;ID della specifica di connessione fissa per PSQL è `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

Per ulteriori informazioni su come ottenere una stringa di connessione, consultare [questo documento](https://www.postgresql.org/docs/9.2/app-psql.html)PSQL.

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

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. Per l&#39;account PSQL è necessaria una sola connessione, in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```http
POST /connections
```

**Richiesta**

Per creare una connessione PSQL, è necessario fornire l&#39;ID univoco della specifica di connessione come parte della richiesta POST. L&#39;ID della specifica di connessione per PSQL è `74a1c565-4e59-48d7-9d67-7c03b8a13137`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test connection for PostgreSQL",
        "description": "Test connection for PostgreSQL",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| ------------- | --------------- |
| `auth.params.connectionString` | Stringa di connessione associata all&#39;account PSQL. Il pattern della stringa di connessione PSQL è: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | L&#39;ID della specifica di connessione per PSQL è: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della connessione di base appena creata. Questo ID è necessario per esplorare il database PSQL nell&#39;esercitazione successiva.

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, avete creato una connessione PSQL utilizzando l&#39; [!DNL Flow Service] API e ottenuto il valore ID univoco della connessione. L&#39;ID connessione può essere utilizzato nell&#39;esercitazione successiva quando si apprende come [esplorare i database o i sistemi NoSQL utilizzando l&#39;API](../../explore/database-nosql.md)del servizio di flusso.
