---
keywords: Experience Platform;home;argomenti popolari;advertising system;Advertising system
solution: Experience Platform
title: Esplorare un sistema pubblicitario utilizzando l’API del servizio Flow
description: Flow Service è utilizzato per raccogliere e centralizzare i dati dei clienti da diverse origini all’interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui tutte le sorgenti supportate sono collegabili. Questa esercitazione utilizza l’API Flow Service per esplorare i sistemi pubblicitari.
exl-id: 3016ce1e-12e6-47ce-a4c5-52f8d440f515
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 3%

---

# Esplora un sistema pubblicitario utilizzando [!DNL Flow Service] API

Dopo aver creato una connessione di base, è ora possibile utilizzare l&#39;ID univoco della connessione di base per navigare ed esplorare la struttura dati e il contenuto dell&#39;origine. Questo ti consente di identificare gli elementi specifici e i rispettivi tipi di dati e formati, prima di creare un flusso di dati e trasferirli a Adobe Experience Platform.

Questa esercitazione utilizza [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) per esplorare i sistemi pubblicitari.

## Introduzione

>[!IMPORTANT]
>
>Questo tutorial richiede di disporre dell’ID di connessione di base univoco per la tua origine pubblicitaria. Se non disponi di questo ID, consulta l’esercitazione su [collegamento di un’origine pubblicitaria a Platform](../../api/create/advertising/ads.md) esercitazione.

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a un sistema pubblicitario utilizzando [!DNL Flow Service] API.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../landing/api-guide.md).

## Esplora le tabelle di dati

Utilizzando la connessione di base per il sistema pubblicitario, puoi esplorare le tabelle di dati eseguendo richieste GET. Utilizza la seguente chiamata per trovare il percorso della tabella da ispezionare o in cui desideri acquisire [!DNL Platform].

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

Una risposta corretta è un array di tabelle da al sistema pubblicitario. Trova la tabella da inserire in [!DNL Platform] e ne prende atto `path` come è necessario fornirlo nel passaggio successivo per esaminarne la struttura.

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

## Inspect: struttura di una tabella

Per controllare la struttura di una tabella dal sistema pubblicitario, esegui una richiesta di GET specificando il percorso di una tabella come parametro di query.

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

In caso di esito positivo, la risposta restituisce la struttura di una tabella. I dettagli relativi a ciascuna colonna della tabella si trovano all’interno di elementi della sezione `columns` array.

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

Seguendo questa esercitazione, hai esplorato il tuo sistema pubblicitario, trovato il percorso della tabella che desideri portare in [!DNL Platform]e ha ottenuto informazioni sulla sua struttura. Queste informazioni sono disponibili nell&#39;esercitazione successiva per [raccogliere dati dal sistema pubblicitario e inserirli in Platform](../collect/advertising.md).
