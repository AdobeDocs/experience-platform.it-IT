---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creazione di integrazioni ETL
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '4102'
ht-degree: 0%

---


# Sviluppo di integrazioni ETL per  Adobe Experience Platform

La guida all&#39;integrazione ETL descrive i passaggi generali per la creazione di connettori sicuri e ad alte prestazioni per [!DNL Experience Platform] l&#39;inserimento dei dati in [!DNL Platform].


- [!DNL Catalog](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)
- [!DNL Data Access](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)
- [!DNL Data Ingestion](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [API di autenticazione e autorizzazione](../tutorials/authentication.md)
- [!DNL Schema Registry](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)

Questa guida include anche chiamate API di esempio da utilizzare per la progettazione di un connettore ETL, con collegamenti alla documentazione che delinea ogni [!DNL Experience Platform] servizio e l&#39;utilizzo della relativa API, in modo più dettagliato.

Un&#39;integrazione di esempio è disponibile [!DNL GitHub] tramite il codice [di riferimento per l&#39;integrazione dell&#39;ecosistema](https://github.com/adobe/acp-data-services-etl-reference) ETL nella [!DNL Apache] versione della licenza 2.0.

## Flusso di lavoro

Il seguente diagramma di flusso di lavoro fornisce una panoramica di alto livello sull’integrazione di componenti di  Adobe Experience Platform con un’applicazione e un connettore ETL.

![](images/etl.png)

## Componenti per Adobi Experience Platform 

Nelle integrazioni di connettori ETL sono coinvolti più componenti  Experience Platform. L&#39;elenco seguente illustra diversi componenti e funzionalità chiave:

- **Adobe  Identity Management System (IMS)** - Fornisce il framework per l&#39;autenticazione  servizi Adobe.
- **Organizzazione** IMS - Un&#39;entità aziendale che può possedere o concedere in licenza prodotti e servizi e consentire l&#39;accesso ai propri membri.
- **Utente** IMS - Membri di un&#39;organizzazione IMS. La relazione tra l’organizzazione e l’utente è molto complessa.
- **[!DNL Sandbox]** - Una partizione virtuale una singola [!DNL Platform] istanza, per aiutare a sviluppare e sviluppare applicazioni di esperienza digitale.
- **Rilevamento** dati - Registra i metadati dei dati acquisiti e trasformati in [!DNL Experience Platform].
- **[!DNL Data Access]** - Fornisce agli utenti un&#39;interfaccia per accedere ai loro dati in [!DNL Experience Platform].
- **[!DNL Data Ingestion]** - Invia dati a [!DNL Experience Platform] con [!DNL Data Ingestion] le API.
- **[!DNL Schema Registry]** - Definisce e memorizza lo schema che descrive la struttura dei dati da utilizzare in [!DNL Experience Platform].

## Getting started with [!DNL Experience Platform] APIs

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere o avere a disposizione per eseguire correttamente le chiamate alle [!DNL Experience Platform] API.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione [sulla panoramica della](../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

## Flusso generale utente

Per iniziare, un utente ETL accede all’interfaccia [!DNL Experience Platform] utente (UI) e crea dei set di dati per l’inserimento utilizzando un connettore standard o un connettore di servizio push.

Nell&#39;interfaccia utente, l&#39;utente crea il set di dati di output selezionando uno schema di set di dati. La scelta dello schema dipende dal tipo di dati (record o serie temporali) in cui viene assimilato [!DNL Platform]. Facendo clic sulla scheda Schemi all&#39;interno dell&#39;interfaccia utente, l&#39;utente potrà visualizzare tutti gli schemi disponibili, incluso il tipo di comportamento supportato dallo schema.

Nello strumento ETL, l&#39;utente inizierà a progettare le trasformazioni di mappatura dopo aver configurato la connessione appropriata (utilizzando le proprie credenziali). Si presume che lo strumento ETL abbia già installato [!DNL Experience Platform] dei connettori (processo non definito in questa Guida all&#39;integrazione).

Nel flusso di lavoro [](./workflow.md)ETL sono stati forniti dei modelli per uno strumento e un flusso di lavoro ETL di esempio. Anche se gli strumenti ETL possono essere diversi in termini di formato, la maggior parte presenta funzionalità simili.

>[!NOTE]
>
>Il connettore ETL deve specificare un filtro di marca temporale che contrassegna la data in cui inserire i dati e l&#39;offset (cioè la finestra per la quale leggere i dati). Lo strumento ETL dovrebbe supportare l’utilizzo di questi due parametri in questa o in un’altra interfaccia utente pertinente. In  Adobe Experience Platform, questi parametri saranno mappati sulle date disponibili (se presenti) o sulla data acquisita presente nell&#39;oggetto batch del dataset.

### Visualizza elenco di set di dati

Utilizzando l&#39;origine dei dati per la mappatura, è possibile ottenere un elenco di tutti i set di dati disponibili tramite [!DNL Catalog API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

Potete inviare una singola richiesta API per visualizzare tutti i set di dati disponibili (ad es. `GET /dataSets`), in cui si consiglia di includere parametri di query che limitano la dimensione della risposta.

Nei casi in cui vengono richieste informazioni _complete_ sui dataset, il payload di risposta può raggiungere oltre 3 GB di dimensione, il che può rallentare le prestazioni complessive. Pertanto, l&#39;utilizzo di parametri di query per filtrare solo le informazioni necessarie renderà [!DNL Catalog] le query più efficienti.

#### Filtro elenco

Quando filtrate le risposte, potete utilizzare più filtri in una singola chiamata separando i parametri con una e commerciale (`&`). Alcuni parametri di query accettano elenchi di valori separati da virgole, ad esempio il filtro &quot;proprietà&quot; nella richiesta di esempio seguente.

[!DNL Catalog] le risposte vengono misurate automaticamente in base ai limiti configurati, tuttavia il parametro di query &quot;limit&quot; può essere utilizzato per personalizzare i vincoli e limitare il numero di oggetti restituiti. I limiti di risposta preconfigurati [!DNL Catalog] sono:

- Se non viene specificato un parametro di limite, il numero massimo di oggetti per payload di risposta è 20.
- Il limite globale per tutte le altre [!DNL Catalog] query è 100 oggetti.
- Per le query del set di dati, se si richiede osservableSchema utilizzando il parametro query delle proprietà, il numero massimo di set di dati restituito è 20.
- I parametri di limite non validi (inclusi `limit=0`) vengono soddisfatti con un errore HTTP 400 che traccia i contorni corretti.
- Se i limiti o gli offset vengono passati come parametri di query, hanno la precedenza su quelli passati come intestazioni.

I parametri delle query sono descritti più dettagliatamente nella panoramica [di](../catalog/home.md)Catalog Service.

**Formato API**

```http
GET /catalog/dataSets
GET /catalog/dataSets?{filter1}={value1},{value2}&{filter2}={value3}
```

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3&properties=name,description,schemaRef" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Per esempi dettagliati su come effettuare chiamate al servizio [Catalogo, consultate la panoramica](../catalog/home.md) del servizio [!DNL Catalog API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)Catalogo.

**Risposta**

La risposta include tre (`limit=3`) set di dati che mostrano &quot;name&quot;, &quot;description&quot; e &quot;schemaRef&quot; come indicato dal parametro della `properties` query.

```json
{
    "5b95b155419ec801e6eee780": {
        "name": "Store Transactions",
        "description": "Retails Store Transactions",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c351fa2f5fee300000fa9e8": {
        "name": "Loyalty Members",
        "description": "Loyalty Program Members",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c1823b19e6f400000993885": {
        "name": "Web Traffic",
        "description": "Retail Web Traffic",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2025a705890c6d4a4a06b16f8cf6f4ca",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

### Visualizza schema set di dati

La proprietà &quot;schemaRef&quot; di un dataset contiene un URI che fa riferimento allo schema XDM su cui si basa il dataset. Lo schema XDM (&quot;schemaRef&quot;) rappresenta tutti i campi _potenziali_ che possono essere utilizzati dal dataset, non necessariamente i campi che _sono_ utilizzati (vedere &quot;osservableSchema&quot; di seguito).

Lo schema XDM è lo schema utilizzato per presentare all&#39;utente un elenco di tutti i campi disponibili su cui è possibile scrivere.

Il primo valore &quot;schemaRef.id&quot; nell&#39;oggetto di risposta precedente (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) è un URI che punta a uno schema XDM specifico nell&#39;oggetto [!DNL Schema Registry]. Lo schema può essere recuperato effettuando una richiesta di ricerca (GET) all&#39; [!DNL Schema Registry] API.

>[!NOTE]
>
>La proprietà &quot;schemaRef&quot; sostituisce la proprietà obsoleta &quot;schema&quot;. Se &quot;schemaRef&quot; è assente dal dataset o non contiene un valore, sarà necessario verificare la presenza di una proprietà &quot;schema&quot;. Ciò può essere fatto sostituendo &quot;schemaRef&quot; con &quot;schema&quot; nel parametro di `properties` query della chiamata precedente. Ulteriori dettagli sulla proprietà &quot;schema&quot; sono disponibili nella sezione [DataSet &quot;schema&quot; Proprietà](#dataset-schema-property-deprecated---eol-2019-05-30) che segue.

**Formato API**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**Richiesta**

La richiesta utilizza l’ `id` URI con codifica URL dello schema (il valore dell’attributo &quot;schemaRef.id&quot;) e richiede un’intestazione Accetto.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

Il formato della risposta dipende dal tipo di intestazione Accetto inviato nella richiesta. Anche le richieste di ricerca richiedono che `version` venga incluso nell’intestazione Accetto. Nella tabella seguente sono riportati i contorni disponibili Accetta intestazioni per le ricerche:

| Accetta | Descrizione |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | Richieste elenco (GET), titoli, ID e versioni |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs e allOf risolti, con titoli e descrizioni |
| `application/vnd.adobe.xed+json; version={major version}` | Raw con $ref e allOf, ha titoli e descrizioni |
| `application/vnd.adobe.xed-notext+json; version={major version}` | Raw con $ref e allOf, senza titoli o descrizioni |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs e allOf risolti, senza titoli o descrizioni |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs e allOf risolti, descrittori inclusi |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` e `application/vnd.adobe.xed-full+json; version={major version}` sono le intestazioni Accetta più utilizzate. `application/vnd.adobe.xed-id+json` è preferibile elencare le risorse in [!DNL Schema Registry] quanto restituisce solo &quot;title&quot;, &quot;id&quot; e &quot;version&quot;. `application/vnd.adobe.xed-full+json; version={major version}` è preferibile visualizzare una risorsa specifica (in base al relativo &quot;id&quot;), in quanto restituisce tutti i campi (nidificati sotto &quot;proprietà&quot;), nonché titoli e descrizioni.

**Risposta**

Lo schema JSON restituito descrive la struttura e le informazioni a livello di campo (&quot;tipo&quot;, &quot;formato&quot;, &quot;minimo&quot;, &quot;massimo&quot;, ecc.) dei dati, serializzati come JSON. Se si utilizza un formato di serializzazione diverso da JSON per l&#39;assimilazione (ad esempio Parquet o Scala), la Guida [al Registro di sistema dello](../xdm/tutorials/create-schema-api.md) schema contiene una tabella che mostra il tipo JSON desiderato (&quot;meta:xdmType&quot;) e la corrispondente rappresentazione in altri formati.

Insieme a questa tabella, la Guida per [!DNL Schema Registry] sviluppatori contiene esempi dettagliati di tutte le possibili chiamate che possono essere effettuate utilizzando l&#39; [!DNL Schema Registry] API.

### Proprietà Dataset &quot;schema&quot; (DEPRECATED - EOL 2019-05-30)

I set di dati possono contenere una proprietà &quot;schema&quot; che ora è obsoleta e rimane temporaneamente disponibile per la compatibilità con le versioni precedenti. Ad esempio, una richiesta di elenco (GET) simile a quella effettuata in precedenza, in cui &quot;schema&quot; è stato sostituito con &quot;schemaRef&quot; nel parametro della `properties` query, potrebbe restituire quanto segue:

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

Se la proprietà &quot;schema&quot; di un dataset è popolata, ciò indica che lo schema è uno `/xdms` schema obsoleto e, laddove supportato, il connettore ETL deve utilizzare il valore nella proprietà &quot;schema&quot; con l&#39; `/xdms` endpoint (un endpoint obsoleto nel [!DNL Catalog API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)) per recuperare lo schema legacy.

**Formato API**

```http
GET /catalog/{"schema" property without the "@"}
```

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

>[!NOTE]
>
>Un parametro di query facoltativo `expansion=xdm`indica all&#39;API di espandere completamente e in linea tutti gli schemi di riferimento. È possibile eseguire questa operazione quando si presenta all&#39;utente un elenco di tutti i campi potenziali.

**Risposta**

Analogamente ai passaggi per [visualizzare lo schema](#view-dataset-schema)del set di dati, la risposta contiene uno schema JSON che descrive la struttura e le informazioni a livello di campo dei dati, serializzati come JSON.

>[!NOTE]
>
>Quando il campo &quot;schema&quot; è completamente vuoto o assente, il connettore deve leggere il campo &quot;schemaRef&quot; e utilizzare l&#39;API [del Registro di](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) schema come mostrato nei passaggi precedenti per [visualizzare uno schema](#view-dataset-schema)di set di dati.

### La proprietà &quot;osservableSchema&quot;

La proprietà &quot;osservableSchema&quot; di un set di dati ha una struttura JSON corrispondente a quella del JSON dello schema XDM. &quot;osservableSchema&quot; contiene i campi presenti nei file di input in arrivo. Durante la scrittura dei dati in [!DNL Experience Platform], non è necessario utilizzare tutti i campi dello schema di destinazione. Devono invece fornire solo i campi utilizzati.

Lo schema osservabile è lo schema da utilizzare per la lettura dei dati o la presentazione di un elenco di campi disponibili per la lettura/mappatura.

```json
{
    "598d6e81b2745f000015edcb": {
        "observableSchema": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "name": {
                    "type": "string",
                },
                "age": {
                    "type": "string",
                }
            }
        }
    }
}
```

### Anteprima dati

L’applicazione ETL può fornire una capacità di visualizzare in anteprima i dati ([&quot;Figura 8&quot; nel flusso di lavoro](./workflow.md)ETL). L&#39;API di accesso ai dati offre diverse opzioni per visualizzare l&#39;anteprima dei dati.

Ulteriori informazioni, comprese le istruzioni dettagliate per visualizzare l&#39;anteprima dei dati mediante l&#39;API di accesso ai dati, sono disponibili nell&#39;esercitazione [sull&#39;accesso ai](../data-access/tutorials/dataset-data.md)dati.

### Ottenete i dettagli del dataset utilizzando il parametro di query &quot;proprietà&quot;

Come illustrato nella procedura precedente per [visualizzare un elenco di set di dati](#view-list-of-datasets), è possibile richiedere &quot;file&quot; utilizzando il parametro di query &quot;proprietà&quot;.

Per informazioni dettagliate sulla query dei set di dati e sui filtri di risposta disponibili, consultate la panoramica [del servizio](../catalog/home.md) catalogo.

**Formato API**

```http
GET /catalog/dataSets?limit={value}&properties={value}
```

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=1&properties=files" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Risposta**

La risposta includerà un dataset (`limit=1`) che mostra la proprietà &quot;files&quot;.

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files"
  }
}
```

### Elenca i file di set di dati utilizzando l&#39;attributo &quot;files&quot;

Potete anche utilizzare una richiesta di GET per recuperare i dettagli del file utilizzando l&#39;attributo &quot;files&quot;.

**Formato API**

```http
GET /catalog/dataSets/{DATASET_ID}/views/{VIEW_ID}/files
```

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

**Risposta**

La risposta include l&#39;ID del file del set di dati come proprietà di primo livello, con i dettagli del file contenuti nell&#39;oggetto ID del file del set di dati.

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542749145828,
        "updated": 1542749145828
    },
    "14d5758c107443e1a83c714e56ca79d0-1": {
        "batchId": "14d5758c107443e1a83c714e56ca79d0",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542752699111,
        "updated": 1542752699111
    },
    "ea40946ac03140ec8ac4f25da360620a-1": {
        "batchId": "ea40946ac03140ec8ac4f25da360620a",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542756935535,
        "updated": 1542756935535
    }
}
```

### Recupero dettagli file

Gli ID del file di set di dati restituiti nella risposta precedente possono essere utilizzati in una richiesta di GET per recuperare ulteriori dettagli del file tramite l&#39; [!DNL Data Access] API.

La panoramica [sull&#39;accesso ai](../data-access/home.md) dati contiene dettagli sull&#39;utilizzo dell&#39; [!DNL Data Access] API.

**Formato API**

```http
GET /export/files/{DATASET_FILE_ID}
```

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

**Risposta**

```json
[
    {
    "name": "{FILE_NAME}.parquet",
    "length": 2576,
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet"
            }
        }
    }
]
```

### Anteprima dei dati del file

La proprietà &quot;href&quot; può essere utilizzata per recuperare i dati di anteprima tramite [!DNL Data Access API](../data-access/home.md).

**Formato API**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

La risposta alla richiesta di cui sopra contiene un&#39;anteprima del contenuto del file.

Ulteriori informazioni sull&#39; [!DNL Data Access] API, incluse richieste e risposte dettagliate, sono disponibili nella panoramica [sull&#39;accesso ai](../data-access/home.md)dati.

### Ottenere &quot;fileDescription&quot; dal dataset

Il componente di destinazione come output di dati trasformati, Data Engineer sceglierà un DataSet di output ([&quot;Figura 12&quot; nel flusso di lavoro](workflow.md)ETL). Lo schema XDM è associato al set di dati di output. I dati da scrivere saranno identificati dall&#39;attributo &quot;fileDescription&quot; dell&#39;entità dataset dalle API di rilevamento dati. Queste informazioni possono essere recuperate utilizzando un ID set di dati (`{DATASET_ID}`). La proprietà &quot;fileDescription&quot; nella risposta JSON fornirà le informazioni richieste.

**Formato API**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{DATASET_ID}` | Il `id` valore del set di dati a cui si sta tentando di accedere. |

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/59c93f3da7d0c00000798f68" \
-H "accept: application/json" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
```

**Risposta**

```JSON
{
  "59c93f3da7d0c00000798f68": {
    "version": "1.0.4",
    "fileDescription": {
        "persisted": false,
        "format": "parquet"
    }
  }
}
```

I dati verranno scritti tramite [!DNL Experience Platform] l&#39;API [di inserimento](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)dati.  La scrittura dei dati è un processo asincrono. Quando i dati vengono scritti  Adobe Experience Platform, viene creato un batch contrassegnato come un successo solo dopo che i dati sono stati scritti completamente.

I dati in [!DNL Experience Platform] devono essere scritti sotto forma di file di parquet.

## Fase di esecuzione

All&#39;avvio dell&#39;esecuzione, il connettore (come definito nel componente di origine) leggerà i dati dall&#39; [!DNL Experience Platform] utilizzo del [!DNL Data Access API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml). Il processo di trasformazione leggerà i dati per un determinato intervallo di tempo. Internamente, esegue una query sui batch di set di dati di origine. Durante l&#39;esecuzione di query, utilizzerà un valore parametrizzato (per i dati delle serie temporali, o per i dati incrementali) per la data di inizio e i file di set di dati per tali batch, quindi inizierà a richiedere i dati per tali file di set di dati.

### Trasformazioni di esempio

Il documento di [esempio sulle trasformazioni](./transformations.md) ETL contiene una serie di trasformazioni di esempio, tra cui la gestione dell&#39;identità e le mappature dei tipi di dati. Utilizzate queste trasformazioni per riferimento.

### Leggi dati da [!DNL Experience Platform]

Utilizzando [!DNL Catalog API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), potete recuperare tutti i batch tra un&#39;ora di inizio e una di fine specificate e ordinarli in base all&#39;ordine in cui sono stati creati.

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Per informazioni sul filtro dei batch, consulta l’esercitazione [sull’accesso ai](../data-access/tutorials/dataset-data.md)dati.

### Estrarre i file da un batch

Una volta ottenuto l’ID per il batch che si sta cercando (`{BATCH_ID}`), è possibile recuperare un elenco di file appartenenti a uno specifico batch tramite [!DNL Data Access API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml).  I dettagli per farlo sono disponibili nell&#39;esercitazione [sull&#39;accesso ai](../data-access/tutorials/dataset-data.md)dati.

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

### Accedere ai file utilizzando l&#39;ID file

Utilizzando l&#39;ID univoco di un file (`{FILE_ID`), l&#39; [!DNL Data Access API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) utente può accedere ai dettagli specifici del file, inclusi nome, dimensione in byte e collegamento per scaricarlo.

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key : {API_KEY}"
```

La risposta può puntare a un singolo file o a una directory. Per informazioni dettagliate, consulta l’esercitazione [sull’accesso ai](../data-access/tutorials/dataset-data.md)dati.

### Accedere al contenuto del file

L&#39; [!DNL Data Access API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) opzione può essere utilizzata per accedere al contenuto di un file specifico. Per recuperare il contenuto, viene effettuata una richiesta di GET utilizzando il valore restituito per `_links.self.href` accedere a un file utilizzando l&#39;ID file.

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

La risposta a questa richiesta contiene il contenuto del file. Per ulteriori informazioni, compresi i dettagli sull&#39;impaginazione delle risposte, consulta l&#39;esercitazione [How to Query Data via data access API](../data-access/tutorials/dataset-data.md) tutorial.

### Convalida dei record per la conformità allo schema

Durante la scrittura dei dati, gli utenti possono scegliere di convalidare i dati in base alle regole di convalida definite nello schema XDM. Ulteriori informazioni sulla convalida dello schema sono disponibili nel codice di riferimento per l&#39;integrazione dell&#39;ecosistema [ETL su GitHub](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

Se si utilizza l&#39;implementazione di riferimento trovata in [!DNL GitHub](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md), è possibile attivare la convalida dello schema in questa implementazione utilizzando la proprietà system `-DenableSchemaValidation=true`.

La convalida può essere eseguita per i tipi XDM logici, utilizzando attributi quali `minLength` e `maxlength` per le stringhe, `minimum` e `maximum` per i numeri interi e altro ancora. La guida [per gli sviluppatori API del Registro di](../xdm/api/getting-started.md) schema contiene una tabella che delinea i tipi XDM e le proprietà che possono essere utilizzate per la convalida.

>[!NOTE]
>
>I valori minimo e massimo forniti per vari `integer` tipi sono i valori MIN e MAX che il tipo può supportare, ma questi valori possono essere ulteriormente limitati a valori minimi e massimi scelti.

### Creare un batch

Una volta elaborati i dati, lo strumento ETL li riscrive [!DNL Experience Platform] utilizzando l&#39;API [di inserimento](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)batch. Prima di poter aggiungere dati a un set di dati, questi devono essere collegati a un batch che verrà successivamente caricato in un set di dati specifico.

**Richiesta**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

I dettagli per la creazione di un batch, incluse le richieste di esempio e le risposte, sono disponibili nella panoramica [di inserimento](../ingestion/batch-ingestion/overview.md)batch.

### Scrivi in dataset

Dopo aver creato un nuovo batch, i file possono essere caricati in un set di dati specifico. È possibile pubblicare più file in un batch finché non vengono promossi. I file possono essere caricati utilizzando l&#39;API _di caricamento file_ piccola; tuttavia, se i file sono troppo grandi e il limite del gateway viene superato, potete utilizzare l&#39;API _Caricamento file_ grande. Per informazioni sull’utilizzo di caricamento di file grandi e piccoli, consultate la panoramica [sull’inserimento dei](../ingestion/batch-ingestion/overview.md)batch.

**Richiesta**

I dati in [!DNL Experience Platform] devono essere scritti sotto forma di file di parquet.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{IMS_ORG}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### Contrassegna caricamento batch completato

Dopo aver caricato tutti i file nel batch, il batch può essere segnalato per il completamento. In questo modo, le voci [!DNL Catalog] &quot;DataSetFile&quot; vengono create per i file completati e associate al batch di generazione. Il [!DNL Catalog] batch viene quindi contrassegnato come riuscito, che attiva i flussi a valle per l&#39;acquisizione dei dati disponibili.

I dati verranno prima inseriti nella posizione di pre-produzione  Adobe Experience Platform e quindi spostati nella posizione finale dopo la catalogazione e la convalida. I batch verranno contrassegnati come validi quando tutti i dati vengono spostati in una posizione permanente.

**Richiesta**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

In caso di esito positivo, la risposta restituirà lo stato HTTP 200 OK e il corpo della risposta sarà vuoto.

Lo strumento ETL farà in modo di notare la marca temporale dei set di dati di origine durante la lettura dei dati.

Nella successiva esecuzione della trasformazione, probabilmente per pianificazione o chiamata dell&#39;evento, l&#39;ETL inizierà a richiedere i dati dalla marca temporale precedentemente salvata e tutti i dati in futuro.

### Ottieni stato ultimo batch

Prima di eseguire le nuove attività nello strumento ETL, è necessario assicurarsi che l&#39;ultimo batch sia stato completato correttamente. L&#39; [!DNL Catalog Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) opzione specifica per il batch fornisce i dettagli dei batch pertinenti.

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Risposta**

Le nuove attività possono essere pianificate se il precedente valore &quot;stato&quot; del batch è &quot;successo&quot;, come mostrato di seguito:

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "CLIENT_USER_ID@AdobeID",
    "updatedUser": "CLIENT_USER_ID@AdobeID",
    "updated": 1494349963467,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

### Ottieni stato ultimo batch per ID

È possibile recuperare un singolo stato batch tramite [!DNL Catalog Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) una richiesta di GET utilizzando l&#39; `{BATCH_ID}`. L&#39;ID `{BATCH_ID}` utilizzato corrisponde all&#39;ID restituito al momento della creazione del batch.

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Risposta - Successo**

La risposta seguente mostra un &quot;successo&quot;:

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

**Risposta - Errore**

In caso di errore, gli &quot;errori&quot; possono essere estratti dalla risposta e visualizzati sullo strumento ETL come messaggi di errore.

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "failure",
    "errors": [
        {
            "code": "200",
            "description": "Error in validating schema for file: 'adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv' with errorMessage=adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv is not a Parquet file. expected magic number at tail [80, 65, 82, 49] but found [57, 98, 55, 10] and errorType=java.lang.RuntimeException",
            "rows": []
        }
    ],
    "version": "1.0.1",
    "availableDates": {}
}
```

## Dati ed eventi incrementali e snapshot rispetto ai profili

I dati possono essere rappresentati in due da due matrici, come segue:

| Eventi incrementali | Profili incrementali |
|-------------------------------|----------------------|
| Eventi snapshot (meno probabile) | Profili snapshot |

I dati dell&#39;evento sono generalmente utilizzati quando in ogni riga sono presenti colonne di marca temporale indicizzate.

I dati del profilo sono generalmente quando non è presente una marca temporale nei dati e ogni riga può essere identificata da una chiave primaria o composita.

Per dati incrementali si intendono solo i dati nuovi/aggiornati che entrano nel sistema e che vengono aggiunti ai dati correnti nei set di dati.

I dati snapshot sono quando tutti i dati entrano nel sistema e sostituiscono alcuni o tutti i dati precedenti in un dataset.

Nel caso di eventi incrementali, lo strumento ETL deve utilizzare le date disponibili/creare la data dell&#39;entità batch. Nel caso del servizio push, le date disponibili non saranno presenti, quindi lo strumento utilizzerà la data di creazione/aggiornamento batch per contrassegnare gli incrementi. È necessario elaborare ogni batch di eventi incrementali.

Per i profili incrementali, lo strumento ETL utilizzerà le date create/aggiornate dell&#39;entità batch. Comunemente ogni batch di dati di profilo incrementali è necessario per essere elaborato.

Gli eventi snapshot sono molto meno probabili a causa delle dimensioni ridotte dei dati. Ma se questo fosse necessario, lo strumento ETL deve selezionare solo l&#39;ultimo batch per l&#39;elaborazione.

Quando si utilizzano i profili snapshot, lo strumento ETL dovrà selezionare l&#39;ultimo batch di dati arrivati nel sistema. Ma se il requisito è quello di tenere traccia delle versioni delle modifiche, tutti i batch saranno richiesti per essere elaborati. L&#39;elaborazione della deduplicazione all&#39;interno del processo ETL contribuirà a controllare i costi di storage.

## Riproduzione batch e rielaborazione dati

La riproduzione batch e il ritrattamento dei dati possono essere richiesti nei casi in cui un cliente scopre che negli ultimi &#39;n&#39; giorni, i dati elaborati da ETL non si sono verificati come previsto o che i dati di origine stessi non sono stati corretti.

A tal fine, gli amministratori dei dati del client utilizzeranno l&#39; [!DNL Platform] interfaccia utente per rimuovere i batch che contengono dati danneggiati. Quindi, è probabile che l&#39;ETL debba essere rieseguito, ripopolando con dati corretti. Se l&#39;origine stessa dispone di dati danneggiati, l&#39;ingegnere/amministratore dei dati dovrà correggere i batch di origine e riacquisire i dati (sia nel Adobe Experience Platform  che tramite connettori ETL).

In base al tipo di dati generato, sarà l&#39;ingegnere dei dati a scegliere se rimuovere un singolo batch o tutti i batch da determinati dataset. I dati verranno rimossi/archiviati come indicato nelle [!DNL Experience Platform] linee guida.

È probabile che la funzionalità ETL per eliminare i dati sia importante.

Una volta completata l&#39;eliminazione, gli amministratori client dovranno riconfigurare  Adobe Experience Platform per riavviare l&#39;elaborazione per i servizi di base dal momento in cui i batch vengono eliminati.

## Elaborazione batch simultanea

A discrezione del cliente, gli amministratori/ingegneri dei dati possono decidere di estrarre, trasformare e caricare i dati in modo sequenziale o simultaneo, a seconda delle caratteristiche di un particolare dataset. Questo sarà anche basato sul caso di utilizzo in cui il client esegue il targeting con i dati trasformati.

Ad esempio, se il client è persistente in un archivio di persistenza aggiornabile e la sequenza o l&#39;ordine degli eventi è importante, il client potrebbe dover elaborare rigorosamente i processi con trasformazioni ETL sequenziali.

In altri casi, i dati non ordinati possono essere elaborati da applicazioni/processi a valle che eseguono l&#39;ordinamento interno utilizzando una data e un&#39;ora specificate. In questi casi, le trasformazioni ETL parallele possono essere realizzabili per migliorare i tempi di elaborazione.

Per i batch di origine, dipenderà di nuovo dalla preferenza del cliente e dal vincolo del consumatore. Se i dati di origine possono essere raccolti in parallelo senza tener conto della reggenza/ordinamento di una riga, il processo di trasformazione può creare batch di processi con un livello più elevato di parallelismo (ottimizzazione basata sull&#39;elaborazione fuori ordine). Tuttavia, se la trasformazione deve rispettare i timestamp o modificare l&#39;ordine di precedenza, l&#39;API di accesso ai dati o l&#39;utilità di pianificazione/chiamata dello strumento ETL dovrà garantire che i batch non vengano elaborati in modo non ordinato, ove possibile.

## Rinvio

Il differimento è un processo in cui i dati di input non sono ancora sufficientemente completi per essere inviati ai processi a valle, ma possono essere utilizzati in futuro. I client determineranno la propria tolleranza individuale per la finestra dei dati per future corrispondenze rispetto al costo dell&#39;elaborazione per informare la loro decisione di mettere da parte i dati e rielaborarli nella successiva esecuzione della trasformazione, sperando che possa essere arricchita e riconciliata/cucita in un momento futuro all&#39;interno della finestra di conservazione. Questo ciclo è in corso finché la riga non viene elaborata a sufficienza o si ritiene che sia troppo stantio per continuare a investire in. Ogni iterazione genererà dati differiti, ovvero un superset di tutti i dati differiti nelle iterazioni precedenti.

 Adobe Experience Platform non identifica i dati differiti al momento, pertanto le implementazioni client devono basarsi sulle configurazioni manuali ETL e Dataset per creare un altro dataset nel [!DNL Platform] mirroring del dataset di origine che può essere utilizzato per mantenere i dati differiti. In questo caso, i dati differiti saranno simili ai dati snapshot. In ogni esecuzione della trasformazione ETL, i dati di origine saranno uniti ai dati differiti e inviati per l&#39;elaborazione.

## Changelog

| Data | Azione | Descrizione |
| ---- | ------ | ----------- |
| 2019-01-19 | Proprietà &quot;fields&quot; rimossa dai set di dati | I set di dati in precedenza includevano una proprietà &quot;fields&quot; che conteneva una copia dello schema. Questa funzionalità non deve più essere utilizzata. Se la proprietà &quot;fields&quot; viene trovata, deve essere ignorata e deve essere utilizzata &quot;OsservaSchema&quot; o &quot;schemaRef&quot;. |
| 2019-03-15 | proprietà &quot;schemaRef&quot; aggiunta ai dataset | La proprietà &quot;schemaRef&quot; di un dataset contiene un URI che fa riferimento allo schema XDM su cui si basa il dataset e rappresenta tutti i potenziali campi che possono essere utilizzati dal dataset. |
| 2019-03-15 | Tutti gli identificatori utente finale vengono mappati sulla proprietà &quot;identityMap&quot; | &quot;identityMap&quot; è un&#39;incapsulazione di tutti gli identificatori univoci di un oggetto, come l&#39;ID CRM, l&#39;ECID o l&#39;ID del programma fedeltà. Questa mappa viene utilizzata [!DNL Identity Service](../identity-service/home.md) per risolvere tutte le identità note e anonime di un oggetto, formando un grafico di identità per ogni utente finale. |
| 2019-05-30 | EOL e Rimuovi proprietà &quot;schema&quot; dai set di dati | La proprietà &quot;schema&quot; del dataset ha fornito un collegamento di riferimento allo schema utilizzando l&#39; `/xdms` endpoint obsoleto nell&#39; [!DNL Catalog] API. Questo è stato sostituito da un &quot;schemaRef&quot; che fornisce &quot;id&quot;, &quot;version&quot; e &quot;contentType&quot; dello schema come indicato nella nuova [!DNL Schema Registry] API. |