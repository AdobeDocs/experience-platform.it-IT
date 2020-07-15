---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Gestione delle etichette di utilizzo dei dati tramite API '
topic: developer guide
translation-type: tm+mt
source-git-commit: b51a13e2eab967099c84d1cca2233e2ace554e01
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 3%

---


# Gestione delle etichette di utilizzo dei dati tramite API

In questo documento vengono fornite istruzioni su come gestire le etichette di utilizzo dei dati utilizzando l&#39;API del servizio criteri e l&#39;API del servizio DataSet.

L&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) Policy Service fornisce diversi endpoint che consentono di creare e gestire le etichette di utilizzo dei dati per la vostra organizzazione.

L&#39;API del servizio DataSet consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte  funzionalità  catalogo dati, ma è separata dall’API del servizio catalogo che gestisce i metadati del set di dati.

## Introduzione

Prima di leggere questa guida, segui i passaggi descritti nella sezione [](../../catalog/api/getting-started.md) introduttiva della guida per gli sviluppatori del catalogo per raccogliere le credenziali necessarie per effettuare chiamate alle [!DNL Platform] API.

Per effettuare chiamate agli endpoint del servizio DataSet descritti in questo documento, è necessario disporre del `id` valore univoco per un set di dati specifico. Se non hai questo valore, consulta la guida sull’ [elenco degli oggetti](../../catalog/api/list-objects.md) catalogo per trovare gli ID dei set di dati esistenti.

## Elenca tutte le etichette {#list-labels}

Utilizzando l&#39; [!DNL Policy Service] API, potete elencare tutte `core` o `custom` le etichette effettuando rispettivamente una richiesta GET a `/labels/core` o `/labels/custom`.

**Formato API**

```http
GET /labels/core
GET /labels/custom
```

**Richiesta**

Nella richiesta seguente sono elencate tutte le etichette personalizzate create all&#39;interno dell&#39;organizzazione.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di etichette personalizzate recuperate dal sistema. Poiché la richiesta di esempio sopra è stata inoltrata a `/labels/custom`, la risposta riportata di seguito mostra solo le etichette personalizzate.

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

## Cercare un&#39;etichetta {#look-up-label}

Potete cercare un&#39;etichetta specifica includendo la `name` proprietà dell&#39;etichetta nel percorso di una richiesta GET all&#39;API del servizio criteri.

**Formato API**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{LABEL_NAME}` | La `name` proprietà dell&#39;etichetta personalizzata che si desidera cercare. |

**Richiesta**

La richiesta seguente recupera l&#39;etichetta personalizzata `L2`, come indicato nel percorso.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli dell&#39;etichetta personalizzata.

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

## Creare o aggiornare un&#39;etichetta personalizzata {#create-update-label}

Per creare o aggiornare un&#39;etichetta personalizzata, è necessario effettuare una richiesta PUT all&#39;API del servizio criteri.

**Formato API**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{LABEL_NAME}` | La `name` proprietà di un&#39;etichetta personalizzata. Se non esiste un&#39;etichetta personalizzata con questo nome, verrà creata una nuova etichetta. Se ne esiste uno, l&#39;etichetta verrà aggiornata. |

**Richiesta**

La seguente richiesta crea una nuova etichetta `L3`, che ha lo scopo di descrivere i dati che contengono informazioni relative ai piani di pagamento selezionati dai clienti.

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
| `name` | Identificatore stringa univoco per l&#39;etichetta. Questo valore viene utilizzato a scopo di ricerca e l&#39;etichetta viene applicata a set di dati e campi, pertanto si consiglia di utilizzarlo in modo breve e conciso. |
| `category` | La categoria dell&#39;etichetta. Sebbene sia possibile creare categorie personalizzate per le etichette personalizzate, è comunque consigliabile utilizzarle `Custom` se si desidera che l&#39;etichetta venga visualizzata nell&#39;interfaccia utente. |
| `friendlyName` | Un nome descrittivo per l&#39;etichetta, utilizzato a scopo di visualizzazione. |
| `description` | (Facoltativo) Una descrizione dell&#39;etichetta per fornire ulteriore contesto. |

