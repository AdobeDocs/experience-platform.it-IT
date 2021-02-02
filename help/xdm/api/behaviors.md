---
keywords: ' Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;schema di registro;schema Registro di sistema;comportamento;comportamenti;comportamenti;comportamenti;comportamenti;'
solution: Experience Platform
title: Guida all'endpoint dei comportamenti
description: L'endpoint /Behaviors nell'API del Registro di sistema dello schema consente di recuperare tutti i comportamenti disponibili nel contenitore globale.
topic: developer guide
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 2%

---


# Endpoint di comportamento

In Experience Data Model (XDM), i comportamenti definiscono la natura dei dati descritti da uno schema. Ogni classe XDM deve fare riferimento a un comportamento specifico che tutti gli schemi che utilizzano tale classe erediteranno. Per quasi tutti i casi di utilizzo in Piattaforma, sono disponibili due comportamenti:

* **[!UICONTROL Record]**: Fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.
* **[!UICONTROL Time-series]**: Fornisce un&#39;istantanea del sistema al momento in cui un&#39;azione è stata eseguita direttamente o indirettamente da un soggetto del record.

>[!NOTE]
>
>In alcuni casi di utilizzo in Piattaforma è richiesto l&#39;uso di uno schema che non utilizza nessuno dei due comportamenti indicati. Per questi casi, è disponibile un terzo comportamento &quot;ad hoc&quot;. Per ulteriori informazioni, vedere l&#39;esercitazione su [creazione di uno schema ad hoc](../tutorials/ad-hoc.md).
>
>Per informazioni più generali sui comportamenti dei dati in termini di impatto sulla composizione dello schema, fare riferimento alla guida sulle [nozioni di base della composizione dello schema](../schema/composition.md).

L&#39;endpoint `/behaviors` nell&#39;API [!DNL Schema Registry] consente di visualizzare i comportamenti disponibili nel contenitore `global`.

## Introduzione

L&#39;endpoint utilizzato in questa guida fa parte dell&#39; [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). Prima di continuare, consultare la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni richieste necessarie per eseguire correttamente chiamate a qualsiasi API  Experience Platform.

## Recupera un elenco di comportamenti {#list}

È possibile recuperare un elenco di tutti i comportamenti disponibili effettuando una richiesta di GET all&#39;endpoint `/behaviors`.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Puoi cercare un comportamento specifico inserendo il relativo ID nel percorso di una richiesta di GET all&#39;endpoint `/behaviors`.

**Formato API**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{BEHAVIOR_ID}` | Il `meta:altId` o l&#39;URL-encoded `$id` del comportamento da ricercare. |

**Richiesta**

La richiesta seguente recupera i dettagli del comportamento del record fornendo la relativa `meta:altId` nel percorso della richiesta.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json;version=1'
```

**Risposta**

Una risposta corretta restituisce i dettagli del comportamento, inclusa la versione, la descrizione e gli attributi forniti dal comportamento alle classi che lo utilizzano.

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

Questa guida riguardava l&#39;utilizzo dell&#39;endpoint `/behaviors` nell&#39;API [!DNL Schema Registry]. Per informazioni su come assegnare un comportamento a una classe utilizzando l&#39;API, vedere la guida [endpoint classi](./classes.md).