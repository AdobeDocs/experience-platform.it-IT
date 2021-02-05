---
keywords: Experience Platform ;home;argomenti più comuni;governance dei dati;criteri di utilizzo dei dati
solution: Experience Platform
title: Creare un criterio di utilizzo dei dati nell'API
topic: policies
type: Tutorial
description: L'API Policy Service consente di creare e gestire i criteri di utilizzo dei dati per determinare quali azioni di marketing possono essere eseguite rispetto ai dati che contengono determinate etichette di utilizzo dei dati. Questo documento fornisce un'esercitazione passo-passo per la creazione di un criterio tramite l'API del servizio criteri.
translation-type: tm+mt
source-git-commit: 55a54463e918fc62378c660ef17f36e2ede471e0
workflow-type: tm+mt
source-wordcount: '1219'
ht-degree: 2%

---


# Creare un criterio di utilizzo dei dati nell&#39;API

[Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) consente di creare e gestire i criteri di utilizzo dei dati per determinare quali azioni di marketing possono essere eseguite rispetto ai dati che contengono determinate etichette di utilizzo dei dati.

Questo documento fornisce un&#39;esercitazione dettagliata per la creazione di un criterio tramite l&#39;API [!DNL Policy Service]. Per una guida più completa alle diverse operazioni disponibili nell&#39;API, vedete la [Guida per gli sviluppatori di Servizi criteri](../api/getting-started.md).

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei seguenti concetti chiave relativi alla creazione e alla valutazione dei criteri:

* [Governance](../home.md) dei dati Adobe Experience Platform: Il framework in base al quale  [!DNL Platform] viene applicata la conformità all&#39;utilizzo dei dati.
   * [Etichette](../labels/overview.md) di utilizzo dati: Le etichette di utilizzo dei dati vengono applicate ai campi di dati XDM, specificando le restrizioni relative alle modalità di accesso ai dati.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standard con cui  [!DNL Platform] organizzare i dati relativi all&#39;esperienza dei clienti.
