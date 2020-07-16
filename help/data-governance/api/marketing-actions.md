---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Azioni di marketing
topic: developer guide
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 1%

---


# Azioni di marketing

Un&#39;azione di marketing, nel contesto del Adobe Experience Platform  [!DNL Data Governance], è un&#39;azione che un consumatore di [!DNL Experience Platform] dati esegue, per la quale è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati.

Per utilizzare le azioni di marketing nell&#39;API è necessario utilizzare l&#39; `/marketingActions` endpoint.

## Elenca tutte le azioni di marketing

Per visualizzare un elenco di tutte le azioni di marketing, è possibile effettuare una richiesta GET `/marketingActions/core` o `/marketingActions/custom` che restituisca tutti i criteri per il contenitore specificato.

**Formato API**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Richiesta**

La richiesta seguente restituirà un elenco di tutte le azioni di marketing personalizzate definite dall&#39;Organizzazione IMS.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

L&#39;oggetto response fornisce il numero totale di azioni di marketing nel contenitore (`count`) e l&#39; `children` array contiene i dettagli per ogni azione di marketing, inclusi l&#39;azione `name` e un `href` per l&#39;azione di marketing. Questo percorso (`_links.self.href`) viene utilizzato per completare l&#39; `marketingActionsRefs` array durante la [creazione di un criterio](policies.md#create-policy)di utilizzo dei dati.

```JSON
{
    "_page": {
        "start": "sampleMarketingAction",
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

## Cerca un&#39;azione di marketing specifica

Puoi anche eseguire una richiesta di ricerca (GET) per visualizzare i dettagli di una specifica azione di marketing. Questa operazione viene eseguita utilizzando l&#39; `name` azione di marketing. Se il nome è sconosciuto, può essere trovato utilizzando la richiesta di elenco (GET) mostrata in precedenza.

**Formato API**

```http
GET /marketingActions/core/{marketingActionName}
GET /marketingActions/custom/{marketingActionName}
```

**Richiesta**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

L&#39;oggetto response contiene i dettagli dell&#39;azione di marketing, incluso il percorso (`_links.self.href`) necessario per fare riferimento all&#39;azione di marketing durante la definizione di un criterio di utilizzo dei dati (`marketingActionsRefs`).

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

## Creazione o aggiornamento di un&#39;azione di marketing

L&#39; [!DNL Policy Service] API consente di definire azioni di marketing personalizzate e di aggiornare quelle esistenti. La creazione e l&#39;aggiornamento vengono entrambi eseguiti utilizzando un&#39;operazione PUT con il nome dell&#39;azione di marketing.

**Formato API**

```http
PUT /marketingActions/custom/{marketingActionName}
```

**Richiesta**

Nella richiesta seguente, tenete presente che il payload della richiesta `name` è uguale a quello `{marketingActionName}` nella chiamata API. A differenza `id` di un criterio di sola lettura e generato dal sistema, la creazione di un&#39;azione di marketing richiede di fornire il nome _previsto_ per l&#39;azione di marketing al momento della creazione.

>[!NOTE]
>
>Se non viene fornito il contenuto `{marketingActionName}` della chiamata, si verificherà un errore 405 (Metodo non consentito) in quanto non è consentito eseguire direttamente un PUT all’ `/marketingActions/custom` endpoint. Inoltre, se il payload `name` nel payload non corrisponde a quello `{marketingActionName}` nel percorso, riceverete un errore 400 (Richiesta non valida).

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

**Risposta**

Se creata correttamente, riceverete uno stato HTTP 201 (Creato) e il corpo della risposta conterrà i dettagli dell&#39;azione di marketing appena creata. Il contenuto `name` della risposta deve corrispondere a quello inviato nella richiesta.

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

## Eliminazione di un&#39;azione di marketing

È possibile eliminare le azioni di marketing inviando una richiesta DELETE all&#39;azione `{marketingActionName}` di marketing che si desidera rimuovere.

>[!NOTE]
>
>Non puoi eliminare azioni di marketing a cui fanno riferimento i criteri esistenti. Se si tenta di farlo, si verificherà un errore 400 (Richiesta non valida) con un messaggio di errore che include gli `id` (o più ID) di qualsiasi criterio (o criterio) contenente un riferimento all&#39;azione di marketing che si sta tentando di eliminare.

**Formato API**

```http
DELETE /marketingActions/custom/{marketingActionName}
```

**Richiesta**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Se l’azione di marketing è stata eliminata correttamente, il corpo della risposta sarà vuoto con lo stato HTTP 200 (OK).

Puoi confermare l&#39;eliminazione cercando di cercare (GET) l&#39;azione di marketing. Dovresti ricevere uno stato HTTP 404 (non trovato) insieme a un messaggio di errore &quot;Non trovato&quot; perché l’azione di marketing è stata rimossa.
