---
keywords: Experience Platform;home;argomenti popolari;dataset api;gestire l'utilizzo dei dati;api utilizzo dati
solution: Experience Platform
title: Gestire le etichette di utilizzo dei dati per i set di dati utilizzando le API
description: L’API Servizio set di dati consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte delle funzionalità del catalogo dati di Adobe Experience Platform, ma è separata dall’API Catalog Service che gestisce i metadati dei set di dati.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 2%

---

# Gestire le etichette di utilizzo dei dati per i set di dati utilizzando le API

Il [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte delle funzionalità del catalogo dati di Adobe Experience Platform, ma è separata dal [!DNL Catalog Service] API per la gestione dei metadati del set di dati.

>[!IMPORTANT]
>
>L’applicazione di etichette a livello di set di dati è supportata solo per i casi di utilizzo di governance dei dati. Se si desidera creare criteri di accesso per i dati, è necessario [applica etichette allo schema](../../xdm/tutorials/labels.md) su cui si basa il set di dati. Consulta la panoramica su [controllo degli accessi basato su attributi](../../access-control/abac/overview.md) per ulteriori informazioni.

Questo documento illustra come gestire le etichette per set di dati e campi utilizzando [!DNL Dataset Service API]. Per i passaggi su come gestire autonomamente le etichette di utilizzo dei dati utilizzando le chiamate API, consulta [guida dell’endpoint &quot;labels&quot;](../api/labels.md) per [!DNL Policy Service API].

## Introduzione

Prima di leggere questa guida, segui i passaggi descritti in [sezione introduttiva](../../catalog/api/getting-started.md) nella guida per gli sviluppatori di Catalog per raccogliere le credenziali necessarie per effettuare chiamate a [!DNL Platform] API.

Per poter effettuare chiamate agli endpoint descritti in questo documento, è necessario disporre dell’univoco `id` per un set di dati specifico. In caso contrario, consulta la guida su [elenco degli oggetti catalogo](../../catalog/api/list-objects.md) per trovare gli ID dei set di dati esistenti.

## Cercare etichette per un set di dati {#look-up}

Per cercare le etichette di utilizzo dei dati applicate a un set di dati esistente, devi effettuare una richiesta GET al [!DNL Dataset Service] API.

**Formato API**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | L&#39;unico `id` valore del set di dati di cui desideri cercare le etichette. |

**Richiesta**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce le etichette di utilizzo dei dati applicate al set di dati.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{ORG_ID}",
    "labels": [ "C1", "C2", "C3", "I1", "I2" ],
    "optionalLabels": [
      {
        "option": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
          "contentType": "application/vnd.adobe.xed-full+json;version=1",
          "schemaPath": "/properties/repositoryCreatedBy"
        },
        "labels": [ "S1", "S2" ]
      }
    ]
  }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `labels` | Elenco di etichette di utilizzo dei dati applicate al set di dati. |
| `optionalLabels` | Elenco di singoli campi all’interno del set di dati a cui sono applicate etichette di utilizzo dei dati. |

## Applicare etichette a un set di dati {#apply}

Puoi creare un set di etichette per un set di dati fornendole nel payload di una richiesta POST o PUT al [!DNL Dataset Service] API. L’utilizzo di uno di questi metodi sovrascrive tutte le etichette esistenti e le sostituisce con quelle fornite nel payload.

**Formato API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | L&#39;unico `id` valore del set di dati per il quale si stanno creando le etichette. |

**Richiesta**

La richiesta PUT di esempio seguente aggiorna le etichette esistenti per un set di dati, nonché un campo specifico all’interno di tale set di dati. I campi forniti nel payload sono gli stessi richiesti per una richiesta POST.

Quando si eseguono chiamate API che aggiornano le etichette esistenti di un set di dati (PUT), un’ `If-Match` deve essere inclusa l’intestazione che indica la versione corrente dell’entità etichetta set di dati in Dataset Service. Al fine di evitare conflitti di dati, il servizio aggiorna l’entità set di dati solo se il `If-Match` string corrisponde all’ultimo tag di versione generato dal sistema per tale set di dati.

>[!NOTE]
>
>Se attualmente non esistono etichette per il set di dati in questione, è possibile aggiungere nuove etichette solo tramite una richiesta POST, che non richiede un’ `If-Match` intestazione. Una volta aggiunte le etichette a un set di dati, viene `etag` viene assegnato un valore che può essere utilizzato per aggiornare o rimuovere le etichette in un secondo momento.

Per recuperare la versione più recente dell’entità etichetta del set di dati, esegui una [richiesta GET](#look-up) al `/datasets/{DATASET_ID}/labels` endpoint. Il valore corrente viene restituito nella risposta in un `etag` intestazione. Quando si aggiornano le etichette dei set di dati esistenti, si consiglia di eseguire prima una richiesta di ricerca per il set di dati per recuperarne l’ultima `etag` valore prima di utilizzare tale valore in `If-Match` dell’intestazione della richiesta PUT successiva.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000' \
  -d '{
        "labels": [ "C1", "C2", "C3", "I1", "I2" ],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/repositoryCreatedBy"
            },
            "labels": [ "S1", "S2" ]
          }
        ]
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `labels` | Elenco di etichette di utilizzo dei dati che desideri aggiungere al set di dati. |
| `optionalLabels` | Elenco dei singoli campi all’interno del set di dati a cui desideri aggiungere etichette. Ogni elemento in questo array deve avere le seguenti proprietà: <br/><br/>`option`: oggetto che contiene [!DNL Experience Data Model] (XDM) attributi del campo. Sono necessarie le tre proprietà seguenti:<ul><li>id</code>: URI $id</code> valore dello schema associato al campo.</li><li>contentType</code>: tipo di contenuto e numero di versione dello schema. Deve assumere la forma di uno dei <a href="../../xdm/api/getting-started.md#accept">Accetta intestazioni</a> per una richiesta di ricerca XDM.</li><li>schemaPath</code>: percorso del campo nello schema del set di dati.</li></ul>`labels`: elenco di etichette di utilizzo dei dati che desideri aggiungere al campo. |

**Risposta**

In caso di esito positivo, la risposta restituisce il set aggiornato di etichette per il set di dati.

```json
{
  "labels": [ "C1", "C2", "C3", "I1", "I2" ],
  "optionalLabels": [
    {
      "option": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
        "contentType": "application/vnd.adobe.xed-full+json;version=1",
        "schemaPath": "/properties/repositoryCreatedBy"
      },
      "labels": [ "S1", "S2" ]
    }
  ]
}
```

## Passaggi successivi

Dopo aver letto questo documento, hai imparato a gestire le etichette di utilizzo dei dati per set di dati e campi utilizzando [!DNL Dataset Service] API. Ora puoi definire [criteri di utilizzo dati](../policies/overview.md) e [criteri di controllo dell’accesso](../../access-control/abac/ui/policies.md) in base alle etichette applicate.

Per ulteriori informazioni sulla gestione dei set di dati in [!DNL Experience Platform], vedere [panoramica dei set di dati](../../catalog/datasets/overview.md).
