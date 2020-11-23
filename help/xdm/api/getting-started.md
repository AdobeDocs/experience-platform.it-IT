---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: Guida introduttiva all'API del Registro di sistema dello schema
description: Questo documento fornisce un'introduzione ai concetti di base da conoscere prima di tentare di eseguire chiamate all'API del Registro di sistema dello schema.
topic: developer guide
translation-type: tm+mt
source-git-commit: b79482635d87efd5b79cf4df781fc0a3a6eb1b56
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 0%

---


# Getting started with the [!DNL Schema Registry] API

L&#39; [!DNL Schema Registry] API consente di creare e gestire diverse risorse Experience Data Model (XDM). Questo documento fornisce un&#39;introduzione ai concetti di base da conoscere prima di tentare di effettuare chiamate all&#39; [!DNL Schema Registry] API.

## Prerequisiti  

L’utilizzo della guida per gli sviluppatori richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione](../schema/composition.md)dello schema: Informazioni sui blocchi di base degli schemi XDM.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

XDM utilizza la formattazione dello schema JSON per descrivere e convalidare la struttura dei dati esperienza cliente acquisiti. Si consiglia pertanto vivamente di consultare la documentazione [](https://json-schema.org/) ufficiale sullo schema JSON per una migliore comprensione di questa tecnologia di base.

## Lettura di chiamate API di esempio

La documentazione [!DNL Schema Registry] API fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi del Experience Platform .

## Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti al gruppo [!DNL Schema Registry], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione relativa alla [sandbox](../../sandboxes/home.md).

Tutte le richieste di ricerca (GET) [!DNL Schema Registry] richiedono un&#39; `Accept` intestazione aggiuntiva, il cui valore determina il formato delle informazioni restituite dall&#39;API. Per ulteriori informazioni, consulta la sezione [Accetta intestazione](#accept) .

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

* `Content-Type: application/json`

## Conosci il tuo TENANT_ID {#know-your-tenant_id}

Nelle guide API verranno visualizzati i riferimenti a un `TENANT_ID`. Questo ID viene utilizzato per garantire che le risorse create siano correttamente denominate e contenute all’interno dell’organizzazione IMS. Se non conosci il tuo ID, puoi accedervi eseguendo la seguente richiesta di GET:

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

Una risposta di successo restituisce informazioni relative all&#39;utilizzo dell&#39; [!DNL Schema Registry]. Questo include un `tenantId` attributo, il cui valore è il vostro `TENANT_ID`.

```JSON
{
  "imsOrg":"{IMS_ORG}",
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
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
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
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
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

## Comprendere le `CONTAINER_ID` {#container}

Le chiamate all&#39; [!DNL Schema Registry] API richiedono l&#39;utilizzo di un `CONTAINER_ID`. Esistono due contenitori in base ai quali è possibile effettuare chiamate API: il `global` contenitore e il `tenant` contenitore.

### Contenitore globale

Il `global` contenitore contiene tutte le classi, i mixin, i tipi di dati e gli schemi standard  Adobe e [!DNL Experience Platform] del partner forniti. È possibile eseguire solo richieste di elenco e di ricerca (GET) per il `global` contenitore.

Esempio di chiamata che utilizza il `global` contenitore:

```http
GET /global/classes
```

### Contenitore tenant

Da non confondere con l&#39;univoco `TENANT_ID`, il `tenant` contenitore contiene tutte le classi, i mixin, i tipi di dati, gli schemi e i descrittori definiti da un&#39;organizzazione IMS. Queste sono esclusive per ogni organizzazione, il che significa che non sono visibili o gestibili da altre organizzazioni IMS. Potete eseguire tutte le operazioni CRUD (GET, POST, PUT, PATCH, DELETE) rispetto alle risorse create nel `tenant` contenitore.

Esempio di chiamata che utilizza il `tenant` contenitore:

```http
POST /tenant/mixins
```

Quando si crea una classe, un mixin, uno schema o un tipo di dati nel `tenant` contenitore, viene salvata nel contenitore [!DNL Schema Registry] e gli viene assegnato un `$id` URI che include il `TENANT_ID`. Questo `$id` viene utilizzato in tutta l&#39;API per fare riferimento a risorse specifiche. Esempi di `$id` valori sono forniti nella sezione successiva.

## Identificazione risorsa {#resource-identification}

Le risorse XDM sono identificate con un `$id` attributo sotto forma di URI, ad esempio gli esempi seguenti:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Per rendere l’URI più facile da usare per il REST, gli schemi dispongono anche di una codifica di notazione dei punti dell’URI in una proprietà denominata `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Le chiamate all&#39; [!DNL Schema Registry] API supporteranno l&#39;URI con codifica URL `$id` o il formato `meta:altId` (notazione punto). Come procedura ottimale, usate l’ `$id` URI con codifica URL per effettuare una chiamata REST all’API, come segue:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Accetta intestazione {#accept}

Quando si eseguono operazioni di elenco e ricerca (GET) nell&#39; [!DNL Schema Registry] API, è necessaria un&#39; `Accept` intestazione per determinare il formato dei dati restituiti dall&#39;API. Quando si cercano risorse specifiche, nell’ `Accept` intestazione deve essere incluso anche un numero di versione.

Nella tabella seguente sono elencati i valori di `Accept` intestazione compatibili, inclusi quelli con numeri di versione, insieme alle descrizioni di ciò che l&#39;API restituirà quando verrà utilizzata.

| Accetta | Descrizione |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Restituisce solo un elenco di ID. Viene utilizzato più comunemente per elencare le risorse. |
| `application/vnd.adobe.xed+json` | Restituisce un elenco dello schema JSON completo con originale `$ref` e `allOf` incluso. Viene utilizzato per restituire un elenco completo delle risorse. |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | XDM raw con `$ref` e `allOf`. Contiene titoli e descrizioni. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` e `allOf` risolto. Contiene titoli e descrizioni. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | XDM raw con `$ref` e `allOf`. Nessun titolo o descrizione. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` e `allOf` risolto. Nessun titolo o descrizione. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` e `allOf` risolto. I descrittori sono inclusi. |

>[!NOTE]
>
>Se si fornisce solo la versione principale (ad esempio 1, 2, 3), il registro restituirà la versione minore più recente (ad esempio .1, .2, .3) automaticamente.

## Vincoli del campo XDM e procedure ottimali

I campi di uno schema sono elencati all&#39;interno del relativo `properties` oggetto. Ciascun campo è esso stesso un oggetto contenente attributi per descrivere e vincolare i dati che il campo può contenere.

Ulteriori informazioni sulla definizione dei tipi di campo nell&#39;API sono disponibili nell&#39; [appendice](appendix.md) di questa guida, inclusi esempi di codice e vincoli facoltativi per i tipi di dati più comunemente utilizzati.

Il seguente campo di esempio illustra un campo XDM formattato correttamente, con ulteriori dettagli sui vincoli di denominazione e sulle procedure ottimali riportati di seguito. Queste pratiche possono essere applicate anche quando si definiscono altre risorse che contengono attributi simili.

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

* Il nome di un oggetto campo può contenere caratteri alfanumerici, trattini o caratteri di sottolineatura, ma non **** può iniziare con un carattere di sottolineatura.
   * **Corretto:** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **Scorretto:** `_fieldName`
* camelCase è preferibile per il nome dell&#39;oggetto field. Esempio: `fieldName`
* Il campo deve includere un `title`, scritto in Case titolo. Esempio: `Field Name`
* Il campo richiede un `type`.
   * La definizione di alcuni tipi può richiedere un facoltativo `format`.
   * Se è necessaria una formattazione specifica dei dati, `examples` è possibile aggiungerla come array.
   * Il tipo di campo può essere definito anche utilizzando qualsiasi tipo di dati presente nel registro. Per ulteriori informazioni, vedere la sezione sulla [creazione di un tipo](./data-types.md#create) di dati nella guida dell&#39;endpoint dei tipi di dati.
* Vengono `description` descritti il campo e le informazioni pertinenti relative ai dati del campo. Dovrebbe essere scritto in frasi complete con un linguaggio chiaro in modo che chiunque acceda allo schema possa capire le intenzioni del campo.

Per ulteriori informazioni sulla definizione di diversi tipi di campi nell&#39;API, consulta il documento sui vincoli [](../schema/field-constraints.md) del campo.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39; [!DNL Schema Registry] API, seleziona una delle guide degli endpoint disponibili.
