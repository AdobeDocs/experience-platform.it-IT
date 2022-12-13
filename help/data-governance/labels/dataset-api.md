---
keywords: Experience Platform;home;argomenti popolari;api set di dati;gestire l’utilizzo dei dati;api di utilizzo dati
solution: Experience Platform
title: Gestire le etichette di utilizzo dei dati per i set di dati utilizzando le API
topic-legacy: developer guide
description: L’API del servizio Dataset consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte delle funzionalità del catalogo dati di Adobe Experience Platform, ma è separato dall’API del servizio catalogo che gestisce i metadati del set di dati.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 7e4c2ef8089276829604c9d8a8dd20a122b18c7a
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 2%

---

# Gestire le etichette di utilizzo dei dati per i set di dati tramite API

La [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte delle funzionalità del catalogo dati di Adobe Experience Platform, ma è separato dal [!DNL Catalog Service] API che gestisce i metadati del set di dati.

>[!IMPORTANT]
>
>L’applicazione di etichette a livello di set di dati è supportata solo per i casi di utilizzo della governance dei dati. Se stai cercando di creare criteri di accesso per i dati, devi [applicare etichette allo schema](../../xdm/tutorials/labels.md) che il set di dati è basato su. Vedi la panoramica su [controllo dell&#39;accesso basato sugli attributi](../../access-control/abac/overview.md) per ulteriori informazioni.

Questo documento illustra come gestire le etichette per i set di dati e i campi utilizzando [!DNL Dataset Service API]. Per i passaggi su come gestire direttamente le etichette di utilizzo dei dati utilizzando le chiamate API, vedi [guida all’endpoint delle etichette](../api/labels.md) per [!DNL Policy Service API].

## Introduzione

Prima di leggere questa guida, segui i passaggi descritti in [sezione guida introduttiva](../../catalog/api/getting-started.md) nella guida per gli sviluppatori del catalogo per raccogliere le credenziali necessarie per effettuare chiamate a [!DNL Platform] API.

Per effettuare chiamate agli endpoint descritti in questo documento, è necessario disporre di `id` per un set di dati specifico. Se non disponi di questo valore, consulta la guida su [elenco degli oggetti del catalogo](../../catalog/api/list-objects.md) per trovare gli ID dei set di dati esistenti.

## Cercare etichette per un set di dati {#look-up}

Puoi cercare le etichette di utilizzo dei dati applicate a un set di dati esistente effettuando una richiesta di GET al [!DNL Dataset Service] API.

**Formato API**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | L&#39;unico `id` valore del set di dati di cui si desidera cercare le etichette. |

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

Una risposta corretta restituisce le etichette di utilizzo dei dati applicate al set di dati.

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

Puoi creare un set di etichette per un set di dati fornendo loro nel payload di una richiesta di POST o PUT al [!DNL Dataset Service] API. L’utilizzo di uno di questi metodi sovrascrive le etichette esistenti e le sostituisce con quelle fornite nel payload.

**Formato API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | L&#39;unico `id` valore del set di dati per cui si creano le etichette. |

**Richiesta**

La richiesta PUT di esempio riportata di seguito aggiorna le etichette esistenti per un set di dati, nonché un campo specifico all’interno di tale set di dati. I campi forniti nel payload sono gli stessi richiesti per una richiesta POST.

Quando effettui chiamate API che aggiornano le etichette esistenti di un set di dati (PUT), un `If-Match` deve essere inclusa l’intestazione che indica la versione corrente dell’entità di etichetta del set di dati nel Servizio set di dati. Per evitare conflitti tra dati, il servizio aggiorna l’entità set di dati solo se la `If-Match` La stringa corrisponde al tag di versione più recente generato dal sistema per quel set di dati.

>[!NOTE]
>
>Se non esistono attualmente etichette per il set di dati in questione, è possibile aggiungere nuove etichette solo tramite una richiesta POST, che non richiede un `If-Match` intestazione. Una volta aggiunte le etichette a un set di dati, un `etag` viene assegnato un valore che può essere utilizzato per aggiornare o rimuovere le etichette in un secondo momento.

Per recuperare la versione più recente dell’entità dataset-label, effettua una [richiesta GET](#look-up) al `/datasets/{DATASET_ID}/labels` punto finale. Il valore corrente viene restituito nella risposta in un `etag` intestazione. Quando si aggiornano le etichette dei set di dati esistenti, si consiglia di eseguire prima una richiesta di ricerca per il set di dati al fine di recuperare le ultime `etag` prima di utilizzare tale valore nel `If-Match` intestazione della richiesta PUT successiva.

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
| `labels` | Elenco di etichette di utilizzo dei dati da aggiungere al set di dati. |
| `optionalLabels` | Elenco di tutti i singoli campi all’interno del set di dati a cui si desidera aggiungere le etichette. Ogni elemento della matrice deve avere le seguenti proprietà: <br/><br/>`option`: Un oggetto che contiene [!DNL Experience Data Model] Attributi (XDM) del campo. Sono richieste le tre proprietà seguenti:<ul><li>id</code>: URI $id</code> valore dello schema associato al campo.</li><li>contentType</code>: Il tipo di contenuto e il numero di versione dello schema. Deve assumere la forma di uno dei <a href="../../xdm/api/getting-started.md#accept">Accetta intestazioni</a> per una richiesta di ricerca XDM.</li><li>schemaPath</code>: Percorso del campo nello schema del set di dati.</li></ul>`labels`: Elenco di etichette di utilizzo dati da aggiungere al campo. |

**Risposta**

Una risposta corretta restituisce il set aggiornato di etichette per il set di dati.

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

Leggendo questo documento, hai imparato a gestire le etichette di utilizzo dei dati per i set di dati e i campi utilizzando [!DNL Dataset Service] API. Ora puoi definire [criteri di utilizzo dei dati](../policies/overview.md) e [criteri di controllo accessi](../../access-control/abac/ui/policies.md) in base alle etichette applicate.

Per ulteriori informazioni sulla gestione dei set di dati in [!DNL Experience Platform], vedi [panoramica dei set di dati](../../catalog/datasets/overview.md).
