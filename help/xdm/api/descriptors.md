---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;Experience data model;Experience data model;Experience Data Model;modello dati;modello dati;modello dati;modello dati;registro schema;registro schema;descrittore;descrittore;descrittori;descrittori;identità;nome descrittivo;nome descrittivo;alternatedisplayinfo;riferimento;riferimento;relazione;relazione
solution: Experience Platform
title: Endpoint API per i descrittori
description: L’endpoint /descriptors nell’API Schema Registry consente di gestire in modo programmatico i descrittori XDM all’interno dell’applicazione Experience.
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 81b53d2bd84eacb32999b957bee9b5e9aa77d5f7
workflow-type: tm+mt
source-wordcount: '1873'
ht-degree: 2%

---

# Endpoint &quot;descriptors&quot;

Gli schemi definiscono una visualizzazione statica delle entità dati, ma non forniscono dettagli specifici sul modo in cui i dati basati su tali schemi (ad esempio, i set di dati) possono relazionarsi tra loro. Adobe Experience Platform consente di descrivere queste relazioni e altri metadati interpretativi su uno schema utilizzando i descrittori.

I descrittori degli schemi sono metadati a livello di tenant, ovvero sono univoci per l’organizzazione IMS e tutte le operazioni dei descrittori hanno luogo nel contenitore tenant.

A ogni schema possono essere applicate una o più entità descrittive dello schema. Ogni entità descrittore dello schema include un descrittore `@type` e `sourceSchema` cui si applica. Una volta applicati, questi descrittori verranno applicati a tutti i set di dati creati utilizzando lo schema.

