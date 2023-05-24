---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;XDM system;Experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: Guida introduttiva all’API Schema Registry
description: Questo documento fornisce un’introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all’API Schema Registry.
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 0%

---

# Guida introduttiva a [!DNL Schema Registry] API

Il [!DNL Schema Registry] API consente di creare e gestire varie risorse Experience Data Model (XDM). Questo documento fornisce un’introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate al [!DNL Schema Registry] API.

## Prerequisiti

L’utilizzo della guida per sviluppatori richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../schema/composition.md): scopri gli elementi di base degli schemi XDM.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

XDM utilizza la formattazione dello schema JSON per descrivere e convalidare la struttura dei dati acquisiti sull’esperienza del cliente. Pertanto, si consiglia vivamente di rivedere [Documentazione ufficiale sullo schema JSON](https://json-schema.org/) per comprendere meglio questa tecnologia di base.

## Lettura delle chiamate API di esempio

Il [!DNL Schema Registry] La documentazione API fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

## Raccogli i valori per le intestazioni richieste

Per effettuare chiamate a [!DNL Platform] , devi prima completare le [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], compresi quelli appartenenti al [!DNL Schema Registry], sono isolate in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedere [documentazione sandbox](../../sandboxes/home.md).

Tutte le richieste di ricerca (GET) a [!DNL Schema Registry] richiede un `Accept` il cui valore determina il formato delle informazioni restituite dall’API. Consulta la [Accetta intestazione](#accept) per ulteriori dettagli.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* `Content-Type: application/json`

## Conoscere il TENANT_ID {#know-your-tenant_id}

Nelle guide API sono riportati i riferimenti a un `TENANT_ID`. Questo ID viene utilizzato per garantire che le risorse create abbiano uno spazio dei nomi corretto e siano contenute all’interno dell’organizzazione. Se non conosci il tuo ID, puoi accedervi eseguendo la seguente richiesta di GET:

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce informazioni relative all’utilizzo da parte della tua organizzazione del [!DNL Schema Registry]. Ciò include `tenantId` , il cui valore è il tuo `TENANT_ID`.

```JSON
{
  "imsOrg":"{ORG_ID}",
  "tenantId":"{TENANT_ID}",
  "counts": {
    "schemas": 4,
    "mixins": 3,
    "datatypes": 1,
    "classes": 2,
    "unions": 0,
  },
  "recentlyCreatedResources": [ 
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "mixins",
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
      "meta:resourceType": "mixins",
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

## Comprendere la `CONTAINER_ID` {#container}

Chiamate a [!DNL Schema Registry] Le API richiedono l’utilizzo di un `CONTAINER_ID`. Esistono due contenitori in cui è possibile effettuare chiamate API: `global` contenitore e `tenant` contenitore.

### Contenitore globale

Il `global` il contenitore contiene tutti gli Adobi standard e [!DNL Experience Platform] il partner ha fornito classi, gruppi di campi di schema, tipi di dati e schemi. È possibile eseguire solo richieste di elenco e ricerca (GET) per `global` contenitore.

Esempio di chiamata che utilizza `global` il contenitore avrà un aspetto simile al seguente:

```http
GET /global/classes
```

### Contenitore tenant

Da non confondere con il tuo unico `TENANT_ID`, il `tenant` contenitore contiene tutte le classi, i gruppi di campi, i tipi di dati, gli schemi e i descrittori definiti da un&#39;organizzazione. Questi sono specifici per ogni organizzazione, il che significa che non sono visibili o gestibili da altre organizzazioni. Puoi eseguire tutte le operazioni CRUD (GET, POST, PUT, PATCH, DELETE) sulle risorse create in `tenant` contenitore.

Esempio di chiamata che utilizza `tenant` il contenitore avrà un aspetto simile al seguente:

```http
POST /tenant/fieldgroups
```

Quando crei una classe, un gruppo di campi, uno schema o un tipo di dati nel `tenant` contenitore, viene salvato nel [!DNL Schema Registry] e ha assegnato un `$id` URI che include `TENANT_ID`. Questo `$id` viene utilizzato in tutta l’API per fare riferimento a risorse specifiche. Esempi di `$id` I valori vengono forniti nella sezione successiva.

## Identificazione risorsa {#resource-identification}

Le risorse XDM sono identificate con un `$id` un attributo nella forma di un URI, ad esempio:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Per rendere l’URI più semplice, gli schemi dispongono anche di una codifica con notazione del punto dell’URI in una proprietà denominata `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Chiamate a [!DNL Schema Registry] L’API supporterà sia il formato con codifica URL `$id` URI o `meta:altId` (formato di notazione con punto). Si consiglia di utilizzare il codice URL `$id` URI quando si effettua una chiamata REST all’API, come segue:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Accetta intestazione {#accept}

Quando si eseguono operazioni di elenco e ricerca (GET) in [!DNL Schema Registry] API, un `Accept` L’intestazione è necessaria per determinare il formato dei dati restituiti dall’API. Quando cerchi risorse specifiche, nella sezione deve essere incluso anche un numero di versione `Accept` intestazione.

Nella tabella seguente sono elencate le opzioni compatibili `Accept` i valori di intestazione, inclusi quelli con i numeri di versione, insieme alle descrizioni di ciò che l’API restituirà quando vengono utilizzati.

| Accept | Descrizione |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Restituisce solo un elenco di ID. Questa funzione viene utilizzata più comunemente per elencare le risorse. |
| `application/vnd.adobe.xed+json` | Restituisce un elenco di schema JSON completo con originale `$ref` e `allOf` incluso. Viene utilizzato per restituire un elenco di risorse complete. |
| `application/vnd.adobe.xed+json; version=1` | XDM non elaborato con `$ref` e `allOf`. Contiene titoli e descrizioni. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` attributi e `allOf` risolto. Contiene titoli e descrizioni. |
| `application/vnd.adobe.xed-notext+json; version=1` | XDM non elaborato con `$ref` e `allOf`. Nessun titolo o descrizione. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` attributi e `allOf` risolto. Nessun titolo o descrizione. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` attributi e `allOf` risolto. Sono inclusi i descrittori. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` e `allOf` risolto, con titoli e descrizioni. I campi obsoleti sono indicati con un simbolo `meta:status` attributo di `deprecated`. |

{style="table-layout:auto"}

>[!NOTE]
>
>Platform attualmente supporta una sola versione principale per ogni schema (`1`). Pertanto, il valore per `version` deve essere sempre `1` quando si eseguono richieste di ricerca per restituire la versione secondaria più recente dello schema. Per ulteriori informazioni sul controllo delle versioni dello schema, consulta la sottosezione seguente.

### Controllo delle versioni degli schemi {#versioning}

Esistono riferimenti alle versioni degli schemi da `Accept` intestazioni nell’API Schema Registry e in `schemaRef.contentType` proprietà nei payload API del servizio Platform a valle.

Attualmente, Platform supporta solo una singola versione principale (`1`) per ogni schema. In base al [regole di evoluzione dello schema](../schema/composition.md#evolution), ogni aggiornamento a uno schema deve essere non distruttivo, il che significa che le nuove versioni secondarie di uno schema (`1.2`, `1.3`, ecc.) sono sempre compatibili con le versioni precedenti di versioni secondarie. Pertanto, quando si specifica `version=1`, il registro dello schema restituisce sempre **più recente** versione principale `1` di uno schema, il che significa che le versioni secondarie precedenti non vengono restituite.

>[!NOTE]
>
>Il requisito non distruttivo per l’evoluzione dello schema viene applicato solo dopo che un set di dati ha fatto riferimento allo schema e si verifica uno dei seguenti casi:
>
>* I dati sono stati acquisiti nel set di dati.
>* Il set di dati è stato abilitato per l’utilizzo in Real-Time Customer Profile (anche se non sono stati acquisiti dati).
>
>Se lo schema non è stato associato a un set di dati che soddisfa uno dei criteri di cui sopra, è possibile apportarvi qualsiasi modifica. Tuttavia, in tutti i casi `version` il componente rimane ancora in `1`.

## Vincoli del campo XDM e best practice

I campi di uno schema sono elencati nei relativi `properties` oggetto. Ogni campo è di per sé un oggetto, contenente attributi per descrivere e vincolare i dati che il campo può contenere. Consulta la guida su [definizione dei campi personalizzati nell’API](../tutorials/custom-fields-api.md) per esempi di codice e vincoli facoltativi per i tipi di dati più comunemente utilizzati.

Il seguente campo di esempio illustra un campo XDM formattato correttamente, con ulteriori dettagli sui vincoli di denominazione e le best practice fornite di seguito. Queste procedure possono essere applicate anche quando si definiscono altre risorse che contengono attributi simili.

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

* Il nome di un oggetto campo può contenere caratteri alfanumerici, trattini o trattini bassi, ma **non può** inizia con un trattino basso.
   * **Corretto:** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **Errato:** `_fieldName`
* camelCase è da preferirsi per il nome dell&#39;oggetto campo. Esempio: `fieldName`
* Il campo deve includere `title`, scritto in Title Case. Esempio: `Field Name`
* Il campo richiede un `type`.
   * La definizione di alcuni tipi può richiedere un `format`.
   * Quando è richiesta una specifica formattazione dei dati, `examples` può essere aggiunto come array.
   * Il tipo di campo può essere definito anche utilizzando qualsiasi tipo di dati del Registro di sistema. Consulta la sezione su [creazione di un tipo di dati](./data-types.md#create) per ulteriori informazioni, nella guida dell’endpoint &quot;data types&quot;.
* Il `description` spiega il campo e le informazioni pertinenti relative ai dati del campo. Deve essere scritto in frasi complete con un linguaggio chiaro in modo che chiunque acceda allo schema possa capire le intenzioni del campo.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando [!DNL Schema Registry] API, seleziona una delle guide endpoint disponibili.
