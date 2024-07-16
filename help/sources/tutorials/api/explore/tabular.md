---
keywords: Experience Platform;home;argomenti popolari;origini;API;esplorare;servizio di flusso
title: Esplorare un Source tabulare utilizzando l’API del servizio Flusso
description: Questa esercitazione utilizza l’API Servizio flusso per esplorare il contenuto e la struttura di un’origine basata su tabella.
exl-id: 0c7a5b8a-2071-4ac2-b2d1-c5534e7c7d9c
source-git-commit: 3bdeec8284873b8d9368f833b24e9922ed489019
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 6%

---

# Esplora le tabelle di dati utilizzando l&#39;API [!DNL Flow Service]

Questo tutorial illustra come esplorare e visualizzare in anteprima la struttura e il contenuto delle tabelle dati utilizzando l&#39;API [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> Per esplorare le tabelle dati, è necessario disporre già di un ID connessione di base valido per un&#39;origine tabulare. Se non disponi di questo ID, consulta i seguenti tutorial per i passaggi su come creare un ID connessione di base per una sorgente tabulare: <ul><li>[Advertising](../../../home.md#advertising)</li><li>[CRM](../../../home.md#customer-relationship-management)</li><li>[Customer success](../../../home.md#customer-success)</li><li>[Database](../../../home.md#database)</li><li>[E-commerce](../../../home.md#ecommerce)</li><li>[Automazione marketing](../../../home.md#marketing-automation)</li><li>[Pagamenti](../../../home.md#payments)</li><li>[Protocolli](../../../home.md#protocols)</li></ul>

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../landing/api-guide.md).

## Esplora le tabelle di dati

È possibile recuperare informazioni sulla struttura delle tabelle dati effettuando una richiesta di GET all&#39;API [!DNL Flow Service] e fornendo l&#39;ID connessione di base dell&#39;origine.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID della connessione di base dell&#39;origine. |

**Richiesta**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un array di tabelle dall’origine. Individua la tabella da inserire in Platform e prendi nota della relativa proprietà `path`, in quanto devi fornirla nel passaggio successivo per esaminarne la struttura.

```json
[
    {
        "type": "table",
        "name": "ACME Spring Campaign",
        "path": "acmeSpringCampaign",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "ACME Summer Campaign",
        "path": "acmeSummerCampaign",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect: struttura di una tabella

Per verificare il contenuto delle tabelle dati, eseguire una richiesta di GET all&#39;API [!DNL Flow Service] specificando il percorso di una tabella come parametro di query.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID della connessione di base dell&#39;origine. |
| `{TABLE_PATH}` | La proprietà path della tabella che si desidera controllare. |

**Richiesta**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=table&object=acmeSpringCampaign' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce informazioni sul contenuto e sulla struttura della tabella specificata. I dettagli relativi a ciascuna colonna della tabella si trovano all&#39;interno di elementi dell&#39;array `columns`.

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
      },
      {
        "name": "Datefield",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "complaint_type",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "complaint_description",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status_change_date",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "city",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield2",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  }
}
```

## Passaggi successivi

Seguendo questa esercitazione, sono state raccolte informazioni sulla struttura e sul contenuto delle tabelle di dati. Inoltre, è stato recuperato il percorso della tabella da acquisire in Platform. Puoi utilizzare queste informazioni per creare una connessione di origine e un flusso di dati per portare i dati in Platform. Per i passaggi specifici su come creare una connessione di origine e un flusso di dati utilizzando l&#39;API [!DNL Flow Service], consulta i seguenti tutorial:

* [Origini Advertising](../collect/advertising.md)
* [Sorgenti CRM](../collect/crm.md)
* [Origini del successo del cliente](../collect/customer-success.md)
* [Origini del database](../collect/database-nosql.md)
* [Origini di e-commerce](../collect/ecommerce.md)
* [Origini di automazione del marketing](../collect/marketing-automation.md)
* [Origini dei pagamenti](../collect/payments.md)
* [Fonti di protocolli](../collect/protocols.md)
