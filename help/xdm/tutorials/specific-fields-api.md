---
title: Aggiungere campi specifici a uno schema utilizzando l’API Schema Registry
description: Scopri come aggiungere singoli campi da gruppi di campi preesistenti a uno schema Experience Data Model (XDM) utilizzando l’API Schema Registry.
source-git-commit: 4bcd949e901c11bb933000f7ae76f17134dda496
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 2%

---

# Aggiungere campi specifici a uno schema utilizzando l’API Schema Registry

Gli schemi Experience Data Model (XDM) sono composti da una classe base, con campi aggiuntivi inclusi tramite l’utilizzo di gruppi di campi standard definiti da Adobe e di gruppi di campi personalizzati definiti dalla tua organizzazione.

Durante la creazione di uno schema, è possibile utilizzare alcuni campi di un determinato gruppo di campi escludendo altri dallo stesso gruppo che non sono necessari. Questa esercitazione mostra come aggiungere singoli campi da un gruppo di campi a uno schema utilizzando l’API Schema Registry.

>[!NOTE]
>
>Per informazioni su come aggiungere e rimuovere singoli campi schema nell’interfaccia utente di Adobe Experience Platform, consulta la guida su [flussi di lavoro basati sui campi](../ui/field-based-workflows.md) (attualmente in versione beta).

## Prerequisiti

Questo tutorial prevede l’esecuzione di chiamate al [API del registro dello schema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Prima di iniziare, controlla [guida per sviluppatori](../api/getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate all’API, tra cui `{TENANT_ID}`, il concetto di contenitori e le intestazioni necessarie per effettuare le richieste.

## Comprensione di `meta:refProperty` campo

Per uno schema specifico, la classe e i gruppi di campi che compongono la sua struttura sono referenziati nel relativo `allOf` array. Ogni componente è rappresentato come un oggetto contenente un `$ref` proprietà che fa riferimento all&#39;URI del componente `$id`.

Il seguente codice JSON rappresenta uno schema semplificato che utilizza una singola classe (`experienceevent`) e gruppo di campi (`experienceevent-all`):

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

Per qualsiasi oggetto in `allOf` matrice che fa riferimento a un gruppo di campi, è possibile aggiungere un elemento di pari livello `meta:refProperty` per specificare quali campi del gruppo devono essere inclusi nello schema.

>[!NOTE]
>
>Ogni campo viene specificato utilizzando una stringa puntatore JSON che rappresenta il percorso del campo all’interno del rispettivo gruppo di campi. La stringa deve iniziare con una barra iniziale (`/`) e non devono includere `properties` spazi dei nomi. Ad esempio: `/_experience/campaign/message/id`.

Se inclusa come stringa, `meta:refProperty` può fare riferimento a un singolo campo in un gruppo. È possibile includere altri campi dello stesso gruppo utilizzando lo stesso `$ref` valore in un altro oggetto con un diverso `meta:refProperty` valore.

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

In alternativa: `meta:refProperty` può essere fornito come array, consentendo di specificare più campi da includere da un dato gruppo all’interno di un singolo `allOf` voce di elenco:

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

Puoi utilizzare una richiesta PUT per riscrivere un intero schema e configurare i campi da includere in `allOf`.

**Formato API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | Il `meta:altId` o con codifica URL `$id` dello schema che desideri riscrivere. |

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
>Per informazioni più dettagliate sulle richieste PUT di schemi, consulta [guida all’endpoint degli schemi](../api/schemas.md#put).

## Aggiungere campi con un’operazione PATCH

È possibile utilizzare una richiesta PATCH per aggiungere singoli campi a uno schema senza sovrascriverne altri. Il registro dello schema supporta tutte le operazioni Patch JSON standard, tra cui `add`, `remove`, e `replace`. Per ulteriori informazioni sulla patch JSON, vedi [Guida di base sulle API](../../landing/api-fundamentals.md#json-patch).

**Formato API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | Il `meta:altId` o con codifica URL `$id` dello schema che desideri riscrivere. |

**Richiesta**

La richiesta seguente aggiunge un nuovo oggetto al file dello schema `allOf` , specificando i campi da aggiungere.

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
>Per informazioni più dettagliate sulle richieste PATCH di schemi, consulta [guida all’endpoint degli schemi](../api/schemas.md#patch).

## Passaggi successivi

Questa guida illustra come utilizzare le chiamate API per aggiungere singoli campi da un gruppo di campi esistente a uno schema. Per informazioni dettagliate su come eseguire attività simili basate sui campi nell’interfaccia utente di Platform, consulta la guida su [flussi di lavoro basati sui campi](../ui/field-based-workflows.md).

Per ulteriori informazioni sulle funzionalità dell’API Schema Registry, consulta [Panoramica API](../api/overview.md) per un elenco completo degli endpoint e dei processi.
