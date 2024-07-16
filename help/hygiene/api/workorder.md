---
title: Endpoint API ordine di lavoro
description: L’endpoint /workorder nell’API di igiene dei dati consente di gestire in modo programmatico le attività di eliminazione per le identità.
badgeBeta: label="Beta" type="Informative"
role: Developer
badge: Beta
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: bf819d506b0ee6f3aba6850f598ee46f16695dfa
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 2%

---

# Endpoint ordine di lavoro {#work-order-endpoint}

L&#39;endpoint `/workorder` nell&#39;API di igiene dei dati consente di gestire programmaticamente le richieste di eliminazione dei record in Adobe Experience Platform.

>[!IMPORTANT]
> 
>La funzionalità di eliminazione dei record è attualmente disponibile in Beta ed è disponibile solo in una **versione limitata**. Non è disponibile per tutti i clienti. Le richieste di cancellazione dei record sono disponibili solo per le organizzazioni nella versione limitata.
>
>Le eliminazioni di record devono essere utilizzate per la pulizia dei dati, la rimozione di dati anonimi o la minimizzazione dei dati. Sono **not** da utilizzare per le richieste di diritti degli interessati (conformità) in relazione alle normative sulla privacy come il Regolamento generale sulla protezione dei dati (RGPD). Per tutti i casi di utilizzo di conformità, utilizzare [Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’API di igiene dei dati. Prima di continuare, controlla la [panoramica](./overview.md) per trovare i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e le informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API Experience Platform.

## Creare una richiesta di eliminazione record {#create}

Per eliminare una o più identità da un singolo set di dati o da tutti i set di dati, effettua una richiesta POST all&#39;endpoint `/workorder`.

>[!IMPORTANT]
> 
>Esistono limiti diversi per il numero totale di eliminazioni di record di identità univoci che possono essere inviate ogni mese. Questi limiti sono basati sul contratto di licenza. Le organizzazioni che hanno acquistato tutte le edizioni di Adobe Real-time Customer Data Platform e Adobe Journey Optimizer possono inviare fino a 100.000 record di identità eliminati ogni mese. Le organizzazioni che hanno acquistato **Adobe Healthcare Shield** o **Adobe Privacy &amp; Security Shield** possono inviare fino a 600.000 record di identità eliminati ogni mese.<br>Una singola [richiesta di eliminazione record tramite l&#39;interfaccia utente](../ui/record-delete.md) consente di inviare contemporaneamente 10.000 ID. Il metodo API per eliminare i record consente di inviare contemporaneamente 100.000 ID.<br>È consigliabile inviare il maggior numero possibile di ID per richiesta, fino al limite di ID. Quando intendi eliminare un volume elevato di ID, devi evitare di inviare un volume basso o un singolo ID per richiesta di cancellazione del record.

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

Dopo aver [creato una richiesta di eliminazione record](#create), puoi controllarne lo stato utilizzando una richiesta GET.

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
