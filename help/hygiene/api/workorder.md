---
title: Endpoint API ordine di lavoro
description: L’endpoint /workorder nell’API di igiene dati ti consente di gestire in modo programmatico le attività di eliminazione per le identità dei consumatori.
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
hide: true
hidefromtoc: true
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 5%

---

# Endpoint ordine di lavoro

>[!IMPORTANT]
>
>Le funzionalità di igiene dei dati in Adobe Experience Platform sono attualmente disponibili solo per le organizzazioni che hanno acquistato Healthcare Shield.

La `/workorder` L’endpoint nell’API di igiene dati ti consente di gestire in modo programmatico le attività di eliminazione per le identità dei consumatori in Adobe Experience Platform.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’API di igiene dei dati. Prima di continuare, controlla la [panoramica](./overview.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e importanti informazioni sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Elimina identità {#delete-identities}

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
| `action` | L&#39;azione da eseguire. Il valore deve essere impostato su `delete_identity` quando si eliminano le identità. |
| `datasetId` | Se esegui l’eliminazione da un singolo set di dati, questo valore deve essere l’ID del set di dati in questione. Se si esegue l&#39;eliminazione da tutti i set di dati, impostare il valore su `ALL`.<br><br>Se specifichi un singolo set di dati, lo schema Experience Data Model (XDM) associato al set di dati deve avere un&#39;identità primaria definita. |
| `identities` | Matrice contenente le identità di almeno un utente le cui informazioni si desidera eliminare. Ogni identità è composta da un [spazio dei nomi identità](../../identity-service/namespaces.md) e un valore:<ul><li>`namespace`: Contiene una singola proprietà stringa, `code`, che rappresenta lo spazio dei nomi Identity. </li><li>`id`: Il valore di identità.</ul>Se `datasetId` specifica un singolo set di dati, ogni entità in `identities` deve utilizzare lo stesso spazio dei nomi di identità dell&#39;identità principale dello schema.<br><br>Se `datasetId` è impostato su `ALL`, `identities` array non è vincolata ad alcun singolo spazio dei nomi, in quanto ogni set di dati potrebbe essere diverso. Tuttavia, le richieste sono ancora vincolate dai namespace disponibili per la tua organizzazione, come segnalato da [Servizio identità](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli dell&#39;eliminazione dell&#39;identità.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "batchId": "fc0cf8af-a176-4107-a31a-381d6af38cbe",
  "bundleOrdinal": 1,
  "payloadByteSize": 362,
  "operationCount": 3,
  "createdAt": 1652122493242,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `workorderId` | ID dell&#39;ordine di eliminazione. Può essere utilizzato per cercare lo stato dell’eliminazione in un secondo momento. |
| `orgId` | L&#39;ID della tua organizzazione. |
| `batchId` | ID del batch a cui è associato questo ordine di eliminazione, utilizzato a scopo di debug. Più ordini di eliminazione vengono raggruppati in un batch che deve essere elaborato dai servizi a valle. |
| `bundleOrdinal` | Ordine in cui l&#39;ordine di eliminazione è stato ricevuto quando è stato raggruppato in un batch per l&#39;elaborazione a valle. Utilizzato a scopo di debug. |
| `payloadByteSize` | La dimensione, in byte, dell&#39;elenco di identità fornite nel payload della richiesta che ha creato questo ordine di eliminazione. |
| `operationCount` | Numero di identità a cui si applica questo ordine di eliminazione. |
| `createdAt` | Una marca temporale di quando è stato creato l&#39;ordine di eliminazione. |
| `responseMessage` | Risposta più recente restituita dal sistema. Se si verifica un errore durante l’elaborazione, questo valore sarà una stringa JSON contenente informazioni dettagliate sull’errore che consentono di comprendere cosa potrebbe essere andato storto. |
| `status` | Lo stato corrente dell&#39;ordine di eliminazione. |
| `createdBy` | Utente che ha creato l&#39;ordine di eliminazione. |

{style=&quot;table-layout:auto&quot;}

## Elencare gli stati di tutte le eliminazioni di identità {#list}

È possibile elencare gli stati di tutte le eliminazioni di identità effettuando una richiesta GET.

**Formato API**

```http
GET /workorder?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUERY_PARAMS}` | Elenco di parametri di query facoltativi per la chiamata di elenco, con più parametri separati da `&` caratteri. I parametri di query accettati sono i seguenti:<ul><li>`data` - Un valore booleano che, se impostato su `true`, include tutti i dati di richiesta e risposta aggiuntivi ricevuti per l’ordine di eliminazione. Predefinito su `false`.</li><li>`start` - Una marca temporale per l&#39;inizio dell&#39;intervallo temporale per la ricerca di ordini di eliminazione.</li><li>`end` - Una marca temporale per la fine dell&#39;intervallo temporale per la ricerca di ordini di eliminazione.</li><li>`page` - La pagina di risposta specifica da restituire.</li><li>`limit` - Il numero di record da visualizzare per pagina.</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli di tutte le operazioni di eliminazione, incluso lo stato corrente. La risposta di esempio seguente è stata troncata per motivi di spazio.

```json
{
  "results": [
    {
      "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
      "orgId": "{ORG_ID}",
      "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650929265295,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    },
    {
      "workorderId": "e4a662e8-a5f3-497d-8d6a-d26970d8732b",
      "orgId": "{ORG_ID}",
      "batchId": "74fe4e38-ed42-4ca5-8bee-88bdc03ae786",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650931057899,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    }
  ],
  "total": 200,
  "count": 50,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=50",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `results` | Contiene l’elenco degli ordini di eliminazione e i relativi dettagli. Per ulteriori informazioni sulle proprietà di un ordine di eliminazione, consulta la risposta di esempio nella sezione su [ricerca di un ordine di eliminazione](#lookup). |
| `total` | Numero totale di ordini di eliminazione rilevati in base ai filtri correnti. |
| `count` | Numero totale di ordini di eliminazione trovati su ogni pagina della risposta. |
| `_links` | Contiene informazioni sull’impaginazione per consentirti di esplorare il resto della risposta:<ul><li>`next`: Contiene un URL per la pagina successiva nella risposta.</li><li>`page`: Contiene un modello URL per accedere a un’altra pagina della risposta o per regolare il numero di elementi restituiti su ciascuna pagina.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Recupera lo stato di un’eliminazione dell’identità (#lookup)

Dopo aver inviato una richiesta a [eliminare un&#39;identità](#delete-identities), puoi controllarne lo stato utilizzando una richiesta GET.

**Formato API**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{WORK_ORDER_ID}` | La `workorderId` dell&#39;eliminazione dell&#39;identità che stai cercando. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/ID6c28e2d2d2b54079aadf7be94568f6d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli dell’operazione di eliminazione, incluso lo stato corrente.

```json
{
  "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
  "orgId": "{ORG_ID}",
  "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
  "bundleOrdinal": 1,
  "payloadByteSize": 164,
  "operationCount": 1,
  "createdAt": 1650929265295,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `workorderId` | ID dell&#39;ordine di eliminazione. Può essere utilizzato per cercare lo stato dell’eliminazione in un secondo momento. |
| `orgId` | L&#39;ID della tua organizzazione. |
| `batchId` | ID del batch a cui è associato questo ordine di eliminazione, utilizzato a scopo di debug. Più ordini di eliminazione vengono raggruppati in un batch che deve essere elaborato dai servizi a valle. |
| `bundleOrdinal` | Ordine in cui l&#39;ordine di eliminazione è stato ricevuto quando è stato raggruppato in un batch per l&#39;elaborazione a valle. Utilizzato a scopo di debug. |
| `payloadByteSize` | La dimensione, in byte, dell&#39;elenco di identità fornite nel payload della richiesta che ha creato questo ordine di eliminazione. |
| `operationCount` | Numero di identità a cui si applica questo ordine di eliminazione. |
| `createdAt` | Una marca temporale di quando è stato creato l&#39;ordine di eliminazione. |
| `responseMessage` | Risposta più recente restituita dal sistema. Se si verifica un errore durante l’elaborazione, questo valore sarà una stringa JSON contenente informazioni dettagliate sull’errore che consentono di comprendere cosa potrebbe essere andato storto. |
| `status` | Lo stato corrente dell&#39;ordine di eliminazione. |
| `createdBy` | Utente che ha creato l&#39;ordine di eliminazione. |
