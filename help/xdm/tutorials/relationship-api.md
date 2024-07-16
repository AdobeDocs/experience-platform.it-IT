---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;Experience data model;Experience data model;Experience Data Model;data model;modello dati;modello dati;modello dati;registro schema;registro schema;schema;schema;schemi;schemi;relazione;relazione;descrittore relazione;descrittore relazione;descrittore relazione;identità riferimento;identità riferimento;
title: Definire una relazione tra due schemi utilizzando l’API Schema Registry
description: Questo documento fornisce un tutorial per definire una relazione uno-a-uno tra due schemi definiti dalla tua organizzazione utilizzando l’API Schema Registry.
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 2%

---

# Definire una relazione tra due schemi utilizzando l&#39;API [!DNL Schema Registry]

La capacità di comprendere le relazioni tra i clienti e le loro interazioni con il brand attraverso vari canali è una parte importante di Adobe Experience Platform. La definizione di queste relazioni all&#39;interno della struttura degli schemi [!DNL Experience Data Model] (XDM) consente di ottenere informazioni complesse sui dati dei clienti.

Sebbene sia possibile dedurre le relazioni tra schemi tramite lo schema di unione e [!DNL Real-Time Customer Profile], questo vale solo per gli schemi che condividono la stessa classe. Per stabilire una relazione tra due schemi appartenenti a classi diverse, è necessario aggiungere un campo relazione dedicato a uno schema **sorgente**, che indica l&#39;identità di uno **schema di riferimento** separato.

>[!NOTE]
>
>L’API Schema Registry si riferisce agli schemi di riferimento come &quot;schemi di destinazione&quot;. Non vanno confusi con gli schemi di destinazione in [Set di mappatura della preparazione dati](../../data-prep/mapping-set.md) o schemi per [connessioni di destinazione](../../destinations/home.md).

Questo documento fornisce un tutorial per definire una relazione uno-a-uno tra due schemi definiti dall&#39;organizzazione utilizzando [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Introduzione

Questo tutorial richiede una buona conoscenza di [!DNL Experience Data Model] (XDM) e [!DNL XDM System]. Prima di iniziare questo tutorial, consulta la seguente documentazione:

