---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;union;Union;unions;Unions;segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: Unioni
description: L'endpoint /sindacati nell'API del Registro di sistema dello schema consente di gestire in modo programmatico gli schemi unione XDM nell'applicazione dell'esperienza.
topic: developer guide
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 1%

---


# Endpoint Unions

Le unioni (o viste di unione) sono schemi generati dal sistema e di sola lettura che aggregano i campi di tutti gli schemi che condividono la stessa classe ([!DNL XDM ExperienceEvent] o [!DNL XDM Individual Profile]) e sono abilitati per [[!DNL Real-time Customer Profile]](../../profile/home.md).

Il presente documento illustra i concetti essenziali per l&#39;utilizzo dei sindacati nell&#39;API del Registro di sistema dello schema, incluse le chiamate di esempio per varie operazioni. Per informazioni più generali sui sindacati in XDM, vedere la sezione sui sindacati in [nozioni di base della composizione dello schema](../schema/composition.md#union).

## Campi dello schema unione

[!DNL Schema Registry] include automaticamente tre campi chiave in uno schema unione: `identityMap`, `timeSeriesEvents` e `segmentMembership`.

### Mappa identità

Un elemento `identityMap` dello schema unione è una rappresentazione delle identità note all&#39;interno degli schemi di record associati all&#39;unione. La mappa identità separa le identità in array diversi, chiave per namespace. Ogni identità elencata è essa stessa un oggetto contenente un valore `id` univoco. Per ulteriori informazioni, vedere la [documentazione del servizio identità](../../identity-service/home.md).

### Eventi serie temporali

L&#39;array `timeSeriesEvents` è un elenco di eventi delle serie temporali relativi agli schemi di record associati all&#39;unione. Quando i dati del profilo vengono esportati nei set di dati, questa matrice viene inclusa per ciascun record. Questa funzione è utile per diversi casi di utilizzo, ad esempio per l&#39;apprendimento automatico, in cui i modelli necessitano dell&#39;intera cronologia del comportamento di un profilo oltre agli attributi del record.

### Mappa appartenenza segmento

La mappa `segmentMembership` memorizza i risultati delle valutazioni dei segmenti. Quando i processi del segmento vengono eseguiti correttamente utilizzando l&#39;API [Segmentazione](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml), la mappa viene aggiornata. `segmentMembership` memorizza inoltre tutti i segmenti di pubblico già valutati che vengono trasferiti in Piattaforma, consentendo l&#39;integrazione con altre soluzioni come Adobe Audience Manager. Per ulteriori informazioni, consulta l&#39;esercitazione sulla [creazione di segmenti tramite API](../../segmentation/tutorials/create-a-segment.md).

## Recupera un elenco di unioni {#list}

Quando si imposta il tag `union` su uno schema, [!DNL Schema Registry] aggiunge automaticamente lo schema all&#39;unione per la classe su cui si basa lo schema. Se non esiste alcuna unione per la classe in questione, viene creata automaticamente una nuova unione. La `$id` dell&#39;unione è simile alla `$id` standard di altre risorse [!DNL Schema Registry], con l&#39;unica differenza aggiunta da due caratteri di sottolineatura e dalla parola &quot;unione&quot; (`__union`).

È possibile visualizzare un elenco di unioni disponibili effettuando una richiesta di GET all&#39;endpoint `/tenant/unions`.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

Il formato della risposta dipende dall&#39;intestazione `Accept` inviata nella richiesta. Le seguenti intestazioni `Accept` sono disponibili per l&#39;elenco delle unioni:

| `Accept` header | Descrizione |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Restituisce un breve riepilogo di ciascuna risorsa. Intestazione consigliata per elencare le risorse. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Restituisce la classe JSON completa per ogni risorsa, con `$ref` originale e `allOf` inclusi. (Limite: 300) |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 (OK) e un array `results` nel corpo della risposta. Se le unioni sono state definite, i dettagli di ciascuna unione vengono forniti come oggetti all&#39;interno dell&#39;array. Se non sono state definite unioni, lo stato HTTP 200 (OK) viene comunque restituito, ma l&#39;array `results` sarà vuoto.

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

