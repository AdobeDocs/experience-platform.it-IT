---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;modello dati;registro schema;registro schema;descrittore;descrittori;descrittori;identità;nome descrittivo;nome descrittivo;nome descrittivo;nome descrittivo;alternatedisplayinfo;riferimento;riferimento;relazione;relazione
solution: Experience Platform
title: Endpoint API per descrittori
description: L’endpoint /descriptors nell’API del Registro di sistema dello schema ti consente di gestire programmaticamente i descrittori XDM all’interno dell’applicazione di esperienza.
topic-legacy: developer guide
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1611'
ht-degree: 1%

---

# Endpoint descrittori

Gli schemi definiscono una visualizzazione statica delle entità dati, ma non forniscono dettagli specifici sul modo in cui i dati basati su questi schemi (ad esempio, i set di dati) possono essere correlati tra loro. Adobe Experience Platform ti consente di descrivere queste relazioni e altri metadati interpretativi su uno schema utilizzando i descrittori.

I descrittori di schema sono metadati a livello di tenant, il che significa che sono univoci per la tua organizzazione IMS e che tutte le operazioni dei descrittori hanno luogo nel contenitore tenant.

A ogni schema può essere applicata una o più entità descrittrici di schema. Ogni entità descrittrice dello schema include un descrittore `@type` e la `sourceSchema` a cui si applica. Una volta applicati, questi descrittori verranno applicati a tutti i set di dati creati utilizzando lo schema.

L’endpoint `/descriptors` nell’ API [!DNL Schema Registry] consente di gestire i descrittori a livello di programmazione all’interno dell’applicazione di esperienza.

## Introduzione

L&#39;endpoint utilizzato in questa guida fa parte dell&#39; [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml). Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla relativa documentazione, una guida per la lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare chiamate a qualsiasi API di Experience Platform.

## Recupera un elenco di descrittori {#list}

Puoi elencare tutti i descrittori che sono stati definiti dalla tua organizzazione effettuando una richiesta di GET a `/tenant/descriptors`.

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

Il formato della risposta dipende dall’intestazione `Accept` inviata nella richiesta. L’endpoint `/descriptors` utilizza intestazioni `Accept` diverse da tutti gli altri endpoint nell’API [!DNL Schema Registry].

>[!IMPORTANT]
>
>I descrittori richiedono intestazioni `Accept` univoche che sostituiscono `xed` con `xdm` e offrono anche un&#39;opzione `link` univoca per i descrittori. Le intestazioni `Accept` corrette sono state incluse nelle chiamate di esempio riportate di seguito, ma presta molta attenzione a garantire che le intestazioni corrette vengano utilizzate quando si lavora con i descrittori.

| `Accept` header | Descrizione |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Restituisce una matrice di ID descrittori |
| `application/vnd.adobe.xdm-link+json` | Restituisce una matrice di percorsi API descrittivi |
| `application/vnd.adobe.xdm+json` | Restituisce una matrice di oggetti descrittivi espansi |
| `application/vnd.adobe.xdm-v2+json` | Questa intestazione `Accept` deve essere utilizzata per utilizzare le funzionalità di paging. |

**Risposta**

La risposta include una matrice per ogni tipo di descrittore con descrittori definiti. In altre parole, se non sono presenti descrittori di un determinato `@type` definito, il Registro di sistema non restituirà una matrice vuota per quel tipo di descrittore.

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
| `{DESCRIPTOR_ID}` | Il `@id` del descrittore da cercare. |

**Richiesta**

La richiesta seguente recupera un descrittore dal relativo valore `@id`. Le versioni dei descrittori non sono disponibili, pertanto nella richiesta di ricerca non è necessaria alcuna intestazione `Accept`.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli del descrittore, inclusi i relativi `@type` e `sourceSchema`, nonché informazioni aggiuntive che variano a seconda del tipo di descrittore. Il `@id` restituito deve corrispondere al descrittore `@id` fornito nella richiesta.

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

