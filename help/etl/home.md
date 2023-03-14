---
keywords: Experience Platform;home;argomenti popolari;ETL;etl;etl integrazioni;etl integrazioni;ETL integrazioni;Home;popular topic;ETL;etl;etl;etl integrazioni;ETL integrazioni
solution: Experience Platform
title: Sviluppo di integrazioni ETL per Adobe Experience Platform
description: La guida all’integrazione di ETL illustra i passaggi generali per la creazione di connettori sicuri e a elevate prestazioni, ad Experience Platform per l’acquisizione di dati in Platform.
exl-id: 7d29b61c-a061-46f8-a31f-f20e4d725655
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '4075'
ht-degree: 1%

---

# Sviluppo di integrazioni ETL per Adobe Experience Platform

La guida all’integrazione di ETL illustra i passaggi generali per la creazione di connettori sicuri e a elevate prestazioni per [!DNL Experience Platform] e acquisizione di dati in [!DNL Platform].


- [[!DNL Catalog]](https://www.adobe.io/experience-platform-apis/references/catalog/)
- [[!DNL Data Access]](https://www.adobe.io/experience-platform-apis/references/data-access/)
- [[!DNL Data Ingestion]](https://www.adobe.io/experience-platform-apis/references/data-ingestion/)
- [Autenticazione e autorizzazione per le API di Experience Platform](https://www.adobe.com/go/platform-api-authentication-en)
- [[!DNL Schema Registry]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)

Questa guida include anche esempi di chiamate API da utilizzare durante la progettazione di un connettore ETL, con collegamenti alla documentazione che ne descrive ognuna [!DNL Experience Platform] e l&#39;utilizzo della relativa API.

Un esempio di integrazione è disponibile su [!DNL GitHub] tramite [Codice di riferimento per l’integrazione dell’ecosistema ETL](https://github.com/adobe/acp-data-services-etl-reference) sotto [!DNL Apache] Licenza versione 2.0.

## Flusso di lavoro

Il seguente diagramma fornisce una panoramica generale dell&#39;integrazione dei componenti Adobe Experience Platform con un&#39;applicazione ETL e un connettore.

![](images/etl.png)

## Componenti Adobe Experience Platform

Nelle integrazioni del connettore ETL sono coinvolti più componenti di Experience Platform. L’elenco seguente illustra diversi componenti e funzionalità chiave:

- **Sistema Adobe Identity Management (IMS)** : fornisce il framework per l’autenticazione ai servizi Adobe.
- **Organizzazione IMS** - un&#39;entità societaria che può possedere o concedere in licenza prodotti e servizi e consentire l&#39;accesso ai suoi membri.
- **Utente IMS** - Membri di un’organizzazione IMS. La relazione tra organizzazione e utente è variabile da molti a molti.
- **[!DNL Sandbox]** - Una partizione virtuale una singola [!DNL Platform] ad esempio, per sviluppare ed evolvere le applicazioni di esperienza digitale.
- **Individuazione dati** - Registra i metadati dei dati acquisiti e trasformati in [!DNL Experience Platform].
- **[!DNL Data Access]** : fornisce agli utenti un’interfaccia per accedere ai propri dati in [!DNL Experience Platform].
- **[!DNL Data Ingestion]** : invia i dati a [!DNL Experience Platform] con [!DNL Data Ingestion] API.
- **[!DNL Schema Registry]** : definisce e memorizza lo schema che descrive la struttura dei dati da utilizzare in [!DNL Experience Platform].

## Guida introduttiva a [!DNL Experience Platform] API

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere o disporre di per effettuare correttamente chiamate a [!DNL Experience Platform] API.

### Lettura delle chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../landing/troubleshooting.md#how-do-i-format-an-api-request) nel [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori per le intestazioni richieste

Per effettuare chiamate a [!DNL Platform] , devi prima completare le [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolati in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedere [documentazione di panoramica sulla sandbox](../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Content-Type: application/json

## Flusso utente generale

Per iniziare, un utente ETL accede al [!DNL Experience Platform] e crea set di dati per l’acquisizione utilizzando un connettore standard o un connettore push-service.

Nell’interfaccia utente, l’utente crea il set di dati di output selezionando uno schema di set di dati. La scelta dello schema dipende dal tipo di dati (record o serie temporali) in cui vengono acquisiti [!DNL Platform]. Facendo clic sulla scheda Schemi nell’interfaccia utente, l’utente potrà visualizzare tutti gli schemi disponibili, incluso il tipo di comportamento supportato dallo schema.

Nello strumento ETL, l’utente inizierà a progettare le trasformazioni di mappatura dopo aver configurato la connessione appropriata (utilizzando le credenziali). Si presume che lo strumento ETL abbia già [!DNL Experience Platform] (processo non definito in questa Guida all&#39;integrazione).

Sono stati forniti dei modelli per un esempio di strumento ETL e di flusso di lavoro nella [Flusso di lavoro ETL](./workflow.md). Sebbene gli strumenti ETL possano differire nel formato, la maggior parte di essi espone funzionalità simili.

>[!NOTE]
>
>Il connettore ETL deve specificare un filtro timestamp che contrassegna la data di acquisizione dei dati e di offset (ad esempio La finestra per la quale devono essere letti i dati). Lo strumento ETL deve supportare l’inserimento di questi due parametri in questa o in un’altra interfaccia utente rilevante. In Adobe Experience Platform, questi parametri verranno mappati sulle date disponibili (se presenti) o sulla data acquisita presente nell’oggetto batch del set di dati.

### Visualizzare l’elenco dei set di dati

Utilizzando l’origine dei dati per la mappatura, è possibile ottenere un elenco di tutti i set di dati disponibili utilizzando [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

Puoi inviare una singola richiesta API per visualizzare tutti i set di dati disponibili (ad esempio `GET /dataSets`), con la best practice di includere parametri di query che limitano la dimensione della risposta.

Nei casi in cui vengono richieste informazioni complete sul set di dati, il payload di risposta può raggiungere dimensioni superiori a 3 GB, rallentando le prestazioni complessive. Pertanto, l’utilizzo di parametri di query per filtrare solo le informazioni necessarie renderà [!DNL Catalog] query più efficienti.

#### Filtraggio elenco

Quando filtri le risposte, puoi utilizzare più filtri in una singola chiamata separando i parametri con una e commerciale (`&`). Alcuni parametri di query accettano elenchi di valori separati da virgole, ad esempio il filtro &quot;properties&quot; nella richiesta di esempio seguente.

[!DNL Catalog] le risposte vengono misurate automaticamente in base ai limiti configurati, tuttavia il parametro di query &quot;limit&quot; può essere utilizzato per personalizzare i vincoli e limitare il numero di oggetti restituiti. Il preconfigurato [!DNL Catalog] i limiti di risposta sono:

- Se non viene specificato un parametro limit, il numero massimo di oggetti per payload di risposta è 20.
- Limite globale per tutti gli altri [!DNL Catalog] query è di 100 oggetti.
- Per le query di set di dati, se observableSchema viene richiesto utilizzando il parametro di query delle proprietà, il numero massimo di set di dati restituiti è 20.
- Parametri limite non validi (inclusi `limit=0`) viene visualizzato un errore HTTP 400 che indica gli intervalli corretti.
- Se i limiti o gli offset vengono passati come parametri di query, hanno la precedenza su quelli passati come intestazioni.

I parametri di query sono descritti più dettagliatamente nella sezione [Panoramica di Catalog Service](../catalog/home.md).

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
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Consulta la sezione [Panoramica di Catalog Service](../catalog/home.md) per esempi dettagliati su come effettuare chiamate al [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

**Risposta**

La risposta include tre (`limit=3`) set di dati che mostrano &quot;name&quot;, &quot;description&quot; e &quot;schemaRef&quot; come indicato da `properties` parametro di query.

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

La proprietà &quot;schemaRef&quot; di un set di dati contiene un URI che fa riferimento allo schema XDM su cui è basato il set di dati. Lo schema XDM (&quot;schemaRef&quot;) rappresenta tutti i campi potenziali che potrebbero essere utilizzati dal set di dati, non necessariamente i campi in uso (vedi &quot;observableSchema&quot; di seguito).

Lo schema XDM è lo schema utilizzato quando devi presentare all’utente un elenco di tutti i campi disponibili in cui è possibile scrivere.

Il primo valore &quot;schemaRef.id&quot; nell’oggetto di risposta precedente (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) è un URI che punta a uno schema XDM specifico nel file [!DNL Schema Registry]. Lo schema può essere recuperato effettuando una richiesta di ricerca (GET) al [!DNL Schema Registry] API.

>[!NOTE]
>
>La proprietà &quot;schemaRef&quot; sostituisce la proprietà &quot;schema&quot;, ora obsoleta. Se &quot;schemaRef&quot; è assente dal set di dati o non contiene un valore, dovrai verificare la presenza di una proprietà &quot;schema&quot;. A tale scopo, sostituisci &quot;schemaRef&quot; con &quot;schema&quot; nel `properties` parametro di query nella chiamata precedente. Ulteriori dettagli sulla proprietà &quot;schema&quot; sono disponibili nella sezione [Proprietà &quot;schema&quot; del set di dati](#dataset-schema-property-deprecated---eol-2019-05-30) che segue.

**Formato API**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**Richiesta**

La richiesta utilizza l’URL codificato `id` URI dello schema (il valore dell’attributo &quot;schemaRef.id&quot;) e richiede un’intestazione Accept.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

Il formato della risposta dipende dal tipo di intestazione Accept inviata nella richiesta. Le richieste di ricerca richiedono anche una `version` essere incluso nell’intestazione Accept. La tabella seguente illustra le intestazioni Accept per le ricerche:

| Accept | Descrizione |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | Elencare (GET) richieste, titoli, ID e versioni |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs e allOf risolto, con titoli e descrizioni |
| `application/vnd.adobe.xed+json; version={major version}` | Raw con $ref e allOf, con titoli e descrizioni |
| `application/vnd.adobe.xed-notext+json; version={major version}` | Raw con $ref e allOf, nessun titolo o descrizione |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs e allOf risolti, nessun titolo o descrizione |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs e allOf risolti, descrittori inclusi |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` e `application/vnd.adobe.xed-full+json; version={major version}` sono le intestazioni Accept più comunemente utilizzate. `application/vnd.adobe.xed-id+json` è da preferirsi per elencare le risorse in [!DNL Schema Registry] in quanto restituisce solo &quot;title&quot;, &quot;id&quot; e &quot;version&quot;. `application/vnd.adobe.xed-full+json; version={major version}` è da preferirsi per visualizzare una risorsa specifica (per il suo &quot;id&quot;), in quanto restituisce tutti i campi (nidificati sotto &quot;proprietà&quot;), nonché titoli e descrizioni.

**Risposta**

Lo schema JSON restituito descrive la struttura e le informazioni a livello di campo (&quot;type&quot;, &quot;format&quot;, &quot;minimum&quot;, &quot;maximum&quot;, ecc.) dei dati, serializzati come JSON. Se utilizzi per l’acquisizione un formato di serializzazione diverso da JSON (ad esempio Parquet o Scala), il [Guida al registro degli schemi](../xdm/tutorials/create-schema-api.md) contiene una tabella che mostra il tipo JSON desiderato (&quot;meta:xdmType&quot;) e la corrispondente rappresentazione in altri formati.

Insieme a questa tabella, [!DNL Schema Registry] La Guida per gli sviluppatori contiene esempi dettagliati di tutte le possibili chiamate che possono essere effettuate utilizzando [!DNL Schema Registry] API.

### Proprietà &quot;schema&quot; del set di dati (OBSOLETO - Fine del ciclo di vita 2019-05-30)

I set di dati possono contenere una proprietà &quot;schema&quot; che ora è obsoleta e rimane temporaneamente disponibile per compatibilità con le versioni precedenti. Ad esempio, una richiesta di inserimento (GET) simile a quella effettuata in precedenza, dove &quot;schema&quot; è stato sostituito da &quot;schemaRef&quot; nel `properties` parametro di query, potrebbe restituire quanto segue:

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

Se la proprietà &quot;schema&quot; di un set di dati è compilata, significa che lo schema è obsoleto `/xdms` e, se supportato, il connettore ETL deve utilizzare il valore nella proprietà &quot;schema&quot; con il `/xdms` endpoint (un endpoint obsoleto nel [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)) per recuperare lo schema legacy.

**Formato API**

```http
GET /catalog/{"schema" property without the "@"}
```

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

>[!NOTE]
>
>Un parametro di query facoltativo, `expansion=xdm`, indica all’API di espandere completamente e in linea tutti gli schemi a cui si fa riferimento. Questa operazione può essere utile quando si presenta all’utente un elenco di tutti i potenziali campi.

**Risposta**

Simile ai passaggi per [visualizzazione dello schema del set di dati](#view-dataset-schema), la risposta contiene uno schema JSON che descrive la struttura e le informazioni a livello di campo dei dati, serializzati come JSON.

>[!NOTE]
>
>Quando il campo &quot;schema&quot; è vuoto o completamente assente, il connettore deve leggere il campo &quot;schemaRef&quot; e utilizzare [API del registro dello schema](https://www.adobe.io/experience-platform-apis/references/schema-registry/) come mostrato nei passaggi precedenti per [visualizzare uno schema di set di dati](#view-dataset-schema).

### La proprietà &quot;observableSchema&quot;

La proprietà &quot;observableSchema&quot; di un set di dati ha una struttura JSON corrispondente a quella dello schema XDM JSON. &quot;observableSchema&quot; contiene i campi presenti nei file di input in ingresso. Durante la scrittura di dati in [!DNL Experience Platform], non è necessario che un utente utilizzi ogni campo dello schema di destinazione. Dovrebbero invece fornire solo i campi in uso.

Lo schema osservabile è lo schema che utilizzeresti per leggere i dati o presentare un elenco di campi disponibili per la lettura o la mappatura da.

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

L&#39;applicazione ETL può fornire la possibilità di visualizzare in anteprima i dati ([&quot;Figura 8&quot; nel flusso di lavoro ETL](./workflow.md)). L’API di accesso ai dati offre diverse opzioni per l’anteprima dei dati.

Ulteriori informazioni, incluse istruzioni dettagliate per l’anteprima dei dati tramite l’API di accesso ai dati, sono disponibili nella sezione [tutorial sull’accesso ai dati](../data-access/tutorials/dataset-data.md).

### Ottenere i dettagli del set di dati utilizzando il parametro di query &quot;properties&quot;

Come illustrato nei passaggi precedenti per [visualizzare un elenco di set di dati](#view-list-of-datasets), è possibile richiedere &quot;file&quot; utilizzando il parametro di query &quot;properties&quot;.

È possibile fare riferimento a [Panoramica di Catalog Service](../catalog/home.md) per informazioni dettagliate sull’esecuzione di query sui set di dati e sui filtri di risposta disponibili.

**Formato API**

```http
GET /catalog/dataSets?limit={value}&properties={value}
```

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=1&properties=files" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Risposta**

La risposta includerà un set di dati (`limit=1`) che mostra la proprietà &quot;files&quot;.

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files"
  }
}
```

### Elencare i file dei set di dati utilizzando l’attributo &quot;files&quot;

Puoi anche utilizzare una richiesta GET per recuperare i dettagli del file utilizzando l’attributo &quot;files&quot;.

**Formato API**

```http
GET /catalog/dataSets/{DATASET_ID}/views/{VIEW_ID}/files
```

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Risposta**

La risposta include l’ID file del set di dati come proprietà di livello principale, con i dettagli del file contenuti nell’oggetto ID file del set di dati.

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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

### Recupera dettagli file

Gli ID file del set di dati restituiti nella risposta precedente possono essere utilizzati in una richiesta GET per recuperare ulteriori dettagli del file tramite [!DNL Data Access] API.

Il [panoramica sull’accesso ai dati](../data-access/home.md) contiene informazioni dettagliate sull&#39;utilizzo di [!DNL Data Access] API.

**Formato API**

```http
GET /export/files/{DATASET_FILE_ID}
```

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
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

### Anteprima dati file

La proprietà &quot;href&quot; può essere utilizzata per recuperare i dati di anteprima tramite [[!DNL Data Access API]](../data-access/home.md).

**Formato API**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

La risposta alla richiesta di cui sopra conterrà un’anteprima del contenuto del file.

Ulteriori informazioni su [!DNL Data Access] API, comprese richieste e risposte dettagliate, è disponibile nella sezione [panoramica sull’accesso ai dati](../data-access/home.md).

### Ottieni &quot;fileDescription&quot; dal set di dati

Il componente di destinazione come output di dati trasformati, l’ingegnere dati sceglierà un set di dati di output ([&quot;Figure 12&quot; nel flusso di lavoro ETL](workflow.md)). Lo schema XDM è associato al set di dati di output. I dati da scrivere saranno identificati dall’attributo &quot;fileDescription&quot; dell’entità set di dati dalle API di individuazione dati. Queste informazioni possono essere recuperate utilizzando un ID set di dati (`{DATASET_ID}`). La proprietà &quot;fileDescription&quot; nella risposta JSON fornirà le informazioni richieste.

**Formato API**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{DATASET_ID}` | Il `id` valore del set di dati a cui stai tentando di accedere. |

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/59c93f3da7d0c00000798f68" \
-H "accept: application/json" \
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
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

I dati verranno scritti in [!DNL Experience Platform] utilizzo [API di acquisizione dati](https://www.adobe.io/experience-platform-apis/references/data-ingestion/).  La scrittura dei dati è un processo asincrono. Quando i dati vengono scritti in Adobe Experience Platform, viene creato un batch contrassegnato come completato solo dopo che i dati sono stati scritti completamente.

Ingresso dati [!DNL Experience Platform] deve essere scritto sotto forma di file Parquet.

## Fase di esecuzione

All’avvio dell’esecuzione, il connettore (come definito nel componente sorgente) leggerà i dati da [!DNL Experience Platform] utilizzando [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/). Il processo di trasformazione legge i dati per un determinato intervallo di tempo. Internamente, eseguirà query su batch di set di dati di origine. Durante l’esecuzione della query, utilizzerà una data di inizio con parametri (continua per i dati di serie temporali o i dati incrementali) ed elencherà i file di set di dati per tali batch, e inizierà ad effettuare richieste di dati per tali file di set di dati.

### Esempio di trasformazioni

Il [esempio di trasformazioni ETL](./transformations.md) Questo documento contiene una serie di trasformazioni di esempio, tra cui la gestione delle identità e le mappature dei tipi di dati. Utilizza queste trasformazioni come riferimento.

### Leggi dati da [!DNL Experience Platform]

Utilizzo di [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/), è possibile recuperare tutti i batch tra un’ora di inizio e un’ora di fine specificate e ordinarli in base all’ordine in cui sono stati creati.

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

I dettagli sul filtraggio dei batch si trovano in [Tutorial sull’accesso ai dati](../data-access/tutorials/dataset-data.md).

### Estrarre file da un batch

Una volta ottenuto l’ID del batch che stai cercando (`{BATCH_ID}`), è possibile recuperare un elenco di file appartenenti a un batch specifico tramite [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/).  I dettagli relativi sono disponibili nella sezione [[!DNL Data Access] esercitazione](../data-access/tutorials/dataset-data.md).

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

### Accedere ai file tramite ID file

Utilizzo dell’ID univoco di un file (`{FILE_ID`), il [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) può essere utilizzato per accedere ai dettagli specifici del file, tra cui il nome, la dimensione in byte e un collegamento per scaricarlo.

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

La risposta può puntare a un singolo file o a una directory. I dettagli su ciascuno sono disponibili nella sezione [[!DNL Data Access] esercitazione](../data-access/tutorials/dataset-data.md).

### Accedere al contenuto dei file

Il [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) può essere utilizzato per accedere al contenuto di un file specifico. Per recuperare il contenuto, viene effettuata una richiesta GET utilizzando il valore restituito per `_links.self.href` quando si accede a un file utilizzando l’ID file.

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

La risposta a questa richiesta contiene il contenuto del file. Per ulteriori informazioni, inclusi i dettagli sull’impaginazione delle risposte, vedi [Eseguire query sui dati tramite API di accesso ai dati](../data-access/tutorials/dataset-data.md) esercitazione.

### Convalidare i record per la conformità allo schema

Durante la scrittura dei dati, gli utenti possono scegliere di convalidare i dati in base alle regole di convalida definite nello schema XDM. Ulteriori informazioni sulla convalida dello schema sono disponibili nella sezione [Codice di riferimento per l&#39;integrazione dell&#39;ecosistema ETL [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

Se utilizzi l’implementazione di riferimento trovata in [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md), è possibile attivare la convalida dello schema in questa implementazione utilizzando la proprietà di sistema `-DenableSchemaValidation=true`.

La convalida può essere eseguita per i tipi XDM logici, utilizzando attributi come `minLength` e `maxlength` per le stringhe, `minimum` e `maximum` per i numeri interi e altro ancora. Il [Guida per gli sviluppatori API del Registro di schema](../xdm/api/getting-started.md) contiene una tabella che illustra i tipi XDM e le proprietà che possono essere utilizzate per la convalida.

>[!NOTE]
>
>I valori minimo e massimo previsti per i vari `integer` I tipi sono i valori MIN e MAX che il tipo può supportare, ma questi valori possono essere ulteriormente limitati ai valori minimi e massimi desiderati.

### Creare un batch

Una volta elaborati i dati, lo strumento ETL li riscriverà in [!DNL Experience Platform] utilizzando [API di acquisizione in batch](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). Prima di poter aggiungere dati a un set di dati, questi devono essere collegati a un batch che verrà successivamente caricato in un set di dati specifico.

**Richiesta**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

I dettagli per la creazione di un batch, inclusi gli esempi di richieste e risposte, sono disponibili nella sezione [Panoramica sull’acquisizione in batch](../ingestion/batch-ingestion/overview.md).

### Scrivi nel set di dati

Dopo aver creato correttamente un nuovo batch, i file possono quindi essere caricati in un set di dati specifico. È possibile registrare più file in un batch fino a quando non viene promosso. I file possono essere caricati utilizzando l’API di caricamento file di piccole dimensioni; tuttavia, se i file sono troppo grandi e il limite del gateway è superato, puoi utilizzare l’API di caricamento file di grandi dimensioni. I dettagli per l’utilizzo dei caricamenti di file sia di grandi dimensioni che di piccole dimensioni sono disponibili nella sezione [Panoramica sull’acquisizione in batch](../ingestion/batch-ingestion/overview.md).

**Richiesta**

Ingresso dati [!DNL Experience Platform] deve essere scritto sotto forma di file Parquet.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{ORG_ID}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### Contrassegna caricamento batch come completato

Dopo che tutti i file sono stati caricati nel batch, il batch può essere segnalato per il completamento. In questo modo, il [!DNL Catalog] Le voci &quot;DataSetFile&quot; vengono create per i file completati e associate al batch generato. Il [!DNL Catalog] Il batch viene quindi contrassegnato come riuscito, che attiva i flussi a valle per acquisire i dati disponibili.

I dati verranno prima recapitati nel percorso di gestione temporanea in Adobe Experience Platform e quindi spostati nel percorso finale dopo la catalogazione e la convalida. I batch verranno contrassegnati come completati quando tutti i dati vengono spostati in una posizione permanente.

**Richiesta**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

In caso di esito positivo, la risposta restituirà lo stato HTTP 200 OK e il corpo della risposta sarà vuoto.

Lo strumento ETL farà in modo di annotare la marca temporale dei set di dati sorgente durante la lettura dei dati.

Nella successiva esecuzione della trasformazione, probabilmente tramite la pianificazione o la chiamata dell’evento, l’ETL inizierà a richiedere i dati dalla marca temporale salvata in precedenza e tutti i dati andranno avanti.

### Ottieni ultimo stato batch

Prima di eseguire nuove attività nello strumento ETL, è necessario verificare che l&#39;ultimo batch sia stato completato correttamente. Il [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) fornisce un&#39;opzione specifica per il batch che fornisce i dettagli dei batch pertinenti.

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Risposta**

È possibile pianificare nuove attività se il valore &quot;status&quot; del batch precedente è &quot;success&quot;, come illustrato di seguito:

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
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

### Ottieni ultimo stato batch per ID

È possibile recuperare un singolo stato del batch tramite [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) emettendo una richiesta di GET utilizzando `{BATCH_ID}`. Il `{BATCH_ID}` utilizzato è lo stesso dell’ID restituito al momento della creazione del batch.

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Risposta - Completata**

La seguente risposta mostra un &quot;successo&quot;:

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
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
    "imsOrg": "{ORG_ID}",
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

I dati possono essere rappresentati in una matrice due per due nel modo seguente:

| Eventi incrementali | Profili incrementali |
|-------------------------------|----------------------|
| Eventi snapshot (meno probabili) | Profili snapshot |

I dati dell’evento si riferiscono in genere a colonne di marca temporale indicizzate in ogni riga.

I dati del profilo si riferiscono in genere a quando nei dati non è presente una marca temporale e ogni riga può essere identificata da una chiave primaria/composita.

I dati incrementali sono il luogo in cui solo i dati nuovi/aggiornati entrano nel sistema e si aggiungono ai dati correnti nei set di dati.

I dati di snapshot si verificano quando tutti i dati entrano nel sistema e sostituiscono alcuni o tutti i dati precedenti in un set di dati.

In caso di eventi incrementali, lo strumento ETL deve utilizzare le date disponibili/la data di creazione dell’entità batch. In caso di servizio push, le date disponibili non saranno presenti, pertanto lo strumento utilizzerà la data di creazione/aggiornamento batch per contrassegnare gli incrementi. Ogni batch di eventi incrementali deve essere elaborato.

Per i profili incrementali, lo strumento ETL utilizzerà le date create/aggiornate dell’entità batch. Di solito è necessario elaborare ogni batch di dati di profilo incrementali.

Gli eventi snapshot sono molto meno probabili a causa delle dimensioni dei dati. Tuttavia, se questo fosse necessario, lo strumento ETL deve scegliere solo l&#39;ultimo batch per l&#39;elaborazione.

Quando si utilizzano i profili snapshot, lo strumento ETL dovrà scegliere l&#39;ultimo batch di dati che è arrivato nel sistema. Tuttavia, se è necessario tenere traccia delle versioni delle modifiche, tutti i batch dovranno essere elaborati. L&#39;elaborazione della deduplicazione all&#39;interno del processo ETL contribuirà al controllo dei costi di storage.

## Ripetizione batch e rielaborazione dati

La ripetizione in batch e la rielaborazione dei dati possono essere necessarie nei casi in cui un client rilevi che negli ultimi &quot;n&quot; giorni i dati elaborati da ETL non si sono verificati come previsto o i dati sorgente stessi potrebbero non essere corretti.

A tal fine, gli amministratori di dati del client utilizzeranno [!DNL Platform] UI per rimuovere i batch contenenti dati danneggiati. Successivamente, sarà probabilmente necessario eseguire nuovamente l’ETL, popolandolo nuovamente con dati corretti. Se l’origine stessa contiene dati danneggiati, il data engineer/amministratore dovrà correggere i batch di origine e riacquisire i dati (in Adobe Experience Platform o tramite connettori ETL).

In base al tipo di dati generato, sarà il data engineer a scegliere di rimuovere un singolo batch o tutti i batch da determinati set di dati. I dati verranno rimossi/archiviati come da [!DNL Experience Platform] linee guida.

È probabile che la funzionalità ETL per eliminare i dati sia importante.

Una volta completata la rimozione, gli amministratori client dovranno riconfigurare Adobe Experience Platform per riavviare l’elaborazione dei servizi core dal momento in cui i batch vengono eliminati.

## Elaborazione batch simultanea

A discrezione del cliente, gli amministratori/ingegneri dei dati possono decidere di estrarre, trasformare e caricare i dati in modo sequenziale o simultaneo a seconda delle caratteristiche di un particolare set di dati. Questo sarà anche basato sul caso di utilizzo in cui il client esegue il targeting con i dati trasformati.

Ad esempio, se il client persiste in un archivio di persistenza aggiornabile e la sequenza o l’ordine degli eventi è importante, il client potrebbe dover elaborare rigorosamente i processi con trasformazioni ETL sequenziali.

In altri casi, i dati fuori servizio possono essere elaborati da applicazioni/processi a valle che ordinano internamente utilizzando una marca temporale specificata. In questi casi, le trasformazioni parallele dell’ETL possono essere attuabili per migliorare i tempi di elaborazione.

Per i batch di origine, dipenderà nuovamente dalle preferenze del client e dal vincolo del consumatore. Se i dati di origine possono essere rilevati in parallelo senza considerare la reggenza o l’ordinamento di una riga, il processo di trasformazione può creare batch di processi con un grado più elevato di parallelismo (ottimizzazione basata sull’elaborazione fuori ordine). Tuttavia, se la trasformazione deve rispettare i timestamp o modificare l’ordine di precedenza, l’API di accesso ai dati o l’utilità di pianificazione/chiamata dello strumento ETL dovranno garantire che i batch non vengano elaborati fuori ordine, ove possibile.

## Differimento

Il rinvio è un processo in cui i dati di input non sono ancora abbastanza completi da essere inviati ai processi a valle, ma possono essere utilizzati in futuro. I clienti determineranno la propria tolleranza individuale alla finitura dei dati per una corrispondenza futura rispetto al costo dell’elaborazione per informare la decisione di mettere da parte i dati e rielaborarli nella successiva esecuzione della trasformazione, sperando che possano essere arricchiti e riconciliati/uniti in un momento futuro all’interno della finestra di conservazione. Questo ciclo è in corso fino a quando la riga non viene elaborata a sufficienza o si ritiene che sia troppo obsoleta per continuare a investire in. Ogni iterazione genera dati differiti che sono un superset di tutti i dati differiti delle iterazioni precedenti.

Al momento Adobe Experience Platform non identifica i dati differiti, pertanto le implementazioni client devono basarsi sulle configurazioni manuali di ETL e Dataset per creare un altro set di dati in [!DNL Platform] mirroring del set di dati di origine che può essere utilizzato per conservare i dati differiti. In questo caso, i dati differiti saranno simili ai dati snapshot. In ogni esecuzione della trasformazione ETL, i dati di origine verranno uniti ai dati differiti e inviati per l’elaborazione.

## Changelog

| Data | Azione | Descrizione |
| ---- | ------ | ----------- |
| 2019-01-19 | Proprietà &quot;fields&quot; rimossa dai set di dati | I set di dati includevano in precedenza una proprietà &quot;fields&quot; contenente una copia dello schema. Questa funzionalità non deve più essere utilizzata. Se viene trovata la proprietà &quot;fields&quot;, questa deve essere ignorata e deve essere utilizzato &quot;observedSchema&quot; o &quot;schemaRef&quot;. |
| 2019-03-15 | Proprietà &quot;schemaRef&quot; aggiunta ai set di dati | La proprietà &quot;schemaRef&quot; di un set di dati contiene un URI che fa riferimento allo schema XDM su cui è basato il set di dati e rappresenta tutti i potenziali campi che potrebbero essere utilizzati dal set di dati. |
| 2019-03-15 | Tutti gli identificatori dell’utente finale vengono mappati sulla proprietà &quot;identityMap&quot; | IdentityMap è un’incapsulazione di tutti gli identificatori univoci di un soggetto, come l’ID del sistema di gestione delle relazioni con i clienti, l’ECID o l’ID del programma fedeltà. Questa mappa è utilizzata da [[!DNL Identity Service]](../identity-service/home.md) per risolvere tutte le identità note e anonime di un soggetto, formando un unico grafico delle identità per ogni utente finale. |
| 2019-05-30 | Fine del ciclo di vita e rimozione della proprietà &quot;schema&quot; dai set di dati | La proprietà &quot;schema&quot; del set di dati ha fornito un collegamento di riferimento allo schema utilizzando la proprietà obsoleta `/xdms` endpoint nella [!DNL Catalog] API. Questo è stato sostituito da un &quot;schemaRef&quot; che fornisce l’&quot;id&quot;, la &quot;versione&quot; e il &quot;contentType&quot; dello schema come riferimento nel nuovo [!DNL Schema Registry] API. |
