---
title: Eliminare i record utilizzando l’API di igiene dati
description: Scopri come correggere o eliminare programmaticamente i dati personali memorizzati dai tuoi clienti in Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: d80a4be3-e072-4bb4-a56d-b34a20f88c78
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 3%

---

# Eliminare i record utilizzando l’API di igiene dati

<!-- >[!IMPORTANT]
>
>This endpoint represents the beta functionality for record deletes. For the latest functionality, please use the [`/workorder` endpoint](./workorder.md) instead. -->

L’API di igiene dei dati ti consente di correggere o eliminare programmaticamente i dati personali memorizzati dei tuoi clienti in Adobe Experience Platform.

Puoi accedere all’API attraverso lo stesso percorso principale del [API Privacy Service](../../privacy-service/api/overview.md): `https://platform.adobe.io/data/core/privacy/`

## Introduzione

Questa sezione fornisce un’introduzione ai concetti di base che devi conoscere prima di tentare di effettuare chiamate all’API di igiene dati.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate all’API di igiene dati, devi prima raccogliere le credenziali di autenticazione. Si tratta delle stesse credenziali utilizzate per accedere all’API di Privacy Service. Fai riferimento a [Panoramica API](./overview.md#getting-started) per generare valori per ciascuna delle intestazioni richieste per l’API di igiene dati, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* `Content-Type: application/json`

### Lettura di chiamate API di esempio

Questo documento fornisce un esempio di chiamata API per dimostrare come formattare le richieste. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/api-guide.md#sample-api) nella guida introduttiva per le API di Experience Platform.

## Creare un processo di eliminazione

È possibile creare un processo di eliminazione effettuando una richiesta di POST.

**Formato API**

```http
POST /jobs
```

**Richiesta**

Il payload della richiesta è strutturato in modo simile a quello di un [elimina la richiesta nell’API di Privacy Service](../../privacy-service/api/privacy-jobs.md#access-delete). Include un `users` array i cui oggetti rappresentano gli utenti i cui dati devono essere eliminati.

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
| `companyContexts` | Matrice contenente informazioni di autenticazione per la tua organizzazione. Deve contenere un singolo oggetto con le seguenti proprietà: <ul><li>`namespace`: Deve essere impostato su `imsOrgID`.</li><li>`value`: Il tuo ID organizzazione IMS. Si tratta dello stesso valore fornito nel `x-gw-ims-org-id` intestazione.</li></ul> |
| `users` | Matrice contenente una raccolta di almeno un utente le cui informazioni si desidera eliminare. Ogni oggetto utente contiene le informazioni seguenti: <ul><li>`key`: Identificatore per un utente utilizzato per qualificare gli ID processo separati nei dati di risposta. È consigliabile scegliere una stringa univoca e facilmente identificabile per questo valore in modo che possa essere referenziata o cercata in un secondo momento.</li><li>`action`: Array che elenca le azioni desiderate da eseguire sui dati dell’utente. Deve contenere un singolo valore stringa: `delete`.</li><li>`userIDs`: Una raccolta di identità per l&#39;utente. Il numero di identità che un singolo utente può avere è limitato a nove. Ciascuna identità contiene le seguenti proprietà: <ul><li>`namespace`: La [spazio dei nomi identità](../../identity-service/namespaces.md) associato all&#39;ID. Questo può essere un [spazio dei nomi standard](../../privacy-service/api/appendix.md#standard-namespaces) riconosciuto da Platform oppure può essere uno spazio dei nomi personalizzato definito dall’organizzazione. Il tipo di spazio dei nomi utilizzato deve riflettersi nel `type` proprietà.</li><li>`value`: Il valore di identità.</li><li>`type`: Deve essere impostato su `standard` se si utilizza uno spazio dei nomi riconosciuto a livello globale, oppure `custom` se utilizzi uno spazio dei nomi definito dall’organizzazione.</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli dei processi creati.

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
