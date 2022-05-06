---
keywords: Experience Platform;home;argomenti popolari;sistema pubblicitario;sistema pubblicitario
solution: Experience Platform
title: Esplorare un sistema pubblicitario utilizzando l’API del servizio di flusso
topic-legacy: overview
description: Flow Service viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti diverse all’interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui è possibile connettere tutte le sorgenti supportate. Questa esercitazione utilizza l’API del servizio Flusso per esplorare i sistemi pubblicitari.
exl-id: 3016ce1e-12e6-47ce-a4c5-52f8d440f515
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 3%

---

# Esplora un sistema pubblicitario utilizzando [!DNL Flow Service] API

Con la creazione di una connessione di base, è ora possibile utilizzare l&#39;ID univoco della connessione di base per navigare ed esplorare la struttura dati e il contenuto della sorgente. Questo ti consente di identificare gli elementi specifici, nonché i rispettivi tipi e formati di dati, prima di creare un flusso di dati e portarli in Adobe Experience Platform.

Questa esercitazione utilizza la funzione [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) per esplorare i sistemi pubblicitari.

## Introduzione

>[!IMPORTANT]
>
>Questa esercitazione richiede l&#39;ID univoco della connessione di base per l&#39;origine pubblicitaria. Se non disponi di questo ID, consulta l’esercitazione su [collegamento di un’origine pubblicitaria a Platform](../../api/create/advertising/ads.md) esercitazione.

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a un sistema pubblicitario utilizzando [!DNL Flow Service] API.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../landing/api-guide.md).

## Esplorare le tabelle di dati

Utilizzando la connessione di base per il sistema pubblicitario, è possibile esplorare le tabelle di dati eseguendo le richieste di GET. Utilizza la seguente chiamata per trovare il percorso della tabella in cui desideri ispezionare o inserire [!DNL Platform].

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta è un array di tabelle da al sistema pubblicitario. Trova il tavolo in cui vuoi inserire [!DNL Platform] e prendono atto della `path` , in quanto è necessario fornirlo nel passaggio successivo per esaminarne la struttura.

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

## Inspect la struttura di una tabella

Per esaminare la struttura di una tabella dal sistema pubblicitario, esegui una richiesta di GET specificando il percorso di una tabella come parametro di query.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID di connessione per il sistema pubblicitario. |
| `{TABLE_PATH}` | Percorso di una tabella all’interno del sistema pubblicitario. |

**Richiesta**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=table&object=v201809.AD_PERFORMANCE_REPORT' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce la struttura di una tabella. I dettagli relativi a ciascuna colonna della tabella si trovano all’interno degli elementi della `columns` array.

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

Seguendo questa esercitazione, hai esplorato il tuo sistema pubblicitario, trovato il percorso della tabella a cui desideri accedere [!DNL Platform]e ha ottenuto informazioni sulla sua struttura. Puoi utilizzare queste informazioni nell’esercitazione successiva per [raccogliere dati dal tuo sistema pubblicitario e inserirli in Platform](../collect/advertising.md).
