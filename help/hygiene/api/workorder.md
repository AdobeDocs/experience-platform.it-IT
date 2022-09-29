---
title: Endpoint API ordine di lavoro
description: L’endpoint /workorder nell’API di igiene dati ti consente di gestire in modo programmatico le attività di eliminazione per le identità dei consumatori.
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: e4cc78591d0d3b4abd660956b1263092697d63d5
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 5%

---

# Endpoint ordine di lavoro

>[!IMPORTANT]
>
>Le funzionalità di igiene dei dati in Adobe Experience Platform sono attualmente disponibili solo per le organizzazioni che hanno acquistato Adobe Healthcare Shield o Privacy Shield.

La `/workorder` L’endpoint nell’API di igiene dati ti consente di gestire in modo programmatico le richieste di cancellazione del consumatore in Adobe Experience Platform.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’API di igiene dei dati. Prima di continuare, controlla la [panoramica](./overview.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e importanti informazioni sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Creare una richiesta di cancellazione del consumatore {#delete-consumers}

Puoi eliminare una o più identità di un consumatore da un singolo set di dati o da tutti i set di dati effettuando una richiesta di POST al `/workorder` punto finale.

**Formato API**

```http
POST /workorder
```

**Richiesta**

A seconda del valore del `datasetId` fornito nel payload della richiesta, la chiamata API eliminerà le identità dei consumatori da tutti i set di dati o da un singolo set di dati specificato. La richiesta seguente elimina tre identità di consumatore da un set di dati specifico.

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
        "displayName": "Example Consumer Delete Request",
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
| `action` | L&#39;azione da eseguire. Il valore deve essere impostato su `delete_identity` per le cancellazioni dal consumatore. |
| `datasetId` | Se esegui l’eliminazione da un singolo set di dati, questo valore deve essere l’ID del set di dati in questione. Se si esegue l&#39;eliminazione da tutti i set di dati, impostare il valore su `ALL`.<br><br>Se specifichi un singolo set di dati, lo schema Experience Data Model (XDM) associato al set di dati deve avere un&#39;identità primaria definita. |
| `displayName` | Nome visualizzato della richiesta di cancellazione del consumatore. |
| `description` | Una descrizione della richiesta di cancellazione del consumatore. |
| `identities` | Matrice contenente le identità di almeno un utente le cui informazioni si desidera eliminare. Ogni identità è composta da un [spazio dei nomi identità](../../identity-service/namespaces.md) e un valore:<ul><li>`namespace`: Contiene una singola proprietà stringa, `code`, che rappresenta lo spazio dei nomi Identity. </li><li>`id`: Il valore di identità.</ul>Se `datasetId` specifica un singolo set di dati, ogni entità in `identities` deve utilizzare lo stesso spazio dei nomi di identità dell&#39;identità principale dello schema.<br><br>Se `datasetId` è impostato su `ALL`, `identities` array non è vincolata ad alcun singolo spazio dei nomi, in quanto ogni set di dati potrebbe essere diverso. Tuttavia, le richieste sono ancora vincolate dai namespace disponibili per la tua organizzazione, come segnalato da [Servizio identità](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli dell’eliminazione del consumatore.

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
  "displayName": "Example Consumer Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| Proprietà | Descrizione |
| --- | --- |
| `workorderId` | ID dell&#39;ordine di eliminazione. Può essere utilizzato per cercare lo stato dell’eliminazione in un secondo momento. |
| `orgId` | L&#39;ID organizzazione. |
| `bundleId` | ID del bundle a cui è associato questo ordine di eliminazione, utilizzato a scopo di debug. Più ordini di eliminazione sono raggruppati per essere elaborati dai servizi a valle. |
| `action` | L&#39;azione eseguita dall&#39;ordine di lavoro. Per le cancellazioni dal consumatore, il valore è `identity-delete`. |
| `createdAt` | Una marca temporale di quando è stato creato l&#39;ordine di eliminazione. |
| `updatedAt` | Timestamp dell&#39;ultimo aggiornamento dell&#39;ordine di eliminazione. |
| `status` | Lo stato corrente dell&#39;ordine di eliminazione. |
| `createdBy` | Utente che ha creato l&#39;ordine di eliminazione. |
| `datasetId` | ID del set di dati soggetto alla richiesta. Se la richiesta è per tutti i set di dati, il valore verrà impostato su `ALL`. |

{style=&quot;table-layout:auto&quot;}

## Recuperare lo stato di una cancellazione del consumatore (#lookup)

Dopo [creazione di una richiesta di cancellazione del consumatore](#delete-consumers), puoi controllarne lo stato utilizzando una richiesta GET.

**Formato API**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{WORK_ORDER_ID}` | La `workorderId` della cancellazione del consumatore che stai cercando. |

{style=&quot;table-layout:auto&quot;}

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

Una risposta corretta restituisce i dettagli dell’operazione di eliminazione, incluso lo stato corrente.

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
  "displayName": "Example Consumer Delete Request",
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
| `workorderId` | ID dell&#39;ordine di eliminazione. Può essere utilizzato per cercare lo stato dell’eliminazione in un secondo momento. |
| `orgId` | L&#39;ID organizzazione. |
| `bundleId` | ID del bundle a cui è associato questo ordine di eliminazione, utilizzato a scopo di debug. Più ordini di eliminazione sono raggruppati per essere elaborati dai servizi a valle. |
| `action` | L&#39;azione eseguita dall&#39;ordine di lavoro. Per le cancellazioni dal consumatore, il valore è `identity-delete`. |
| `createdAt` | Una marca temporale di quando è stato creato l&#39;ordine di eliminazione. |
| `updatedAt` | Timestamp dell&#39;ultimo aggiornamento dell&#39;ordine di eliminazione. |
| `status` | Lo stato corrente dell&#39;ordine di eliminazione. |
| `createdBy` | Utente che ha creato l&#39;ordine di eliminazione. |
| `datasetId` | ID del set di dati soggetto alla richiesta. Se la richiesta è per tutti i set di dati, il valore verrà impostato su `ALL`. |
| `productStatusDetails` | Matrice che elenca lo stato corrente dei processi a valle relativi alla richiesta. Ogni oggetto array contiene le seguenti proprietà:<ul><li>`productName`: Nome del servizio a valle.</li><li>`productStatus`: Lo stato attuale di elaborazione della richiesta del servizio a valle.</li><li>`createdAt`: Una marca temporale di quando il servizio ha pubblicato lo stato più recente.</li></ul> |

## Aggiornare una richiesta di cancellazione del consumatore

È possibile aggiornare `displayName` e `description` per eliminare un consumatore effettuando una richiesta di PUT.

**Formato API**

```http
PUT /workorder{WORK_ORDER_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{WORK_ORDER_ID}` | La `workorderId` della cancellazione del consumatore che stai cercando. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X GET \
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
| `displayName` | Nome visualizzato aggiornato per la richiesta di cancellazione del consumatore. |
| `description` | Una descrizione aggiornata per la richiesta di cancellazione del consumatore. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli dell’eliminazione del consumatore.

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
  "displayName" : "Update - displayName",
  "description" : "Update - description",
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
| `workorderId` | ID dell&#39;ordine di eliminazione. Può essere utilizzato per cercare lo stato dell’eliminazione in un secondo momento. |
| `orgId` | L&#39;ID organizzazione. |
| `bundleId` | ID del bundle a cui è associato questo ordine di eliminazione, utilizzato a scopo di debug. Più ordini di eliminazione sono raggruppati per essere elaborati dai servizi a valle. |
| `action` | L&#39;azione eseguita dall&#39;ordine di lavoro. Per le cancellazioni dal consumatore, il valore è `identity-delete`. |
| `createdAt` | Una marca temporale di quando è stato creato l&#39;ordine di eliminazione. |
| `updatedAt` | Timestamp dell&#39;ultimo aggiornamento dell&#39;ordine di eliminazione. |
| `status` | Lo stato corrente dell&#39;ordine di eliminazione. |
| `createdBy` | Utente che ha creato l&#39;ordine di eliminazione. |
| `datasetId` | ID del set di dati soggetto alla richiesta. Se la richiesta è per tutti i set di dati, il valore verrà impostato su `ALL`. |
| `productStatusDetails` | Matrice che elenca lo stato corrente dei processi a valle relativi alla richiesta. Ogni oggetto array contiene le seguenti proprietà:<ul><li>`productName`: Nome del servizio a valle.</li><li>`productStatus`: Lo stato attuale di elaborazione della richiesta del servizio a valle.</li><li>`createdAt`: Una marca temporale di quando il servizio ha pubblicato lo stato più recente.</li></ul> |

{style=&quot;table-layout:auto&quot;}
