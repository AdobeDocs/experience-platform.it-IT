---
keywords: Experience Platform;home;argomenti popolari;governance dei dati;etichetta di utilizzo dati api;policy service api
solution: Experience Platform
title: Gestire le etichette di utilizzo dei dati utilizzando le API
description: L’API Servizio set di dati consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte delle funzionalità del catalogo dati di Adobe Experience Platform, ma è separata dall’API Catalog Service che gestisce i metadati dei set di dati.
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 3%

---


# Gestire le etichette di utilizzo dei dati tramite API

In questo documento vengono descritti i passaggi necessari per gestire le etichette di utilizzo dei dati utilizzando l&#39;API [!DNL Policy Service] e l&#39;API [!DNL Dataset Service].

[[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) fornisce diversi endpoint che consentono di creare e gestire le etichette di utilizzo dei dati per l&#39;organizzazione.

L&#39;API [!DNL Dataset Service] consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte delle funzionalità del catalogo dati di Adobe Experience Platform, ma è separata dall&#39;API [!DNL Catalog Service] che gestisce i metadati del set di dati.

## Introduzione

Prima di leggere questa guida, segui i passaggi descritti nella [sezione introduttiva](../../catalog/api/getting-started.md) nella guida per sviluppatori di Catalog per raccogliere le credenziali necessarie per effettuare chiamate alle API [!DNL Platform].

Per effettuare chiamate agli endpoint [!DNL Dataset Service] descritti in questo documento, è necessario disporre del valore `id` univoco per un set di dati specifico. Se non disponi di questo valore, consulta la guida in [elenco di oggetti Catalog](../../catalog/api/list-objects.md) per trovare gli ID dei set di dati esistenti.

## Elenca tutte le etichette {#list-labels}

Utilizzando l&#39;API [!DNL Policy Service], è possibile elencare tutte le etichette `core` o `custom` effettuando una richiesta GET rispettivamente a `/labels/core` o `/labels/custom`.

**Formato API**

```http
GET /labels/core
GET /labels/custom
```

**Richiesta**

Nella richiesta seguente sono elencate tutte le etichette personalizzate create nell’organizzazione.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di etichette personalizzate recuperate dal sistema. Poiché la richiesta di esempio precedente è stata effettuata a `/labels/custom`, la risposta seguente mostra solo etichette personalizzate.

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "L1",
            "category": "Custom",
            "friendlyName": "Banking Information",
            "description": "Data containing banking information for a customer.",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594396718731,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594396718731,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L1"
                }
            }
        },
        {
            "name": "L2",
            "category": "Custom",
            "friendlyName": "Purchase History Data",
            "description": "Data containing information on past transactions",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594397415663,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594397728708,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
                }
            }
        }
    ]
}
```

## Cercare un’etichetta {#look-up-label}

Per cercare un&#39;etichetta specifica, includere la proprietà `name` dell&#39;etichetta nel percorso di una richiesta GET all&#39;API [!DNL Policy Service].

**Formato API**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{LABEL_NAME}` | La proprietà `name` dell&#39;etichetta personalizzata che si desidera cercare. |

**Richiesta**

La richiesta seguente recupera l&#39;etichetta personalizzata `L2`, come indicato nel percorso.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli dell’etichetta personalizzata.

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{ORG_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "created": 1594397415663,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1594397728708,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
        }
    }
}
```

## Creare o aggiornare un’etichetta personalizzata {#create-update-label}

Per creare o aggiornare un&#39;etichetta personalizzata, è necessario effettuare una richiesta PUT all&#39;API [!DNL Policy Service].

**Formato API**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{LABEL_NAME}` | La proprietà `name` di un&#39;etichetta personalizzata. Se non esiste un’etichetta personalizzata con questo nome, verrà creata una nuova etichetta. Se ne esiste una, l’etichetta verrà aggiornata. |

**Richiesta**

