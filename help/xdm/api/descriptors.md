---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;descriptor;Descriptor;descriptors;Descriptors;identity;Identity;friendly name;Friendly name;alternatedisplayinfo;reference;Reference;relationship;Relationship
solution: Experience Platform
title: Descrittori
description: L'endpoint /descriptors nell'API del Registro di sistema dello schema consente di gestire in modo programmatico i descrittori XDM all'interno dell'applicazione dell'esperienza.
topic: developer guide
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 1%

---


# Endpoint descrittori

Gli schemi definiscono una visualizzazione statica delle entità di dati, ma non forniscono dettagli specifici su come i dati basati su tali schemi (ad esempio, set di dati) possono essere correlati tra loro. Adobe Experience Platform consente di descrivere queste relazioni e altri metadati interpretativi relativi a uno schema utilizzando i descrittori.

I descrittori dello schema sono metadati a livello di tenant, il che significa che sono univoci per l&#39;organizzazione IMS e che tutte le operazioni del descrittore hanno luogo nel contenitore tenant.

A ogni schema può essere applicata una o più entità descrittori dello schema. Ogni entità descrittore dello schema include un descrittore `@type` e la `sourceSchema` a cui si applica. Una volta applicati, questi descrittori verranno applicati a tutti i set di dati creati utilizzando lo schema.

L&#39;endpoint `/descriptors` nell&#39;API [!DNL Schema Registry] consente di gestire i descrittori a livello di programmazione all&#39;interno dell&#39;applicazione dell&#39;esperienza.

## Introduzione

L&#39;endpoint utilizzato in questa guida fa parte dell&#39; [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml). Prima di continuare, consultare la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni richieste necessarie per eseguire correttamente chiamate a qualsiasi API  Experience Platform.

## Recupera un elenco di descrittori {#list}

Potete elencare tutti i descrittori definiti dall&#39;organizzazione effettuando una richiesta di GET a `/tenant/descriptors`.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

Il formato della risposta dipende dall&#39;intestazione `Accept` inviata nella richiesta. Tenere presente che l&#39;endpoint `/descriptors` utilizza intestazioni `Accept` diverse da tutti gli altri endpoint nell&#39;API [!DNL Schema Registry].

>[!IMPORTANT]
>
>I descrittori richiedono intestazioni `Accept` univoche che sostituiscono `xed` con `xdm` e offrono anche un&#39;opzione `link` univoca per i descrittori. Le intestazioni `Accept` corrette sono state incluse nelle chiamate di esempio riportate di seguito, ma prestate molta attenzione nell&#39;assicurare che vengano utilizzate le intestazioni corrette quando lavorate con i descrittori.

| `Accept` header | Descrizione |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Restituisce un array di ID descrittori |
| `application/vnd.adobe.xdm-link+json` | Restituisce un array di percorsi API del descrittore |
| `application/vnd.adobe.xdm+json` | Restituisce un array di oggetti descrittori espansi |
| `application/vnd.adobe.xdm-v2+json` | Questa intestazione `Accept` deve essere utilizzata per utilizzare le funzionalità di paging. |

**Risposta**

La risposta include un array per ciascun tipo di descrittore con descrittori definiti. In altre parole, se non sono presenti descrittori di un determinato `@type` definito, il Registro di sistema non restituirà una matrice vuota per quel tipo di descrittore.

Quando si utilizza l&#39;intestazione `link` `Accept`, ogni descrittore viene visualizzato come un elemento di array nel formato `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

Se desiderate visualizzare i dettagli di un descrittore specifico, potete cercare (GET) un singolo descrittore utilizzando il relativo `@id`.

