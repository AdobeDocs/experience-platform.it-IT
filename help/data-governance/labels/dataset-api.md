---
keywords: Experience Platform;home;argomenti popolari;dataset api;gestire l'utilizzo dei dati;api utilizzo dati
solution: Experience Platform
title: Gestire le etichette di utilizzo dei dati per i set di dati utilizzando le API
description: L’API Servizio set di dati consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte delle funzionalità del catalogo dati di Adobe Experience Platform, ma è separata dall’API Catalog Service che gestisce i metadati dei set di dati.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 319bcc742b09f979cd744c8d66f032886427ea9e
workflow-type: tm+mt
source-wordcount: '1318'
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

Puoi applicare un set di etichette per un intero set di dati fornendole nel payload di una richiesta POST o PUT a [!DNL Dataset Service] API. Il corpo della richiesta è lo stesso per entrambe le chiamate. Non è possibile aggiungere etichette ai singoli campi del set di dati.

**Formato API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | L&#39;unico `id` valore del set di dati per il quale si stanno creando le etichette. |

**Richiesta**

L’esempio di richiesta POST seguente aggiorna l’intero set di dati con un `C1` etichetta. I campi forniti nel payload sono gli stessi richiesti per una richiesta PUT.

Quando si eseguono chiamate API che aggiornano le etichette esistenti di un set di dati (PUT), un’ `If-Match` deve essere inclusa l’intestazione che indica la versione corrente dell’entità etichetta set di dati in Dataset Service. Al fine di evitare conflitti di dati, il servizio aggiorna l’entità set di dati solo se il `If-Match` string corrisponde all’ultimo tag di versione generato dal sistema per tale set di dati.

>[!NOTE]
>
>Se attualmente esistono etichette per il set di dati in questione, è possibile aggiungere nuove etichette solo tramite una richiesta PUT, che richiede un `If-Match` intestazione. Una volta aggiunte le etichette a un set di dati, viene `etag` per aggiornare o rimuovere le etichette in un secondo momento<br>Prima di eseguire il metodo PUT, è necessario eseguire una richiesta GET sulle etichette dei set di dati. Assicurati di aggiornare solo i campi specifici destinati alla modifica nella richiesta, lasciando invariati gli altri. Inoltre, assicurati che la chiamata PUT mantenga le stesse entità principali della chiamata GET. Qualsiasi discrepanza genererebbe un errore per il cliente.

Per recuperare la versione più recente dell’entità etichetta del set di dati, esegui una [richiesta GET](#look-up) al `/datasets/{DATASET_ID}/labels` endpoint. Il valore corrente viene restituito nella risposta in un `etag` intestazione. Quando si aggiornano le etichette dei set di dati esistenti, si consiglia di eseguire prima una richiesta di ricerca per il set di dati per recuperarne l’ultima `etag` valore prima di utilizzare tale valore in `If-Match` dell’intestazione della richiesta PUT successiva.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "entityId": {
          "namespace": "AEP",
          "id": "test-ds-id",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": [
            {
              "id": "_ddgduleint.schemas.4a95cdba7d560e3bca7d8c5c7b58f00ca543e2bb1e4137d6",
              "type": "schema",
              "namespace": "AEP"
            }
        ]
      } '
