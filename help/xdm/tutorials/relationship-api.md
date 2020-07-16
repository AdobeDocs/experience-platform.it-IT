---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definire una relazione tra due schemi utilizzando l'API del Registro di sistema dello schema
topic: tutorials
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '1458'
ht-degree: 1%

---


# Definire una relazione tra due schemi utilizzando l&#39; [!DNL Schema Registry] API


La capacità di comprendere le relazioni tra i clienti e le loro interazioni con il tuo marchio attraverso vari canali è una parte importante del  Adobe Experience Platform. La definizione di queste relazioni all&#39;interno della struttura degli schemi [!DNL Experience Data Model] (XDM) consente di acquisire informazioni complesse sui dati dei clienti.

Questo documento fornisce un&#39;esercitazione per definire una relazione uno-a-uno tra due schemi definiti dall&#39;organizzazione che utilizza l&#39; [!DNL Schema Registry API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Introduzione

Questa esercitazione richiede una buona conoscenza di [!DNL Experience Data Model] (XDM) e [!DNL XDM System]. Prima di iniziare questa esercitazione, consulta la seguente documentazione:

* [Sistema XDM in  Experience Platform](../home.md): Panoramica di XDM e della relativa implementazione in  Experience Platform.
   * [Nozioni di base sulla composizione](../schema/composition.md)dello schema: Introduzione dei blocchi costitutivi degli schemi XDM.
* [!DNL Real-time Customer Profile](../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Prima di iniziare questa esercitazione, consulta la guida [allo](../api/getting-started.md) sviluppo per informazioni importanti da conoscere per effettuare correttamente le chiamate all&#39; [!DNL Schema Registry] API. Ciò include il vostro `{TENANT_ID}`, il concetto di &quot;contenitori&quot; e le intestazioni necessarie per effettuare le richieste (con particolare attenzione all’intestazione Accetta e ai suoi possibili valori).

## Definire uno schema di origine e di destinazione {#define-schemas}

È previsto che siano già stati creati i due schemi che verranno definiti nella relazione. Questa esercitazione crea una relazione tra i membri del programma fedeltà corrente di un&#39;organizzazione (definito in uno schema &quot;Membri fedeltà&quot;) e i loro alberghi preferiti (definiti in uno schema &quot;Hotel&quot;).

Le relazioni dello schema sono rappresentate da un **[!UICONTROL source schema]** campo che fa riferimento a un altro campo all&#39;interno di un campo **[!UICONTROL destination schema]**. Nei passaggi successivi, &quot;[!UICONTROL Loyalty Members]&quot; sarà lo schema di origine, mentre &quot;[!UICONTROL Hotels]&quot; fungerà da schema di destinazione.

Per definire una relazione tra due schemi, è innanzitutto necessario acquisire i `$id` valori per entrambi gli schemi. Se conoscete i nomi visualizzati (`title`) degli schemi, potete trovare `$id` i relativi valori effettuando una richiesta GET all&#39; `/tenant/schemas` endpoint nell&#39; [!DNL Schema Registry] API.

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
>L’intestazione Accetta `application/vnd.adobe.xed-id+json` restituisce solo i titoli, gli ID e le versioni degli schemi risultanti.

**Risposta**

Una risposta corretta restituisce un elenco di schemi definiti dall’organizzazione, inclusi i relativi schemi `name`, `$id`, `meta:altId`e `version`.

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

Registrare i `$id` valori dei due schemi tra cui si desidera definire una relazione. Questi valori verranno utilizzati nei passaggi successivi.

## Definire i campi di riferimento per entrambi gli schemi

All&#39;interno [!DNL Schema Registry], i descrittori di relazione funzionano in modo simile alle chiavi esterne nelle tabelle SQL: un campo nello schema di origine funge da riferimento a un campo di uno schema di destinazione. Quando si definisce una relazione, ogni schema deve avere un campo dedicato da utilizzare come riferimento all&#39;altro schema.

>[!IMPORTANT]
>
>Se gli schemi devono essere abilitati per l&#39;uso in [!DNL Real-time Customer Profile](../../profile/home.md), il campo di riferimento per lo schema di destinazione deve essere il relativo **[!UICONTROL primary identity]**. Questo è spiegato più in dettaglio in questa esercitazione.

Se uno schema non dispone di un campo a questo scopo, potrebbe essere necessario creare un mixin con il nuovo campo e aggiungerlo allo schema. Il nuovo campo deve avere un `type` valore &quot;string&quot;.

Ai fini di questa esercitazione, lo schema di destinazione &quot;Hotels&quot; contiene già un campo a tal fine: `hotelId`. Tuttavia, lo schema di origine &quot;Membri fedeltà&quot; non dispone di tale campo e deve essere dotato di un nuovo mixin che aggiunga un nuovo campo, `favoriteHotel`sotto il relativo `TENANT_ID` spazio nomi.

### Creare un nuovo mixin

Per aggiungere un nuovo campo a uno schema, è innanzitutto necessario definirlo in un mixin. Per creare un nuovo mixin, effettuate una richiesta POST all’ `/tenant/mixins` endpoint.

**Formato API**

```http
POST /tenant/mixins
```

**Richiesta**

La richiesta seguente crea un nuovo mixin che aggiunge un `favoriteHotel` campo nello `TENANT_ID` spazio dei nomi di qualsiasi schema a cui viene aggiunto.

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel mixin for the Loyalty Members schema.",
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

Una risposta corretta restituisce i dettagli del mixin appena creato.

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
    "description": "Favorite hotel mixin for the Loyalty Members schema.",
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
| `$id` | Identificatore univoco del nuovo mixin generato dal sistema di sola lettura. Ha la forma di un URI. |

Registra l’ `$id` URI del mixin, da utilizzare nel passaggio successivo per aggiungere il mixin allo schema di origine.

### Aggiungere il mixin allo schema di origine

Dopo aver creato un mixin, potete aggiungerlo allo schema di origine effettuando una richiesta PATCH all&#39; `/tenant/schemas/{SCHEMA_ID}` endpoint.

**Formato API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | L&#39; `$id` URI con codifica URL o `meta:altId` dello schema di origine. |

**Richiesta**

La richiesta seguente aggiunge il mixin &quot;Favorite Hotel&quot; allo schema &quot;Fedeltà Membri&quot;.

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
        "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
      }
    }
  ]'
