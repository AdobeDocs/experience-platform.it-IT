---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Unioni
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 1%

---


# Unioni

Le unioni (o viste di unione) sono schemi generati dal sistema e di sola lettura che aggregano i campi di tutti gli schemi che condividono la stessa classe ([!DNL XDM ExperienceEvent] o [!DNL XDM Individual Profile]) e sono abilitati per [!DNL Real-time Customer Profile](../../profile/home.md).

Il presente documento illustra i concetti essenziali per l&#39;utilizzo dei sindacati nell&#39;API del Registro di sistema dello schema, incluse le chiamate di esempio per varie operazioni. Per informazioni più generali sulle unioni in XDM, consultate la sezione sui sindacati nelle [nozioni di base della composizione](../schema/composition.md#union)dello schema.

## Unione

Include [!DNL Schema Registry] automaticamente tre mixin nello schema unione: `identityMap`, `timeSeriesEvents`e `segmentMembership`.

### Mappa identità

Uno schema unione `identityMap` è una rappresentazione delle identità note all&#39;interno degli schemi di record associati all&#39;unione. La mappa identità separa le identità in array diversi, chiave per namespace. Ogni identità elencata è essa stessa un oggetto contenente un `id` valore univoco.

See the [Identity Service documentation](../../identity-service/home.md) for more information.

### Eventi serie temporali

L&#39; `timeSeriesEvents` array è un elenco di eventi delle serie temporali relativi agli schemi di record associati all&#39;unione. Quando [!DNL Profile] i dati vengono esportati in set di dati, questa matrice viene inclusa per ciascun record. Questa funzione è utile per diversi casi di utilizzo, ad esempio per l&#39;apprendimento automatico, in cui i modelli necessitano dell&#39;intera cronologia del comportamento di un profilo oltre agli attributi del record.

### Mappa appartenenza segmento

La `segmentMembership` mappa memorizza i risultati delle valutazioni dei segmenti. Quando i processi del segmento vengono eseguiti correttamente tramite l&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)Segmentazione, la mappa viene aggiornata. `segmentMembership` memorizza inoltre tutti i segmenti di pubblico già valutati che vengono trasferiti in Platform, consentendo l&#39;integrazione con altre soluzioni come  Adobe Audience Manager.

Per ulteriori informazioni, consulta l’esercitazione sulla [creazione di segmenti tramite API](../../segmentation/tutorials/create-a-segment.md) .

## Abilita uno schema per l&#39;appartenenza a un&#39;unione

Affinché uno schema possa essere incluso nella visualizzazione unione unita, è necessario aggiungere il tag &quot;unione&quot; all&#39; `meta:immutableTags` attributo dello schema. Questa operazione viene eseguita tramite una richiesta di PATCH per aggiornare lo schema e aggiungere l&#39; `meta:immutableTags` array con il valore &quot;union&quot;.

>[!NOTE]
>
>I tag immutabili sono tag destinati a essere impostati ma non rimossi.

**Formato API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | L&#39; `$id` URI con codifica URL o `meta:altId` dello schema che si desidera abilitare per l&#39;uso in [!DNL Profile]. |

**Richiesta**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/meta:immutableTags", "value": ["union"]}
      ]'
```

**Risposta**

Una risposta corretta restituisce i dettagli dello schema aggiornato, che ora include una `meta:immutableTags` matrice contenente il valore stringa &quot;union&quot;.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.2",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552091263267,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Elenca unioni

Quando si imposta il tag &quot;union&quot; su uno schema, viene creata e mantenuta [!DNL Schema Registry] automaticamente un&#39;unione per la classe su cui si basa lo schema. Il `$id` nome dell&#39;unione è simile allo standard `$id` di una classe, con l&#39;unica differenza che è aggiunta da due caratteri di sottolineatura e la parola &quot;unione&quot; (`"__union"`).

Per visualizzare un elenco delle unioni disponibili, potete eseguire una richiesta di GET all&#39; `/unions` endpoint.

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

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 (OK) e un `results` array nel corpo della risposta. Se le unioni sono state definite, le `title`, `$id`, `meta:altId`e `version` per ciascuna unione vengono fornite come oggetti all&#39;interno della matrice. Se non sono state definite unioni, lo stato HTTP 200 (OK) viene comunque restituito, ma la `results` matrice sarà vuota.

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

## Cercare una specifica unione

Potete visualizzare un&#39;unione specifica eseguendo una richiesta di GET che include alcuni o tutti i dettagli dell&#39;unione, a seconda dell&#39;intestazione Accetto `$id` .

>[!NOTE]
>
>Le ricerche unionali sono disponibili utilizzando l&#39; `/unions` endpoint e `/schemas` per consentirne l&#39;utilizzo nelle [!DNL Profile] esportazioni in un dataset.

**Formato API**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{UNION_ID}` | L&#39; `$id` URI con codifica URL dell&#39;unione da cercare. Gli URI per gli schemi di unione vengono aggiunti con &quot;__union&quot;. |

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

Le richieste di ricerca unioni richiedono che un oggetto `version` sia incluso nell&#39;intestazione Accetto.

Le seguenti intestazioni Accetta sono disponibili per le ricerche dello schema unione:

| Accetta | Descrizione |
| -------|------------ |
| application/vnd.adobe.xed+json; version={MAJOR_VERSION} | Non elaborato con `$ref` e `allOf`. Include titoli e descrizioni. |
| application/vnd.adobe.xed-full+json; version={MAJOR_VERSION} | `$ref` e `allOf` risolto. Include titoli e descrizioni. |

**Risposta**

Una risposta corretta restituisce la visualizzazione unione di tutti gli schemi che implementano la classe di cui `$id` è stata fornita nel percorso della richiesta.

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

## Elenca gli schemi in un&#39;unione

Per vedere quali schemi fanno parte di un&#39;unione specifica, potete eseguire una richiesta di GET utilizzando i parametri di query per filtrare gli schemi all&#39;interno del contenitore tenant.

Utilizzando il parametro `property` query, potete configurare la risposta solo per gli schemi di restituzione contenenti un `meta:immutableTags` campo e un `meta:class` uguale alla classe a cui si accede tramite unione.

**Formato API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CLASS_ID}` | La classe `$id` di cui si desidera accedere all&#39;unione. |

**Richiesta**

La richiesta seguente cerca tutti gli schemi che fanno parte dell&#39;unione di [!DNL XDM Individual Profile] classi.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco filtrato di schemi, contenente solo quelli che soddisfano entrambi i requisiti. Tenere presente che quando si utilizzano più parametri di query, viene considerata una relazione AND. Il formato della risposta dipende dall’intestazione Accetto inviata nella richiesta.

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
