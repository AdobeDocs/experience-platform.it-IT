---
title: Gestire i valori consigliati nell’API
description: Scopri come aggiungere valori consigliati a un campo stringa nell’API del Registro di sistema dello schema.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: 2f916ea4b05ca67c2b9e603512d732a2a3f7a3b2
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# Gestire i valori suggeriti nell’API

Per qualsiasi campo stringa in Experience Data Model (XDM), puoi definire un **enum** che vincola i valori che il campo può acquisire a un set predefinito. Se tenti di acquisire dati in un campo enum e il valore non corrisponde a nessuno di quelli definiti nella relativa configurazione, l’acquisizione verrà negata.

A differenza degli enum, aggiunta **valori consigliati** in un campo stringa non vincola i valori che può acquisire. Al contrario, i valori suggeriti influenzano i valori predefiniti disponibili nel [Interfaccia utente di segmentazione](../../segmentation/ui/overview.md) quando si include il campo stringa come attributo.

>[!NOTE]
>
>Si verifica un ritardo di circa cinque minuti perché i valori consigliati aggiornati di un campo si riflettano nell’interfaccia utente Segmentazione.

Questa guida illustra come gestire i valori suggeriti utilizzando [API del Registro di sistema dello schema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Per i passaggi da seguire nell’interfaccia utente di Adobe Experience Platform, consulta la sezione [Guida all’interfaccia utente per enum e valori consigliati](../ui/fields/enum.md).

## Prerequisiti

Questa guida presuppone che tu abbia familiarità con gli elementi della composizione dello schema in XDM e che sia in grado di utilizzare l’API del Registro di sistema dello schema per creare e modificare le risorse XDM. Per un’introduzione, fai riferimento alla seguente documentazione:

* [Nozioni di base sulla composizione dello schema](../schema/composition.md)
* [Guida all’API del registro dello schema](../api/overview.md)

Si consiglia inoltre vivamente di rivedere il [regole di evoluzione per enum e valori suggeriti](../ui/fields/enum.md#evolution) se stai aggiornando i campi esistenti. Se gestisci i valori suggeriti per gli schemi che partecipano a un&#39;unione, consulta la sezione [regole per l’unione di enum e valori consigliati](../ui/fields/enum.md#merging).

## Composizione

Nell’API, i valori vincolati per un **enum** i campi sono rappresentati da un `enum` mentre un `meta:enum` L&#39;oggetto fornisce nomi visualizzati descrittivi per tali valori:

```json
"exampleStringField": {
  "type": "string",
  "enum": [
    "value1",
    "value2",
    "value3"
  ],
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

Per i campi enum, il Registro di sistema dello schema non consente `meta:enum` da estendere oltre i valori di cui `enum`, poiché il tentativo di acquisire valori stringa al di fuori di tali vincoli non passerebbe la convalida.

In alternativa, è possibile definire un campo stringa che non contiene un `enum` utilizza solo `meta:enum` oggetto da indicare **valori consigliati**:

```json
"exampleStringField": {
  "type": "string",
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

Poiché la stringa non ha un `enum` array per definire vincoli, i relativi `meta:enum` può essere estesa per includere nuovi valori.

<!-- ## Manage suggested values for standard fields

For existing standard fields, you can [add suggested values](#add-suggested-standard) or [remove suggested values](#remove-suggested-standard). -->

## Aggiungere valori consigliati a un campo standard {#add-suggested-standard}

Per estendere `meta:enum` di un campo stringa standard, è possibile creare un [descrittore del nome descrittivo](../api/descriptors.md#friendly-name) per il campo in questione in uno schema specifico.

>[!NOTE]
>
>I valori consigliati per i campi stringa possono essere aggiunti solo a livello di schema. In altre parole, l&#39;estensione del `meta:enum` di un campo standard in uno schema non influisce sugli altri schemi che utilizzano lo stesso campo standard.

La seguente richiesta aggiunge valori consigliati allo standard `eventType` (fornito dal [Classe ExperienceEvent XDM](../classes/experienceevent.md)) per lo schema identificato in `sourceSchema`:

```curl
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "sourceProperty": "/eventType",
        "title": {
            "en_us": "Enum Event Type"
        },
        "description": {
            "en_us": "Event type field with soft enum values"
        },
        "meta:enum": {
          "eventA": {
            "en_us": "Event Type A"
          },
          "eventB": {
            "en_us": "Event Type B"
          }
        }
      }'
```

Dopo aver applicato il descrittore, il Registro di sistema dello schema risponde con quanto segue durante il recupero dello schema (risposta troncata per lo spazio):

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "eventType": {
      "type":"string",
      "title": "Enum Event Type",
      "description": "Event type field with soft enum values.",
      "meta:enum": {
        "customEventA": "Custom Event Type A",
        "customEventB": "Custom Event Type B"
      }
    }
  }
}
```

>[!NOTE]
>
>Se il campo standard contiene già valori in `meta:enum`, i nuovi valori del descrittore non sovrascrivono i campi esistenti e vengono aggiunti al loro posto:
>
>
```json
>"standardField": {
>   "type":"string",
>   "title": "Example standard enum field",
>   "description": "Standard field with existing enum values.",
>   "meta:enum": {
>       "standardEventA": "Standard Event Type A",
>       "standardEventB": "Standard Event Type B",
>       "customEventA": "Custom Event Type A",
>       "customEventB": "Custom Event Type B"
>   }
>}
>```

<!-- ### Remove suggested values {#remove-suggested-standard}

If a standard string field has predefined suggested values, you can remove any values that you do not wish to see in segmentation. This is done through by creating a [friendly name descriptor](../api/descriptors.md#friendly-name) for the schema that includes an `xdm:excludeMetaEnum` property.

**API format**

```http
POST /tenant/descriptors
```

**Request**

The following request removes the suggested values "[!DNL Web Form Filled Out]" and "[!DNL Media ping]" for `eventType` in a schema based on the [XDM ExperienceEvent class](../classes/experienceevent.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/xdm:eventType",
        "xdm:excludeMetaEnum": {
          "web.formFilledOut": "Web Form Filled Out",
          "media.ping": "Media ping"
        }
      }'
```

| Property | Description |
| --- | --- |
| `@type` | The type of descriptor being defined. For a friendly name descriptor, this value must be set to `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | The `$id` URI of the schema where the descriptor is being defined. |
| `xdm:sourceVersion` | The major version of the source schema. |
| `xdm:sourceProperty` | The path to the specific property whose suggested values you want to manage. The path should begin with a slash (`/`) and not end with one. Do not include `properties` in the path (for example, use `/personalEmail/address` instead of `/properties/personalEmail/properties/address`). |
| `meta:excludeMetaEnum` | An object that describes the suggested values that should be excluded for the field in segmentation. The key and value for each entry must match those included in the original `meta:enum` of the field in order for the entry to be excluded.  |

{style="table-layout:auto"}

**Response**

A successful response returns HTTP status 201 (Created) and the details of the newly created descriptor. The suggested values included under `xdm:excludeMetaEnum` will now be hidden from the Segmentation UI.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out"
  },
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
``` -->

## Gestione dei valori consigliati per un campo personalizzato {#suggested-custom}

Per gestire `meta:enum` di un campo personalizzato, è possibile aggiornare la classe principale, il gruppo di campi o il tipo di dati del campo tramite una richiesta PATCH.

>[!WARNING]
>
>A differenza dei campi standard, l’ `meta:enum` di un campo personalizzato influisce su tutti gli altri schemi che utilizzano tale campo. Se non desideri che le modifiche si propaghino tra gli schemi, considera invece la creazione di una nuova risorsa personalizzata:
>
>* [Creare una classe personalizzata](../api/classes.md#create)
>* [Creare un gruppo di campi personalizzato](../api/field-groups.md#create)
>* [Creare un tipo di dati personalizzato](../api/data-types.md#create)


La seguente richiesta aggiorna il `meta:enum` di un campo &quot;livello fedeltà&quot; fornito da un tipo di dati personalizzato:

```curl
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/loyaltyLevel/meta:enum",
          "value": {
            "ultra-platinum": "Ultra Platinum",
            "platinum": "Platinum",
            "gold": "Gold",
            "silver": "Silver",
            "bronze": "Bronze"
          }
        }
      ]'
```

Dopo aver applicato la modifica, il Registro di sistema dello schema risponde con quanto segue durante il recupero dello schema (risposta troncata per lo spazio):

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "loyaltyLevel": {
      "type":"string",
      "title": "Loyalty Level",
      "description": "The loyalty program tier that this customer qualifies for.",
      "meta:enum": {
        "ultra-platinum": "Ultra Platinum",
        "platinum": "Platinum",
        "gold": "Gold",
        "silver": "Silver",
        "bronze": "Bronze"
      }
    }
  }
}
```

## Passaggi successivi

Questa guida illustra come gestire i valori consigliati per i campi stringa nell’API del Registro di sistema dello schema. Consulta la guida su [definizione di campi personalizzati nell’API](./custom-fields-api.md) per ulteriori informazioni su come creare diversi tipi di campi.
