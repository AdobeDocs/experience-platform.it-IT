---
keywords: Experience Platform;home;argomenti popolari;Applicazione dei criteri;azioni di marketing api;applicazione basata su API;governance dei dati
solution: Experience Platform
title: Endpoint API per azioni di marketing
description: Un’azione di marketing, nel contesto della governance dei dati di Adobe Experience Platform, è un’azione eseguita da un consumatore di dati Experience Platform, per la quale è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati.
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 3%

---

# Endpoint &quot;marketing actions&quot;

Un’azione di marketing, nel contesto della governance dei dati di Adobe Experience Platform, è un’azione che [!DNL Experience Platform] dati richiesti dal consumatore, per i quali è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati.

Puoi gestire le azioni di marketing per la tua organizzazione utilizzando `/marketingActions` nell’API del servizio criteri.

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte del [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Prima di continuare, controlla [guida introduttiva](./getting-started.md) per collegamenti alla documentazione correlata, una guida per la lettura delle chiamate API di esempio di questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a [!DNL Experience Platform] API.

## Recuperare un elenco di azioni di marketing {#list}

Per recuperare un elenco di azioni di marketing core o personalizzate, devi effettuare una richiesta GET a `/marketingActions/core` o `/marketingActions/custom`, rispettivamente.

**Formato API**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Richiesta**

La richiesta seguente recupera un elenco di azioni di marketing personalizzate gestite dall’organizzazione.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli di ogni azione di marketing recuperata, inclusi i relativi `name` e `href`. Il `href` viene utilizzato per identificare l’azione di marketing quando [creazione di un criterio di utilizzo dei dati](policies.md#create-policy).

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
| `children` | Array di oggetti che contengono i dettagli delle azioni di marketing recuperate. |
| `name` | Il nome dell’azione di marketing, che funge da identificatore univoco quando [ricerca di un’azione di marketing specifica](#lookup). |
| `_links.self.href` | Un riferimento URI per l’azione di marketing, che può essere utilizzato per completare `marketingActionsRefs` array quando [creazione di un criterio di utilizzo dei dati](policies.md#create-policy). |

## Cercare un’azione di marketing specifica {#lookup}

Per cercare i dettagli di una specifica azione di marketing, devi includere i `name` nel percorso di una richiesta GET.

**Formato API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Il `name` dell’azione di marketing che desideri cercare. |

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

L’oggetto di risposta contiene i dettagli dell’azione di marketing, incluso il percorso (`_links.self.href`) necessario per fare riferimento all’azione di marketing quando [definizione di un criterio di utilizzo dei dati](policies.md#create-policy) (`marketingActionsRefs`).

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

Puoi creare una nuova azione di marketing personalizzata o aggiornarne una esistente includendo il nome esistente o previsto dell’azione di marketing nel percorso di una richiesta PUT.

**Formato API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell’azione di marketing da creare o aggiornare. Se nel sistema esiste già un’azione di marketing con il nome fornito, tale azione viene aggiornata. Se non esiste, viene creata una nuova azione di marketing per il nome fornito. |

**Richiesta**

La richiesta seguente crea una nuova azione di marketing denominata `crossSiteTargeting`, a condizione che nel sistema non esista ancora un’azione di marketing con lo stesso nome. Se un `crossSiteTargeting` l’azione di marketing esiste, ma aggiorna tale azione di marketing in base alle proprietà fornite nel payload.

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
| `name` | Nome dell’azione di marketing da creare o aggiornare. <br><br>**IMPORTANTE**: questa proprietà deve corrispondere al valore `{MARKETING_ACTION_NAME}` nel percorso, altrimenti si verificherà un errore HTTP 400 (Richiesta non valida). In altre parole, una volta creata un’azione di marketing, `name` non può essere modificata. |
| `description` | Una descrizione facoltativa per fornire ulteriore contesto per l’azione di marketing. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli dell’azione di marketing. Se è stata aggiornata un’azione di marketing esistente, la risposta restituisce lo stato HTTP 200 (OK). Se è stata creata una nuova azione di marketing, la risposta restituisce lo stato HTTP 201 (Creato).

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

Per eliminare un’azione di marketing personalizzata, devi includere il relativo nome nel percorso di una richiesta DELETE.

>[!NOTE]
>
>Le azioni di marketing a cui fanno riferimento i criteri esistenti non possono essere eliminate. Il tentativo di eliminare una di queste azioni di marketing genera un errore HTTP 400 (Richiesta non valida) insieme a un messaggio che include gli ID di tutti i criteri che fanno riferimento all’azione di marketing.

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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 (OK) con un corpo di risposta vuoto.

Puoi confermare l’eliminazione tentando di: [cercare l’azione di marketing](#look-up). Se l’azione di marketing è stata rimossa dal sistema, dovresti ricevere un errore HTTP 404 (Non trovato).
