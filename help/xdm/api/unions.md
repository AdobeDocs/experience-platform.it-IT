---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;modello dati;registro schema;registro schema;unione;unioni;unioni;appartenenza segmento;timeSeriesEvents;
solution: Experience Platform
title: Endpoint API Unions
description: L’endpoint /sindacati nell’API del Registro di sistema dello schema ti consente di gestire programmaticamente gli schemi di unione XDM nell’applicazione di esperienza.
topic-legacy: developer guide
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 3%

---

# Endpoint Unions

Le unioni (o visualizzazioni di unione) sono schemi generati dal sistema e di sola lettura che aggregano i campi di tutti gli schemi che condividono la stessa classe ([!DNL XDM ExperienceEvent] o [!DNL XDM Individual Profile]) e sono abilitati per [[!DNL Real-Time Customer Profile]](../../profile/home.md).

Questo documento descrive i concetti essenziali per lavorare con i sindacati nell’API del Registro di sistema dello schema, incluse le chiamate di esempio per varie operazioni. Per informazioni più generali sui sindacati in XDM, consulta la sezione sui sindacati in [nozioni di base sulla composizione dello schema](../schema/composition.md#union).

## Campi dello schema unione

La [!DNL Schema Registry] include automaticamente tre campi chiave all&#39;interno di uno schema di unione: `identityMap`, `timeSeriesEvents`e `segmentMembership`.

### Mappa identità

Schema di unione `identityMap` è una rappresentazione delle identità note all&#39;interno degli schemi di record associati all&#39;unione. La mappa identità separa le identità in diversi array collegati dallo spazio dei nomi. Ogni identità elencata è essa stessa un oggetto contenente un `id` valore. Consulta la sezione [Documentazione del servizio Identity](../../identity-service/home.md) per ulteriori informazioni.

### Eventi della serie temporale

La `timeSeriesEvents` array è un elenco di eventi serie temporali relativi agli schemi di record associati all&#39;unione. Quando i dati di profilo vengono esportati nei set di dati, questa matrice viene inclusa per ogni record. Questo è utile per vari casi d’uso, ad esempio per l’apprendimento automatico, in cui i modelli necessitano dell’intera cronologia dei comportamenti di un profilo oltre agli attributi del record.

### Mappa di appartenenza al segmento

La `segmentMembership` map memorizza i risultati delle valutazioni dei segmenti. Quando i processi di segmento vengono eseguiti correttamente utilizzando la variabile [API di segmentazione](https://www.adobe.io/experience-platform-apis/references/segmentation/), la mappa viene aggiornata. `segmentMembership` memorizza anche tutti i segmenti di pubblico valutati in precedenza acquisiti in Platform, consentendo l’integrazione con altre soluzioni come Adobe Audience Manager. Guarda l’esercitazione su [creazione di segmenti utilizzando le API](../../segmentation/tutorials/create-a-segment.md) per ulteriori informazioni.

## Recupera un elenco di unioni {#list}

Quando si imposta la `union` su uno schema, il [!DNL Schema Registry] aggiunge automaticamente lo schema all&#39;unione per la classe su cui è basato lo schema. Se non esiste alcuna unione per la classe in questione, viene creata automaticamente una nuova unione. La `$id` per l&#39;unione è simile allo standard `$id` di altri [!DNL Schema Registry] risorse, con l&#39;unica differenza che è aggiunta da due caratteri di sottolineatura e la parola &quot;unione&quot; (`__union`).

È possibile visualizzare un elenco delle unioni disponibili effettuando una richiesta di GET al `/tenant/unions` punto finale.

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

Il formato della risposta dipende dal `Accept` intestazione inviata nella richiesta. I seguenti `Accept` Le intestazioni sono disponibili per l&#39;elenco dei sindacati:

| `Accept` header | Descrizione |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Restituisce un breve riepilogo di ciascuna risorsa. Intestazione consigliata per l’elenco delle risorse. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Restituisce la classe JSON completa per ogni risorsa, con originale `$ref` e `allOf` incluso. (Limite: 300) |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 (OK) e un `results` nel corpo della risposta. Se sono state definite unioni, i dettagli di ciascuna unione vengono forniti come oggetti all&#39;interno della matrice. Se non sono state definite unioni, viene comunque restituito lo stato HTTP 200 (OK), ma la `results` array vuoto.

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

## Cercare un sindacato {#lookup}

Puoi visualizzare un&#39;unione specifica eseguendo una richiesta di GET che include `$id` e, a seconda dell&#39;intestazione Accept, alcuni o tutti i dettagli dell&#39;unione.

>[!NOTE]
>
>Le ricerche dell’Unione sono disponibili utilizzando `/unions` e `/schemas` endpoint per abilitarli da utilizzare in [!DNL Profile] esporta in un set di dati.

**Formato API**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{UNION_ID}` | L’URL è codificato `$id` URI dell&#39;unione da cercare. Gli URI per gli schemi di unione vengono aggiunti con &quot;__union&quot;. |

{style=&quot;table-layout:auto&quot;}

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

Le richieste di ricerca dell’unione richiedono un `version` nell’intestazione Accept.

Le seguenti intestazioni Accept sono disponibili per le ricerche dello schema di unione:

| Accept | Descrizione |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | Raw con `$ref` e `allOf`. Include titoli e descrizioni. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` attributi e `allOf` risolto. Include titoli e descrizioni. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce la visualizzazione dell&#39;unione di tutti gli schemi che implementano la classe di cui `$id` è stato fornito nel percorso della richiesta.

Il formato della risposta dipende dall’intestazione Accept inviata nella richiesta. Prova a utilizzare diverse intestazioni Accept per confrontare le risposte e determinare quale intestazione è migliore per il tuo caso d’uso.

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

## Abilitare uno schema per l&#39;appartenenza all&#39;unione {#enable}

Affinché uno schema sia incluso nell&#39;unione per la sua classe, un `union` è necessario aggiungere il tag al `meta:immutableTags` attributo. Puoi eseguire questa operazione effettuando una richiesta PATCH per aggiungere un `meta:immutableTags` array con un singolo valore stringa di `union` allo schema in questione. Consulta la sezione [guida all’endpoint degli schemi](./schemas.md#union) per un esempio dettagliato.

## Elencare schemi in un’unione {#list-schemas}

Per vedere quali schemi fanno parte di un’unione specifica, puoi eseguire una richiesta di GET al gruppo `/tenant/schemas` punto finale. Utilizzo della `property` parametro query, è possibile configurare la risposta in modo che restituiscano solo schemi contenenti un `meta:immutableTags` campo e `meta:class` uguale alla classe a cui accedi.

**Formato API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CLASS_ID}` | La `$id` della classe di cui si desidera elencare gli schemi abilitati per l&#39;unione. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta seguente recupera un elenco di tutti gli schemi che fanno parte dell&#39;unione per [!DNL XDM Individual Profile] classe.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dal `Accept` intestazione inviata nella richiesta. I seguenti `Accept` le intestazioni sono disponibili per elencare gli schemi:

| `Accept` header | Descrizione |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Restituisce un breve riepilogo di ciascuna risorsa. Intestazione consigliata per l’elenco delle risorse. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Restituisce lo schema JSON completo per ogni risorsa, con originale `$ref` e `allOf` incluso. (Limite: 300) |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce un elenco filtrato di schemi, contenente solo quelli appartenenti alla classe specificata che sono stati abilitati per l’appartenenza all’unione. Tenere presente che quando si utilizzano più parametri di query, si presume una relazione AND.

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
