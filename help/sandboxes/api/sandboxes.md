---
keywords: Experience Platform;home;argomenti popolari;guida per gli sviluppatori sandbox
solution: Experience Platform
title: Endpoint API per la gestione delle sandbox
topic-legacy: developer guide
description: L’endpoint /sandbox nell’API Sandbox consente di gestire le sandbox in Adobe Experience Platform a livello di programmazione.
source-git-commit: f84898a87a8a86783220af7f74e17f464a780918
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 2%

---

# Endpoint di gestione sandbox

Le sandbox in Adobe Experience Platform forniscono ambienti di sviluppo isolati che consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sull’ambiente di produzione. L’endpoint `/sandboxes` nell’ API [!DNL Sandbox] consente di gestire le sandbox in Platform a livello di programmazione.

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39; [[!DNL Sandbox] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml). Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla relativa documentazione, una guida per la lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare chiamate a qualsiasi API di Experience Platform.

## Recupera un elenco di sandbox {#list}

Puoi elencare tutte le sandbox appartenenti all’organizzazione IMS (attive o meno), effettuando una richiesta di GET all’endpoint `/sandboxes` .

**Formato API**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Parametri di query opzionali per filtrare i risultati in base a. Per ulteriori informazioni, consulta la sezione sui [parametri di query](./appendix.md#query) . |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di sandbox appartenenti all’organizzazione, inclusi dettagli quali `name`, `title`, `state` e `type`.

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev-2",
            "title": "Development 2",
            "state": "creating",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-07 10:16:02",
            "lastModifiedDate": "2019-09-07 10:16:02",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ],
    "_page": {
        "limit": 4,
        "count": 4
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes/?limit={limit}&offset={offset}",
            "templated": true
        },
        "prev": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=0&limit=1",
            "templated": null
        },
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=1&limit=1",
            "templated": null
        }
    }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della sandbox. Questa proprietà viene utilizzata a scopo di ricerca nelle chiamate API. |
| `title` | Nome visualizzato della sandbox. |
| `state` | Lo stato di elaborazione corrente della sandbox. Lo stato di una sandbox può essere uno dei seguenti: <br/><ul><li>`creating`: La sandbox è stata creata, ma viene comunque fornita dal sistema.</li><li>`active`: La sandbox viene creata e attiva.</li><li>`failed`: A causa di un errore, il sistema non è in grado di eseguire il provisioning della sandbox ed è disabilitato.</li><li>`deleted`: La sandbox è stata disabilitata manualmente.</li></ul> |
| `type` | Il tipo di sandbox. Gli attuali tipi di sandbox supportati sono `development` e `production`. |
| `isDefault` | Proprietà booleana che indica se questa sandbox è la sandbox di produzione predefinita per l’organizzazione. |
| `eTag` | Identificatore per una versione specifica della sandbox. Utilizzato per il controllo delle versioni e l’efficienza del caching, questo valore viene aggiornato ogni volta che viene apportata una modifica alla sandbox. |

## Cercare una sandbox {#lookup}

Puoi cercare un singolo sandbox effettuando una richiesta GET che include la proprietà `name` della sandbox nel percorso della richiesta.

**Formato API**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La proprietà `name` della sandbox che desideri cercare. |

**Richiesta**

La richiesta seguente recupera una sandbox denominata &quot;dev-2&quot;.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Risposta**

Una risposta corretta restituisce i dettagli della sandbox, inclusi i relativi `name`, `title`, `state` e `type`.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "creating",
    "type": "development",
    "region": "VA7",
    "isDefault": false,
    "eTag": 1,
    "createdDate": "2019-09-07 10:16:02",
    "lastModifiedDate": "2019-09-07 10:16:02",
    "createdBy": "{USER_ID}",
    "modifiedBy": "{USER_ID}"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della sandbox. Questa proprietà viene utilizzata a scopo di ricerca nelle chiamate API. |
| `title` | Nome visualizzato della sandbox. |
| `state` | Lo stato di elaborazione corrente della sandbox. Lo stato di una sandbox può essere uno dei seguenti: <ul><li>**creazione**: La sandbox è stata creata, ma viene comunque fornita dal sistema.</li><li>**attivo**: La sandbox viene creata e attiva.</li><li>**non riuscito**: A causa di un errore, il sistema non è in grado di eseguire il provisioning della sandbox ed è disabilitato.</li><li>**eliminato**: La sandbox è stata disabilitata manualmente.</li></ul> |
| `type` | Il tipo di sandbox. Gli attuali tipi di sandbox supportati includono: `development` e `production`. |
| `isDefault` | Proprietà booleana che indica se questa sandbox è la sandbox predefinita per l’organizzazione. In genere si tratta della sandbox di produzione. |
| `eTag` | Identificatore per una versione specifica della sandbox. Utilizzato per il controllo delle versioni e l’efficienza del caching, questo valore viene aggiornato ogni volta che viene apportata una modifica alla sandbox. |

## Creare una sandbox {#create}

Puoi creare una nuova sandbox di sviluppo o produzione effettuando una richiesta POST all’endpoint `/sandboxes` .

### Creare una sandbox di sviluppo

Per creare una sandbox di sviluppo, devi fornire un attributo `type` con un valore di `development` nel payload della richiesta.

**Formato API**

```http
POST /sandboxes
```

**Richiesta**

La seguente richiesta crea una nuova sandbox di sviluppo denominata &quot;acme-dev&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "type": "development"
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Identificatore che verrà utilizzato per accedere alla sandbox nelle richieste future. Questo valore deve essere univoco e la best practice prevede di renderlo il più descrittivo possibile. Questo valore non può contenere spazi o caratteri speciali. |
| `title` | Un nome leggibile dall’utente utilizzato a scopo di visualizzazione nell’interfaccia utente di Platform. |
| `type` | Tipo di sandbox da creare. Per una sandbox non di produzione, questo valore deve essere `development`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova sandbox creata, indicando che la relativa `state` è &quot;creazione&quot;.