**Risposta**

Una risposta corretta restituisce i dettagli dell&#39;etichetta personalizzata, con codice HTTP 200 (OK) se un&#39;etichetta esistente è stata aggiornata, oppure 201 (Creato) se è stata creata una nuova etichetta.

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

## Cerca etichette per un set di dati {#look-up-dataset-labels}

È possibile ricercare le etichette di utilizzo dei dati applicate a un dataset esistente effettuando una richiesta GET all&#39;API del servizio DataSet.

**Formato API**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | Il `id` valore univoco del set di dati di cui si desidera cercare le etichette. |

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
| `labels` | Elenco di etichette di utilizzo dati applicate al set di dati. |
| `optionalLabels` | Elenco di singoli campi all’interno del dataset a cui sono applicate etichette di utilizzo dei dati. |

## Applicare etichette a un dataset {#apply-dataset-labels}

Potete creare un set di etichette per un dataset inserendolo nel payload di una richiesta POST o PUT all&#39;API del servizio Dataset. L’utilizzo di uno di questi metodi sovrascrive tutte le etichette esistenti e le sostituisce con quelle fornite nel payload.

**Formato API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | Il `id` valore univoco del set di dati per il quale si creano le etichette. |

**Richiesta**

La seguente richiesta POST aggiunge una serie di etichette al set di dati, oltre a un campo specifico all’interno del set di dati. I campi forniti nel payload sono gli stessi richiesti per una richiesta PUT.

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
| `labels` | Elenco di etichette di utilizzo dati da aggiungere al dataset. |
| `optionalLabels` | Un elenco di tutti i singoli campi all&#39;interno del set di dati a cui si desidera aggiungere etichette. Ogni elemento di questa matrice deve avere le seguenti proprietà: <br/><br/>`option`: Un oggetto che contiene gli attributi Experience Data Model (XDM) del campo. Sono richieste le tre proprietà seguenti:<ul><li>id</code>: Il valore URI $id</code> dello schema associato al campo.</li><li>contentType</code>: Il tipo di contenuto e il numero di versione dello schema. Questo deve assumere la forma di una delle intestazioni <a href="../../xdm/api/look-up-resource.md"></a> Accetta valide per una richiesta di ricerca XDM.</li><li>schemaPath</code>: Percorso del campo all&#39;interno dello schema del set di dati.</li></ul>`labels`: Elenco di etichette di utilizzo dati da aggiungere al campo. |

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

## Rimozione di etichette da un dataset {#remove-dataset-labels}

È possibile rimuovere le etichette applicate a un dataset effettuando una richiesta di DELETE all&#39;API del servizio DataSet.

**Formato API**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | Il `id` valore univoco del set di dati di cui si desidera rimuovere le etichette. |

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

Risposta corretta: stato HTTP 200 (OK), a indicare che le etichette sono state rimosse. Potete [cercare le etichette](#look-up-dataset-labels) esistenti per il set di dati in una chiamata separata per confermarlo.

## Passaggi successivi

Leggendo questo documento, hai imparato a gestire le etichette di utilizzo dei dati utilizzando le API.

Dopo aver aggiunto le etichette di utilizzo dei dati a livello di set di dati e di campo, è possibile iniziare a trasferire i dati in  Experience Platform. Per saperne di più, leggi la documentazione [sull’inserimento dei](../../ingestion/home.md)dati.

È inoltre possibile definire criteri di utilizzo dei dati in base alle etichette applicate. Per ulteriori informazioni, vedere la panoramica [dei criteri di utilizzo dei](../policies/overview.md)dati.

Per ulteriori informazioni sulla gestione dei set di dati in [!DNL Experience Platform], vedere la panoramica [dei](../../catalog/datasets/overview.md)set di dati.