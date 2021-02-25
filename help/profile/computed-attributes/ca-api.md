---
keywords: Experience Platform ;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API attributi calcolati
topic: guida
type: Documentazione
description: In Adobe Experience Platform, gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento in attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate tra segmentazione, attivazione e personalizzazione. Questa guida mostra come creare, visualizzare, aggiornare ed eliminare gli attributi calcolati utilizzando l'API Profilo cliente in tempo reale.
translation-type: tm+mt
source-git-commit: 6ae96ab25bd7992fe93d15bfc16b58a2fe7b4b7c
workflow-type: tm+mt
source-wordcount: '2279'
ht-degree: 2%

---


# (Alfa) Endpoint API degli attributi calcolati

>[!IMPORTANT]
>
>La funzionalità degli attributi calcolati descritta in questo documento è attualmente in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento in attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate tra segmentazione, attivazione e personalizzazione. Questa guida include chiamate API di esempio per eseguire operazioni CRUD di base utilizzando l&#39;endpoint `/computedAttributes`.

Per ulteriori informazioni sugli attributi calcolati, iniziare leggendo la [panoramica degli attributi calcolati](overview.md).

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39; [Real-time Customer Profile API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

Prima di continuare, consultare la [Guida introduttiva all&#39;API profilo](../api/getting-started.md) per i collegamenti alla documentazione consigliata, una guida alla lettura delle chiamate API di esempio visualizzate in questo documento e informazioni importanti sulle intestazioni richieste necessarie per eseguire correttamente chiamate a qualsiasi API  Experience Platform.

## Configurare un campo attributo calcolato

Per creare un attributo calcolato, è innanzitutto necessario identificare il campo in uno schema che contenga il valore dell&#39;attributo calcolato.

Fare riferimento alla documentazione relativa alla [configurazione di un attributo calcolato](configure-api.md) per una guida completa end-to-end alla creazione di un campo attributo calcolato in uno schema.

>[!WARNING]
>
>Per procedere con la guida API è necessario che sia configurato un campo attributo calcolato.

## Creare un attributo calcolato {#create-a-computed-attribute}

Con il campo attributo calcolato definito nello schema abilitato per il profilo, ora puoi configurare un attributo calcolato. Se non lo avete già fatto, seguite il flusso di lavoro descritto nella documentazione [configurazione di un attributo calcolato](configure-api.md).

Per creare un attributo calcolato, si inizia effettuando una richiesta di POST all&#39;endpoint `/config/computedAttributes` con un corpo della richiesta contenente i dettagli dell&#39;attributo calcolato che si desidera creare.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "birthdayCurrentMonth",
        "path" : "_{TENANT_ID}",
        "description" : "Computed attribute to capture if the customer birthday is in the current month.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Proprietà | Descrizione |
|---|---|
| `name` | Il nome del campo dell&#39;attributo calcolato, sotto forma di stringa. |
| `path` | Percorso del campo contenente l&#39;attributo calcolato. Questo percorso si trova all&#39;interno dell&#39;attributo `properties` dello schema e NON deve includere il nome del campo nel percorso. Durante la scrittura del percorso, omettete i livelli multipli degli attributi `properties`. |
| `{TENANT_ID}` | Se non si ha familiarità con l&#39;ID tenant, fare riferimento ai passaggi per trovare l&#39;ID tenant nella [Guida per gli sviluppatori del Registro di sistema dello schema](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Una descrizione dell&#39;attributo calcolato. Questa funzione è particolarmente utile se sono stati definiti più attributi calcolati in quanto aiuterà gli altri utenti all&#39;interno dell&#39;organizzazione IMS a determinare l&#39;attributo calcolato corretto da utilizzare. |
| `expression.value` | Un&#39;espressione [!DNL Profile Query Language] (PQL) valida. Gli attributi calcolati al momento supportano le seguenti funzioni: sum, count, min, max e booleano. Per un elenco delle espressioni di esempio, fare riferimento alla documentazione di [esempi di espressioni PQL](expressions.md). |
| `schema.name` | La classe su cui si basa lo schema contenente il campo dell&#39;attributo calcolato. Esempio: `_xdm.context.experienceevent` per uno schema basato sulla classe ExperienceEvent XDM. |

**Risposta**

Un attributo calcolato creato correttamente restituisce HTTP Status 200 (OK) e un corpo di risposta contenente i dettagli dell&#39;attributo calcolato appena creato. Questi dettagli includono un `id` univoco generato dal sistema, di sola lettura, che può essere utilizzato per fare riferimento all&#39;attributo calcolato durante altre operazioni API.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
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

| Proprietà | Descrizione |
|---|---|
| `id` | Un ID univoco, di sola lettura, generato dal sistema che può essere utilizzato per fare riferimento all&#39;attributo calcolato durante altre operazioni API. |
| `imsOrgId` | L&#39;organizzazione IMS relativa all&#39;attributo calcolato deve corrispondere al valore inviato nella richiesta. |
| `sandbox` | L&#39;oggetto sandbox contiene i dettagli della sandbox all&#39;interno della quale è stato configurato l&#39;attributo calcolato. Queste informazioni vengono estratte dall’intestazione della sandbox inviata nella richiesta. Per ulteriori informazioni, consultate la [panoramica sulle sandbox](../../sandboxes/home.md). |
| `positionPath` | Un array contenente l&#39;elemento `path` decostruito al campo inviato nella richiesta. |
| `returnSchema.meta:xdmType` | Il tipo di campo in cui verrà memorizzato l&#39;attributo calcolato. |
| `definedOn` | Un array che mostra gli schemi unione su cui è stato definito l&#39;attributo calcolato. Contiene un oggetto per schema unione, il che significa che all&#39;interno dell&#39;array possono essere presenti più oggetti se l&#39;attributo calcolato è stato aggiunto a più schemi in base a classi diverse. |
| `active` | Valore booleano che indica se l&#39;attributo calcolato è attualmente attivo o meno. Per impostazione predefinita, il valore è `true`. |
| `type` | Il tipo di risorsa creata, in questo caso &quot;ComputedAttribute&quot; è il valore predefinito. |
| `createEpoch` e `updateEpoch` | L&#39;ora in cui è stato creato l&#39;attributo calcolato e l&#39;ultimo aggiornamento, rispettivamente. |

## Creare un attributo calcolato che faccia riferimento ad attributi calcolati esistenti

È inoltre possibile creare un attributo calcolato che faccia riferimento ad attributi calcolati esistenti. A tal fine, iniziare effettuando una richiesta POST all&#39;endpoint `/config/computedAttributes`. Il corpo della richiesta conterrà i riferimenti agli attributi calcolati nel campo `expression.value` come illustrato nell&#39;esempio seguente.

**Formato API**

```http
POST /config/computedAttributes
```

**Richiesta**

In questo esempio, sono già stati creati due attributi calcolati che verranno utilizzati per definire un terzo. Gli attributi calcolati esistenti sono:

* **`totalSpend`:** Acquisisce l&#39;importo totale in dollari speso da un cliente.
* **`countPurchases`:** Conta il numero di acquisti effettuati da un cliente.

La richiesta seguente fa riferimento ai due attributi calcolati esistenti, utilizzando PQL valido per suddividere al fine di calcolare il nuovo attributo calcolato `averageSpend`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "averageSpend",
        "path" : "_{TENANT_ID}.purchaseSummary",
        "description" : "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Proprietà | Descrizione |
|---|---|
| `name` | Il nome del campo dell&#39;attributo calcolato, sotto forma di stringa. |
| `path` | Percorso del campo contenente l&#39;attributo calcolato. Questo percorso si trova all&#39;interno dell&#39;attributo `properties` dello schema e NON deve includere il nome del campo nel percorso. Durante la scrittura del percorso, omettete i livelli multipli degli attributi `properties`. |
| `{TENANT_ID}` | Se non si ha familiarità con l&#39;ID tenant, fare riferimento ai passaggi per trovare l&#39;ID tenant nella [Guida per gli sviluppatori del Registro di sistema dello schema](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Una descrizione dell&#39;attributo calcolato. Questa funzione è particolarmente utile se sono stati definiti più attributi calcolati in quanto aiuterà gli altri utenti all&#39;interno dell&#39;organizzazione IMS a determinare l&#39;attributo calcolato corretto da utilizzare. |
| `expression.value` | Un&#39;espressione PQL valida. Gli attributi calcolati al momento supportano le seguenti funzioni: sum, count, min, max e booleano. Per un elenco delle espressioni di esempio, fare riferimento alla documentazione di [esempi di espressioni PQL](expressions.md).<br/><br/>In questo esempio, l&#39;espressione fa riferimento a due attributi calcolati esistenti. Per fare riferimento agli attributi si utilizza `path` e `name` dell&#39;attributo calcolato, così come appaiono nello schema in cui sono stati definiti gli attributi calcolati. Ad esempio, il `path` del primo attributo calcolato di riferimento è `_{TENANT_ID}.purchaseSummary` e il `name` è `totalSpend`. |
| `schema.name` | La classe su cui si basa lo schema contenente il campo dell&#39;attributo calcolato. Esempio: `_xdm.context.experienceevent` per uno schema basato sulla classe ExperienceEvent XDM. |

**Risposta**

Un attributo calcolato creato correttamente restituisce HTTP Status 200 (OK) e un corpo di risposta contenente i dettagli dell&#39;attributo calcolato appena creato. Questi dettagli includono un `id` univoco generato dal sistema, di sola lettura, che può essere utilizzato per fare riferimento all&#39;attributo calcolato durante altre operazioni API.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
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
    "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
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
| `id` | Un ID univoco, di sola lettura, generato dal sistema che può essere utilizzato per fare riferimento all&#39;attributo calcolato durante altre operazioni API. |
| `imsOrgId` | L&#39;organizzazione IMS relativa all&#39;attributo calcolato deve corrispondere al valore inviato nella richiesta. |
| `sandbox` | L&#39;oggetto sandbox contiene i dettagli della sandbox all&#39;interno della quale è stato configurato l&#39;attributo calcolato. Queste informazioni vengono estratte dall’intestazione della sandbox inviata nella richiesta. Per ulteriori informazioni, consultate la [panoramica sulle sandbox](../../sandboxes/home.md). |
| `positionPath` | Un array contenente l&#39;elemento `path` decostruito al campo inviato nella richiesta. |
| `returnSchema.meta:xdmType` | Il tipo di campo in cui verrà memorizzato l&#39;attributo calcolato. |
| `definedOn` | Un array che mostra gli schemi unione su cui è stato definito l&#39;attributo calcolato. Contiene un oggetto per schema unione, il che significa che all&#39;interno dell&#39;array possono essere presenti più oggetti se l&#39;attributo calcolato è stato aggiunto a più schemi in base a classi diverse. |
| `active` | Valore booleano che indica se l&#39;attributo calcolato è attualmente attivo o meno. Per impostazione predefinita, il valore è `true`. |
| `type` | Il tipo di risorsa creata, in questo caso &quot;ComputedAttribute&quot; è il valore predefinito. |
| `createEpoch` e `updateEpoch` | L&#39;ora in cui è stato creato l&#39;attributo calcolato e l&#39;ultimo aggiornamento, rispettivamente. |

## Accesso agli attributi calcolati

Quando lavorate con gli attributi calcolati utilizzando l&#39;API, esistono due opzioni per accedere agli attributi calcolati definiti dall&#39;organizzazione. La prima consiste nell&#39;elencare tutti gli attributi calcolati, la seconda consiste nel visualizzare un attributo calcolato specifico per mezzo della sua `id` univoca.

I passaggi per entrambi i pattern di accesso sono descritti in questo documento. Per iniziare, selezionare una delle opzioni seguenti:

* **[Elenca tutti gli attributi](#list-all-computed-attributes) calcolati esistenti:** Restituisce un elenco di tutti gli attributi calcolati esistenti creati dalla tua organizzazione.
* **[Visualizzare un attributo](#view-a-computed-attribute) calcolato specifico:** Restituire i dettagli di un singolo attributo calcolato specificandone l’ID durante la richiesta.

### Elenca tutti gli attributi calcolati {#list-all-computed-attributes}

L&#39;organizzazione IMS può creare più attributi calcolati e l&#39;esecuzione di una richiesta di GET all&#39;endpoint `/config/computedAttributes` consente di elencare tutti gli attributi calcolati esistenti per l&#39;organizzazione.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una risposta corretta include un attributo `_page` che fornisce il numero totale di attributi calcolati (`totalCount`) e il numero di attributi calcolati sulla pagina (`pageSize`).

La risposta include anche un array `children` composto da uno o più oggetti, ognuno dei quali contiene i dettagli di un attributo calcolato. Se l&#39;organizzazione non dispone di attributi calcolati, i valori `totalCount` e `pageSize` saranno 0 (zero) e l&#39;array `children` sarà vuoto.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{IMS_ORG}",
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
            "imsOrgId": "{IMS_ORG}",
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
                "type" : "PQL", 
                "format" : "pql/text", 
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
| `_page.totalCount` | Il numero totale di attributi calcolati definiti dall&#39;organizzazione IMS. |
| `_page.pageSize` | Il numero di attributi calcolati restituiti in questa pagina di risultati. Se `pageSize` è uguale a `totalCount`, significa che è presente una sola pagina di risultati e che sono stati restituiti tutti gli attributi calcolati. Se non sono uguali, è possibile accedere ad altre pagine di risultati. Vedere `_links.next` per informazioni dettagliate. |
| `children` | Un array composto da uno o più oggetti, ciascuno contenente i dettagli di un singolo attributo calcolato. Se non sono stati definiti attributi calcolati, la matrice `children` è vuota. |
| `id` | Un valore univoco, di sola lettura, generato dal sistema assegnato automaticamente a un attributo calcolato al momento della creazione. Per ulteriori informazioni sui componenti di un oggetto attributo calcolato, vedere la sezione relativa alla creazione di un attributo calcolato](#create-a-computed-attribute) precedente in questa esercitazione.[ |
| `_links.next` | Se viene restituita una singola pagina di attributi calcolati, `_links.next` è un oggetto vuoto, come illustrato nella risposta di esempio precedente. Se l&#39;organizzazione dispone di molti attributi calcolati, questi verranno restituiti su più pagine a cui è possibile accedere effettuando una richiesta di GET al valore `_links.next`. |

### Visualizzare un attributo calcolato {#view-a-computed-attribute}

Potete visualizzare uno specifico attributo calcolato eseguendo una richiesta di GET all&#39;endpoint `/config/computedAttributes` e includendo l&#39;ID attributo calcolato nel percorso della richiesta.

**Formato API**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parametro | Descrizione |
|---|---|
| `{ATTRIBUTE_ID}` | ID dell’attributo calcolato che si desidera visualizzare. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
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

Se è necessario aggiornare un attributo calcolato esistente, è possibile eseguire questa operazione eseguendo una richiesta PATCH all&#39;endpoint `/config/computedAttributes` e includendo l&#39;ID dell&#39;attributo calcolato che si desidera aggiornare nel percorso della richiesta.

**Formato API**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parametro | Descrizione |
|---|---|
| `{ATTRIBUTE_ID}` | L&#39;ID dell&#39;attributo calcolato che si desidera aggiornare. |

**Richiesta**

Questa richiesta utilizza la formattazione [JSON Patch](http://jsonpatch.com/) per aggiornare il &quot;valore&quot; del campo &quot;espressione&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| Proprietà | Descrizione |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | Un&#39;espressione [!DNL Profile Query Language] (PQL) valida. Gli attributi calcolati al momento supportano le seguenti funzioni: sum, count, min, max e booleano. Per un elenco delle espressioni di esempio, fare riferimento alla documentazione di [esempi di espressioni PQL](expressions.md). |

**Risposta**

Un aggiornamento riuscito restituisce lo stato HTTP 204 (nessun contenuto) e un corpo di risposta vuoto. Se desiderate confermare che l&#39;aggiornamento sia stato eseguito correttamente, potete eseguire una richiesta di GET per visualizzare l&#39;attributo calcolato in base al relativo ID.

## Eliminare un attributo calcolato

È inoltre possibile eliminare un attributo calcolato utilizzando l&#39;API. Questa operazione viene eseguita eseguendo una richiesta DELETE all&#39;endpoint `/config/computedAttributes` e includendo l&#39;ID dell&#39;attributo calcolato che si desidera eliminare nel percorso della richiesta.

>[!NOTE]
>
>Prestare attenzione quando si elimina un attributo calcolato perché potrebbe essere in uso in più schemi e l&#39;operazione DELETE non può essere annullata.

**Formato API**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parametro | Descrizione |
|---|---|
| `{ATTRIBUTE_ID}` | ID dell’attributo calcolato che si desidera eliminare. |

**Richiesta**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**Risposta**

Una richiesta di eliminazione riuscita restituisce lo stato HTTP 200 (OK) e un corpo di risposta vuoto. Per confermare che l&#39;eliminazione è avvenuta correttamente, potete eseguire una richiesta di GET per cercare l&#39;attributo calcolato dal relativo ID. Se l&#39;attributo è stato eliminato, si riceverà un errore HTTP Status 404 (Non trovato).

## Creare una definizione di segmento che faccia riferimento a un attributo calcolato

Adobe Experience Platform consente di creare segmenti che definiscono un gruppo di attributi o comportamenti specifici da un gruppo di profili. Una definizione di segmento include un&#39;espressione che racchiude una query scritta in PQL. Queste espressioni possono anche fare riferimento agli attributi calcolati.

Nell&#39;esempio seguente viene creata una definizione di segmento che fa riferimento a un attributo calcolato esistente. Per ulteriori informazioni sulle definizioni dei segmenti e su come utilizzarle nell&#39;API del servizio di segmentazione, fare riferimento alla [guida dell&#39;endpoint API delle definizioni dei segmenti](../../segmentation/api/segment-definitions.md).

Per iniziare, effettuate una richiesta POST all&#39;endpoint `/segment/definitions`, fornendo l&#39;attributo calcolato nel corpo della richiesta.

**Formato API**

```http
POST /segment/definitions
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Un nome univoco per il segmento, come stringa. |
| `description` | Descrizione leggibile della definizione. |
| `schema.name` | Schema associato alle entità nel segmento. È costituito da un campo `id` o `name`. |
| `expression` | Un oggetto contenente campi con informazioni sulla definizione del segmento. |
| `expression.type` | Specifica il tipo di espressione. Attualmente, è supportato solo &quot;PQL&quot;. |
| `expression.format` | Indica la struttura dell&#39;espressione in valore. Attualmente, è supportato solo `pql/text`. |
| `expression.value` | Un&#39;espressione PQL valida, in questo esempio include un riferimento a un attributo calcolato esistente. |

Per ulteriori informazioni sugli attributi di definizione dello schema, fare riferimento agli esempi forniti nella [guida dell&#39;endpoint API delle definizioni dei segmenti](../../segmentation/api/segment-definitions.md).

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della nuova definizione del segmento creata. Per ulteriori informazioni sugli oggetti di risposta per la definizione dei segmenti, fare riferimento alla [guida per l&#39;endpoint API delle definizioni dei segmenti](../../segmentation/api/segment-definitions.md).

```json
{
    "id": "add3933f-ac5c-4240-8259-3a4528ee4885",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "id": "119835c3-5fab-4c18-ae01-4ccab328fc5c",
    "imsOrgId": "{IMS_ORG}",
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

Ora che hai imparato le basi degli attributi calcolati, sei pronto a iniziare a definirli per la tua organizzazione.