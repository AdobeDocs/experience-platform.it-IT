---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;modello dati;registro schema;registro schema;comportamento;comportamenti;comportamenti;comportamenti;
solution: Experience Platform
title: Endpoint API per i comportamenti
description: L’endpoint /Behaviors nell’API del Registro di sistema dello schema consente di recuperare tutti i comportamenti disponibili nel contenitore globale.
topic-legacy: developer guide
exl-id: 3b45431f-1d55-4279-8b62-9b27863885ec
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 2%

---

# Endpoint di comportamento

In Experience Data Model (XDM), i comportamenti definiscono la natura dei dati descritti da uno schema. Ogni classe XDM deve fare riferimento a un comportamento specifico che tutti gli schemi che utilizzano tale classe erediteranno. Per quasi tutti i casi d’uso in Platform, sono disponibili due comportamenti:

* **[!UICONTROL Record]**: Fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.
* **[!UICONTROL Serie]** temporali: Fornisce un&#39;istantanea del sistema al momento in cui un&#39;azione è stata eseguita direttamente o indirettamente da un soggetto del record.

>[!NOTE]
>
>In Platform sono presenti alcuni casi d’uso che richiedono l’uso di uno schema che non utilizza nessuno dei comportamenti sopra descritti. Per questi casi, è disponibile un terzo comportamento &quot;ad hoc&quot;. Per ulteriori informazioni, consulta l’esercitazione su [creazione di uno schema ad-hoc](../tutorials/ad-hoc.md) .
>
>Per informazioni più generali sui comportamenti dei dati in termini di come influiscono sulla composizione dello schema, consulta la guida sulle [nozioni di base sulla composizione dello schema](../schema/composition.md).

L’endpoint `/behaviors` nell’ API [!DNL Schema Registry] ti consente di visualizzare i comportamenti disponibili nel contenitore `global` .

## Introduzione

L&#39;endpoint utilizzato in questa guida fa parte dell&#39; [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla relativa documentazione, una guida per la lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare chiamate a qualsiasi API di Experience Platform.

## Recupera un elenco di comportamenti {#list}

Puoi recuperare un elenco di tutti i comportamenti disponibili effettuando una richiesta di GET all’endpoint `/behaviors` .

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

Puoi cercare un comportamento specifico fornendo il relativo ID nel percorso di una richiesta di GET all’ `/behaviors` endpoint.

**Formato API**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{BEHAVIOR_ID}` | Il `meta:altId` o il codice URL `$id` del comportamento da cercare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta seguente recupera i dettagli del comportamento del record fornendo il relativo `meta:altId` nel percorso della richiesta.

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

Una risposta corretta restituisce i dettagli del comportamento, inclusa la relativa versione, descrizione e gli attributi forniti dal comportamento alle classi che lo utilizzano.

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

Questa guida descrive l’utilizzo dell’endpoint `/behaviors` nell’ API [!DNL Schema Registry] . Per informazioni su come assegnare un comportamento a una classe utilizzando l&#39;API, consulta la [guida all&#39;endpoint delle classi](./classes.md).
