---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creazione di un criterio di utilizzo dei dati
topic: policies
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 2%

---


# Creare un criterio di utilizzo dei dati nell&#39;API

L&#39;etichettatura e l&#39;applicazione dell&#39;uso dei dati (DULE) è il meccanismo fondamentale del  Adobe Experience Platform [!DNL Data Governance]. L&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) DULE Policy Service consente di creare e gestire criteri DULE per determinare quali azioni di marketing possono essere eseguite rispetto ai dati che contengono determinate etichette DULE.

Questo documento fornisce un&#39;esercitazione dettagliata per la creazione di un criterio DULE tramite l&#39; [!DNL Policy Service] API. Per una guida più completa alle diverse operazioni disponibili nell&#39;API, vedete la guida [per gli sviluppatori di](../api/getting-started.md)Policy Service.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei seguenti concetti chiave relativi alla creazione e alla valutazione di criteri DULE:

* [!DNL Data Governance](../home.md): Il framework in base al quale [!DNL Platform] viene applicata la conformità all&#39;utilizzo dei dati.
* [Etichette](../labels/overview.md)di utilizzo dati: Le etichette di utilizzo dei dati vengono applicate ai campi di dati XDM, specificando le restrizioni relative alle modalità di accesso ai dati.
* [!DNL Experience Data Model (XDM)](../../xdm/home.md): Il framework standard con cui [!DNL Platform] organizzare i dati relativi all&#39;esperienza del cliente.
* [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Prima di avviare questa esercitazione, consulta la guida [](../api/getting-started.md) allo sviluppatore per informazioni importanti che devi conoscere per effettuare correttamente chiamate all’ [!DNL Policy Service] API DULE, comprese le intestazioni richieste e come leggere le chiamate API di esempio.

## Definire un&#39;azione di marketing {#define-action}

Nel [!DNL Data Governance] quadro, un&#39;azione di marketing è un&#39;azione che un consumatore di [!DNL Experience Platform] dati esegue, per la quale è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati.

Il primo passo per creare un criterio DULE consiste nel determinare quale azione marketing verrà valutata dal criterio. Questa operazione può essere eseguita utilizzando una delle seguenti opzioni:

* [Cerca un&#39;azione di marketing esistente](#look-up)
* [Creare una nuova azione di marketing](#create-new)

### Cerca un&#39;azione di marketing esistente {#look-up}

Puoi cercare le azioni di marketing esistenti da valutare in base al criterio DULE effettuando una richiesta di GET a uno degli `/marketingActions` endpoint.

**Formato API**

A seconda che tu stia cercando un&#39;azione di marketing fornita dalla tua organizzazione [!DNL Experience Platform] o un&#39;azione di marketing personalizzata creata dalla tua organizzazione, usa rispettivamente gli `marketingActions/core` o `marketingActions/custom` gli endpoint.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Richiesta**

La richiesta seguente utilizza l’ `marketingActions/custom` endpoint, che raccoglie un elenco di tutte le azioni di marketing definite dall’organizzazione IMS.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta di successo restituisce il numero totale di azioni di marketing trovate (`count`) ed elenca i dettagli delle azioni di marketing stesse all&#39;interno dell&#39; `children` array.

```json
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
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714012088,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550793833224,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550793833224,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `_links.self.href` | Ogni elemento all&#39;interno dell&#39; `children` array contiene un ID URI per l&#39;azione di marketing elencata. |

Quando trovi l&#39;azione di marketing da utilizzare, registra il valore della relativa `href` proprietà. Questo valore viene utilizzato durante il passaggio successivo della [creazione di un criterio](#create-policy)DULE.

### Creare una nuova azione di marketing {#create-new}

Puoi creare una nuova azione di marketing eseguendo una richiesta di PUT all’ `/marketingActions/custom/` endpoint e fornendo un nome per l’azione di marketing alla fine del percorso della richiesta.

**Formato API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Il nome della nuova azione di marketing da creare. Questo nome funge da identificatore principale dell&#39;azione di marketing e deve pertanto essere univoco. La best practice consiste nel assegnare all’azione di marketing un nome descrittivo ma conciso. |

**Richiesta**

La richiesta seguente crea una nuova azione di marketing personalizzata denominata &quot;exportToThirdParty&quot;. Il payload della richiesta `name` è uguale al nome fornito nel percorso della richiesta.

```shell
curl -X PUT \  
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "exportToThirdParty",
      "description": "Export data to a third party"
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome dell’azione di marketing da creare. Questo nome deve corrispondere al nome fornito nel percorso della richiesta, altrimenti si verificherà un errore 400 (Richiesta non valida). |
| `description` | Una descrizione leggibile dell&#39;azione di marketing. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e i dettagli dell’azione di marketing appena creata.

```json
{
    "name": "exportToThirdParty",
    "description": "Export data to a third party",
    "imsOrg": "{IMS_ORG}",
    "created": 1550713341915,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER",
    "updated": 1550713856390,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
        }
    }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `_links.self.href` | ID URI dell’azione di marketing. |

Registra l&#39;ID URI dell&#39;azione di marketing appena creata, che verrà utilizzata nel passaggio successivo per la creazione di un criterio DULE.

## Creare un criterio DULE {#create-policy}

Per creare un nuovo criterio è necessario fornire l&#39;ID URI di un&#39;azione di marketing con un&#39;espressione delle etichette DULE che vietano tale azione di marketing.

Questa espressione è denominata espressione **** policy ed è un oggetto contenente (A) un&#39;etichetta DULE, oppure (B) un operatore e gli operandi, ma non entrambi. A sua volta, ogni operando è anche un oggetto con espressione di criterio. Ad esempio, un criterio relativo all&#39;esportazione di dati a terzi potrebbe essere vietato se sono presenti `C1 OR (C3 AND C7)` etichette. Questa espressione viene specificata come:

```json
"deny": {
  "operator": "OR",
  "operands": [
    {
      "label": "C1"
    },
    {
      "operator": "AND",
      "operands": [
        {
          "label": "C3"
        },
        {
          "label": "C7"
        }
      ]
    }
  ]
}
```

>[!NOTE]
>
>Sono supportati solo gli operatori OR e AND.

Dopo aver configurato l&#39;espressione del criterio, potete creare un nuovo criterio DULE effettuando una richiesta POST all&#39; `/policies/custom` endpoint.

**Formato API**

```http
POST /policies/custom
```

**Richiesta**

La richiesta seguente crea un criterio DULE denominato &quot;Export Data to Third Party&quot; fornendo un&#39;azione di marketing e un&#39;espressione del criterio nel payload della richiesta.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
      "../marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
      "operator": "OR",
      "operands": [
        {"label": "C1"},
        {
          "operator": "AND",
          "operands": [
            {"label": "C3"},
            {"label": "C7"}
          ]
        }
      ]
    }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `marketingActionRefs` | Un array contenente il `href` valore di un&#39;azione di marketing, ottenuto nel passaggio [](#define-action)precedente. Anche se l&#39;esempio precedente elenca una sola azione di marketing, è possibile fornire più azioni. |
| `deny` | L&#39;oggetto policy espressione. Definisce le etichette e le condizioni DULE che causerebbero il rifiuto dell&#39;azione di marketing a cui si fa riferimento in `marketingActionRefs`. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e i dettagli del criterio appena creato.

```json
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "OR",
        "operands": [
            {
                "label": "C1"
            },
            {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "C7"
                    }
                ]
            }
        ]
    },
    "imsOrg": "{IMS_ORG}",
    "created": 1565651746693,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER",
    "updated": 1565651746693,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
    },
    "id": "5d51f322e553c814e67af1a3"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | Valore generato dal sistema di sola lettura che identifica in modo univoco il criterio DULE. |