```

| Proprietà | Descrizione |
| --- | --- |
| `op` | L’operazione PATCH da eseguire. Questa richiesta utilizza l&#39; `add` operazione. |
| `path` | Percorso del campo dello schema in cui verrà aggiunta la nuova risorsa. Quando si aggiungono mixin agli schemi, il valore deve essere `/allOf/-`. |
| `value.$ref` | Il `$id` valore del mixin da aggiungere. |

**Risposta**

Una risposta corretta restituisce i dettagli dello schema aggiornato, che ora include il `$ref` valore del mixin aggiunto sotto la sua `allOf` matrice.

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
    "imsOrg": "{IMS_ORG}",
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

## Definire i campi identità primari per entrambi gli schemi

>[!NOTE]
>
>Questo passaggio è richiesto solo per gli schemi che saranno attivati per l&#39;utilizzo in [!DNL Real-time Customer Profile](../../profile/home.md). Se non si desidera che uno schema partecipi a un&#39;unione o se gli schemi dispongono già di identità primarie definite, è possibile passare alla fase successiva della [creazione di un descrittore](#create-descriptor) di identità di riferimento per lo schema di destinazione.

Affinché gli schemi possano essere attivati per l&#39;uso in [!DNL Real-time Customer Profile], è necessario che abbiano definito un&#39;identità primaria. Inoltre, lo schema di destinazione di una relazione deve utilizzare la propria identità primaria come campo di riferimento.

Ai fini di questa esercitazione, lo schema di origine ha già un&#39;identità primaria definita, ma non lo schema di destinazione. È possibile contrassegnare un campo dello schema come campo di identità principale creando un descrittore di identità. Questa operazione viene eseguita eseguendo una richiesta POST all&#39; `/tenant/descriptors` endpoint.

**Formato API**

```http
POST /tenant/descriptors
```

**Richiesta**

La richiesta seguente crea un nuovo descrittore di identità che definisce il `hotelId` campo dello schema di destinazione &quot;Hotels&quot; come campo di identità principale.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true
  }'
```