* [Sandbox](../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Prima di avviare questa esercitazione, consultare la [guida allo sviluppo](../api/getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate all&#39;API [!DNL Policy Service], incluse le intestazioni richieste e come leggere le chiamate API di esempio.

## Definire un&#39;azione di marketing {#define-action}

Nel framework [!DNL Data Governance], un&#39;azione di marketing è un&#39;azione eseguita da un consumatore di dati [!DNL Experience Platform] per la quale è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati.

Il primo passaggio nella creazione di un criterio di utilizzo dei dati consiste nel determinare quale azione di marketing verrà valutata dal criterio. Questa operazione può essere eseguita utilizzando una delle seguenti opzioni:

* [Cerca un&#39;azione di marketing esistente](#look-up)
* [Creare una nuova azione di marketing](#create-new)

### Cerca un&#39;azione di marketing esistente {#look-up}

Puoi cercare le azioni di marketing esistenti da valutare in base al criterio effettuando una richiesta di GET a uno degli endpoint `/marketingActions`.

**Formato API**

A seconda che tu stia cercando un&#39;azione di marketing fornita da [!DNL Experience Platform] o un&#39;azione di marketing personalizzata creata dalla tua organizzazione, utilizza rispettivamente gli endpoint `marketingActions/core` o `marketingActions/custom`.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Richiesta**

La richiesta seguente utilizza l&#39;endpoint `marketingActions/custom`, che raccoglie un elenco di tutte le azioni di marketing definite dall&#39;organizzazione IMS.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce il numero totale di azioni di marketing trovate (`count`) ed elenca i dettagli delle azioni di marketing stesse all&#39;interno dell&#39;array `children`.

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
| `_links.self.href` | Ogni elemento all&#39;interno dell&#39;array `children` contiene un ID URI per l&#39;azione di marketing elencata. |

Quando trovi l&#39;azione di marketing da utilizzare, registra il valore della relativa proprietà `href`. Questo valore viene utilizzato durante il passaggio successivo di [creazione di un criterio](#create-policy).

### Crea una nuova azione di marketing {#create-new}

Puoi creare una nuova azione di marketing eseguendo una richiesta PUT all&#39;endpoint `/marketingActions/custom/` e fornendo un nome per l&#39;azione di marketing alla fine del percorso della richiesta.

**Formato API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Il nome della nuova azione di marketing da creare. Questo nome funge da identificatore principale dell&#39;azione di marketing e deve pertanto essere univoco. La best practice consiste nel assegnare all’azione di marketing un nome descrittivo ma conciso. |

**Richiesta**

La richiesta seguente crea una nuova azione di marketing personalizzata denominata &quot;exportToThirdParty&quot;. Tenere presente che il `name` nel payload della richiesta è uguale al nome fornito nel percorso della richiesta.

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

Registra l&#39;ID URI dell&#39;azione di marketing appena creata, che verrà utilizzata nella fase successiva della creazione di un criterio.

## Creare un criterio {#create-policy}

Per creare un nuovo criterio è necessario fornire l&#39;ID URI di un&#39;azione di marketing con un&#39;espressione delle etichette di utilizzo che ne impediscono l&#39;esecuzione.

Questa espressione è denominata espressione policy ed è un oggetto contenente (A) un&#39;etichetta, (B) un operatore e gli operandi, ma non entrambi. A sua volta, ogni operando è anche un oggetto con espressione di criterio. Ad esempio, un criterio relativo all&#39;esportazione di dati a terzi potrebbe essere vietato se sono presenti etichette `C1 OR (C3 AND C7)`. Questa espressione viene specificata come:

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

Dopo aver configurato l&#39;espressione del criterio, potete creare un nuovo criterio effettuando una richiesta POST all&#39;endpoint `/policies/custom`.

**Formato API**

```http
POST /policies/custom
```

**Richiesta**

La richiesta seguente crea un criterio denominato &quot;Esporta dati a terze parti&quot; fornendo un&#39;azione di marketing e un&#39;espressione di criterio nel payload della richiesta.

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
| `marketingActionRefs` | Un array contenente il valore `href` di un&#39;azione di marketing, ottenuto nel [passaggio precedente](#define-action). Anche se l&#39;esempio precedente elenca una sola azione di marketing, è possibile fornire più azioni. |
| `deny` | L&#39;oggetto policy espressione. Definisce le etichette e le condizioni di utilizzo che potrebbero causare il rifiuto dell&#39;azione di marketing a cui si fa riferimento in `marketingActionRefs`. |

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
| `id` | Valore generato dal sistema di sola lettura che identifica il criterio in modo univoco. |

Registra l&#39;ID URI del criterio appena creato, in quanto viene utilizzato nel passaggio successivo per abilitare il criterio.

## Abilitare il criterio

>[!NOTE]
>
>Anche se questo passaggio è facoltativo se desiderate lasciare il criterio in stato `DRAFT`, tenete presente che per impostazione predefinita il criterio deve avere lo stato impostato su `ENABLED` per poter partecipare alla valutazione. Per informazioni su come fare eccezioni per i criteri nello stato `DRAFT`, vedere la guida relativa all&#39;applicazione dei criteri [.](../enforcement/api-enforcement.md)

Per impostazione predefinita, i criteri con la proprietà `status` impostata su `DRAFT` non partecipano alla valutazione. Potete abilitare il criterio per la valutazione eseguendo una richiesta di PATCH all&#39;endpoint `/policies/custom/` e fornendo l&#39;identificatore univoco per il criterio alla fine del percorso della richiesta.

**Formato API**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{POLICY_ID}` | Il valore `id` del criterio che si desidera abilitare. |

**Richiesta**

La richiesta seguente esegue un&#39;operazione PATCH sulla proprietà `status` del criterio, modificando il valore da `DRAFT` a `ENABLED`.

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
| `value` | Il nuovo valore da assegnare alla proprietà specificata in `path`. Questa richiesta imposta la proprietà `status` del criterio su &quot;ENABLED&quot;. |

**Risposta**

Una risposta di successo restituisce lo stato HTTP 200 (OK) e i dettagli del criterio aggiornato, con la `status` ora impostata su `ENABLED`.

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

Seguendo questa esercitazione hai creato con successo un criterio di utilizzo dei dati per un&#39;azione di marketing. È ora possibile continuare l&#39;esercitazione su [imposizione dei criteri di utilizzo dei dati](../enforcement/api-enforcement.md) per apprendere come verificare la presenza di violazioni dei criteri e gestirle nell&#39;applicazione di esperienza.

Per ulteriori informazioni sulle diverse operazioni disponibili nell&#39;API [!DNL Policy Service], vedere la [Guida per gli sviluppatori di servizi di policy](../api/getting-started.md). Per informazioni su come applicare criteri per i dati [!DNL Real-time Customer Profile], consulta l&#39;esercitazione su [come applicare la conformità all&#39;utilizzo dei dati per i segmenti di pubblico](../../segmentation/tutorials/governance.md).

Per informazioni su come gestire i criteri di utilizzo nell&#39;interfaccia utente [!DNL Experience Platform], vedere la [guida utente dei criteri](user-guide.md).