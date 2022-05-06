---
keywords: Experience Platform;home;argomenti popolari;database di terze parti;servizio flusso di database
solution: Experience Platform
title: Esplorare un database utilizzando l’API del servizio di flusso
topic-legacy: overview
description: Questa esercitazione utilizza l’API del servizio di flusso per esplorare i contenuti e la struttura dei file di un database di terze parti.
exl-id: 94935492-a7be-48dc-8089-18476590bf98
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 2%

---

# Esplorare un database utilizzando [!DNL Flow Service] API

Questa esercitazione utilizza la funzione [!DNL Flow Service] API per esplorare i contenuti e la struttura dei file di un database di terze parti.

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a un database di terze parti utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Questa esercitazione richiede una connessione valida con il database di terze parti da cui si desidera acquisire i dati. Una connessione valida include l&#39;ID delle specifiche di connessione del database e l&#39;ID di connessione. Ulteriori informazioni sulla creazione di una connessione al database e sul recupero di tali valori sono disponibili nella sezione [panoramica dei connettori sorgente](./../../../home.md#database).

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell&#39;esercitazione sull&#39;autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le E[!DNL xperience Platform] Chiamate API, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], compresi quelli appartenenti [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* `Content-Type: application/json`

## Esplorare le tabelle di dati

Utilizzando l’ID di connessione per il database, è possibile esplorare le tabelle di dati eseguendo le richieste GET. Utilizza la seguente chiamata per trovare il percorso della tabella in cui desideri ispezionare o inserire [!DNL Platform].

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

Una risposta corretta restituisce un array di tabelle dal database. Trova il tavolo in cui vuoi inserire [!DNL Platform] e prendono atto della `path` , in quanto è necessario fornirlo nel passaggio successivo per esaminarne la struttura.

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

## Inspect la struttura di una tabella

Per esaminare la struttura di una tabella dal database, eseguire una richiesta di GET specificando il percorso di una tabella come parametro di query.

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

Una risposta corretta restituisce la struttura della tabella specificata. I dettagli relativi a ciascuna colonna della tabella si trovano all’interno degli elementi della `columns` array.

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

Seguendo questa esercitazione, hai esplorato il database e trovato il percorso della tabella in cui desideri inserire [!DNL Platform]e ha ottenuto informazioni sulla sua struttura. Puoi utilizzare queste informazioni nell’esercitazione successiva per [raccogliere i dati dal database e inserirli in Platform](../collect/database-nosql.md).
