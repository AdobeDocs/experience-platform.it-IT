---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API per gli attributi calcolati
topic-legacy: guide
type: Documentation
description: In Adobe Experience Platform, gli attributi calcolati sono funzioni utilizzate per aggregare dati a livello di evento in attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate tra segmentazione, attivazione e personalizzazione. Questa guida mostra come creare, visualizzare, aggiornare ed eliminare gli attributi calcolati utilizzando l’API Profilo cliente in tempo reale.
exl-id: 6b35ff63-590b-4ef5-ab39-c36c39ab1d58
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2277'
ht-degree: 2%

---

# (Alpha) Endpoint API per gli attributi calcolati

>[!IMPORTANT]
>
>La funzionalità dell&#39;attributo calcolato descritta in questo documento è attualmente in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Gli attributi calcolati sono funzioni utilizzate per aggregare dati a livello di evento in attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate tra segmentazione, attivazione e personalizzazione. Questa guida include chiamate API di esempio per l’esecuzione di operazioni CRUD di base utilizzando l’endpoint `/computedAttributes` .

Per ulteriori informazioni sugli attributi calcolati, inizia leggendo la [panoramica sugli attributi calcolati](overview.md).

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39; [API Profilo cliente in tempo reale](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

Prima di continuare, controlla la [Guida introduttiva all’API di profilo](../api/getting-started.md) per i collegamenti alla documentazione consigliata, una guida per la lettura delle chiamate API di esempio visualizzate in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare chiamate a qualsiasi API di Experience Platform.

## Configurare un campo attributo calcolato

Per creare un attributo calcolato, devi innanzitutto identificare il campo in uno schema che contenga il valore dell&#39;attributo calcolato.

Consulta la documentazione relativa alla [configurazione di un attributo calcolato](configure-api.md) per una guida completa end-to-end alla creazione di un campo attributo calcolato in uno schema.

>[!WARNING]
>
>Per procedere con la guida API è necessario che sia configurato un campo attributo calcolato.

## Crea un attributo calcolato {#create-a-computed-attribute}

Con il campo dell’attributo calcolato definito nello schema abilitato per il profilo, ora puoi configurare un attributo calcolato. Se non lo hai già fatto, segui il flusso di lavoro descritto nella documentazione [configurazione di un attributo calcolato](configure-api.md) .

Per creare un attributo calcolato, inizia effettuando una richiesta POST all&#39;endpoint `/config/computedAttributes` con un corpo della richiesta contenente i dettagli dell&#39;attributo calcolato che desideri creare.

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
| `name` | Nome del campo dell&#39;attributo calcolato come stringa. |
| `path` | Percorso del campo contenente l&#39;attributo calcolato. Questo percorso si trova all&#39;interno dell&#39;attributo `properties` dello schema e NON deve includere il nome del campo nel percorso. Durante la scrittura del percorso, ometti i diversi livelli degli attributi `properties` . |
| `{TENANT_ID}` | Se non conosci il tuo ID tenant, fai riferimento ai passaggi per trovare l’ID tenant nella [Guida per gli sviluppatori del Registro di sistema dello schema](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Descrizione dell&#39;attributo calcolato. Questa funzione è particolarmente utile quando sono stati definiti più attributi calcolati, in quanto aiuterà gli altri utenti dell’organizzazione IMS a determinare l’attributo calcolato corretto da utilizzare. |
| `expression.value` | Un&#39;espressione [!DNL Profile Query Language] (PQL) valida. Gli attributi calcolati supportano attualmente le seguenti funzioni: sum, count, min, max e booleano. Per un elenco di espressioni di esempio, consulta la documentazione [espressioni PQL di esempio](expressions.md) . |
| `schema.name` | Classe su cui si basa lo schema contenente il campo dell&#39;attributo calcolato. Esempio: `_xdm.context.experienceevent` per uno schema basato sulla classe ExperienceEvent XDM. |

**Risposta**

Un attributo calcolato creato correttamente restituisce HTTP Status 200 (OK) e un corpo di risposta contenente i dettagli dell&#39;attributo calcolato appena creato. Questi dettagli includono un `id` generato dal sistema univoco e di sola lettura che può essere utilizzato per fare riferimento all&#39;attributo calcolato durante altre operazioni API.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
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
| `id` | ID univoco generato dal sistema, di sola lettura, che può essere utilizzato per fare riferimento all&#39;attributo calcolato durante altre operazioni API. |
| `imsOrgId` | L’organizzazione IMS relativa all’attributo calcolato deve corrispondere al valore inviato nella richiesta. |
| `sandbox` | L&#39;oggetto sandbox contiene i dettagli della sandbox in cui è stato configurato l&#39;attributo calcolato. Queste informazioni sono tratte dall’intestazione della sandbox inviata nella richiesta. Per ulteriori informazioni, consulta la [panoramica sulle sandbox](../../sandboxes/home.md). |
| `positionPath` | Matrice contenente il `path` decostruito al campo inviato nella richiesta. |
| `returnSchema.meta:xdmType` | Il tipo di campo in cui verrà memorizzato l&#39;attributo calcolato. |
| `definedOn` | Matrice che mostra gli schemi dell&#39;unione su cui è stato definito l&#39;attributo calcolato. Contiene un oggetto per schema di unione, il che significa che possono essere presenti più oggetti all&#39;interno dell&#39;array se l&#39;attributo calcolato è stato aggiunto a più schemi in base a classi diverse. |
| `active` | Un valore booleano che indica se l&#39;attributo calcolato è attualmente attivo o meno. Per impostazione predefinita, il valore è `true`. |
| `type` | Il tipo di risorsa creata, in questo caso &quot;ComputedAttribute&quot;, è il valore predefinito. |
| `createEpoch` e `updateEpoch` | Data e ora di creazione dell&#39;attributo calcolato e dell&#39;ultimo aggiornamento, rispettivamente. |

## Crea un attributo calcolato che fa riferimento ad attributi calcolati esistenti

È inoltre possibile creare un attributo calcolato che faccia riferimento ad attributi calcolati esistenti. Per farlo, inizia effettuando una richiesta POST all’endpoint `/config/computedAttributes` . Il corpo della richiesta conterrà i riferimenti agli attributi calcolati nel campo `expression.value` come mostrato nell’esempio seguente.

**Formato API**

```http
POST /config/computedAttributes
```

**Richiesta**

In questo esempio, sono già stati creati due attributi calcolati e verranno utilizzati per definire un terzo. Gli attributi calcolati esistenti sono:

* **`totalSpend`:** acquisisce l’importo totale in dollari speso da un cliente.
* **`countPurchases`:** conta il numero di acquisti effettuati da un cliente.

La richiesta seguente fa riferimento ai due attributi calcolati esistenti, utilizzando un PQL valido per suddividere per calcolare il nuovo attributo calcolato `averageSpend`.

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
| `name` | Nome del campo dell&#39;attributo calcolato come stringa. |
| `path` | Percorso del campo contenente l&#39;attributo calcolato. Questo percorso si trova all&#39;interno dell&#39;attributo `properties` dello schema e NON deve includere il nome del campo nel percorso. Durante la scrittura del percorso, ometti i diversi livelli degli attributi `properties` . |
| `{TENANT_ID}` | Se non conosci il tuo ID tenant, fai riferimento ai passaggi per trovare l’ID tenant nella [Guida per gli sviluppatori del Registro di sistema dello schema](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Descrizione dell&#39;attributo calcolato. Questa funzione è particolarmente utile quando sono stati definiti più attributi calcolati, in quanto aiuterà gli altri utenti dell’organizzazione IMS a determinare l’attributo calcolato corretto da utilizzare. |
| `expression.value` | Un&#39;espressione PQL valida. Gli attributi calcolati supportano attualmente le seguenti funzioni: sum, count, min, max e booleano. Per un elenco di espressioni di esempio, consulta la documentazione [espressioni PQL di esempio](expressions.md) .<br/><br/>In questo esempio, l&#39;espressione fa riferimento a due attributi calcolati esistenti. Gli attributi sono referenziati utilizzando `path` e `name` dell&#39;attributo calcolato come appaiono nello schema in cui sono stati definiti gli attributi calcolati. Ad esempio, il `path` del primo attributo calcolato a cui si fa riferimento è `_{TENANT_ID}.purchaseSummary` e il `name` è `totalSpend`. |
| `schema.name` | Classe su cui si basa lo schema contenente il campo dell&#39;attributo calcolato. Esempio: `_xdm.context.experienceevent` per uno schema basato sulla classe ExperienceEvent XDM. |

**Risposta**

Un attributo calcolato creato correttamente restituisce HTTP Status 200 (OK) e un corpo di risposta contenente i dettagli dell&#39;attributo calcolato appena creato. Questi dettagli includono un `id` generato dal sistema univoco e di sola lettura che può essere utilizzato per fare riferimento all&#39;attributo calcolato durante altre operazioni API.

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
| `id` | ID univoco generato dal sistema, di sola lettura, che può essere utilizzato per fare riferimento all&#39;attributo calcolato durante altre operazioni API. |
| `imsOrgId` | L’organizzazione IMS relativa all’attributo calcolato deve corrispondere al valore inviato nella richiesta. |
| `sandbox` | L&#39;oggetto sandbox contiene i dettagli della sandbox in cui è stato configurato l&#39;attributo calcolato. Queste informazioni sono tratte dall’intestazione della sandbox inviata nella richiesta. Per ulteriori informazioni, consulta la [panoramica sulle sandbox](../../sandboxes/home.md). |
| `positionPath` | Matrice contenente il `path` decostruito al campo inviato nella richiesta. |
| `returnSchema.meta:xdmType` | Il tipo di campo in cui verrà memorizzato l&#39;attributo calcolato. |
| `definedOn` | Matrice che mostra gli schemi dell&#39;unione su cui è stato definito l&#39;attributo calcolato. Contiene un oggetto per schema di unione, il che significa che possono essere presenti più oggetti all&#39;interno dell&#39;array se l&#39;attributo calcolato è stato aggiunto a più schemi in base a classi diverse. |
| `active` | Un valore booleano che indica se l&#39;attributo calcolato è attualmente attivo o meno. Per impostazione predefinita, il valore è `true`. |
| `type` | Il tipo di risorsa creata, in questo caso &quot;ComputedAttribute&quot;, è il valore predefinito. |
| `createEpoch` e `updateEpoch` | Data e ora di creazione dell&#39;attributo calcolato e dell&#39;ultimo aggiornamento, rispettivamente. |

## Accedere agli attributi calcolati

Quando lavori con gli attributi calcolati utilizzando l’API, sono disponibili due opzioni per accedere agli attributi calcolati definiti dall’organizzazione. Il primo è quello di elencare tutti gli attributi calcolati, il secondo è quello di visualizzare un attributo calcolato specifico per il suo `id` univoco.

I passaggi per entrambi i pattern di accesso sono descritti in questo documento. Seleziona una delle seguenti opzioni per iniziare:

* **[Elenca tutti gli attributi calcolati esistenti](#list-all-computed-attributes):** restituisce un elenco di tutti gli attributi calcolati esistenti creati dalla tua organizzazione.
* **[Visualizza un attributo calcolato specifico](#view-a-computed-attribute):** restituisce i dettagli di un singolo attributo calcolato specificandone l’ID durante la richiesta.

### Elenca tutti gli attributi calcolati {#list-all-computed-attributes}

L’organizzazione IMS può creare più attributi calcolati e l’esecuzione di una richiesta di GET all’endpoint `/config/computedAttributes` consente di elencare tutti gli attributi calcolati esistenti per l’organizzazione.

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

Una risposta di successo include un attributo `_page` che fornisce il numero totale di attributi calcolati (`totalCount`) e il numero di attributi calcolati sulla pagina (`pageSize`).

La risposta include anche un array `children` composto da uno o più oggetti, ciascuno contenente i dettagli di un attributo calcolato. Se l’organizzazione non dispone di attributi calcolati, i valori `totalCount` e `pageSize` saranno 0 (zero) e la matrice `children` sarà vuota.

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
| `_page.totalCount` | Il numero totale di attributi calcolati definiti dall’organizzazione IMS. |
| `_page.pageSize` | Il numero di attributi calcolati restituiti in questa pagina di risultati. Se `pageSize` è uguale a `totalCount`, significa che esiste una sola pagina di risultati e che sono stati restituiti tutti gli attributi calcolati. Se non sono uguali, è possibile accedere ad altre pagine di risultati. Per ulteriori informazioni, vedere `_links.next` . |
| `children` | Matrice composta da uno o più oggetti, ognuno contenente i dettagli di un singolo attributo calcolato. Se non sono stati definiti attributi calcolati, la matrice `children` è vuota. |
| `id` | Valore univoco generato dal sistema, di sola lettura, assegnato automaticamente a un attributo calcolato al momento della creazione. Per ulteriori informazioni sui componenti di un oggetto attributo calcolato, consulta la sezione sulla [creazione di un attributo calcolato](#create-a-computed-attribute) precedente in questa esercitazione. |
| `_links.next` | Se viene restituita una singola pagina di attributi calcolati, `_links.next` è un oggetto vuoto, come illustrato nella risposta di esempio precedente. Se la tua organizzazione dispone di molti attributi calcolati, questi verranno restituiti su più pagine a cui puoi accedere effettuando una richiesta di GET al valore `_links.next` . |

### Visualizza un attributo calcolato {#view-a-computed-attribute}

Puoi visualizzare un attributo calcolato specifico effettuando una richiesta di GET all&#39;endpoint `/config/computedAttributes` e includendo l&#39;ID attributo calcolato nel percorso della richiesta.

**Formato API**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parametro | Descrizione |
|---|---|
| `{ATTRIBUTE_ID}` | ID dell&#39;attributo calcolato che si desidera visualizzare. |

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

Se hai bisogno di aggiornare un attributo calcolato esistente, puoi farlo effettuando una richiesta PATCH all’endpoint `/config/computedAttributes` e includendo l’ID dell’attributo calcolato che desideri aggiornare nel percorso della richiesta.

**Formato API**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parametro | Descrizione |
|---|---|
| `{ATTRIBUTE_ID}` | ID dell&#39;attributo calcolato che si desidera aggiornare. |

**Richiesta**

Questa richiesta utilizza la [formattazione della patch JSON](http://jsonpatch.com/) per aggiornare il &quot;valore&quot; del campo &quot;espressione&quot;.

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
| `{NEW_EXPRESSION_VALUE}` | Un&#39;espressione [!DNL Profile Query Language] (PQL) valida. Gli attributi calcolati supportano attualmente le seguenti funzioni: sum, count, min, max e booleano. Per un elenco di espressioni di esempio, consulta la documentazione [espressioni PQL di esempio](expressions.md) . |

**Risposta**

Un aggiornamento corretto restituisce lo stato HTTP 204 (nessun contenuto) e un corpo di risposta vuoto. Se desideri confermare che l&#39;aggiornamento è stato eseguito correttamente, puoi eseguire una richiesta GET per visualizzare l&#39;attributo calcolato in base al relativo ID.

## Eliminare un attributo calcolato

È inoltre possibile eliminare un attributo calcolato utilizzando l’API. A tal fine, invia una richiesta DELETE all’endpoint `/config/computedAttributes` e include l’ID dell’attributo calcolato che desideri eliminare nel percorso della richiesta.

>[!NOTE]
>
>Presta attenzione quando elimini un attributo calcolato perché potrebbe essere in uso in più schemi e l&#39;operazione DELETE non può essere annullata.

**Formato API**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parametro | Descrizione |
|---|---|
| `{ATTRIBUTE_ID}` | ID dell&#39;attributo calcolato che si desidera eliminare. |

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

Una richiesta di eliminazione corretta restituisce lo stato HTTP 200 (OK) e un corpo di risposta vuoto. Per confermare che l&#39;eliminazione è avvenuta correttamente, puoi eseguire una richiesta GET per cercare l&#39;attributo calcolato dal relativo ID. Se l&#39;attributo è stato eliminato, riceverai un errore di stato HTTP 404 (Non trovato).

## Creare una definizione di segmento che faccia riferimento a un attributo calcolato

Adobe Experience Platform consente di creare segmenti che definiscono un gruppo di attributi o comportamenti specifici da un gruppo di profili. Una definizione di segmento include un’espressione che incapsula una query scritta in PQL. Queste espressioni possono anche fare riferimento ad attributi calcolati.

Nell&#39;esempio seguente viene creata una definizione di segmento che fa riferimento a un attributo calcolato esistente. Per ulteriori informazioni sulle definizioni dei segmenti e su come utilizzarli nell’API del servizio di segmentazione, consulta la [guida agli endpoint API per le definizioni dei segmenti](../../segmentation/api/segment-definitions.md).

Per iniziare, effettua una richiesta POST all’endpoint `/segment/definitions`, fornendo l’attributo calcolato nel corpo della richiesta.

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
| `description` | Una descrizione della definizione leggibile dall&#39;uomo. |
| `schema.name` | Lo schema associato alle entità nel segmento. È costituito da un campo `id` o `name`. |
| `expression` | Un oggetto contenente campi con informazioni sulla definizione del segmento. |
| `expression.type` | Specifica il tipo di espressione. Attualmente, è supportato solo &quot;PQL&quot;. |
| `expression.format` | Indica la struttura dell&#39;espressione nel valore. Attualmente, è supportato solo `pql/text`. |
| `expression.value` | Un&#39;espressione PQL valida, in questo esempio include un riferimento a un attributo calcolato esistente. |

Per ulteriori informazioni sugli attributi di definizione dello schema, consulta gli esempi forniti nella [guida per gli endpoint API delle definizioni dei segmenti](../../segmentation/api/segment-definitions.md).

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della nuova definizione del segmento creata. Per ulteriori informazioni sugli oggetti di risposta per la definizione dei segmenti, consulta la [guida all’endpoint API per le definizioni dei segmenti](../../segmentation/api/segment-definitions.md).

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

Dopo aver appreso le nozioni di base degli attributi calcolati, puoi iniziare a definirli per la tua organizzazione.
