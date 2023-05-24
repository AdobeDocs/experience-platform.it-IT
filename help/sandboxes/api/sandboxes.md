---
keywords: Experience Platform;home;argomenti popolari;guida per sviluppatori sandbox
solution: Experience Platform
title: Endpoint API per la gestione delle sandbox
description: L’endpoint /sandbox nell’API Sandbox consente di gestire in modo programmatico le sandbox in Adobe Experience Platform.
exl-id: 0ff653b4-3e31-4ea5-a22e-07e18795f73e
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1488'
ht-degree: 4%

---

# Endpoint di gestione sandbox

Le sandbox in Adobe Experience Platform forniscono ambienti di sviluppo isolati che consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sull’ambiente di produzione. Il `/sandboxes` endpoint nella [!DNL Sandbox] API consente di gestire in modo programmatico le sandbox in Platform.

## Introduzione

L’endpoint API utilizzato in questa guida fa parte del [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Prima di continuare, controlla [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida per la lettura delle chiamate API di esempio di questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recuperare un elenco di sandbox {#list}

Per elencare tutte le sandbox appartenenti alla tua organizzazione (attive o meno), devi effettuare una richiesta GET al `/sandboxes` endpoint.

**Formato API**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Parametri di query facoltativi in base ai quali filtrare i risultati. Consulta la sezione su [parametri di query](./appendix.md#query) per ulteriori informazioni. |

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

In caso di esito positivo, la risposta restituisce un elenco di sandbox appartenenti alla tua organizzazione, inclusi dettagli quali `name`, `title`, `state`, e `type`.

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
| `state` | Lo stato di elaborazione corrente della sandbox. Lo stato di una sandbox può essere uno dei seguenti: <br/><ul><li>`creating`: la sandbox è stata creata ma è ancora in fase di provisioning da parte del sistema.</li><li>`active`: la sandbox viene creata e attivata.</li><li>`failed`: a causa di un errore, non è stato possibile eseguire il provisioning della sandbox da parte del sistema ed è disabilitata.</li><li>`deleted`: la sandbox è stata disabilitata manualmente.</li></ul> |
| `type` | Il tipo di sandbox. I tipi di sandbox attualmente supportati includono `development` e `production`. |
| `isDefault` | Una proprietà booleana che indica se questa sandbox è la sandbox di produzione predefinita per l’organizzazione. |
| `eTag` | Identificatore di una versione specifica della sandbox. Utilizzato per il controllo delle versioni e l’efficienza della memorizzazione nella cache, questo valore viene aggiornato ogni volta che viene apportata una modifica alla sandbox. |

## Cercare una sandbox {#lookup}

Per cercare una singola sandbox, devi eseguire una richiesta GET che includa la `name` nel percorso della richiesta.

**Formato API**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | Il `name` della sandbox che desideri cercare. |

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

In caso di esito positivo, la risposta restituisce i dettagli della sandbox, compresi i relativi `name`, `title`, `state`, e `type`.

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
| `state` | Lo stato di elaborazione corrente della sandbox. Lo stato di una sandbox può essere uno dei seguenti: <ul><li>**creazione**: la sandbox è stata creata ma è ancora in fase di provisioning da parte del sistema.</li><li>**attivo**: la sandbox viene creata e attivata.</li><li>**non riuscito**: a causa di un errore, non è stato possibile eseguire il provisioning della sandbox da parte del sistema ed è disabilitata.</li><li>**eliminato**: la sandbox è stata disabilitata manualmente.</li></ul> |
| `type` | Il tipo di sandbox. I tipi di sandbox attualmente supportati includono: `development` e `production`. |
| `isDefault` | Una proprietà booleana che indica se questa sandbox è la sandbox predefinita per l’organizzazione. In genere si tratta della sandbox di produzione. |
| `eTag` | Identificatore di una versione specifica della sandbox. Utilizzato per il controllo delle versioni e l’efficienza della memorizzazione nella cache, questo valore viene aggiornato ogni volta che viene apportata una modifica alla sandbox. |

## Creare una sandbox {#create}

>[!NOTE]
>
>Quando crei una nuova sandbox, devi prima aggiungerla al tuo profilo di prodotto in [Adobe Admin Console](https://adminconsole.adobe.com/) prima di iniziare a utilizzare la nuova sandbox. Consulta la documentazione su [gestione delle autorizzazioni per un profilo di prodotto](../../access-control/ui/permissions.md) per informazioni su come effettuare il provisioning di una sandbox per un profilo di prodotto.

Per creare una nuova sandbox di sviluppo o produzione, devi effettuare una richiesta POST al `/sandboxes` endpoint.

### Creare una sandbox di sviluppo

Per creare una sandbox di sviluppo, devi fornire una `type` attributo con valore `development` nel payload della richiesta.

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

In caso di esito positivo, la risposta restituisce i dettagli della sandbox appena creata, mostrando che il relativo `state` è &quot;creazione&quot;.

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
>Il provisioning delle sandbox richiede all’incirca 30 secondi dal sistema, dopodiché `state` diventerà &quot;attivo&quot; o &quot;non riuscito&quot;.

### Creare una sandbox di produzione

Per creare una sandbox di produzione, devi fornire una `type` attributo con valore `production` nel payload della richiesta.

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

In caso di esito positivo, la risposta restituisce i dettagli della sandbox appena creata, mostrando che il relativo `state` è &quot;creazione&quot;.

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
>Il provisioning delle sandbox richiede all’incirca 30 secondi dal sistema, dopodiché `state` diventerà &quot;attivo&quot; o &quot;non riuscito&quot;.

## Aggiornare una sandbox {#put}

Per aggiornare uno o più campi in una sandbox, devi eseguire una richiesta PATCH che includa i `name` nel percorso della richiesta e nella proprietà da aggiornare nel payload della richiesta.

>[!NOTE]
>
>Attualmente solo di una sandbox `title` può essere aggiornata.

**Formato API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | Il `name` della sandbox da aggiornare. |

**Richiesta**

La richiesta seguente aggiorna il `title` proprietà della sandbox denominata &quot;acme&quot;.

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

Le sandbox dispongono di una funzione di &quot;ripristino di fabbrica&quot; che elimina tutte le risorse non predefinite da una sandbox. Per reimpostare una sandbox, effettua una richiesta PUT che include i `name` nel percorso della richiesta.

**Formato API**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | Il `name` della sandbox da reimpostare. |
| `validationOnly` | Un parametro opzionale che consente di eseguire un controllo pre-volo sull’operazione di ripristino della sandbox senza effettuare la richiesta effettiva. Imposta questo parametro su `validationOnly=true` per verificare se la sandbox che stai per ripristinare contiene dati di condivisione di Adobe Analytics, Adobe Audience Manager o segmenti. |

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

In caso di esito positivo, la risposta restituisce i dettagli della sandbox aggiornata, mostrando che il relativo `state` è &quot;resetting&quot; (ripristino).

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

La sandbox di produzione predefinita e tutte le sandbox di produzione create dall’utente non possono essere reimpostate se il grafico delle identità ospitato al suo interno è utilizzato anche da Adobe Analytics per [Analisi multidispositivo (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=it) o se il grafo delle identità ospitato al suo interno è utilizzato anche da Adobe Audience Manager per [Destinazioni basate su persone (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=it) funzionalità.

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

Puoi procedere con il ripristino di una sandbox di produzione utilizzata per la condivisione bidirezionale dei segmenti con [!DNL Audience Manager] o [!DNL Audience Core Service] aggiungendo il `ignoreWarnings` parametro della richiesta.

**Formato API**

```http
PUT /sandboxes/{SANDBOX_NAME}?ignoreWarnings=true
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | Il `name` della sandbox da reimpostare. |
| `ignoreWarnings` | Un parametro opzionale che consente di saltare il controllo di convalida e forzare il ripristino di una sandbox di produzione utilizzata per la condivisione bidirezionale dei segmenti con [!DNL Audience Manager] o [!DNL Audience Core Service]. Questo parametro non può essere applicato a una sandbox di produzione predefinita. |

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

In caso di esito positivo, la risposta restituisce i dettagli della sandbox aggiornata, mostrando che il relativo `state` è &quot;resetting&quot; (ripristino).

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

Per eliminare una sandbox, devi eseguire una richiesta DELETE che includa la `name` nel percorso della richiesta.

>[!NOTE]
>
>Con questa chiamata API vengono aggiornati i `status` su &quot;deleted&quot; e la disattiva. Le richieste GET possono comunque recuperare i dettagli della sandbox anche dopo la sua eliminazione.

**Formato API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{SANDBOX_NAME}` | Il `name` della sandbox da eliminare. |
| `validationOnly` | Parametro facoltativo che consente di eseguire un controllo preliminare sull’operazione di eliminazione sandbox senza effettuare la richiesta effettiva. Imposta questo parametro su `validationOnly=true` per verificare se la sandbox che stai per ripristinare contiene dati di condivisione di Adobe Analytics, Adobe Audience Manager o segmenti. |
| `ignoreWarnings` | Un parametro opzionale che consente di saltare il controllo di convalida e di forzare l’eliminazione di una sandbox di produzione creata dall’utente e utilizzata per la condivisione bidirezionale dei segmenti con [!DNL Audience Manager] o [!DNL Audience Core Service]. Questo parametro non può essere applicato a una sandbox di produzione predefinita. |

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

In caso di esito positivo, la risposta restituisce i dettagli aggiornati della sandbox, mostrando che il relativo `state` è &quot;cancellato&quot;.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
