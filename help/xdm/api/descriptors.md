---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;Experience data model;Experience data model;Experience Data Model;modello dati;modello dati;modello dati;modello dati;registro schema;registro schema;descrittore;descrittore;descrittori;descrittori;identità;nome descrittivo;nome descrittivo;alternatedisplayinfo;riferimento;riferimento;relazione;relazione
solution: Experience Platform
title: Endpoint API per i descrittori
description: L’endpoint /descriptors nell’API Schema Registry consente di gestire in modo programmatico i descrittori XDM all’interno dell’applicazione Experience.
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 866e00459c66ea4678cd98d119a7451fd8e78253
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 2%

---

# Endpoint &quot;descriptors&quot;

Gli schemi definiscono una visualizzazione statica delle entità dati, ma non forniscono dettagli specifici sul modo in cui i dati basati su tali schemi (ad esempio, i set di dati) possono relazionarsi tra loro. Adobe Experience Platform consente di descrivere queste relazioni e altri metadati interpretativi su uno schema utilizzando i descrittori.

I descrittori degli schemi sono metadati a livello di tenant, ovvero sono univoci per l’organizzazione e tutte le operazioni dei descrittori hanno luogo nel contenitore tenant.

A ogni schema possono essere applicate una o più entità descrittive dello schema. Ogni entità descrittore dello schema include un descrittore `@type` e il `sourceSchema` a cui si applica. Una volta applicati, questi descrittori verranno applicati a tutti i set di dati creati utilizzando lo schema.

L&#39;endpoint `/descriptors` nell&#39;API [!DNL Schema Registry] consente di gestire in modo programmatico i descrittori all&#39;interno dell&#39;applicazione Experience.

## Introduzione

L&#39;endpoint utilizzato in questa guida fa parte dell&#39;[[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e per le informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recuperare un elenco di descrittori {#list}

È possibile elencare tutti i descrittori definiti dall&#39;organizzazione effettuando una richiesta GET a `/tenant/descriptors`.

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

Il formato della risposta dipende dall&#39;intestazione `Accept` inviata nella richiesta. L&#39;endpoint `/descriptors` utilizza intestazioni `Accept` diverse da tutti gli altri endpoint nell&#39;API [!DNL Schema Registry].

>[!IMPORTANT]
>
>I descrittori richiedono intestazioni `Accept` univoche che sostituiscono `xed` con `xdm` e offrono anche un&#39;opzione `link` univoca per i descrittori. Le intestazioni `Accept` corrette sono state incluse nelle chiamate di esempio seguenti, ma è necessario prestare particolare attenzione per assicurarsi che vengano utilizzate le intestazioni corrette quando si lavora con i descrittori.

| Intestazione `Accept` | Descrizione |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Restituisce una matrice di ID descrittori |
| `application/vnd.adobe.xdm-link+json` | Restituisce una matrice di percorsi API descrittori |
| `application/vnd.adobe.xdm+json` | Restituisce una matrice di oggetti descrittori espansi |
| `application/vnd.adobe.xdm-v2+json` | Questa intestazione `Accept` deve essere utilizzata per utilizzare le funzionalità di paging. |

{style="table-layout:auto"}

**Risposta**

La risposta include un array per ogni tipo di descrittore che ha definito i descrittori. In altre parole, se non sono presenti descrittori di un determinato `@type` definito, il Registro di sistema non restituirà una matrice vuota per quel tipo di descrittore.

Quando si utilizza l&#39;intestazione `link` `Accept`, ogni descrittore viene visualizzato come un elemento array nel formato `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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
| `{DESCRIPTOR_ID}` | `@id` del descrittore che si desidera cercare. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente recupera un descrittore dal suo valore `@id`. I descrittori non dispongono di versioni, pertanto non è richiesta alcuna intestazione `Accept` nella richiesta di ricerca.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del descrittore, inclusi `@type` e `sourceSchema`, nonché ulteriori informazioni che variano a seconda del tipo di descrittore. Il valore restituito `@id` deve corrispondere al descrittore `@id` fornito nella richiesta.

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

È possibile creare un nuovo descrittore effettuando una richiesta POST all&#39;endpoint `/tenant/descriptors`.

