---
title: Aggiungere campi specifici a uno schema utilizzando l’API Schema Registry
description: Scopri come aggiungere singoli campi da gruppi di campi preesistenti a uno schema Experience Data Model (XDM) utilizzando l’API Schema Registry.
exl-id: 696cce2b-bbde-416a-9f52-12ab4da9c2c6
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 2%

---

# Aggiungere campi specifici a uno schema utilizzando l’API Schema Registry

Gli schemi Experience Data Model (XDM) sono composti da una classe base, con campi aggiuntivi inclusi tramite l’utilizzo di gruppi di campi standard definiti da Adobe e di gruppi di campi personalizzati definiti dalla tua organizzazione.

Durante la creazione di uno schema, è possibile utilizzare alcuni campi di un determinato gruppo di campi escludendo altri dallo stesso gruppo che non sono necessari. Questa esercitazione mostra come aggiungere singoli campi da un gruppo di campi a uno schema utilizzando l’API Schema Registry.

>[!NOTE]
>
>Per informazioni su come aggiungere e rimuovere singoli campi dello schema nell&#39;interfaccia utente di Adobe Experience Platform, consulta la guida sui [flussi di lavoro basati sui campi](../ui/field-based-workflows.md) (attualmente in versione beta).

## Prerequisiti

Questo tutorial prevede l&#39;esecuzione di chiamate all&#39;API [Schema Registry](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Prima di iniziare, consulta la [guida per gli sviluppatori](../api/getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, tra cui `{TENANT_ID}`, il concetto di contenitori e le intestazioni necessarie per effettuare le richieste.

## Informazioni sul campo `meta:refProperty`

Per uno schema specifico, la classe e i gruppi di campi che ne costituiscono la struttura fanno riferimento al suo array `allOf`. Ogni componente è rappresentato come un oggetto contenente una proprietà `$ref` che fa riferimento all&#39;URI del componente `$id`.

Il seguente JSON rappresenta uno schema semplificato che utilizza una singola classe (`experienceevent`) e un gruppo di campi (`experienceevent-all`):

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

Per qualsiasi oggetto nell&#39;array `allOf` che fa riferimento a un gruppo di campi, è possibile aggiungere un campo di pari livello `meta:refProperty` per specificare quali campi del gruppo devono essere inclusi nello schema.

>[!NOTE]
>
>Ogni campo viene specificato utilizzando una stringa puntatore JSON che rappresenta il percorso del campo all’interno del rispettivo gruppo di campi. La stringa deve iniziare con una barra iniziale (`/`) e non deve includere spazi dei nomi `properties`. Esempio: `/_experience/campaign/message/id`.

Se incluso come stringa, `meta:refProperty` può fare riferimento a un singolo campo in un gruppo. È possibile includere altri campi dello stesso gruppo utilizzando lo stesso valore `$ref` in un altro oggetto con un valore `meta:refProperty` diverso.

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

In alternativa, è possibile fornire `meta:refProperty` come array, consentendo di specificare più campi da includere da un determinato gruppo all&#39;interno di una singola voce di elenco `allOf`:

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

## Aggiungere campi con un’operazione PUT

È possibile utilizzare una richiesta PUT per riscrivere un intero schema e configurare i campi da includere in `allOf`.

**Formato API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | `meta:altId` o `$id` con codifica URL dello schema che si desidera riscrivere. |

**Richiesta**

La richiesta seguente aggiorna i campi specifici inclusi dal gruppo di campi nell&#39;array `allOf`.

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

In caso di esito positivo, la risposta restituisce i dettagli dello schema aggiornato.

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
>Per informazioni più dettagliate sulle richieste PUT per gli schemi, consulta la [guida dell&#39;endpoint Schemas](../api/schemas.md#put).

## Aggiungere campi con un’operazione PATCH

È possibile utilizzare una richiesta PATCH per aggiungere singoli campi a uno schema senza sovrascriverne altri. Il registro dello schema supporta tutte le operazioni Patch JSON standard, inclusi `add`, `remove` e `replace`. Per ulteriori informazioni sulla patch JSON, consulta la [guida delle API fondamentali](../../landing/api-fundamentals.md#json-patch).

**Formato API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | `meta:altId` o `$id` con codifica URL dello schema che si desidera riscrivere. |

**Richiesta**

La richiesta seguente aggiunge un nuovo oggetto all&#39;array `allOf` dello schema, specificando i campi da aggiungere.

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

In caso di esito positivo, la risposta restituisce i dettagli dello schema aggiornato.

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
>Per informazioni più dettagliate sulle richieste PATCH per gli schemi, consulta la [guida dell&#39;endpoint Schemas](../api/schemas.md#patch).

## Passaggi successivi

Questa guida illustra come utilizzare le chiamate API per aggiungere singoli campi da un gruppo di campi esistente a uno schema. Per informazioni dettagliate su come eseguire attività simili basate sui campi nell&#39;interfaccia utente di Platform, consulta la guida sui [flussi di lavoro basati sui campi](../ui/field-based-workflows.md).

Per ulteriori informazioni sulle funzionalità dell&#39;API Schema Registry, fare riferimento alla [panoramica API](../api/overview.md) per un elenco completo degli endpoint e dei processi.