```

| Proprietà | Descrizione |
| --- | --- |
| `entityId` | Questo identifica l’entità del set di dati specifico da aggiornare. |
| `entityId.namespace` | Viene utilizzato per evitare conflitti tra ID. Il `namespace` è `AEP`. |
| `entityId.id` | ID della risorsa da aggiornare. Questo si riferisce al `datasetId`. |
| `entityId.type` | Tipo della risorsa da aggiornare. Questo sarà sempre `dataset`. |
| `labels` | Elenco di etichette di utilizzo dei dati che desideri aggiungere all’intero set di dati. |
| `parents` | Il `parents` contiene un elenco di `entityId`Questo set di dati erediterà le etichette da. I set di dati possono ereditare le etichette da schemi e/o set di dati. |

**Risposta**

In caso di esito positivo, la risposta restituisce il set aggiornato di etichette per il set di dati.

>[!IMPORTANT]
>
>Il `optionalLabels` La proprietà è stata dichiarata obsoleta per l’utilizzo con le richieste POST. Non è più possibile aggiungere etichette dati ai campi del set di dati. Un’operazione POST genera un errore se `optionalLabel` è presente un valore. Tuttavia, puoi eliminare le etichette dai singoli campi utilizzando una richiesta PUT e il `optionalLabels` proprietà. Per ulteriori informazioni, consulta la sezione su [rimozione di etichette da un set di dati](#remove).

```json
{
  "parents": [
      {
        "id": "_ddgduleint.schemas.4a95cdba7d560e3bca7d8c5c7b58f00ca543e2bb1e4137d6",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-201",
  "message": "POST Successful"
} 
```

## Rimuovere le etichette da un set di dati {#remove}

È possibile rimuovere qualsiasi etichetta di campo applicata in precedenza aggiornando la `optionalLabels` valore/i con un sottoinsieme delle etichette di campo esistenti o un elenco vuoto per rimuoverle completamente. Effettuare una richiesta PUT al [!DNL Dataset Service] API per aggiornare o rimuovere le etichette applicate in precedenza.

**Formato API**

```http
PUT /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | L&#39;unico `id` valore del set di dati per il quale si stanno creando le etichette. |

**Richiesta**

Il seguente set di dati su cui viene applicata l’operazione PUT aveva C1 optionalLabel sul campo properties/person/properties/address e C1, C2 optionalLabels sul campo /properties/person/properties/name/fullName. Dopo l’operazione put, il primo campo non avrà alcuna etichetta (l’etichetta C1 è stata rimossa) e il secondo campo avrà solo l’etichetta C1 (l’etichetta C2 è stata rimossa)

Nell’esempio seguente, viene utilizzata una richiesta PUT per rimuovere le etichette aggiunte ai singoli campi. Prima di presentare la richiesta, il `fullName` il campo aveva `C1` e `C2` etichette applicate e `address` il campo aveva già un `C1` etichetta applicata. La richiesta PUT sostituisce le etichette esistenti `C1, C2` etichette da `fullName` campo con `C1` etichetta che utilizza `optionalLabels.labels` parametro. La richiesta sostituisce anche la `C1` etichetta da `address` con un set vuoto di etichette di campo.

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
        "entityId": {
          "namespace": "AEP",
          "id": "646b814d52e1691c07b41032",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": [],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/name/properties/fullName"
            },
            "labels": [
              "C1"
            ]
          },
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/address"
            },
            "labels": []
          }
        ]
      }'
```

| Parametro | Descrizione |
| --- | --- |
| `entityId` | Questo identifica l’entità del set di dati specifico da aggiornare. Il `entityId` deve includere i tre valori seguenti:<br/><br/>`namespace`: utilizzato per evitare conflitti tra ID. Il `namespace` è `AEP`.<br/>`id`: ID della risorsa da aggiornare. Questo si riferisce al `datasetId`.<br/>`type`: tipo di risorsa da aggiornare. Questo sarà sempre `dataset`. |
| `labels` | Elenco di etichette di utilizzo dei dati che desideri aggiungere all’intero set di dati. |
| `parents` | Il `parents` contiene un elenco di `entityId`Questo set di dati erediterà le etichette da. I set di dati possono ereditare le etichette da schemi e/o set di dati. |
| `optionalLabels` | Questo parametro viene utilizzato per rimuovere le etichette applicate in precedenza a un campo set di dati. Elenco dei singoli campi all’interno del set di dati da cui desideri rimuovere le etichette. Ogni elemento in questo array deve avere le seguenti proprietà: <br/><br/>`option`: oggetto che contiene [!DNL Experience Data Model] (XDM) attributi del campo. Sono necessarie le tre proprietà seguenti:<ul><li><code>id</code>: URI <code>$id</code> valore dello schema associato al campo.</li><li><code>contentType</code>: tipo di contenuto e numero di versione dello schema. Deve assumere la forma di uno dei <a href="../../xdm/api/getting-started.md#accept">Accetta intestazioni</a> per una richiesta di ricerca XDM.</li><li><code>schemaPath</code>: percorso del campo nello schema del set di dati.</li></ul>`labels`: questo valore deve contenere un sottoinsieme delle etichette di campo esistenti applicate o essere vuoto per rimuovere tutte le etichette di campo esistenti. I metodi PUT o POST ora restituiscono un errore se `optionalLabels` il campo contiene etichette nuove o modificate. |

**Risposta**

In caso di esito positivo, la risposta restituisce il set aggiornato di etichette per il set di dati.

```json
{
  "parents": [
      {
        "id": "_xdm.context.identity-graph-flattened-export",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-200",
  "message": "PUT Successful"
} 
```

## Passaggi successivi

Dopo aver letto questo documento, hai imparato a gestire le etichette di utilizzo dei dati per set di dati e campi utilizzando [!DNL Dataset Service] API. Ora puoi definire [criteri di utilizzo dati](../policies/overview.md) e [criteri di controllo dell’accesso](../../access-control/abac/ui/policies.md) in base alle etichette applicate.

Per ulteriori informazioni sulla gestione dei set di dati in [!DNL Experience Platform], vedere [panoramica dei set di dati](../../catalog/datasets/overview.md).
