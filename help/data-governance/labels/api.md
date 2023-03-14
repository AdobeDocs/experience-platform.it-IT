---
keywords: Experience Platform;home;argomenti popolari;governance dei dati;etichetta di utilizzo dati api;policy service api
solution: Experience Platform
title: Gestire le etichette di utilizzo dei dati utilizzando le API
description: L’API Servizio set di dati consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte delle funzionalità del catalogo dati di Adobe Experience Platform, ma è separata dall’API Catalog Service che gestisce i metadati dei set di dati.
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 3%

---


# Gestire le etichette di utilizzo dei dati tramite API

Questo documento descrive come gestire le etichette di utilizzo dei dati utilizzando [!DNL Policy Service] API e [!DNL Dataset Service] API.

Il [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) fornisce diversi endpoint che ti consentono di creare e gestire le etichette di utilizzo dei dati per la tua organizzazione.

Il [!DNL Dataset Service] API consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte delle funzionalità del catalogo dati di Adobe Experience Platform, ma è separata dal [!DNL Catalog Service] API per la gestione dei metadati del set di dati.

## Introduzione

Prima di leggere questa guida, segui i passaggi descritti in [sezione introduttiva](../../catalog/api/getting-started.md) nella guida per gli sviluppatori di Catalog per raccogliere le credenziali necessarie per effettuare chiamate a [!DNL Platform] API.

Per effettuare chiamate al [!DNL Dataset Service] endpoint descritti in questo documento, è necessario disporre dell&#39;unica `id` per un set di dati specifico. In caso contrario, consulta la guida su [elenco degli oggetti catalogo](../../catalog/api/list-objects.md) per trovare gli ID dei set di dati esistenti.

## Elenca tutte le etichette {#list-labels}

Utilizzo di [!DNL Policy Service] API, puoi elencare tutti `core` o `custom` effettuando una richiesta GET a `/labels/core` o `/labels/custom`, rispettivamente.

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

In caso di esito positivo, la risposta restituisce un elenco di etichette personalizzate recuperate dal sistema. Poiché l&#39;esempio precedente è stato chiesto a `/labels/custom`, la risposta seguente mostra solo etichette personalizzate.

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

Per cercare un’etichetta specifica, includi le `name` nel percorso di una richiesta GET al [!DNL Policy Service] API.

**Formato API**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{LABEL_NAME}` | Il `name` dell’etichetta personalizzata che desideri cercare. |

**Richiesta**

La richiesta seguente recupera l’etichetta personalizzata `L2`, come indicato nel percorso.

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

Per creare o aggiornare un’etichetta personalizzata, devi effettuare una richiesta PUT al [!DNL Policy Service] API.

**Formato API**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{LABEL_NAME}` | Il `name` di un&#39;etichetta personalizzata. Se non esiste un’etichetta personalizzata con questo nome, verrà creata una nuova etichetta. Se ne esiste una, l’etichetta verrà aggiornata. |

**Richiesta**

La richiesta seguente crea una nuova etichetta, `L3`, che mira a descrivere dati contenenti informazioni relative ai piani di pagamento selezionati dei clienti.

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
| `category` | Categoria dell’etichetta. Sebbene sia possibile creare categorie personalizzate per le etichette personalizzate, si consiglia vivamente di utilizzare `Custom` se desideri che l’etichetta venga visualizzata nell’interfaccia utente. |
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
| `optionalLabels` | Elenco di singoli campi all’interno del set di dati a cui sono applicate etichette di utilizzo dei dati. Sono necessarie le seguenti sottoproprietà:<br/><br/>`option`: oggetto che contiene [!DNL Experience Data Model] (XDM) attributi del campo. Sono necessarie le tre proprietà seguenti:<ul><li>`id`: URI `$id` valore dello schema associato al campo.</li><li>`contentType`: indica il formato e la versione dello schema. Consulta la sezione su [controllo delle versioni dello schema](../../xdm/api/getting-started.md#versioning) per ulteriori informazioni, consulta la guida dell’API XDM.</li><li>`schemaPath`: percorso della proprietà dello schema in questione, scritto in [Puntatore JSON](../../landing/api-fundamentals.md#json-pointer) sintassi.</li></ul>`labels`: elenco di etichette di utilizzo dei dati che desideri aggiungere al campo. |

- id: il valore URI $id per lo schema XDM su cui si basa il set di dati.
- contentType: indica il formato e la versione dello schema. Consulta la sezione su [controllo delle versioni dello schema](../../xdm/api/getting-started.md#versioning) per ulteriori informazioni, consulta la guida dell’API XDM.
- schemaPath: percorso della proprietà dello schema in questione, scritto in [Puntatore JSON](../../landing/api-fundamentals.md#json-pointer) sintassi.

## Applicare etichette a un set di dati {#apply-dataset-labels}

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
| `optionalLabels` | Elenco dei singoli campi all’interno del set di dati a cui desideri aggiungere etichette. Ogni elemento in questo array deve avere le seguenti proprietà:<br/><br/>`option`: oggetto che contiene [!DNL Experience Data Model] (XDM) attributi del campo. Sono necessarie le tre proprietà seguenti:<ul><li>`id`: URI `$id` valore dello schema associato al campo.</li><li>`contentType`: indica il formato e la versione dello schema. Consulta la sezione su [controllo delle versioni dello schema](../../xdm/api/getting-started.md#versioning) per ulteriori informazioni, consulta la guida dell’API XDM.</li><li>`schemaPath`: percorso della proprietà dello schema in questione, scritto in [Puntatore JSON](../../landing/api-fundamentals.md#json-pointer) sintassi.</li></ul>`labels`: elenco di etichette di utilizzo dei dati che desideri aggiungere al campo. |

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

Per rimuovere le etichette applicate a un set di dati, devi effettuare una richiesta DELETE al [!DNL Dataset Service] API.

**Formato API**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | L&#39;unico `id` valore del set di dati di cui si desidera rimuovere le etichette. |

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

Risposta corretta dello stato HTTP 200 (OK), che indica che le etichette sono state rimosse. È possibile [cerca le etichette esistenti](#look-up-dataset-labels) per il set di dati in una chiamata separata per confermarlo.

## Passaggi successivi

Dopo aver letto questo documento, hai imparato a gestire le etichette di utilizzo dei dati utilizzando le API.

Dopo aver aggiunto le etichette di utilizzo dei dati a livello di set di dati e di campo, puoi iniziare ad acquisire i dati in [!DNL Experience Platform]. Per ulteriori informazioni, consulta la sezione [documentazione sull’acquisizione dei dati](../../ingestion/home.md).

Ora puoi anche definire i criteri di utilizzo dei dati in base alle etichette applicate. Per ulteriori informazioni, vedere [panoramica dei criteri di utilizzo dei dati](../policies/overview.md).

Per ulteriori informazioni sulla gestione dei set di dati in [!DNL Experience Platform], vedere [panoramica dei set di dati](../../catalog/datasets/overview.md).