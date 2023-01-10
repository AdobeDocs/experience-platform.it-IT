---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;registro schema;registro schema;
solution: Experience Platform
title: Guida introduttiva all’API del Registro di sistema dello schema
description: Questo documento fornisce un'introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all'API del Registro di sistema dello schema.
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 1%

---

# Guida introduttiva a [!DNL Schema Registry] API

La [!DNL Schema Registry] L’API ti consente di creare e gestire diverse risorse Experience Data Model (XDM). Questo documento fornisce un&#39;introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate al [!DNL Schema Registry] API.

## Prerequisiti

L’utilizzo della guida per gli sviluppatori richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../schema/composition.md): Scopri i blocchi di base degli schemi XDM.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

XDM utilizza la formattazione dello schema JSON per descrivere e convalidare la struttura dei dati sulla customer experience acquisiti. Si consiglia pertanto vivamente di rivedere il [documentazione ufficiale dello schema JSON](https://json-schema.org/) per una migliore comprensione di questa tecnologia di base.

## Lettura di chiamate API di esempio

La [!DNL Schema Registry] La documentazione API fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

## Raccogli i valori delle intestazioni richieste

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], compresi quelli appartenenti al [!DNL Schema Registry], sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione sandbox](../../sandboxes/home.md).

