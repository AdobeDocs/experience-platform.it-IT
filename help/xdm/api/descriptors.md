---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;modello dati;registro schema;registro schema;descrittore;descrittori;descrittori;identità;nome descrittivo;nome descrittivo;nome descrittivo;nome descrittivo;alternatedisplayinfo;riferimento;riferimento;relazione;relazione
solution: Experience Platform
title: Endpoint API per descrittori
description: L’endpoint /descriptors nell’API del Registro di sistema dello schema ti consente di gestire programmaticamente i descrittori XDM all’interno dell’applicazione di esperienza.
topic-legacy: developer guide
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: e8ad829ac4ea89c0d0167e6b414db577c9ecf094
workflow-type: tm+mt
source-wordcount: '1900'
ht-degree: 4%

---

# Endpoint descrittori

Gli schemi definiscono una visualizzazione statica delle entità dati, ma non forniscono dettagli specifici sul modo in cui i dati basati su questi schemi (ad esempio, i set di dati) possono essere correlati tra loro. Adobe Experience Platform ti consente di descrivere queste relazioni e altri metadati interpretativi su uno schema utilizzando i descrittori.

I descrittori di schema sono metadati a livello di tenant, il che significa che sono univoci per la tua organizzazione IMS e che tutte le operazioni dei descrittori hanno luogo nel contenitore tenant.

A ogni schema può essere applicata una o più entità descrittrici di schema. Ogni entità descrittrice dello schema include un descrittore `@type` e `sourceSchema` a cui si applica. Una volta applicati, questi descrittori verranno applicati a tutti i set di dati creati utilizzando lo schema.

