---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;Experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;schema registry;comportamento;comportamento;comportamenti;comportamenti;
solution: Experience Platform
title: Endpoint API per i comportamenti
description: L’endpoint /behaviors nell’API Schema Registry consente di recuperare tutti i comportamenti disponibili nel contenitore globale.
exl-id: 3b45431f-1d55-4279-8b62-9b27863885ec
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 3%

---

# Endpoint &quot;Behaviors&quot;

In Experience Data Model (XDM), i comportamenti definiscono la natura dei dati descritti da uno schema. Ogni classe XDM deve fare riferimento a un comportamento specifico che verrà ereditato da tutti gli schemi che utilizzano tale classe. Per quasi tutti i casi di utilizzo in Experience Platform, sono disponibili due comportamenti:

* **[!UICONTROL Record]**: fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.
* **[!UICONTROL Serie temporale]**: fornisce un&#39;istantanea del sistema nel momento in cui un oggetto record ha eseguito un&#39;azione direttamente o indirettamente.

>[!NOTE]
>
>In Experience Platform, in alcuni casi, è necessario utilizzare uno schema che non utilizza nessuno dei comportamenti di cui sopra. Per questi casi, è disponibile un terzo comportamento &quot;ad hoc&quot;. Per ulteriori informazioni, consulta il tutorial su [creazione di uno schema ad hoc](../tutorials/ad-hoc.md).
>
>Per informazioni più generali sui comportamenti dei dati in termini di influenza sulla composizione dello schema, consulta la guida sulle [nozioni di base sulla composizione dello schema](../schema/composition.md).

L&#39;endpoint `/behaviors` nell&#39;API [!DNL Schema Registry] consente di visualizzare i comportamenti disponibili nel contenitore `global`.

## Introduzione

L&#39;endpoint utilizzato in questa guida fa parte dell&#39;[[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e per le informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recuperare un elenco di comportamenti {#list}

Per recuperare un elenco di tutti i comportamenti disponibili, eseguire una richiesta GET all&#39;endpoint `/behaviors`.

**Formato API**

```http
GET /global/behaviors
```

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

**Risposta**

```json
{
    "results": [
        {
            "$id": "https://ns.adobe.com/xdm/data/record",
            "meta:altId": "_xdm.data.record",
            "version": "1.16.4",
            "title": "Record Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/adhoc",
            "meta:altId": "_xdm.data.adhoc",
            "version": "1.16.4",
            "title": "Ad Hoc Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/time-series",
            "meta:altId": "_xdm.data.time-series",
            "version": "1.16.4",
            "title": "Time-series Schema"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null
    }
}
```

## Cercare un comportamento {#lookup}

Per cercare un comportamento specifico, devi fornire il relativo ID nel percorso di una richiesta GET all&#39;endpoint `/behaviors`.

**Formato API**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{BEHAVIOR_ID}` | `meta:altId` o `$id` con codifica URL del comportamento da cercare. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente recupera i dettagli del comportamento del record fornendo il relativo `meta:altId` nel percorso della richiesta.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json;version=1'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del comportamento, inclusa la versione, la descrizione e gli attributi forniti dal comportamento alle classi che lo utilizzano.

```json
{
    "$id": "https://ns.adobe.com/xdm/data/record",
    "meta:altId": "_xdm.data.record",
    "meta:resourceType": "behaviors",
    "version": "1.16.4",
    "title": "Record Schema",
    "type": "object",
    "description": "Used to indicate the behavior of record data semantic when composed into data schemas.",
    "definitions": {
        "record": {
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "A unique identifier for the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/record",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:xdmType": "object",
    "meta:status": "stable",
    "$schema": "http://json-schema.org/draft-06/schema#",
    "meta:registryMetadata": {
        "repo:createdDate": 1606266789446,
        "repo:lastModifiedDate": 1606266789446,
        "eTag": "2cc114a54949a9668fe2ad046ccece59192e1bfa28f14e5ac7c893acb7820ba2",
        "meta:globalLibVersion": "1.16.4"
    }
}
```

## Passaggi successivi

Questa guida descrive l&#39;utilizzo dell&#39;endpoint `/behaviors` nell&#39;API [!DNL Schema Registry]. Per informazioni su come assegnare un comportamento a una classe utilizzando l&#39;API, consulta la [guida dell&#39;endpoint delle classi](./classes.md).
