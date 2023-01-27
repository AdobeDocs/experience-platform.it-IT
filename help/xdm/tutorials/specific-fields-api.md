---
title: Aggiunta di campi specifici a uno schema tramite l’API del Registro di sistema dello schema
description: Scopri come aggiungere singoli campi da gruppi di campi preesistenti a uno schema Experience Data Model (XDM) utilizzando l’API del Registro di sistema dello schema.
source-git-commit: 4bcd949e901c11bb933000f7ae76f17134dda496
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 2%

---

# Aggiunta di campi specifici a uno schema tramite l’API del Registro di sistema dello schema

Gli schemi Experience Data Model (XDM) sono composti da una classe base, con campi aggiuntivi inclusi tramite l’uso di gruppi di campi standard definiti dai gruppi di campi Adobi e personalizzati definiti dall’organizzazione.

Quando si crea uno schema, è possibile utilizzare alcuni campi di un determinato gruppo di campi escludendo altri dallo stesso gruppo di cui non si ha bisogno. Questa esercitazione mostra come aggiungere singoli campi da un gruppo di campi a uno schema utilizzando l&#39;API del Registro di sistema dello schema.

>[!NOTE]
>
>Per informazioni su come aggiungere e rimuovere singoli campi di schema nell’interfaccia utente di Adobe Experience Platform, consulta la guida in [flussi di lavoro basati sul campo](../ui/field-based-workflows.md) (attualmente in versione beta).

## Prerequisiti

Questa esercitazione prevede l’esecuzione di chiamate al [API del Registro di sistema dello schema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Prima di iniziare, controlla la [guida per sviluppatori](../api/getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, tra cui la `{TENANT_ID}`, il concetto di contenitori e le intestazioni richieste per effettuare richieste.

## Informazioni sulla `meta:refProperty` field

Per qualsiasi schema specifico, i gruppi di classi e campi che ne compongono la struttura sono indicati nei relativi riferimenti `allOf` array. Ciascun componente è rappresentato come un oggetto contenente un `$ref` che fa riferimento all&#39;URI del componente `$id`.

Il seguente JSON rappresenta uno schema semplificato che utilizza una singola classe (`experienceevent`) e gruppo di campi (`experienceevent-all`):

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all"
    }
  ]
}
```

Per qualsiasi oggetto nel `allOf` array che fa riferimento a un gruppo di campi, è possibile aggiungere un elemento di pari livello `meta:refProperty` campo per specificare quali campi del gruppo devono essere inclusi nello schema.

>[!NOTE]
>
>Ogni campo viene specificato utilizzando una stringa puntatore JSON che rappresenta il percorso del campo all’interno del rispettivo gruppo di campi. La stringa deve iniziare con una barra (`/`) e non deve includere `properties` spazi dei nomi. Ad esempio: `/_experience/campaign/message/id`.

Se incluso come stringa, `meta:refProperty` può fare riferimento a un singolo campo in un gruppo. Altri campi dello stesso gruppo possono essere inclusi utilizzando lo stesso `$ref` in un altro oggetto con un valore diverso `meta:refProperty` valore.

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/id"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/size"
    }
  ]
}
```

In alternativa, `meta:refProperty` può essere fornito come array, consentendo di specificare più campi da includere da un determinato gruppo in un singolo `allOf` voce di elenco:

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ]
}
```

## Aggiunta di campi tramite un’operazione PUT

È possibile utilizzare una richiesta di PUT per riscrivere un intero schema e configurare i campi che si desidera includere in `allOf`.

**Formato API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | La `meta:altId` o con codifica URL `$id` dello schema che si desidera riscrivere. |

**Richiesta**

La richiesta seguente aggiorna i campi specifici inclusi nel gruppo di campi sotto `allOf` array.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "title": "My Sample Schema",
        "description": "My Sample Description",
        "type": "object",
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
          },
          {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        ]
      }'
```

**Risposta**

Una risposta corretta restituisce i dettagli dello schema aggiornato.

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>Per informazioni più dettagliate sulle richieste di schemi di PUT, consulta [guida all’endpoint degli schemi](../api/schemas.md#put).

## Aggiunta di campi tramite un’operazione PATCH

È possibile utilizzare una richiesta di PATCH per aggiungere singoli campi a uno schema senza sovrascrivere altri campi. Il Registro di sistema dello schema supporta tutte le operazioni standard di patch JSON, tra cui `add`, `remove`e `replace`. Per ulteriori informazioni sulla patch JSON, consulta la sezione [Guida di base sulle API](../../landing/api-fundamentals.md#json-patch).

**Formato API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | La `meta:altId` o con codifica URL `$id` dello schema che si desidera riscrivere. |

**Richiesta**

La richiesta seguente aggiunge un nuovo oggetto al `allOf` array, specifica dei campi da aggiungere.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        }
      ]'
```

**Risposta**

Una risposta corretta restituisce i dettagli dello schema aggiornato.

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>Per informazioni più dettagliate sulle richieste di schemi di PATCH, consulta [guida all’endpoint degli schemi](../api/schemas.md#patch).

## Passaggi successivi

Questa guida illustra come utilizzare le chiamate API per aggiungere a uno schema singoli campi da un gruppo di campi esistente. Per informazioni dettagliate su come eseguire attività simili basate su campi nell’interfaccia utente di Platform, consulta la guida su [flussi di lavoro basati sul campo](../ui/field-based-workflows.md).

Per ulteriori informazioni sulle funzionalità dell&#39;API del Registro di sistema dello schema, consulta [Panoramica API](../api/overview.md) per un elenco completo degli endpoint e dei processi.
