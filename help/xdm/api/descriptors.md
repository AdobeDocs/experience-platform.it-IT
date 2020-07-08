---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Descrittori
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 1%

---


# Descrittori

Gli schemi definiscono una visualizzazione statica delle entità di dati, ma non forniscono dettagli specifici su come i dati basati su tali schemi (ad esempio, set di dati) possono essere correlati tra loro.  Adobe Experience Platform consente di descrivere queste relazioni e altri metadati interpretativi di uno schema utilizzando i descrittori.

I descrittori dello schema sono metadati a livello di tenant, il che significa che sono univoci per l&#39;organizzazione IMS e che tutte le operazioni del descrittore hanno luogo nel contenitore tenant.

A ogni schema può essere applicata una o più entità descrittori dello schema. Ogni entità descrittore dello schema include un descrittore `@type` e l&#39; `sourceSchema` oggetto a cui si applica. Una volta applicati, questi descrittori verranno applicati a tutti i set di dati creati utilizzando lo schema.

Questo documento fornisce esempi di chiamate API per descrittori, oltre a un elenco completo di descrittori disponibili e i campi richiesti per la definizione di ciascun tipo.

>[!NOTE]
>
>I descrittori richiedono intestazioni Accetto univoche che sostituiscono `xed` con `xdm`, ma che sono molto simili a Accetta intestazioni utilizzate altrove nel Registro di sistema dello schema. Le intestazioni Accetta corrette sono state incluse nelle chiamate di esempio riportate di seguito, ma prestate particolare attenzione a garantire l’utilizzo delle intestazioni corrette.

## Descrittori elenco

Una singola richiesta GET può essere utilizzata per restituire un elenco di tutti i descrittori definiti dall&#39;organizzazione.

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

Il formato della risposta dipende dall’intestazione Accetta inviata nella richiesta. Tenere presente che l&#39; `/descriptors` endpoint utilizza intestazioni Accetta diverse da tutti gli altri endpoint nell&#39;API del Registro di sistema dello schema.

Il descrittore Accetta intestazioni sostituisce `xed` con `xdm`, e offre un&#39; `link` opzione univoca per i descrittori.

| Accetta | Descrizione |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Restituisce un array di ID descrittori |
| `application/vnd.adobe.xdm-link+json` | Restituisce un array di percorsi API del descrittore |
| `application/vnd.adobe.xdm+json` | Restituisce un array di oggetti descrittori espansi |

**Risposta**

La risposta include un array per ciascun tipo di descrittore con descrittori definiti. In altre parole, se non esistono descrittori di un certo tipo `@type` definito, il Registro di sistema non restituirà una matrice vuota per quel tipo di descrittore.

Quando si utilizza l&#39;intestazione `link` Accetto, ogni descrittore viene visualizzato come un elemento di array nel formato `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

## Cercare un descrittore

Se desiderate visualizzare i dettagli di un descrittore specifico, potete cercare (GET) un singolo descrittore utilizzando il relativo `@id`.

**Formato API**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DESCRIPTOR_ID}` | Specifica `@id` del descrittore da cercare. |

**Richiesta**

I descrittori non dispongono di una versione, pertanto nella richiesta di ricerca non è richiesta alcuna intestazione Accetto.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli del descrittore, inclusi i relativi `@type` e `sourceSchema`, nonché informazioni aggiuntive che variano a seconda del tipo di descrittore. Il valore restituito `@id` deve corrispondere al descrittore `@id` fornito nella richiesta.

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

## Creare un descrittore

Il Registro di sistema dello schema consente di definire diversi tipi di descrittori. Ogni tipo di descrittore richiede l&#39;invio di campi specifici nella richiesta POST. Un elenco completo dei descrittori e i campi necessari per definirli è disponibile nella sezione appendice sulla [definizione dei descrittori](#defining-descriptors).

**Formato API**

```http
POST /tenant/descriptors
```

**Richiesta**

La richiesta seguente definisce un descrittore di identità in un campo &quot;indirizzo e-mail&quot; in uno schema di esempio. Questo indica  Experience Platform di utilizzare l&#39;indirizzo e-mail come identificatore per unire insieme le informazioni sull&#39;utente.

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

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e i dettagli del descrittore appena creato, incluso `@id`il relativo. Il campo `@id` è di sola lettura assegnato dal Registro di sistema dello schema e utilizzato per fare riferimento al descrittore nell&#39;API.

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

## Descrittore di aggiornamento

Potete aggiornare un descrittore effettuando una richiesta PUT che fa riferimento alla `@id` descrizione del descrittore che desiderate aggiornare nel percorso della richiesta.

**Formato API**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DESCRIPTOR_ID}` | Indica `@id` il nome del descrittore da aggiornare. |