```json
{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>Il provisioning delle sandbox da parte del sistema richiede circa 30 secondi, dopodiché le `state` diventeranno &quot;attive&quot; o &quot;non riuscite&quot;.

### Creare una sandbox di produzione

Per creare una sandbox di produzione, devi fornire un attributo `type` con un valore di `production` nel payload della richiesta.

**Formato API**

```http
POST /sandboxes
```

**Richiesta**

La seguente richiesta crea una nuova sandbox di produzione denominata &quot;acme&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H `Accept: application/json` \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme",
    "title": "Acme Business Group",
    "type": "production"
}'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Identificatore che verrà utilizzato per accedere alla sandbox nelle richieste future. Questo valore deve essere univoco e la best practice prevede di renderlo il più descrittivo possibile. Questo valore non può contenere spazi o caratteri speciali. |
| `title` | Un nome leggibile dall’utente utilizzato a scopo di visualizzazione nell’interfaccia utente di Platform. |
| `type` | Tipo di sandbox da creare. Per una sandbox di produzione, questo valore deve essere `production`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova sandbox creata, indicando che la relativa `state` è &quot;creazione&quot;.

```json
{
    "name": "acme",
    "title": "Acme Business Group",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```

>[!NOTE]
>
>Il provisioning delle sandbox da parte del sistema richiede circa 30 secondi, dopodiché le `state` diventeranno &quot;attive&quot; o &quot;non riuscite&quot;.

## Aggiornare una sandbox {#put}

È possibile aggiornare uno o più campi in una sandbox effettuando una richiesta di PATCH che include il `name` della sandbox nel percorso della richiesta e la proprietà da aggiornare nel payload della richiesta.

>[!NOTE]
>
>Attualmente è possibile aggiornare solo la proprietà `title` di una sandbox.

**Formato API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La proprietà `name` della sandbox che desideri aggiornare. |

**Richiesta**

La richiesta seguente aggiorna la proprietà `title` della sandbox denominata &quot;acme&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
  -d '{
    "title": "Acme Business Group prod"
  }'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 (OK) con i dettagli della sandbox appena aggiornata.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "active",
    "type": "production",
    "region": "VA7"
}
```

## Reimpostare una sandbox {#reset}

>[!IMPORTANT]
>
>Non è possibile ripristinare la sandbox di produzione predefinita se il grafico di identità ospitato al suo interno viene utilizzato anche da Adobe Analytics per la funzione [Cross Device Analytics (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html) o se il grafico di identità ospitato al suo interno viene utilizzato anche da Adobe Audience Manager per la funzione [People Based Destinations (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html) .

Le sandbox di sviluppo dispongono di una funzione di &quot;reimpostazione di fabbrica&quot; che elimina tutte le risorse non predefinite da una sandbox. Puoi reimpostare una sandbox effettuando una richiesta di PUT che include il `name` della sandbox nel percorso della richiesta.

**Formato API**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La proprietà `name` della sandbox da reimpostare. |

**Richiesta**

La richiesta seguente reimposta una sandbox denominata &quot;acme-dev&quot;.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme-dev \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `action` | Questo parametro deve essere fornito nel payload della richiesta con un valore di &quot;reset&quot; per reimpostare la sandbox. |

**Risposta**

Una risposta corretta restituisce i dettagli della sandbox aggiornata, indicando che la relativa `state` è &quot;reimpostazione&quot;.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>Una volta reimpostata la sandbox, il sistema impiega circa 30 secondi per effettuare il provisioning. Una volta eseguito il provisioning, l’ `state` della sandbox diventa &quot;attivo&quot; o &quot;non riuscito&quot;.

La tabella seguente contiene possibili eccezioni che potrebbero impedire la reimpostazione di una sandbox:

| Codice di errore | Descrizione |
| --- | --- |
| `2074-400` | Impossibile reimpostare questa sandbox perché il grafico delle identità ospitato in questa sandbox viene utilizzato anche da Adobe Analytics per la funzione Cross Device Analytics (CDA). |
| `2075-400` | Impossibile reimpostare questa sandbox perché il grafico delle identità ospitato in questa sandbox viene utilizzato anche da Adobe Audience Manager per la funzione Destinazioni basate su persone (PBD). |
| `2076-400` | Non è possibile reimpostare questa sandbox perché il grafico delle identità ospitato in questa sandbox viene utilizzato anche da Adobe Audience Manager per la funzione People Based Destinations (PBD) e da Adobe Analytics per la funzione Cross Device Analytics (CDA). |
| `2077-400` | Avviso: La sandbox `{SANDBOX_NAME}` viene utilizzata per la condivisione di segmenti bidirezionale con Adobe Audience Manager o con il servizio core Audience. |

## Eliminare una sandbox {#delete}

>[!IMPORTANT]
>
>Impossibile eliminare la sandbox di produzione predefinita.

È possibile eliminare una sandbox effettuando una richiesta di DELETE che include nel percorso della richiesta la versione `name` della sandbox.

>[!NOTE]
>
>L’esecuzione di questa chiamata API aggiorna la proprietà della sandbox `status` su &quot;eliminata&quot; e la disattiva. Le richieste GET possono ancora recuperare i dettagli della sandbox dopo che è stata eliminata.

**Formato API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La `name` della sandbox da eliminare. |

**Richiesta**

La richiesta seguente elimina una sandbox denominata &quot;acme-dev&quot;.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Risposta**

Una risposta corretta restituisce i dettagli aggiornati della sandbox, indicando che la relativa `state` è &quot;eliminata&quot;.

```json
{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