Il `/descriptors` endpoint nella [!DNL Schema Registry] API consente di gestire in modo programmatico i descrittori all’interno dell’applicazione Experience.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’[[!DNL Schema Registry] API di ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Prima di continuare, controlla [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida per la lettura delle chiamate API di esempio di questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recuperare un elenco di descrittori {#list}

Puoi elencare tutti i descrittori definiti dalla tua organizzazione effettuando una richiesta GET a `/tenant/descriptors`.

**Formato API**

```http
GET /tenant/descriptors
```

**Richiesta**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

Il formato della risposta dipende da `Accept` intestazione inviata nella richiesta. Tieni presente che `/descriptors` utilizzi endpoint `Accept` intestazioni diverse da tutti gli altri endpoint nel [!DNL Schema Registry] API.

>[!IMPORTANT]
>
>I descrittori richiedono univoci `Accept` intestazioni che sostituiscono `xed` con `xdm`, e offrono anche un `link` opzione univoca per i descrittori. Il corretto `Accept` le intestazioni sono state incluse negli esempi di chiamate riportati di seguito, ma è necessario prestare particolare attenzione per assicurarsi che vengano utilizzate le intestazioni corrette quando si lavora con i descrittori.

| `Accept` intestazione | Descrizione |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Restituisce una matrice di ID descrittori |
| `application/vnd.adobe.xdm-link+json` | Restituisce una matrice di percorsi API descrittori |
| `application/vnd.adobe.xdm+json` | Restituisce una matrice di oggetti descrittori espansi |
| `application/vnd.adobe.xdm-v2+json` | Questo `Accept` per utilizzare le funzionalità di paging, è necessario utilizzare l’intestazione. |

{style="table-layout:auto"}

**Risposta**

La risposta include un array per ogni tipo di descrittore che ha definito i descrittori. In altre parole, se non ci sono descrittori di un determinato `@type` definito, il Registro di sistema non restituirà una matrice vuota per quel tipo di descrittore.

Quando si utilizza `link` `Accept` , ogni descrittore viene visualizzato come un elemento array nel formato `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

```JSON
{
  "xdm:alternateDisplayInfo": [
    "/tenant/descriptors/85dc1bc8b91516ac41163365318e38a9f1e4f351",
    "/tenant/descriptors/49bd5abb5a1310ee80ebc1848eb508d383a462cf",
    "/tenant/descriptors/b3b3e548f1c653326bcf5459ceac4140fc0b9e08"
  ],
  "xdm:descriptorIdentity": [
    "/tenant/descriptors/f7a4bc25429496c4740f8f9a7a49ba96862c5379"
  ],
  "xdm:descriptorOneToOne": [
    "/tenant/descriptors/cb509fd6f8ab6304e346905441a34b58a0cd481a"
  ]
}
```

## Cercare un descrittore {#lookup}

Se desideri visualizzare i dettagli di un descrittore specifico, puoi cercare (GET) un singolo descrittore utilizzando `@id`.

**Formato API**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DESCRIPTOR_ID}` | Il `@id` del descrittore che desideri cercare. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente recupera un descrittore tramite il suo `@id` valore. I descrittori non dispongono di versioni, pertanto no `Accept` L’intestazione è obbligatoria nella richiesta di ricerca.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del descrittore, inclusi i relativi `@type` e `sourceSchema`, nonché informazioni aggiuntive che variano a seconda del tipo di descrittore. Il restituito `@id` deve corrispondere al descrittore `@id` fornite nella richiesta.

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "createdUser": "{CREATED_USER}",
  "imsOrg": "{ORG_ID}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Creare un descrittore {#create}

Per creare un nuovo descrittore, devi effettuare una richiesta POST al `/tenant/descriptors` endpoint.

>[!IMPORTANT]
>
>Il [!DNL Schema Registry] consente di definire diversi tipi di descrittori. Ogni tipo di descrittore richiede l’invio di campi specifici nel corpo della richiesta. Consulta la [appendice](#defining-descriptors) per un elenco completo dei descrittori e dei campi necessari per definirli.

**Formato API**

```http
POST /tenant/descriptors
```

**Richiesta**

La seguente richiesta definisce un descrittore di identità in un campo &quot;indirizzo e-mail&quot; in uno schema di esempio. Questo comunica [!DNL Experience Platform] utilizzare l’indirizzo e-mail come identificatore per unire le informazioni sull’individuo.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 (Creato) e i dettagli del descrittore appena creato, inclusi `@id`. Il `@id` è un campo di sola lettura assegnato da [!DNL Schema Registry] e utilizzato per fare riferimento al descrittore nell’API.

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Aggiornare un descrittore {#put}

Per aggiornare un descrittore, devi includere `@id` nel percorso di una richiesta PUT.

**Formato API**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DESCRIPTOR_ID}` | Il `@id` del descrittore che desideri aggiornare. |

{style="table-layout:auto"}

**Richiesta**

Questa richiesta riscrive essenzialmente il descrittore, pertanto il corpo della richiesta deve includere tutti i campi necessari per definire un descrittore di quel tipo. In altre parole, il payload della richiesta di aggiornamento (PUT) di un descrittore è lo stesso del payload di [creare (POST) un descrittore](#create) dello stesso tipo.

>[!IMPORTANT]
>
>Come per la creazione di descrittori con richieste POST, ogni tipo di descrittore richiede l’invio di campi specifici nei payload di richieste PUT. Consulta la [appendice](#defining-descriptors) per un elenco completo dei descrittori e dei campi necessari per definirli.

L’esempio seguente aggiorna un descrittore di identità in modo che faccia riferimento a un diverso `xdm:sourceProperty` (`mobile phone`) e modificare la `xdm:namespace` a `Phone`.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/mobilePhone/number",
        "xdm:namespace": "Phone",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 (Creato) e il `@id` del descrittore aggiornato (che deve corrispondere al `@id` inviato nella richiesta).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

Esecuzione di una [richiesta di ricerca (GET)](#lookup) per visualizzare il descrittore, i campi sono stati aggiornati per riflettere le modifiche inviate nella richiesta PUT.

## Eliminare un descrittore {#delete}

Talvolta potrebbe essere necessario rimuovere un descrittore definito dall&#39; [!DNL Schema Registry]. A tale scopo, effettua una richiesta DELETE facendo riferimento al `@id` del descrittore che desideri rimuovere.

**Formato API**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DESCRIPTOR_ID}` | Il `@id` del descrittore che desideri eliminare. |

{style="table-layout:auto"}

**Richiesta**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto) e un corpo vuoto.

Per confermare che il descrittore è stato eliminato, puoi eseguire una [richiesta di ricerca](#lookup) rispetto al descrittore `@id`. La risposta restituisce lo stato HTTP 404 (non trovato) perché il descrittore è stato rimosso dal [!DNL Schema Registry].

## Appendice

La sezione seguente fornisce informazioni aggiuntive sull’utilizzo dei descrittori in [!DNL Schema Registry] API.

### Definizione dei descrittori {#defining-descriptors}

Le sezioni seguenti forniscono una panoramica dei tipi di descrittori disponibili, inclusi i campi obbligatori per la definizione di un descrittore per ciascun tipo.

#### Descrittore di identità

Un descrittore di identità segnala che &quot;[!UICONTROL sourceProperty]&quot; del &quot;[!UICONTROL sourceSchema]&quot; è un [!DNL Identity] campo come descritto da [Servizio Adobe Experience Platform Identity](../../identity-service/home.md).

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false
}
```

| Proprietà | Descrizione |
| --- | --- |
| `@type` | Tipo di descrittore da definire. Per un descrittore di identità, questo valore deve essere impostato su `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | Il `$id` URI dello schema in cui viene definito il descrittore. |
| `xdm:sourceVersion` | Versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso della proprietà specifica che sarà l’identità. Il percorso deve iniziare con &quot;/&quot; e non terminare con uno. Non includere &quot;properties&quot; nel percorso (ad esempio, utilizza &quot;/personalEmail/address&quot; invece di &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:namespace` | Il `id` o `code` valore dello spazio dei nomi dell’identità. È possibile trovare un elenco di spazi dei nomi utilizzando [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service). |
| `xdm:property` | o `xdm:id` o `xdm:code`, a seconda della `xdm:namespace` utilizzato. |
| `xdm:isPrimary` | Valore booleano facoltativo. Se è true, indica il campo come identità primaria. Gli schemi possono contenere una sola identità primaria. |

{style="table-layout:auto"}

#### Descrittore del nome intuitivo {#friendly-name}

I descrittori di nomi descrittivi consentono a un utente di modificare `title`, `description`, e `meta:enum` valori dei campi dello schema della libreria principale. Particolarmente utile quando si lavora con &quot;eVar&quot; e altri campi &quot;generici&quot; che si desidera etichettare come contenenti informazioni specifiche dell’organizzazione. L’interfaccia utente può utilizzarli per mostrare un nome più descrittivo o per mostrare solo i campi con un nome descrittivo.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:title": {
    "en_us": "Event Type"
  },
  "xdm:description": {
    "en_us": "The type of experience event detected by the system."
  },
  "meta:enum": {
    "click": "Mouse Click",
    "addCart": "Add to Cart",
    "checkout": "Cart Checkout"
  },
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out",
    "media.ping": "Media ping"
  }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `@type` | Tipo di descrittore da definire. Per un descrittore di nome descrittivo, questo valore deve essere impostato su `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | Il `$id` URI dello schema in cui viene definito il descrittore. |
| `xdm:sourceVersion` | Versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso della proprietà specifica di cui si desidera modificare i dettagli. Il percorso deve iniziare con una barra (`/`) e non terminare con uno. Non includere `properties` nel percorso (ad esempio, utilizza `/personalEmail/address` invece di `/properties/personalEmail/properties/address`). |
| `xdm:title` | Il nuovo titolo che si desidera visualizzare per questo campo, scritto in Maiuscole/minuscole. |
| `xdm:description` | È possibile aggiungere una descrizione facoltativa insieme al titolo. |
| `meta:enum` | Se il campo indicato da `xdm:sourceProperty` è un campo stringa, `meta:enum` può essere utilizzato per aggiungere valori suggeriti per il campo nell’interfaccia utente di segmentazione. È importante notare che `meta:enum` non dichiara un’enumerazione né fornisce alcuna convalida dei dati per il campo XDM.<br><br>Da utilizzare solo per i campi XDM di base definiti dall’Adobe. Se la proprietà di origine è un campo personalizzato definito dall’organizzazione, è invece necessario modificare la proprietà `meta:enum` proprietà direttamente tramite una richiesta PATCH alla risorsa principale del campo. |
| `meta:excludeMetaEnum` | Se il campo indicato da `xdm:sourceProperty` è un campo stringa con valori suggeriti esistenti forniti in un `meta:enum` , puoi includere questo oggetto in un descrittore di nome descrittivo per escludere alcuni o tutti questi valori dalla segmentazione. La chiave e il valore di ogni voce devono corrispondere a quelli inclusi nell&#39;originale `meta:enum` del campo per escludere la voce. |

{style="table-layout:auto"}

#### Descrittore di relazione

I descrittori di relazione descrivono una relazione tra due schemi diversi, basata sulle proprietà descritte in `sourceProperty` e `destinationProperty`. Guarda il tutorial su [definizione di una relazione tra due schemi](../tutorials/relationship-api.md) per ulteriori informazioni.

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:destinationSchema": 
    "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:destinationVersion": 1,
  "xdm:destinationProperty": "/parentField/subField"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `@type` | Tipo di descrittore da definire. Per un descrittore di relazione, questo valore deve essere impostato su `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | Il `$id` URI dello schema in cui viene definito il descrittore. |
| `xdm:sourceVersion` | Versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso del campo nello schema di origine in cui viene definita la relazione. Deve iniziare con &quot;/&quot; e non finire con uno. Non includere &quot;properties&quot; nel percorso (ad esempio, &quot;/personalEmail/address&quot; invece di &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | Il `$id` URI dello schema di riferimento con cui questo descrittore definisce una relazione. |
| `xdm:destinationVersion` | Versione principale dello schema di riferimento. |
| `xdm:destinationProperty` | Percorso opzionale di un campo di destinazione all’interno dello schema di riferimento. Se questa proprietà viene omessa, il campo di destinazione viene dedotto da tutti i campi che contengono un descrittore di identità di riferimento corrispondente (vedi sotto). |

{style="table-layout:auto"}

#### Descrittore dell’identità di riferimento

I descrittori di identità di riferimento forniscono un contesto di riferimento all’identità primaria di un campo schema, consentendo che i campi di altri schemi vi facciano riferimento. Lo schema di riferimento deve avere già un campo di identità primaria definito prima che altri schemi possano farvi riferimento tramite questo descrittore.

```json
{
  "@type": "xdm:descriptorReferenceIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:identityNamespace": "Email"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `@type` | Tipo di descrittore da definire. Per un descrittore di identità di riferimento, questo valore deve essere impostato su `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | Il `$id` URI dello schema in cui viene definito il descrittore. |
| `xdm:sourceVersion` | Versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso del campo nello schema di origine che verrà utilizzato per fare riferimento allo schema di riferimento. Deve iniziare con &quot;/&quot; e non finire con uno. Non includere &quot;properties&quot; nel percorso (ad esempio, `/personalEmail/address` invece di `/properties/personalEmail/properties/address`). |
| `xdm:identityNamespace` | Il codice dello spazio dei nomi dell’identità per la proprietà sorgente. |

{style="table-layout:auto"}

#### Descrittore di campo obsoleto

È possibile [rendere obsoleto un campo all’interno di una risorsa XDM personalizzata](../tutorials/field-deprecation-api.md#custom) aggiungendo un `meta:status` attributo impostato su `deprecated` al campo in questione. Tuttavia, se desideri rendere obsoleti i campi forniti dalle risorse XDM standard negli schemi, puoi assegnare allo schema in questione un descrittore di campo obsoleto per ottenere lo stesso effetto. Utilizzo di [corretto `Accept` intestazione](../tutorials/field-deprecation-api.md#verify-deprecation), puoi quindi visualizzare quali campi standard sono obsoleti per uno schema quando lo cerchi nell’API.

```json
{
  "@type": "xdm:descriptorDeprecated",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/faxPhone"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `@type` | Tipo di descrittore. Per un descrittore di campo obsoleto, questo valore deve essere impostato su `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | URI `$id` dello schema a cui si sta applicando il descrittore. |
| `xdm:sourceVersion` | Versione dello schema a cui si sta applicando il descrittore. Deve essere impostato su `1`. |
| `xdm:sourceProperty` | Percorso della proprietà all’interno dello schema a cui si sta applicando il descrittore. Se desideri applicare il descrittore a più proprietà, puoi fornire un elenco di percorsi sotto forma di array (ad esempio, `["/firstName", "/lastName"]`). |

{style="table-layout:auto"}
