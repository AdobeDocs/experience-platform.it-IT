---
keywords: Experience Platform;home;argomenti popolari;pagamento;;home;popular topic;payment
solution: Experience Platform
title: Esplorare un sistema di pagamento utilizzando l’API del servizio Flusso
description: Questa esercitazione utilizza l’API del servizio Flow per esplorare le applicazioni di pagamento.
exl-id: 7d0231de-46c0-49df-8a10-aeb42a2c8822
source-git-commit: 104db777446b19fa9e3ea7538ae1dda6f51a00b1
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 13%

---

# Esplora un sistema di pagamento utilizzando l&#39;API [!DNL Flow Service]

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da diverse origini all&#39;interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui tutte le sorgenti supportate sono collegabili.

Questo tutorial utilizza l&#39;API [!DNL Flow Service] per esplorare le applicazioni di pagamento.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Experience Platform].
* [Sandbox](../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Experience Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a un&#39;applicazione di pagamento tramite l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Per esplorare i file e la struttura dei file dell&#39;origine, è necessario disporre di una connessione attiva con un&#39;applicazione di pagamento. Per ulteriori informazioni, consulta i seguenti documenti:

* [[!DNL Square]](../create/payments/square.md)
* [[!DNL Stripe]](../create/payments/stripe.md)

### Lettura delle chiamate API di esempio

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate alle API [!DNL Experience Platform], devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

* Autorizzazione: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Experience Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* Tipo di contenuto: `application/json`

## Esplora le tabelle di dati

Utilizzando l’ID di connessione per il sistema di pagamenti in uso, puoi esplorare le tabelle di dati eseguendo le richieste di GET. Utilizzare la seguente chiamata per trovare il percorso della tabella da controllare o acquisire in [!DNL Experience Platform].

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID di una connessione alla base pagamenti. |

**Richiesta**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/24151d58-ffa7-4960-951d-58ffa7396097/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un array di tabelle dal sistema di pagamenti. Individuare la tabella che si desidera inserire in [!DNL Experience Platform] e prendere nota della relativa proprietà `path`, in quanto è necessario fornirla nel passaggio successivo per esaminarne la struttura.

```json
[
    {
        "type": "table",
        "name": "Stripe.Billing_Plans",
        "path": "Stripe.Billing_Plans",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Stripe.Billing_Plans_Payment_Definition",
        "path": "Stripe.Billing_Plans_Payment_Definition",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Stripe.Billing_Plans_Payment_Definition_Charge_Models",
        "path": "Stripe.Billing_Plans_Payment_Definition_Charge_Models",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Stripe.Catalog_Products",
        "path": "Stripe.Catalog_Products",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Controllare la struttura di una tabella

Per controllare la struttura di una tabella dal sistema dei pagamenti, eseguire una richiesta GET specificando il percorso di una tabella come parametro di query.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | ID di connessione del sistema di pagamenti. |
| `{TABLE_PATH}` | Percorso di una tabella all’interno del sistema di pagamenti. |

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/24151d58-ffa7-4960-951d-58ffa7396097/explore?objectType=table&object=test1.Mytable' \
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
                "name": "Product_Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Product_Name",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Description",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Type",
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

Seguendo questa esercitazione, hai esplorato il tuo sistema di pagamenti, trovato il percorso della tabella che desideri acquisire in [!DNL Experience Platform] e ottenuto informazioni relative alla sua struttura. Puoi utilizzare queste informazioni nel prossimo tutorial per [raccogliere dati dal tuo sistema di pagamenti e inserirli in Experience Platform](../collect/payments.md).