| Parametro | Descrizione |
| --- | --- |
| `@type` | Il tipo di descrittore da creare. Il `@type` valore dei descrittori di identità è `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | Il `$id` valore dello schema di destinazione, ottenuto nel passaggio [](#define-schemas)precedente. |
| `xdm:sourceVersion` | Numero di versione dello schema. |
| `sourceProperty` | Percorso del campo specifico che fungerà da identità principale dello schema. Questo percorso deve iniziare con &quot;/&quot; e non terminare con uno, escludendo anche eventuali spazi dei nomi &quot;proprietà&quot;. Ad esempio, la richiesta di cui sopra utilizza `/_{TENANT_ID}/hotelId` invece di `/properties/_{TENANT_ID}/properties/hotelId`. |
| `xdm:namespace` | Spazio dei nomi identità per il campo identità. `hotelId` è un valore ECID in questo esempio, pertanto viene utilizzato lo spazio dei nomi &quot;ECID&quot;. Per un elenco degli spazi dei nomi disponibili, consultate la panoramica [dello spazio dei nomi](../../identity-service/home.md) identità. |
| `xdm:isPrimary` | Proprietà booleana che determina se il campo identità sarà l&#39;identità principale per lo schema. Poiché questa richiesta definisce un&#39;identità primaria, il valore è impostato su true. |

**Risposta**

Una risposta corretta restituisce i dettagli del descrittore di identità appena creato.

```json
{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true,
    "meta:containerId": "tenant",
    "@id": "e3cfa302d06dc27080e6b54663511a02dd61316f"
}
```

## Creare un descrittore di identità di riferimento

Ai campi dello schema deve essere applicato un descrittore di identità di riferimento se questi vengono utilizzati come riferimento da altri schemi in una relazione. Poiché il `favoriteHotel` campo in &quot;Membri fedeltà&quot; farà riferimento al `hotelId` campo in &quot;Hotel&quot;, `hotelId` deve essere fornito un descrittore di identità di riferimento.

Create un descrittore di riferimento per lo schema di destinazione effettuando una richiesta POST all&#39; `/tenant/descriptors` endpoint.

**Formato API**

```http
POST /tenant/descriptors
```

**Richiesta**

La richiesta seguente crea un descrittore di riferimento per il `hotelId` campo nello schema di destinazione &quot;Hotels&quot;.

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
    "xdm:identityNamespace": "ECID"
  }'
```

| Parametro | Descrizione |
| --- | --- |
| `xdm:sourceSchema` | L&#39; `$id` URL dello schema di destinazione. |
| `xdm:sourceVersion` | Il numero di versione dello schema di destinazione. |
| `sourceProperty` | Percorso del campo identità principale dello schema di destinazione. |
| `xdm:identityNamespace` | Lo spazio dei nomi identità del campo di riferimento. `hotelId` è un valore ECID in questo esempio, pertanto viene utilizzato lo spazio dei nomi &quot;ECID&quot;. Per un elenco degli spazi dei nomi disponibili, consultate la panoramica [dello spazio dei nomi](../../identity-service/home.md) identità. |

**Risposta**

Una risposta corretta restituisce i dettagli del descrittore di riferimento appena creato per lo schema di destinazione.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "ECID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Creare un descrittore di relazione {#create-descriptor}

I descrittori delle relazioni stabiliscono una relazione uno-a-uno tra uno schema di origine e uno schema di destinazione. Potete creare un nuovo descrittore di relazione facendo una richiesta POST all&#39; `/tenant/descriptors` endpoint.

**Formato API**

```http
POST /tenant/descriptors
```

**Richiesta**

La richiesta seguente crea un nuovo descrittore di relazione, con &quot;Membri fedeltà&quot; come schema di origine e &quot;Membri fedeltà legacy&quot; come schema di destinazione.

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
| `@type` | Il tipo di descrittore da creare. Il `@type` valore dei descrittori di relazione è `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | L&#39; `$id` URL dello schema di origine. |
| `xdm:sourceVersion` | Il numero di versione dello schema di origine. |
| `sourceProperty`: | Percorso del campo di riferimento nello schema di origine. |
| `xdm:destinationSchema` | L&#39; `$id` URL dello schema di destinazione. |
| `xdm:destinationVersion` | Il numero di versione dello schema di destinazione. |
| `destinationProperty`: | Percorso del campo di riferimento nello schema di destinazione. |

### Risposta

Una risposta corretta restituisce i dettagli del descrittore della relazione appena creato.

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

Seguendo questa esercitazione, è stata creata una relazione uno-a-uno tra due schemi. Per ulteriori informazioni sull&#39;utilizzo dei descrittori tramite l&#39; [!DNL Schema Registry] API, vedere la guida [per gli sviluppatori del Registro di](../api/getting-started.md)schema. Per informazioni sulla definizione delle relazioni tra schemi nell&#39;interfaccia utente, vedere l&#39;esercitazione sulla [definizione delle relazioni tra schemi utilizzando l&#39;Editor](relationship-ui.md)di schema.