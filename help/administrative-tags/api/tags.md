---
title: Endpoint tag unificato
description: Scopri come creare, aggiornare, gestire ed eliminare categorie e tag utilizzando le API di Adobe Experience Platform.
role: Developer
exl-id: 6687d1da-a5e4-435a-9f99-1b0f9ac98088
source-git-commit: 717a4ea0568200c940cf9b8f26f4dd2aa9c00a3e
workflow-type: tm+mt
source-wordcount: '1860'
ht-degree: 4%

---

# Endpoint &quot;unified tags&quot;

>[!IMPORTANT]
>
>L&#39;URL dell&#39;endpoint per questo set di endpoint è `https://experience.adobe.io`.

I tag sono una funzionalità che consente di gestire le tassonomie dei metadati per classificare gli oggetti aziendali in modo da semplificarne l&#39;individuazione e la classificazione. Successivamente puoi organizzare questi tag in altri gruppi aggiungendoli alle categorie di tag.

Questa guida fornisce informazioni utili per comprendere meglio i tag e le categorie di tag e include chiamate API di esempio per eseguire azioni di base utilizzando l’API.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte delle API di Adobe Experience Platform. Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, incluse le intestazioni richieste e la lettura di esempi di chiamate API

### Glossario

Il glossario seguente evidenzia la differenza tra un **tag** e una **categoria di tag**.

- **Tag**: un tag consente di gestire la tassonomia dei metadati per gli oggetti business e di classificarli in modo da semplificarne l&#39;individuazione e la classificazione.
   - **Tag non categorizzato**: un tag non categorizzato è un tag che non appartiene a una categoria di tag. Per impostazione predefinita, i tag creati non saranno categorizzati.
- **Categoria tag**: una categoria di tag consente di raggruppare i tag in set significativi, consentendo di fornire più contesto allo scopo del tag.

## Recuperare un elenco di categorie di tag {#get-tag-categories}

Per recuperare un elenco di categorie di tag appartenenti alla tua organizzazione, devi effettuare una richiesta GET all&#39;endpoint `/tagCategory`.

**Formato API**

```http
GET /tagCategory
GET /tagCategory?{QUERY_PARAMETERS}
```

Per recuperare le categorie di tag è possibile utilizzare i seguenti parametri di query facoltativi.

| Parametro query | Descrizione | Esempio |
| --------------- | ----------- | ------- |
| `start` | Percorso da cui inizia l’elenco dei risultati. È possibile utilizzarlo per indicare l’indice iniziale per l’impaginazione dei risultati. | `start=a` |
| `limit` | Il numero massimo di categorie di tag che si desidera recuperare per pagina. | `limit=20` |
| `property` | Attributo in base al quale filtrare quando si recuperano le categorie di tag. I valori supportati includono: &lt;ul≥<li>`name`: nome della categoria di tag.</li></ul> | `property=name==category` |
| `sortBy` | Ordine in base al quale vengono ordinate le categorie di tag. I valori supportati sono `name`, `createdAt` e `modifiedAt`. | `sortBy=name` |
| `sortOrder` | Direzione in cui vengono ordinate le categorie di tag. I valori supportati includono `asc` e `desc`. | `sortOrder=asc` |

**Richiesta**

+++Una richiesta di esempio per elencare tutte le categorie di tag nell’organizzazione

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco di tutte le categorie di tag per l’organizzazione.

+++Risposta di esempio contenente un elenco di tutte le categorie di tag dell’organizzazione.

```json
{
    "_page": {
        "count": 1,
        "limit": 10,
        "property": []
    },
    "tags": [
        {
            "id": "e2b7c656-067b-4413-a366-adde0401df50",
            "name": "Test Category",
            "description": "A sample description for the test tag category.",
            "org": "{ORG_ID}",
            "createdBy": "{USER_ID}",
            "createdAt": "1661752268000",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "1661752268000",
            "tagCount": 0
        }
    ]
}
```

+++

## Crea una nuova categoria di tag {#create-tag-category}

>[!IMPORTANT]
>
>Solo l’amministratore di sistema e l’amministratore di prodotto possono utilizzare questa chiamata API.