>[!IMPORTANT]
>
>[!DNL Schema Registry] consente di definire diversi tipi di descrittori. Ogni tipo di descrittore richiede l’invio di campi specifici nel corpo della richiesta. Per un elenco completo dei descrittori e dei campi necessari per definirli, consulta la [appendice](#defining-descriptors).

**Formato API**

```http
POST /tenant/descriptors
```

**Richiesta**

La seguente richiesta definisce un descrittore di identità in un campo &quot;indirizzo e-mail&quot; in uno schema di esempio. Questo comunica a [!DNL Experience Platform] di utilizzare l&#39;indirizzo e-mail come identificatore per unire le informazioni sulla persona.

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

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 (Creato) e i dettagli del descrittore appena creato, incluso `@id`. `@id` è un campo di sola lettura assegnato da [!DNL Schema Registry] e utilizzato per fare riferimento al descrittore nell&#39;API.

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
| `{DESCRIPTOR_ID}` | `@id` del descrittore che si desidera aggiornare. |

{style="table-layout:auto"}

**Richiesta**

Questa richiesta riscrive essenzialmente il descrittore, pertanto il corpo della richiesta deve includere tutti i campi necessari per definire un descrittore di quel tipo. In altre parole, il payload della richiesta per aggiornare (PUT) un descrittore è lo stesso del payload per [creare (POST) un descrittore](#create) dello stesso tipo.

>[!IMPORTANT]
>
>Come per la creazione di descrittori tramite richieste POST, ogni tipo di descrittore richiede l’invio di campi specifici nei payload di richieste PUT. Per un elenco completo dei descrittori e dei campi necessari per definirli, consulta la [appendice](#defining-descriptors).

Nell&#39;esempio seguente viene aggiornato un descrittore di identità in modo che faccia riferimento a un altro `xdm:sourceProperty` (`mobile phone`) e viene modificato `xdm:namespace` in `Phone`.

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

L&#39;esecuzione di una [richiesta di ricerca (GET)](#lookup) per visualizzare il descrittore indica che i campi sono stati aggiornati per riflettere le modifiche inviate nella richiesta PUT.

## Eliminare un descrittore {#delete}

Talvolta potrebbe essere necessario rimuovere un descrittore definito da [!DNL Schema Registry]. A tale scopo, effettuare una richiesta DELETE facendo riferimento a `@id` del descrittore che si desidera rimuovere.

**Formato API**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DESCRIPTOR_ID}` | `@id` del descrittore che si desidera eliminare. |

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

Per confermare che il descrittore è stato eliminato, è possibile eseguire una [richiesta di ricerca](#lookup) rispetto al descrittore `@id`. La risposta restituisce lo stato HTTP 404 (non trovato) perché il descrittore è stato rimosso da [!DNL Schema Registry].

## Appendice

La sezione seguente fornisce informazioni aggiuntive sull&#39;utilizzo dei descrittori nell&#39;API [!DNL Schema Registry].

### Definizione dei descrittori {#defining-descriptors}

>[!NOTE]
>
>Il numero massimo di descrittori applicabili alla sandbox di un’organizzazione è 4000.

Le sezioni seguenti forniscono una panoramica dei tipi di descrittori disponibili, inclusi i campi obbligatori per la definizione di un descrittore per ciascun tipo.

>[!IMPORTANT]
>
>Non è possibile assegnare un’etichetta all’oggetto spazio dei nomi tenant, poiché il sistema applicherebbe tale etichetta a ogni campo personalizzato nella sandbox. È invece necessario specificare il nodo foglia sotto l’oggetto da etichettare.

#### Descrittore di identità

Un descrittore di identità segnala che &quot;[!UICONTROL sourceProperty]&quot; di &quot;[!UICONTROL sourceSchema]&quot; è un campo [!DNL Identity] come descritto da [Servizio Adobe Experience Platform Identity](../../identity-service/home.md).

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
| `xdm:sourceSchema` | URI `$id` dello schema in cui viene definito il descrittore. |
| `xdm:sourceVersion` | Versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso della proprietà specifica che sarà l’identità. Il percorso deve iniziare con &quot;/&quot; e non terminare con uno. Non includere &quot;properties&quot; nel percorso (ad esempio, utilizza &quot;/personalEmail/address&quot; invece di &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:namespace` | Il valore `id` o `code` dello spazio dei nomi dell&#39;identità. È possibile trovare un elenco di spazi dei nomi utilizzando [[!DNL Identity Service API]](https://developer.adobe.com/experience-platform-apis/references/identity-service). |
| `xdm:property` | `xdm:id` o `xdm:code`, a seconda di `xdm:namespace` utilizzati. |
| `xdm:isPrimary` | Valore booleano facoltativo. Se è true, indica il campo come identità primaria. Gli schemi possono contenere una sola identità primaria. |

{style="table-layout:auto"}

#### Descrittore del nome intuitivo {#friendly-name}

I descrittori di nomi descrittivi consentono a un utente di modificare i valori `title`, `description` e `meta:enum` dei campi dello schema della libreria principale. Particolarmente utile quando si lavora con &quot;eVar&quot; e altri campi &quot;generici&quot; che si desidera etichettare come contenenti informazioni specifiche dell’organizzazione. L’interfaccia utente può utilizzarli per mostrare un nome più descrittivo o per mostrare solo i campi con un nome descrittivo.

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
| `xdm:sourceSchema` | URI `$id` dello schema in cui viene definito il descrittore. |
| `xdm:sourceVersion` | Versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso della proprietà specifica di cui si desidera modificare i dettagli. Il percorso deve iniziare con una barra (`/`) e non terminare con una. Non includere `properties` nel percorso (ad esempio, utilizzare `/personalEmail/address` invece di `/properties/personalEmail/properties/address`). |
| `xdm:title` | Il nuovo titolo che si desidera visualizzare per questo campo, scritto in Maiuscole/minuscole. |
| `xdm:description` | È possibile aggiungere una descrizione facoltativa insieme al titolo. |
| `meta:enum` | Se il campo indicato da `xdm:sourceProperty` è un campo stringa, `meta:enum` può essere utilizzato per aggiungere valori suggeriti per il campo nell&#39;interfaccia utente Segmentazione. È importante notare che `meta:enum` non dichiara un&#39;enumerazione o non fornisce alcuna convalida dei dati per il campo XDM.<br><br>Da utilizzare solo per i campi XDM di base definiti dall&#39;Adobe. Se la proprietà di origine è un campo personalizzato definito dall&#39;organizzazione, è invece necessario modificare la proprietà `meta:enum` del campo direttamente tramite una richiesta PATCH alla risorsa padre del campo. |
| `meta:excludeMetaEnum` | Se il campo indicato da `xdm:sourceProperty` è un campo stringa con valori suggeriti esistenti forniti in un campo `meta:enum`, è possibile includere questo oggetto in un descrittore di nome descrittivo per escludere alcuni o tutti questi valori dalla segmentazione. La chiave e il valore di ogni voce devono corrispondere a quelli inclusi nel `meta:enum` originale del campo per escludere la voce. |

{style="table-layout:auto"}

#### Descrittore di relazione

I descrittori di relazione descrivono una relazione tra due schemi diversi, basata sulle proprietà descritte in `sourceProperty` e `destinationProperty`. Per ulteriori informazioni, vedere il tutorial su [definizione di una relazione tra due schemi](../tutorials/relationship-api.md).

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
| `xdm:sourceSchema` | URI `$id` dello schema in cui viene definito il descrittore. |
| `xdm:sourceVersion` | Versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso del campo nello schema di origine in cui viene definita la relazione. Deve iniziare con &quot;/&quot; e non finire con uno. Non includere &quot;properties&quot; nel percorso (ad esempio, &quot;/personalEmail/address&quot; invece di &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | URI `$id` dello schema di riferimento con cui questo descrittore definisce una relazione. |
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
| `xdm:sourceSchema` | URI `$id` dello schema in cui viene definito il descrittore. |
| `xdm:sourceVersion` | Versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso del campo nello schema di origine che verrà utilizzato per fare riferimento allo schema di riferimento. Deve iniziare con &quot;/&quot; e non finire con uno. Non includere &quot;properties&quot; nel percorso (ad esempio, `/personalEmail/address` invece di `/properties/personalEmail/properties/address`). |
| `xdm:identityNamespace` | Il codice dello spazio dei nomi dell’identità per la proprietà sorgente. |

{style="table-layout:auto"}

#### Descrittore di campo obsoleto

È possibile [rendere obsoleto un campo all&#39;interno di una risorsa XDM personalizzata](../tutorials/field-deprecation-api.md#custom) aggiungendo un attributo `meta:status` impostato su `deprecated` al campo in questione. Tuttavia, se desideri rendere obsoleti i campi forniti dalle risorse XDM standard negli schemi, puoi assegnare allo schema in questione un descrittore di campo obsoleto per ottenere lo stesso effetto. Utilizzando l&#39;intestazione `Accept` [corretta](../tutorials/field-deprecation-api.md#verify-deprecation), puoi visualizzare quali campi standard sono obsoleti per uno schema quando lo cerchi nell&#39;API.

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
| `xdm:sourceProperty` | Percorso della proprietà all’interno dello schema a cui si sta applicando il descrittore. Se si desidera applicare il descrittore a più proprietà, è possibile fornire un elenco di percorsi sotto forma di array (ad esempio, `["/firstName", "/lastName"]`). |

{style="table-layout:auto"}
