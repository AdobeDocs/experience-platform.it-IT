---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Gestione delle etichette di utilizzo dei dati tramite API '
topic: developer guide
translation-type: tm+mt
source-git-commit: 1fce86193bc1660d0f16408ed1b9217368549f6c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 3%

---


# Gestione delle etichette di utilizzo dei dati tramite API

L&#39;API del servizio DataSet consente di gestire in modo programmatico le etichette di utilizzo per i set di dati. Fa parte delle funzionalità del catalogo dati di Adobe Experience Platform, ma è separato dall&#39;API del servizio catalogo che gestisce i metadati del set di dati.

In questo documento sono descritti i passaggi necessari per gestire le etichette di utilizzo dei dati a livello di set di dati e di campo mediante l&#39;API del servizio DataSet.

## Introduzione

Prima di leggere questa guida, segui i passaggi descritti nella sezione [](../../catalog/api/getting-started.md) introduttiva della guida per gli sviluppatori del catalogo per raccogliere le credenziali necessarie per effettuare chiamate alle [!DNL Platform] API.

Per effettuare chiamate agli endpoint descritti nelle sezioni seguenti, è necessario disporre del `id` valore univoco per un set di dati specifico. Se non hai questo valore, consulta la guida sull’ [elenco degli oggetti](../../catalog/api/list-objects.md) catalogo per trovare gli ID dei set di dati esistenti.

## Cerca etichette per un set di dati {#lookup}

È possibile ricercare le etichette di utilizzo dei dati applicate a un dataset esistente effettuando una richiesta GET.

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

## Applicare etichette a un dataset

Potete creare un set di etichette per un set di dati inserendovi nel payload di una richiesta POST o PUT. L’utilizzo di uno di questi metodi sovrascrive tutte le etichette esistenti e le sostituisce con quelle fornite nel payload.

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

## Eliminare etichette per un set di dati

È possibile eliminare le etichette applicate a un dataset effettuando una richiesta DELETE.

**Formato API**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | Il `id` valore univoco del set di dati di cui si desidera eliminare le etichette. |

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

Risposta corretta: stato HTTP 200 (OK), che indica che le etichette sono state eliminate. Potete [cercare le etichette](#lookup) esistenti per il set di dati in una chiamata separata per confermarlo.

## Passaggi successivi

Ora che hai aggiunto etichette di utilizzo dei dati a livello di set di dati e di campo, puoi iniziare a assimilare i dati in Experience Platform. Per saperne di più, leggi la documentazione [sull’inserimento dei](../../ingestion/home.md)dati.

È inoltre possibile definire criteri di utilizzo dei dati in base alle etichette applicate. Per ulteriori informazioni, vedere la panoramica [dei criteri di utilizzo dei](../policies/overview.md)dati.

Per ulteriori informazioni sulla gestione dei set di dati in [!DNL Experience Platform], vedere la panoramica [dei](../../catalog/datasets/overview.md)set di dati.