## Cerca un&#39;unione {#lookup}

Potete visualizzare un&#39;unione specifica eseguendo una richiesta di GET che include `$id` e, a seconda dell&#39;intestazione Accetto, alcuni o tutti i dettagli dell&#39;unione.

>[!NOTE]
>
>Le ricerche dell&#39;unione sono disponibili utilizzando l&#39;endpoint `/unions` e `/schemas` per consentirne l&#39;utilizzo nelle esportazioni [!DNL Profile] in un dataset.

**Formato API**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{UNION_ID}` | L&#39;URI `$id` con codifica URL dell&#39;unione da cercare. Gli URI per gli schemi di unione vengono aggiunti con &quot;__union&quot;. |

**Richiesta**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

Le richieste di ricerca unionali richiedono l&#39;inclusione di un elemento `version` nell&#39;intestazione Accetto.

Le seguenti intestazioni Accetta sono disponibili per le ricerche dello schema unione:

| Accetta | Descrizione |
| -------|------------ |
| application/vnd.adobe.xed+json; version={MAJOR_VERSION} | Non elaborato con `$ref` e `allOf`. Include titoli e descrizioni. |
| application/vnd.adobe.xed-full+json; version={MAJOR_VERSION} | `$ref` e  `allOf` risolto. Include titoli e descrizioni. |

**Risposta**

Una risposta corretta restituisce la visualizzazione unione di tutti gli schemi che implementano la classe di cui `$id` è stato fornito nel percorso della richiesta.

Il formato della risposta dipende dall’intestazione Accetta inviata nella richiesta. Provate con diverse intestazioni Accetta per confrontare le risposte e determinare quale intestazione è più adatta all’uso da parte dell’utente.

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

## Abilita uno schema per l&#39;appartenenza all&#39;unione {#enable}

Affinché uno schema possa essere incluso nell&#39;unione per la relativa classe, è necessario aggiungere un tag `union` all&#39;attributo `meta:immutableTags` dello schema. A tal fine, è possibile effettuare una richiesta di PATCH per aggiungere allo schema in questione un array `meta:immutableTags` con un singolo valore di stringa `union`. Per un esempio dettagliato, vedere la [guida dell&#39;endpoint degli schemi](./schemas.md#union).

## Elenca gli schemi in un&#39;unione {#list-schemas}

Per vedere quali schemi fanno parte di un&#39;unione specifica, potete eseguire una richiesta di GET all&#39;endpoint `/tenant/schemas`. Utilizzando il parametro di query `property`, potete configurare la risposta solo per gli schemi di restituzione contenenti un campo `meta:immutableTags` e un `meta:class` uguale alla classe a cui state accedendo.

**Formato API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CLASS_ID}` | Il `$id` della classe di cui si desidera elencare gli schemi abilitati per l&#39;unione. |

**Richiesta**

La richiesta seguente recupera un elenco di tutti gli schemi che fanno parte dell&#39;unione per la classe [!DNL XDM Individual Profile].

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dall&#39;intestazione `Accept` inviata nella richiesta. Per elencare gli schemi sono disponibili le seguenti intestazioni `Accept`:

| `Accept` header | Descrizione |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Restituisce un breve riepilogo di ciascuna risorsa. Intestazione consigliata per elencare le risorse. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Restituisce lo schema JSON completo per ogni risorsa, con `$ref` originale e `allOf` inclusi. (Limite: 300) |

**Risposta**

Una risposta corretta restituisce un elenco filtrato di schemi, contenente solo quelli appartenenti alla classe specificata che sono stati abilitati per l&#39;appartenenza all&#39;unione. Tenere presente che quando si utilizzano più parametri di query, viene considerata una relazione AND.

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
