---
keywords: Experience Platform;home;argomenti popolari;database di terze parti;servizio flusso database
solution: Experience Platform
title: Esplorare un database utilizzando l’API del servizio Flusso
description: Questa esercitazione utilizza l’API del servizio Flusso per esplorare il contenuto e la struttura di file di un database di terze parti.
exl-id: 94935492-a7be-48dc-8089-18476590bf98
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 10%

---

# Esplorare un database utilizzando l&#39;API [!DNL Flow Service]

Questa esercitazione utilizza l&#39;API [!DNL Flow Service] per esplorare il contenuto e la struttura di file di un database di terze parti.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a un database di terze parti tramite l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Questo tutorial richiede una connessione valida con il database di terze parti da cui desideri acquisire i dati. Una connessione valida include l&#39;ID di specifica di connessione e l&#39;ID di connessione del database. Ulteriori informazioni sulla creazione di una connessione al database e sul recupero di questi valori sono disponibili nella [panoramica dei connettori di origine](./../../../home.md#database).

### Lettura delle chiamate API di esempio

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API E[!DNL xperience Platform], come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* `Content-Type: application/json`

## Esplora le tabelle di dati

Utilizzando l’ID di connessione per il database, puoi esplorare le tabelle di dati eseguendo richieste GET. Utilizzare la seguente chiamata per trovare il percorso della tabella da controllare o acquisire in [!DNL Platform].

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID di connessione dell&#39;origine del database. |

**Richiesta**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/6990abad-977d-41b9-a85d-17ea8cf1c0e4/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce una matrice di tabelle dal database. Individuare la tabella che si desidera inserire in [!DNL Platform] e prendere nota della relativa proprietà `path`, in quanto è necessario fornirla nel passaggio successivo per esaminarne la struttura.

```json
[
    {
        "type": "table",
        "name": "test1.Mytable",
        "path": "test1.Mytable",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "test1.austin_demo",
        "path": "test1.austin_demo",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect: struttura di una tabella

Per controllare la struttura di una tabella dal database, eseguire una richiesta di GET specificando il percorso di una tabella come parametro di query.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID di una connessione al database. |
| `{TABLE_PATH}` | Percorso di una tabella. |

**Richiesta**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/6990abad-977d-41b9-a85d-17ea8cf1c0e4/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce la struttura della tabella specificata. I dettagli relativi a ciascuna colonna della tabella si trovano all&#39;interno di elementi dell&#39;array `columns`.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "TestID",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Name",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    }
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai esplorato il database, trovato il percorso della tabella da acquisire in [!DNL Platform] e ottenuto informazioni relative alla sua struttura. Puoi utilizzare queste informazioni nel prossimo tutorial per [raccogliere dati dal database e inserirli in Platform](../collect/database-nosql.md).