È possibile creare una nuova categoria di tag effettuando una richiesta POST all&#39;endpoint `/tagCategory`.

**Formato API**

```http
POST /tagCategory
```

**Richiesta**

+++Richiesta di esempio per creare una nuova categoria di tag.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "Sample Test Category",
    "description": "Sample test category"
 }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Nome della categoria di tag da creare. |
| `description` | Descrizione della categoria di tag da creare. |

+++

**Risposta**

Una risposta di esempio restituisce lo stato HTTP 200 con i dettagli della categoria di tag appena creata.

+++Risposta di esempio contenente i dettagli della categoria di tag appena creata.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Sample Test Category",
    "description": "Sample test category",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## Recuperare una categoria di tag specifica {#get-tag-category}

Per recuperare una categoria di tag specifica che appartiene alla tua organizzazione, devi effettuare una richiesta di GET all&#39;endpoint `/tagCategory` e specificare l&#39;ID della categoria di tag.

**Formato API**

```http
GET /tagCategory/{TAG_CATEGORY_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | ID della categoria di tag che stai recuperando. |

**Richiesta**

+++Richiesta di esempio per recuperare una categoria di tag specifica

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della categoria di tag specificata.

+++Risposta di esempio contenente i dettagli della categoria di tag specificata.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "A sample description for the test tag category.",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | ID della categoria di tag richiesta. |
| `name` | Nome della categoria di tag richiesta. |
| `description` | Descrizione della categoria di tag richiesta. |
| `createdBy` | ID dell’utente che ha creato la categoria di tag. |
| `createdAt` | La marca temporale di quando è stata creata la categoria di tag. |
| `modifiedBy` | ID dell’ultimo utente che ha aggiornato la categoria di tag. |
| `modifiedAt` | La marca temporale dell’ultimo aggiornamento della categoria di tag. |
| `tagCount` | Numero di tag appartenenti alla categoria di tag. |

+++

## Aggiornare una categoria di tag specifica {#update-tag-category}

>[!IMPORTANT]
>
>Solo l’amministratore di sistema e l’amministratore di prodotto possono utilizzare questa chiamata API.

Per aggiornare i dettagli di una categoria di tag specifica che appartiene alla tua organizzazione, devi eseguire una richiesta PATCH all&#39;endpoint `/tagCategory` e specificare l&#39;ID della categoria di tag.

**Formato API**

```http
PATCH /tagCategory/{TAG_CATEGORY_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | ID della categoria di tag che stai recuperando. |

**Richiesta**

+++Richiesta di esempio per aggiornare una categoria di tag specifica

```shell
curl -X PATCH https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "description",
    "value": "Updated sample description",
    "from": "Sample description"
 }]'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `op` | Operazione completata. Per aggiornare una categoria di tag specifica, impostare questo valore su `replace`. |
| `path` | Percorso del campo che verrà aggiornato. I valori supportati includono `name` e `description`. |
| `value` | Valore aggiornato del campo da aggiornare. |
| `from` | Valore originale del campo che si desidera aggiornare. |

+++

**Risposta**

In caso di esito positivo, la risposta HTTP status 200 contiene informazioni sulla categoria di tag appena aggiornata.

+++Una risposta di esempio contenente i dettagli della categoria di tag appena aggiornata.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "Updated sample description",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## Eliminare una categoria di tag specifica {#delete-tag-category}

>[!IMPORTANT]
>
>Solo l’amministratore di sistema e l’amministratore di prodotto possono utilizzare questa chiamata API.

Per eliminare una categoria di tag specifica appartenente alla tua organizzazione, devi eseguire una richiesta DELETE all&#39;endpoint `/tagCategory` e specificare l&#39;ID della categoria di tag.

**Formato API**

```http
DELETE /tagCategory/{TAG_CATEGORY_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | ID della categoria di tag che stai recuperando. |

**Richiesta**

+++Richiesta di esempio per eliminare una categoria di tag specifica

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 insieme a una risposta vuota.

## Recuperare un elenco di tag {#get-tags}

Per recuperare un elenco di tag appartenenti alla tua organizzazione, devi effettuare una richiesta di GET all&#39;endpoint `/tags` e all&#39;ID della categoria di tag.

**Formato API**

```http
GET /tags
GET /tags?{QUERY_PARAMETERS}
```

Durante il recupero dei tag è possibile utilizzare i seguenti parametri di query facoltativi.

| Parametro query | Descrizione | Esempio |
| --------------- | ----------- | ------- |
| `start` | Percorso da cui inizia l’elenco dei risultati. È possibile utilizzarlo per indicare l’indice iniziale per l’impaginazione dei risultati. | `start=a` |
| `limit` | Il numero massimo di tag da recuperare per pagina. | `limit=20` |
| `property` | Attributo in base al quale filtrare quando si recuperano i tag. I valori supportati includono:<ul><li>`name`: nome del tag.</li><li>`archived`: archiviazione o annullamento dell&#39;archiviazione dei tag. È possibile impostare questo valore su `true` o `false`.</li><li>`tagCategoryId`: ID della categoria di tag a cui appartiene il tag.</li></ul> | <ul><li>`property=name==TestTag`</li><li>`property=archived==false`</li><li>`property=tagCategoryId==e2b7c656-067b-4413-a366-adde0401df50`</li> |
| `sortBy` | L’ordine in cui i tag sono ordinati per. I valori supportati sono `name`, `createdAt` e `modifiedAt`. | `sortBy=name` |
| `sortOrder` | Direzione in cui vengono ordinate le categorie di tag. I valori supportati includono `asc` e `desc`. | `sortOrder=asc` |


**Richiesta**

+++Richiesta di esempio per recuperare tutti i tag appartenenti a una categoria di tag specifica

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags?property=tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli dei tag appartenenti alla categoria di tag specifica.

+++ Una risposta di esempio che contiene i dettagli dei tag richiesti.

```json
{
    "_page": {
        "count": 166,
        "limit": 10,
        "next": "eyJjb21wb3NpdGVUb2tlbiI6IntcInRva2VuXCI6XCIrUklEOn52a0owQUp3WDRrVko1d0FBQUFBQUFBPT0jUlQ6MiNUUkM6MjAjUlREOnVDTmQyWlAvWjV6TGdvUGVGR1JHQk1KNVExVmR6Mnc9I0lTVjoyI0lFTzo2NTU2NyNRQ0Y6OCNGUEM6QWdFQ0J3TG1BQ1NmQnNBQ0JBb0FBQVFBQ0FBQUNJQVlnQWVBRElBTmdBWEFFTUJCUUVBQUFBQkFRQkdBSElBR2dBQ0FENEFId0FKUkRFQUNBZ2dBUUJnQUVBQUlIb0FaZ0FDQUJNQUFRVUFBUUFCQVFScUFBc0FTQUFBRUxvQU9nQWFBQmNBQVlBQUFHSUlCUUFDQU1vQUlnQWlBQk1DQUFRQUFnZ0FnQUM2QURZQTNnQWlBR1lBQWdCZUFBY0FCZ0JlQUM4QURBQUlBQWdBQVFBQ0FBRUZBQVFFQUFBRWdBQ0FBSjRCR2dBeUFCSUFPZ0F5QU13QVNRQ0FBQUVBdGdCRUFBR0FkZ0FuQUFDZ0NBQUFBQ0lCQUFDSkFnQUJBRUFDQUg0QUhnQWFBQllBVUFFQUNCQUFFQUFRQUF4QUFzUnJBQUlFQUFBYkxoQklIQVBBQUhnUUVBTEVxQUE4RkNBQVFtcUVBd0FBTWd3Y09BSFdIa1FBZ0JGT0FTNEN4QVE0QVwiLFwicmFuZ2VcIjp7XCJtaW5cIjpcIlwiLFwibWF4XCI6XCJGRlwifX0iLCJvcmRlckJ5SXRlbXMiOlt7Iml0ZW0iOjE2OTQ0ODg2MDMwMDB9XSwicmlkIjoidmtKMEFKd1g0a1hHV2dFQUFBQUFBQT09IiwiaW5jbHVzaXZlIjp0cnVlfQ==",
        "property": [
            "tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50"
        ]
    },
    "tags": [
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8af14b1e-f267-44ad-b94c-9ac70274e3d5",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624481530",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8b907a2c-0f15-4d2c-9672-bf545d5e47ab",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624489131",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "e30bd956-afad-40a1-8f4a-7e4428855856",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624494191",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705451722000,
            "createdBy": "{USER_ID}",
            "id": "3bf6a6ba-0b11-4d83-8f35-db6e5b9652d8",
            "modifiedAt": 1705451722000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705451701640",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705422929000,
            "createdBy": "{USER_ID}",
            "id": "0910dfc8-7924-473d-afc6-1aa68337b3b6",
            "modifiedAt": 1705422929000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705422890399",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705394126000,
            "createdBy": "{USER_ID}",
            "id": "b426085e-580b-4147-9921-8ba77ffa77a9",
            "modifiedAt": 1705394126000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705394104556",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": true,
            "createdAt": 1705392795000,
            "createdBy": "{USER_ID}",
            "id": "92961035-e72b-45a0-9625-781380017585",
            "modifiedAt": 1705392832000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705392794917",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705335274000,
            "createdBy": "{USER_ID}",
            "id": "436ce801-ef87-45fd-b34a-9ce938a447e1",
            "modifiedAt": 1705335274000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705335252944",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694776514000,
            "createdBy": "{USER_ID}",
            "id": "1e6e9836-5e18-4340-a959-3206c9bc3a94",
            "modifiedAt": 1694776514000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694776510734",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694488609000,
            "createdBy": "{USER_ID}",
            "id": "b8400673-2f90-48e9-b73b-cdfbba5ab361",
            "modifiedAt": 1694488609000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694488608301",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        }
    ]
}
```

+++

## Crea un nuovo tag {#create-tag}

>[!IMPORTANT]
>
>Solo l’amministratore di sistema e l’amministratore di prodotto possono utilizzare questa chiamata API per creare un nuovo tag in una categoria di tag specificata.
>
>Se stai creando un tag non categorizzato, **non** hai bisogno delle autorizzazioni di amministratore.

È possibile creare un nuovo tag effettuando una richiesta POST all&#39;endpoint `/tags`.

**Formato API**

```http
POST /tags
```

**Richiesta**

+++Richiesta di esempio per creare un nuovo tag.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "sampleTag"
 }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | **Richiesto**. Nome del tag da creare. |
| `tagCategoryId` | *Facoltativo*. ID della categoria di tag a cui desideri che appartenga il tag. Se non viene specificato, il tag verrà creato come parte della categoria Non categorizzato. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 con i dettagli del tag appena creato.

+++Risposta di esempio contenente i dettagli del tag appena creato.

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Uncategorized-{ORG_ID}",
    "tagCategoryName": "Uncategorized",
    "archived": false
}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `name` | Nome del tag appena creato. |
| `id` | ID del tag appena creato. |
| `org` | ID dell’organizzazione a cui appartiene il tag. |
| `createdAt` | La marca temporale di quando è stato creato il tag. |
| `createdBy` | ID dell’utente che ha creato il tag. |
| `modifiedAt` | La marca temporale dell’ultimo aggiornamento del tag. |
| `modifiedBy` | ID dell’ultimo utente che ha aggiornato il tag. |
| `tagCategoryId` | ID della categoria di tag a cui appartiene il tag. |
| `tagCategoryName` | Nome della categoria di tag a cui appartiene il tag. |