* [Sistema XDM nell&#39;Experience Platform](../home.md): panoramica di XDM e della relativa implementazione in [!DNL Experience Platform].
   * [Nozioni di base sulla composizione dello schema](../schema/composition.md): introduzione dei blocchi predefiniti degli schemi XDM.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Prima di iniziare questo tutorial, consulta la [guida per gli sviluppatori](../api/getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all&#39;API [!DNL Schema Registry]. Ciò include `{TENANT_ID}`, il concetto di &quot;contenitori&quot; e le intestazioni necessarie per effettuare le richieste (con particolare attenzione all&#39;intestazione [!DNL Accept] e ai suoi possibili valori).

## Definire uno schema di origine e di riferimento {#define-schemas}

È previsto che tu abbia già creato i due schemi che verranno definiti nella relazione. Questa esercitazione crea una relazione tra i membri del programma fedeltà corrente di un&#39;organizzazione (definito in uno schema &quot;[!DNL Loyalty Members]&quot;) e i relativi hotel preferiti (definiti in uno schema &quot;[!DNL Hotels]&quot;).

Le relazioni tra schemi sono rappresentate da uno **schema di origine** con un campo che fa riferimento a un altro campo in uno **schema di riferimento**. Nei passaggi seguenti, &quot;[!DNL Loyalty Members]&quot; sarà lo schema di origine, mentre &quot;[!DNL Hotels]&quot; fungerà da schema di riferimento.

>[!IMPORTANT]
>
>Per stabilire una relazione, entrambi gli schemi devono avere identità primarie definite ed essere abilitati per [!DNL Real-Time Customer Profile]. Per istruzioni su come configurare di conseguenza gli schemi, consulta la sezione su [abilitazione di uno schema da utilizzare nel profilo](./create-schema-api.md#profile) nell&#39;esercitazione per la creazione dello schema.

Per definire una relazione tra due schemi, è necessario innanzitutto acquisire i valori `$id` per entrambi gli schemi. Se si conoscono i nomi visualizzati (`title`) degli schemi, è possibile trovare i relativi valori `$id` effettuando una richiesta GET all&#39;endpoint `/tenant/schemas` nell&#39;API [!DNL Schema Registry].

**Formato API**

```http
GET /tenant/schemas
```

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE]
>
>L&#39;intestazione `application/vnd.adobe.xed-id+json` di [!DNL Accept] restituisce solo i titoli, gli ID e le versioni degli schemi risultanti.

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di schemi definiti dall&#39;organizzazione, inclusi `name`, `$id`, `meta:altId` e `version`.

```json
{
    "results": [
        {
            "title": "Newsletter Subscriptions",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/192a66930afad02408429174c311ae73",
            "meta:altId": "_{TENANT_ID}.schemas.192a66930afad02408429174c311ae73",
            "version": "1.2"
        },
        {
            "title": "Loyalty Members",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
            "version": "1.5"
        },
        {
            "title": "Hotels",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
            "meta:altId": "_{TENANT_ID}.schemas.d4ad4b8463a67f6755f2aabbeb9e02c7",
            "version": "1.0"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform-stage.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

Registra i valori `$id` dei due schemi tra cui vuoi definire una relazione. Questi valori verranno utilizzati nei passaggi successivi.

## Definisci un campo di riferimento per lo schema di origine

All&#39;interno di [!DNL Schema Registry], i descrittori di relazione funzionano in modo simile alle chiavi esterne nelle tabelle del database relazionale: un campo nello schema di origine funge da riferimento al campo di identità primaria di uno schema di riferimento. Se lo schema di origine non dispone di un campo per questo scopo, potrebbe essere necessario creare un gruppo di campi schema con il nuovo campo e aggiungerlo allo schema. Questo nuovo campo deve avere un valore `type` di `string`.

>[!IMPORTANT]
>
>Lo schema di origine non può utilizzare la propria identità primaria come campo di riferimento.

In questa esercitazione, lo schema di riferimento &quot;[!DNL Hotels]&quot; contiene un campo `hotelId` che funge da identità primaria dello schema. Tuttavia, lo schema di origine &quot;[!DNL Loyalty Members]&quot; non dispone di un campo dedicato da utilizzare come riferimento a `hotelId`, pertanto è necessario creare un gruppo di campi personalizzato per aggiungere un nuovo campo allo schema: `favoriteHotel`.

>[!NOTE]
>
>Se lo schema di origine dispone già di un campo dedicato che intendi utilizzare come campo di riferimento, puoi passare al passaggio [creazione di un descrittore di riferimento](#reference-identity).

### Crea un nuovo gruppo di campi

Per aggiungere un nuovo campo a uno schema, è necessario innanzitutto definirlo in un gruppo di campi. È possibile creare un nuovo gruppo di campi effettuando una richiesta POST all&#39;endpoint `/tenant/fieldgroups`.

**Formato API**

```http
POST /tenant/fieldgroups
```

**Richiesta**

La richiesta seguente crea un nuovo gruppo di campi che aggiunge un campo `favoriteHotel` nello spazio dei nomi `_{TENANT_ID}` di qualsiasi schema a cui viene aggiunto.

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel field group for the Loyalty Members schema.",
        "definitions": {
            "favoriteHotel": {
              "properties": {
                "_{TENANT_ID}": {
                  "type":"object",
                  "properties": {
                    "favoriteHotel": {
                      "title": "Favorite Hotel",
                      "type": "string",
                      "description": "Favorite hotel for a Loyalty Member."
                    }
                  }
                }
              }
            }
        },
        "allOf": [
            {
              "$ref": "#/definitions/favoriteHotel"
            }
        ]
      }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del gruppo di campi appena creato.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220",
    "meta:altId": "_{TENANT_ID}.mixins.3387945212ad76ee59b6d2b964afb220",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "type": "object",
    "title": "Favorite Hotel",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Favorite hotel field group for the Loyalty Members schema.",
    "definitions": {
        "favoriteHotel": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "favoriteHotel": {
                            "title": "Favorite Hotel",
                            "type": "string",
                            "description": "Favorite hotel for a Loyalty Member.",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/favoriteHotel"
        }
    ],
    "meta:xdmType": "object",
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:registryMetadata": {
        "eTag": "quM2aMPyb2NkkEiZHNCs/MG34E4=",
        "palm:sandboxName": "prod"
    }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `$id` | Identificatore univoco del nuovo gruppo di campi generato dal sistema e di sola lettura. Si presenta sotto forma di URI. |

{style="table-layout:auto"}

Registra l&#39;URI `$id` del gruppo di campi, da utilizzare nel passaggio successivo per aggiungere il gruppo di campi allo schema di origine.

### Aggiungere il gruppo di campi allo schema di origine

Dopo aver creato un gruppo di campi, è possibile aggiungerlo allo schema di origine effettuando una richiesta PATCH all&#39;endpoint `/tenant/schemas/{SCHEMA_ID}`.

**Formato API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | URI `$id` con codifica URL o `meta:altId` dello schema di origine. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente aggiunge il gruppo di campi &quot;[!DNL Favorite Hotel]&quot; allo schema &quot;[!DNL Loyalty Members]&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    { 
      "op": "add", 
      "path": "/allOf/-", 
      "value":  {
        "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
      }
    }
  ]'
```

| Proprietà | Descrizione |
| --- | --- |
| `op` | Operazione PATCH da eseguire. Questa richiesta utilizza l&#39;operazione `add`. |
| `path` | Percorso del campo schema in cui verrà aggiunta la nuova risorsa. Quando si aggiungono gruppi di campi agli schemi, il valore deve essere &quot;/allOf/-&quot;. |
| `value.$ref` | `$id` del gruppo di campi da aggiungere. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli dello schema aggiornato, che ora include il valore `$ref` del gruppo di campi aggiunto nel relativo array `allOf`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
    "meta:resourceType": "schemas",
    "version": "1.1",
    "type": "object",
    "title": "Loyalty Members",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
        }
    ],
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:tenantNamespace": "_{TENANT_ID}",
    "imsOrg": "{ORG_ID}",
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3",
        "https://ns.adobe.com/{TENANT_ID}/mixins/61969bc646b66a6230a7e8840f4a4d33"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557525483804,
        "repo:lastModifiedDate": 1566419670915,
        "xdm:createdClientId": "{API_KEY}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "eTag": "ITNzu8BVTO5pw9wfCtTTpk6U4WY="
    }
}
```

## Creare un descrittore di identità di riferimento {#reference-identity}

Ai campi schema deve essere applicato un descrittore di identità di riferimento se vengono utilizzati come riferimento a un altro schema in una relazione. Poiché il campo `favoriteHotel` in &quot;[!DNL Loyalty Members]&quot; farà riferimento al campo `hotelId` in &quot;[!DNL Hotels]&quot;, a `favoriteHotel` deve essere assegnato un descrittore di identità di riferimento.

Creare un descrittore di riferimento per lo schema di origine effettuando una richiesta POST all&#39;endpoint `/tenant/descriptors`.

**Formato API**

```http
POST /tenant/descriptors
```

**Richiesta**

La richiesta seguente crea un descrittore di riferimento per il campo `favoriteHotel` nello schema di origine &quot;[!DNL Loyalty Members]&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID"
  }'
```