È possibile creare un nuovo descrittore effettuando una richiesta POST all&#39;endpoint `/tenant/descriptors`.

>[!IMPORTANT]
>
>Il [!DNL Schema Registry] ti consente di definire diversi tipi di descrittori. Ogni tipo di descrittore richiede che i propri campi specifici siano inviati nel corpo della richiesta. Per un elenco completo dei descrittori e dei campi necessari per definirli, consultare l&#39; [appendice](#defining-descriptors) .

**Formato API**

```http
POST /tenant/descriptors
```

**Richiesta**

La richiesta seguente definisce un descrittore di identità su un campo &quot;Indirizzo e-mail&quot; in uno schema di esempio. Questo indica a [!DNL Experience Platform] di utilizzare l’indirizzo e-mail come identificatore per unire le informazioni sull’utente.

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

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e i dettagli del nuovo descrittore creato, incluso `@id`. Il `@id` è un campo di sola lettura assegnato da [!DNL Schema Registry] e utilizzato per fare riferimento al descrittore nell&#39;API.

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
| `{DESCRIPTOR_ID}` | Il `@id` del descrittore da aggiornare. |

**Richiesta**

Questa richiesta essenzialmente riscrive il descrittore, pertanto il corpo della richiesta deve includere tutti i campi necessari per definire un descrittore di quel tipo. In altre parole, il payload della richiesta per aggiornare (PUT) un descrittore è lo stesso del payload per [creare (POST) un descrittore](#create) dello stesso tipo.

>[!IMPORTANT]
>
>Come per la creazione di descrittori utilizzando le richieste di POST, ogni tipo di descrittore richiede l’invio di campi specifici nei payload di richiesta PUT. Per un elenco completo dei descrittori e dei campi necessari per definirli, consultare l&#39; [appendice](#defining-descriptors) .

L&#39;esempio seguente aggiorna un descrittore di identità per fare riferimento a un `xdm:sourceProperty` diverso (`mobile phone`) e modifica `xdm:namespace` in `Phone`.

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

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e il `@id` del descrittore aggiornato (che deve corrispondere al `@id` inviato nella richiesta).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

Quando si esegue una richiesta [ricerca (GET)](#lookup) per visualizzare il descrittore, i campi vengono ora aggiornati per riflettere le modifiche inviate nella richiesta PUT.

## Eliminare un descrittore {#delete}

A volte può essere necessario rimuovere un descrittore definito dalla sezione [!DNL Schema Registry]. A questo scopo, invia una richiesta DELETE che fa riferimento al `@id` del descrittore che desideri rimuovere.

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

Per confermare che il descrittore è stato eliminato, è possibile eseguire una [richiesta di ricerca](#lookup) rispetto al descrittore `@id`. La risposta restituisce lo stato HTTP 404 (Non trovato) perché il descrittore è stato rimosso dal [!DNL Schema Registry].

## Appendice

La sezione seguente fornisce informazioni aggiuntive sulle operazioni con i descrittori nell’ API [!DNL Schema Registry] .

### Definizione dei descrittori {#defining-descriptors}

Le sezioni seguenti forniscono una panoramica dei tipi di descrittori disponibili, compresi i campi obbligatori per la definizione di un descrittore di ciascun tipo.

#### Descrittore di identità

Un descrittore di identità segnala che &quot;[!UICONTROL sourceProperty]&quot; del campo &quot;[!UICONTROL sourceSchema]&quot; è un campo [!DNL Identity] come descritto da [Servizio Adobe Experience Platform Identity](../../identity-service/home.md).

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
| `xdm:sourceVersion` | Versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso della proprietà specifica che sarà l&#39;identità. Il percorso deve iniziare con un &quot;/&quot; e non terminare con uno. Non includere &quot;proprietà&quot; nel percorso (ad esempio, usa &quot;/personalEmail/address&quot; invece di &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:namespace` | Il valore `id` o `code` dello spazio dei nomi di identità. È possibile trovare un elenco di namespace utilizzando [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml). |
| `xdm:property` | A seconda del `xdm:namespace` utilizzato, è possibile utilizzare `xdm:id` o `xdm:code`. |
| `xdm:isPrimary` | Un valore booleano facoltativo. Se true, indica il campo come identità principale. Gli schemi possono contenere una sola identità principale. |

#### descrittore di nome descrittivo

I descrittori di nomi descrittivi consentono a un utente di modificare i valori `title`, `description` e `meta:enum` dei campi dello schema della libreria principale. Particolarmente utile quando si lavora con &quot;eVar&quot; e altri campi &quot;generici&quot; che si desidera etichettare come contenenti informazioni specifiche della propria organizzazione. L’interfaccia utente può usarli per mostrare un nome più descrittivo o per mostrare solo i campi con un nome descrittivo.

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
| `xdm:sourceVersion` | Versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso della proprietà specifica che sarà l&#39;identità. Il percorso deve iniziare con un &quot;/&quot; e non terminare con uno. Non includere &quot;proprietà&quot; nel percorso (ad esempio, usa &quot;/personalEmail/address&quot; invece di &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:title` | Nuovo titolo da visualizzare per questo campo, scritto in Case titolo. |
| `xdm:description` | È possibile aggiungere una descrizione facoltativa insieme al titolo. |
| `meta:enum` | Se il campo indicato da `xdm:sourceProperty` è un campo stringa, `meta:enum` determina l’elenco dei valori suggeriti per il campo nell’ [!DNL Experience Platform] interfaccia utente. È importante notare che `meta:enum` non dichiara un&#39;enumerazione né fornisce alcuna convalida di dati per il campo XDM.<br><br>Deve essere utilizzato solo per i campi XDM di base definiti da Adobe. Se la proprietà sorgente è un campo personalizzato definito dall’organizzazione, è invece necessario modificare la proprietà `meta:enum` del campo direttamente tramite una richiesta di PATCH alla risorsa principale del campo. |

#### Descrittore di relazione

I descrittori di relazione descrivono una relazione tra due schemi diversi, basati sulle proprietà descritte in `sourceProperty` e `destinationProperty`. Per ulteriori informazioni, consulta l’esercitazione su [definizione di una relazione tra due schemi](../tutorials/relationship-api.md) .

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
| `xdm:sourceVersion` | Versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso del campo nello schema di origine in cui viene definita la relazione. Deve iniziare con un &quot;/&quot; e non terminare con uno. Non includere &quot;proprietà&quot; nel percorso (ad esempio, &quot;/personalEmail/address&quot; invece di &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | URI `$id` dello schema di destinazione con cui questo descrittore sta definendo una relazione. |
| `xdm:destinationVersion` | Versione principale dello schema di destinazione. |
| `xdm:destinationProperty` | Percorso facoltativo di un campo di destinazione nello schema di destinazione. Se questa proprietà viene omessa, il campo di destinazione viene dedotto da qualsiasi campo contenente un descrittore di identità di riferimento corrispondente (vedere di seguito). |


#### Descrittore di identità di riferimento

I descrittori di identità di riferimento forniscono un contesto di riferimento all’identità principale di un campo di schema, consentendo di farvi riferimento da campi di altri schemi. I campi devono essere già etichettati con un descrittore di identità prima di poter essere applicati a un descrittore di riferimento.

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
| `xdm:sourceVersion` | Versione principale dello schema di origine. |
| `xdm:sourceProperty` | Percorso del campo nello schema di origine in cui viene definito il descrittore. Deve iniziare con un &quot;/&quot; e non terminare con uno. Non includere &quot;proprietà&quot; nel percorso (ad esempio, &quot;/personalEmail/address&quot; invece di &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:identityNamespace` | Codice dello spazio dei nomi identità per la proprietà sorgente. |
