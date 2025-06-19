---
title: Registra richieste di eliminazione (endpoint ordine di lavoro)
description: L’endpoint /workorder nell’API di igiene dei dati consente di gestire in modo programmatico le attività di eliminazione per le identità.
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: d569b1d04fa76e0a0e48364a586e8a1a773b9bf2
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 2%

---

# Registra richieste di eliminazione (endpoint ordine di lavoro) {#work-order-endpoint}

L&#39;endpoint `/workorder` nell&#39;API di igiene dei dati consente di gestire programmaticamente le richieste di eliminazione dei record in Adobe Experience Platform.

>[!IMPORTANT]
> 
>Le eliminazioni di record devono essere utilizzate per la pulizia dei dati, la rimozione di dati anonimi o la minimizzazione dei dati. Sono **not** da utilizzare per le richieste di diritti degli interessati (conformità) in relazione alle normative sulla privacy come il Regolamento generale sulla protezione dei dati (RGPD). Per tutti i casi di utilizzo di conformità, utilizzare [Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’API di igiene dei dati. Prima di continuare, controlla la [panoramica](./overview.md) per trovare i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e le informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Quote e timeline di elaborazione {#quotas}

Registra Le richieste di cancellazione sono soggette ai limiti di invio giornalieri e mensili degli identificatori, determinati in base al diritto alla licenza della tua organizzazione. Questi limiti si applicano sia alle richieste di eliminazione basate su API che su interfaccia utente.

>[!NOTE]
>
>Puoi inviare fino a **1.000.000 identificatori al giorno**, ma solo se lo consente la quota mensile rimanente. Se il limite mensile è inferiore a 1 milione, le richieste giornaliere non possono superare tale limite.

### Diritto invio mensile per prodotto {#quota-limits}

La tabella seguente illustra i limiti di invio degli identificatori per prodotto e livello di adesione. Per ogni prodotto, il limite mensile è il minore tra due valori: un limite fisso di identificazione o una soglia basata su percentuale associata al volume di dati concesso in licenza.

| Prodotto | Descrizione diritto | Limite mensile (scegliendo il valore minore) |
|----------|-------------------------|---------------------------------|
| REAL-TIME CDP o ADOBE JOURNEY OPTIMIZER | Senza il componente aggiuntivo Privacy and Security Shield o Healthcare Shield | 2.000.000 identificatori o il 5% del pubblico indirizzabile |
| REAL-TIME CDP o ADOBE JOURNEY OPTIMIZER | Con il componente aggiuntivo Privacy and Security Shield o Healthcare Shield | 15.000.000 identificatori o il 10% del pubblico indirizzabile |
| Customer Journey Analytics | Senza il componente aggiuntivo Privacy and Security Shield o Healthcare Shield | 2.000.000 identificatori o 100 identificatori per milione di righe CJA di diritto |
| Customer Journey Analytics | Con il componente aggiuntivo Privacy and Security Shield o Healthcare Shield | 15.000.000 identificatori o 200 identificatori per milione di righe CJA di diritto |

>[!NOTE]
>
> La maggior parte delle organizzazioni avrà limiti mensili inferiori in base al proprio pubblico indirizzabile effettivo o ai diritti di riga di CJA.

Le quote vengono reimpostate il primo giorno di ogni mese di calendario. La quota non utilizzata **non** viene riportata.

>[!NOTE]
>
>Le quote si basano sui diritti mensili concessi in licenza dalla tua organizzazione per **identificatori inviati**. Queste non vengono applicate dai guardrail di sistema, ma possono essere monitorate e riviste.
>
>Eliminazione record è un **servizio condiviso**. Il limite mensile riflette il diritto più alto tra Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics ed eventuali componenti aggiuntivi Shield applicabili.

### Elaborazione dei timeline per l’invio degli identificatori {#sla-processing-timelines}

Dopo l’invio, le richieste di eliminazione dei record vengono messe in coda ed elaborate in base al livello di adesione.

| Descrizione del prodotto e della licenza | Durata coda | Tempo di elaborazione massimo (SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Senza il componente aggiuntivo Privacy and Security Shield o Healthcare Shield | Fino a 15 giorni | 30 giorni |
| Con il componente aggiuntivo Privacy and Security Shield o Healthcare Shield | In genere 24 ore | 15 giorni |

Se l’organizzazione richiede limiti più elevati, contatta il rappresentante Adobe per una revisione dell’adesione.

>[!TIP]
>
>Per verificare l&#39;utilizzo o il livello di adesione corrente, vedere la [Guida di riferimento della quota](../api/quota.md).

## Creare una richiesta di eliminazione record {#create}

È possibile eliminare una o più identità da un singolo set di dati o da tutti i set di dati effettuando una richiesta POST all&#39;endpoint `/workorder`.

>[!TIP]
>
>Ogni richiesta di eliminazione del record inviata tramite l&#39;API può includere fino a **100.000 identità**. Per massimizzare l’efficienza, invia il maggior numero possibile di identità per richiesta ed evita invii di volumi ridotti, ad esempio ordini di lavoro con ID singolo.

**Formato API**

```http
POST /workorder
```

>[!NOTE]
>
>Le richieste del ciclo di vita dei dati possono modificare solo set di dati basati su identità primarie o una mappa di identità. Una richiesta deve specificare l’identità primaria o fornire una mappa di identità.

**Richiesta**

A seconda del valore di `datasetId` fornito nel payload della richiesta, la chiamata API eliminerà le identità da tutti i set di dati o da un singolo set di dati specificato. La richiesta seguente elimina tre identità da un set di dati specifico.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "action": "delete_identity",
        "datasetId": "c48b51623ec641a2949d339bad69cb15",
        "displayName": "Example Record Delete Request",
        "description": "Cleanup identities required by Jira request 12345.",
        "identities": [
          {
            "namespace": {
              "code": "email"
            },
            "id": "poul.anderson@example.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cordwainer.smith@gmail.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cyril.kornbluth@yahoo.com"
          }
        ]
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `action` | Azione da eseguire. Il valore deve essere impostato su `delete_identity` per le eliminazioni di record. |
| `datasetId` | Se stai eliminando dati da un singolo set di dati, questo valore deve essere l’ID del set di dati in questione. Se si elimina da tutti i set di dati, impostare il valore su `ALL`.<br><br>Se specifichi un singolo set di dati, lo schema Experience Data Model (XDM) associato al set di dati deve avere un&#39;identità primaria definita. Se il set di dati non ha un’identità primaria, per poter essere modificato da una richiesta del ciclo di vita dei dati deve disporre di una mappa di identità.<br>Se esiste una mappa di identità, questa sarà presente come campo di primo livello denominato `identityMap`.<br>Tieni presente che una riga di set di dati può avere molte identità nella mappa delle identità, ma solo una può essere contrassegnata come principale. `"primary": true` deve essere incluso per forzare `id` a corrispondere a un&#39;identità primaria. |
| `displayName` | Nome visualizzato per la richiesta di eliminazione del record. |
| `description` | Descrizione della richiesta di eliminazione record. |
| `identities` | Matrice contenente le identità di almeno un utente di cui desideri eliminare le informazioni. Ogni identità è composta da uno spazio dei nomi [identità](../../identity-service/features/namespaces.md) e da un valore:<ul><li>`namespace`: contiene una singola proprietà stringa, `code`, che rappresenta lo spazio dei nomi dell&#39;identità. </li><li>`id`: valore di identità.</ul>Se `datasetId` specifica un singolo set di dati, ogni entità in `identities` deve utilizzare lo stesso spazio dei nomi identità dell&#39;identità primaria dello schema.<br><br>Se `datasetId` è impostato su `ALL`, l&#39;array `identities` non è vincolato ad alcun singolo spazio dei nomi poiché ogni set di dati potrebbe essere diverso. Tuttavia, le tue richieste sono ancora vincolate agli spazi dei nomi disponibili per la tua organizzazione, come segnalato da [Identity Service](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli dell’eliminazione del record.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| Proprietà | Descrizione |
| --- | --- |
| `workorderId` | ID dell’ordine di eliminazione. Questa può essere utilizzata per cercare lo stato dell’eliminazione in un secondo momento. |
| `orgId` | ID organizzazione. |
| `bundleId` | ID del bundle a cui è associato questo ordine di eliminazione, utilizzato a scopo di debug. Più ordini di eliminazione sono raggruppati per essere elaborati dai servizi a valle. |
| `action` | Azione eseguita dall&#39;ordine di lavoro. Per le eliminazioni di record, il valore è `identity-delete`. |
| `createdAt` | Un timestamp indicante quando è stato creato l’ordine di eliminazione. |
| `updatedAt` | Timestamp dell’ultimo aggiornamento dell’ordine di eliminazione. |
| `status` | Stato corrente dell&#39;ordine di eliminazione. |
| `createdBy` | Utente che ha creato l&#39;ordine di eliminazione. |
| `datasetId` | ID del set di dati soggetto alla richiesta. Se la richiesta è per tutti i set di dati, il valore sarà impostato su `ALL`. |

{style="table-layout:auto"}

## Recuperare lo stato di un&#39;eliminazione record {#lookup}

Dopo aver [creato una richiesta di eliminazione record](#create), puoi verificarne lo stato utilizzando una richiesta GET.

**Formato API**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{WORK_ORDER_ID}` | `workorderId` dell&#39;eliminazione record che si sta cercando. |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli dell’operazione di eliminazione, compreso lo stato corrente.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345.",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `workorderId` | ID dell’ordine di eliminazione. Questa può essere utilizzata per cercare lo stato dell’eliminazione in un secondo momento. |
| `orgId` | ID organizzazione. |
| `bundleId` | ID del bundle a cui è associato questo ordine di eliminazione, utilizzato a scopo di debug. Più ordini di eliminazione sono raggruppati per essere elaborati dai servizi a valle. |
| `action` | Azione eseguita dall&#39;ordine di lavoro. Per le eliminazioni di record, il valore è `identity-delete`. |
| `createdAt` | Un timestamp indicante quando è stato creato l’ordine di eliminazione. |
| `updatedAt` | Timestamp dell’ultimo aggiornamento dell’ordine di eliminazione. |
| `status` | Stato corrente dell&#39;ordine di eliminazione. |
| `createdBy` | Utente che ha creato l&#39;ordine di eliminazione. |
| `datasetId` | ID del set di dati soggetto alla richiesta. Se la richiesta è per tutti i set di dati, il valore sarà impostato su `ALL`. |
| `productStatusDetails` | Array che elenca lo stato corrente dei processi a valle correlati alla richiesta. Ogni oggetto array contiene le seguenti proprietà:<ul><li>`productName`: nome del servizio downstream.</li><li>`productStatus`: stato di elaborazione corrente della richiesta dal servizio downstream.</li><li>`createdAt`: marca temporale di quando il servizio ha pubblicato lo stato più recente.</li></ul> |

## Aggiornare una richiesta di eliminazione record

È possibile aggiornare `displayName` e `description` per un&#39;eliminazione record effettuando una richiesta PUT.

**Formato API**

```http
PUT /workorder{WORK_ORDER_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{WORK_ORDER_ID}` | `workorderId` dell&#39;eliminazione record che si sta cercando. |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName" : "Update - displayName",
        "description" : "Update - description"
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `displayName` | Nome visualizzato aggiornato per la richiesta di eliminazione del record. |
| `description` | Descrizione aggiornata della richiesta di eliminazione record. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli dell’eliminazione del record.

```json
{
    "workorderId": "DI-61828416-963a-463f-91c1-dbc4d0ddbd43",
    "orgId": "{ORG_ID}",
    "bundleId": "BN-aacacc09-d10c-48c5-a64c-2ced96a78fca",
    "action": "identity-delete",
    "createdAt": "2024-06-12T20:02:49.398448Z",
    "updatedAt": "2024-06-13T21:35:01.944749Z",
    "operationCount": 1,
    "status": "ingested",
    "createdBy": "{USER_ID}",
    "datasetId": "666950e6b7e2022c9e7d7a33",
    "datasetName": "Acme_Dataset_E2E_Identity_Map_Schema_5_1718178022379",
    "displayName": "Updated Display Name",
    "description": "Updated Description",
    "productStatusDetails": [
        {
            "productName": "Data Management",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Identity Service",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:36:09.020832Z"
        },
        {
            "productName": "Profile Service",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Journey Orchestrator",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:12:19.843199Z"
        }
    ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `workorderId` | ID dell’ordine di eliminazione. Questa può essere utilizzata per cercare lo stato dell’eliminazione in un secondo momento. |
| `orgId` | ID organizzazione. |
| `bundleId` | ID del bundle a cui è associato questo ordine di eliminazione, utilizzato a scopo di debug. Più ordini di eliminazione sono raggruppati per essere elaborati dai servizi a valle. |
| `action` | Azione eseguita dall&#39;ordine di lavoro. Per le eliminazioni di record, il valore è `identity-delete`. |
| `createdAt` | Un timestamp indicante quando è stato creato l’ordine di eliminazione. |
| `updatedAt` | Timestamp dell’ultimo aggiornamento dell’ordine di eliminazione. |
| `status` | Stato corrente dell&#39;ordine di eliminazione. |
| `createdBy` | Utente che ha creato l&#39;ordine di eliminazione. |
| `datasetId` | ID del set di dati soggetto alla richiesta. Se la richiesta è per tutti i set di dati, il valore sarà impostato su `ALL`. |
| `productStatusDetails` | Array che elenca lo stato corrente dei processi a valle correlati alla richiesta. Ogni oggetto array contiene le seguenti proprietà:<ul><li>`productName`: nome del servizio downstream.</li><li>`productStatus`: stato di elaborazione corrente della richiesta dal servizio downstream.</li><li>`createdAt`: marca temporale di quando il servizio ha pubblicato lo stato più recente.</li></ul> |

{style="table-layout:auto"}
