---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Elenco delle risorse
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 2%

---


# Elenco delle risorse

È possibile visualizzare un elenco di tutte le risorse del Registro di sistema dello schema di un determinato tipo (classi, mixin, schemi, tipi di dati o descrittori) all&#39;interno di un contenitore eseguendo una singola richiesta GET.

>[!NOTE]
>
>Quando si elencano le risorse, il Registro di sistema dello schema limita i set di risultati a 300 elementi. Per restituire risorse oltre questo limite, è necessario utilizzare i parametri [di](#paging)paging. È inoltre consigliabile utilizzare i parametri di query per [filtrare i risultati](#filtering) e ridurre il numero di risorse restituite.

**Formato API**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
GET /{CONTAINER_ID}/{RESOURCE_TYPE}?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore in cui si trovano le risorse (&quot;global&quot; o &quot;tenant&quot;). |
| `{RESOURCE_TYPE}` | Il tipo di risorsa da recuperare dalla Libreria schema. I tipi validi sono `classes`, `mixins`, `schemas`, `datatypes`e `descriptors`. |
| `{QUERY_PARAMS`} | Parametri di query facoltativi per filtrare i risultati per. Per ulteriori informazioni, consulta la sezione sui parametri [di](#query) query. |

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
| application/vnd.adobe.xed-id+json | Restituisce un breve riepilogo di ciascuna risorsa. Intestazione consigliata per elencare le risorse. (Limite: 300) |
| application/vnd.adobe.xed+json | Restituisce lo schema JSON completo per ciascuna risorsa, con originale `$ref` e `allOf` incluso. (Limite: 300) |
| application/vnd.adobe.xdm-v2+json | Quando si utilizza l&#39; `/descriptors` endpoint, questa intestazione Accetta deve essere utilizzata per utilizzare le funzionalità di paging. |

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

## Utilizzo dei parametri di query {#query}

Il Registro di sistema dello schema supporta l&#39;utilizzo di parametri di query per elencare le risorse e filtrare i risultati.

>[!NOTE]
>
>Quando si combinano più parametri di query, questi devono essere separati da e commerciale (`&`).

### Pagine {#paging}

I parametri di query più comuni per il paging includono:

| Parametro | Descrizione |
| --- | --- |
| `start` | Specificate dove devono iniziare i risultati elencati. Questo valore può essere ottenuto dall&#39; `_page.next` attributo di una risposta a un elenco e utilizzato per accedere alla pagina successiva dei risultati. Se il `_page.next` valore è null, non è disponibile alcuna pagina aggiuntiva. |
| `limit` | Limita il numero di risorse restituite. Esempio: `limit=5` restituirà un elenco di cinque risorse. |
| `orderby` | Ordinare i risultati in base a una proprietà specifica. Esempio: `orderby=title` ordinerà i risultati in ordine crescente (A-Z) in base al titolo. Se si aggiunge un titolo `-` prima del titolo (`orderby=-title`), gli elementi vengono ordinati per titolo in ordine decrescente (Z-A). |

### Filtro {#filtering}

Potete filtrare i risultati utilizzando il `property` parametro, utilizzato per applicare un operatore specifico a una determinata proprietà JSON all&#39;interno delle risorse recuperate. Gli operatori supportati includono:

| Operatore | Descrizione | Esempio |
| --- | --- | --- |
| `==` | Filtra in base al fatto che la proprietà sia uguale al valore fornito. | `property=title==test` |
| `!=` | Filtra in base al fatto che la proprietà non sia uguale al valore fornito. | `property=title!=test` |
| `<` | Filtra in base al fatto che la proprietà sia minore del valore fornito. | `property=version<5` |
| `>` | Filtra in base al fatto che la proprietà sia maggiore del valore fornito. | `property=version>5` |
| `<=` | Filtra se la proprietà è minore o uguale al valore specificato. | `property=version<=5` |
| `>=` | Filtra in base al fatto che la proprietà sia maggiore o uguale al valore fornito. | `property=version>=5` |
| `~` | Filtra in base al fatto che la proprietà corrisponda o meno a un&#39;espressione regolare specificata. | `property=title~test$` |
| (Nessuno) | Se si specifica solo il nome della proprietà, vengono restituite solo le voci in cui esiste la proprietà. | `property=title` |

>[!TIP]
>
>Potete usare il `property` parametro per filtrare i mixin in base alla classe compatibile. Ad esempio, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` restituisce solo i mixin compatibili con la classe Profilo singolo XDM.
