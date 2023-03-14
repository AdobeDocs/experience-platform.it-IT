---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Endpoint API etichette
description: Scopri come gestire le etichette di utilizzo dei dati in Experience Platform utilizzando l’API del servizio criteri.
exl-id: 9a01f65c-01f1-4298-bdcf-b7e00ccfe9f2
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 4%

---

# Endpoint &quot;labels&quot;

Le etichette di utilizzo dei dati consentono di categorizzare i dati in base ai criteri di utilizzo applicabili a tali dati. Il `/labels` endpoint nella [!DNL Policy Service API] consente di gestire in modo programmatico le etichette di utilizzo dei dati all’interno dell’applicazione experience.

>[!NOTE]
>
>Il `/labels` l’endpoint viene utilizzato solo per recuperare, creare e aggiornare le etichette di utilizzo dei dati. Per i passaggi su come aggiungere etichette a set di dati e campi utilizzando le chiamate API, consulta la guida su [gestione delle etichette dei set di dati](../labels/dataset-api.md).

## Introduzione

L’endpoint API utilizzato in questa guida fa parte del [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/). Prima di continuare, controlla [guida introduttiva](getting-started.md) per collegamenti alla documentazione correlata, una guida per la lettura delle chiamate API di esempio di questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a [!DNL Experience Platform] API.

## Recuperare un elenco di etichette {#list}

Puoi elencare tutti `core` o `custom` effettuando una richiesta GET a `/labels/core` o `/labels/custom`, rispettivamente.

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

## Cercare un’etichetta {#look-up}

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

## Creare o aggiornare un’etichetta personalizzata {#create-update}

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

## Passaggi successivi

Questa guida trattava l&#39;utilizzo di `/labels` nell’API del servizio criteri. Per i passaggi su come applicare etichette a set di dati e campi, consulta [guida API per le etichette dei set di dati](../labels/dataset-api.md).
