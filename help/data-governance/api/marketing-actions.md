---
keywords: ' Experience Platform;home;argomenti popolari;Applicazione delle regole;azioni di marketing api;applicazione basata sulle API;governance dei dati'
solution: Experience Platform
title: Endpoint API di Marketing Actions
topic: developer guide
description: Un'azione di marketing, nel contesto di Adobe Experience Platform Data Governance, è un'azione che un consumatore di dati di Experience Platform  intraprende, per la quale è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 2%

---


# Endpoint delle azioni di marketing

Un&#39;azione di marketing, nel contesto dell&#39;Adobe Experience Platform [!DNL Data Governance], è un&#39;azione eseguita da un consumatore di dati [!DNL Experience Platform] per la quale è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati.

Puoi gestire le azioni di marketing per la tua organizzazione utilizzando l&#39;endpoint `/marketingActions` nell&#39;API del servizio criteri.

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte dell&#39; [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Prima di continuare, consultare la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per eseguire correttamente chiamate a qualsiasi API [!DNL Experience Platform].

## Recupera un elenco di azioni di marketing {#list}

Puoi recuperare un elenco di azioni di marketing di base o personalizzate effettuando una richiesta di GET a `/marketingActions/core` o `/marketingActions/custom`, rispettivamente.

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

Una risposta corretta restituisce i dettagli per ogni azione di marketing recuperata, inclusi i valori `name` e `href`. Il valore `href` viene utilizzato per identificare l&#39;azione di marketing durante la creazione di [criteri di utilizzo dei dati](policies.md#create-policy).

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
| `children` | Un array di oggetti che contiene i dettagli delle azioni di marketing recuperate. |
| `name` | Nome dell&#39;azione di marketing, che funge da identificatore univoco quando [cerca un&#39;azione di marketing specifica](#lookup). |
| `_links.self.href` | Un riferimento URI per l&#39;azione di marketing, che può essere utilizzato per completare l&#39;array `marketingActionsRefs` durante la creazione di un criterio di utilizzo dei dati](policies.md#create-policy).[ |

## Cerca un&#39;azione di marketing specifica {#lookup}

Puoi cercare i dettagli di una specifica azione di marketing inserendo la proprietà `name` dell&#39;azione di marketing nel percorso di una richiesta di GET.

**Formato API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | La proprietà `name` dell&#39;azione di marketing da ricercare. |

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

L&#39;oggetto response contiene i dettagli dell&#39;azione di marketing, incluso il percorso (`_links.self.href`) necessario per fare riferimento all&#39;azione di marketing quando si definisce un criterio di utilizzo dei dati [](policies.md#create-policy) (`marketingActionsRefs`).

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

## Creare o aggiornare un&#39;azione di marketing personalizzata {#create-update}

Puoi creare una nuova azione di marketing personalizzata, o aggiornarne una esistente, includendo il nome esistente o previsto dell&#39;azione di marketing nel percorso di una richiesta di PUT.

**Formato API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell&#39;azione di marketing da creare o aggiornare. Se nel sistema esiste già un&#39;azione di marketing con il nome specificato, tale azione di marketing viene aggiornata. Se non esiste, viene creata una nuova azione di marketing per il nome fornito. |

**Richiesta**

La richiesta seguente crea una nuova azione di marketing denominata `crossSiteTargeting`, a condizione che nel sistema non esista ancora un&#39;azione di marketing con lo stesso nome. Se esiste un&#39;azione di marketing `crossSiteTargeting`, questa chiamata aggiorna l&#39;azione di marketing in base alle proprietà fornite nel payload.

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
| `name` | Nome dell&#39;azione di marketing da creare o aggiornare. <br><br>**IMPORTANTE**: Questa proprietà deve corrispondere al percorso,  `{MARKETING_ACTION_NAME}` in caso contrario si verificherà un errore HTTP 400 (Richiesta non valida). In altre parole, una volta creata un&#39;azione di marketing, la relativa proprietà `name` non può essere modificata. |
| `description` | Una descrizione facoltativa per fornire ulteriore contesto all&#39;azione di marketing. |

**Risposta**

Una risposta corretta restituisce i dettagli dell’azione di marketing. Se un&#39;azione di marketing esistente è stata aggiornata, la risposta restituisce lo stato HTTP 200 (OK). Se è stata creata una nuova azione di marketing, la risposta restituisce lo stato HTTP 201 (Creato).

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

## Eliminazione di un&#39;azione di marketing personalizzata {#delete}

Puoi eliminare un&#39;azione di marketing personalizzata inserendone il nome nel percorso di una richiesta di DELETE.

>[!NOTE]
>
>Le azioni di marketing cui fanno riferimento i criteri esistenti non possono essere eliminate. Se si tenta di eliminare una di queste azioni di marketing, si verificherà un errore HTTP 400 (Richiesta non valida) con un messaggio che include gli ID di tutti i criteri che fanno riferimento all&#39;azione di marketing.

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

Puoi confermare l&#39;eliminazione cercando di [ricercare l&#39;azione di marketing](#look-up). Se l’azione di marketing è stata rimossa dal sistema, riceverai un errore HTTP 404 (non trovato).
