---
keywords: Experience Platform;home;popular topics;ecommerce;eCommerce
solution: Experience Platform
title: Esplora una connessione di eCommerce tramite l’API del servizio di flusso
topic: overview
description: Questa esercitazione utilizza l’API del servizio di flusso per esplorare le connessioni eCommerce.
translation-type: tm+mt
source-git-commit: 4696bcb17427bb50549a315294baf7fbd87ac01d
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 2%

---


# Esplora una connessione di eCommerce tramite l&#39; [!DNL Flow Service] API

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie origini all&#39;interno di Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39; [!DNL Flow Service] API per esplorare una connessione di terze parti **[!UICONTROL eCommerce]** .

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Sources]](../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] i servizi.
* [[!DNL Sandboxes]](../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a una **[!UICONTROL eCommerce]** connessione utilizzando l&#39; [!DNL Flow Service] API.

### Ottenere un ID connessione

Per esplorare la **[!UICONTROL eCommerce]** connessione utilizzando [!DNL Platform] le API, è necessario possedere un ID di connessione valido. Se non disponete già di una connessione per la **[!UICONTROL eCommerce]** connessione con cui desiderate lavorare, potete crearne una tramite la seguente esercitazione:

* [Shopificare](../create/ecommerce/shopify.md)

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* `Content-Type: application/json`

## Esplora le tabelle di dati

Utilizzando l&#39;ID **[!UICONTROL eCommerce]** connessione, è possibile esplorare le tabelle di dati eseguendo richieste di GET. Utilizzate la seguente chiamata per trovare il percorso della tabella in cui desiderate ispezionare o assimilare [!DNL Platform].

**Formato API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| Parametro | Descrizione |
| --- | --- |
| `{CONNECTION_ID}` | L&#39;ID **[!UICONTROL eCommerce]** connessione. |

**Richiesta**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un array di tabelle dalla **[!UICONTROL eCommerce]** connessione. Trovare la tabella che si desidera inserire [!DNL Platform] e prendere nota della relativa `path` proprietà, in quanto è necessario fornire nel passaggio successivo per ispezionare la sua struttura.

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

##  Inspect la struttura di una tabella

Per esaminare la struttura di una tabella dalla **[!UICONTROL eCommerce]** connessione, eseguire una richiesta di GET specificando il percorso di una tabella all&#39;interno di un parametro di `object` query.

**Formato API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | ID connessione della **[!UICONTROL eCommerce]** connessione. |
| `{TABLE_PATH}` | Percorso di una tabella all&#39;interno della **[!UICONTROL eCommerce]** connessione. |

**Richiesta**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=table&object=Orders' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce la struttura della tabella specificata. I dettagli relativi a ciascuna colonna della tabella si trovano all&#39;interno degli elementi dell&#39; `columns` array.

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

Seguendo questa esercitazione, hai esplorato la tua **[!UICONTROL eCommerce]** connessione, trovato il percorso della tabella in cui desideri immergerti [!DNL Platform]e ottenuto informazioni sulla sua struttura. Potete utilizzare queste informazioni nell&#39;esercitazione successiva per [raccogliere i dati eCommerce e importarli nella piattaforma](../collect/ecommerce.md).
