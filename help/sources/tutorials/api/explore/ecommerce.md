---
keywords: Experience Platform;home;argomenti popolari;ecommerce;eCommerce
solution: Experience Platform
title: Esplorare una connessione eCommerce utilizzando l’API del servizio Flusso
description: Questa esercitazione utilizza l’API del servizio Flusso per esplorare le connessioni eCommerce.
exl-id: 832ce399-6c9f-40da-8e7c-5434503c16b6
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 2%

---

# Esplora una connessione eCommerce utilizzando [!DNL Flow Service] API

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da diverse origini all’interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui tutte le sorgenti supportate sono collegabili.

Questa esercitazione utilizza [!DNL Flow Service] API per esplorare terze parti **[!UICONTROL eCommerce]** connessione.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Sources]](../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [[!DNL Sandboxes]](../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a un **[!UICONTROL eCommerce]** connessione tramite [!DNL Flow Service] API.

### Ottenere un ID di connessione

Per esplorare il tuo **[!UICONTROL eCommerce]** connessione tramite [!DNL Platform] API, devi disporre di un ID di connessione valido. Se non disponi già di una connessione per **[!UICONTROL eCommerce]** connessione che desideri utilizzare, puoi crearne una tramite la seguente esercitazione:

* [Shopify](../create/ecommerce/shopify.md)

### Lettura delle chiamate API di esempio

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nel [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori per le intestazioni richieste

Per effettuare chiamate a [!DNL Platform] , devi prima completare le [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], compresi quelli appartenenti a [!DNL Flow Service], sono isolate in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* `Content-Type: application/json`

## Esplora le tabelle di dati

Utilizzo di **[!UICONTROL eCommerce]** ID connessione, puoi esplorare le tabelle di dati eseguendo richieste GET. Utilizza la seguente chiamata per trovare il percorso della tabella da ispezionare o in cui desideri acquisire [!DNL Platform].

**Formato API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| Parametro | Descrizione |
| --- | --- |
| `{CONNECTION_ID}` | Il tuo **[!UICONTROL eCommerce]** ID connessione. |

**Richiesta**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce una matrice di tabelle dalla **[!UICONTROL eCommerce]** connessione. Trova la tabella da inserire in [!DNL Platform] e ne prende atto `path` come è necessario fornirlo nel passaggio successivo per esaminarne la struttura.

```json
[
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Discount_Codes",
        "path": "Shopify.Abandoned_Checkout_Discount_Codes",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Line_Items",
        "path": "Shopify.Abandoned_Checkout_Line_Items",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Blogs",
        "path": "Shopify.Blogs",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Orders",
        "path": "Shopify.Orders",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect: struttura di una tabella

Per controllare la struttura di una tabella dal **[!UICONTROL eCommerce]** connessione, esegui una richiesta di GET specificando il percorso di una tabella in un `object` parametro di query.

**Formato API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | ID di connessione del tuo **[!UICONTROL eCommerce]** connessione. |
| `{TABLE_PATH}` | Percorso di una tabella all’interno del **[!UICONTROL eCommerce]** connessione. |

**Richiesta**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=table&object=Orders' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce la struttura della tabella specificata. I dettagli relativi a ciascuna colonna della tabella si trovano all’interno di elementi della sezione `columns` array.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Blog_Id",
                "type": "double",
                "xdm": {
                    "type": "number"
                }
            },
            {
                "name": "Title",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Created_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Tags",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Updated_At": "2020-11-05T10:54:36",
            "Title": "News",
            "Commentable": "no",
            "Blog_Id": 5.5458332804E10,
            "Handle": "news",
            "Created_At": "2020-02-14T09:11:15"
        }
    ]
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai esplorato **[!UICONTROL eCommerce]** connessione, trovato il percorso della tabella in cui desideri inserire [!DNL Platform]e ha ottenuto informazioni sulla sua struttura. Queste informazioni sono disponibili nell&#39;esercitazione successiva per [raccogliere i dati di eCommerce e inserirli in Platform](../collect/ecommerce.md).
