---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;XDM system;Experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;schema Registry;union;unioni;unioni;segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: Endpoint API Unions
description: L’endpoint /unions nell’API Schema Registry consente di gestire in modo programmatico gli schemi di unione XDM nell’applicazione Experience.
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
source-git-commit: 3da2e8f66f08a7bb9533795f7854ad583734911c
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 2%

---

# Endpoint Unions

Le unioni (o le visualizzazioni unione) sono schemi di sola lettura generati dal sistema che aggregano i campi di tutti gli schemi che condividono la stessa classe ([!DNL XDM ExperienceEvent] o [!DNL XDM Individual Profile]) e sono abilitati per [[!DNL Real-Time Customer Profile]](../../profile/home.md).

Questo documento descrive i concetti essenziali per l’utilizzo delle unioni nell’API del registro dello schema, inclusi gli esempi di chiamate per varie operazioni. Per informazioni più generali sulle unioni in XDM, consulta la sezione sulle unioni nelle [nozioni di base sulla composizione dello schema](../schema/composition.md#union).

## Campi schema di unione

[!DNL Schema Registry] include automaticamente tre campi chiave in uno schema di unione: `identityMap`, `timeSeriesEvents` e `segmentMembership`.

### Mappa identità

`identityMap` di uno schema di unione è una rappresentazione delle identità note all&#39;interno degli schemi di record associati dell&#39;unione. La mappa delle identità separa le identità in array diversi in base allo spazio dei nomi. Ogni identità elencata è essa stessa un oggetto contenente un valore `id` univoco. Per ulteriori informazioni, consulta la [documentazione del servizio Identity](../../identity-service/home.md).

### Eventi di serie temporali

L&#39;array `timeSeriesEvents` è un elenco di eventi di serie temporali correlati agli schemi di record associati all&#39;unione. Quando i dati di profilo vengono esportati in set di dati, questo array viene incluso per ogni record. Ciò è utile per vari casi d’uso, come l’apprendimento automatico in cui i modelli richiedono l’intera cronologia del comportamento di un profilo, oltre agli attributi record.

### Mappa di appartenenza al segmento

La mappa `segmentMembership` memorizza i risultati della valutazione di una definizione di segmento. Quando i processi di segmentazione vengono eseguiti correttamente utilizzando l&#39;[API di segmentazione](https://www.adobe.io/experience-platform-apis/references/segmentation/), la mappa viene aggiornata. `segmentMembership` memorizza anche eventuali tipi di pubblico pre-valutati che vengono acquisiti in Platform, consentendo l&#39;integrazione con altre soluzioni come Adobe Audience Manager. Per ulteriori informazioni, consulta l&#39;esercitazione sulla [creazione di tipi di pubblico tramite API](../../segmentation/tutorials/create-a-segment.md).

## Recuperare un elenco di unioni {#list}

Quando si imposta il tag `union` su uno schema, [!DNL Schema Registry] aggiunge automaticamente lo schema all&#39;unione per la classe su cui si basa lo schema. Se non esiste alcuna unione per la classe in questione, viene creata automaticamente una nuova unione. `$id` per l&#39;unione è simile allo standard `$id` di altre risorse [!DNL Schema Registry], con l&#39;unica differenza che è seguito da due trattini bassi e dalla parola &quot;unione&quot; (`__union`).

È possibile visualizzare un elenco di unioni disponibili effettuando una richiesta GET all&#39;endpoint `/tenant/unions`.

**Formato API**

```http
GET /tenant/unions
```

**Richiesta**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

Il formato della risposta dipende dall&#39;intestazione `Accept` inviata nella richiesta. Le seguenti intestazioni di `Accept` sono disponibili per l&#39;elenco dei sindacati:

| Intestazione `Accept` | Descrizione |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Restituisce un breve riepilogo di ciascuna risorsa. Questa è l’intestazione consigliata per l’elenco delle risorse. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Restituisce la classe JSON completa per ogni risorsa, inclusi `$ref` e `allOf` originali. (Limite: 300) |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 (OK) e un array `results` nel corpo della risposta. Se sono state definite unioni, i dettagli di ogni unione vengono forniti come oggetti all’interno dell’array. Se non è stata definita alcuna unione, viene comunque restituito lo stato HTTP 200 (OK) ma l&#39;array `results` sarà vuoto.

```JSON
{
    "results": [
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile__union",
            "meta:altId": "_xdm.context.profile__union",
            "version": "1"
        },
        {
            "title": "Property",
            "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590__union",
            "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590__union",
            "version": "1"
        }
    ]
}
```

## Cercare un’unione {#lookup}

È possibile visualizzare un&#39;unione specifica eseguendo una richiesta di GET che includa `$id` e, a seconda dell&#39;intestazione Accept, alcuni o tutti i dettagli dell&#39;unione.

>[!NOTE]
>
>Le ricerche di unione sono disponibili utilizzando l&#39;endpoint `/unions` e `/schemas` per consentirne l&#39;utilizzo in [!DNL Profile] esportazioni in un set di dati.

**Formato API**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{UNION_ID}` | URI `$id` con codifica URL dell&#39;unione da cercare. Agli URI per gli schemi di unione viene aggiunto &quot;__union&quot;. |

{style="table-layout:auto"}

**Richiesta**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

Le richieste di ricerca unione richiedono l&#39;inclusione di `version` nell&#39;intestazione Accept.

Per le ricerche dello schema di unione sono disponibili le seguenti intestazioni Accept:

| Accetta | Descrizione |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | Raw con `$ref` e `allOf`. Include titoli e descrizioni. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` attributi e `allOf` risolti. Include titoli e descrizioni. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce la visualizzazione unione di tutti gli schemi che implementano la classe di cui è stato fornito `$id` nel percorso della richiesta.

Il formato della risposta dipende dall’intestazione Accept inviata nella richiesta. Prova a confrontare le risposte con diverse intestazioni Accept e a determinare quale sia la migliore per il tuo caso d’uso.

```JSON
{
    "type": "object",
    "description": "Union view of all schemas that extend https://ns.adobe.com/xdm/context/profile",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        }
    ],
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "title": "Union object for https://ns.adobe.com/xdm/context/profile",
    "$id": "https://ns.adobe.com/xdm/context/profile__union",
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:altId": "_xdm.context.profile__union",
    "version": "1.0",
    "meta:resourceType": "unions",
    "meta:registryMetadata": {}
}
```

## Abilita uno schema per l’iscrizione all’unione {#enable}

Per includere uno schema nell&#39;unione per la relativa classe, è necessario aggiungere un tag `union` all&#39;attributo `meta:immutableTags` dello schema. A tale scopo, è possibile eseguire una richiesta PATCH per aggiungere un array `meta:immutableTags` con un singolo valore stringa di `union` allo schema in questione. Per un esempio dettagliato, consulta la [guida dell&#39;endpoint degli schemi](./schemas.md#union).

## Elencare schemi in un’unione {#list-schemas}

Per vedere quali schemi fanno parte di un&#39;unione specifica, è possibile eseguire una richiesta GET all&#39;endpoint `/tenant/schemas`. Utilizzando il parametro di query `property`, puoi configurare la risposta in modo che restituisca solo schemi contenenti un campo `meta:immutableTags` e un `meta:class` uguali alla classe di cui stai accedendo all&#39;unione.

**Formato API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CLASS_ID}` | `$id` della classe di cui si desidera elencare gli schemi abilitati per l&#39;unione. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente recupera un elenco di tutti gli schemi che fanno parte dell&#39;unione per la classe [!DNL XDM Individual Profile].

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dall&#39;intestazione `Accept` inviata nella richiesta. Le seguenti intestazioni `Accept` sono disponibili per gli schemi di elenco:

| Intestazione `Accept` | Descrizione |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Restituisce un breve riepilogo di ciascuna risorsa. Questa è l’intestazione consigliata per l’elenco delle risorse. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Restituisce lo schema JSON completo per ogni risorsa, con `$ref` e `allOf` originali inclusi. (Limite: 300) |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco filtrato di schemi, contenente solo quelli che appartengono alla classe specificata e che sono stati abilitati per l’appartenenza all’unione. Tieni presente che quando utilizzi più parametri di query, viene assunta una relazione AND.

```JSON
{
    "results": [
        {
            "title": "Schema 1",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "meta:altId": "_{TENANT_ID}.schemas.142afb78d8b368a5ba97a6cc8fc7e033",
            "version": "1.2"
        },
        {
            "title": "Schema 2",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e7297a6ddfc7812ab3a7b504a1ab98da",
            "meta:altId": "_{TENANT_ID}.schemas.e7297a6ddfc7812ab3a7b504a1ab98da",
            "version": "1.5"
        },
        {
            "title": "Schema 3",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/50f960bb810e99a21737254866a477bf",
            "meta:altId": "_{TENANT_ID}.schemas.50f960bb810e99a21737254866a477bf",
            "version": "1.2"
        },
        {
            "title": "Schema 4",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/a39655ca8ea3d5c1f36a463b45fccca8",
            "meta:altId": "_{TENANT_ID}.schemas.a39655ca8ea3d5c1f36a463b45fccca8",
            "version": "1.1"
        },
        {
            "title": "Schema 5",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/c063fac45c6d6285ef33b0e2af09f633",
            "meta:altId": "_{TENANT_ID}.schemas.c063fac45c6d6285ef33b0e2af09f633",
            "version": "1.2"
        },
        {
            "title": "Schema 6",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/dfebb19b93827b70bbad006137812537",
            "meta:altId": "_{TENANT_ID}.schemas.dfebb19b93827b70bbad006137812537",
            "version": "1.7"
        }
    ],
    "_links": {
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
        }
    }
}
```
