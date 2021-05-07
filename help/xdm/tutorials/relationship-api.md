---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;modello dati;registro schema;schema;schema;schemi;schemi;schemi;relazione;relazione;descrittore di relazione;descrittore di relazione;identità di riferimento;identità di riferimento;
solution: Experience Platform
title: Definire una relazione tra due schemi utilizzando l’API del Registro di sistema dello schema
description: Questo documento fornisce un'esercitazione per definire una relazione uno-a-uno tra due schemi definiti dall'organizzazione utilizzando l'API del Registro di sistema dello schema.
topic-legacy: tutorial
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '1354'
ht-degree: 1%

---

# Definire una relazione tra due schemi utilizzando l’API [!DNL Schema Registry]

La capacità di comprendere le relazioni tra i clienti e le loro interazioni con il tuo marchio attraverso vari canali è una parte importante di Adobe Experience Platform. La definizione di queste relazioni all’interno della struttura degli schemi [!DNL Experience Data Model] (XDM) consente di ottenere informazioni complesse sui dati dei clienti.

Mentre le relazioni dello schema possono essere dedotte mediante l&#39;uso dello schema di unione e di [!DNL Real-time Customer Profile], questo vale solo per gli schemi che condividono la stessa classe. Per stabilire una relazione tra due schemi appartenenti a classi diverse, è necessario aggiungere un campo di relazione dedicato a uno schema di origine che fa riferimento all&#39;identità di uno schema di destinazione.

Questo documento fornisce un&#39;esercitazione per definire una relazione uno-a-uno tra due schemi definiti dall&#39;organizzazione utilizzando il percorso [[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Introduzione

Questa esercitazione richiede una buona comprensione di [!DNL Experience Data Model] (XDM) e [!DNL XDM System]. Prima di iniziare questa esercitazione, consulta la seguente documentazione:

* [Sistema XDM in Experience Platform](../home.md): Panoramica di XDM e della sua implementazione in  [!DNL Experience Platform].
   * [Nozioni di base sulla composizione](../schema/composition.md) dello schema: Introduzione dei blocchi costitutivi degli schemi XDM.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Prima di avviare questa esercitazione, controlla la [guida per gli sviluppatori](../api/getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’ API [!DNL Schema Registry]. Questo include il tuo `{TENANT_ID}`, il concetto di &quot;contenitori&quot; e le intestazioni richieste per effettuare richieste (con particolare attenzione all&#39;intestazione [!DNL Accept] e ai suoi possibili valori).

## Definire uno schema di origine e destinazione {#define-schemas}

È previsto che siano già stati creati i due schemi che verranno definiti nella relazione. Questa esercitazione crea una relazione tra i membri del programma fedeltà corrente di un&#39;organizzazione (definito in uno schema &quot;[!DNL Loyalty Members]&quot;) e i loro alberghi preferiti (definito in uno schema &quot;[!DNL Hotels]&quot;).

Le relazioni dello schema sono rappresentate da uno **schema di origine** con un campo che fa riferimento a un altro campo all&#39;interno di uno **schema di destinazione**. Nei passaggi seguenti, &quot;[!DNL Loyalty Members]&quot; sarà lo schema di origine, mentre &quot;[!DNL Hotels]&quot; fungerà da schema di destinazione.

>[!IMPORTANT]
>
>Per stabilire una relazione, entrambi gli schemi devono avere identità principali definite ed essere abilitati per [!DNL Real-time Customer Profile]. Per informazioni su come configurare di conseguenza gli schemi, consulta la sezione relativa all’ [abilitazione di uno schema da utilizzare in Profile](./create-schema-api.md#profile) nell’esercitazione sulla creazione dello schema.

Per definire una relazione tra due schemi, è innanzitutto necessario acquisire i valori `$id` di entrambi gli schemi. Se conosci i nomi visualizzati (`title`) degli schemi, puoi trovare i loro valori `$id` effettuando una richiesta di GET all’endpoint `/tenant/schemas` nell’API [!DNL Schema Registry].

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE]
>
>L&#39;intestazione [!DNL Accept] `application/vnd.adobe.xed-id+json` restituisce solo i titoli, gli ID e le versioni degli schemi risultanti.

**Risposta**

Una risposta corretta restituisce un elenco di schemi definiti dall’organizzazione, inclusi `name`, `$id`, `meta:altId` e `version`.

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

Registra i valori `$id` dei due schemi che desideri definire una relazione tra di essi. Questi valori verranno utilizzati nei passaggi successivi.

## Definire un campo di riferimento per lo schema di origine

All&#39;interno di [!DNL Schema Registry], i descrittori di relazione funzionano in modo simile alle chiavi esterne nelle tabelle di database relazionali: un campo nello schema di origine funge da riferimento al campo di identità principale di uno schema di destinazione. Se lo schema di origine non dispone di un campo per questo scopo, potrebbe essere necessario creare un gruppo di campi dello schema con il nuovo campo e aggiungerlo allo schema. Questo nuovo campo deve avere un valore `type` di &quot;[!DNL string]&quot;.

>[!IMPORTANT]
>
>A differenza dello schema di destinazione, lo schema di origine non può utilizzare la propria identità primaria come campo di riferimento.

In questa esercitazione, lo schema di destinazione &quot;[!DNL Hotels]&quot; contiene un campo `hotelId` che funge da identità principale dello schema e agisce quindi anche come campo di riferimento. Tuttavia, lo schema di origine &quot;[!DNL Loyalty Members]&quot; non dispone di un campo dedicato da utilizzare come riferimento e deve essere assegnato un nuovo gruppo di campi che aggiunge un nuovo campo allo schema: `favoriteHotel`.

>[!NOTE]
>
>Se lo schema di origine dispone già di un campo dedicato che si intende utilizzare come campo di riferimento, è possibile passare al passaggio [creazione di un descrittore di riferimento](#reference-identity).

### Crea un nuovo gruppo di campi

Per aggiungere un nuovo campo a uno schema, è innanzitutto necessario definirlo in un gruppo di campi. È possibile creare un nuovo gruppo di campi effettuando una richiesta POST all&#39;endpoint `/tenant/fieldgroups`.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Una risposta corretta restituisce i dettagli del gruppo di campi appena creato.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/3387945212ad76ee59b6d2b964afb220",
    "meta:altId": "_{TENANT_ID}.fieldgroups.3387945212ad76ee59b6d2b964afb220",
    "meta:resourceType": "fieldgroups",
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
| `$id` | Identificatore univoco del nuovo gruppo di campi generato dal sistema di sola lettura. Si presenta sotto forma di URI. |

Registra l&#39; URI `$id` del gruppo di campi, da utilizzare nel passaggio successivo dell&#39;aggiunta del gruppo di campi allo schema di origine.

### Aggiungi il gruppo di campi allo schema di origine

Dopo aver creato un gruppo di campi, è possibile aggiungerlo allo schema di origine effettuando una richiesta PATCH all&#39;endpoint `/tenant/schemas/{SCHEMA_ID}`.

**Formato API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | URI con codifica URL `$id` o `meta:altId` dello schema di origine. |

**Richiesta**

La richiesta seguente aggiunge il gruppo di campi &quot;[!DNL Favorite Hotel]&quot; allo schema &quot;[!DNL Loyalty Members]&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    { 
      "op": "add", 
      "path": "/allOf/-", 
      "value":  {
        "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/3387945212ad76ee59b6d2b964afb220"
      }
    }
  ]'
```

| Proprietà | Descrizione |
| --- | --- |
| `op` | Operazione PATCH da eseguire. Questa richiesta utilizza l&#39;operazione `add` . |
| `path` | Percorso del campo schema in cui verrà aggiunta la nuova risorsa. Quando si aggiungono gruppi di campi agli schemi, il valore deve essere &quot;/allOf/-&quot;. |
| `value.$ref` | Il `$id` del gruppo di campi da aggiungere. |

**Risposta**

Una risposta corretta restituisce i dettagli dello schema aggiornato, che ora include il valore `$ref` del gruppo di campi aggiunti sotto la relativa matrice `allOf`.

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
            "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/ec16dfa484358f80478b75cde8c430d3"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/3387945212ad76ee59b6d2b964afb220"
        }
    ],
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:tenantNamespace": "_{TENANT_ID}",
    "imsOrg": "{IMS_ORG}",
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/fieldgroups/ec16dfa484358f80478b75cde8c430d3",
        "https://ns.adobe.com/{TENANT_ID}/fieldgroups/61969bc646b66a6230a7e8840f4a4d33"
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

Ai campi dello schema deve essere applicato un descrittore di identità di riferimento se vengono utilizzati come riferimento da altri schemi in una relazione. Poiché il campo `favoriteHotel` in &quot;[!DNL Loyalty Members]&quot; fa riferimento al campo `hotelId` in &quot;[!DNL Hotels]&quot;, `hotelId` deve avere un descrittore di identità di riferimento.

Crea un descrittore di riferimento per lo schema di destinazione effettuando una richiesta POST all&#39;endpoint `/tenant/descriptors`.

**Formato API**

```http
POST /tenant/descriptors
```

**Richiesta**

La richiesta seguente crea un descrittore di riferimento per il campo `hotelId` nello schema di destinazione &quot;[!DNL Hotels]&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "Hotel ID"
  }'
```

| Parametro | Descrizione |
| --- | --- |
| `@type` | Il tipo di descrittore da definire. Per i descrittori di riferimento il valore deve essere &quot;xdm:descriptorReferenceIdentity&quot;. |
| `xdm:sourceSchema` | URL `$id` dello schema di destinazione. |
| `xdm:sourceVersion` | Numero di versione dello schema di destinazione. |
| `sourceProperty` | Percorso del campo di identità principale dello schema di destinazione. |
| `xdm:identityNamespace` | Spazio dei nomi identità del campo di riferimento. Deve essere lo stesso namespace utilizzato quando si definisce il campo come identità principale dello schema. Per ulteriori informazioni, consulta la [panoramica dello spazio dei nomi di identità](../../identity-service/home.md) . |

**Risposta**

Una risposta corretta restituisce i dettagli del descrittore di riferimento appena creato per lo schema di destinazione.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Creare un descrittore di relazione {#create-descriptor}

I descrittori di relazione stabiliscono una relazione uno-a-uno tra uno schema di origine e uno schema di destinazione. Una volta definito un descrittore di riferimento per lo schema di destinazione, puoi creare un nuovo descrittore di relazione effettuando una richiesta POST all&#39;endpoint `/tenant/descriptors`.

**Formato API**

```http
POST /tenant/descriptors
```

**Richiesta**

La richiesta seguente crea un nuovo descrittore di relazione, con &quot;[!DNL Loyalty Members]&quot; come schema di origine e &quot;[!DNL Legacy Loyalty Members]&quot; come schema di destinazione.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `@type` | Il tipo di descrittore da creare. Il valore `@type` per i descrittori di relazione è &quot;xdm:descriptorOneToOne&quot;. |
| `xdm:sourceSchema` | URL `$id` dello schema di origine. |
| `xdm:sourceVersion` | Numero di versione dello schema di origine. |
| `xdm:sourceProperty` | Percorso del campo di riferimento nello schema di origine. |
| `xdm:destinationSchema` | URL `$id` dello schema di destinazione. |
| `xdm:destinationVersion` | Numero di versione dello schema di destinazione. |
| `xdm:destinationProperty` | Percorso del campo di riferimento nello schema di destinazione. |

### Risposta

Una risposta corretta restituisce i dettagli del descrittore di relazione appena creato.

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

Seguendo questa esercitazione, è stata creata una relazione uno-a-uno tra due schemi. Per ulteriori informazioni sull&#39;utilizzo dei descrittori tramite l&#39;API [!DNL Schema Registry], consulta la [Guida per gli sviluppatori del Registro di sistema dello schema](../api/descriptors.md). Per i passaggi su come definire le relazioni di schema nell&#39;interfaccia utente, consulta l&#39;esercitazione su [definizione delle relazioni di schema utilizzando l&#39;Editor di schema](relationship-ui.md).
