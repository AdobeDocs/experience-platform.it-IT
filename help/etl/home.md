---
keywords: Experience Platform;home;argomenti popolari;ETL;etl;integrazioni etl;integrazioni ETL
solution: Experience Platform
title: Sviluppo di integrazioni ETL per Adobe Experience Platform
topic-legacy: overview
description: La guida all’integrazione ETL descrive i passaggi generali per la creazione di connettori sicuri e ad alte prestazioni, ad Experience Platform per l’acquisizione di dati in Platform.
exl-id: 7d29b61c-a061-46f8-a31f-f20e4d725655
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '4075'
ht-degree: 1%

---

# Sviluppo di integrazioni ETL per Adobe Experience Platform

La guida all’integrazione ETL descrive i passaggi generali per la creazione di connettori sicuri e ad alte prestazioni per [!DNL Experience Platform] e acquisizione di dati in [!DNL Platform].


- [[!DNL Catalog]](https://www.adobe.io/experience-platform-apis/references/catalog/)
- [[!DNL Data Access]](https://www.adobe.io/experience-platform-apis/references/data-access/)
- [[!DNL Data Ingestion]](https://www.adobe.io/experience-platform-apis/references/data-ingestion/)
- [Autenticazione e autorizzazione per le API di Experience Platform](https://www.adobe.com/go/platform-api-authentication-en)
- [[!DNL Schema Registry]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)

Questa guida include anche esempi di chiamate API da utilizzare durante la progettazione di un connettore ETL, con collegamenti alla documentazione che ne descrive ogni [!DNL Experience Platform] e l&#39;utilizzo della relativa API, in maggiori dettagli.

Un’integrazione di esempio è disponibile in [!DNL GitHub] tramite [Codice di riferimento per l’integrazione dell’ecosistema ETL](https://github.com/adobe/acp-data-services-etl-reference) in [!DNL Apache] Licenza versione 2.0.

## Flusso di lavoro

Il seguente diagramma del flusso di lavoro fornisce una panoramica di alto livello sull’integrazione dei componenti Adobe Experience Platform con un’applicazione e un connettore ETL.

![](images/etl.png)

## Componenti Adobe Experience Platform

Sono presenti più componenti di Experience Platform coinvolti nelle integrazioni dei connettori ETL. L’elenco seguente illustra diversi componenti e funzionalità chiave:

- **Adobe Identity Management System (IMS)** - Fornisce il framework per l’autenticazione ai servizi Adobe.
- **Organizzazione IMS** - un&#39;entità aziendale che può possedere o concedere in licenza prodotti e servizi e consentire l&#39;accesso ai propri membri.
- **Utente IMS** - Membri di un&#39;organizzazione IMS. La relazione tra l&#39;organizzazione e l&#39;utente è molto importante per molti.
- **[!DNL Sandbox]** - Una partizione virtuale una sola [!DNL Platform] per sviluppare e sviluppare applicazioni di esperienza digitale.
- **Individuazione dati** - Registra i metadati dei dati acquisiti e trasformati in [!DNL Experience Platform].
- **[!DNL Data Access]** - Fornisce agli utenti un&#39;interfaccia per accedere ai loro dati in [!DNL Experience Platform].
- **[!DNL Data Ingestion]** - Invia dati a [!DNL Experience Platform] con [!DNL Data Ingestion] API.
- **[!DNL Schema Registry]** - Definisce e memorizza lo schema che descrive la struttura dei dati da utilizzare in [!DNL Experience Platform].

## Guida introduttiva a [!DNL Experience Platform] API

Le sezioni seguenti forniscono informazioni aggiuntive che dovrai conoscere o avere a disposizione per effettuare correttamente le chiamate a [!DNL Experience Platform] API.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione panoramica su sandbox](../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Tipo di contenuto: application/json

## Flusso utente generale

Per iniziare, un utente ETL accede al [!DNL Experience Platform] interfaccia utente e crea set di dati per l’acquisizione utilizzando un connettore standard o un connettore push-service.

Nell’interfaccia utente, l’utente crea il set di dati di output selezionando uno schema di set di dati. La scelta dello schema dipende dal tipo di dati (record o serie temporali) in cui viene acquisito [!DNL Platform]. Facendo clic sulla scheda Schemi nell’interfaccia utente, l’utente sarà in grado di visualizzare tutti gli schemi disponibili, compreso il tipo di comportamento supportato dallo schema.

Nello strumento ETL, l’utente inizierà a progettare le trasformazioni di mappatura dopo aver configurato la connessione appropriata (utilizzando le proprie credenziali). Si presume che lo strumento ETL abbia già [!DNL Experience Platform] connettori installati (processo non definito in questa Guida all&#39;integrazione).

Sono stati forniti mapping per uno strumento ETL di esempio e un flusso di lavoro nel [Flusso di lavoro ETL](./workflow.md). Anche se gli strumenti ETL possono differire nel formato, la maggior parte espone funzionalità simili.

>[!NOTE]
>
>Il connettore ETL deve specificare un filtro di marca temporale che contrassegna la data in cui acquisire i dati e l’offset (ovvero la finestra per la quale i dati devono essere letti). Lo strumento ETL dovrebbe supportare l’acquisizione di questi due parametri in questa o in un’altra interfaccia utente pertinente. In Adobe Experience Platform, questi parametri verranno mappati alle date disponibili (se presenti) o alla data acquisita presente nell’oggetto batch del set di dati.

### Visualizza elenco di set di dati

Utilizzando l’origine dei dati per la mappatura, è possibile recuperare un elenco di tutti i set di dati disponibili utilizzando la variabile [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

Puoi emettere una singola richiesta API per visualizzare tutti i set di dati disponibili (ad esempio `GET /dataSets`), in particolare per includere parametri di query che limitano la dimensione della risposta.

Nei casi in cui vengono richieste informazioni complete sui set di dati, il payload di risposta può raggiungere dimensioni superiori a 3 GB, il che può rallentare le prestazioni complessive. Pertanto, utilizzando i parametri di query per filtrare solo le informazioni necessarie, [!DNL Catalog] query più efficienti.

#### Filtro elenco

Quando filtri le risposte, puoi utilizzare più filtri in una singola chiamata separando i parametri con una e commerciale (`&`). Alcuni parametri di query accettano elenchi di valori separati da virgole, come il filtro &quot;proprietà&quot; nella richiesta di esempio seguente.

[!DNL Catalog] le risposte vengono misurate automaticamente in base ai limiti configurati, tuttavia il parametro di query &quot;limit&quot; può essere utilizzato per personalizzare i vincoli e limitare il numero di oggetti restituiti. Preconfigurato [!DNL Catalog] i limiti di risposta sono:

- Se non viene specificato un parametro di limite, il numero massimo di oggetti per payload di risposta è 20.
- Limite globale per tutti gli altri [!DNL Catalog] Le query sono 100 oggetti.
- Per le query dei set di dati, se si richiede OsservableSchema utilizzando il parametro di query delle proprietà, il numero massimo di set di dati restituiti è 20.
- Parametri limite non validi (inclusi `limit=0`) sono soddisfatte con un errore HTTP 400 che delinea gli intervalli appropriati.
- Se i limiti o gli offset vengono passati come parametri di query, hanno la precedenza su quelli passati come intestazioni.

I parametri di query sono descritti più dettagliatamente nella sezione [Panoramica del servizio catalogo](../catalog/home.md).

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

Fai riferimento alla [Panoramica del servizio catalogo](../catalog/home.md) per esempi dettagliati su come effettuare chiamate al [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

**Risposta**

La risposta include tre (`limit=3`) i set di dati che mostrano &quot;name&quot;, &quot;description&quot; e &quot;schemaRef&quot; come indicato dalla `properties` parametro query.

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

La proprietà &quot;schemaRef&quot; di un set di dati contiene un URI che fa riferimento allo schema XDM su cui è basato il set di dati. Lo schema XDM (&quot;schemaRef&quot;) rappresenta tutti i campi potenziali che possono essere utilizzati dal set di dati, non necessariamente i campi in uso (vedi &quot;osservableSchema&quot; di seguito).

Lo schema XDM è lo schema utilizzato quando è necessario presentare all’utente un elenco di tutti i campi disponibili in cui è possibile scrivere.

Il primo valore &quot;schemaRef.id&quot; nell&#39;oggetto di risposta precedente (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) è un URI che punta a uno schema XDM specifico nel [!DNL Schema Registry]. Lo schema può essere recuperato effettuando una richiesta di ricerca (GET) al [!DNL Schema Registry] API.

>[!NOTE]
>
>La proprietà &quot;schemaRef&quot; sostituisce la proprietà &quot;schema&quot; ora obsoleta. Se &quot;schemaRef&quot; è assente dal set di dati o non contiene un valore, dovrai verificare la presenza di una proprietà &quot;schema&quot;. Per eseguire questa operazione, sostituisci &quot;schemaRef&quot; con &quot;schema&quot; nel `properties` parametro query nella chiamata precedente. Maggiori dettagli sulla proprietà &quot;schema&quot; sono disponibili nella sezione [Proprietà &quot;schema&quot; del set di dati](#dataset-schema-property-deprecated---eol-2019-05-30) sezione che segue.

**Formato API**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**Richiesta**

La richiesta utilizza l’URL codificato `id` URI dello schema (il valore dell&#39;attributo &quot;schemaRef.id&quot;) e richiede un&#39;intestazione Accept.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

Il formato della risposta dipende dal tipo di intestazione Accept inviato nella richiesta. Le richieste di ricerca richiedono anche un `version` nell’intestazione Accept. La tabella seguente illustra le intestazioni Accept disponibili per le ricerche:

| Accept | Descrizione |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | Richieste elenco (GET), titoli, id e versioni |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs e allOf risolti, ha titoli e descrizioni |
| `application/vnd.adobe.xed+json; version={major version}` | Raw con $ref e allOf, ha titoli e descrizioni |
| `application/vnd.adobe.xed-notext+json; version={major version}` | Raw con $ref e allOf, senza titoli o descrizioni |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs e allOf risolti, senza titoli o descrizioni |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs e allOf risolti, descrittori inclusi |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` e `application/vnd.adobe.xed-full+json; version={major version}` sono le intestazioni Accept più comunemente utilizzate. `application/vnd.adobe.xed-id+json` è da preferirsi per elencare le risorse in [!DNL Schema Registry] poiché restituisce solo &quot;title&quot;, &quot;id&quot; e &quot;version&quot;. `application/vnd.adobe.xed-full+json; version={major version}` è da preferirsi per visualizzare una risorsa specifica (in base al suo &quot;id&quot;), in quanto restituisce tutti i campi (nidificati sotto &quot;proprietà&quot;), nonché titoli e descrizioni.

**Risposta**

Lo schema JSON restituito descrive la struttura e le informazioni a livello di campo (&quot;tipo&quot;, &quot;formato&quot;, &quot;minimo&quot;, &quot;massimo&quot;, ecc.) dei dati, serializzati come JSON. Se utilizzi un formato di serializzazione diverso da JSON per l’acquisizione (ad esempio Parquet o Scala), la variabile [Guida al registro dello schema](../xdm/tutorials/create-schema-api.md) contiene una tabella che mostra il tipo JSON desiderato (&quot;meta:xdmType&quot;) e la corrispondente rappresentazione in altri formati.

Insieme a questa tabella, il [!DNL Schema Registry] La Guida per gli sviluppatori contiene esempi dettagliati di tutte le possibili chiamate che possono essere effettuate utilizzando [!DNL Schema Registry] API.

### Proprietà &quot;schema&quot; del set di dati (OBSOLETO - EOL 2019-05-30)

I set di dati possono contenere una proprietà &quot;schema&quot; che ora è obsoleta e rimane temporaneamente disponibile per la compatibilità con le versioni precedenti. Ad esempio, una richiesta di elenco (GET) simile a quella effettuata in precedenza, in cui &quot;schema&quot; è stato sostituito da &quot;schemaRef&quot; nel `properties` parametro query, potrebbe restituire quanto segue:

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

Se la proprietà &quot;schema&quot; di un set di dati è compilata, lo schema è diventato obsoleto `/xdms` schema e, se supportato, il connettore ETL deve utilizzare il valore nella proprietà &quot;schema&quot; con `/xdms` endpoint (un endpoint obsoleto nel [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)) per recuperare lo schema legacy.

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
>Un parametro di query facoltativo, `expansion=xdm`, comunica all’API di espandere completamente e in linea tutti gli schemi di riferimento. È consigliabile eseguire questa operazione quando si presenta all’utente un elenco di tutti i campi potenziali.

**Risposta**

Simile ai passaggi per [visualizzazione schema set di dati](#view-dataset-schema), la risposta contiene uno schema JSON che descrive la struttura e le informazioni a livello di campo dei dati, serializzati come JSON.

>[!NOTE]
>
>Quando il campo &quot;schema&quot; è completamente vuoto o assente, il connettore deve leggere il campo &quot;schemaRef&quot; e utilizzare il [API del Registro di sistema dello schema](https://www.adobe.io/experience-platform-apis/references/schema-registry/) come mostrato nei passaggi precedenti a [visualizzare uno schema di set di dati](#view-dataset-schema).

### Proprietà &quot;osservableSchema&quot;

La proprietà &quot;osservableSchema&quot; di un set di dati presenta una struttura JSON corrispondente a quella dello schema XDM JSON. Lo &quot;schema osservabile&quot; contiene i campi presenti nei file di input in arrivo. Quando si scrivono dati a [!DNL Experience Platform], non è necessario che un utente utilizzi ogni campo dello schema di destinazione. Dovrebbero invece fornire solo i campi in uso.

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

L’applicazione ETL può fornire una capacità di visualizzare in anteprima i dati ([&quot;Figura 8&quot; nel flusso di lavoro ETL](./workflow.md)). L’API di accesso ai dati fornisce diverse opzioni per l’anteprima dei dati.

Ulteriori informazioni, incluse istruzioni dettagliate per visualizzare in anteprima i dati utilizzando l’API di accesso ai dati, sono disponibili nella sezione [esercitazione sull&#39;accesso ai dati](../data-access/tutorials/dataset-data.md).

### Ottieni i dettagli del set di dati utilizzando il parametro di query &quot;properties&quot;

Come mostrato nei passaggi precedenti a [visualizzare un elenco di set di dati](#view-list-of-datasets), puoi richiedere &quot;file&quot; utilizzando il parametro di query &quot;properties&quot;.

Puoi fare riferimento alla [Panoramica del servizio catalogo](../catalog/home.md) per informazioni dettagliate sulla query dei set di dati e sui filtri di risposta disponibili.

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

La risposta include un set di dati (`limit=1`) che mostra la proprietà &quot;files&quot;.

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files"
  }
}
```

### Elencare file di set di dati utilizzando l’attributo &quot;files&quot;

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

La risposta include l&#39;ID del file di set di dati come proprietà di livello principale, con i dettagli del file contenuti nell&#39;oggetto ID del file di set di dati.

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

### Dettagli del file di recupero

Gli ID del file di set di dati restituiti nella risposta precedente possono essere utilizzati in una richiesta di GET per recuperare ulteriori dettagli del file tramite la [!DNL Data Access] API.

La [panoramica sull&#39;accesso ai dati](../data-access/home.md) contiene dettagli su come utilizzare il [!DNL Data Access] API.

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

La proprietà &quot;href&quot; può essere utilizzata per recuperare i dati di anteprima tramite il [[!DNL Data Access API]](../data-access/home.md).

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

La risposta alla richiesta di cui sopra contiene un&#39;anteprima del contenuto del file.

Ulteriori informazioni sulle [!DNL Data Access] L’API, incluse richieste e risposte dettagliate, è disponibile nella sezione [panoramica sull&#39;accesso ai dati](../data-access/home.md).

### Ottieni &quot;fileDescription&quot; dal set di dati

Il componente di destinazione come output dei dati trasformati, data engineer sceglierà un set di dati di output ([&quot;Figura 12&quot; nel flusso di lavoro ETL](workflow.md)). Lo schema XDM è associato al set di dati di output. I dati da scrivere saranno identificati dall’attributo &quot;fileDescription&quot; dell’entità di set di dati dalle API di individuazione dati. Queste informazioni possono essere recuperate utilizzando un ID set di dati (`{DATASET_ID}`). La proprietà &quot;fileDescription&quot; nella risposta JSON fornirà le informazioni richieste.

**Formato API**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{DATASET_ID}` | La `id` valore del set di dati a cui si sta tentando di accedere. |

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

I dati verranno scritti in [!DNL Experience Platform] utilizzo [API di acquisizione dati](https://www.adobe.io/experience-platform-apis/references/data-ingestion/).  La scrittura di dati è un processo asincrono. Quando i dati vengono scritti in Adobe Experience Platform, un batch viene creato e contrassegnato come un successo solo dopo che i dati sono stati scritti completamente.

Ingresso dati [!DNL Experience Platform] devono essere scritti sotto forma di file Parquet.

## Fase di esecuzione

All’avvio dell’esecuzione, il connettore (come definito nel componente di origine) legge i dati da [!DNL Experience Platform] utilizzando [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/). Il processo di trasformazione leggerà i dati per un determinato intervallo di tempo. Internamente, eseguirà query sui batch di set di dati di origine. Durante l’esecuzione delle query, utilizzerà un valore parametrizzato (che continua per i dati delle serie temporali o i dati incrementali) per la data di inizio e i file di set di dati per tali batch, quindi inizierà a richiedere i dati per tali file di set di dati.

### Trasformazioni di esempio

La [trasformazioni ETL di esempio](./transformations.md) il documento contiene un certo numero di trasformazioni di esempio, tra cui la gestione dell&#39;identità e le mappature del tipo di dati. Usa queste trasformazioni per riferimento.

### Leggi dati da [!DNL Experience Platform]

Utilizzo della [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/), puoi recuperare tutti i batch tra un&#39;ora di inizio e una di fine specificate e ordinarli in base all&#39;ordine in cui sono stati creati.

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

I dettagli sui batch di filtri si trovano nella sezione [Esercitazione sull&#39;accesso ai dati](../data-access/tutorials/dataset-data.md).

### Estrarre file da un batch

Una volta ottenuto l&#39;ID per il batch che stai cercando (`{BATCH_ID}`), è possibile recuperare un elenco di file appartenenti a un batch specifico tramite il [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/).  I dettagli per farlo sono disponibili nella sezione [[!DNL Data Access] tutorial](../data-access/tutorials/dataset-data.md).

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

### Accedere ai file utilizzando l’ID file

Utilizzo dell&#39;ID univoco di un file (`{FILE_ID`), [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) può essere utilizzato per accedere ai dettagli specifici del file, inclusi nome, dimensione in byte e un collegamento per scaricarlo.

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

La risposta può puntare a un singolo file o a una directory. I dettagli su ciascuno sono disponibili nella sezione [[!DNL Data Access] tutorial](../data-access/tutorials/dataset-data.md).

### Accedere al contenuto del file

La [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) può essere utilizzato per accedere al contenuto di un file specifico. Per recuperare il contenuto, viene effettuata una richiesta di GET utilizzando il valore restituito per `_links.self.href` quando si accede a un file utilizzando l’ID file.

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

La risposta a questa richiesta contiene il contenuto del file. Per ulteriori informazioni, compresi i dettagli sull’impaginazione delle risposte, consulta la sezione [Come eseguire query sui dati tramite API di accesso ai dati](../data-access/tutorials/dataset-data.md) esercitazione.

### Convalida dei record per la conformità allo schema

Quando i dati vengono scritti, gli utenti possono scegliere di convalidare i dati in base alle regole di convalida definite nello schema XDM. Ulteriori informazioni sulla convalida dello schema sono disponibili nella sezione [Codice di riferimento per l&#39;integrazione dell&#39;ecosistema ETL su [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

Se utilizzi l’implementazione di riferimento trovata in [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md), è possibile attivare la convalida dello schema in questa implementazione utilizzando la proprietà system `-DenableSchemaValidation=true`.

La convalida può essere eseguita per tipi XDM logici, utilizzando attributi come `minLength` e `maxlength` per le stringhe, `minimum` e `maximum` per numeri interi e altro ancora. La [Guida per gli sviluppatori API del Registro di sistema dello schema](../xdm/api/getting-started.md) contiene una tabella che delinea i tipi XDM e le proprietà utilizzabili per la convalida.

>[!NOTE]
>
>Valori minimi e massimi previsti per vari `integer` I tipi sono i valori MIN e MAX che il tipo può supportare, ma questi valori possono essere ulteriormente vincolati a valori minimi e massimi a scelta.

### Creare un batch

Una volta elaborati i dati, lo strumento ETL restituirà i dati a [!DNL Experience Platform] utilizzando [API di acquisizione in batch](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). Prima di poter aggiungere dati a un set di dati, questi devono essere collegati a un batch che verrà successivamente caricato in un set di dati specifico.

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

I dettagli per la creazione di un batch, incluse le richieste di esempio e le risposte, sono disponibili nella sezione [Panoramica sull’acquisizione in batch](../ingestion/batch-ingestion/overview.md).

### Scrivi nel set di dati

Dopo aver creato correttamente un nuovo batch, i file possono quindi essere caricati in un set di dati specifico. È possibile pubblicare più file in un batch fino a quando non viene promosso. I file possono essere caricati utilizzando l’API di caricamento file di piccole dimensioni; tuttavia, se i file sono troppo grandi e il limite del gateway viene superato, puoi utilizzare l’API di caricamento file di grandi dimensioni. I dettagli per l’utilizzo di Caricamento file di grandi e piccole dimensioni si trovano nella sezione [Panoramica sull’acquisizione in batch](../ingestion/batch-ingestion/overview.md).

**Richiesta**

Ingresso dati [!DNL Experience Platform] devono essere scritti sotto forma di file Parquet.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{ORG_ID}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### Contrassegna caricamento batch completato

Dopo che tutti i file sono stati caricati nel batch, il batch può essere segnalato per il completamento. Facendo questo, il [!DNL Catalog] Le voci &quot;DataSetFile&quot; vengono create per i file completati e associate al batch di generazione. La [!DNL Catalog] batch viene quindi contrassegnato come riuscito, che attiva i flussi a valle per acquisire i dati disponibili.

I dati verranno prima trasferiti nella posizione di staging su Adobe Experience Platform e quindi spostati nella posizione finale dopo la catalogazione e la convalida. I batch verranno contrassegnati come completati una volta che tutti i dati saranno stati spostati in una posizione permanente.

**Richiesta**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

In caso di esito positivo, la risposta restituirà lo stato HTTP 200 OK e il corpo della risposta sarà vuoto.

Lo strumento ETL si accerterà di annotare la marca temporale dei set di dati di origine durante la lettura dei dati.

Nell’esecuzione della trasformazione successiva, probabilmente per pianificazione o chiamata dell’evento, l’ETL inizierà a richiedere i dati dalla marca temporale salvata in precedenza e tutti i dati in corso.

### Ottieni stato ultimo batch

Prima di eseguire nuove attività nello strumento ETL, è necessario assicurarsi che l&#39;ultimo batch sia stato completato correttamente. La [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) fornisce un&#39;opzione specifica per il batch che fornisce i dettagli dei batch pertinenti.

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

È possibile programmare nuove attività se il precedente valore di &quot;stato&quot; del batch è &quot;successo&quot;, come illustrato di seguito:

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

### Ottieni stato ultimo batch per ID

È possibile recuperare un singolo stato batch tramite [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) emettendo una richiesta di GET utilizzando `{BATCH_ID}`. La `{BATCH_ID}` utilizzato è lo stesso ID restituito al momento della creazione del batch.

**Richiesta**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Risposta - Operazione riuscita**

La risposta seguente mostra un &quot;successo&quot;:

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

## Dati ed eventi incrementali e snapshot e profili

I dati possono essere rappresentati in due da due matrici come segue:

| Eventi incrementali | Profili incrementali |
|-------------------------------|----------------------|
| Eventi di snapshot (con minore probabilità) | Profili snapshot |

I dati evento sono in genere presenti nelle colonne di marca temporale indicizzate di ogni riga.

I dati del profilo si verificano in genere quando non è presente una marca temporale nei dati e ogni riga può essere identificata da una chiave primaria/composita.

I dati incrementali sono il punto in cui solo i dati nuovi/aggiornati vengono inseriti nel sistema e vengono aggiunti ai dati correnti nei set di dati.

I dati snapshot vengono generati quando tutti i dati vengono inseriti nel sistema e sostituiscono alcuni o tutti i dati precedenti in un set di dati.

Nel caso di eventi incrementali, lo strumento ETL deve utilizzare le date disponibili/creare la data dell’entità batch. Nel caso del servizio push, le date disponibili non saranno presenti, quindi lo strumento utilizzerà la data di creazione/aggiornamento in batch per contrassegnare gli incrementi. È necessario elaborare ogni batch di eventi incrementali.

Per i profili incrementali, lo strumento ETL utilizzerà date create/aggiornate di entità batch. Di solito, ogni batch di dati di profilo incrementali deve essere elaborato.

Gli eventi snapshot sono molto meno probabili a causa della dimensione pura dei dati. Tuttavia, se ciò dovesse essere necessario, lo strumento ETL deve selezionare solo l&#39;ultimo batch da elaborare.

Quando si utilizzano i profili di snapshot, lo strumento ETL dovrà scegliere l&#39;ultimo batch di dati arrivati nel sistema. Ma se il requisito è quello di tenere traccia delle versioni delle modifiche, tutti i batch saranno tenuti ad essere elaborati. L&#39;elaborazione della deduplicazione all&#39;interno del processo ETL contribuirà a controllare i costi di storage.

## Riproduzione in batch e rielaborazione dei dati

La riproduzione in batch e la rielaborazione dei dati possono essere necessarie nei casi in cui un cliente scopra che, negli ultimi &quot;n&quot; giorni, i dati in fase di elaborazione ETL non si sono verificati come previsto o che i dati sorgente stessi potrebbero non essere stati corretti.

A questo scopo, gli amministratori di dati del cliente utilizzeranno il [!DNL Platform] Interfaccia utente per rimuovere i batch contenenti dati corrotti. Quindi, sarà probabilmente necessario rieseguire l’ETL, ripopolando in tal modo i dati corretti. Se l’origine stessa conteneva dati corrotti, l’ingegnere/amministratore dei dati dovrà correggere i batch di origine e riacquisire i dati (in Adobe Experience Platform o tramite connettori ETL).

In base al tipo di dati generato, sarà l’ingegnere dei dati a scegliere di rimuovere un singolo batch o tutti i batch da determinati set di dati. I dati verranno rimossi/archiviati come da [!DNL Experience Platform] linee guida.

È probabile che la funzionalità ETL per eliminare i dati sia importante.

Una volta completata l&#39;eliminazione, gli amministratori client dovranno riconfigurare Adobe Experience Platform per riavviare l&#39;elaborazione dei servizi principali dal momento in cui i batch vengono eliminati.

## Elaborazione batch simultanea

A discrezione del cliente, gli amministratori/ingegneri dei dati possono decidere di estrarre, trasformare e caricare i dati in modo sequenziale o simultaneo a seconda delle caratteristiche di un particolare set di dati. Questo sarà anche basato sul caso d’uso in cui il cliente esegue il targeting con i dati trasformati.

Ad esempio, se il client persiste in un archivio di persistenza aggiornabile e la sequenza o l’ordine degli eventi è importante, potrebbe essere necessario elaborare rigorosamente i processi con trasformazioni ETL sequenziali.

In altri casi, i dati fuori ordine possono essere elaborati da applicazioni/processi a valle che eseguono l’ordinamento interno utilizzando una data marca temporale. In questi casi, le trasformazioni parallele ETL possono essere fattibili per migliorare i tempi di elaborazione.

Per i batch di origine, dipenderà nuovamente dalla preferenza del cliente e dal vincolo del consumatore. Se i dati di origine possono essere raccolti in parallelo senza tenere conto della regenza/ordinamento di una riga, allora il processo di trasformazione può creare batch di processi con un più alto grado di parallelismo (ottimizzazione basata sull&#39;elaborazione fuori ordine). Tuttavia, se la trasformazione deve rispettare timestamp o modificare l’ordine di precedenza, la pianificazione/chiamata dell’API di accesso ai dati o dello strumento ETL dovrà garantire che i batch non vengano elaborati in modo non ordinato, ove possibile.

## Differenza

Il differimento è un processo in cui i dati di input non sono ancora abbastanza completi da essere inviati ai processi a valle, ma possono essere utilizzabili in futuro. I clienti determineranno la propria tolleranza individuale per l&#39;ottimizzazione dei dati per future corrispondenze rispetto al costo del trattamento per informare la loro decisione di mettere da parte i dati e rielaborarli nella successiva esecuzione della trasformazione, sperando che possano essere arricchiti e riconciliati/uniti in un futuro momento all&#39;interno della finestra di conservazione. Questo ciclo è in corso fino a quando la riga non viene elaborata a sufficienza o è considerato troppo vecchio per continuare ad investire in. Ogni iterazione genera dati differiti che è un superset di tutti i dati differiti nelle iterazioni precedenti.

Adobe Experience Platform non identifica i dati differiti al momento, pertanto le implementazioni client devono basarsi sulle configurazioni ETL e del manuale del set di dati per creare un altro set di dati in [!DNL Platform] mirroring del set di dati di origine che può essere utilizzato per mantenere i dati differiti. In questo caso, i dati differiti saranno simili ai dati snapshot. In ogni esecuzione della trasformazione ETL, i dati di origine saranno uniti ai dati differiti e inviati per l’elaborazione.

## Changelog

| Data | Azione | Descrizione |
| ---- | ------ | ----------- |
| 01/01/2019 | Proprietà &quot;fields&quot; rimossa dai set di dati | I set di dati in precedenza includevano una proprietà &quot;field&quot; che conteneva una copia dello schema. Questa funzionalità non deve più essere utilizzata. Se viene trovata la proprietà &quot;fields&quot;, ignorarla e utilizzare invece &quot;osservSchema&quot; o &quot;schemaRef&quot;. |
| 03/03/2019 | proprietà &quot;schemaRef&quot; aggiunta ai set di dati | La proprietà &quot;schemaRef&quot; di un set di dati contiene un URI che fa riferimento allo schema XDM su cui è basato il set di dati e rappresenta tutti i campi potenziali che possono essere utilizzati dal set di dati. |
| 03/03/2019 | Tutti gli identificatori dell&#39;utente finale vengono mappati sulla proprietà &quot;identityMap&quot; | &quot;identityMap&quot; è un&#39;incapsulazione di tutti gli identificatori univoci di un soggetto, come ID CRM, ECID o ID programma fedeltà. Questa mappa è utilizzata da [[!DNL Identity Service]](../identity-service/home.md) risolvere tutte le identità note e anonime di un soggetto, formando un unico grafico di identità per ciascun utente finale. |
| 05/05/2019 | Fine del ciclo vita e rimozione della proprietà &quot;schema&quot; dai set di dati | La proprietà &quot;schema&quot; del set di dati forniva un collegamento di riferimento allo schema utilizzando l’opzione obsoleta `/xdms` punto finale [!DNL Catalog] API. Questo è stato sostituito da un &quot;schemaRef&quot; che fornisce &quot;id&quot;, &quot;version&quot; e &quot;contentType&quot; dello schema come indicato nel nuovo [!DNL Schema Registry] API. |
