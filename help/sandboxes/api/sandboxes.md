---
keywords: Experience Platform;home;argomenti popolari;guida per gli sviluppatori sandbox
solution: Experience Platform
title: Endpoint API per la gestione delle sandbox
description: L’endpoint /sandbox nell’API Sandbox consente di gestire le sandbox in Adobe Experience Platform a livello di programmazione.
exl-id: 0ff653b4-3e31-4ea5-a22e-07e18795f73e
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1488'
ht-degree: 4%

---

# Endpoint di gestione sandbox

Le sandbox in Adobe Experience Platform forniscono ambienti di sviluppo isolati che consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sull’ambiente di produzione. La `/sandboxes` punto finale [!DNL Sandbox] L’API ti consente di gestire in modo programmatico le sandbox in Platform.

## Introduzione

L’endpoint API utilizzato in questa guida fa parte del [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e importanti informazioni sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recupera un elenco di sandbox {#list}

Puoi elencare tutte le sandbox appartenenti all’organizzazione (attive o meno), effettuando una richiesta di GET al `/sandboxes` punto finale.

**Formato API**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Parametri di query opzionali per filtrare i risultati in base a. Vedi la sezione su [parametri di query](./appendix.md#query) per ulteriori informazioni. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di sandbox appartenenti all’organizzazione, inclusi dettagli quali `name`, `title`, `state`e `type`.

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
| `type` | Il tipo di sandbox. Gli attuali tipi di sandbox supportati includono `development` e `production`. |
| `isDefault` | Proprietà booleana che indica se questa sandbox è la sandbox di produzione predefinita per l’organizzazione. |
| `eTag` | Identificatore per una versione specifica della sandbox. Utilizzato per il controllo delle versioni e l’efficienza del caching, questo valore viene aggiornato ogni volta che viene apportata una modifica alla sandbox. |

## Cercare una sandbox {#lookup}

Puoi cercare un singolo sandbox effettuando una richiesta GET che include i `name` nel percorso della richiesta.

**Formato API**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La `name` della sandbox che si desidera cercare. |

**Richiesta**

La richiesta seguente recupera una sandbox denominata &quot;dev-2&quot;.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Risposta**

Una risposta corretta restituisce i dettagli della sandbox, inclusa la relativa `name`, `title`, `state`e `type`.

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
| `state` | Lo stato di elaborazione corrente della sandbox. Lo stato di una sandbox può essere uno dei seguenti: <ul><li>**creazione**: La sandbox è stata creata, ma viene comunque fornita dal sistema.</li><li>**attivo**: La sandbox viene creata e attiva.</li><li>**fallito**: A causa di un errore, il sistema non è in grado di eseguire il provisioning della sandbox ed è disabilitato.</li><li>**cancellato**: La sandbox è stata disabilitata manualmente.</li></ul> |
| `type` | Il tipo di sandbox. Gli attuali tipi di sandbox supportati includono: `development` e `production`. |
| `isDefault` | Proprietà booleana che indica se questa sandbox è la sandbox predefinita per l’organizzazione. In genere si tratta della sandbox di produzione. |
| `eTag` | Identificatore per una versione specifica della sandbox. Utilizzato per il controllo delle versioni e l’efficienza del caching, questo valore viene aggiornato ogni volta che viene apportata una modifica alla sandbox. |

## Creare una sandbox {#create}

>[!NOTE]
>
>Quando crei una nuova sandbox, devi prima aggiungerla al tuo profilo di prodotto in [Adobe Admin Console](https://adminconsole.adobe.com/) prima di iniziare a utilizzare la nuova sandbox. Consulta la documentazione su [gestione delle autorizzazioni per un profilo di prodotto](../../access-control/ui/permissions.md) per informazioni su come eseguire il provisioning di una sandbox a un profilo di prodotto.

Puoi creare una nuova sandbox di sviluppo o produzione effettuando una richiesta di POST al `/sandboxes` punto finale.

### Creare una sandbox di sviluppo

Per creare una sandbox di sviluppo, devi fornire un `type` attributo con valore di `development` nel payload della richiesta.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Una risposta corretta restituisce i dettagli della nuova sandbox creata, mostrando che la relativa `state` è &quot;creazione&quot;.

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
>Le sandbox richiedono circa 30 secondi per essere fornite dal sistema, dopo di che il loro `state` diventerà &quot;attivo&quot; o &quot;non riuscito&quot;.

### Creare una sandbox di produzione

Per creare una sandbox di produzione, devi fornire un `type` attributo con valore di `production` nel payload della richiesta.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Una risposta corretta restituisce i dettagli della nuova sandbox creata, mostrando che la relativa `state` è &quot;creazione&quot;.

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
>Le sandbox richiedono circa 30 secondi per essere fornite dal sistema, dopo di che il loro `state` diventerà &quot;attivo&quot; o &quot;non riuscito&quot;.

## Aggiornare una sandbox {#put}

È possibile aggiornare uno o più campi in una sandbox effettuando una richiesta di PATCH che include i `name` nel percorso della richiesta e nella proprietà da aggiornare nel payload della richiesta.

>[!NOTE]
>
>Attualmente solo una sandbox `title` può essere aggiornata.

**Formato API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La `name` della sandbox che si desidera aggiornare. |

**Richiesta**

La seguente richiesta aggiorna il `title` della sandbox denominata &quot;acme&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Le sandbox hanno una funzione di &quot;reimpostazione di fabbrica&quot; che elimina tutte le risorse non predefinite da una sandbox. Puoi reimpostare una sandbox effettuando una richiesta di PUT che include le sandbox di `name` nel percorso della richiesta.

**Formato API**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La `name` della sandbox che si desidera reimpostare. |
| `validationOnly` | Un parametro facoltativo che consente di eseguire un controllo pre-volo sull’operazione di ripristino della sandbox senza effettuare la richiesta effettiva. Imposta questo parametro su `validationOnly=true` per verificare se la sandbox che stai per reimpostare contiene dati di condivisione di segmenti, Adobe Analytics, Adobe Audience Manager o. |

**Richiesta**

La richiesta seguente reimposta una sandbox denominata &quot;acme-dev&quot;.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme-dev?validationOnly=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `action` | Questo parametro deve essere fornito nel payload della richiesta con un valore di &quot;reset&quot; per reimpostare la sandbox. |

**Risposta**

>[!NOTE]
>
>Una volta reimpostata la sandbox, il sistema impiega circa 30 secondi per effettuare il provisioning.

Una risposta corretta restituisce i dettagli della sandbox aggiornata, mostrando che `state` è &quot;reimpostazione&quot;.

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

La sandbox di produzione predefinita e tutte le sandbox di produzione create dall’utente non possono essere reimpostate se il grafico di identità ospitato al suo interno viene utilizzato anche da Adobe Analytics per [Analisi multidispositivo (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=it) o se il grafico di identità ospitato al suo interno viene utilizzato anche da Adobe Audience Manager per [Destinazioni basate su persone (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=it) funzionalità.

Di seguito è riportato un elenco di possibili eccezioni che potrebbero impedire la reimpostazione di una sandbox:

```json
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2074-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2075-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature, as well by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2076-400"
},
{
    "status": 400,
    "title": "Warning: Sandbox `{SANDBOX_NAME}` is used for bi-directional segment sharing with Adobe Audience Manager or Audience Core Service.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2077-400"
}
```

Puoi procedere alla reimpostazione di una sandbox di produzione utilizzata per la condivisione di segmenti bidirezionale con [!DNL Audience Manager] o [!DNL Audience Core Service] aggiungendo la `ignoreWarnings` alla richiesta.

**Formato API**

```http
PUT /sandboxes/{SANDBOX_NAME}?ignoreWarnings=true
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La `name` della sandbox che si desidera reimpostare. |
| `ignoreWarnings` | Un parametro opzionale che consente di saltare il controllo di convalida e forzare la reimpostazione di una sandbox di produzione utilizzata per la condivisione di segmenti bidirezionale con [!DNL Audience Manager] o [!DNL Audience Core Service]. Questo parametro non può essere applicato a una sandbox di produzione predefinita. |

**Richiesta**

La richiesta seguente reimposta una sandbox di produzione denominata &quot;acme&quot;.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

**Risposta**

Una risposta corretta restituisce i dettagli della sandbox aggiornata, mostrando che `state` è &quot;reimpostazione&quot;.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "resetting",
    "type": "production",
    "region": "VA7"
}
```

## Eliminare una sandbox {#delete}

>[!IMPORTANT]
>
>Impossibile eliminare la sandbox di produzione predefinita.

È possibile eliminare una sandbox effettuando una richiesta di DELETE che include le sandbox di `name` nel percorso della richiesta.

>[!NOTE]
>
>L’esecuzione di questa chiamata API aggiorna la sandbox di `status` su &quot;cancellato&quot; e lo disattiva. Le richieste GET possono ancora recuperare i dettagli della sandbox dopo che è stata eliminata.

**Formato API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La `name` della sandbox da eliminare. |
| `validationOnly` | Un parametro facoltativo che consente di eseguire un controllo pre-volo sull’operazione di eliminazione della sandbox senza effettuare la richiesta effettiva. Imposta questo parametro su `validationOnly=true` per verificare se la sandbox che stai per reimpostare contiene dati di condivisione di segmenti, Adobe Analytics, Adobe Audience Manager o. |
| `ignoreWarnings` | Un parametro opzionale che consente di saltare il controllo di convalida e forzare l’eliminazione di una sandbox di produzione creata dall’utente utilizzata per la condivisione di segmenti bidirezionali con [!DNL Audience Manager] o [!DNL Audience Core Service]. Questo parametro non può essere applicato a una sandbox di produzione predefinita. |

**Richiesta**

La richiesta seguente elimina una sandbox di produzione denominata &quot;acme&quot;.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Risposta**

Una risposta corretta restituisce i dettagli aggiornati della sandbox, indicando che la relativa `state` è &quot;cancellato&quot;.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