Registra l&#39;ID URI del criterio DULE appena creato, in quanto viene utilizzato nel passaggio successivo per abilitare il criterio.

## Abilita criterio DULE

>[!NOTE]
>
>Anche se questo passaggio è facoltativo se desiderate lasciare il criterio DULE nello `DRAFT` stato, tenete presente che per impostazione predefinita un criterio deve avere lo stato impostato su `ENABLED` per poter partecipare alla valutazione. Per informazioni su come fare eccezioni per i criteri di [stato, vedere l&#39;esercitazione sull&#39;applicazione dei criteri](../enforcement/api-enforcement.md) `DRAFT` DULE.

Per impostazione predefinita, i criteri DULE con `status` proprietà impostata per `DRAFT` non partecipano alla valutazione. Potete abilitare il criterio per la valutazione eseguendo una richiesta di PATCH all&#39; `/policies/custom/` endpoint e fornendo l&#39;identificatore univoco per il criterio alla fine del percorso della richiesta.

**Formato API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | Il `id` valore del criterio che si desidera abilitare. |

**Richiesta**

La richiesta seguente esegue un&#39;operazione PATCH sulla `status` proprietà del criterio DULE, modificando il valore da `DRAFT` a `ENABLED`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    {
      "op": "replace",
      "path": "/status",
      "value": "ENABLED"
    }
  ]'
```

| Proprietà | Descrizione |
| --- | --- |
| `op` | Tipo di operazione PATCH da eseguire. Questa richiesta esegue un&#39;operazione di sostituzione. |
| `path` | Percorso del campo da aggiornare. Quando si abilita un criterio, il valore deve essere impostato su &quot;/status&quot;. |
| `value` | Il nuovo valore da assegnare alla proprietà specificata in `path`. Questa richiesta imposta la `status` proprietà del criterio su &quot;ENABLED&quot;. |

**Risposta**

Una risposta di successo restituisce lo stato HTTP 200 (OK) e i dettagli del criterio aggiornato, con `status` la relativa ora impostata su `ENABLED`.

```json
{
    "name": "Export Data to Third Party",
    "status": "ENABLED",
    "marketingActionRefs": [
        "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "OR",
        "operands": [
            {
                "label": "C1"
            },
            {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "C7"
                    }
                ]
            }
        ]
    },
    "imsOrg": "{IMS_ORG}",
    "created": 1565651746693,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER}",
    "updated": 1565723012139,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
    },
    "id": "5d51f322e553c814e67af1a3"
}
```

## Passaggi successivi

Seguendo questa esercitazione hai creato con successo un criterio di utilizzo dei dati per un&#39;azione di marketing. È ora possibile continuare l&#39;esercitazione sull&#39; [applicazione dei criteri](../enforcement/api-enforcement.md) di utilizzo dei dati per apprendere come verificare la presenza di violazioni dei criteri e gestirle nell&#39;applicazione di esperienza.

Per ulteriori informazioni sulle diverse operazioni disponibili nell&#39; [!DNL Policy Service] API, consultate la guida [per gli sviluppatori di](../api/getting-started.md)Policy Service. Per informazioni su come applicare criteri per [!DNL Real-time Customer Profile] i dati, consulta l’esercitazione sull’ [imposizione della conformità per l’utilizzo dei dati da parte dei segmenti](../../segmentation/tutorials/governance.md)di pubblico.

Per informazioni su come gestire i criteri di utilizzo nell&#39;interfaccia [!DNL Experience Platform] utente, consultate la guida [utente ai](user-guide.md)criteri.