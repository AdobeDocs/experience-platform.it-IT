---
keywords: Experience Platform;home;argomenti popolari;automazione marketing
solution: Experience Platform
title: Esplorare un sistema di automazione del marketing utilizzando l’API del servizio Flow
description: Questa esercitazione utilizza l’API Flow Service per esplorare i sistemi di automazione del marketing.
exl-id: 250c1ba0-1baa-444f-ab2b-58b3a025561e
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 3%

---

# Esplora un sistema di automazione del marketing utilizzando [!DNL Flow Service] API

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da diverse origini all’interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui tutte le sorgenti supportate sono collegabili.

Questa esercitazione utilizza [!DNL Flow Service] API per esplorare i sistemi di automazione del marketing.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a un sistema di automazione marketing utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Questo tutorial richiede una connessione valida con l’applicazione di automazione marketing di terze parti da cui desideri acquisire i dati. Una connessione valida include l&#39;ID di specifica di connessione e l&#39;ID di connessione dell&#39;applicazione. Ulteriori informazioni sulla creazione di una connessione di automazione marketing e sul recupero di questi valori sono disponibili nella sezione [collegare un’origine di automazione marketing a Platform](../../api/create/marketing-automation/hubspot.md) esercitazione.

### Lettura delle chiamate API di esempio

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nel [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori per le intestazioni richieste

Per effettuare chiamate a [!DNL Platform] , devi prima completare le [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* Autorizzazione: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], compresi quelli appartenenti a [!DNL Flow Service], sono isolate in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* Content-Type: `application/json`

## Esplora le tabelle di dati

Utilizzando la connessione di base per il sistema di automazione marketing, puoi esplorare le tabelle di dati eseguendo richieste GET. Utilizza la seguente chiamata per trovare il percorso della tabella da ispezionare o in cui desideri acquisire [!DNL Platform].

**Formato API**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID della connessione di base per il sistema di automazione marketing. |

**Richiesta**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/2fce94c1-9a93-4971-8e94-c19a93097129/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta è un array di tabelle da al sistema di automazione marketing. Trova la tabella da inserire in [!DNL Platform] e ne prende atto `path` come è necessario fornirlo nel passaggio successivo per esaminarne la struttura.

```json
[
    {
        "type": "table",
        "name": "Hubspot.All_Deals",
        "path": "Hubspot.All_Deals",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Blog_Authors",
        "path": "Hubspot.Blog_Authors",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Blog_Comments",
        "path": "Hubspot.Blog_Comments",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Contacts",
        "path": "Hubspot.Contacts",
        "canPreview": true,
        "canFetchSchema": true
    },
]
```

## Inspect: struttura di una tabella

Per controllare la struttura di una tabella dal sistema di automazione marketing, esegui una richiesta di GET specificando il percorso di una tabella come parametro di query.

**Formato API**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID di connessione per il sistema di automazione marketing. |
| `{TABLE_PATH}` | Percorso di una tabella all’interno del sistema di automazione marketing. |

**Richiesta**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/2fce94c1-9a93-4971-8e94-c19a93097129/explore?objectType=table&object=Hubspot.Contacts' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce la struttura di una tabella. I dettagli relativi a ciascuna colonna della tabella si trovano all’interno di elementi della sezione `columns` array.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Properties_Firstname_Value",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Properties_Lastname_Value",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Added_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Portal_Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
        ]
    }
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai esplorato il tuo sistema di automazione marketing, trovato il percorso della tabella che desideri portare in [!DNL Platform]e ha ottenuto informazioni sulla sua struttura. Queste informazioni sono disponibili nell&#39;esercitazione successiva per [raccogliere dati dal sistema di automazione marketing e inserirli in Platform](../collect/marketing-automation.md).
