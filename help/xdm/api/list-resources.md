---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Elenco delle risorse
topic: developer guide
translation-type: tm+mt
source-git-commit: 1541b027a4e572dc5e4e64de1117a269c58bafab

---


# Elenco delle risorse

È possibile visualizzare un elenco di tutte le risorse (schemi, classi, mixin o tipi di dati) all&#39;interno di un contenitore eseguendo una singola richiesta GET. Per facilitare il filtraggio dei risultati, il Registro di sistema dello schema supporta l&#39;utilizzo di parametri di query per elencare le risorse.

I parametri di query più comuni includono:

* `limit` - Limita il numero di risorse restituite. Esempio: `limit=5` restituirà un elenco di cinque risorse.
* `orderby` - Ordinare i risultati in base a una proprietà specifica. Esempio: i risultati `orderby=title` verranno ordinati in ordine crescente (A-Z) in base al titolo. Se si aggiunge un titolo `-` prima del titolo (`orderby=-title`), gli elementi vengono ordinati per titolo in ordine decrescente (Z-A).
* `property` - Filtrare i risultati su qualsiasi attributo di livello principale. Ad esempio, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` restituisce solo i mixin compatibili con la classe Profilo singolo XDM.

Quando si combinano più parametri di query, questi devono essere separati da e commerciale (`&`).

**Formato API**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore in cui si trovano le risorse (&quot;global&quot; o &quot;tenant&quot;). |
| `{RESOURCE_TYPE}` | Il tipo di risorsa da recuperare dalla Libreria schema. I tipi validi sono `datatypes`, `mixins`, `schemas`e `classes`. |

**Richiesta**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes&limit=2 \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dall’intestazione Accetta inviata nella richiesta. Le seguenti intestazioni Accetta sono disponibili per elencare le risorse:

| Accetta intestazione | Descrizione |
| ------- | ------------ |
| application/vnd.adobe.xed-id+json | Restituisce un breve riepilogo di ciascuna risorsa, generalmente l&#39;intestazione preferita per l&#39;elenco |
| application/vnd.adobe.xed+json | Restituisce lo schema JSON completo per ogni risorsa, con originale `$ref` e `allOf` incluso |

**Risposta**

La richiesta precedente utilizzava l’intestazione `application/vnd.adobe.xed-id+json` Accetto, pertanto la risposta include solo gli attributi `title`, `$id`, `meta:altId`e `version` per ogni risorsa. La sostituzione `full` nell&#39;intestazione Accetto restituisce tutti gli attributi di ogni risorsa. Selezionate l’intestazione Accetto appropriata in base alle informazioni richieste nella risposta.

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```