Tutte le richieste di ricerca (GET) al [!DNL Schema Registry] richiedere un `Accept` header, il cui valore determina il formato delle informazioni restituite dall’API. Consulta la sezione [Accetta intestazione](#accept) per ulteriori informazioni, consulta la sezione seguente.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* `Content-Type: application/json`

## Conosci il tuo TENANT_ID {#know-your-tenant_id}

Nelle guide API vengono visualizzati i riferimenti a un `TENANT_ID`. Questo ID viene utilizzato per garantire che le risorse create siano spaccate correttamente e contenute all’interno dell’organizzazione IMS. Se non conosci il tuo ID, puoi accedervi eseguendo la seguente richiesta GET:

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

Una risposta corretta restituisce informazioni relative all&#39;utilizzo da parte della tua organizzazione del [!DNL Schema Registry]. Questo include `tenantId` attributo, il cui valore è il tuo `TENANT_ID`.

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

## Comprendere il `CONTAINER_ID` {#container}

invita [!DNL Schema Registry] L’API richiede l’utilizzo di un `CONTAINER_ID`. Esistono due contenitori per i quali è possibile effettuare chiamate API: la `global` e `tenant` contenitore.

### Contenitore globale

La `global` contenitore contiene tutti gli Adobi standard e [!DNL Experience Platform] il partner ha fornito classi, gruppi di campi di schema, tipi di dati e schemi. È possibile eseguire richieste di elenco e di ricerca (GET) solo per `global` contenitore.

Un esempio di chiamata che utilizza il `global` Il contenitore avrà un aspetto simile al seguente:

```http
GET /global/classes
```

### Contenitore tenant

Da non confondere con il tuo unico `TENANT_ID`, `tenant` Il contenitore contiene tutte le classi, i gruppi di campi, i tipi di dati, gli schemi e i descrittori definiti da un&#39;organizzazione IMS. Sono esclusive per ogni organizzazione, il che significa che non sono visibili o gestibili da altre organizzazioni IMS. Puoi eseguire tutte le operazioni CRUD (GET, POST, PUT, PATCH, DELETE) rispetto alle risorse create in `tenant` contenitore.

Un esempio di chiamata che utilizza il `tenant` Il contenitore avrà un aspetto simile al seguente:

```http
POST /tenant/fieldgroups
```

Quando si crea una classe, un gruppo di campi, uno schema o un tipo di dati nel `tenant` viene salvato nel [!DNL Schema Registry] e assegnato un `$id` URI che include `TENANT_ID`. Questo `$id` viene utilizzato in tutta l’API per fare riferimento a risorse specifiche. Esempi di `$id` I valori vengono forniti nella sezione successiva.

## Identificazione risorsa {#resource-identification}

Le risorse XDM sono identificate con un `$id` sotto forma di URI, ad esempio gli esempi seguenti:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Per rendere l’URI più facile da usare come REST, gli schemi hanno anche una codifica di notazione del punto dell’URI in una proprietà denominata `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

invita [!DNL Schema Registry] L’API supporterà l’URL con codifica `$id` URI o `meta:altId` (formato di notazione del punto). Si consiglia di utilizzare la codifica URL `$id` URI quando si effettua una chiamata REST all’API, come riportato di seguito:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Accetta intestazione {#accept}

Quando si eseguono operazioni di elenco e ricerca (GET) nella [!DNL Schema Registry] API `Accept` per determinare il formato dei dati restituiti dall’API, è necessaria l’intestazione . Quando cerchi risorse specifiche, devi includere anche un numero di versione nel `Accept` intestazione.

Nella tabella seguente è riportato un elenco di elementi compatibili `Accept` i valori di intestazione, compresi quelli con numeri di versione, e le descrizioni di ciò che l&#39;API restituirà una volta utilizzate.

| Accept | Descrizione |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Restituisce solo un elenco di ID. Viene utilizzato più comunemente per elencare le risorse. |
| `application/vnd.adobe.xed+json` | Restituisce un elenco di schemi JSON completi con originale `$ref` e `allOf` incluso. Viene utilizzato per restituire un elenco completo delle risorse. |
| `application/vnd.adobe.xed+json; version=1` | XDM non elaborato con `$ref` e `allOf`. Presenta titoli e descrizioni. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` attributi e `allOf` risolto. Presenta titoli e descrizioni. |
| `application/vnd.adobe.xed-notext+json; version=1` | XDM non elaborato con `$ref` e `allOf`. Nessun titolo o descrizione. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` attributi e `allOf` risolto. Nessun titolo o descrizione. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` attributi e `allOf` risolto. I descrittori sono inclusi. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` e `allOf` risolto, con titoli e descrizioni. I campi obsoleti sono indicati con un `meta:status` attributo `deprecated`. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Platform supporta attualmente una sola versione principale per ogni schema (`1`). Pertanto, il valore `version` deve sempre `1` quando si eseguono richieste di ricerca per restituire la versione secondaria più recente dello schema. Per ulteriori informazioni sul controllo delle versioni dello schema, consulta la sottosezione seguente.

### Controllo delle versioni di uno schema {#versioning}

Alle versioni dello schema viene fatto riferimento da `Accept` intestazioni nell&#39;API del Registro di sistema dello schema e in `schemaRef.contentType` proprietà nei payload API del servizio Platform a valle.

Al momento Platform supporta solo una singola versione principale (`1`) per ogni schema. Secondo il [regole di evoluzione dello schema](../schema/composition.md#evolution), ogni aggiornamento a uno schema deve essere non distruttivo, il che significa che le nuove versioni secondarie di uno schema (`1.2`, `1.3`, ecc.) sono sempre compatibili con le versioni precedenti. Pertanto, quando si specifica `version=1`, il Registro di sistema dello schema restituisce sempre il **più recente** versione principale `1` di uno schema , il che significa che non vengono restituite le versioni secondarie precedenti.

>[!NOTE]
>
>Il requisito non distruttivo per l’evoluzione dello schema viene applicato solo dopo che un set di dati vi ha fatto riferimento e uno dei casi seguenti è vero:
>
>* I dati sono stati acquisiti nel set di dati.
>* Il set di dati è stato abilitato per l’utilizzo in Profilo cliente in tempo reale (anche se non sono stati acquisiti dati).
>
>Se lo schema non è stato associato a un set di dati che soddisfa uno dei criteri di cui sopra, è possibile apportare qualsiasi modifica. Tuttavia, in tutti i casi `version` il componente rimane ancora disponibile `1`.

## Vincoli del campo XDM e best practice

I campi di uno schema sono elencati all’interno dei relativi `properties` oggetto. Ciascun campo è esso stesso un oggetto, contenente gli attributi per descrivere e vincolare i dati che il campo può contenere. Consulta la guida su [definizione di campi personalizzati nell’API](../tutorials/custom-fields-api.md) per esempi di codice e vincoli facoltativi per i tipi di dati più comunemente utilizzati.

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

* Il nome di un oggetto campo può contenere caratteri alfanumerici, trattini o caratteri di sottolineatura, ma **non possono** inizia con un carattere di sottolineatura.
   * **Corretto:** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **Errato:** `_fieldName`
* camelCase è da preferire per il nome dell&#39;oggetto field . Esempio: `fieldName`
* Il campo deve includere un `title`, scritto in Case titolo. Esempio: `Field Name`
* Il campo richiede un `type`.
   * La definizione di alcuni tipi può richiedere un `format`.
   * Se è necessaria una formattazione specifica dei dati, `examples` può essere aggiunto come array.
   * Il tipo di campo può essere definito anche utilizzando qualsiasi tipo di dati presente nel registro. Vedi la sezione su [creazione di un tipo di dati](./data-types.md#create) nella guida dell’endpoint per i tipi di dati per ulteriori informazioni.
* La `description` spiega il campo e le informazioni pertinenti relative ai dati sul campo. Dovrebbe essere scritto in frasi complete con un linguaggio chiaro in modo che chiunque acceda allo schema possa capire le intenzioni del campo.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando [!DNL Schema Registry] API, seleziona una delle guide degli endpoint disponibili.