+++

## Recuperare un tag specifico {#get-tag}

Per recuperare un tag specifico appartenente alla tua organizzazione, devi eseguire una richiesta di GET all&#39;endpoint `/tags` e specificare l&#39;ID del tag da recuperare.

**Formato API**

```http
GET /tags/{TAG_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TAG_ID}` | ID del tag che stai recuperando. |

**Richiesta**

+++Richiesta di esempio per recuperare un tag specifico

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli del tag specificato.

+++Risposta di esempio contenente i dettagli del tag specificato.

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `name` | Nome del tag recuperato. |
| `id` | ID del tag recuperato. |
| `org` | ID dell’organizzazione a cui appartiene il tag. |
| `createdAt` | La marca temporale di quando è stato creato il tag. |
| `createdBy` | ID dell’utente che ha creato il tag. |
| `modifiedAt` | La marca temporale dell’ultimo aggiornamento del tag. |
| `modifiedBy` | ID dell’ultimo utente che ha aggiornato il tag. |
| `tagCategoryId` | ID della categoria di tag a cui appartiene il tag. |
| `tagCategoryName` | Nome della categoria di tag a cui appartiene il tag. |
| `archived` | Stato di archiviazione del tag. Se impostato su `true`, significa che il tag è archiviato. |

+++

## Convalida tag {#validate-tags}

