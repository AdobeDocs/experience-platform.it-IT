---
keywords: Experience Platform;home;argomenti popolari;applicazione dei criteri;api delle azioni di marketing;applicazione basata su API;governance dei dati
solution: Experience Platform
title: Endpoint API per le azioni di marketing
topic-legacy: developer guide
description: Un’azione di marketing, nel contesto della governance dei dati di Adobe Experience Platform, è un’azione eseguita da un consumatore di dati di Experience Platform per la quale è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati.
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 3%

---

# Endpoint azione marketing

Un’azione di marketing, nel contesto della governance dei dati di Adobe Experience Platform, è un’azione che [!DNL Experience Platform] prende i dati del consumatore, per i quali è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati.

Puoi gestire le azioni di marketing per la tua organizzazione utilizzando la `/marketingActions` endpoint nell&#39;API del servizio criteri.

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte del [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio presenti in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi [!DNL Experience Platform] API.

## Recupera un elenco di azioni di marketing {#list}

Puoi recuperare un elenco delle azioni di marketing principali o personalizzate effettuando una richiesta GET a `/marketingActions/core` o `/marketingActions/custom`, rispettivamente.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli di ogni azione di marketing recuperata, inclusa la relativa `name` e `href`. La `href` viene utilizzato per identificare l’azione di marketing quando [creazione di un criterio di utilizzo dati](policies.md#create-policy).

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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `name` | Il nome dell’azione di marketing, che agisce come identificatore univoco quando [ricerca di un’azione di marketing specifica](#lookup). |
| `_links.self.href` | Un riferimento URI per l’azione di marketing, che può essere utilizzato per completare il `marketingActionsRefs` quando [creazione di un criterio di utilizzo dati](policies.md#create-policy). |

## Ricerca di un’azione di marketing specifica {#lookup}

Puoi cercare i dettagli di una specifica azione di marketing includendo le `name` nel percorso di una richiesta GET.

**Formato API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | La `name` proprietà dell’azione di marketing che desideri cercare. |

**Richiesta**

La richiesta seguente recupera un’azione di marketing personalizzata denominata `combineData`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

L&#39;oggetto response contiene i dettagli dell&#39;azione di marketing, incluso il percorso (`_links.self.href`) necessaria per fare riferimento all’azione di marketing quando [definizione di un criterio di utilizzo dei dati](policies.md#create-policy) (`marketingActionsRefs`).

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{ORG_ID}",
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

## Creare o aggiornare un’azione di marketing personalizzata {#create-update}

Puoi creare una nuova azione di marketing personalizzata o aggiornare una esistente includendo il nome esistente o previsto dell’azione di marketing nel percorso di una richiesta di PUT.

**Formato API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell’azione di marketing da creare o aggiornare. Se nel sistema esiste già un’azione di marketing con il nome specificato, l’azione di marketing viene aggiornata. Se non esiste, viene creata una nuova azione di marketing per il nome fornito. |

**Richiesta**

La seguente richiesta crea una nuova azione di marketing denominata `crossSiteTargeting`, purché nel sistema non esista ancora un’azione di marketing con lo stesso nome. Se `crossSiteTargeting` esiste un’azione di marketing, questa chiamata aggiorna invece tale azione di marketing in base alle proprietà fornite nel payload.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome dell’azione di marketing da creare o aggiornare. <br><br>**IMPORTANTE**: Questa proprietà deve corrispondere al `{MARKETING_ACTION_NAME}` nel percorso , in caso contrario si verificherà un errore HTTP 400 (Bad Request). In altre parole, una volta creata un’azione di marketing, la `name` impossibile modificare la proprietà. |
| `description` | Una descrizione facoltativa per fornire ulteriore contesto per l’azione di marketing. |

**Risposta**

Una risposta corretta restituisce i dettagli dell’azione di marketing. Se è stata aggiornata un&#39;azione di marketing esistente, la risposta restituisce lo stato HTTP 200 (OK). Se è stata creata una nuova azione di marketing, la risposta restituisce lo stato HTTP 201 (Creato).

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{ORG_ID}",
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 (OK) con un corpo di risposta vuoto.

Puoi confermare l’eliminazione tentando di [cerca l’azione di marketing](#look-up). Dovresti ricevere un errore HTTP 404 (Non trovato) se l’azione di marketing è stata rimossa dal sistema.
