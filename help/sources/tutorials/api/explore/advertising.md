---
keywords: ' Experience Platform;casa;argomenti popolari;sistema pubblicitario;sistema pubblicitario'
solution: Experience Platform
title: Esplora un sistema pubblicitario utilizzando l'API del servizio di flusso
topic: overview
description: Flow Service è utilizzato per raccogliere e centralizzare i dati dei clienti da varie origini diverse all'interno di Adobe Experience Platform. Il servizio fornisce un'interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate. Questa esercitazione utilizza l'API del servizio di flusso per esplorare i sistemi pubblicitari.
translation-type: tm+mt
source-git-commit: 62266187ed1f3ce2f0acca3f50487fb70cfa7307
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 1%

---


# Esplora un sistema pubblicitario utilizzando l&#39;API [!DNL Flow Service]

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie origini all&#39;interno di Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39;API [!DNL Flow Service] per esplorare i sistemi pubblicitari.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../home.md):  [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
* [Sandbox](../../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a un sistema pubblicitario utilizzando l&#39;API [!DNL Flow Service].

### Raccogli credenziali richieste

Questa esercitazione richiede una connessione valida con l&#39;applicazione pubblicitaria di terze parti da cui si desidera acquisire i dati. Una connessione valida include l&#39;ID della specifica di connessione dell&#39;applicazione e l&#39;ID di connessione. Ulteriori informazioni sulla creazione di una connessione pubblicitaria e il recupero di tali valori sono disponibili nell&#39;esercitazione [collegare un&#39;origine pubblicitaria a Platform](../../api/create/advertising/ads.md).

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a2/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* `Content-Type: application/json`

## Esplora le tabelle di dati

Utilizzando la connessione di base per il sistema pubblicitario, potete esplorare le tabelle di dati eseguendo le richieste di GET. Utilizzate la seguente chiamata per trovare il percorso della tabella che desiderate ispezionare o assimilare in [!DNL Platform].

**Formato API**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID della connessione di base per il sistema pubblicitario. |

**Richiesta**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta di successo è un array di tabelle da al sistema pubblicitario. Trovare la tabella che si desidera inserire in [!DNL Platform] e prendere nota della relativa proprietà `path`, in quanto è necessario fornirla nel passaggio successivo per ispezionare la struttura.

```json
[
    {
        "type": "table",
        "name": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "path": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "path": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "path": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_PERFORMANCE_REPORT",
        "path": "v201809.AD_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

##  Inspect la struttura di una tabella

Per esaminare la struttura di una tabella dal sistema pubblicitario, eseguire una richiesta di GET specificando il percorso di una tabella come parametro di query.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID connessione per il sistema pubblicitario. |
| `{TABLE_PATH}` | Percorso di una tabella all&#39;interno del sistema pubblicitario. |

**Richiesta**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=table&object=v201809.AD_PERFORMANCE_REPORT' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce la struttura di una tabella. I dettagli relativi a ciascuna colonna della tabella si trovano all&#39;interno degli elementi dell&#39;array `columns`.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "CallOnlyPhoneNumber",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "AdGroupId",
                "type": "long",
                "xdm": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                }
            },
            {
                "name": "AdGroupName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Date",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
        ]
    }
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai esplorato il tuo sistema pubblicitario, trovato il percorso della tabella che desideri portare in [!DNL Platform], e ottenuto informazioni sulla sua struttura. Potete utilizzare queste informazioni nell&#39;esercitazione successiva per [raccogliere i dati dal sistema pubblicitario e inserirli nella piattaforma](../collect/advertising.md).
