---
keywords: ' Experience Platform;home;argomenti popolari'
solution: Experience Platform
title: Endpoint etichette
topic: developer guide
description: Scoprite come gestire le etichette di utilizzo dei dati in  Experience Platform utilizzando l'API del servizio criteri.
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 3%

---


# Endpoint etichette

Le etichette di utilizzo dei dati consentono di classificare i dati in base ai criteri di utilizzo che possono essere applicati a tali dati. L&#39;endpoint `/labels` in [!DNL Policy Service API] consente di gestire le etichette di utilizzo dei dati a livello di codice all&#39;interno dell&#39;applicazione dell&#39;esperienza.

>[!NOTE]
>
>L&#39;endpoint `/labels` viene utilizzato solo per recuperare, creare e aggiornare le etichette di utilizzo dei dati. Per i passaggi su come aggiungere etichette ai set di dati e ai campi utilizzando le chiamate API, fare riferimento alla guida sulla [gestione delle etichette dei set di dati](../labels/dataset-api.md).

## Introduzione

L&#39;endpoint API utilizzato in questa guida è parte del [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Prima di continuare, consultare la [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per eseguire correttamente chiamate a qualsiasi API [!DNL Experience Platform].

## Recupera un elenco di etichette {#list}

È possibile elencare tutte le etichette `core` o `custom` effettuando una richiesta di GET rispettivamente a `/labels/core` o `/labels/custom`.

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

Una risposta corretta restituisce un elenco di etichette personalizzate recuperate dal sistema. Poiché la richiesta di esempio sopra è stata effettuata su `/labels/custom`, la risposta riportata di seguito mostra solo etichette personalizzate.

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

## Cercare un&#39;etichetta {#look-up}

È possibile ricercare un&#39;etichetta specifica inserendo la proprietà `name` dell&#39;etichetta nel percorso di una richiesta di GET all&#39;API [!DNL Policy Service].

**Formato API**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{LABEL_NAME}` | La proprietà `name` dell&#39;etichetta personalizzata da ricercare. |

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

## Creare o aggiornare un&#39;etichetta personalizzata {#create-update}

Per creare o aggiornare un&#39;etichetta personalizzata, è necessario effettuare una richiesta di PUT all&#39;API [!DNL Policy Service].

**Formato API**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{LABEL_NAME}` | La proprietà `name` di un&#39;etichetta personalizzata. Se non esiste un&#39;etichetta personalizzata con questo nome, verrà creata una nuova etichetta. Se ne esiste uno, l&#39;etichetta verrà aggiornata. |

**Richiesta**

La richiesta seguente crea una nuova etichetta, `L3`, che ha lo scopo di descrivere i dati che contengono informazioni relative ai piani di pagamento selezionati dai clienti.

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
| `category` | La categoria dell&#39;etichetta. Sebbene sia possibile creare le proprie categorie per le etichette personalizzate, si consiglia vivamente di utilizzare `Custom` se si desidera che l&#39;etichetta venga visualizzata nell&#39;interfaccia utente. |
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

## Passaggi successivi

Questa guida riguardava l&#39;utilizzo dell&#39;endpoint `/labels` nell&#39;API del servizio criteri. Per i passaggi su come applicare etichette a set di dati e campi, fare riferimento alla [Guida API per le etichette di set di dati](../labels/dataset-api.md).