| Parametro | Descrizione |
| --- | --- |
| `@type` | Tipo di descrittore da definire. Per i descrittori di riferimento il valore deve essere `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | URL `$id` dello schema di origine. |
| `xdm:sourceVersion` | Numero di versione dello schema di origine. |
| `sourceProperty` | Percorso del campo nello schema di origine che verrà utilizzato per fare riferimento all&#39;identità primaria dello schema di riferimento. |
| `xdm:identityNamespace` | Lo spazio dei nomi dell’identità del campo di riferimento. Deve corrispondere allo stesso spazio dei nomi dell’identità primaria dello schema di riferimento. Per ulteriori informazioni, consulta la [panoramica dello spazio dei nomi delle identità](../../identity-service/home.md). |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del descrittore di riferimento appena creato per il campo sorgente.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Creare un descrittore di relazione {#create-descriptor}

I descrittori di relazione stabiliscono una relazione uno-a-uno tra uno schema di origine e uno schema di riferimento. Dopo aver definito un descrittore di identità di riferimento per il campo appropriato nello schema di origine, è possibile creare un nuovo descrittore di relazione effettuando una richiesta POST all&#39;endpoint `/tenant/descriptors`.

**Formato API**

```http
POST /tenant/descriptors
```

**Richiesta**

La richiesta seguente crea un nuovo descrittore di relazione, con &quot;[!DNL Loyalty Members]&quot; come schema di origine e &quot;[!DNL Hotels]&quot; come schema di riferimento.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId"
  }'
```

| Parametro | Descrizione |
| --- | --- |
| `@type` | Tipo di descrittore da creare. Il valore `@type` per i descrittori di relazione è `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | URL `$id` dello schema di origine. |
| `xdm:sourceVersion` | Numero di versione dello schema di origine. |
| `xdm:sourceProperty` | Percorso del campo di riferimento nello schema di origine. |
| `xdm:destinationSchema` | URL `$id` dello schema di riferimento. |
| `xdm:destinationVersion` | Numero di versione dello schema di riferimento. |
| `xdm:destinationProperty` | Percorso del campo dell’identità primaria nello schema di riferimento. |

{style="table-layout:auto"}

### Risposta

In caso di esito positivo, la risposta restituisce i dettagli del descrittore di relazione appena creato.

```json
{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId",
    "meta:containerId": "tenant",
    "@id": "76f6cc7105f4eaab7eb4a5e1cb4804cadc741669"
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente una relazione uno-a-uno tra due schemi. Per ulteriori informazioni sull&#39;utilizzo dei descrittori tramite l&#39;API [!DNL Schema Registry], vedere la [Guida per gli sviluppatori del registro dello schema](../api/descriptors.md). Per informazioni su come definire le relazioni tra schemi nell&#39;interfaccia utente, vedere l&#39;esercitazione [definizione delle relazioni tra schemi tramite l&#39;Editor di schema](relationship-ui.md).