**Formato API**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DESCRIPTOR_ID}` | Il `@id` del descrittore che si desidera cercare. |

**Richiesta**

La richiesta seguente recupera un descrittore per il valore `@id`. I descrittori non dispongono di una versione, pertanto nella richiesta di ricerca non è necessaria alcuna intestazione `Accept`.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli del descrittore, inclusi i dettagli `@type` e `sourceSchema`, nonché informazioni aggiuntive che variano a seconda del tipo di descrittore. La `@id` restituita deve corrispondere al descrittore `@id` fornito nella richiesta.

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
  "imsOrg": "{IMS_ORG}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Creare un descrittore {#create}

Potete creare un nuovo descrittore effettuando una richiesta di POST all&#39;endpoint `/tenant/descriptors`.

>[!IMPORTANT]
>
>[!DNL Schema Registry] consente di definire diversi tipi di descrittori. Ogni tipo di descrittore richiede l&#39;invio di campi specifici nel corpo della richiesta. Vedere l&#39; [appendice](#defining-descriptors) per un elenco completo dei descrittori e i campi necessari per definirli.

**Formato API**

```http
POST /tenant/descriptors
```

**Richiesta**

La richiesta seguente definisce un descrittore di identità in un campo &quot;indirizzo e-mail&quot; in uno schema di esempio. Questo indica a [!DNL Experience Platform] di utilizzare l&#39;indirizzo e-mail come identificatore per unire informazioni sull&#39;utente.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e i dettagli del descrittore appena creato, incluso `@id`. `@id` è un campo di sola lettura assegnato da [!DNL Schema Registry] e utilizzato per fare riferimento al descrittore nell&#39;API.

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

Potete aggiornare un descrittore inserendo il relativo `@id` nel percorso di una richiesta di PUT.

**Formato API**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DESCRIPTOR_ID}` | Il `@id` del descrittore da aggiornare. |

**Richiesta**

La richiesta riscrive essenzialmente il descrittore, pertanto il corpo della richiesta deve includere tutti i campi necessari per definire un descrittore di quel tipo. In altre parole, il payload di richiesta per aggiornare (PUT) un descrittore è lo stesso del payload per [creare (POST) un descrittore](#create) dello stesso tipo.

>[!IMPORTANT]
>
>Come per la creazione di descrittori tramite richieste di POST, ogni tipo di descrittore richiede l&#39;invio di campi specifici in payload di richieste di PUT. Vedere l&#39; [appendice](#defining-descriptors) per un elenco completo dei descrittori e i campi necessari per definirli.

L&#39;esempio seguente aggiorna un descrittore di identità per fare riferimento a un `xdm:sourceProperty` diverso (`mobile phone`) e modifica il `xdm:namespace` in `Phone`.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e la `@id` del descrittore aggiornato (che deve corrispondere alla `@id` inviata nella richiesta).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

Se si esegue una [richiesta di ricerca (GET)](#lookup) per visualizzare il descrittore, i campi vengono ora aggiornati per riflettere le modifiche inviate nella richiesta di PUT.

## Eliminare un descrittore {#delete}

Talvolta potrebbe essere necessario rimuovere un descrittore definito dall&#39; [!DNL Schema Registry]. Questa operazione viene eseguita eseguendo una richiesta di DELETE che fa riferimento alla `@id` del descrittore che si desidera rimuovere.

**Formato API**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DESCRIPTOR_ID}` | Il `@id` del descrittore da eliminare. |

**Richiesta**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto.

Per confermare che il descrittore è stato eliminato, è possibile eseguire una [richiesta di ricerca](#lookup) rispetto al descrittore `@id`. La risposta restituisce lo stato HTTP 404 (non trovato) perché il descrittore è stato rimosso dalla directory [!DNL Schema Registry].

## Appendice

La sezione seguente fornisce informazioni aggiuntive sull&#39;utilizzo dei descrittori nell&#39;API [!DNL Schema Registry].

### Definizione dei descrittori {#defining-descriptors}

Le sezioni seguenti forniscono una panoramica dei tipi di descrittori disponibili, compresi i campi richiesti per la definizione di un descrittore di ciascun tipo.

#### Descrittore identità

Un descrittore di identità segnala che &quot;[!UICONTROL sourceProperty]&quot; di &quot;[!UICONTROL sourceSchema]&quot; è un campo [!DNL Identity] come descritto da [Adobe Experience Platform Identity Service](../../identity-service/home.md).

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
| `@type` | Il tipo di descrittore da definire. |
| `xdm:sourceSchema` | URI `$id` dello schema in cui viene definito il descrittore. |
| `xdm:sourceVersion` | La versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso della proprietà specifica che sarà l&#39;identità. Il percorso deve iniziare con &quot;/&quot; e non terminare con uno. Non includere &quot;proprietà&quot; nel percorso (ad esempio, utilizzare &quot;/personalEmail/address&quot; invece di &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:namespace` | Il valore `id` o `code` dello spazio dei nomi dell&#39;identità. È possibile trovare un elenco di spazi dei nomi utilizzando il percorso [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml). |
| `xdm:property` | `xdm:id` o `xdm:code`, a seconda della `xdm:namespace` utilizzata. |
| `xdm:isPrimary` | Un valore booleano facoltativo. Se true, indica il campo come identità principale. Gli schemi possono contenere una sola identità primaria. |

#### descrittore di nome descrittivo

I descrittori di nomi descrittivi descrittivi consentono all&#39;utente di modificare i valori `title`, `description` e `meta:enum` dei campi dello schema della libreria di base. Particolarmente utile quando si utilizzano &quot;eVar&quot; e altri campi &quot;generici&quot; che si desidera etichettare come contenenti informazioni specifiche per la propria organizzazione. L’interfaccia utente può utilizzarli per visualizzare un nome più descrittivo o per mostrare solo i campi con un nome descrittivo.

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
  }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `@type` | Il tipo di descrittore da definire. |
