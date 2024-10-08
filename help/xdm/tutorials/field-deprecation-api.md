---
title: Dichiarare obsoleto un campo XDM nell’API
description: Scopri come rendere obsoleti i campi Experience Data Model (XDM) nell’API Schema Registry.
exl-id: e49517c4-608d-4e05-8466-75724ca984a8
source-git-commit: f9f783b75bff66d1bf3e9c6d1ed1c543bd248302
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 6%

---

# Deprecare un campo XDM nell’API

In Experience Data Model (XDM), è possibile rendere obsoleto un campo all&#39;interno di uno schema o di una risorsa personalizzata utilizzando l&#39;[API Schema Registry](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Se un campo viene dichiarato obsoleto, viene nascosto nelle interfacce utente a valle, ad esempio nell&#39;area di lavoro e nel Customer Journey Analytics [!UICONTROL Profili]. In caso contrario, si tratta di una modifica che non interrompe il processo e non influisce negativamente sui flussi di dati esistenti.

Questo documento illustra come rendere obsoleti i campi per diverse risorse XDM. Per i passaggi relativi alla deprecazione di un campo XDM tramite l&#39;Editor di schema nell&#39;interfaccia utente di Experience Platform, consulta l&#39;esercitazione su [deprecazione di un campo XDM nell&#39;interfaccia utente](./field-deprecation-ui.md).

## Introduzione

Questo tutorial richiede l’esecuzione di chiamate all’API Schema Registry. Consulta la [guida per gli sviluppatori](../api/getting-started.md) per informazioni importanti che devi conoscere per effettuare queste chiamate API. Ciò include `{TENANT_ID}`, il concetto di &quot;contenitori&quot; e le intestazioni necessarie per effettuare le richieste (con particolare attenzione all&#39;intestazione `Accept` e ai suoi possibili valori).

## Dichiarare obsoleto un campo personalizzato {#custom}

Per rendere obsoleto un campo in una classe, un gruppo di campi o un tipo di dati personalizzato, aggiornare la risorsa personalizzata tramite una richiesta PUT o PATCH e aggiungere l&#39;attributo `meta:status: deprecated` al campo in questione.

>[!NOTE]
>
>Per informazioni generali sull’aggiornamento delle risorse personalizzate in XDM, consulta la seguente documentazione:
>
>* [Aggiorna una classe](../api/classes.md#patch)
>* [Aggiorna un gruppo di campi](../api/field-groups.md#patch)
>* [Aggiornare un tipo di dati](../api/data-types.md#patch)

La chiamata API di esempio seguente depreca un campo in un tipo di dati personalizzato.

**Formato API**

```http
PATCH /tenant/datatypes/{DATA_TYPE_ID}
```

**Richiesta**

La richiesta seguente depreca il campo `expansionArea` per un tipo di dati che descrive una proprietà immobiliare.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/properties/expansionArea/meta:status",
          "value": "deprecated"
        }
      ]'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli di aggiornamento della risorsa personalizzata, con il campo obsoleto contenente un valore `meta:status` di `deprecated`. La risposta di esempio seguente è stata troncata per motivi di spazio.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "datatypes",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a real-estate property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
        "properties": {
            "expansionArea": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
              "meta:status": "deprecated",
            },
            "propertyName": {
              "title": "Property Name",
              "description": "Name of the property",
              "type": "string"
            },
            "propertyCity": {
              "title": "Property City",
              "description": "City where the property is located.",
              "type": "string"
            },
            "propertyCountry": {
              "title": "Property Country",
              "description": "Country where the property is located.",
              "type": "string"
            },
            "phoneNumber": {
              "title": "Phone Number",
              "description": "Primary phone number for the property.",
              "type": "string"
            },
            "propertyType": {
              "type": "string",
              "title": "Property Type",
              "description": "Type and primary use of property.",
              "enum": [
                  "retail",
                  "yoga",
                  "fitness"
              ],
              "meta:enum": {
                  "retail": "Retail Store",
                  "yoga": "Yoga Studio",
                  "fitness": "Fitness Center"
              }
            },
            "propertyConstruction": {
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
            },
            "squareFeet": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1594941263588,
    "repo:lastModifiedDate": 1594941538433,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "5e8a5e508eb2ed344c08cb23ed27cfb60c841bec59a2f7513deda0f7af903021",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Deprecare un campo standard in uno schema {#standard}

I campi di classi standard, gruppi di campi e tipi di dati non possono essere deprecati direttamente. È invece possibile renderlo obsoleto nei singoli schemi che utilizzano queste risorse standard utilizzando un descrittore.

### Creare un descrittore di campo obsoleto {#create-descriptor}

Per creare un descrittore per i campi dello schema che desideri rendere obsoleti, invia una richiesta POST all&#39;endpoint `/tenant/descriptors`.

**Formato API**

```http
POST /tenant/descriptors
```

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:descriptorDeprecated",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/faxPhone"
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `@type` | Tipo di descrittore. Per un descrittore di campo obsoleto, questo valore deve essere impostato su `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | URI `$id` dello schema a cui si sta applicando il descrittore. |
| `xdm:sourceVersion` | Versione dello schema a cui si sta applicando il descrittore. Deve essere impostato su `1`. |
| `xdm:sourceProperty` | Percorso della proprietà all’interno dello schema a cui si sta applicando il descrittore. Se si desidera applicare il descrittore a più proprietà, è possibile fornire un elenco di percorsi sotto forma di array (ad esempio, `["/firstName", "/lastName"]`). |

**Risposta**

```json
{
    "@id": "d882b1202bac0ac71f1e31fbcd9afbcc37f364270186b4b3",
    "@type": "xdm:descriptorDeprecated",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/faxPhone",
    "imsOrg": "{IMS_ORG}",
    "version": "1",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production"
}
```

### Verifica il campo obsoleto {#verify-deprecation}

Dopo aver applicato il descrittore, è possibile verificare se il campo è stato dichiarato obsoleto cercando lo schema in questione utilizzando l&#39;intestazione `Accept` appropriata.

>[!NOTE]
>
>La visualizzazione di campi obsoleti quando si elencano gli schemi non è al momento supportata.

**Formato API**

```http
GET /tenant/schemas
```

**Richiesta**

Per includere informazioni sui campi obsoleti nella risposta API, è necessario impostare l&#39;intestazione `Accept` su `application/vnd.adobe.xed-deprecatefield+json; version=1`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-deprecatefield+json; version=1'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli dello schema, con il campo obsoleto contenente un valore `meta:status` di `deprecated`. La risposta di esempio seguente è stata troncata per motivi di spazio.

```json
"faxPhone": {
    "title": "Fax phone",
    "description": "Fax phone number.",
    "type": "object",
    "meta:xdmType": "object",
    "properties": {},
    "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
    "meta:xdmField": "xdm:faxPhone",
    "meta:status": "deprecated"
}
```

## Passaggi successivi

Questo documento illustra come rendere obsoleti i campi XDM utilizzando l’API Schema Registry. Per ulteriori informazioni sulla configurazione dei campi per le risorse personalizzate, consulta la guida su [definizione dei campi XDM nell&#39;API](./custom-fields-api.md). Per ulteriori informazioni sulla gestione dei descrittori, consulta la [guida dell&#39;endpoint descrittori](../api/descriptors.md).
