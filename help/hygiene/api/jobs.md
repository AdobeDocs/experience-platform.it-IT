---
title: Eliminare i record utilizzando l’API di igiene dei dati
description: Scopri come correggere o eliminare in modo programmatico i dati personali memorizzati dai clienti in Adobe Experience Platform.
role: Developer
hide: true
hidefromtoc: true
exl-id: d80a4be3-e072-4bb4-a56d-b34a20f88c78
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 6%

---

# Eliminare i record utilizzando l’API di igiene dei dati

<!-- >[!IMPORTANT]
>
>This endpoint represents the beta functionality for record deletes. For the latest functionality, please use the [`/workorder` endpoint](./workorder.md) instead. -->

L’API di igiene dei dati consente di correggere o eliminare in modo programmatico i dati personali memorizzati dai clienti in Adobe Experience Platform.

Puoi accedere all&#39;API tramite lo stesso percorso radice dell&#39;[API Privacy Service](../../privacy-service/api/overview.md): `https://platform.adobe.io/data/core/privacy/`

## Introduzione

Questa sezione fornisce un’introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all’API di igiene dei dati.

### Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate all’API di igiene dei dati, devi prima raccogliere le credenziali di autenticazione. Si tratta delle stesse credenziali utilizzate per accedere all’API Privacy Service. Consulta la [panoramica API](./overview.md#getting-started) per generare valori per ciascuna delle intestazioni richieste per l&#39;API di igiene dei dati, come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* `Content-Type: application/json`

### Lettura delle chiamate API di esempio

Questo documento fornisce un esempio di chiamata API per dimostrare come formattare le richieste. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/api-guide.md#sample-api) nella guida introduttiva per le API di Experience Platform.

## Creare un processo di eliminazione

Per creare un processo di eliminazione, devi eseguire una richiesta POST.

**Formato API**

```http
POST /jobs
```

**Richiesta**

Il payload della richiesta è strutturato in modo simile a quello di una richiesta [delete nell&#39;API Privacy Service](../../privacy-service/api/privacy-jobs.md#access-delete). Include un array `users` i cui oggetti rappresentano gli utenti i cui dati devono essere eliminati.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "companyContexts": [
          {
            "namespace": "imsOrgID",
            "value": "{ORG_ID}"
          }
        ],
        "users": [
          {
            "key": "John Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "email",
                "value": "johnd@example.com",
                "type": "standard",
              },
              {
                "namespace": "ECID",
                "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
                "type": "standard"
              }
            ]
          },
          {
            "key": "Jane Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "Loyalty ID",
                "value": "30583967185734",
                "type": "custom"
              }
            ]
          }
        ]
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `companyContexts` | Array contenente le informazioni di autenticazione per l’organizzazione. Deve contenere un singolo oggetto con le seguenti proprietà: <ul><li>`namespace`: deve essere impostato su `imsOrgID`.</li><li>`value`: ID organizzazione. È lo stesso valore fornito nell&#39;intestazione `x-gw-ims-org-id`.</li></ul> |
| `users` | Matrice contenente una raccolta di almeno un utente di cui si desidera eliminare le informazioni. Ogni oggetto utente contiene le seguenti informazioni: <ul><li>`key`: identificatore di un utente utilizzato per qualificare gli ID di processo separati nei dati di risposta. È consigliabile scegliere una stringa univoca e facilmente identificabile per questo valore, in modo che sia possibile farvi riferimento o cercarlo in un secondo momento.</li><li>`action`: array che elenca le azioni desiderate da eseguire sui dati dell&#39;utente. Deve contenere un singolo valore stringa: `delete`.</li><li>`userIDs`: raccolta di identità per l&#39;utente. Il numero di identità che un singolo utente può avere è limitato a nove. Ogni identità contiene le seguenti proprietà: <ul><li>`namespace`: [spazio dei nomi identità](../../identity-service/features/namespaces.md) associato all&#39;ID. Può trattarsi di uno spazio dei nomi [standard](../../privacy-service/api/appendix.md#standard-namespaces) riconosciuto da Platform oppure di uno spazio dei nomi personalizzato definito dall&#39;organizzazione. Il tipo di spazio dei nomi utilizzato deve essere riflesso nella proprietà `type`.</li><li>`value`: valore di identità.</li><li>`type`: deve essere impostato su `standard` se si utilizza uno spazio dei nomi riconosciuto a livello globale oppure su `custom` se si utilizza uno spazio dei nomi definito dall&#39;organizzazione.</li></ul></li></ul> |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli dei processi creati.

```json
{
  "requestId": "16318094870430026RX-334",
  "totalRecords": 2,
  "jobs": [
    {
      "jobId": "c9b5fd82-db14-4c27-8bec-64a06e1fbda4",
      "customer": {
        "user": {
          "key": "John Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "email",
              "value": "johnd@example.com",
              "type": "standard",
              "namespaceId": 6,
              "isDeletedClientSide": false
            },
            {
              "namespace": "ECID",
              "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
              "type": "standard",
              "namespaceId": 4,
              "isDeletedClientSide": false
            }
          ]
        }
      }
    },
    {
      "jobId": "8ddc8e73-cecc-4be3-ae44-cdba127f7c70",
      "customer": {
        "user": {
          "key": "Jane Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "Loyalty ID",
              "value": "30583967185734",
              "type": "custom",
              "isDeletedClientSide": false
            }
          ]
        }
      }
    }
  ]
}
```
