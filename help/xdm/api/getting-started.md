---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida per lo sviluppo API del Registro di sistema dello schema
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 0%

---


# Guida per lo sviluppo API del Registro di sistema dello schema

Il Registro di sistema dello schema viene utilizzato per accedere alla Libreria schema all&#39;interno  Adobe Experience Platform, fornendo un&#39;interfaccia utente e RESTful API da cui sono accessibili tutte le risorse libreria disponibili.

Utilizzando l&#39;API del Registro di sistema dello schema, è possibile eseguire operazioni CRUD di base per visualizzare e gestire tutti gli schemi e le risorse correlate disponibili all&#39;interno  Adobe Experience Platform. Sono inclusi quelli definiti da Adobe,  partner Experience Platform e fornitori le cui applicazioni vengono utilizzate. Potete inoltre utilizzare le chiamate API per creare nuovi schemi e risorse per la vostra organizzazione, nonché visualizzare e modificare le risorse già definite.

Questa guida per gli sviluppatori fornisce i passaggi necessari per iniziare a utilizzare l&#39;API del Registro di sistema dello schema. La guida fornisce quindi chiamate API di esempio per eseguire operazioni chiave utilizzando il Registro di sistema dello schema.

## Prerequisiti

Questa guida richiede una buona conoscenza dei seguenti componenti del  Adobe Experience Platform:

* [Sistema](../home.md)XDM (Experience Data Model): Framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../schema/composition.md)dello schema: Informazioni sui blocchi di base degli schemi XDM.
* [Profilo](../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../sandboxes/home.md):  Experience Platform fornisce sandbox virtuali che dividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per eseguire correttamente chiamate all&#39;API del Registro di sistema dello schema.

## Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi di  Experience Platform.

## Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API Platform, è prima necessario completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API Experience Platform, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in  Experience Platform, comprese quelle appartenenti al Registro di sistema dello schema, sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API Platform richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Platform, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste di ricerca (GET) al Registro di sistema dello schema richiedono un&#39;intestazione Accetto aggiuntiva, il cui valore determina il formato delle informazioni restituite dall&#39;API. Per ulteriori informazioni, consulta la sezione [Accetta intestazione](#accept) .

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

* Content-Type: application/json

## Conosci il tuo TENANT_ID {#know-your-tenant_id}

In questa guida verranno visualizzati i riferimenti a un `TENANT_ID`. Questo ID viene utilizzato per garantire che le risorse create siano correttamente denominate e contenute all’interno dell’organizzazione IMS. Se non conosci il tuo ID, puoi accedervi eseguendo la seguente richiesta GET:

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

Una risposta corretta restituisce informazioni relative all&#39;utilizzo del Registro di sistema dello schema da parte dell&#39;organizzazione. Questo include un `tenantId` attributo, il cui valore è il vostro `TENANT_ID`.

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

* `tenantId`: Il `TENANT_ID` valore per l’organizzazione IMS.

## Comprendere le `CONTAINER_ID` {#container}

Le chiamate all&#39;API del Registro di sistema dello schema richiedono l&#39;utilizzo di un `CONTAINER_ID`. Esistono due contenitori in base ai quali è possibile effettuare chiamate API: il contenitore **** globale e il contenitore **** tenant.

### Contenitore globale

Il contenitore globale include tutte le classi, i mixin, i tipi di dati e gli schemi standard di Adobe e  partner Experience Platform. È possibile eseguire solo richieste di elenco e ricerca (GET) per il contenitore globale.

### Contenitore tenant

Da non confondere con l&#39;univoco `TENANT_ID`, il contenitore tenant contiene tutte le classi, i mixin, i tipi di dati, gli schemi e i descrittori definiti da un&#39;organizzazione IMS. Queste sono esclusive per ogni organizzazione, il che significa che non sono visibili o gestibili da altre organizzazioni IMS. È possibile eseguire tutte le operazioni CRUD (GET, POST, PUT, PATCH, DELETE) rispetto alle risorse create nel contenitore tenant.

Quando si crea una classe, un mixin, uno schema o un tipo di dati nel contenitore tenant, questo viene salvato nel Registro di sistema dello schema e gli viene assegnato un `$id` URI che include l&#39;utente `TENANT_ID`. Questo `$id` viene utilizzato in tutta l&#39;API per fare riferimento a risorse specifiche. Esempi di `$id` valori sono forniti nella sezione successiva.

## Identificazione dello schema {#schema-identification}

Gli schemi sono identificati con un `$id` attributo in forma di URI, ad esempio:
* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Per rendere l’URI più facile da usare per il REST, gli schemi dispongono anche di una codifica di notazione dei punti dell’URI in una proprietà denominata `meta:altId`:
* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Le chiamate all&#39;API del Registro di sistema dello schema supporteranno l&#39; `$id` URI con codifica URL o il formato `meta:altId` (notazione punto). Come procedura ottimale, usate l’ `$id` URI con codifica URL per effettuare una chiamata REST all’API, come segue:
* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Accetta intestazione {#accept}

Quando si eseguono operazioni di elenco e ricerca (GET) nell&#39;API del Registro di sistema dello schema, è necessario un&#39;intestazione Accetto per determinare il formato dei dati restituiti dall&#39;API. Quando si cercano risorse specifiche, nell’intestazione Accetto deve essere incluso anche un numero di versione.

Nella tabella seguente sono elencati i valori di intestazione Accetta compatibili, inclusi quelli con numeri di versione, insieme alle descrizioni di ciò che l&#39;API restituirà quando verrà utilizzata.

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
>Se fornisci solo la `major` versione (ad esempio 1, 2, 3), il registro restituirà la versione più recente `minor` (ad esempio .1, .2, .3) automaticamente.

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
   * Il tipo di campo può essere definito anche utilizzando qualsiasi tipo di dati presente nel registro. Per ulteriori informazioni, consulta la sezione sulla [creazione di un tipo](create-data-type.md) di dati in questa guida.
* Vengono `description` descritti il campo e le informazioni pertinenti relative ai dati del campo. Dovrebbe essere scritto in frasi complete con un linguaggio chiaro in modo che chiunque acceda allo schema possa capire le intenzioni del campo.

Per ulteriori informazioni sulla definizione dei tipi di campo nell&#39;API, consultate l&#39; [appendice](appendix.md) .

## Passaggi successivi

Questo documento ha trattato le conoscenze preliminari necessarie per effettuare chiamate all&#39;API del Registro di sistema dello schema, incluse le credenziali di autenticazione richieste. Potete ora procedere alle chiamate di esempio fornite in questa guida per gli sviluppatori e seguire le relative istruzioni. Per una descrizione dettagliata di come creare uno schema nell&#39;API, fare riferimento alla seguente [esercitazione](../tutorials/create-schema-api.md).
