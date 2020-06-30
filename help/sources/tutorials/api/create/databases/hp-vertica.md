---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore HP Vertica utilizzando l'API del servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 2%

---


# Creare un connettore HP [!DNL Vertica] utilizzando l&#39; [!DNL Flow Service] API

>[!NOTE]
>Il [!DNL Vertica] connettore HP è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti diverse all&#39;interno  Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39; [!DNL Flow Service] API per guidarti nei passaggi necessari per connettere HP [!DNL Vertica] a [!DNL Experience Platform].

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti del  Adobe Experience Platform:

- [Origini](https://docs.adobe.com/content/help/en/experience-platform/source-connectors/home.html): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie fonti, fornendo al contempo la possibilità di strutturare, mappare e migliorare i dati in arrivo tramite [!DNL Platform] i servizi.
- [Sandbox](https://docs.adobe.com/content/help/en/experience-platform/sandbox/home.html): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi con successo ad HP [!DNL Vertica] tramite l&#39; [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] connettersi con HP [!DNL Vertica], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Stringa di connessione utilizzata per connettersi all&#39; [!DNL Vertica] istanza HP. Il pattern della stringa di connessione per HP [!DNL Vertica] è `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |
| `connectionSpec.id` | Identificatore necessario per creare una connessione. L&#39;ID della specifica di connessione fissa per HP [!DNL Vertica] è: `a8b6a1a4-5735-42b4-952c-85dce0ac38b5` |

Per ulteriori informazioni sull&#39;acquisizione di una stringa di connessione, consultare [questo documento](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm)HP Vertica.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](https://docs.adobe.com/content/help/en/experience-platform/landing/troubleshooting.html#reading-example-api-calls) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], inclusi i connettori di origine, sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

- Content-Type: `application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione per [!DNL Vertica] account HP, in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```http
POST /connections
```

**Richiesta**

Per creare una connessione HP [!DNL Vertica] , è necessario fornire l&#39;ID univoco della specifica di connessione come parte della richiesta POST. L&#39;ID della specifica di connessione per HP [!DNL Vertica] è `a8b6a1a4-5735-42b4-952c-85dce0ac38b5`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for HP Vertica",
        "description": "Connection for HP Vertica",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
            "version": "1.0"
        }
    }'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `auth.params.connectionString` | Stringa di connessione associata al tuo [!DNL Vertica] account HP. Il pattern della stringa di connessione per HP [!DNL Vertica] è: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | ID della specifica [!DNL Vertica] di connessione HP: `a8b6a1a4-5735-42b4-952c-85dce0ac38b5`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell&#39;esercitazione successiva.

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione HP [!DNL Vertica] utilizzando l&#39; [!DNL Flow Service] API e hai ottenuto il valore ID univoco della connessione. Puoi usare questo ID nell’esercitazione successiva per imparare a [esplorare i database utilizzando l’API](../../explore/database-nosql.md)del servizio di flusso.
