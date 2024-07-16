---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;data model;sampledata;sample data;rpc;
solution: Experience Platform
title: Endpoint API dati di esempio
description: L’endpoint /sampledata nell’API Schema Registry consente di generare dati di esempio mappati alla struttura di qualsiasi schema XDM esistente.
exl-id: 424d33ca-0624-4891-bf83-044ac2861579
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 2%

---

# Endpoint di dati di esempio

Per acquisire i dati in Adobe Experience Platform, il formato e la struttura dei dati devono essere conformi a uno schema Experience Data Model (XDM) esistente. A seconda della complessità dello schema per un particolare set di dati, può essere difficile determinare la forma esatta dei dati prevista dal set di dati al momento dell’acquisizione.

Utilizzando l&#39;endpoint `/sampledata` nell&#39;API [!DNL Schema Registry], puoi generare un oggetto di acquisizione di esempio per qualsiasi schema creato in precedenza.

## Introduzione

L&#39;endpoint utilizzato in questa guida fa parte dell&#39;[[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e per le informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

L&#39;endpoint dei dati di esempio fa parte delle chiamate di procedura remota (RPC) supportate da [!DNL Schema Registry]. A differenza di altri endpoint nell&#39;API [!DNL Schema Registry], gli endpoint RPC non richiedono intestazioni aggiuntive come `Accept` o `Content-Type` e non utilizzano un `CONTAINER_ID`. Devono invece utilizzare lo spazio dei nomi `/rpc`, come dimostrato nella chiamata API seguente.

## Recuperare i dati di esempio per uno schema

È possibile recuperare dati di esempio per qualsiasi schema all’interno della Libreria schemi specificando l’ID dello schema nel percorso di una richiesta GET all’endpoint.

**Formato API**

```http
GET /rpc/sampledata/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | `meta:altId` o `$id` con codifica URL dello schema per cui si desidera generare i dati di esempio. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente genera dati di esempio per uno schema Membri fedeltà.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/sampledata/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un oggetto dati di esempio per lo schema specificato.

```json
{
    "@id": "/uri-reference",
    "_{TENANT_ID}": {
        "favoriteHotel": "string",
        "loyalty": {
            "loyaltyId": "string",
            "loyaltyLevel": "string",
            "loyaltyPoints": 4862,
            "memberSince": "2018-11-12T20:20:39+00:00"
        }
    },
    "repo:createDate": "2004-10-23T12:00:00-06:00",
    "repo:modifyDate": "2004-10-23T12:00:00-06:00",
    "xdm:createdByBatchID": "/uri-reference",
    "xdm:faxPhone": {
        "xdm:extension": "string",
        "xdm:number": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:validity": "consistent"
    },
    "xdm:homeAddress": {
        "@id": "/uri-reference",
        "repo:createDate": "2004-10-23T12:00:00-06:00",
        "repo:modifyDate": "2004-10-23T12:00:00-06:00",
        "schema:description": "string",
        "schema:elevation": 31148.05,
        "schema:latitude": 29.25,
        "schema:longitude": -145.42,
        "xdm:city": "string",
        "xdm:country": "string",
        "xdm:countryCode": "US",
        "xdm:createdByBatchID": "/uri-reference",
        "xdm:dmaID": 1612,
        "xdm:label": "string",
        "xdm:lastVerifiedDate": "2018-01-12",
        "xdm:modifiedByBatchID": "/uri-reference",
        "xdm:msaID": 26375,
        "xdm:postOfficeBox": "string",
        "xdm:postalCode": "string",
        "xdm:primary": false,
        "xdm:region": "string",
        "xdm:repositoryCreatedBy": "string",
        "xdm:repositoryLastModifiedBy": "string",
        "xdm:state": "string",
        "xdm:stateProvince": "US-CA",
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:street1": "string",
        "xdm:street2": "string",
        "xdm:street3": "string",
        "xdm:street4": "string"
    },
    "xdm:homePhone": {
        "xdm:extension": "string",
        "xdm:number": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:validity": "consistent"
    },
    "xdm:identityMap": {
        "key": [
            {
                "xdm:authenticatedState": "ambiguous",
                "xdm:id": "string",
                "xdm:primary": false
            }
        ]
    },
    "xdm:mobilePhone": {
        "xdm:extension": "string",
        "xdm:number": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:validity": "consistent"
    },
    "xdm:modifiedByBatchID": "/uri-reference",
    "xdm:person": {
        "xdm:birthDate": "2018-01-12",
        "xdm:birthDayAndMonth": "01-23",
        "xdm:birthYear": 6427,
        "xdm:gender": "not_specified",
        "xdm:maritalStatus": "not_specified",
        "xdm:name": {
            "xdm:courtesyTitle": "string",
            "xdm:firstName": "string",
            "xdm:fullName": "string",
            "xdm:lastName": "string",
            "xdm:middleName": "string",
            "xdm:suffix": "string"
        },
        "xdm:nationality": "US",
        "xdm:taxId": "string"
    },
    "xdm:personalEmail": {
        "xdm:address": "john.smith@abc.com",
        "xdm:label": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:type": "unknown"
    },
    "xdm:repositoryCreatedBy": "string",
    "xdm:repositoryLastModifiedBy": "string"
}
```