**Richiesta**

Questa richiesta _riscrive_ in sostanza il descrittore, pertanto il corpo della richiesta deve includere tutti i campi necessari per definire un descrittore di quel tipo. In altre parole, il payload di richiesta per aggiornare (PUT) un descrittore è lo stesso del payload per creare (POST) un descrittore dello stesso tipo.

In questo esempio, il descrittore di identità viene aggiornato per fare riferimento a un altro `xdm:sourceProperty` (&quot;telefono cellulare&quot;) e cambiare il `xdm:namespace` nome in &quot;telefono&quot;.

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

I dettagli relativi alle proprietà `xdm:namespace` e `xdm:property`, comprese le modalità di accesso, sono disponibili nella sezione dell&#39;appendice relativa alla [definizione dei descrittori](#defining-descriptors).

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e il `@id` valore del descrittore aggiornato (che deve corrispondere a quello `@id` inviato nella richiesta).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

Se si esegue una richiesta di ricerca (GET) per visualizzare il descrittore, i campi ora vengono aggiornati per riflettere le modifiche inviate nella richiesta PUT.

## Elimina descrittore

Talvolta potrebbe essere necessario rimuovere un descrittore definito dal Registro di sistema dello schema. Questa operazione viene eseguita effettuando una richiesta di DELETE che fa riferimento al descrittore `@id` da rimuovere.

**Formato API**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DESCRIPTOR_ID}` | Indica `@id` il nome del descrittore da eliminare. |

**Richiesta**

Accetta intestazioni non è necessaria quando si eliminano descrittori.

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

Per confermare che il descrittore è stato eliminato, potete eseguire una richiesta di ricerca rispetto al descrittore `@id`. La risposta restituisce lo stato HTTP 404 (non trovato) perché il descrittore è stato rimosso dal Registro di sistema dello schema.

## Appendice

La sezione seguente fornisce informazioni aggiuntive sull&#39;utilizzo dei descrittori nell&#39;API del Registro di sistema dello schema.

### Definizione dei descrittori

Le sezioni seguenti forniscono una panoramica dei tipi di descrittori disponibili, compresi i campi richiesti per la definizione di un descrittore di ciascun tipo.

#### Descrittore identità

Un descrittore di identità segnala che &quot;sourceProperty&quot; di &quot;sourceSchema&quot; è un campo Identity come descritto da [Adobe Experience Platform Identity Service](../../identity-service/home.md).

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
| `xdm:namespace` | Il valore `id` o `code` dello spazio dei nomi identità. È possibile trovare un elenco di spazi dei nomi utilizzando l&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)Servizio identità. |
| `xdm:property` | O `xdm:id` o `xdm:code`, a seconda dell&#39; `xdm:namespace` utilizzo. |
| `xdm:isPrimary` | Un valore booleano facoltativo. Se true, indica il campo come identità principale. Gli schemi possono contenere una sola identità primaria. |

#### descrittore di nome descrittivo

I descrittori di nomi descrittivi descrittivi consentono all&#39;utente di modificare i `title`, `description`e `meta:enum` i valori dei campi dello schema della libreria di base. Particolarmente utile quando si utilizzano &quot;eVar&quot; e altri campi &quot;generici&quot; che si desidera etichettare come contenenti informazioni specifiche per la propria organizzazione. L’interfaccia utente può utilizzarli per visualizzare un nome più descrittivo o per mostrare solo i campi con un nome descrittivo.

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
| `meta:enum` | Se il campo indicato da `xdm:sourceProperty` è un campo stringa, `meta:enum` determina l&#39;elenco dei valori consigliati per il campo nell&#39;interfaccia utente di Experience Platform . È importante notare che non `meta:enum` dichiara un&#39;enumerazione né fornisce alcuna convalida di dati per il campo XDM.<br><br>Deve essere utilizzato solo per i campi XDM di base definiti da Adobe. Se la proprietà source è un campo personalizzato definito dall&#39;organizzazione, è necessario modificare la `meta:enum` proprietà del campo direttamente tramite una richiesta [](./update-resource.md)PATCH. |

#### Descrittore della relazione

I descrittori delle relazioni descrivono una relazione tra due schemi diversi, basata sulle proprietà descritte in `sourceProperty` e `destinationProperty`. Per ulteriori informazioni, vedere l&#39;esercitazione sulla [definizione di una relazione tra due schemi](../tutorials/relationship-api.md) .

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

I descrittori di identità di riferimento forniscono un contesto di riferimento a un campo dello schema, consentendo il collegamento con il campo dell&#39;identità principale di uno schema di destinazione. I campi devono essere già etichettati con un descrittore di identità prima di potervi applicare un descrittore di riferimento.

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