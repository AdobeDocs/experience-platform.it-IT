---
keywords: Experience Platform;home;argomenti popolari;origini;API;esplorare;servizio di flusso
title: Esplorare una sorgente tabulare utilizzando l’API del servizio di flusso
description: Questa esercitazione utilizza l’API del servizio di flusso per esplorare i contenuti e la struttura di un’origine basata su tabelle.
source-git-commit: 1333eac5e022ef32f051120496154a88e2f9324e
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 3%

---

# Esplorare le tabelle di dati utilizzando [!DNL Flow Service] API

Questa esercitazione fornisce passaggi su come esplorare e visualizzare in anteprima la struttura e il contenuto delle tabelle di dati utilizzando [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API.

>[!NOTE]
>
> Per esplorare le tabelle di dati, è necessario disporre già di un ID di connessione di base valido per un&#39;origine tabulare. Se non disponi di questo ID, consulta le seguenti esercitazioni per i passaggi necessari per creare un ID di connessione di base per un’origine tabulare: <ul><li>[Advertising](../../../home.md#advertising)</li><li>[CRM](../../../home.md#customer-relationship-management)</li><li>[Successo cliente](../../../home.md#customer-success)</li><li>[Database](../../../home.md#database)</li><li>[E-commerce](../../../home.md#ecommerce)</li><li>[Automazione del marketing](../../../home.md#marketing-automation)</li><li>[Pagamenti](../../../home.md#payments)</li><li>[Protocolli](../../../home.md#protocols)</li></ul>

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../landing/api-guide.md).

## Esplorare le tabelle di dati

È possibile recuperare informazioni sulla struttura delle tabelle di dati effettuando una richiesta di GET al [!DNL Flow Service] API fornendo l&#39;ID di connessione di base della sorgente.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID connessione di base della sorgente. |

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

Una risposta corretta restituisce un array di tabelle dall&#39;origine. Trova la tabella che desideri portare in Platform e prendi nota della sua `path` , in quanto è necessario fornirlo nel passaggio successivo per esaminarne la struttura.

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

## Inspect la struttura di una tabella

Per esaminare il contenuto delle tabelle di dati, esegui una richiesta di GET al [!DNL Flow Service] API quando si specifica il percorso di una tabella come parametro di query.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID connessione di base della sorgente. |
| `{TABLE_PATH}` | Proprietà del percorso della tabella che si desidera esaminare. |

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

Una risposta corretta restituisce informazioni sul contenuto e sulla struttura della tabella specificata. I dettagli relativi a ciascuna colonna della tabella si trovano all’interno degli elementi della `columns` array.

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

Seguendo questa esercitazione, hai raccolto informazioni sulla struttura e il contenuto delle tabelle di dati. Inoltre, hai recuperato il percorso della tabella che desideri inserire in Platform. Puoi utilizzare queste informazioni per creare una connessione sorgente e un flusso di dati per trasferire i tuoi dati a Platform. Per istruzioni specifiche su come creare una connessione sorgente e un flusso di dati utilizzando i [!DNL Flow Service] API:

* [Fonti pubblicitarie](../collect/advertising.md)
* [Origini CRM](../collect/crm.md)
* [Fonti di successo del cliente](../collect/customer-success.md)
* [Origini del database](../collect/database-nosql.md)
* [Fonti di e-commerce](../collect/ecommerce.md)
* [Origini dell&#39;automazione del marketing](../collect/marketing-automation.md)
* [Origini dei pagamenti](../collect/payments.md)
* [Origini dei protocolli](../collect/protocols.md)