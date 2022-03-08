---
title: Estendi un campo con enumerazione sfumata
description: Scopri come estendere un campo enum soft nell’API del Registro di sistema dello schema.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: a26c8d43ff7874bcedd2adb3d6da995986198c96
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Estendere un campo di enum morbido

In Experience Data Model (XDM), un campo enum rappresenta un campo stringa vincolato a un sottoinsieme di valori predefinito. I campi Enum possono fornire una convalida per garantire che i dati acquisiti siano conformi a un insieme di valori accettati (denominati &quot;enum rigido&quot;), oppure possono semplicemente rappresentare un insieme di valori consigliati senza imporre vincoli (denominati &quot;enum morbido&quot;).

Nell’API del Registro di sistema dello schema, i valori vincolati per un enum rigido sono rappresentati da un `enum` mentre un `meta:enum` L&#39;oggetto fornisce nomi visualizzati descrittivi per tali valori:

```json
"sampleHardEnumField": {
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

Per i campi enum rigidi, il Registro di sistema dello schema non consente `meta:enum` da estendere oltre i valori di cui `enum`, poiché il tentativo di acquisire valori stringa al di fuori di tali vincoli non passerebbe la convalida.

Al contrario, un campo di enum morbido non contiene un `enum` utilizza solo `meta:enum` oggetto per indicare i valori consigliati:

```json
"sampleSoftEnumField": {
  "type": "string",
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

Poiché gli enum morbidi non hanno gli stessi vincoli di convalida degli enum rigidi, i loro `meta:enum` è possibile estendere le proprietà per includere nuovi valori. Questa esercitazione illustra come estendere i campi di enum soft standard e personalizzati nell’API del Registro di sistema dello schema.

## Prerequisiti

Questa guida presuppone che tu abbia familiarità con gli elementi della composizione dello schema in XDM e che sia in grado di utilizzare l’API del Registro di sistema dello schema per creare e modificare le risorse XDM. Per un’introduzione, fai riferimento alla seguente documentazione:

* [Nozioni di base sulla composizione dello schema](../schema/composition.md)
* [Guida all’API del registro dello schema](../api/overview.md)

## Estendere un campo standard di enum soft

Per estendere `meta:enum` di un campo stringa standard, è possibile creare un [descrittore del nome descrittivo](../api/descriptors.md#friendly-name) per il campo in questione in uno schema specifico.

>[!NOTE]
>
>Gli enum soft standard possono essere estesi solo a livello di schema. In altre parole, l&#39;estensione del `meta:enum` di un campo standard in uno schema non influisce sugli altri schemi che utilizzano lo stesso campo standard.

La richiesta seguente aggiunge valori soft enum allo standard `eventType` (fornito dal [Classe ExperienceEvent XDM](../classes/experienceevent.md)) per lo schema identificato in `sourceSchema`:

```curl
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## Estendere un campo di enum soft personalizzato

Per estendere `meta:enum` di un campo personalizzato, è possibile aggiornare la classe principale, il gruppo di campi o il tipo di dati del campo tramite una richiesta PATCH.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Questa guida illustra come estendere gli enum soft nell’API del Registro di sistema dello schema. Consulta la guida su [definizione di campi personalizzati nell’API](./custom-fields-api.md) per ulteriori informazioni su come creare diversi tipi di campi.
