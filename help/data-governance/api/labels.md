---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Endpoint API etichette
description: Scopri come gestire le etichette di utilizzo dei dati in Experience Platform utilizzando l’API del servizio criteri.
role: Developer
exl-id: 9a01f65c-01f1-4298-bdcf-b7e00ccfe9f2
source-git-commit: 77d68a42b16c78cdc2b55f7776ba1c8ec98d8acd
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 4%

---

# Endpoint &quot;labels&quot;

Le etichette di utilizzo dei dati consentono di categorizzare i dati in base ai criteri di utilizzo applicabili a tali dati. L&#39;endpoint `/labels` in [!DNL Policy Service API] consente di gestire in modo programmatico le etichette di utilizzo dei dati all&#39;interno dell&#39;applicazione Experience.

>[!NOTE]
>
>L&#39;endpoint `/labels` viene utilizzato solo per recuperare, creare e aggiornare le etichette di utilizzo dei dati. Non è possibile eliminare le etichette. Tuttavia, puoi aggiungere o rimuovere etichette ai set di dati e ai campi utilizzando le chiamate API. Per istruzioni, consulta la guida nel documento [gestione delle etichette dei set di dati](../labels/dataset-api.md).

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte di [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/). Prima di continuare, consulta la [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API [!DNL Experience Platform].

## Recuperare un elenco di etichette {#list}

È possibile elencare tutte le etichette `core` o `custom` effettuando una richiesta di GET rispettivamente a `/labels/core` o `/labels/custom`.

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

## Cercare un’etichetta {#look-up}

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

## Creare o aggiornare un’etichetta personalizzata {#create-update}

Per creare o aggiornare un&#39;etichetta personalizzata, è necessario effettuare una richiesta PUT all&#39;API [!DNL Policy Service].

>[!NOTE]
>
>Se si desidera rimuovere le etichette da un set di dati, è possibile eseguire una [richiesta PUT sull&#39;API del servizio Set di dati](../labels/dataset-api.md#remove) oppure utilizzare l&#39;[interfaccia utente Set di dati](../labels/user-guide.md#remove-labels-from-a-dataset).

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

## Passaggi successivi

Questa guida descrive l&#39;utilizzo dell&#39;endpoint `/labels` nell&#39;API del servizio criteri. Per i passaggi su come applicare etichette a set di dati e campi, consulta la [guida API per le etichette dei set di dati](../labels/dataset-api.md).
