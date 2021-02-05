---
keywords: ' Experience Platform;home;argomenti popolari;dataset api;gestire l''utilizzo dei dati;data usage api'
solution: Experience Platform
title: 'Gestione delle etichette di utilizzo dei dati per i set di dati tramite API '
topic: developer guide
description: L'API del servizio DataSet consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte delle funzionalità dei cataloghi di dati di Adobe Experience Platform, ma è separata dall'API Catalog Service che gestisce i metadati dei set di dati.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 2%

---


# Gestione delle etichette di utilizzo dei dati per i set di dati tramite API

[[!DNL Dataset Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte delle funzionalità dei cataloghi di dati di Adobe Experience Platform, ma è separata dall&#39;API [!DNL Catalog Service] che gestisce i metadati dei dataset.

Questo documento descrive come gestire le etichette per set di dati e campi utilizzando [!DNL Dataset Service API]. Per i passaggi su come gestire direttamente le etichette di utilizzo dei dati utilizzando le chiamate API, vedere la guida [alle etichette endpoint](../api/labels.md) per [!DNL Policy Service API].

## Introduzione

Prima di leggere questa guida, segui i passaggi descritti nella sezione [guida introduttiva](../../catalog/api/getting-started.md) nella guida per gli sviluppatori di Catalog per raccogliere le credenziali necessarie per effettuare chiamate alle [!DNL Platform] API.

Per effettuare chiamate agli endpoint descritti in questo documento, è necessario disporre del valore `id` univoco per un set di dati specifico. Se non si dispone di questo valore, consultare la guida in [elenco degli oggetti catalogo](../../catalog/api/list-objects.md) per individuare gli ID dei set di dati esistenti.

## Cerca etichette per un set di dati {#look-up}

È possibile ricercare le etichette di utilizzo dei dati applicate a un dataset esistente effettuando una richiesta di GET all&#39;API [!DNL Dataset Service].

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

## Applicare etichette a un set di dati {#apply}

Potete creare un set di etichette per un set di dati inserendole nel payload di una richiesta di POST o PUT all&#39;API [!DNL Dataset Service]. L’utilizzo di uno di questi metodi sovrascrive tutte le etichette esistenti e le sostituisce con quelle fornite nel payload.

**Formato API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | Valore `id` univoco del set di dati per il quale si creano le etichette. |

**Richiesta**

La seguente richiesta di PUT aggiorna le etichette esistenti per un set di dati, nonché un campo specifico all&#39;interno di tale set di dati. I campi forniti nel payload sono gli stessi richiesti per una richiesta di POST.

>[!IMPORTANT]
>
>Quando si effettuano richieste di PUT all&#39;endpoint `/datasets/{DATASET_ID}/labels`, è necessario fornire un&#39;intestazione `If-Match` valida. Per ulteriori informazioni sull&#39;utilizzo dell&#39;intestazione richiesta, vedere la sezione [appendice](#if-match).

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `labels` | Elenco di etichette di utilizzo dati da aggiungere al dataset. |
| `optionalLabels` | Un elenco di tutti i singoli campi all&#39;interno del set di dati a cui si desidera aggiungere etichette. Ogni elemento di questa matrice deve avere le seguenti proprietà: <br/><br/>`option`: Un oggetto che contiene gli attributi [!DNL Experience Data Model] (XDM) del campo. Sono richieste le tre proprietà seguenti:<ul><li>id</code>: Il valore URI $id</code> dello schema associato al campo.</li><li>contentType</code>: Il tipo di contenuto e il numero di versione dello schema. Questa operazione deve essere eseguita sotto forma di una delle <a href="../../xdm/api/getting-started.md#accept">Accetta intestazioni</a> valide per una richiesta di ricerca XDM.</li><li>schemaPath</code>: Percorso del campo all&#39;interno dello schema del set di dati.</li></ul>`labels`: Elenco di etichette di utilizzo dati da aggiungere al campo. |

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

## Rimuovere le etichette da un set di dati {#remove}

Potete rimuovere le etichette applicate a un dataset effettuando una richiesta di DELETE all&#39;API [!DNL Dataset Service].

**Formato API**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | Valore univoco `id` del set di dati di cui si desidera rimuovere le etichette. |

**Richiesta**

La seguente richiesta rimuove le etichette per il set di dati specificato nel percorso.

>[!IMPORTANT]
>
>Quando si effettuano richieste di DELETE all&#39;endpoint `/datasets/{DATASET_ID}/labels`, è necessario fornire un&#39;intestazione `If-Match` valida. Per ulteriori informazioni sull&#39;utilizzo dell&#39;intestazione richiesta, vedere la sezione [appendice](#if-match).

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000'
```

**Risposta**

Risposta corretta: stato HTTP 200 (OK), a indicare che le etichette sono state rimosse. È possibile [cercare le etichette esistenti](#look-up) per il set di dati in una chiamata separata per confermare questo.

## Passaggi successivi

Leggendo questo documento, hai imparato a gestire le etichette di utilizzo dei dati per set di dati e campi utilizzando l&#39;API [!DNL Dataset Service].

Dopo aver aggiunto le etichette di utilizzo dei dati a livello di set di dati e di campo, è possibile iniziare a assimilare i dati in [!DNL Experience Platform]. Per saperne di più, leggere la [documentazione di inserimento dei dati](../../ingestion/home.md).

È inoltre possibile definire criteri di utilizzo dei dati in base alle etichette applicate. Per ulteriori informazioni, vedere la [panoramica dei criteri di utilizzo dei dati](../policies/overview.md).

Per ulteriori informazioni sulla gestione dei set di dati in [!DNL Experience Platform], vedere la [panoramica dei set di dati](../../catalog/datasets/overview.md).

## Appendice {#appendix}

La sezione seguente contiene informazioni aggiuntive sull&#39;utilizzo delle etichette tramite l&#39;API del servizio DataSet.

### [!DNL If-Match] header  {#if-match}

Quando si effettuano chiamate API che aggiornano le etichette esistenti di un dataset (PUT e DELETE), è necessario includere un&#39;intestazione `If-Match` che indica la versione corrente dell&#39;entità dataset-etichetta nel servizio Dataset. Per evitare conflitti di dati, il servizio aggiornerà l&#39;entità dataset solo se la stringa inclusa `If-Match` corrisponde al tag versione più recente generato dal sistema per quel dataset.

>[!NOTE]
>
>Se al momento non esistono etichette per il set di dati in questione, è possibile aggiungere nuove etichette solo tramite una richiesta di POST, che non richiede un&#39;intestazione `If-Match`. Una volta aggiunte le etichette a un set di dati, viene assegnato un valore `etag` che può essere utilizzato per aggiornare o rimuovere le etichette in un secondo momento.

Per recuperare la versione più recente dell&#39;entità dataset-label, eseguire una [richiesta di GET](#look-up) nell&#39;endpoint `/datasets/{DATASET_ID}/labels`. Il valore corrente viene restituito nella risposta sotto un&#39;intestazione `etag`. Quando si aggiornano le etichette di set di dati esistenti, si consiglia di eseguire prima una richiesta di ricerca per il set di dati per recuperare il valore `etag` più recente prima di utilizzare tale valore nell&#39;intestazione `If-Match` della richiesta di PUT o DELETE successiva.