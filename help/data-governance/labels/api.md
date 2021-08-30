---
keywords: Experience Platform;home;argomenti popolari;governance dei dati;api dell'etichetta di utilizzo dei dati;api del servizio criteri
solution: Experience Platform
title: 'Gestire le etichette di utilizzo dei dati utilizzando le API '
topic-legacy: developer guide
description: L’API del servizio Dataset consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte delle funzionalità del catalogo dati di Adobe Experience Platform, ma è separato dall’API del servizio catalogo che gestisce i metadati del set di dati.
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 3%

---


# Gestire le etichette di utilizzo dei dati tramite API

Questo documento fornisce passaggi su come gestire le etichette di utilizzo dei dati utilizzando le API [!DNL Policy Service] e [!DNL Dataset Service].

Il [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) fornisce diversi endpoint che consentono di creare e gestire le etichette di utilizzo dei dati per la tua organizzazione.

L’ API [!DNL Dataset Service] ti consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte delle funzionalità del catalogo dati di Adobe Experience Platform, ma è separato dall’ [!DNL Catalog Service] API che gestisce i metadati del set di dati.

## Introduzione

Prima di leggere questa guida, segui i passaggi descritti nella sezione [guida introduttiva](../../catalog/api/getting-started.md) nella guida per gli sviluppatori del catalogo per raccogliere le credenziali necessarie per effettuare chiamate alle API [!DNL Platform] .

Per effettuare chiamate agli endpoint [!DNL Dataset Service] descritti in questo documento, è necessario disporre del valore univoco `id` per un set di dati specifico. Se non disponi di questo valore, consulta la guida in [elenco degli oggetti del catalogo](../../catalog/api/list-objects.md) per trovare gli ID dei set di dati esistenti.

## Elenca tutte le etichette {#list-labels}

Utilizzando l’API [!DNL Policy Service], puoi elencare tutte le etichette `core` o `custom` effettuando una richiesta di GET rispettivamente a `/labels/core` o `/labels/custom`.

**Formato API**

```http
GET /labels/core
GET /labels/custom
```

**Richiesta**

Nella richiesta seguente sono elencate tutte le etichette personalizzate create all’interno dell’organizzazione.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di etichette personalizzate recuperate dal sistema. Poiché la richiesta di esempio precedente è stata effettuata su `/labels/custom`, la risposta seguente mostra solo etichette personalizzate.

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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

## Cerca un&#39;etichetta {#look-up-label}

Puoi cercare un’etichetta specifica includendo la proprietà `name` dell’etichetta nel percorso di una richiesta di GET all’ [!DNL Policy Service] API.

**Formato API**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{LABEL_NAME}` | La proprietà `name` dell&#39;etichetta personalizzata che si desidera cercare. |

**Richiesta**

La richiesta seguente recupera l’etichetta personalizzata `L2`, come indicato nel percorso.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli dell’etichetta personalizzata.

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{IMS_ORG}",
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

Per creare o aggiornare un’etichetta personalizzata, devi effettuare una richiesta PUT all’API [!DNL Policy Service] .

**Formato API**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{LABEL_NAME}` | La proprietà `name` di un&#39;etichetta personalizzata. Se non esiste un’etichetta personalizzata con questo nome, verrà creata una nuova etichetta. Se esiste, l’etichetta verrà aggiornata. |

**Richiesta**

La seguente richiesta crea una nuova etichetta, `L3`, che ha lo scopo di descrivere i dati che contengono informazioni relative ai piani di pagamento selezionati dai clienti.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Identificatore stringa univoco per l&#39;etichetta. Questo valore viene utilizzato a scopo di ricerca e applica l’etichetta ai set di dati e ai campi, pertanto si consiglia di breve e concisa. |
| `category` | La categoria dell&#39;etichetta. Mentre puoi creare categorie personalizzate per le etichette personalizzate, è consigliabile utilizzare `Custom` per visualizzare l’etichetta nell’interfaccia utente. |
| `friendlyName` | Un nome descrittivo per l’etichetta, utilizzato a scopo di visualizzazione. |
| `description` | (Facoltativo) Una descrizione dell’etichetta per fornire ulteriore contesto. |

**Risposta**

Una risposta corretta restituisce i dettagli dell’etichetta personalizzata, con codice HTTP 200 (OK) se è stata aggiornata un’etichetta esistente, oppure 201 (Creato) se è stata creata una nuova etichetta.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{IMS_ORG}",
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

Puoi cercare le etichette di utilizzo dei dati applicate a un set di dati esistente effettuando una richiesta di GET all’ [!DNL Dataset Service] API.

