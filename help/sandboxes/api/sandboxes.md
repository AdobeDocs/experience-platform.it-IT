---
keywords: Experience Platform;home;argomenti popolari;guida per sviluppatori sandbox
solution: Experience Platform
title: Endpoint API per la gestione delle sandbox
description: L’endpoint /sandbox nell’API Sandbox consente di gestire in modo programmatico le sandbox in Adobe Experience Platform.
role: Developer
exl-id: 0ff653b4-3e31-4ea5-a22e-07e18795f73e
source-git-commit: c15b24990835746a51a50a3e7e7b6a85701c0eb9
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 4%

---

# Endpoint di gestione sandbox

Le sandbox in Adobe Experience Platform forniscono ambienti di sviluppo isolati che consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sull’ambiente di produzione. L&#39;endpoint `/sandboxes` nell&#39;API [!DNL Sandbox] consente di gestire in modo programmatico le sandbox in Platform.

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39;[[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e per le informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recuperare un elenco di sandbox {#list}

Per elencare tutte le sandbox appartenenti alla tua organizzazione (attive o meno), devi eseguire una richiesta GET all&#39;endpoint `/sandboxes`.

**Formato API**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Parametri di query facoltativi in base ai quali filtrare i risultati. Per ulteriori informazioni, vedere la sezione relativa ai [parametri di query](./appendix.md#query). |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di sandbox appartenenti all&#39;organizzazione, inclusi dettagli quali `name`, `title`, `state` e `type`.

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
| `state` | Lo stato di elaborazione corrente della sandbox. Lo stato di una sandbox può essere uno dei seguenti: <br/><ul><li>`creating`: la sandbox è stata creata, ma è ancora in corso il provisioning da parte del sistema.</li><li>`active`: la sandbox è stata creata ed è attiva.</li><li>`failed`: a causa di un errore, non è stato possibile eseguire il provisioning della sandbox da parte del sistema ed è disabilitato.</li><li>`deleted`: Sandbox disabilitata manualmente.</li></ul> |
| `type` | Il tipo di sandbox. I tipi di sandbox attualmente supportati sono `development` e `production`. |
| `isDefault` | Una proprietà booleana che indica se questa sandbox è la sandbox di produzione predefinita per l’organizzazione. |
| `eTag` | Identificatore di una versione specifica della sandbox. Utilizzato per il controllo delle versioni e l’efficienza della memorizzazione nella cache, questo valore viene aggiornato ogni volta che viene apportata una modifica alla sandbox. |

## Cercare una sandbox {#lookup}

Per cercare una singola sandbox, devi eseguire una richiesta GET che includa la proprietà `name` della sandbox nel percorso della richiesta.

**Formato API**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La proprietà `name` della sandbox da cercare. |

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

In caso di esito positivo, la risposta restituisce i dettagli della sandbox, inclusi `name`, `title`, `state` e `type`.

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
| `state` | Lo stato di elaborazione corrente della sandbox. Lo stato di una sandbox può essere uno dei seguenti: <ul><li>**creazione**: la sandbox è stata creata, ma è ancora in fase di provisioning da parte del sistema.</li><li>**active**: la sandbox è stata creata ed è attiva.</li><li>**non riuscito**: a causa di un errore, non è stato possibile eseguire il provisioning della sandbox da parte del sistema ed è disabilitato.</li><li>**eliminato**: sandbox disabilitata manualmente.</li></ul> |
| `type` | Il tipo di sandbox. I tipi di sandbox attualmente supportati sono: `development` e `production`. |
| `isDefault` | Una proprietà booleana che indica se questa sandbox è la sandbox predefinita per l’organizzazione. In genere si tratta della sandbox di produzione. |
| `eTag` | Identificatore di una versione specifica della sandbox. Utilizzato per il controllo delle versioni e l’efficienza della memorizzazione nella cache, questo valore viene aggiornato ogni volta che viene apportata una modifica alla sandbox. |

## Creare una sandbox {#create}

>[!NOTE]
>
>Quando viene creata una nuova sandbox, devi prima aggiungere la nuova sandbox al tuo profilo di prodotto in [Adobe Admin Console](https://adminconsole.adobe.com/) prima di poter iniziare a utilizzare la nuova sandbox. Per informazioni su come eseguire il provisioning di una sandbox per un profilo di prodotto, consulta la documentazione su [gestione delle autorizzazioni per un profilo di prodotto](../../access-control/ui/permissions.md).

Per creare una nuova sandbox di sviluppo o produzione, devi eseguire una richiesta POST all&#39;endpoint `/sandboxes`.

### Creare una sandbox di sviluppo

Per creare una sandbox di sviluppo, devi fornire un attributo `type` con il valore `development` nel payload della richiesta.

**Formato API**

```http
POST /sandboxes
```

**Richiesta**

La richiesta seguente crea una nuova sandbox di sviluppo denominata &quot;acme-dev&quot;.

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
| `name` | Identificatore che verrà utilizzato per accedere alla sandbox nelle richieste future. Questo valore deve essere univoco e si consiglia di renderlo il più descrittivo possibile. Questo valore non può contenere spazi o caratteri speciali. |
| `title` | Nome leggibile utilizzato a scopo di visualizzazione nell’interfaccia utente di Platform. |
| `type` | Tipo di sandbox da creare. Per una sandbox non di produzione, questo valore deve essere `development`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della sandbox appena creata, mostrando che il relativo `state` è in fase di &quot;creazione&quot;.

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
>Il provisioning delle sandbox richiede circa 30 secondi dal sistema, dopo di che i relativi `state` diventeranno &quot;attivi&quot; o &quot;non riusciti&quot;.

### Creare una sandbox di produzione

Per creare una sandbox di produzione, devi fornire un attributo `type` con il valore di `production` nel payload della richiesta.

**Formato API**

```http
POST /sandboxes
```

**Richiesta**

La richiesta seguente crea una nuova sandbox di produzione denominata &quot;acme&quot;.

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
| `name` | Identificatore che verrà utilizzato per accedere alla sandbox nelle richieste future. Questo valore deve essere univoco e si consiglia di renderlo il più descrittivo possibile. Questo valore non può contenere spazi o caratteri speciali. |
| `title` | Nome leggibile utilizzato a scopo di visualizzazione nell’interfaccia utente di Platform. |
| `type` | Tipo di sandbox da creare. Per una sandbox di produzione, questo valore deve essere `production`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della sandbox appena creata, mostrando che il relativo `state` è in fase di &quot;creazione&quot;.

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
>Il provisioning delle sandbox richiede circa 30 secondi dal sistema, dopo di che i relativi `state` diventeranno &quot;attivi&quot; o &quot;non riusciti&quot;.

## Aggiornare una sandbox {#put}

Per aggiornare uno o più campi in una sandbox, devi eseguire una richiesta PATCH che includa il `name` della sandbox nel percorso della richiesta e la proprietà da aggiornare nel payload della richiesta.

>[!NOTE]
>
>Attualmente è possibile aggiornare solo la proprietà `title` di una sandbox.

**Formato API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La proprietà `name` della sandbox da aggiornare. |

**Richiesta**

La richiesta seguente aggiorna la proprietà `title` della sandbox denominata &quot;acme&quot;.

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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 (OK) con i dettagli della sandbox appena aggiornata.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "active",
    "type": "production",
    "region": "VA7"
}
```

## Ripristinare una sandbox {#reset}

Le sandbox dispongono di una funzione di &quot;ripristino di fabbrica&quot; che elimina tutte le risorse non predefinite da una sandbox. Per reimpostare una sandbox, devi eseguire una richiesta PUT che includa nel percorso della richiesta il valore `name` della sandbox.

**Formato API**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La proprietà `name` della sandbox da reimpostare. |
| `validationOnly` | Un parametro opzionale che consente di eseguire un controllo pre-volo sull’operazione di ripristino della sandbox senza effettuare la richiesta effettiva. Imposta questo parametro su `validationOnly=true` per verificare se la sandbox che stai per reimpostare contiene dati di condivisione di segmenti, Adobe Analytics o Adobe Audience Manager. |

**Richiesta**

La richiesta seguente ripristina una sandbox denominata &quot;acme-dev&quot;.

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
| `action` | Per ripristinare la sandbox, questo parametro deve essere fornito nel payload della richiesta con il valore &quot;reset&quot;. |

**Risposta**

>[!NOTE]
>
>Una volta reimpostata la sandbox, il provisioning da parte del sistema richiede circa 30 secondi.

In caso di esito positivo, la risposta restituisce i dettagli della sandbox aggiornata, mostrando che il relativo `state` è &quot;resettato&quot;.

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

La sandbox di produzione predefinita e tutte le sandbox di produzione create dall&#39;utente non possono essere reimpostate se il grafo delle identità ospitato al suo interno è utilizzato anche da Adobe Analytics per la funzione [Cross Device Analytics (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=it) oppure se il grafo delle identità ospitato al suo interno è utilizzato anche da Adobe Audience Manager per la funzione [People Based Destinations (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=it).

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

È possibile procedere alla reimpostazione di una sandbox di produzione utilizzata per la condivisione bidirezionale dei segmenti con [!DNL Audience Manager] o [!DNL Audience Core Service] aggiungendo il parametro `ignoreWarnings` alla richiesta.

**Formato API**

```http
PUT /sandboxes/{SANDBOX_NAME}?ignoreWarnings=true
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | La proprietà `name` della sandbox da reimpostare. |
| `ignoreWarnings` | Parametro facoltativo che consente di ignorare il controllo di convalida e forzare la reimpostazione di una sandbox di produzione utilizzata per la condivisione bidirezionale dei segmenti con [!DNL Audience Manager] o [!DNL Audience Core Service]. Questo parametro non può essere applicato a una sandbox di produzione predefinita. |

**Richiesta**

La richiesta seguente ripristina una sandbox di produzione denominata &quot;acme&quot;.

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

In caso di esito positivo, la risposta restituisce i dettagli della sandbox aggiornata, mostrando che il relativo `state` è &quot;resettato&quot;.

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
>Non è possibile eliminare la sandbox di produzione predefinita.

Per eliminare una sandbox, devi eseguire una richiesta DELETE che includa nel percorso della richiesta il valore `name` della sandbox.

>[!NOTE]
>
>Con questa chiamata API, la proprietà `status` della sandbox viene aggiornata a &quot;eliminata&quot; e disattivata. Le richieste GET possono comunque recuperare i dettagli della sandbox anche dopo la sua eliminazione.

**Formato API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | `name` della sandbox da eliminare. |
| `validationOnly` | Parametro facoltativo che consente di eseguire un controllo preliminare sull’operazione di eliminazione sandbox senza effettuare la richiesta effettiva. Imposta questo parametro su `validationOnly=true` per verificare se la sandbox che stai per reimpostare contiene dati di condivisione di segmenti, Adobe Analytics o Adobe Audience Manager. |
| `ignoreWarnings` | Parametro facoltativo che consente di ignorare il controllo di convalida e forzare l&#39;eliminazione di una sandbox di produzione creata dall&#39;utente e utilizzata per la condivisione bidirezionale dei segmenti con [!DNL Audience Manager] o [!DNL Audience Core Service]. Questo parametro non può essere applicato a una sandbox di produzione predefinita. |

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

In caso di esito positivo, la risposta restituisce i dettagli aggiornati della sandbox, mostrando che il relativo `state` è &quot;eliminato&quot;.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