È possibile verificare se esistono tag effettuando una richiesta POST all&#39;endpoint `/tags/validate`.

**Formato API**

```http
POST /tags/validate
```

**Richiesta**

+++Una richiesta di esempio per convalidare gli ID tag forniti.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "ids": [
        "2bd5ddd9-7284-4767-81d9-c75b122f2a6a","d113f40c-0097-4626-8d5f-6d5017694453", "invalid-tag"
    ],
    "entity": "{API_KEY}"
 }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `ids` | Array contenente un elenco di ID tag da convalidare. |
| `entity` | Entità che richiede la convalida. È possibile utilizzare il valore `{API_KEY}` per questo parametro. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni sui tag validi e non validi.

+++Una risposta di esempio che mostra quali tag sono validi e non validi.

```json
{
    "invalidTags": [
        {
            "id": "invalid-tag"
        }
    ],
    "validTags": [
        {
            "id": "d113f40c-0097-4626-8d5f-6d5017694453"
        },
        {
            "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a"
        }
    ]
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `invalidTags` | Matrice contenente un elenco degli ID tag non validi. |
| `validTags` | Matrice che contiene un elenco degli ID tag validi. |

+++

## Aggiornare un tag specifico {#update-tag}

È possibile aggiornare un tag specificato effettuando una richiesta PATCH all&#39;endpoint `/tags` e fornendo l&#39;ID del tag che si desidera aggiornare.

**Formato API**

```http
PATCH /tags/{TAG_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TAG_ID}` | ID del tag da aggiornare. |

**Richiesta**

+++Richiesta di esempio per aggiornare un tag specifico

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "name",
    "value": "newSampleTag",
    "from": "sampleTag"
 }]'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `op` | Operazione da eseguire. In questo caso d&#39;uso, sarà sempre impostato su `replace`. |
| `path` | Percorso del campo che verrà aggiornato. I valori supportati sono `name`, `archived` e `tagCategoryId`. |
| `value` | Valore aggiornato del campo da aggiornare. |
| `from` | Valore originale del campo che si desidera aggiornare. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli del tag appena aggiornato.

+++Risposta di esempio contenente i dettagli del tag aggiornato.

```json
{
    "name": "newSampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

+++

## Eliminare un tag specifico {#delete-tag}

>[!IMPORTANT]
>
>Solo l’amministratore di sistema e l’amministratore di prodotto possono utilizzare questa chiamata API.
>
>Inoltre, il tag **non può** essere associato ad alcun oggetto aziendale e **deve** essere archiviato prima di poter eliminare il tag. È possibile archiviare il tag utilizzando l&#39;endpoint [aggiorna tag](#update-tag).

È possibile eliminare un tag specifico creando un tag DELETE nell&#39;endpoint `/tags` e specificando l&#39;ID del tag che si desidera eliminare.

**Formato API**

```http
DELETE /tags/{TAG_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TAG_ID}` | ID del tag da eliminare. |

**Richiesta**

+++Richiesta di esempio per eliminare un tag specifico

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 insieme a una risposta vuota.

## Passaggi successivi

Dopo aver letto questa guida, avrai una migliore comprensione di come creare, gestire ed eliminare tag e categorie di tag utilizzando le API di Adobe Experience Platform. Per ulteriori informazioni sulla gestione dei tag tramite l&#39;interfaccia utente, leggere la [guida alla gestione dei tag](../ui/managing-tags.md). Per ulteriori informazioni sulla gestione delle categorie di tag tramite l&#39;interfaccia utente, leggere la [guida alle categorie di tag](../ui/tags-categories.md).
