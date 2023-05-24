---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API per attributi calcolati
type: Documentation
description: In Adobe Experience Platform, gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento in attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate in segmentazione, attivazione e personalizzazione. Questa guida illustra come creare, visualizzare, aggiornare ed eliminare gli attributi calcolati utilizzando l’API Profilo cliente in tempo reale.
exl-id: 6b35ff63-590b-4ef5-ab39-c36c39ab1d58
hide: true
hidefromtoc: true
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2274'
ht-degree: 3%

---

# Endpoint API per attributi calcolati (Alpha)

>[!IMPORTANT]
>
>La funzionalità degli attributi calcolati descritta in questo documento è attualmente in formato alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento negli attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate in segmentazione, attivazione e personalizzazione. Questa guida include esempi di chiamate API per eseguire operazioni CRUD di base utilizzando `/computedAttributes` endpoint.

Per ulteriori informazioni sugli attributi calcolati, consulta la sezione [panoramica degli attributi calcolati](overview.md).

## Introduzione

L’endpoint API utilizzato in questa guida fa parte del [API Profilo cliente in tempo reale](https://www.adobe.com/go/profile-apis-en).

Prima di continuare, controlla [Guida introduttiva all’API del profilo](../api/getting-started.md) per collegamenti alla documentazione consigliata, una guida per la lettura delle chiamate API di esempio visualizzate in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Configurare un campo attributo calcolato

Per creare un attributo calcolato, devi innanzitutto identificare il campo in uno schema che conterrà il valore dell’attributo calcolato.

Consulta la documentazione su [configurazione di un attributo calcolato](configure-api.md) per una guida end-to-end completa alla creazione di un campo attributo calcolato in uno schema.

>[!WARNING]
>
>Per procedere con la guida API è necessario configurare un campo attributo calcolato.

## Creare un attributo calcolato {#create-a-computed-attribute}

Con il campo attributo calcolato definito nello schema Profilo abilitato, ora puoi configurare un attributo calcolato. Se non lo hai già fatto, segui il flusso di lavoro descritto nella sezione [configurazione di un attributo calcolato](configure-api.md) documentazione.

Per creare un attributo calcolato, inizia effettuando una richiesta POST al `/config/computedAttributes` endpoint con un corpo della richiesta contenente i dettagli dell’attributo calcolato che desideri creare.

**Formato API**

```http
POST /config/computedAttributes
```

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "birthdayCurrentMonth",
        "path": "_{TENANT_ID}",
        "description": "Computed attribute to capture if the customer birthday is in the current month.",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Proprietà | Descrizione |
|---|---|
| `name` | Nome del campo attributo calcolato sotto forma di stringa. |
| `path` | Percorso del campo contenente l’attributo calcolato. Questo percorso si trova all’interno di `properties` dello schema e NON deve includere il nome del campo nel percorso. Durante la scrittura del percorso, ometti i livelli multipli di `properties` attributi. |
| `{TENANT_ID}` | Se non conosci il tuo ID tenant, consulta i passaggi per trovare il tuo ID tenant in [Guida per gli sviluppatori del registro dello schema](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Descrizione dell&#39;attributo calcolato. Questa funzione è particolarmente utile quando sono stati definiti più attributi calcolati, in quanto consente ad altri utenti all’interno dell’organizzazione di determinare l’attributo calcolato corretto da utilizzare. |
| `expression.value` | Un valore valido [!DNL Profile Query Language] espressione (PQL). Gli attributi calcolati supportano attualmente le seguenti funzioni: sum, count, min, max e boolean. Per un elenco delle espressioni di esempio, consulta [espressioni PQL di esempio](expressions.md) documentazione. |
| `schema.name` | Classe su cui si basa lo schema contenente il campo attributo calcolato. Esempio: `_xdm.context.experienceevent` per uno schema basato sulla classe ExperienceEvent XDM. |

**Risposta**

Un attributo calcolato creato correttamente restituisce lo stato HTTP 200 (OK) e un corpo di risposta contenente i dettagli dell’attributo calcolato appena creato. Questi dettagli includono un univoco, di sola lettura, generato dal sistema `id` che possono essere utilizzati per fare riferimento all’attributo calcolato durante altre operazioni API.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

| Proprietà | Descrizione |
|---|---|
| `id` | ID univoco generato dal sistema e di sola lettura, che può essere utilizzato per fare riferimento all’attributo calcolato durante altre operazioni API. |
| `imsOrgId` | L’organizzazione IMS correlata all’attributo calcolato deve corrispondere al valore inviato nella richiesta. |
| `sandbox` | L’oggetto sandbox contiene i dettagli della sandbox in cui è stato configurato l’attributo calcolato. Queste informazioni sono tratte dall’intestazione sandbox inviata nella richiesta. Per ulteriori informazioni, vedere [panoramica sulle sandbox](../../sandboxes/home.md). |
| `positionPath` | Array contenente il decostruito `path` al campo inviato nella richiesta. |
| `returnSchema.meta:xdmType` | Tipo di campo in cui verrà memorizzato l&#39;attributo calcolato. |
| `definedOn` | Matrice che mostra gli schemi di unione su cui è stato definito l’attributo calcolato. Contiene un oggetto per schema di unione, il che significa che possono esserci più oggetti all’interno dell’array se l’attributo calcolato è stato aggiunto a più schemi basati su classi diverse. |
| `active` | Valore booleano che indica se l’attributo calcolato è attualmente attivo o meno. Il valore per impostazione predefinita è `true`. |
| `type` | Il tipo di risorsa creata, in questo caso &quot;ComputedAttribute&quot; è il valore predefinito. |
| `createEpoch` e `updateEpoch` | L’ora in cui l’attributo calcolato è stato creato e aggiornato per ultimo, rispettivamente. |

## Creare un attributo calcolato che faccia riferimento agli attributi calcolati esistenti

È inoltre possibile creare un attributo calcolato che faccia riferimento agli attributi calcolati esistenti. A tal fine, inizia effettuando una richiesta POST al `/config/computedAttributes` endpoint. Il corpo della richiesta conterrà riferimenti agli attributi calcolati nella sezione `expression.value` come mostrato nell’esempio che segue.

**Formato API**

```http
POST /config/computedAttributes
```

**Richiesta**

In questo esempio, sono già stati creati due attributi calcolati che verranno utilizzati per definire un terzo attributo. Gli attributi calcolati esistenti sono:

* **`totalSpend`:** Acquisisce l’importo totale in dollari speso da un cliente.
* **`countPurchases`:** Conta il numero di acquisti effettuati da un cliente.

La richiesta seguente fa riferimento ai due attributi calcolati esistenti, utilizzando un PQL valido da dividere per calcolare il nuovo `averageSpend` attributo calcolato.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "averageSpend",
        "path": "_{TENANT_ID}.purchaseSummary",
        "description": "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Proprietà | Descrizione |
|---|---|
| `name` | Nome del campo attributo calcolato sotto forma di stringa. |
| `path` | Percorso del campo contenente l’attributo calcolato. Questo percorso si trova all’interno di `properties` dello schema e NON deve includere il nome del campo nel percorso. Durante la scrittura del percorso, ometti i livelli multipli di `properties` attributi. |
| `{TENANT_ID}` | Se non conosci il tuo ID tenant, consulta i passaggi per trovare il tuo ID tenant in [Guida per gli sviluppatori del registro dello schema](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Descrizione dell&#39;attributo calcolato. Questa funzione è particolarmente utile quando sono stati definiti più attributi calcolati, in quanto aiuterà gli altri utenti all’interno dell’organizzazione IMS a determinare l’attributo calcolato corretto da utilizzare. |
| `expression.value` | Espressione PQL valida. Gli attributi calcolati supportano attualmente le seguenti funzioni: sum, count, min, max e boolean. Per un elenco delle espressioni di esempio, consulta [espressioni PQL di esempio](expressions.md) documentazione.<br/><br/>In questo esempio, l’espressione fa riferimento a due attributi calcolati esistenti. Per fare riferimento agli attributi, utilizza `path` e `name` dell’attributo calcolato così come appare nello schema in cui sono stati definiti gli attributi calcolati. Ad esempio, il `path` del primo attributo calcolato di riferimento è `_{TENANT_ID}.purchaseSummary` e `name` è `totalSpend`. |
| `schema.name` | Classe su cui si basa lo schema contenente il campo attributo calcolato. Esempio: `_xdm.context.experienceevent` per uno schema basato sulla classe ExperienceEvent XDM. |

**Risposta**

Un attributo calcolato creato correttamente restituisce lo stato HTTP 200 (OK) e un corpo di risposta contenente i dettagli dell’attributo calcolato appena creato. Questi dettagli includono un univoco, di sola lettura, generato dal sistema `id` che possono essere utilizzati per fare riferimento all’attributo calcolato durante altre operazioni API.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "averageSpend",
    "path": "_{TENANT_ID}.purchaseSummary",
    "positionPath": [
        "_{TENANT_ID}",
        "purchaseSummary"
    ],
    "description": "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
    "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "number"
    },
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"\bVR)JMSR())(+KLOJKկHO+I(/(OI/S8{E:",
    "dependencies": [
        "c08a92f3-2418-4a3d-89d0-96f15fda3e5d",
        "4ed9e3aa-57ae-4705-9e8a-7fba9a6a7010"
    ],
    "dependents": [],
    "active": true,
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
      },
    "type": "ComputedAttribute",
    "createEpoch": 1613696592,
    "updateEpoch": 1613696593
}
```

| Proprietà | Descrizione |
|---|---|
| `id` | ID univoco generato dal sistema e di sola lettura, che può essere utilizzato per fare riferimento all’attributo calcolato durante altre operazioni API. |
| `imsOrgId` | L’organizzazione IMS correlata all’attributo calcolato deve corrispondere al valore inviato nella richiesta. |
| `sandbox` | L’oggetto sandbox contiene i dettagli della sandbox in cui è stato configurato l’attributo calcolato. Queste informazioni sono tratte dall’intestazione sandbox inviata nella richiesta. Per ulteriori informazioni, vedere [panoramica sulle sandbox](../../sandboxes/home.md). |
| `positionPath` | Array contenente il decostruito `path` al campo inviato nella richiesta. |
| `returnSchema.meta:xdmType` | Tipo di campo in cui verrà memorizzato l&#39;attributo calcolato. |
| `definedOn` | Matrice che mostra gli schemi di unione su cui è stato definito l’attributo calcolato. Contiene un oggetto per schema di unione, il che significa che possono esserci più oggetti all’interno dell’array se l’attributo calcolato è stato aggiunto a più schemi basati su classi diverse. |
| `active` | Valore booleano che indica se l’attributo calcolato è attualmente attivo o meno. Il valore per impostazione predefinita è `true`. |
| `type` | Il tipo di risorsa creata, in questo caso &quot;ComputedAttribute&quot; è il valore predefinito. |
| `createEpoch` e `updateEpoch` | L’ora in cui l’attributo calcolato è stato creato e aggiornato per ultimo, rispettivamente. |

## Accedere agli attributi calcolati

Quando si utilizzano gli attributi calcolati utilizzando l’API, sono disponibili due opzioni per accedere agli attributi calcolati definiti dall’organizzazione. Il primo consiste nell&#39;elencare tutti gli attributi calcolati, il secondo consiste nel visualizzare un attributo calcolato specifico in base al relativo univoco `id`.

I passaggi per entrambi i modelli di accesso sono descritti in questo documento. Per iniziare, seleziona una delle seguenti opzioni:

* **[Elenca tutti gli attributi calcolati esistenti](#list-all-computed-attributes):** Restituisce un elenco di tutti gli attributi calcolati esistenti creati dall’organizzazione.
* **[Visualizza un attributo calcolato specifico](#view-a-computed-attribute):** Restituisce i dettagli di un singolo attributo calcolato specificandone l’ID durante la richiesta.

### Elenca tutti gli attributi calcolati {#list-all-computed-attributes}

L’organizzazione IMS può creare più attributi calcolati ed eseguire una richiesta GET al `/config/computedAttributes` l’endpoint ti consente di elencare tutti gli attributi calcolati esistenti per la tua organizzazione.

**Formato API**

```http
GET /config/computedAttributes
```

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una risposta corretta include `_page` attributo che fornisce il numero totale di attributi calcolati (`totalCount`) e il numero di attributi calcolati sulla pagina (`pageSize`).

La risposta include anche un `children` matrice composta da uno o più oggetti, ciascuno contenente i dettagli di un attributo calcolato. Se la tua organizzazione non dispone di attributi calcolati, il `totalCount` e `pageSize` sarà 0 (zero) e il valore `children` l’array sarà vuoto.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "birthdayCurrentMonth",
            "path": "person._{TENANT_ID}",
            "positionPath": [
                "person",
                "_{TENANT_ID}"
            ],
            "description": "Computed attribute to capture if the customer birthday is in the current month.",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "person.birthDate.getMonth() = currentMonth()"
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1572555223,
            "updateEpoch": 1572555225
        },
        {
            "id": "ae0c6552-cf49-4725-8979-116366e8e8d3",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "productDownloads",
            "path": "_{TENANT_ID}",
            "positionPath": [
                "_{TENANT_ID}"
            ],
            "description": "Calculate total product downloads.",
            "expression": {
                "type": "PQL", 
                "format": "pql/text", 
                "value":  "let Y = xEvent[_coresvc.event.subType = \"DOWNLOAD\"].groupBy(_coresvc.attributes[name = \"product\"].value).map({
                  \"downloaded\": this.head()._coresvc.attributes[name = \"product\"].head().value,
                  \"downloadsSum\": this.count(),
                  \"downloadsToday\": this[timestamp occurs today].count(),
                  \"downloadsPast30Days\": this[timestamp occurs < 30 days before now].count(),
                  \"downloadsPast60Days\": this[timestamp occurs < 60 days before now].count(),
                  \"downloadsPast90Days\": this[timestamp occurs < 90 days before now].count() }) in { \"uniqueProductDownloadSum\": Y.count(), \"products\": Y }"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "schema": {
                "name": "_xdm.context.profile"
            },
            "encodedDefinedOn": "\u001f?\b\u0000\u0000\u0000\u0000\u0000\u0000\u0000?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?\u0005\u00008{?E:\u0000\u0000\u0000",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1571945277,
            "updateEpoch": 1571945280
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Proprietà | Descrizione |
|---|---|
| `_page.totalCount` | Numero totale di attributi calcolati definiti dall’organizzazione IMS. |
| `_page.pageSize` | Il numero di attributi calcolati restituiti in questa pagina di risultati. Se `pageSize` è uguale a `totalCount`, significa che esiste una sola pagina di risultati e che sono stati restituiti tutti gli attributi calcolati. Se non sono uguali, è possibile accedere ad altre pagine di risultati. Consulta `_links.next` per i dettagli. |
| `children` | Matrice composta da uno o più oggetti, ciascuno contenente i dettagli di un singolo attributo calcolato. Se non sono stati definiti attributi calcolati, il `children` l’array è vuoto. |
| `id` | Valore univoco generato dal sistema e di sola lettura assegnato automaticamente a un attributo calcolato al momento della creazione. Per ulteriori informazioni sui componenti di un oggetto attributo calcolato, consulta la sezione su [creazione di un attributo calcolato](#create-a-computed-attribute) precedenti in questa esercitazione. |
| `_links.next` | Se viene restituita una singola pagina di attributi calcolati, `_links.next` è un oggetto vuoto, come mostrato nella risposta di esempio precedente. Se la tua organizzazione dispone di molti attributi calcolati, questi verranno restituiti su più pagine a cui puoi accedere effettuando una richiesta GET al `_links.next` valore. |

### Visualizzare un attributo calcolato {#view-a-computed-attribute}

Puoi visualizzare un attributo calcolato specifico effettuando una richiesta GET al `/config/computedAttributes` e includendo l’ID attributo calcolato nel percorso della richiesta.

**Formato API**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parametro | Descrizione |
|---|---|
| `{ATTRIBUTE_ID}` | ID dell’attributo calcolato che desideri visualizzare. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

## Aggiornare un attributo calcolato

Se devi aggiornare un attributo calcolato esistente, puoi effettuare una richiesta PATCH al `/config/computedAttributes` e includendo l’ID dell’attributo calcolato che desideri aggiornare nel percorso della richiesta.

**Formato API**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parametro | Descrizione |
|---|---|
| `{ATTRIBUTE_ID}` | ID dell’attributo calcolato che desideri aggiornare. |

**Richiesta**

Questa richiesta utilizza [Formattazione patch JSON](https://datatracker.ietf.org/doc/html/rfc6902) per aggiornare il valore del campo espressione.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type": "PQL", 
            "format": "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| Proprietà | Descrizione |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | Un valore valido [!DNL Profile Query Language] espressione (PQL). Gli attributi calcolati supportano attualmente le seguenti funzioni: sum, count, min, max e boolean. Per un elenco delle espressioni di esempio, consulta [espressioni PQL di esempio](expressions.md) documentazione. |

**Risposta**

In caso di esito positivo, l’aggiornamento restituisce lo stato HTTP 204 (nessun contenuto) e un corpo di risposta vuoto. Se desideri confermare l’esito positivo dell’aggiornamento, puoi eseguire una richiesta di GET per visualizzare l’attributo calcolato in base al relativo ID.

## Eliminare un attributo calcolato

È inoltre possibile eliminare un attributo calcolato utilizzando l’API. A tale scopo, invia una richiesta DELETE al `/config/computedAttributes` e includendo l’ID dell’attributo calcolato che desideri eliminare nel percorso della richiesta.

>[!NOTE]
>
>Presta attenzione durante l’eliminazione di un attributo calcolato, poiché potrebbe essere utilizzato in più schemi e l’operazione DELETE non può essere annullata.

**Formato API**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parametro | Descrizione |
|---|---|
| `{ATTRIBUTE_ID}` | ID dell’attributo calcolato che desideri eliminare. |

**Richiesta**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**Risposta**

In caso di esito positivo, la richiesta di eliminazione restituisce lo stato HTTP 200 (OK) e un corpo di risposta vuoto. Per confermare che l’eliminazione è avvenuta correttamente, puoi eseguire una richiesta GET per cercare l’attributo calcolato in base al relativo ID. Se l&#39;attributo è stato eliminato, verrà visualizzato un errore di stato HTTP 404 (non trovato).

## Creare una definizione di segmento che fa riferimento a un attributo calcolato

Adobe Experience Platform consente di creare segmenti che definiscono un gruppo di attributi o comportamenti specifici da un gruppo di profili. Una definizione di segmento include un’espressione che incapsula una query scritta in PQL. Queste espressioni possono anche fare riferimento ad attributi calcolati.

Nell&#39;esempio seguente viene creata una definizione di segmento che fa riferimento a un attributo calcolato esistente. Per ulteriori informazioni sulle definizioni dei segmenti e su come utilizzarle nell’API del servizio di segmentazione, consulta [guida dell’endpoint API per le definizioni dei segmenti](../../segmentation/api/segment-definitions.md).

Per iniziare, effettua una richiesta POST al `/segment/definitions` endpoint, che fornisce l’attributo calcolato nel corpo della richiesta.

**Formato API**

```http
POST /segment/definitions
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "downloadedInLast7Days",
        "description": "Has product been downloaded in last 7 days?",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "ttlInDays": 30,
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "_{TENANT_ID}.downloadsLast7Days > 0",
            "meta": "m"
        },
        "dataGovernancePolicy": {
            "excludeOptOut": true
        },
        "evaluationInfo": {
            "batch": {
                "enabled": false
            },
            "continuous": {
                "enabled": true
            },
            "synchronous": {
                "enabled": false
            }
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Un nome univoco per il segmento, sotto forma di stringa. |
| `description` | Una descrizione leggibile della definizione. |
| `schema.name` | Lo schema associato alle entità nel segmento. È costituito da un `id` o `name` campo. |
| `expression` | Oggetto contenente campi con informazioni sulla definizione del segmento. |
| `expression.type` | Specifica il tipo di espressione. Attualmente, è supportato solo &quot;PQL&quot;. |
| `expression.format` | Indica la struttura dell’espressione in valore. Attualmente, solo `pql/text` è supportato. |
| `expression.value` | Espressione PQL valida. In questo esempio include un riferimento a un attributo calcolato esistente. |

Per ulteriori informazioni sugli attributi di definizione dello schema, consulta gli esempi forniti nella sezione [guida dell’endpoint API per le definizioni dei segmenti](../../segmentation/api/segment-definitions.md).

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della definizione del segmento appena creata. Per ulteriori informazioni sugli oggetti di risposta di definizione del segmento, consulta [guida dell’endpoint API per le definizioni dei segmenti](../../segmentation/api/segment-definitions.md).

```json
{
    "id": "add3933f-ac5c-4240-8259-3a4528ee4885",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "id": "119835c3-5fab-4c18-ae01-4ccab328fc5c",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "segment-downloadedInLast7Days",
    "description": "Has product been downloaded in last 7 days?",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "_{TENANT_ID}.downloadsLast7Days > 0",
        "meta": "m"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1602016581000,
    "updateEpoch": 1610609459,
    "updateTime": 1610609459000,
    "createEpoch": 1602016554,
    "_etag": "\"8b01611a-0000-0200-0000-5ffff3330000\"",
    "dependents": [
        "023d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [
    "103d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "type": "SegmentDefinition"
}
```

## Passaggi successivi

Ora che hai imparato le nozioni di base sugli attributi calcolati, puoi iniziare a definirli per la tua organizzazione.