La richiesta seguente crea una nuova etichetta, `L3`, che ha lo scopo di descrivere i dati contenenti informazioni relative ai piani di pagamento selezionati dai clienti.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "L3",
        "category": "Custom",
        "friendlyName": "Payment Plan",
        "description": "Data containing information on selected payment plans."
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Un identificatore di stringa univoco per l’etichetta. Questo valore viene utilizzato a scopo di ricerca e per applicare l’etichetta a set di dati e campi, pertanto si consiglia che sia breve e conciso. |
| `category` | Categoria dell’etichetta. Sebbene sia possibile creare categorie personalizzate per le etichette personalizzate, si consiglia vivamente di utilizzare `Custom` se si desidera che l&#39;etichetta venga visualizzata nell&#39;interfaccia utente. |
| `friendlyName` | Un nome descrittivo per l’etichetta, utilizzato a scopo di visualizzazione. |
| `description` | (Facoltativo) Una descrizione dell’etichetta per fornire ulteriore contesto. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli dell’etichetta personalizzata, con codice HTTP 200 (OK) se è stata aggiornata un’etichetta esistente, oppure 201 (Creato) se è stata creata una nuova etichetta.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{ORG_ID}",
  "sandboxName": "{SANDBOX_NAME}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L3"
    }
  }
}
```

## Cercare etichette per un set di dati {#look-up-dataset-labels}

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
| `optionalLabels` | Elenco di singoli campi all’interno del set di dati a cui sono applicate etichette di utilizzo dei dati. Sono necessarie le seguenti sottoproprietà:<br/><br/>`option`: un oggetto contenente gli attributi [!DNL Experience Data Model] (XDM) del campo. Sono necessarie le tre proprietà seguenti:<ul><li>`id`: valore URI `$id` dello schema associato al campo.</li><li>`contentType`: indica il formato e la versione dello schema. Per ulteriori informazioni, consulta la sezione sul controllo delle versioni dello schema [1} nella guida dell&#39;API XDM.](../../xdm/api/getting-started.md#versioning)</li><li>`schemaPath`: percorso della proprietà dello schema in questione, scritto con sintassi [JSON Pointer](../../landing/api-fundamentals.md#json-pointer).</li></ul>`labels`: elenco di etichette di utilizzo dei dati che si desidera aggiungere al campo. |

- id: il valore URI $id per lo schema XDM su cui si basa il set di dati.
- contentType: indica il formato e la versione dello schema. Per ulteriori informazioni, consulta la sezione sul controllo delle versioni dello schema [1} nella guida dell&#39;API XDM.](../../xdm/api/getting-started.md#versioning)
- schemaPath: percorso della proprietà dello schema in questione, scritto con sintassi [JSON Pointer](../../landing/api-fundamentals.md#json-pointer).

## Applicare etichette a un set di dati {#apply-dataset-labels}

È possibile creare un set di etichette per un set di dati fornendole nel payload di una richiesta POST o PUT all&#39;API [!DNL Dataset Service]. L’utilizzo di uno di questi metodi sovrascrive tutte le etichette esistenti e le sostituisce con quelle fornite nel payload.

**Formato API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | Valore `id` univoco del set di dati per il quale si stanno creando le etichette. |

**Richiesta**

La seguente richiesta POST aggiunge una serie di etichette al set di dati, nonché un campo specifico all’interno di tale set di dati. I campi forniti nel payload sono gli stessi richiesti per una richiesta PUT.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
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
| `optionalLabels` | Elenco dei singoli campi all’interno del set di dati a cui desideri aggiungere etichette. Ogni elemento in questo array deve avere le seguenti proprietà:<br/><br/>`option`: un oggetto che contiene gli attributi [!DNL Experience Data Model] (XDM) del campo. Sono necessarie le tre proprietà seguenti:<ul><li>`id`: valore URI `$id` dello schema associato al campo.</li><li>`contentType`: indica il formato e la versione dello schema. Per ulteriori informazioni, consulta la sezione sul controllo delle versioni dello schema [1} nella guida dell&#39;API XDM.](../../xdm/api/getting-started.md#versioning)</li><li>`schemaPath`: percorso della proprietà dello schema in questione, scritto con sintassi [JSON Pointer](../../landing/api-fundamentals.md#json-pointer).</li></ul>`labels`: elenco di etichette di utilizzo dei dati che si desidera aggiungere al campo. |

**Risposta**

In caso di esito positivo, la risposta restituisce le etichette aggiunte al set di dati.

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

## Rimuovere le etichette da un set di dati {#remove-dataset-labels}

È possibile rimuovere le etichette applicate a un set di dati effettuando una richiesta DELETE all&#39;API [!DNL Dataset Service].

**Formato API**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | Valore `id` univoco del set di dati di cui si desidera rimuovere le etichette. |

**Richiesta**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Risposta corretta dello stato HTTP 200 (OK), che indica che le etichette sono state rimosse. Puoi [cercare le etichette esistenti](#look-up-dataset-labels) per il set di dati in una chiamata separata per confermarlo.

## Passaggi successivi

Dopo aver letto questo documento, hai imparato a gestire le etichette di utilizzo dei dati utilizzando le API.

Dopo aver aggiunto le etichette di utilizzo dei dati a livello di set di dati e di campo, puoi iniziare a acquisire dati in [!DNL Experience Platform]. Per ulteriori informazioni, consulta la [documentazione sull&#39;acquisizione dei dati](../../ingestion/home.md).

Ora puoi anche definire i criteri di utilizzo dei dati in base alle etichette applicate. Per ulteriori informazioni, vedere la [panoramica dei criteri di utilizzo dei dati](../policies/overview.md).

Per ulteriori informazioni sulla gestione dei set di dati in [!DNL Experience Platform], vedere la [panoramica dei set di dati](../../catalog/datasets/overview.md).