**Formato API**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | Valore univoco `id` del set di dati di cui si desidera cercare le etichette. |

**Richiesta**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce le etichette di utilizzo dei dati applicate al set di dati.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{IMS_ORG}",
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
| `optionalLabels` | Elenco di singoli campi all’interno del set di dati a cui sono applicate etichette di utilizzo dei dati. Sono richieste le seguenti sottoproprietà:<br/><br/>`option`: Oggetto che contiene gli attributi [!DNL Experience Data Model] (XDM) del campo. Sono richieste le tre proprietà seguenti:<ul><li>`id`: Il  `$id` valore URI dello schema associato al campo.</li><li>`contentType`: Indica il formato e la versione dello schema. Per ulteriori informazioni, consulta la sezione sul [controllo delle versioni dello schema](../../xdm/api/getting-started.md#versioning) nella guida API XDM .</li><li>`schemaPath`: Percorso della proprietà dello schema in questione, scritto in  [JSON ](../../landing/api-fundamentals.md#json-pointer) Pointersintassi.</li></ul>`labels`: Elenco di etichette di utilizzo dati da aggiungere al campo. |

- id: Valore URI $id per lo schema XDM su cui si basa il set di dati.
- contentType: Indica il formato e la versione dello schema. Per ulteriori informazioni, consulta la sezione sul [controllo delle versioni dello schema](../../xdm/api/getting-started.md#versioning) nella guida API XDM .
- schemaPath: Percorso della proprietà dello schema in questione, scritto con sintassi [JSON Pointer](../../landing/api-fundamentals.md#json-pointer).

## Applicare etichette a un set di dati {#apply-dataset-labels}

Puoi creare un set di etichette per un set di dati fornendo loro nel payload di una richiesta di POST o PUT all’ API [!DNL Dataset Service] . L’utilizzo di uno di questi metodi sovrascrive le etichette esistenti e le sostituisce con quelle fornite nel payload.

**Formato API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | Valore `id` univoco del set di dati per cui si stanno creando le etichette. |

**Richiesta**

La seguente richiesta di POST aggiunge una serie di etichette al set di dati, nonché un campo specifico all’interno di tale set di dati. I campi forniti nel payload sono gli stessi richiesti per una richiesta PUT.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `labels` | Elenco di etichette di utilizzo dei dati da aggiungere al set di dati. |
| `optionalLabels` | Elenco di tutti i singoli campi all’interno del set di dati a cui si desidera aggiungere le etichette. Ogni elemento della matrice deve avere le seguenti proprietà:<br/><br/>`option`: Oggetto che contiene gli attributi [!DNL Experience Data Model] (XDM) del campo. Sono richieste le tre proprietà seguenti:<ul><li>`id`: Il  `$id` valore URI dello schema associato al campo.</li><li>`contentType`: Indica il formato e la versione dello schema. Per ulteriori informazioni, consulta la sezione sul [controllo delle versioni dello schema](../../xdm/api/getting-started.md#versioning) nella guida API XDM .</li><li>`schemaPath`: Percorso della proprietà dello schema in questione, scritto in  [JSON ](../../landing/api-fundamentals.md#json-pointer) Pointersintassi.</li></ul>`labels`: Elenco di etichette di utilizzo dati da aggiungere al campo. |

**Risposta**

Una risposta corretta restituisce le etichette aggiunte al set di dati.

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

Puoi rimuovere le etichette applicate a un set di dati effettuando una richiesta DELETE all’ API [!DNL Dataset Service] .

**Formato API**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | Valore univoco `id` del set di dati di cui si desidera rimuovere le etichette. |

**Richiesta**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta, stato HTTP 200 (OK), che indica che le etichette sono state rimosse. Puoi [cercare le etichette esistenti](#look-up-dataset-labels) per il set di dati in una chiamata separata per confermarlo.

## Passaggi successivi

Leggendo questo documento, hai imparato a gestire le etichette di utilizzo dei dati utilizzando le API.

Dopo aver aggiunto le etichette di utilizzo dei dati a livello di set di dati e di campo, puoi iniziare a inserire i dati in [!DNL Experience Platform]. Per ulteriori informazioni, inizia leggendo la [documentazione sull&#39;acquisizione dei dati](../../ingestion/home.md).

È inoltre possibile definire criteri di utilizzo dei dati in base alle etichette applicate. Per ulteriori informazioni, consulta la [panoramica dei criteri di utilizzo dei dati](../policies/overview.md).

Per ulteriori informazioni sulla gestione dei set di dati in [!DNL Experience Platform], consulta la [panoramica dei set di dati](../../catalog/datasets/overview.md).