---
keywords: Experience Platform;home;argomenti popolari;applicazione dei criteri;api delle azioni di marketing;applicazione basata su API;governance dei dati
solution: Experience Platform
title: Endpoint API per le azioni di marketing
topic-legacy: developer guide
description: Un’azione di marketing, nel contesto della governance dei dati di Adobe Experience Platform, è un’azione eseguita da un consumatore di dati di Experience Platform per la quale è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati.
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 2%

---

# Endpoint azione marketing

Un’azione di marketing, nel contesto di Adobe Experience Platform [!DNL Data Governance], è un’azione eseguita da un consumatore di dati [!DNL Experience Platform] per la quale è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati.

Puoi gestire le azioni di marketing per la tua organizzazione utilizzando l’endpoint `/marketingActions` nell’API del servizio criteri.

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte di [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla relativa documentazione, una guida per la lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API [!DNL Experience Platform].

## Recupera un elenco di azioni di marketing {#list}

Puoi recuperare un elenco delle azioni di marketing principali o personalizzate effettuando una richiesta di GET rispettivamente a `/marketingActions/core` o `/marketingActions/custom`.

**Formato API**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Richiesta**

La richiesta seguente recupera un elenco di azioni di marketing personalizzate gestite dalla tua organizzazione.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli di ogni azione di marketing recuperata, compresi i relativi `name` e `href`. Il valore `href` viene utilizzato per identificare l&#39;azione di marketing durante la [creazione di un criterio di utilizzo dei dati](policies.md#create-policy).

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/marketingActions/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "sampleMarketingAction",
            "description": "Marketing Action description.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550714012088,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714012088,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550793833224,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550793833224,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `_page.count` | Numero totale di azioni di marketing restituite. |
| `children` | Matrice di oggetti che contiene i dettagli delle azioni di marketing recuperate. |
| `name` | Il nome dell&#39;azione di marketing, che agisce come identificatore univoco quando [cerca un&#39;azione di marketing specifica](#lookup). |
| `_links.self.href` | Un riferimento URI per l’azione di marketing, che può essere utilizzato per completare la matrice `marketingActionsRefs` durante la creazione di un criterio di utilizzo dei dati](policies.md#create-policy).[ |

## Cerca un&#39;azione di marketing specifica {#lookup}

Puoi cercare i dettagli di una specifica azione di marketing includendo la proprietà `name` dell’azione di marketing nel percorso di una richiesta di GET.

**Formato API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | La proprietà `name` dell’azione di marketing che desideri cercare. |

**Richiesta**

La richiesta seguente recupera un&#39;azione di marketing personalizzata denominata `combineData`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

L&#39;oggetto response contiene i dettagli dell&#39;azione di marketing, incluso il percorso (`_links.self.href`) necessario per fare riferimento all&#39;azione di marketing quando [si definisce un criterio di utilizzo dei dati](policies.md#create-policy) (`marketingActionsRefs`).

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{IMS_ORG}",
    "created": 1550793805590,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550793805590,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
        }
    }
}
```

## Crea o aggiorna un&#39;azione di marketing personalizzata {#create-update}

Puoi creare una nuova azione di marketing personalizzata o aggiornare una esistente includendo il nome esistente o previsto dell’azione di marketing nel percorso di una richiesta di PUT.

**Formato API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell’azione di marketing da creare o aggiornare. Se nel sistema esiste già un’azione di marketing con il nome specificato, l’azione di marketing viene aggiornata. Se non esiste, viene creata una nuova azione di marketing per il nome fornito. |

**Richiesta**

La richiesta seguente crea una nuova azione di marketing denominata `crossSiteTargeting`, purché nel sistema non sia ancora presente un’azione di marketing con lo stesso nome. Se esiste un’azione di marketing `crossSiteTargeting`, questa chiamata aggiorna invece tale azione di marketing in base alle proprietà fornite nel payload.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome dell’azione di marketing da creare o aggiornare. <br><br>**IMPORTANTE**: Questa proprietà deve corrispondere a  `{MARKETING_ACTION_NAME}` nel percorso, altrimenti si verificherà un errore HTTP 400 (Bad Request). In altre parole, una volta creata un’azione di marketing, la relativa proprietà `name` non può essere modificata. |
| `description` | Una descrizione facoltativa per fornire ulteriore contesto per l’azione di marketing. |

**Risposta**

Una risposta corretta restituisce i dettagli dell’azione di marketing. Se è stata aggiornata un&#39;azione di marketing esistente, la risposta restituisce lo stato HTTP 200 (OK). Se è stata creata una nuova azione di marketing, la risposta restituisce lo stato HTTP 201 (Creato).

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{IMS_ORG}",
    "created": 1550713341915,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550713856390,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
        }
    }
}
```

## Eliminare un’azione di marketing personalizzata {#delete}

Puoi eliminare un’azione di marketing personalizzata includendone il nome nel percorso di una richiesta DELETE.

>[!NOTE]
>
>Le azioni di marketing a cui fanno riferimento i criteri esistenti non possono essere eliminate. Il tentativo di eliminare una di queste azioni di marketing si tradurrà in un errore HTTP 400 (Bad Request) insieme a un messaggio che include gli ID di tutti i criteri che fanno riferimento all&#39;azione di marketing.

**Formato API**

```http
DELETE /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell’azione di marketing da eliminare. |

**Richiesta**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 (OK) con un corpo di risposta vuoto.

Puoi confermare l’eliminazione tentando di [cercare l’azione di marketing](#look-up). Dovresti ricevere un errore HTTP 404 (Non trovato) se l’azione di marketing è stata rimossa dal sistema.
