---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;registro schema;registro schema;
solution: Experience Platform
title: Guida introduttiva all’API del Registro di sistema dello schema
description: Questo documento fornisce un'introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all'API del Registro di sistema dello schema.
topic-legacy: developer guide
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '1370'
ht-degree: 0%

---

# Guida introduttiva all’ API [!DNL Schema Registry]

L’ API [!DNL Schema Registry] ti consente di creare e gestire diverse risorse Experience Data Model (XDM). Questo documento fornisce un’introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all’ API [!DNL Schema Registry] .

## Prerequisiti

L’utilizzo della guida per gli sviluppatori richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

XDM utilizza la formattazione dello schema JSON per descrivere e convalidare la struttura dei dati sulla customer experience acquisiti. Si consiglia pertanto vivamente di consultare la [documentazione ufficiale dello schema JSON](https://json-schema.org/) per una migliore comprensione di questa tecnologia di base.

## Lettura di chiamate API di esempio

La documentazione [!DNL Schema Registry] API fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

## Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Schema Registry], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la documentazione [sandbox](../../sandboxes/home.md).

Tutte le richieste di ricerca (GET) a [!DNL Schema Registry] richiedono un’intestazione `Accept` aggiuntiva, il cui valore determina il formato delle informazioni restituite dall’API. Per ulteriori informazioni, consulta la sezione [Accetta intestazione](#accept) di seguito.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* `Content-Type: application/json`

## Conosci il tuo TENANT_ID {#know-your-tenant_id}

Nelle guide API sono disponibili riferimenti a `TENANT_ID`. Questo ID viene utilizzato per garantire che le risorse create siano spaccate correttamente e contenute all’interno dell’organizzazione IMS. Se non conosci il tuo ID, puoi accedervi eseguendo la seguente richiesta GET:

**Formato API**

```http
GET /stats
```

**Richiesta**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce informazioni sull&#39;utilizzo di [!DNL Schema Registry] da parte della tua organizzazione. Ciò include un attributo `tenantId` il cui valore è `TENANT_ID`.

```JSON
{
  "imsOrg":"{IMS_ORG}",
  "tenantId":"{TENANT_ID}",
  "counts": {
    "schemas": 4,
    "fieldgroups": 3,
    "datatypes": 1,
    "classes": 2,
    "unions": 0,
  },
  "recentlyCreatedResources": [ 
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "fieldgroups",
      "meta:created": "Sat Feb 02 2019 00:24:30 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/5bdb5582be0c0f3ebfc1c603b705764f",
      "title": "Tenant Class",
      "description": "Tenant Defined Class",
      "meta:resourceType": "classes",
      "meta:created": "Fri Feb 01 2019 22:46:21 GMT+0000 (UTC)",
      "version": "1.0"
    } 
  ],
  "recentlyUpdatedResources": [
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "fieldgroups",
      "meta:updated": "Sat Feb 02 2019 00:34:06 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "title": "Data Schema",
      "description": "Schema for Data Information",
      "meta:resourceType": "schemas",
      "meta:updated": "Fri Feb 01 2019 23:47:43 GMT+0000 (UTC)",
      "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab",
      "meta:classTitle": "Sample Class",
      "version": "1.1"
    }
 ],
 "classUsage": {
    "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "title": "Tenant Data Schema",
        "description": "Schema for tenant-specific data."
      }
    ],
    "https://ns.adobe.com/xdm/context/profile": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/3ac6499f0a43618bba6b138226ae3542",
        "title": "Simple Profile",
        "description": "A simple profile schema."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "title": "Program Schema",
        "description": "Schema for program-related data."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/4025a705890c6d4a4a06b16f8cf6f4ca",
        "title": "Sample Schema",
        "description": "A sample schema."
      }
    ]
  }
 }
```

## Comprendere `CONTAINER_ID` {#container}

Le chiamate all&#39;API [!DNL Schema Registry] richiedono l&#39;utilizzo di un `CONTAINER_ID`. Esistono due contenitori per i quali è possibile effettuare chiamate API: il contenitore `global` e il contenitore `tenant`.

### Contenitore globale

Il contenitore `global` contiene tutti gli Adobi standard e il partner [!DNL Experience Platform] ha fornito classi, gruppi di campi di schema, tipi di dati e schemi. È possibile eseguire richieste di elenco e ricerca (GET) solo per il contenitore `global` .

Un esempio di chiamata che utilizza il contenitore `global` ha il seguente aspetto:

```http
GET /global/classes
```

### Contenitore tenant

Da non confondere con il `TENANT_ID` univoco, il contenitore `tenant` contiene tutte le classi, i gruppi di campi, i tipi di dati, gli schemi e i descrittori definiti da un&#39;organizzazione IMS. Sono esclusive per ogni organizzazione, il che significa che non sono visibili o gestibili da altre organizzazioni IMS. Puoi eseguire tutte le operazioni CRUD (GET, POST, PUT, PATCH, DELETE) rispetto alle risorse create nel contenitore `tenant` .

Un esempio di chiamata che utilizza il contenitore `tenant` ha il seguente aspetto:

```http
POST /tenant/fieldgroups
```

Quando crei una classe, un gruppo di campi, uno schema o un tipo di dati nel contenitore `tenant`, questo viene salvato nel [!DNL Schema Registry] e gli viene assegnato un URI `$id` che include il `TENANT_ID`. Questo `$id` viene utilizzato in tutta l’API per fare riferimento a risorse specifiche. Esempi di valori `$id` sono forniti nella sezione successiva.

## Identificazione della risorsa {#resource-identification}

Le risorse XDM sono identificate con un attributo `$id` sotto forma di URI, ad esempio nei seguenti esempi:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Per rendere l’URI più facile da usare come REST, gli schemi hanno anche una codifica di notazione del punto dell’URI in una proprietà denominata `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Le chiamate all&#39;API [!DNL Schema Registry] supporteranno l&#39;URI con codifica URL `$id` o il `meta:altId` (formato di notazione del punto). Si consiglia di utilizzare l’URI con codifica URL `$id` quando si effettua una chiamata REST all’API, come riportato di seguito:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Accetta intestazione {#accept}

Quando si eseguono operazioni di elenco e ricerca (GET) nell’ API [!DNL Schema Registry], è necessaria un’intestazione `Accept` per determinare il formato dei dati restituiti dall’API. Quando cerchi risorse specifiche, nell’intestazione `Accept` deve essere incluso anche un numero di versione.

Nella tabella seguente sono elencati i valori di intestazione `Accept` compatibili, inclusi quelli con numeri di versione, insieme alle descrizioni di ciò che l&#39;API restituirà quando vengono utilizzati.

| Accept | Descrizione |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Restituisce solo un elenco di ID. Viene utilizzato più comunemente per elencare le risorse. |
| `application/vnd.adobe.xed+json` | Restituisce un elenco dello schema JSON completo con i valori originali `$ref` e `allOf` inclusi. Viene utilizzato per restituire un elenco completo delle risorse. |
| `application/vnd.adobe.xed+json; version=1` | XDM grezzo con `$ref` e `allOf`. Presenta titoli e descrizioni. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` attributi e  `allOf` risolti. Presenta titoli e descrizioni. |
| `application/vnd.adobe.xed-notext+json; version=1` | XDM grezzo con `$ref` e `allOf`. Nessun titolo o descrizione. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` attributi e  `allOf` risolti. Nessun titolo o descrizione. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` attributi e  `allOf` risolti. I descrittori sono inclusi. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Platform supporta attualmente una sola versione principale per ogni schema (`1`). Pertanto, il valore per `version` deve sempre essere `1` quando si eseguono richieste di ricerca per restituire la versione secondaria più recente dello schema. Per ulteriori informazioni sul controllo delle versioni dello schema, consulta la sottosezione seguente.

### Controllo delle versioni di uno schema {#versioning}

Le versioni dello schema sono referenziate dalle intestazioni `Accept` nell’API del Registro di sistema dello schema e nelle proprietà `schemaRef.contentType` nei payload API del servizio Platform a valle.

Attualmente, Platform supporta solo una singola versione principale (`1`) per ogni schema. In base alle [regole di evoluzione dello schema](../schema/composition.md#evolution), ogni aggiornamento di uno schema deve essere non distruttivo, il che significa che le nuove versioni secondarie di uno schema (`1.2`, `1.3`, ecc.) sono sempre compatibili con le versioni precedenti. Pertanto, quando si specifica `version=1`, il Registro di sistema dello schema restituisce sempre la **versione principale** più recente `1` di uno schema , il che significa che non vengono restituite le versioni secondarie precedenti.

>[!NOTE]
>
>Il requisito non distruttivo per l’evoluzione dello schema viene applicato solo dopo che un set di dati vi ha fatto riferimento e uno dei casi seguenti è vero:
>
>* I dati sono stati acquisiti nel set di dati.
>* Il set di dati è stato abilitato per l’utilizzo in Profilo cliente in tempo reale (anche se non sono stati acquisiti dati).

>
>
Se lo schema non è stato associato a un set di dati che soddisfa uno dei criteri di cui sopra, è possibile apportare qualsiasi modifica. Tuttavia, in tutti i casi il componente `version` rimane comunque in corrispondenza di `1`.

## Vincoli del campo XDM e best practice

I campi di uno schema sono elencati all&#39;interno del relativo oggetto `properties`. Ciascun campo è esso stesso un oggetto, contenente gli attributi per descrivere e vincolare i dati che il campo può contenere.

Per ulteriori informazioni sulla definizione dei tipi di campo nell’API, consulta la [guida ai vincoli di campo](../schema/field-constraints.md) per questa guida, inclusi esempi di codice e vincoli facoltativi per i tipi di dati più comunemente utilizzati.

Il campo di esempio seguente illustra un campo XDM formattato correttamente, con ulteriori dettagli sui vincoli di denominazione e sulle best practice fornite di seguito. Queste pratiche possono essere applicate anche quando si definiscono altre risorse che contengono attributi simili.

```JSON
"fieldName": {
    "title": "Field Name",
    "type": "string",
    "format": "date-time",
    "examples": [
        "2004-10-23T12:00:00-06:00"
    ],
    "description": "Full sentence describing the field, using proper grammar and punctuation.",
}
```

* Il nome di un oggetto campo può contenere caratteri alfanumerici, trattini o caratteri di sottolineatura, ma **potrebbe non essere** iniziare con un trattino basso.
   * **Corretto:** `fieldName`,  `field_name2`,  `Field-Name`,  `field-name_3`
   * **Errato:** `_fieldName`
* camelCase è da preferire per il nome dell&#39;oggetto field . Esempio: `fieldName`
* Il campo deve includere un carattere `title`, scritto in Case titolo. Esempio: `Field Name`
* Il campo richiede un valore `type`.
   * La definizione di alcuni tipi può richiedere un valore facoltativo `format`.
   * Se è richiesta una formattazione specifica dei dati, è possibile aggiungere `examples` come array.
   * Il tipo di campo può essere definito anche utilizzando qualsiasi tipo di dati presente nel registro. Per ulteriori informazioni, consulta la sezione su [creazione di un tipo di dati](./data-types.md#create) nella guida all’endpoint per i tipi di dati .
* Il `description` spiega il campo e le informazioni pertinenti relative ai dati del campo. Dovrebbe essere scritto in frasi complete con un linguaggio chiaro in modo che chiunque acceda allo schema possa capire le intenzioni del campo.

Per ulteriori informazioni su come definire diversi tipi di campi nell’API, consulta il documento sui [vincoli di campo](../schema/field-constraints.md) .

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l’ [!DNL Schema Registry] API , seleziona una delle guide dell’endpoint disponibili.
