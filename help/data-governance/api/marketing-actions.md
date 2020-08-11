---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Azioni di marketing
topic: developer guide
translation-type: tm+mt
source-git-commit: cb3a17aa08c67c66101cbf3842bf306ebcca0305
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 2%

---


# Endpoint delle azioni di marketing

Un&#39;azione di marketing, nel contesto dell&#39;Adobe Experience Platform [!DNL Data Governance], è un&#39;azione eseguita da un consumatore di [!DNL Experience Platform] dati, per la quale è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati.

Puoi gestire le azioni di marketing per la tua organizzazione utilizzando l&#39; `/marketingActions` endpoint nell&#39;API del servizio criteri.

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte dell&#39; [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Prima di continuare, consultate la guida [introduttiva per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente chiamate a qualsiasi](./getting-started.md) [!DNL Experience Platform] API.

## Recupera un elenco di azioni di marketing {#list}

Puoi recuperare un elenco di azioni di marketing di base o personalizzate effettuando una richiesta di GET a `/marketingActions/core` o, rispettivamente, `/marketingActions/custom`a.

**Formato API**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Richiesta**

La richiesta seguente recupera un elenco di azioni di marketing personalizzate gestite dalla tua organizzazione.

```sh
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli per ogni azione di marketing recuperata, inclusi i relativi `name` e `href`. Il `href` valore viene utilizzato per identificare l&#39;azione di marketing durante la [creazione di un criterio](policies.md#create-policy)di utilizzo dei dati.

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
| `name` | Nome dell&#39;azione di marketing, che funge da identificatore univoco quando si [cerca una specifica azione](#lookup)di marketing. |
| `_links.self.href` | Un riferimento URI per l&#39;azione di marketing, che può essere utilizzato per completare l&#39; `marketingActionsRefs` array durante la [creazione di un criterio](policies.md#create-policy)di utilizzo dei dati. |

## Cerca un&#39;azione di marketing specifica {#lookup}

Puoi cercare i dettagli di una specifica azione di marketing inserendo la `name` proprietà dell&#39;azione di marketing nel percorso di una richiesta di GET.

**Formato API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | La `name` proprietà dell’azione di marketing da ricercare. |

**Richiesta**

La richiesta seguente recupera un&#39;azione di marketing personalizzata denominata `combineData`.

```sh
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

L&#39;oggetto response contiene i dettagli dell&#39;azione di marketing, incluso il percorso (`_links.self.href`) necessario per fare riferimento all&#39;azione di marketing durante la [definizione di un criterio](policies.md#create-policy) di utilizzo dei dati (`marketingActionsRefs`).

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

## Creazione o aggiornamento di un&#39;azione di marketing personalizzata {#create-update}

Puoi creare una nuova azione di marketing personalizzata, o aggiornarne una esistente, includendo il nome esistente o previsto dell&#39;azione di marketing nel percorso di una richiesta di PUT.

**Formato API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell&#39;azione di marketing da creare o aggiornare. Se nel sistema esiste già un&#39;azione di marketing con il nome specificato, tale azione di marketing viene aggiornata. Se non esiste, viene creata una nuova azione di marketing per il nome fornito. |

**Richiesta**

La richiesta seguente crea una nuova azione di marketing denominata `crossSiteTargeting`, a condizione che nel sistema non esista ancora un&#39;azione di marketing con lo stesso nome. Se esiste un&#39;azione `crossSiteTargeting` di marketing, questa chiamata aggiorna invece l&#39;azione di marketing in base alle proprietà fornite nel payload.

```sh
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
| `name` | Nome dell&#39;azione di marketing da creare o aggiornare. <br><br>**IMPORTANTE **: Questa proprietà deve corrispondere al percorso`{MARKETING_ACTION_NAME}`in caso contrario si verificherà un errore HTTP 400 (Richiesta non valida). In altre parole, una volta creata un&#39;azione di marketing, non sarà più possibile modificarne`name`la proprietà. |
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
>Non è possibile eliminare le azioni di marketing a cui fanno riferimento i criteri esistenti. Se si tenta di eliminare una di queste azioni di marketing, si verificherà un errore HTTP 400 (Richiesta non valida) con un messaggio che include gli ID di tutti i criteri che fanno riferimento all&#39;azione di marketing.

**Formato API**

```http
DELETE /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nome dell’azione di marketing da eliminare. |

**Richiesta**

```sh
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 (OK) con un corpo di risposta vuoto.

Puoi confermare l’eliminazione cercando di [ricercare l’azione](#look-up)di marketing. Se l’azione di marketing è stata rimossa dal sistema, riceverai un errore HTTP 404 (non trovato).
