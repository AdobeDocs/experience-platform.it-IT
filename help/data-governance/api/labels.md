---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Endpoint API per le etichette
topic-legacy: developer guide
description: Scopri come gestire le etichette di utilizzo dei dati in Experience Platform utilizzando l’API del servizio criteri.
exl-id: 9a01f65c-01f1-4298-bdcf-b7e00ccfe9f2
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 4%

---

# Endpoint etichette

Le etichette per l’utilizzo dei dati ti consentono di classificare i dati in base a criteri di utilizzo che possono essere applicati a tali dati. L’endpoint `/labels` in [!DNL Policy Service API] consente di gestire in modo programmatico le etichette di utilizzo dei dati all’interno dell’applicazione di esperienza.

>[!NOTE]
>
>L’endpoint `/labels` viene utilizzato solo per recuperare, creare e aggiornare le etichette di utilizzo dei dati. Per i passaggi su come aggiungere etichette ai set di dati e ai campi utilizzando le chiamate API, consulta la guida sulla [gestione delle etichette dei set di dati](../labels/dataset-api.md).

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte del [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/). Prima di continuare, controlla la [guida introduttiva](getting-started.md) per i collegamenti alla relativa documentazione, una guida per la lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API [!DNL Experience Platform].

## Recupera un elenco di etichette {#list}

È possibile elencare tutte le etichette `core` o `custom` effettuando una richiesta di GET rispettivamente a `/labels/core` o `/labels/custom`.

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

## Cerca un&#39;etichetta {#look-up}

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

## Creare o aggiornare un’etichetta personalizzata {#create-update}

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

## Passaggi successivi

Questa guida ha trattato l’utilizzo dell’endpoint `/labels` nell’API dei servizi criteri. Per i passaggi su come applicare le etichette ai set di dati e ai campi, consulta la [guida API delle etichette dei set di dati](../labels/dataset-api.md).