| `xdm:sourceSchema` | URI `$id` dello schema in cui viene definito il descrittore. |
| `xdm:sourceVersion` | La versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso della proprietà specifica che sarà l&#39;identità. Il percorso deve iniziare con &quot;/&quot; e non terminare con uno. Non includere &quot;proprietà&quot; nel percorso (ad esempio, utilizzare &quot;/personalEmail/address&quot; invece di &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:title` | Il nuovo titolo che si desidera visualizzare per questo campo, scritto in Case titolo. |
| `xdm:description` | È possibile aggiungere una descrizione facoltativa insieme al titolo. |
| `meta:enum` | Se il campo indicato da `xdm:sourceProperty` è un campo stringa, `meta:enum` determina l&#39;elenco dei valori consigliati per il campo nell&#39;interfaccia di [!DNL Experience Platform]. È importante notare che `meta:enum` non dichiara un&#39;enumerazione né fornisce alcuna convalida di dati per il campo XDM.<br><br>Deve essere utilizzato solo per i campi XDM di base definiti dal Adobe . Se la proprietà source è un campo personalizzato definito dall&#39;organizzazione, è necessario modificare la proprietà `meta:enum` del campo direttamente tramite una richiesta di PATCH alla risorsa padre del campo. |

#### Descrittore della relazione

I descrittori delle relazioni descrivono una relazione tra due schemi diversi, basata sulle proprietà descritte in `sourceProperty` e `destinationProperty`. Per ulteriori informazioni, vedere l&#39;esercitazione su [definizione di una relazione tra due schemi](../tutorials/relationship-api.md).

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
| `@type` | Il tipo di descrittore da definire. |
| `xdm:sourceSchema` | URI `$id` dello schema in cui viene definito il descrittore. |
| `xdm:sourceVersion` | La versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso del campo nello schema di origine in cui viene definita la relazione. Deve iniziare con un &quot;/&quot; e non terminare con uno. Non includere &quot;proprietà&quot; nel percorso (ad esempio, &quot;/personalEmail/address&quot; invece di &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | URI `$id` dello schema di destinazione con cui il descrittore sta definendo una relazione. |
| `xdm:destinationVersion` | La versione principale dello schema di destinazione. |
| `xdm:destinationProperty` | Percorso facoltativo di un campo di destinazione nello schema di destinazione. Se questa proprietà viene omessa, il campo target viene ricavato da tutti i campi che contengono un descrittore di identità di riferimento corrispondente (vedere di seguito). |


#### Descrittore identità di riferimento

I descrittori di identità di riferimento forniscono un contesto di riferimento all&#39;identità primaria di un campo dello schema, consentendo di farvi riferimento dai campi di altri schemi. Per poter applicare un descrittore di riferimento, i campi devono essere già etichettati con un descrittore di identità.

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
| `@type` | Il tipo di descrittore da definire. |
| `xdm:sourceSchema` | URI `$id` dello schema in cui viene definito il descrittore. |
| `xdm:sourceVersion` | La versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso del campo nello schema di origine in cui viene definito il descrittore. Deve iniziare con un &quot;/&quot; e non terminare con uno. Non includere &quot;proprietà&quot; nel percorso (ad esempio, &quot;/personalEmail/address&quot; invece di &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:identityNamespace` | Il codice dello spazio dei nomi dell&#39;identità per la proprietà source. |