La `/descriptors` punto finale [!DNL Schema Registry] L’API ti consente di gestire in modo programmatico i descrittori all’interno dell’applicazione di esperienza.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’[[!DNL Schema Registry] API di ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e importanti informazioni sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recupera un elenco di descrittori {#list}

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

Il formato della risposta dipende dal `Accept` intestazione inviata nella richiesta. Tieni presente che `/descriptors` utilizzi endpoint `Accept` intestazioni diverse da tutti gli altri endpoint nel [!DNL Schema Registry] API.

>[!IMPORTANT]
>
>I descrittori richiedono un valore univoco `Accept` intestazioni che sostituiscono `xed` con `xdm`e offre anche `link` opzione univoca per i descrittori. Il `Accept` le intestazioni sono state incluse nelle chiamate di esempio riportate di seguito, ma presta molta attenzione a garantire che vengano utilizzate le intestazioni corrette quando lavori con i descrittori.

| `Accept` header | Descrizione |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Restituisce una matrice di ID descrittori |
| `application/vnd.adobe.xdm-link+json` | Restituisce una matrice di percorsi API descrittivi |
| `application/vnd.adobe.xdm+json` | Restituisce una matrice di oggetti descrittivi espansi |
| `application/vnd.adobe.xdm-v2+json` | Questo `Accept` Per utilizzare le funzionalità di paging, è necessario utilizzare l&#39;intestazione . |

{style=&quot;table-layout:auto&quot;}

**Risposta**

La risposta include una matrice per ogni tipo di descrittore con descrittori definiti. In altre parole, se non ci sono descrittori di un certo `@type` definito, il Registro di sistema non restituirà una matrice vuota per quel tipo di descrittore.

Quando utilizzi `link` `Accept` intestazione, ogni descrittore viene visualizzato come un elemento array nel formato `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

Se desideri visualizzare i dettagli di un descrittore specifico, puoi cercare (GET) un singolo descrittore utilizzando il relativo `@id`.

**Formato API**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DESCRIPTOR_ID}` | La `@id` del descrittore che si desidera cercare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La seguente richiesta recupera un descrittore dalla relativa `@id` valore. I descrittori non dispongono di versioni, pertanto non sono disponibili `Accept` L’intestazione è obbligatoria nella richiesta di ricerca.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli del descrittore, incluso il relativo `@type` e `sourceSchema`, nonché informazioni aggiuntive che variano a seconda del tipo di descrittore. Il restituito `@id` deve corrispondere al descrittore `@id` nella richiesta.

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

Puoi creare un nuovo descrittore effettuando una richiesta POST al `/tenant/descriptors` punto finale.

>[!IMPORTANT]
>
>La [!DNL Schema Registry] consente di definire diversi tipi di descrittori. Ogni tipo di descrittore richiede che i propri campi specifici siano inviati nel corpo della richiesta. Consulta la sezione [appendice](#defining-descriptors) per un elenco completo dei descrittori e dei campi necessari per definirli.

**Formato API**

```http
POST /tenant/descriptors
```

**Richiesta**

La richiesta seguente definisce un descrittore di identità su un campo &quot;Indirizzo e-mail&quot; in uno schema di esempio. Questo è [!DNL Experience Platform] utilizzare l’indirizzo e-mail come identificatore per unire le informazioni sull’utente.

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

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e i dettagli del descrittore appena creato, incluso il relativo `@id`. La `@id` è un campo di sola lettura assegnato da [!DNL Schema Registry] e utilizzato per fare riferimento al descrittore nell’API.

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

È possibile aggiornare un descrittore includendo il relativo `@id` nel percorso di una richiesta PUT.

**Formato API**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DESCRIPTOR_ID}` | La `@id` del descrittore da aggiornare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

Questa richiesta essenzialmente riscrive il descrittore, pertanto il corpo della richiesta deve includere tutti i campi necessari per definire un descrittore di quel tipo. In altre parole, il payload della richiesta per aggiornare (PUT) un descrittore è lo stesso del payload per [creare (POST) un descrittore](#create) dello stesso tipo.

>[!IMPORTANT]
>
>Come per la creazione di descrittori utilizzando le richieste di POST, ogni tipo di descrittore richiede l’invio di campi specifici nei payload di richiesta PUT. Consulta la sezione [appendice](#defining-descriptors) per un elenco completo dei descrittori e dei campi necessari per definirli.

Nell&#39;esempio seguente viene aggiornato un descrittore di identità per fare riferimento a un diverso `xdm:sourceProperty` (`mobile phone`) e modifica il `xdm:namespace` a `Phone`.

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

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e il `@id` del descrittore aggiornato (che deve corrispondere al `@id` inviato nella richiesta).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

Esecuzione di un [richiesta di ricerca (GET)](#lookup) per visualizzare il descrittore, i campi sono stati aggiornati per riflettere le modifiche inviate nella richiesta di PUT.

## Eliminare un descrittore {#delete}

A volte può essere necessario rimuovere un descrittore definito dalla [!DNL Schema Registry]. A questo scopo, invia una richiesta DELETE che fa riferimento al `@id` del descrittore che si desidera rimuovere.

**Formato API**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DESCRIPTOR_ID}` | La `@id` del descrittore da eliminare. |

{style=&quot;table-layout:auto&quot;}

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

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto.

Per confermare che il descrittore è stato eliminato, puoi eseguire un [richiesta di ricerca](#lookup) contro il descrittore `@id`. La risposta restituisce lo stato HTTP 404 (Non trovato) perché il descrittore è stato rimosso dalla [!DNL Schema Registry].

## Appendice

La sezione seguente fornisce informazioni aggiuntive sulle operazioni con i descrittori nel [!DNL Schema Registry] API.

### Definizione dei descrittori {#defining-descriptors}

Le sezioni seguenti forniscono una panoramica dei tipi di descrittori disponibili, compresi i campi obbligatori per la definizione di un descrittore di ciascun tipo.

#### Descrittore di identità

Un descrittore di identità segnala che &quot;[!UICONTROL sourceProperty]&quot; del &quot;[!UICONTROL sourceSchema]&quot; è un [!DNL Identity] campo descritto da [Servizio Adobe Experience Platform Identity](../../identity-service/home.md).

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
| `@type` | Il tipo di descrittore da definire. Per un descrittore di identità, questo valore deve essere impostato su `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | La `$id` URI dello schema in cui viene definito il descrittore. |
| `xdm:sourceVersion` | Versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso della proprietà specifica che sarà l&#39;identità. Il percorso deve iniziare con un &quot;/&quot; e non terminare con uno. Non includere &quot;proprietà&quot; nel percorso (ad esempio, usa &quot;/personalEmail/address&quot; invece di &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:namespace` | La `id` o `code` valore dello spazio dei nomi identità. È possibile trovare un elenco di spazi dei nomi utilizzando [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service). |
| `xdm:property` | O `xdm:id` o `xdm:code`, a seconda del `xdm:namespace` utilizzato. |
| `xdm:isPrimary` | Un valore booleano facoltativo. Se true, indica il campo come identità principale. Gli schemi possono contenere una sola identità principale. |

{style=&quot;table-layout:auto&quot;}

#### descrittore di nome descrittivo {#friendly-name}

I descrittori di nomi descrittivi consentono a un utente di modificare `title`, `description`e `meta:enum` valori dei campi dello schema della libreria principale. Particolarmente utile quando si lavora con &quot;eVar&quot; e altri campi &quot;generici&quot; che si desidera etichettare come contenenti informazioni specifiche della propria organizzazione. L’interfaccia utente può usarli per mostrare un nome più descrittivo o per mostrare solo i campi con un nome descrittivo.

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
| `@type` | Il tipo di descrittore da definire. Per un descrittore di nome descrittivo, questo valore deve essere impostato su `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | La `$id` URI dello schema in cui viene definito il descrittore. |
| `xdm:sourceVersion` | Versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso della proprietà specifica di cui si desidera modificare i dettagli. Il percorso deve iniziare con una barra (`/`) e non terminare con uno. Non includere `properties` nel percorso (ad esempio, utilizza `/personalEmail/address` anziché `/properties/personalEmail/properties/address`). |
| `xdm:title` | Nuovo titolo da visualizzare per questo campo, scritto in Case titolo. |
| `xdm:description` | È possibile aggiungere una descrizione facoltativa insieme al titolo. |
| `meta:enum` | Se il campo indicato da `xdm:sourceProperty` è un campo stringa, `meta:enum` può essere utilizzato per aggiungere valori consigliati per il campo nell’interfaccia utente Segmentazione. È importante notare che `meta:enum` non dichiara un&#39;enumerazione né fornisce alcuna convalida di dati per il campo XDM.<br><br>Deve essere utilizzato solo per i campi XDM di base definiti da Adobe. Se la proprietà sorgente è un campo personalizzato definito dall&#39;organizzazione, è invece necessario modificare il campo `meta:enum` direttamente tramite una richiesta di PATCH alla risorsa principale del campo. |
| `meta:excludeMetaEnum` | Se il campo indicato da `xdm:sourceProperty` è un campo stringa che contiene valori suggeriti esistenti forniti in un `meta:enum` è possibile includere questo oggetto in un descrittore di nome descrittivo per escludere alcuni o tutti questi valori dalla segmentazione. La chiave e il valore di ciascuna voce devono corrispondere a quelli inclusi nell&#39;originale `meta:enum` del campo per escludere la voce. |

{style=&quot;table-layout:auto&quot;}

#### Descrittore di relazione

I descrittori di relazione descrivono una relazione tra due schemi diversi, basata sulle proprietà descritte in `sourceProperty` e `destinationProperty`. Guarda l’esercitazione su [definizione di una relazione tra due schemi](../tutorials/relationship-api.md) per ulteriori informazioni.

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
| `@type` | Il tipo di descrittore da definire. Per un descrittore di relazione, questo valore deve essere impostato su `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | La `$id` URI dello schema in cui viene definito il descrittore. |
| `xdm:sourceVersion` | Versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso del campo nello schema di origine in cui viene definita la relazione. Deve iniziare con un &quot;/&quot; e non terminare con uno. Non includere &quot;proprietà&quot; nel percorso (ad esempio, &quot;/personalEmail/address&quot; invece di &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | La `$id` URI dello schema di destinazione con cui questo descrittore sta definendo una relazione. |
| `xdm:destinationVersion` | Versione principale dello schema di destinazione. |
| `xdm:destinationProperty` | Percorso facoltativo di un campo di destinazione nello schema di destinazione. Se questa proprietà viene omessa, il campo di destinazione viene dedotto da qualsiasi campo contenente un descrittore di identità di riferimento corrispondente (vedere di seguito). |

{style=&quot;table-layout:auto&quot;}

#### Descrittore di identità di riferimento

I descrittori di identità di riferimento forniscono un contesto di riferimento all’identità principale di un campo di schema, consentendo di farvi riferimento da campi di altri schemi. Lo schema di destinazione deve avere già un campo di identità principale definito prima che possa essere fatto riferimento da altri schemi tramite questo descrittore.

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
| `@type` | Il tipo di descrittore da definire. Per un descrittore di identità di riferimento, questo valore deve essere impostato su `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | La `$id` URI dello schema in cui viene definito il descrittore. |
| `xdm:sourceVersion` | Versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso del campo nello schema di origine che verrà utilizzato per fare riferimento allo schema di destinazione. Deve iniziare con un &quot;/&quot; e non terminare con uno. Non includere &quot;proprietà&quot; nel percorso (ad esempio, `/personalEmail/address` anziché `/properties/personalEmail/properties/address`). |
| `xdm:identityNamespace` | Codice dello spazio dei nomi identità per la proprietà sorgente. |

{style=&quot;table-layout:auto&quot;}

#### Descrittore di campo obsoleto

È possibile [deprecazione di un campo all’interno di una risorsa XDM personalizzata](../tutorials/field-deprecation.md#custom) aggiungendo un `meta:status` attributo impostato su `deprecated` al settore in questione. Tuttavia, se desideri deprecare i campi forniti dalle risorse XDM standard negli schemi, puoi assegnare un descrittore di campo obsoleto allo schema in questione per ottenere lo stesso effetto. Utilizzo della [corretto `Accept` header](../tutorials/field-deprecation.md#verify-deprecation), puoi quindi visualizzare quali campi standard sono obsoleti per uno schema quando lo cerchi nell’API.

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
| `@type` | Tipo di descrittore. Per un descrittore di deprecazione del campo, è necessario impostare questo valore su `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | URI `$id` dello schema a cui si applica il descrittore. |
| `xdm:sourceVersion` | Versione dello schema a cui si applica il descrittore. Deve essere impostato su `1`. |
| `xdm:sourceProperty` | Percorso della proprietà all&#39;interno dello schema a cui si applica il descrittore. Se si desidera applicare il descrittore a più proprietà, è possibile fornire un elenco di percorsi sotto forma di array (ad esempio, `["/firstName", "/lastName"]`). |

{style=&quot;table-layout:auto&quot;}
