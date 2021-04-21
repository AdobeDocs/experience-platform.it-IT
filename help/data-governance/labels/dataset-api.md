---
keywords: Experience Platform;home;argomenti popolari;api set di dati;gestire l’utilizzo dei dati;api di utilizzo dati
solution: Experience Platform
title: 'Gestire le etichette di utilizzo dei dati per i set di dati utilizzando le API '
topic-legacy: developer guide
description: L’API del servizio Dataset consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte delle funzionalità del catalogo dati di Adobe Experience Platform, ma è separato dall’API del servizio catalogo che gestisce i metadati del set di dati.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 2%

---

# Gestire le etichette di utilizzo dei dati per i set di dati tramite API

Il [[!DNL Dataset Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) ti consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte delle funzionalità del catalogo dati di Adobe Experience Platform, ma è separato dall’ [!DNL Catalog Service] API che gestisce i metadati del set di dati.

Questo documento illustra come gestire le etichette per i set di dati e i campi utilizzando [!DNL Dataset Service API]. Per i passaggi su come gestire direttamente le etichette di utilizzo dei dati utilizzando le chiamate API, consulta la [guida all&#39;endpoint delle etichette](../api/labels.md) per il tag [!DNL Policy Service API].

## Introduzione

Prima di leggere questa guida, segui i passaggi descritti nella sezione [guida introduttiva](../../catalog/api/getting-started.md) nella guida per gli sviluppatori del catalogo per raccogliere le credenziali necessarie per effettuare chiamate alle API [!DNL Platform] .

Per effettuare chiamate agli endpoint descritti in questo documento, è necessario disporre del valore univoco `id` per un set di dati specifico. Se non disponi di questo valore, consulta la guida in [elenco degli oggetti del catalogo](../../catalog/api/list-objects.md) per trovare gli ID dei set di dati esistenti.

## Cercare etichette per un set di dati {#look-up}

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
| `optionalLabels` | Elenco di singoli campi all’interno del set di dati a cui sono applicate etichette di utilizzo dei dati. |

## Applicare etichette a un set di dati {#apply}

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

La seguente richiesta di PUT aggiorna le etichette esistenti per un set di dati, nonché un campo specifico all’interno di tale set di dati. I campi forniti nel payload sono gli stessi richiesti per una richiesta POST.

>[!IMPORTANT]
>
>Quando si effettuano richieste PUT all’endpoint `/datasets/{DATASET_ID}/labels` è necessario fornire un’intestazione `If-Match` valida. Per ulteriori informazioni sull&#39;utilizzo dell&#39;intestazione richiesta, vedere la sezione [appendice](#if-match) .

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
| `labels` | Elenco di etichette di utilizzo dei dati da aggiungere al set di dati. |
| `optionalLabels` | Elenco di tutti i singoli campi all’interno del set di dati a cui si desidera aggiungere le etichette. Ogni elemento della matrice deve avere le seguenti proprietà: <br/><br/>`option`: Oggetto che contiene gli attributi [!DNL Experience Data Model] (XDM) del campo. Sono richieste le tre proprietà seguenti:<ul><li>id</code>: Valore URI $id</code> dello schema associato al campo.</li><li>contentType</code>: Il tipo di contenuto e il numero di versione dello schema. Questo deve assumere la forma di una delle <a href="../../xdm/api/getting-started.md#accept">Accetta intestazioni</a> valide per una richiesta di ricerca XDM.</li><li>schemaPath</code>: Percorso del campo nello schema del set di dati.</li></ul>`labels`: Elenco di etichette di utilizzo dati da aggiungere al campo. |

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

Puoi rimuovere le etichette applicate a un set di dati effettuando una richiesta DELETE all’ API [!DNL Dataset Service] .

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
>Quando si effettuano richieste DELETE all’endpoint `/datasets/{DATASET_ID}/labels` è necessario fornire un’intestazione `If-Match` valida. Per ulteriori informazioni sull&#39;utilizzo dell&#39;intestazione richiesta, vedere la sezione [appendice](#if-match) .

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

Una risposta corretta, stato HTTP 200 (OK), che indica che le etichette sono state rimosse. Puoi [cercare le etichette esistenti](#look-up) per il set di dati in una chiamata separata per confermarlo.

## Passaggi successivi

Leggendo questo documento, hai imparato a gestire le etichette di utilizzo dei dati per i set di dati e i campi utilizzando l’API [!DNL Dataset Service].

Dopo aver aggiunto le etichette di utilizzo dei dati a livello di set di dati e di campo, puoi iniziare a inserire i dati in [!DNL Experience Platform]. Per ulteriori informazioni, inizia leggendo la [documentazione sull&#39;acquisizione dei dati](../../ingestion/home.md).

È inoltre possibile definire criteri di utilizzo dei dati in base alle etichette applicate. Per ulteriori informazioni, consulta la [panoramica dei criteri di utilizzo dei dati](../policies/overview.md).

Per ulteriori informazioni sulla gestione dei set di dati in [!DNL Experience Platform], consulta la [panoramica dei set di dati](../../catalog/datasets/overview.md).

## Appendice {#appendix}

La sezione seguente contiene informazioni aggiuntive sull’utilizzo delle etichette tramite l’API Servizio set di dati.

### [!DNL If-Match] header  {#if-match}

Quando si eseguono chiamate API che aggiornano le etichette esistenti di un set di dati (PUT e DELETE), deve essere inclusa un’intestazione `If-Match` che indica la versione corrente dell’entità etichetta di set di dati nel servizio set di dati. Per evitare conflitti tra dati, il servizio aggiorna l’entità set di dati solo se la stringa inclusa `If-Match` corrisponde al tag di versione più recente generato dal sistema per quel set di dati.

>[!NOTE]
>
>Se non esistono attualmente etichette per il set di dati in questione, è possibile aggiungere nuove etichette solo tramite una richiesta POST, che non richiede un’intestazione `If-Match`. Una volta aggiunte le etichette a un set di dati, viene assegnato un valore `etag` che può essere utilizzato per aggiornare o rimuovere le etichette in un secondo momento.

Per recuperare la versione più recente dell&#39;entità dataset-label, effettua una [richiesta di GET](#look-up) all&#39;endpoint `/datasets/{DATASET_ID}/labels`. Il valore corrente viene restituito nella risposta sotto un&#39;intestazione `etag` . Quando si aggiornano le etichette dei set di dati esistenti, è consigliabile eseguire prima una richiesta di ricerca per il set di dati per recuperare il valore `etag` più recente prima di utilizzare tale valore nell’intestazione `If-Match` della richiesta PUT o DELETE successiva.
