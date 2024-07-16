---
keywords: Experience Platform;home;argomenti popolari;dataset api;gestire l'utilizzo dei dati;api utilizzo dati
solution: Experience Platform
title: Gestire le etichette di utilizzo dei dati per i set di dati utilizzando le API
description: L’API Servizio set di dati consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte delle funzionalità del catalogo dati di Adobe Experience Platform, ma è separata dall’API Catalog Service che gestisce i metadati dei set di dati.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 8db484e4a65516058d701ca972fcbcb6b73abb31
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 2%

---

# Gestire le etichette di utilizzo dei dati per i set di dati utilizzando le API

[[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte delle funzionalità del catalogo dati di Adobe Experience Platform, ma è separata dall&#39;API [!DNL Catalog Service] che gestisce i metadati del set di dati.

>[!IMPORTANT]
>
>L’applicazione di etichette a livello di set di dati è supportata solo per i casi di utilizzo di governance dei dati. Se si tenta di creare criteri di accesso per i dati, è necessario [applicare etichette allo schema](../../xdm/tutorials/labels.md) su cui si basa il set di dati. Per ulteriori informazioni, consulta la panoramica sul controllo degli accessi basato su [attributi](../../access-control/abac/overview.md).

Questo documento illustra come gestire le etichette per set di dati e campi utilizzando [!DNL Dataset Service API]. Per i passaggi su come gestire autonomamente le etichette di utilizzo dei dati tramite chiamate API, consulta la [guida dell&#39;endpoint delle etichette](../api/labels.md) per [!DNL Policy Service API].

## Introduzione

Prima di leggere questa guida, segui i passaggi descritti nella [sezione introduttiva](../../catalog/api/getting-started.md) nella guida per sviluppatori di Catalog per raccogliere le credenziali necessarie per effettuare chiamate alle API [!DNL Platform].

Per effettuare chiamate agli endpoint descritti in questo documento, è necessario disporre del valore `id` univoco per un set di dati specifico. Se non disponi di questo valore, consulta la guida in [elenco di oggetti Catalog](../../catalog/api/list-objects.md) per trovare gli ID dei set di dati esistenti.

## Cercare etichette per un set di dati {#look-up}

Per cercare le etichette di utilizzo dei dati applicate a un set di dati esistente, effettuare una richiesta GET all&#39;API [!DNL Dataset Service].

**Formato API**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | Valore `id` univoco del set di dati di cui si desidera cercare le etichette. |

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

È possibile applicare un set di etichette per un intero set di dati fornendole nel payload di una richiesta POST o PUT all&#39;API [!DNL Dataset Service]. Il corpo della richiesta è lo stesso per entrambe le chiamate. Non è possibile aggiungere etichette ai singoli campi del set di dati.

**Formato API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | Valore `id` univoco del set di dati per il quale si stanno creando le etichette. |

**Richiesta**

La richiesta POST di esempio seguente aggiorna l&#39;intero set di dati con un&#39;etichetta `C1`. I campi forniti nel payload sono gli stessi richiesti per una richiesta PUT.

Quando si eseguono chiamate API che aggiornano le etichette esistenti di un set di dati (PUT), è necessario includere un&#39;intestazione `If-Match` che indica la versione corrente dell&#39;entità etichetta del set di dati in Dataset Service. Per evitare conflitti di dati, il servizio aggiorna l&#39;entità set di dati solo se la stringa `If-Match` inclusa corrisponde all&#39;ultimo tag di versione generato dal sistema per tale set di dati.

>[!NOTE]
>
>Se esistono etichette per il set di dati in questione, è possibile aggiungere nuove etichette solo tramite una richiesta PUT, che richiede un&#39;intestazione `If-Match`. Dopo aver aggiunto le etichette a un set di dati, è necessario specificare il valore `etag` più recente per aggiornare o rimuovere le etichette in un secondo momento<br>Prima di eseguire il metodo PUT, è necessario eseguire una richiesta GET sulle etichette del set di dati. Assicurati di aggiornare solo i campi specifici destinati alla modifica nella richiesta, lasciando invariati gli altri. Inoltre, assicurati che la chiamata PUT mantenga le stesse entità principali della chiamata GET. Qualsiasi discrepanza genererebbe un errore per il cliente.

Per recuperare la versione più recente dell&#39;entità etichetta del set di dati, eseguire una [richiesta di GET](#look-up) all&#39;endpoint `/datasets/{DATASET_ID}/labels`. Il valore corrente viene restituito nella risposta sotto un&#39;intestazione `etag`. Quando si aggiornano le etichette dei set di dati esistenti, è consigliabile eseguire prima una richiesta di ricerca per il set di dati per recuperare il valore `etag` più recente prima di utilizzare tale valore nell&#39;intestazione `If-Match` della richiesta PUT successiva.

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
        "parents": []
      } '
```

| Proprietà | Descrizione |
| --- | --- |
| `entityId` | Questo identifica l’entità del set di dati specifico da aggiornare. |
| `entityId.namespace` | Viene utilizzato per evitare conflitti tra ID. `namespace` è `AEP`. |
| `entityId.id` | ID della risorsa da aggiornare. Si riferisce a `datasetId`. |
| `entityId.type` | Tipo della risorsa da aggiornare. Questo sarà sempre `dataset`. |
| `labels` | Elenco di etichette di utilizzo dei dati che desideri aggiungere all’intero set di dati. |
| `parents` | L&#39;array `parents` contiene un elenco di `entityId` da cui questo set di dati erediterà le etichette. I set di dati possono ereditare le etichette da schemi e/o set di dati. |

**Risposta**

In caso di esito positivo, la risposta restituisce il set aggiornato di etichette per il set di dati.

>[!IMPORTANT]
>
>La proprietà `optionalLabels` è stata dichiarata obsoleta per l&#39;utilizzo con le richieste POST. Non è più possibile aggiungere etichette dati ai campi del set di dati. Un&#39;operazione POST genererà un errore se è presente un valore `optionalLabel`. Tuttavia, è possibile eliminare le etichette dai singoli campi utilizzando una richiesta PUT e la proprietà `optionalLabels`. Per ulteriori informazioni, vedere la sezione relativa alla rimozione di [etichette da un set di dati](#remove).

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

È possibile rimuovere le etichette di campo applicate in precedenza aggiornando i valori `optionalLabels` esistenti con un sottoinsieme delle etichette di campo esistenti o con un elenco vuoto per rimuoverle completamente. Effettuare una richiesta PUT all&#39;API [!DNL Dataset Service] per aggiornare o rimuovere le etichette applicate in precedenza.

**Formato API**

```http
PUT /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | Valore `id` univoco del set di dati per il quale si stanno creando le etichette. |

**Richiesta**

Il seguente set di dati su cui viene applicata l’operazione PUT aveva C1 optionalLabel sul campo properties/person/properties/address e C1, C2 optionalLabels sul campo /properties/person/properties/name/fullName. Dopo l’operazione put, il primo campo non avrà alcuna etichetta (l’etichetta C1 è stata rimossa) e il secondo campo avrà solo l’etichetta C1 (l’etichetta C2 è stata rimossa)

Nell’esempio seguente, viene utilizzata una richiesta PUT per rimuovere le etichette aggiunte ai singoli campi. Prima della richiesta, al campo `fullName` erano applicate le etichette `C1` e `C2` e al campo `address` era già applicata l&#39;etichetta `C1`. La richiesta PUT sostituisce le etichette esistenti `C1, C2` dal campo `fullName` con un&#39;etichetta `C1` utilizzando il parametro `optionalLabels.labels`. La richiesta sostituisce anche l&#39;etichetta `C1` del campo `address` con un set vuoto di etichette di campo.

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
        "parents": [
          {
            "id": "_xdm.context.identity-graph-flattened-export",
            "type": "schema",
            "namespace": "AEP"
          }
        ],
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
| `entityId` | Questo identifica l’entità del set di dati specifico da aggiornare. `entityId` deve includere i tre valori seguenti:<br/><br/>`namespace`: utilizzato per evitare conflitti tra ID. `namespace` è `AEP`.<br/>`id`: ID della risorsa da aggiornare. Si riferisce a `datasetId`.<br/>`type`: tipo di risorsa da aggiornare. Questo sarà sempre `dataset`. |
| `labels` | Elenco di etichette di utilizzo dei dati che desideri aggiungere all’intero set di dati. |
| `parents` | L&#39;array `parents` contiene un elenco di `entityId` da cui questo set di dati erediterà le etichette. I set di dati possono ereditare le etichette da schemi e/o set di dati. |
| `optionalLabels` | Questo parametro viene utilizzato per rimuovere le etichette applicate in precedenza a un campo set di dati. Elenco dei singoli campi all’interno del set di dati da cui desideri rimuovere le etichette. Ogni elemento in questo array deve avere le seguenti proprietà: <br/><br/>`option`: un oggetto che contiene gli attributi [!DNL Experience Data Model] (XDM) del campo. Sono necessarie le tre proprietà seguenti:<ul><li><code>id</code>: URI <code>$id</code> valore dello schema associato al campo.</li><li><code>contentType</code>: tipo di contenuto e numero di versione dello schema. Deve essere una delle <a href="../../xdm/api/getting-started.md#accept">intestazioni Accept</a> valide per una richiesta di ricerca XDM.</li><li><code>schemaPath</code>: percorso del campo nello schema del set di dati.</li></ul>`labels`: questo valore deve contenere un sottoinsieme delle etichette di campo esistenti applicate o essere vuoto per rimuovere tutte le etichette di campo esistenti. I metodi PUT o POST ora restituiscono un errore se il campo `optionalLabels` contiene etichette nuove o modificate. |

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

Dopo aver letto questo documento, hai imparato a gestire le etichette di utilizzo dei dati per set di dati e campi utilizzando l&#39;API [!DNL Dataset Service]. È ora possibile definire [criteri di utilizzo dati](../policies/overview.md) e [criteri di controllo dell&#39;accesso](../../access-control/abac/ui/policies.md) in base alle etichette applicate.

Per ulteriori informazioni sulla gestione dei set di dati in [!DNL Experience Platform], vedere la [panoramica dei set di dati](../../catalog/datasets/overview.md).
