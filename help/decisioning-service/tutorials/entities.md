---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Gestire le entità del servizio di disattivazione tramite API
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '7207'
ht-degree: 0%

---


# Gestione di oggetti e regole di disattivazione tramite API

Questo documento fornisce un&#39;esercitazione per lavorare con le entità aziendali utilizzando  API di Adobe Experience Platform. [!DNL Decisioning Service]

L&#39;esercitazione è suddivisa in due parti:

- Le API Repository generiche per la gestione degli oggetti aziendali sono introdotte nella [prima parte](#managing-repository-entities-using-apis). Queste API sono generiche nel senso che forniscono funzionalità di creazione, lettura, aggiornamento, eliminazione e ricerca per **qualsiasi** tipo di oggetto aziendale. Viene descritto il modello API generale e viene spiegato il rapporto con l&#39;Hypertext Application Language (HAL).

- Applicando le conoscenze sulle API del repository, la [seconda parte](#creating-and-managing-offer-decisioning-entities-using-apis) si concentra sulle entità aziendali gestite tramite le API del repository. Con le stesse API applicate l&#39;unica differenza tra la gestione di due entità diverse, come un&#39;attività e una regola business, è il payload di richiesta e risposta, più i valori di intestazione necessari che indicano il tipo di oggetto gestito.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei [!DNL Experience Platform] servizi e delle convenzioni API. Il [!DNL Platform] repository è un servizio utilizzato da molti altri [!DNL Platform] servizi per memorizzare oggetti aziendali e vari tipi di metadati. Offre un modo sicuro e flessibile per gestire e interrogare gli oggetti da utilizzare in diversi servizi di runtime. La [!DNL Decisioning Service] è una di quelle. Prima di iniziare questa esercitazione, consulta la documentazione per i seguenti elementi:

- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Framework standard con cui Platform organizza i dati sull&#39;esperienza dei clienti.
- [!DNL Decisioning Service](./../home.md): Illustra i concetti e i componenti utilizzati per la decodifica delle esperienze in generale e per le decisioni sulle offerte in particolare. Illustra le strategie utilizzate per scegliere l&#39;opzione migliore da presentare durante l&#39;esperienza di un cliente.
- [!DNL Profile Query Language (PQL)](../../segmentation/pql/overview.md): PQL è un linguaggio potente per scrivere espressioni sulle istanze XDM. PQL viene utilizzato per definire le regole decisionali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per eseguire correttamente le chiamate alle [!DNL Platform] API.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

## Convenzioni API repository

[!DNL Decisioning Service] è controllato da una serie di oggetti business correlati tra loro. Tutti gli oggetti aziendali sono memorizzati nel repository degli oggetti [!DNL Platform’s] aziendali. Una caratteristica chiave di questo repository è che le API sono ortogonali al tipo di oggetto business. Invece di utilizzare un&#39;API POST, GET, PUT, PATCH o DELETE che indica il tipo di risorsa nel suo endpoint API, ci sono solo 6 endpoint generici, ma accettano o restituiscono un parametro che indica il tipo di oggetto quando è necessario tale parametro. Lo schema deve essere registrato con l&#39;archivio, ma oltre a questo, l&#39;archivio è utilizzabile per un set di tipi di oggetto aperto.

Oltre alle intestazioni elencate sopra, le API per creare, leggere, aggiornare, eliminare e interrogare gli oggetti del repository hanno le seguenti convenzioni:

- I percorsi endpoint per tutte le API del repository iniziano con `https://platform.adobe.io/data/core/xcore/`.

I formati di payload API sono negoziati con un&#39; `Accept` intestazione o `Content-Type` . I formati dei messaggi nell&#39; `Accept` intestazione o nell&#39; `Content-Type` intestazione sono indicati da un valore `application/vnd.adobe.platform.xcore.{FORMAT}+json` in cui {FORMAT} dipende dalla richiesta o dal messaggio di risposta API dell&#39;archivio specifico, secondo la tabella seguente.

| FORMATO variante | Descrizione dell’entità richiesta o risposta |
| --- | --- |
| seguita<br>da un parametro `schema={schemaId}` | Il messaggio contiene un&#39;istanza descritta da uno schema JSON indicato dallo schema del parametro format. L’istanza viene racchiusa in una proprietà JSON `_instance`. Le altre proprietà di livello principale nel payload di risposta specificano le informazioni del repository disponibili per tutte le risorse.  I messaggi conformi al formato HAL hanno una `_links` proprietà che contiene riferimenti in formato HAL. |
| `patch.hal` | Il messaggio contiene un payload JSON PATCH con il presupposto che l’istanza da patch sia conforme a HAL. Ciò significa che non solo le proprietà dell&#39;istanza, ma anche i collegamenti HAL dell&#39;istanza possono essere patch. Si noti che esistono restrizioni sulle proprietà che possono essere aggiornate dal client. |
| `home.hal` | Il messaggio contiene una rappresentazione in formato JSON di una risorsa del documento principale per l&#39;archivio. |
| xdm.receipt | Il messaggio contiene una risposta in formato JSON per un&#39;operazione di creazione, aggiornamento (completo e patch) o eliminazione. Le ricevute contengono dati di controllo che indicano la revisione dell&#39;istanza sotto forma di ETag. |

L&#39;utilizzo di ciascuna variante **di** formato dipende dall&#39;API specifica:

| API | Intestazione Content-Type | Accetta intestazione |
| --- | --- | --- |
| Crea contenitore <br/>di creazione istanza | `hal`<br/>con parametro dello schema | `xdm.receipt` |
| Aggiorna contenitore<br/>InstanceUpdate | `hal`<br/>con parametro dello schema | `xdm.receipt` |
| Istanza patch | `patch.hal` | `xdm.receipt` |
| Elimina contenitore<br/>instanceDelete | N/D | `xdm.receipt` |
| Leggi contenitore<br/>InstanceRead | N/D | `hal` con `schema` parametro |
| Elenca contenitori<br/>instanceList | N/D | `hal` con `schema` parametro speciale `https://ns.adobe.com/experience/xcore/hal/results` |
| Ricerca di istanze | N/D | hal con `schema` parametro speciale `https://ns.adobe.com/experience/xcore/hal/results` |
| Leggi radice repo | N/D | `home.hal` |

Per le API create, aggiornate e lette del contenitore, lo schema del parametro del formato ha il valore `https://ns.adobe.com/experience/xcore/container`.

`ContainerId` è il primo parametro di percorso per le API di istanza. Tutte le entità aziendali risiedono in ciò che viene chiamato contenitore. Un contenitore è un meccanismo di isolamento per tenere distanti le diverse preoccupazioni. Il primo elemento percorso per le API dell&#39;istanza del repository che segue l&#39;endpoint generale è l&#39; `containerId`. L’identificatore è ottenuto dall’elenco di contenitori accessibili al chiamante. Ad esempio, l&#39;API per creare un&#39;istanza in un contenitore è `POST https://platform.adobe.io/data/core/xcore/{containerId}/instances`.

L&#39;elenco dei contenitori accessibili viene ottenuto chiamando l&#39;endpoint radice del repository &quot;/&quot; con una richiesta HTTP GET utilizzando le intestazioni standard.

## Gestione dell&#39;accesso ai contenitori

Un amministratore può raggruppare entità, risorse e autorizzazioni di accesso simili in profili. Questo riduce il carico di gestione ed è supportato dall’interfaccia utente [Admin Console  di](https://adminconsole.adobe.com)Adobe. È necessario essere un amministratore di prodotto per  Adobe Experience Platform nell&#39;organizzazione per creare profili e assegnare utenti a tali profili.

È sufficiente creare profili di prodotto che corrispondano a determinate autorizzazioni in un unico passaggio e quindi aggiungere semplicemente gli utenti a tali profili. I profili fungono da gruppi ai quali sono state concesse autorizzazioni e ogni utente reale o tecnico del gruppo eredita tali autorizzazioni.

### Elenca contenitori accessibili a utenti e integrazioni

Quando l’amministratore ha concesso l’accesso ai contenitori per utenti o integrazioni regolari, tali contenitori saranno visualizzati nell’elenco &quot;Home&quot; del repository. L’elenco può essere diverso per utenti o integrazioni diversi in quanto è un sottoinsieme di tutti i contenitori accessibili al chiamante. L&#39;elenco dei contenitori può essere filtrato in base alla loro associazione ai contesti dei prodotti. Il parametro del filtro viene chiamato `product` e può essere ripetuto. Se viene fornito più di un filtro contesto del prodotto, verrà restituita l&#39;unione dei contenitori che hanno associazioni con uno qualsiasi dei contesti del prodotto specificati. È possibile associare un singolo contenitore a più contesti di prodotto.

Il contesto dei [!DNL Platform][!DNL Decisioning Service] contenitori è attualmente `dma_offers`.

>[!NOTE]
>
>Il contesto per [!DNL Platform Decisioning Containers] sta per cambiare presto in `acp`. Il filtraggio è facoltativo, ma i filtri solo per `dma_offers` una versione futura richiedono modifiche. Per prepararsi a questa modifica, i client non devono utilizzare filtri o applicare entrambi i contesti di prodotto come filtro.

**Richiesta**

```shell
curl -X GET {ENDPOINT_PATH}/?product=dma_offers&product=acp \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.home.hal+json' \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' 
```

**Risposta**

```json
{ 
    "_embedded": { 
        "https://ns.adobe.com/experience/xcore/container": [ 
            { 
              "instanceId": "82d1f250-85b6-11e9-ac80-99ba4655b277", 
              "schemas": [ 
                "https://ns.adobe.com/experience/xcore/container;version=0.1" 
              ], 
              "productContexts": [ 
                "dma_offers" 
              ], 
              "repo:etag": 1, 
              "repo:createdDate": "2019-06-03T04:17:33.684Z", 
              "repo:lastModifiedDate": "2019-06-03T04:17:33.684Z", 
              "repo:createdBy": "CREATOR_ACCOUNT_ID", 
              "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
              "repo:createdByClientId": "CLIENT_ID_OR_API_KEY", 
              "repo:lastModifiedByClientId": "CLIENT_ID_OR_API_KEY", 
              "_instance": { 
                "repo:name": "My Organization's container", 
                "dataCenter": "VA7" 
              }, 
              "_links": { 
                "self": { 
                  "href": "/containers/82d1f250-85b6-11e9-ac80-99ba4655b277" 
                } 
              } 
            } 
        ] 
    }, 
    "_links": { 
        "self": { 
            "href": "/"  
        } 
    } 
}  
```

Prendete nota degli elementi `instanceId` elencati negli elementi dei risultati. Viene utilizzato come `containerId` parametro nelle API per leggere e manipolare gli oggetti aziendali normali.

L’elenco è già filtrato per gli utenti in base ai loro privilegi di accesso, ma può essere ulteriormente filtrato tramite una query di proprietà.

## API generiche per gestire le entità

### Creare istanze

L&#39;API per creare una nuova istanza nell&#39;archivio utilizza un parametro `containerId` path e identifica il tipo di istanza nell&#39;intestazione con il parametro `Content-Type` schema.

Le proprietà dell&#39;istanza sono riportate nel payload racchiuso nella `_instance` proprietà. Le proprietà dell&#39;istanza devono essere valide rispetto allo schema JSON con l&#39;identificatore dello schema specificato.

La `_links` proprietà HAL deve essere presente ma può essere vuota. Ciò significa che non sono definiti collegamenti personalizzati per questa istanza.

**Richiesta**

```shell
curl -X POST {ENDPOINT_PATH}/{CONTAINER_ID}/instances \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '{ 
    "_instance": { 
        {JSON_PAYLOAD} 
    }, 
    "_links": { 
    } 
}' 
```

**Risposta**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "GENERATED_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "YOUR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
}
```

La risposta contiene l&#39;instanceId dell&#39;oggetto appena creato. Questo instanceId è immutabile, è sempre assegnato dall&#39;archivio e univoco a livello globale. Il valore funge da identificatore fisico.

Inoltre, un URI (Universal Resource Identifier) viene restituito nella `@id` proprietà del payload di risposta se lo schema dispone di tale proprietà. Ogni istanza deve avere una proprietà che funga da URI e la chiave primaria dell&#39;istanza. Questo identificatore viene utilizzato da un’altra istanza per creare relazioni con la nuova istanza, anche tra tipi diversi. Nella versione corrente, gli URI vengono generati dalla directory archivio e sono contenuti nella `@id` proprietà. Le versioni future potrebbero allentare questa regola e consentire ai client di gestire i propri valori URI e assegnare un nome alla proprietà che la contiene.

Tenete presente che questi URI non sono URL e non forniscono un modo per recuperare direttamente la risorsa. Per indicare questo aspetto, l&#39;URI ha il prefisso di uno schema URI che non specifica un protocollo di recupero. Tuttavia, gli URI possono essere utilizzati per cercare l&#39;istanza con una query.

La risposta REST avrà un&#39;intestazione Posizione che contiene un componente URL che può essere utilizzato per recuperare l&#39;istanza appena creata. Questo componente è un riferimento URI relativo e deve essere applicato all’URI di base del repository. L&#39;URI di base viene restituito nell&#39; `Content-Base` intestazione.

La `repo:etag` proprietà specifica la revisione dell&#39;istanza. Questo valore può essere utilizzato nelle operazioni di aggiornamento per garantire coerenza. L’intestazione HTTP `If-Match` può essere utilizzata per aggiungere una condizione a una chiamata API PUT o PATCH che garantisca che non vi siano altre modifiche all’istanza che potrebbero accidentalmente essere sovrascritte. Il `repo:etag` valore viene restituito con ogni chiamata di creazione, lettura, aggiornamento, eliminazione e query. Il valore viene utilizzato come valore nell&#39; ` If-Match` intestazione, in base alla [RFC7232 Section 3.1](https://tools.ietf.org/html/rfc7232#section-3.1).

Le proprietà rimanenti indicano quale account e quale chiave API è stata utilizzata per creare e per modificare l&#39;istanza. Poiché l’istanza è stata creata da questa chiamata, i rispettivi valori sono quelli della richiesta.

### Ricerca di un’istanza per ID

Utilizzando l’URL nell’intestazione Posizione restituita con la chiamata Create, un’applicazione può cercare un’istanza.

**Richiesta**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

>[!NOTE]
>
>Sebbene `instanceId` venga fornito come parametro di percorso, le applicazioni non dovrebbero, se possibile, creare il percorso stesso e seguire i collegamenti alle istanze contenute nelle operazioni di elenco e di ricerca. Per ulteriori informazioni, vedere le sezioni ‎ 6.4.4 e ‎ 6.4.6.

**Risposta**

```json
{ 
  "instanceId": "ID_OF_THIS_INSTANCE", 
  "schemas": [ 
    "SCHEMA_ID_OF_INSTANCE" 
  ], 
  "repo:etag": 1, 
  "repo:createdDate": "2019-03-24T15:52:12.725Z", 
  "repo:lastModifiedDate": "2019-03-24T15:52:12.725Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
  "_instance": { 
    JSON_PROPERTIES_OF_THIS_INSTANCE 
  }, 
  "_links": { 
    "self": { 
      "name": "GENERATED_UNIQUE_LINK_NAME", 
      "href": "RELATIVE_URL_TO_INSTANCE" 
    } 
  } 
} 
```

Le proprietà JSON dell&#39;istanza sono racchiuse nella `_instance` proprietà e le altre proprietà di livello principale contengono i metadati relativi all&#39;istanza.

La risorsa contiene anche un array di ID di schema JSON. Questa matrice indica gli schemi JSON con cui questa istanza viene convalidata.

Ogni istanza contiene un collegamento HAL del tipo di relazione self che corrisponde all&#39;autorelazione registrata IANA (come definita dal [RFC5988]).

**Test per le nuove revisioni di un&#39;istanza**

Il `eTag` valore corrente dell&#39;istanza viene restituito con la risposta, che consente ai client di eseguire operazioni condizionali rispetto all&#39;istanza, sia per evitare di recuperare nuovamente lo stesso stato della risorsa, sia per evitare di sovrascrivere i valori di una revisione successiva senza che il cliente ne sia a conoscenza.

L&#39;API di ricerca consente a un client di specificare un parametro di `If-None-Match` intestazione. Vedere la definizione di questo parametro HTTP standard [RFC2616]. Il valore del tag di entità specificato dal client è il valore ricevuto con la risposta più recente, da una chiamata API di aggiornamento, lettura, elenco o ricerca. Il `etag` valore deve essere opaco per il client e deve essere indicato come stringa, racchiuso tra virgolette.

**Richiesta**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'If-None-Match: "{LAST_RECEIVED_ETAG}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

L&#39;API repository risponderà con uno stato 304 Non modificato quando l&#39;ultima revisione dell&#39;istanza è quella con il tag specificato.

### Elenca le istanze di uno schema - Ordinamento e paging

I client non saranno in grado di tenere traccia delle istanze che stanno creando e quindi di accedervi tramite il loro instanceId fisico. L&#39;utilizzo dell&#39;API Leggi istanza sarà l&#39;eccezione. I client non sono inoltre a conoscenza delle istanze create da altri client.

Un pattern di accesso più tipico consiste nell&#39;scorrere le pagine del set di tutte le istanze.

**Richiesta**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}" \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Risposta**

La risposta dipende dalla risposta `{schemaId}` specificata. Ad esempio, per &quot;https<span></span>://ns.adobe.com/experience/offer-management/offer-activity&amp;id=xcore:offer-activity:fa24f9e8fc15c73&quot; la risposta è simile a quella riportata di seguito.

```json
{
"requestTime": "2019-06-28T06:54:05.606Z",
"_embedded": {
  "results": [],
  "total": 0,
  "count": 0
  },
  "_links": {
  "self": {
  "href": "/653da250-71b8-11e9-a3fe-9b1d0913f3ed/instances?schema=https://ns.adobe.com/experience/offer-management/offer-activity&id=xcore:offer-activity:fa24f9e8fc15c73",
"@type": "https://ns.adobe.com/experience/xcore/hal/results"
  }
  },
  "containerId": "653da250-71b8-11e9-a3fe-9b1d0913f3ed",
  "schemaNs": "https://ns.adobe.com/experience/offer-management/offer-activity;version=0.1"
}
```

>[!NOTE]
>
>Il risultato contiene le istanze per lo schema specificato o per la prima pagina dell&#39;elenco. Nota: le istanze possono essere conformi a più schemi e quindi visualizzate in più elenchi.

Le risorse di pagina sono transitorie e di sola lettura; non possono essere aggiornate o eliminate. Il modello di paging consente l&#39;accesso casuale ai sottoinsiemi di elenchi di grandi dimensioni per un periodo di tempo prolungato senza mantenere alcuno stato per client.

Per accedere a un elenco di istanze per pagina in questo modo, deve essere possibile definire un ordinamento stabile sulle voci enumerate da tale elenco di istanze. Nota: &quot;stable&quot; non indica che le istanze verranno visualizzate in una pagina predeterminata. Infatti, quando un ordine di pagina viene formato ordinando le istanze in base a una proprietà P e un client aggiorna questa proprietà P, un altro client potrebbe raggiungere di nuovo l&#39;istanza su una pagina diversa durante il paging dell&#39;elenco. In altre parole, il modello favorisce la restituzione di risultati più recenti.

Tuttavia, se l&#39;ordinamento è basato su una proprietà non modificabile, l&#39;ordinamento &quot;stable&quot; garantisce il raggiungimento di tutte le istanze esistenti all&#39;inizio dell&#39;operazione di paging (a meno che non siano state eliminate al momento del raggiungimento della pagina). Quando questo ordinamento si trova in una proprietà che aumenta monotonalmente, vengono raggiunte anche le istanze create dopo l&#39;avvio dell&#39;operazione di paging.

Un client può fornire suggerimenti sulle dimensioni di pagina desiderate, ma spetta interamente al repository fornire più o meno istanze con la pagina restituita. Per garantire l&#39;ordine stabile, il servizio deve aggiungere o rimuovere elementi dalla pagina in modo che il valore della proprietà di ordinamento sia diverso tra i bordi delle pagine. In questo modo la pagina successiva non conterrà più alcuni elementi dell&#39;ultima pagina o in uno scenario di peggiore probabilità si bloccherà con gli stessi elementi in ogni pagina.

La paging è controllata dai seguenti parametri:

- **`orderBy`**: Contiene un elenco ordinato e separato da virgole di proprietà in base al quale viene ordinato l&#39;elenco delle istanze. La prima proprietà viene utilizzata per l&#39;ordinamento principale, la seconda proprietà per risolvere i legami nell&#39;ordinamento principale e così via. Quando viene specificata una proprietà con un valore univoco per istanza, i legami non sono possibili e dopo ogni elemento può verificarsi un&#39;interruzione di pagina. Il nome di una proprietà può avere il prefisso `+` per indicare l&#39;ordine crescente o `-` per indicare l&#39;ordine decrescente di tale proprietà. Se il nome della proprietà non ha un prefisso, il risultato viene ordinato in ordine crescente. Se non `orderBy` è specificato nella richiesta, l&#39;archivio utilizzerà invece la proprietà instanceId fisica.
- **`start`**: I client utilizzano il parametro start per definire la pagina da recuperare. Il parametro start determina l’inizio della pagina desiderata. La risposta conterrà istanze che iniziano con quelle con un valore di `orderBy` proprietà rigorosamente maggiore di (per crescente) o rigorosamente minore (per decrescente) del valore specificato. Quando il parametro query non viene specificato, per impostazione predefinita viene utilizzato un valore instanceId che esegue l&#39;ordinamento prima dell&#39;identificatore della prima istanza possibile, pertanto questo valore viene omesso dalla prima pagina.
- **`limit`**: specifica un numero intero positivo come suggerimento sul numero massimo di elementi da restituire per una determinata richiesta. Le dimensioni effettive della risposta possono essere inferiori o maggiori, in quanto limitate dalla necessità di fornire un funzionamento affidabile del parametro start

### Elenchi di filtri

Il filtraggio dei risultati dell&#39;elenco è possibile e avviene indipendentemente dal meccanismo di paging. I filtri ignorano semplicemente le istanze nell&#39;ordine degli elenchi o chiedono esplicitamente di includere solo le istanze che soddisfano una determinata condizione. Un client può richiedere che l&#39;espressione della proprietà venga utilizzata come filtro oppure può specificare un elenco di URI da utilizzare come valori della chiave primaria delle istanze.

- **`property`**: Contiene un percorso nome proprietà seguito da un operatore di confronto seguito da un valore. <br/>
L&#39;elenco delle istanze restituite contiene quelle per le quali l&#39;espressione restituisce true. Ad esempio, se l&#39;istanza ha una proprietà payload 
`status` e i valori possibili sono `draft`, `approved`, `archived` , e `deleted` il parametro query `property=_instance.status==approved` restituisce solo le istanze per le quali lo stato è approvato. <br/>
<br/>
La proprietà da confrontare con il valore specificato è identificata come percorso. I singoli componenti del tracciato sono separati da `.`, come: `_instance.xdm:prop1.xdm:prop1_1.xdm:prop1_1_1`<br/>

Per le proprietà con valori stringa, numerici o data/ora, gli operatori consentiti sono: `==`, `!=`, `<`, `<=`, `>` e `>=`. Inoltre, per le proprietà con un valore stringa, `~` è possibile utilizzare un operatore. L&#39; `~` operatore corrisponde alla proprietà specificata in base a un&#39;espressione regolare. Il valore stringa della proprietà deve corrispondere all&#39; **intera** espressione affinché le entità vengano incluse nei risultati filtrati. Ad esempio, la ricerca della stringa `cars` in un punto qualsiasi all&#39;interno del valore della proprietà richiede l&#39;espressione regolare `.*cars.*`. Senza l&#39;interlinea o `.*`la fine, solo le entità corrispondono a un valore di proprietà che inizia o termina rispettivamente con `cars`. Per l&#39; `~` operatore, il confronto tra i caratteri lettera non fa distinzione tra maiuscole e minuscole. Per tutti gli altri operatori, il confronto fa distinzione tra maiuscole e minuscole.<br/><br/>
Non solo le proprietà payload dell&#39;istanza possono essere utilizzate nelle espressioni filtro. Le proprietà dell&#39;involucro vengono confrontate allo stesso modo, ad esempio `property=repo:lastModifiedDate>=2019-02-23T16:30:00.000Z`. <br/>
<br/>
Il parametro di `property` query può essere ripetuto in modo da applicare più condizioni di filtro, ad esempio per restituire tutte le istanze che sono state modificate dopo una determinata data e prima di una determinata data. I valori in tali espressioni devono essere codificati nell’URL. Se non viene specificata alcuna espressione e il nome della proprietà viene semplicemente elencato, gli elementi idonei sono quelli con una proprietà con il nome specificato.<br/>
<br/>

- **`id`**: A volte un elenco deve essere filtrato dall’URI delle istanze. Il parametro di `property` query può essere utilizzato per filtrare un&#39;istanza, ma per ottenere più di un&#39;istanza, è possibile fornire alla richiesta un elenco di URI. Il `id` parametro viene ripetuto e ogni occorrenza specifica un valore URI. `id={URI_1}&id={URI_2},…` I valori URI devono essere codificati nell’URL.

I risultati della pagina vengono restituiti come tipo mime speciale `application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results"`.

**Richiesta**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}"&orderby${ORDER_BY_PROPERTY_PATH}&property={TIMESTAMP_PROPERTY_PATH}>=2019-02-19T03:19:03.627Z&property${TIMESTAMP_PROPERTY_PATH}<=2019-06-19T03:19:03.627Z \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Risposta**

```json
{ 
  "requestTime": "2019-06-10T22:12:13.642Z", 
  "_embedded": { 
    "results": [ 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T03:19:03.627Z", 
        "repo:lastModifiedDate": "2019-04-19T03:19:03.627Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 
        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      }, 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T20:30:31.361Z", 
        "repo:lastModifiedDate": "2019-04-19T20:30:31.361Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 

        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      } 
    ], 
    "total": 2, 
    "count": 2 
  }, 
  "_links": { 
    "self": { 
      "href": "RELATIVE_URL_TO_THIS_RESULT" 
    } 
  }, 
  "containerId": "CONTAINER_ID_OF_THIS_LIST", 
  "schemaNs": "SCHEMA_ID_OF_INSTANCE_LIST" 
} 
```

La risposta contiene l&#39;elenco degli elementi dei risultati all&#39;interno dei risultati della proprietà JSON accanto a due proprietà che indicano il numero di risultati in questa pagina e il numero totale di elementi nell&#39;elenco filtrato a partire dalla pagina appena restituita.

### Ricerca full-text e query strutturate

Nei casi in cui i client desiderano fornire condizioni di filtro più complesse e le istanze di ricerca in base ai termini contenuti nelle proprietà stringa, l&#39;archivio offre un&#39;API di ricerca più potente.

**Richiesta**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/queries/core/search?schema="{SCHEMA_ID}"&… \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

<!-- TODO: needs example response -->

Oltre ai parametri di paging e filtro delle API elenco, questa API consente ai client di aggiungere parametri full text e query booleane.

La ricerca full text è controllata dai seguenti parametri:

- **`q`**: Contiene un elenco non ordinato separato da spazi di termini normalizzati prima che venga confrontato con eventuali proprietà stringa delle istanze. Le proprietà delle stringhe vengono analizzate in base ai termini e anche questi vengono normalizzati. La query di ricerca tenta di corrispondere a uno o più dei termini specificati nel `q` parametro. I caratteri +, -, =, &amp;&amp;, ||, >, &lt;,!, (,), {, }, [,]^, &quot;, ~, *, ?, :, / hanno un significato speciale per determinare i limiti della parola all&#39;interno della stringa di query e devono essere preceduti da una barra rovesciata quando vengono visualizzati in un token che deve corrispondere al carattere. La stringa di query può essere racchiusa tra virgolette doppie per ottenere una corrispondenza esatta tra le stringhe e per evitare i caratteri speciali.
- **`field`**: Se i termini di ricerca devono essere associati solo a un sottoinsieme delle proprietà, il parametro field può indicare il percorso di tale proprietà. Il parametro può essere ripetuto per indicare più proprietà alle quali deve essere confrontata.
- **`qop`**: Contiene un parametro di controllo utilizzato per modificare il comportamento corrispondente della ricerca. Quando il parametro è impostato su e allora tutti i termini di ricerca devono corrispondere e quando il parametro è assente o il suo valore è impostato su o allora uno qualsiasi dei termini può conteggiare per una corrispondenza.

### Aggiornamento e patch delle istanze

Per aggiornare un&#39;istanza, un client può sovrascrivere l&#39;elenco completo delle proprietà contemporaneamente oppure utilizzare una richiesta JSON PATCH per manipolare singoli valori di proprietà, inclusi gli elenchi.

In entrambi i casi l&#39;URL della richiesta specifica il percorso dell&#39;istanza fisica e in entrambi i casi la risposta sarà un payload di ricevuta JSON come quello restituito dall&#39;operazione [di](#create-instances)creazione. Un client deve preferibilmente utilizzare l&#39; `Location` intestazione o un collegamento HAL ricevuto da una chiamata API precedente per questo oggetto come percorso URL completo per questa API. Se questo non è possibile, il client può creare l’URL dal `containerId` e dal `instanceId`.

**Richiesta** (PUT)

```shell
curl -X PUT {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'\ 
  -d '{ 
  "_instance": { 
    {JSON_PROPERTIES_OF_THIS_INSTANCE} 
  }, 
  "_links": { 
    {HAL_LINKS_OF_THIS_INSTANCE} 
  } 
}'  
```

**Request** (PATCH)

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '[ 
  { 
    {JSON_PATCH_INSTRUCTIONS_FOR_THIS_INSTANCE} 
  } 
]'
```

La richiesta PATCH applica le istruzioni e quindi convalida l&#39;entità risultante rispetto allo schema e alle stesse regole di integrità entità e referenziale della richiesta PUT.

**Controllo delle modifiche dei valori delle proprietà**

Potete impedire che le proprietà vengano impostate al momento della creazione e/o dell&#39;aggiornamento, utilizzando le seguenti annotazioni:

- **`"meta:usereditable"`**: Booleano: quando una richiesta proviene da un agente utente che identifica il chiamante con un token di accesso utente o tecnico dell&#39;account, le proprietà annotate con `"meta:usereditable": false` non devono essere presenti nel payload. Se lo sono, non devono avere un valore diverso da quello attualmente impostato. Se i valori differiscono, la richiesta di aggiornamento o patch viene rifiutata con lo stato 422 Entità non elaborabile.
- **`"meta:immutable"`**: Booleano - Le proprietà annotate con `"meta:immutable": true` non possono essere modificate una volta impostate. Ciò vale per le richieste provenienti da un utente finale, l&#39;integrazione di un account tecnico o un servizio speciale.

**Test per aggiornamento simultaneo**

Esistono delle condizioni in cui più client tentano di aggiornare contemporaneamente un’istanza. Il repository è gestito su un cluster di nodi di calcolo senza gestione centrale delle transazioni. Per evitare che un client scriva un&#39;istanza scritta simultaneamente da un altro client, questi può utilizzare un aggiornamento condizionale o una richiesta di patch. Specificando la `etag` stringa nell’intestazione `If-Match` l’archivio verifica che solo la prima richiesta abbia esito positivo e che le richieste successive da parte di altri client che utilizzano lo stesso `etag` valore non riescano. Il `etag` valore cambia con ogni modifica dell&#39;istanza. I client devono recuperare l&#39;istanza per ottenere il `etag` valore più recente e solo un client su molti tentativi di aggiornamento può riuscire con tale valore. Altri clienti verranno rifiutati con un messaggio 409 Conflict.

### Eliminazione delle istanze

Le istanze possono essere eliminate con una chiamata DELETE. Un client deve preferibilmente utilizzare l&#39; `Location` intestazione o un collegamento HAL ricevuto da una chiamata API precedente per questo come percorso URL completo. Se questo non è possibile, il client può creare l&#39;URL dal `containerId` e dal fisico `instanceId`.

**Richiesta**

```shell
curl -X DELETE {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Risposta**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "INSTANCE_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "CREATOR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
} 
```

Dopo aver ricevuto una richiesta di eliminazione, il repository verifica la presenza di altre istanze di qualsiasi schema, facendo comunque riferimento all&#39;istanza da eliminare. In un sistema distribuito e altamente disponibile, l&#39;integrità referenziale non può essere controllata immediatamente. In presenza di relazioni chiave esterne definite, i controlli verranno eseguiti in modo asincrono. Ciò comporta un leggero ritardo nella risposta all&#39;esito della richiesta di eliminazione. Quando tali controlli vengono eseguiti, la risposta immediata include lo stato 202 Accettato e un collegamento per verificare il risultato dell&#39;operazione di eliminazione nell&#39; `Location` intestazione. Il cliente deve quindi verificare il collegamento per verificare il risultato.

Se viene trovata un&#39;istanza che fa riferimento all&#39;istanza da eliminare, il risultato sarà un rifiuto dell&#39;operazione di eliminazione. Se non vengono rilevati altri riferimenti di chiave esterna, l&#39;eliminazione viene completata. Se il risultato non è ancora deciso, la risposta indicherà che entro altri 202 risposte accettate con la stessa `Location` intestazione e chiederà al cliente di continuare a controllare. Una volta determinato il risultato, la risposta indicherà che con uno stato Ok 200 e il payload della risposta conterrà il risultato della richiesta di eliminazione originale. La risposta 200 Ok indica solo che il risultato è noto e che il corpo della risposta conterrà la conferma o il rifiuto della richiesta di eliminazione.

## Creazione di offerte e relativi componenti secondari

Le API descritte nella sezione precedente si applicano uniformemente a tutti i tipi di oggetti aziendali. L&#39;unica differenza tra, ad esempio, la creazione di un&#39;offerta e un&#39;attività sarebbe l&#39; `content-type` intestazione che rileva lo schema JSON il payload JSON della richiesta conforme allo schema. Pertanto, le sezioni seguenti dovranno concentrarsi solo su tali schemi e sulle loro relazioni.

Quando si utilizzano le API con il tipo di contenuto `application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"`, le proprietà dell&#39;istanza vengono incorporate nella `_instance` proprietà accanto alla quale è presente una `_links` proprietà. Questo sarà il formato generale in cui tutte le istanze sono rappresentate:

```json
{ 
  … ENVELOPE PROPERTIES 
  "_instance": { 
    INSTANCE PROPERTIES 
  }, 
  "_links": {
    HAL PROPERTIES 
  } 
}
```

>[!NOTE]
>
>Per motivi di brevità, in tutti gli snippet JSON solo le proprietà dell&#39;istanza sono illustrate e solo quando è richiesto vengono visualizzate le proprietà busta e la sezione _links.

### Proprietà generali delle offerte

Le offerte sono un tipo di opzione di decisione e lo schema JSON delle offerte eredita le proprietà standard delle opzioni che ogni istanza di opzione avrà.

- **`@id`** - Un identificatore univoco per ciascuna opzione che è la chiave primaria e utilizzato per fare riferimento all&#39;opzione di altri oggetti. Questa proprietà viene assegnata quando l&#39;istanza viene creata, è immutabile e non modificabile.
- **`xdm:name`** - Ogni opzione ha un nome che viene utilizzato per scopi di ricerca e visualizzazione. Il nome non è immutabile e non può essere utilizzato per identificare l&#39;istanza in modo univoco. Il nome può essere selezionato liberamente ma deve essere univoco tra le istanze delle offerte.

```json
{ 
  "@id": "INSTANCE_URI",                         // meta:immutable=true, meta:usereditable=false 
  "xdm:name": "A name for the Decision Option",  // meta:immutable=false 
  "xdm:characteristics": { 
    properties specific to this instance         // property names can vary per instance 
  } 
}
```

Consultate [Aggiornamento e patch delle istanze](#updating-and-patching-instances) per l’intera sintassi cURL. Il `schemaId` parametro deve essere `https://ns.adobe.com/experience/offer-management/personalized-offer` o `https://ns.adobe.com/experience/offer-management/fallback-offer` se l&#39;offerta è un&#39;offerta di fallback.

Ciascuna istanza di offerta può avere un set facoltativo di proprietà che sono caratteristiche solo per tale istanza. Le offerte diverse possono avere chiavi diverse per queste proprietà, ma i valori devono essere stringhe. Queste proprietà possono essere utilizzate nelle regole di decisione e segmentazione. Sono inoltre accessibili per assemblare l&#39;esperienza decisa per personalizzare ulteriormente i messaggi.

### ciclo di vita dell&#39;offerta

Esiste un flusso di transizione dello stato semplice che tutte le Opzioni seguiranno. Cominciano in uno stato bozza e quando sono pronti il loro stato sarà impostato su approvato. Una volta trascorsa la data di fine, possono essere spostati nello stato di archiviazione. In questo stato, possono essere eliminati o riutilizzati spostandoli di nuovo nello stato di bozza.

![](../images/entities/offer-lifecycle.png)

- **`xdm:status`** - Questa proprietà viene utilizzata per la gestione del ciclo di vita dell&#39;istanza. Il valore rappresenta uno stato del flusso di lavoro utilizzato per indicare se l&#39;offerta è ancora in costruzione (valore = bozza), può essere generalmente considerata dal runtime (valore = approvato) o se non deve più essere utilizzata (valore = archiviato).

Una semplice operazione PATCH sull’istanza viene in genere utilizzata per manipolare una `xdm:status` proprietà:

```json
[
  {
    "op":    "replace",
    "path":  "/_instance/xdm:status",
    "value": "approved" 
  }
]
```

Consultate [Aggiornamento e patch delle istanze](#updating-and-patching-instances) per l’intera sintassi cURL. Il `schemaId` parametro deve essere `https://ns.adobe.com/experience/offer-management/personalized-offer` o `https://ns.adobe.com/experience/offer-management/fallback-offer` se l&#39;offerta è un&#39;offerta di fallback.

### Rappresentazioni e posizionamenti

Le offerte sono opzioni decisionali con rappresentazioni dei contenuti. Quando viene presa una decisione, l&#39;opzione viene scelta e il relativo identificatore viene utilizzato per ottenere i riferimenti di contenuto o di contenuto per la posizione da specificare. Un&#39;offerta può avere più di una rappresentazione, ma ciascuna di esse deve avere un riferimento di posizionamento diverso. In questo modo, con un determinato posizionamento, la rappresentazione può essere determinata in modo non ambiguo.
Durante l&#39;operazione di decisione, la posizione viene determinata insieme all&#39;oggetto activity. Le offerte che non dispongono di una rappresentazione con tale posizione come riferimento vengono eliminate automaticamente dall&#39;elenco delle scelte.

Prima che sia possibile aggiungere delle rappresentazioni a un&#39;offerta, le istanze di posizionamento devono esistere. Tali istanze vengono create con l&#39;identificatore`https://ns.adobe.com/experience/offer-management/offer-placement`dello schema.

```json
{
  "xdm:name": "Kiosk Placement 1",
  "xdm:channel": "https://ns.adobe.com/xdm/channels/web",
  "xdm:componentType": 
     "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
  "xdm:contentTypes": [
    "image/png", "image/png"
  ],
  "xdm:description": "Generic placeholder for offers in the Kiosk application. \nTechnical constraints: max width 530dpi, min width 480 dpi, aspect ratio 12:5. \nStylistic constraints: single background color with text block in complementary colors, \nNo magenta, please!"
} 
```

Consultate [Aggiornamento e patch delle istanze](#updating-and-patching-instances) per l’intera sintassi cURL. Il `schemaId` parametro deve essere `https://ns.adobe.com/experience/offer-management/personalized-offer` o `https://ns.adobe.com/experience/offer-management/fallback-offer` se l&#39;offerta è un&#39;offerta di fallback.

Un&#39;istanza **Placement** può avere le seguenti proprietà:

- **`xdm:name`** - Contiene il nome assegnato per il posizionamento per farvi riferimento nelle interazioni umane e nelle interfacce utente.
- **`xdm:description`** - Utilizzato per trasmettere intenzioni leggibili dall&#39;uomo su come il contenuto di questo posizionamento viene utilizzato nella distribuzione complessiva del messaggio. Quando i canali di distribuzione definiscono nuovi posizionamenti, possono aggiungere ulteriori informazioni in questa proprietà in modo che un creatore di contenuti possa creare o selezionare il contenuto di conseguenza. Tali istruzioni non sono interpretate o applicate formalmente. Questa proprietà serve solo come luogo per comunicare le intenzioni.
- **`xdm:channel`** - L&#39;URI di un canale. Il canale indica dove deve essere distribuito il contenuto dinamico. Il vincolo di canale viene utilizzato per trasmettere non solo la posizione in cui verrà utilizzata l&#39;offerta, ma anche per determinare l&#39;editor di contenuto o il validatore utilizzato per l&#39;esperienza.
- **`xdm:componentType`** - Un identificatore del modello, ovvero URI, per il contenuto che può essere visualizzato nella posizione descritta da questa posizione. I tipi di componente sono: collegamento immagine, HTML o testo normale. Ciascun tipo di componente può includere un set specifico di proprietà (un modello) che l’elemento contenuto può avere. L’elenco dei tipi di componenti può essere esteso. Esistono tre valori predefiniti per il tipo di componente:
   - `https://ns.adobe.com/experience/offer-management/content-component-imagelink`
   - `https://ns.adobe.com/experience/offer-management/content-component-text`
   - `https://ns.adobe.com/experience/offer-management/content-component-html`
- **`xdm:contentTypes`**, Un vincolo per i tipi di supporti dei componenti previsti in questa posizione. Per un tipo di componente possono essere presenti più tipi di supporti, ad esempio diversi formati immagine.

**Gli elementi di rappresentazione** in un&#39;offerta presentano una struttura di oggetto nella proprietà array `xdm:representations`. Ogni elemento può avere le seguenti proprietà:

- **`xdm:placement`** - Questa proprietà contiene il riferimento all&#39;istanza di posizionamento. Il valore viene controllato quando la rappresentazione viene aggiunta all&#39;offerta. Un&#39;istanza di posizionamento con tale URI deve esistere e non deve essere contrassegnata come eliminata. Inoltre, viene eseguito un controllo per garantire che un&#39;istanza di offerta non contenga due rappresentazioni con lo stesso valore per il riferimento di posizionamento.
- **`xdm:components`** - I componenti contenuto sono i frammenti associati a una particolare rappresentazione dell&#39;offerta. Tali frammenti vengono successivamente utilizzati per comporre l’esperienza dell’utente finale. Il servizio di gestione delle decisioni di per sé non compone l’esperienza utente finale completa. Le seguenti proprietà fanno parte del modello di ogni componente.
   - **`@type`** - questa proprietà identifica il tipo di componente. Un altro nome per questo concetto è il modello di frammento di contenuto. Il `@type` componente è semplicemente un URI per un modello definito dall’applicazione o dal servizio che sta assemblando l’esperienza dell’utente finale.
   - **`repo:id`** - questa proprietà contiene un identificatore univoco globale e immutabile per la risorsa principale del componente, presente nella directory archivio in cui è memorizzata la risorsa.
   - **`repo:name`** - Questa proprietà contiene un nome leggibile dall’utente per la risorsa nella directory archivio. Questo nome è definito dall’utente e non è garantito come univoco.
   - **`repo:resolveURL`** - questa proprietà contiene un indicatore di posizione univoco per la lettura della risorsa in un archivio dei contenuti. In questo modo sarà più facile ottenere la risorsa senza che il cliente comprenda quali API chiamare. L’URL restituisce i byte della risorsa principale.
   - **`dc:format`** - questa proprietà proviene dalla Dublin Core Metadata Initiative. Il formato può essere utilizzato per determinare il software, l&#39;hardware o altre apparecchiature necessarie per visualizzare o utilizzare la risorsa. Si consiglia di selezionare un valore da un vocabolario controllato (ad esempio, l&#39;elenco dei tipi di supporti Internet che definiscono i formati dei supporti per computer).
   - **`dc:language`** - Questa proprietà contiene la lingua o le lingue della risorsa. Le lingue sono specificate nel codice della lingua come definito in IETF RFC 3066.

Nella `@type` proprietà sono disponibili tre tipi di componenti predefiniti:

- https<span></span>://ns.adobe.com/experience/offer-management/content-component-imagelink
- https<span></span>://ns.adobe.com/experience/offer-management/content-component-text
- https<span></span>://ns.adobe.com/experience/offer-management/content-component-html

A seconda del valore della `@type` proprietà, `xdm:components` conterrà proprietà aggiuntive:

- **`xdm:linkURL`** - Presentato quando il componente è un collegamento immagine. Questa proprietà conterrà il collegamento associato all’immagine e al quale l’utente `user-agent` si sposterà quando interagisce con il contenuto dell’offerta.
- **`xdm:copyline`** - Utilizzato quando il componente è un testo. Oltre a fare riferimento a una risorsa di testo, ad esempio per il testo in formato esteso Le offerte con formattazione, una stringa di testo breve può essere memorizzata direttamente nella proprietà xdm:copyline.

I client possono utilizzare proprietà aggiuntive per impostare e valutare le istruzioni per la gestione del contesto. Ad esempio, il client Offer UI Library aggiunge le seguenti proprietà facoltative per gestire più facilmente la visualizzazione:

- All&#39;interno di ciascun elemento dell&#39; `xdm:components` array, il client dell&#39;interfaccia utente della libreria Offer aggiunge le seguenti proprietà. Tali proprietà non devono essere eliminate o modificate senza comprendere l’impatto sull’interfaccia utente:
   - **`offerui:previewThumbnail`** - Si tratta di una proprietà opzionale utilizzata dall&#39;interfaccia utente della libreria Offer per visualizzare un rendering della risorsa. Questa rappresentazione non equivale alla risorsa stessa. Ad esempio, il contenuto potrebbe essere HTML e la rappresentazione è un&#39;immagine bitmap che ne mostra solo un&#39;approssimazione. Questa rappresentazione (di qualità inferiore) viene visualizzata all’interno del blocco di rappresentazione dell’offerta.

Un esempio di operazione PATCH su un’istanza di offerta mostra come manipolare le rappresentazioni:

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:representations/-",
    "value": {
      "xdm:placement": "xcore:offer-placement:e51944a87919861",
      "xdm:components": [
        {
          "xdm:copyline": "Get what you want!",
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-text",
          "dc:format": "text/plain"
        }
      ]
    } 
  }
]' 
```

Consultate [Aggiornamento e patch delle istanze](#updating-and-patching-instances) per l’intera sintassi cURL. Il `schemaId` parametro deve essere `https://ns.adobe.com/experience/offer-management/personalized-offer` o `https://ns.adobe.com/experience/offer-management/fallback-offer` se l&#39;offerta è un&#39;offerta di fallback.

L&#39;operazione PATCH potrebbe non riuscire se non è `xdm:representations` ancora presente una proprietà. In tal caso, l&#39;operazione di aggiunta di cui sopra potrebbe essere preceduta da un&#39;altra operazione di aggiunta che crea l&#39;array oppure la singola operazione di aggiunta imposta l&#39;array direttamente. `xdm:representations` 
Gli schemi e le proprietà descritti vengono utilizzati per tutti i tipi di offerte, le offerte di personalizzazione e le offerte di fallback. Le due sezioni seguenti sui vincoli e sulle regole decisionali per spiegare gli aspetti delle offerte di personalizzazione.

## Impostazione dei vincoli delle offerte

### Limiti calendario

Le opzioni di decisione in generale possono essere data e ora di inizio e fine che fungono da vincolo di calendario. Le proprietà sono incorporate nella proprietà `xdm:selectionConstraint`:

- **`xdm:startDate`** - Questa proprietà indica la data e l&#39;ora di inizio. Il valore è una stringa formattata in base alle regole RFC 3339, ad esempio come indicato di seguito: &quot;2019-06-13T11:21:23.356Z&quot;.
Le opzioni decisionali che non hanno raggiunto la data e l&#39;ora di inizio non sono ancora considerate ammissibili nella decisione.
- **`xdm:endDate`** - Questa proprietà indica la data e l&#39;ora di fine. Il valore è una stringa formattata in base alle regole RFC 3339, ad esempio come indicato di seguito: &quot;2019-07-13T11:00:00.000Z&quot;Le opzioni decisionali che hanno superato la data e l&#39;ora di fine non sono più considerate ammissibili al processo decisionale.

La modifica di un vincolo di calendario può essere eseguita con la seguente chiamata PATCH:

```json
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint",
    "value": {
      "xdm:startDate": "2019-06-13T00:00:00.000Z",
      "xdm:endDate":   "2019-07-13T00:00:00.000Z"
    } 
  }
]' 
```

Consultate [Aggiornamento e patch delle istanze](#updating-and-patching-instances) per l’intera sintassi cURL. Il `schemaId` parametro deve essere `https://ns.adobe.com/experience/offer-management/personalized-offer`. Le offerte di fallback non presentano vincoli.

### Limiti di ritaglio

Un vincolo di capping è un componente di un&#39;opzione di decisione che definisce i parametri per il capping. Per &quot;maschiatura&quot; si intende il processo di limitazione del numero di volte che un’opzione può essere proposta, sia per un profilo singolo che per tutti i profili. Le proprietà contengono un valore intero che deve essere maggiore o uguale a 1. Le proprietà sono nidificate all&#39;interno di una proprietà `xdm:cappingConstraint`:

- **`xdm:globalCap`** - Un massimale globale è un limite per il numero totale di offerte che possono essere proposte.
- **`xdm:profileCap`** - Un limite di profilo è un limite al numero di volte che un&#39;offerta può essere proposta a un determinato profilo.

L’impostazione o la modifica del vincolo di capping su un’offerta di personalizzazione può essere effettuata con la seguente chiamata PATCH:

```json
[
  {
    "op":   "add",
    "path": "/_instance/xdm:cappingConstraint",
    "value": {
      "xdm:globalCap":  1000000,
      "xdm:profileCap": 5
    } 
  }
]' 
```

Consultate [Aggiornamento e patch delle istanze](#updating-and-patching-instances) per l’intera sintassi cURL. Il `schemaId` parametro deve essere `https://ns.adobe.com/experience/offer-management/personalized-offer`. Le offerte di fallback non presentano vincoli.

Per rimuovere i valori di capping, l&#39;operazione &quot;add&quot; viene sostituita con l&#39;operazione &quot;remove&quot;. Tenete presente che i valori di capping esistono singolarmente e possono essere impostati o rimossi anche singolarmente.

### Limiti di idoneità

Le offerte possono essere selezionate in base alle condizioni nel processo decisionale. Quando un&#39;offerta di personalizzazione ha un riferimento a una regola di idoneità, la condizione della regola deve essere valutata su true affinché l&#39;oggetto dell&#39;offerta venga preso in considerazione per un determinato profilo. Le regole di idoneità vengono create e gestite indipendentemente dalle opzioni di decisione e la stessa regola può essere utilizzata per fare riferimento a più offerte di personalizzazione.

Il riferimento alla regola è incorporato nella proprietà `xdm:selectionConstraint`:

- **`xdm:eligibilityRule`** - Questa proprietà contiene un riferimento a una regola di idoneità. Il valore è l&#39;istanza `@id` di uno schemahttps://ns.adobe.com/experience/offer-management/eligibility-rule.

L’aggiunta e l’eliminazione di una regola possono essere eseguite anche con un’operazione PATCH:

```
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint/xdm:eligibilityRule",
    "value": "xcore:eligibility-rule:f84c6b33cc63c65" 
  }
]'
```

Consultate [Aggiornamento e patch delle istanze](#updating-and-patching-instances) per l’intera sintassi cURL. Il `schemaId` parametro deve essere `https://ns.adobe.com/experience/offer-management/personalized-offer`. Le offerte di fallback non presentano vincoli.

La regola di idoneità è incorporata nella `xdm:selectionConstraint` proprietà insieme ai vincoli del calendario. Le operazioni PATCH non devono tentare di rimuovere l’intera `SelectionConstraint` proprietà.

## Impostazione della priorità di un&#39;offerta

Le opzioni di decisione idonee verranno classificate per determinare l&#39;opzione migliore per il profilo specificato. Per supportare la classifica e fornire un valore predefinito nel caso in cui la classificazione non possa essere determinata da un altro meccanismo, è possibile impostare una priorità di base per ogni offerta di personalizzazione.
La priorità di base è incorporata nella proprietà `xdm:rank`:

- **`xdm:priority`** - Questa proprietà rappresenta l&#39;ordine predefinito in cui viene selezionata un&#39;offerta su un&#39;altra nel caso in cui non sia noto alcun ordine di classificazione specifico per il profilo. Se dopo aver confrontato il valore di priorità due o più offerte di personalizzazione sono ancora legate, una viene scelta in modo casuale e utilizzata nella proposta di offerta. Il valore di questa proprietà deve essere un numero intero maggiore o uguale a 0.

Per regolare la priorità di base è possibile effettuare la seguente chiamata PATCH:

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '[
  {
    "op":   "replace",
    "path": "/_instance/xdm:rank/xdm:priority",
    "value": 0 
  }
]'
```

Consultate [Aggiornamento e patch delle istanze](#updating-and-patching-instances) per l’intera sintassi cURL. Il `schemaId` parametro deve essere `https://ns.adobe.com/experience/offer-management/personalized-offer`. Le offerte di fallback non dispongono di proprietà di classifica.

## Gestione delle regole di decisione

Le regole di ammissibilità contengono le condizioni che vengono valutate per determinare se una determinata opzione di decisione è idonea per un determinato profilo. L&#39;associazione di una regola a una o più opzioni di decisione implica che per questa opzione la regola deve essere valutata su true affinché l&#39;opzione sia considerata per l&#39;utente. La regola può contenere test sugli attributi del profilo, valutare le espressioni che comportano eventi di esperienza per questo profilo e includere dati contestuali passati alla richiesta di decisione. Ad esempio, una condizione può essere descritta come:

> &quot;Include le persone con stato di elite e che hanno volato su un volo tre volte nell&#39;ultimo 6 mese con numero di volo del volo corrente&quot;.

Le istanze vengono create con l&#39;identificatore dello schemahttps://ns.adobe.com/experience/offer-management/eligibility-rule. La `_instance` proprietà della chiamata di creazione o aggiornamento è simile alla seguente:

```json
{
  "xdm:name": "Eligible for a free flight upgrade",
  "xdm:condition": {
    "xdm:value": 
      "membership.status = \"elite\" 
       and (select e from xEvent 
            where e.type = \"flight\" 
              and e.flightnumber = @{{SCHEMA_ID}}.flightnumber
              and (e.timestamp occurs <= 6 months before now).count() > 3
           )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

Consultate [Aggiornamento e patch delle istanze](#updating-and-patching-instances) per l’intera sintassi cURL. Il `schemaId` parametro deve essere `https://ns.adobe.com/experience/offer-management/eligibility-rule`.

Il valore nella proprietà condition della regola contiene un&#39;espressione PQL. Ai dati contestuali viene fatto riferimento tramite l&#39;espressione speciale del percorso @{schemaID}.

Le regole si allineano naturalmente con i segmenti nella regola [!DNL Experience Platform] e spesso una regola riutilizza semplicemente l&#39;intento di un segmento testando la `segmentMembership` proprietà di un profilo. La `segmentMembership` proprietà contiene i risultati delle condizioni dei segmenti già valutate. Questo consente a un&#39;organizzazione di definire una volta i tipi di pubblico specifici del proprio dominio, denominarli e valutare le condizioni una volta sola.

## Gestione delle raccolte di offerte

### Creazione di tag e offerte di tag

Le offerte possono essere organizzate in raccolte in cui ogni raccolta definisce la condizione di filtro da applicare. Attualmente l&#39;espressione del filtro in una raccolta può avere uno dei due moduli:

1. Il `@id` parametro dell&#39;offerta deve corrispondere a uno in un elenco di identificatori affinché l&#39;offerta sia nella raccolta. Questo filtro è semplicemente un&#39;enumerazione degli URI delle offerte nella raccolta.
2. Un&#39;offerta può contenere un elenco di riferimenti di tag e il filtro della raccolta è costituito da un elenco di tag. L&#39;offerta è nella raccolta quando:\
   a. i tag di un filtro corrispondono a uno dei tag dell’offerta\
   b. tutti i tag del filtro corrispondono a uno dei tag dell’offerta

I tag sono semplici istanze a cui è possibile collegare le istanze delle offerte. Si tratta di istanze autonome con un nome per visualizzarle. Il nome deve essere univoco tra le istanze per facilitarne la visualizzazione nell’interfaccia utente.

Gli oggetti tag servono a stabilire una classificazione tra le opzioni decisionali (offerte). Un tag può essere collegato a molte offerte e un’offerta può contenere diversi riferimenti di tag. Una categoria di offerte è stabilita facendo riferimento a tutte le offerte correlate a un determinato insieme di istanze di tag.

Le istanze dei tag vengono create con l&#39;identificatore dello schema https://ns.adobe.com/experience/offer-management/tag. La `_instance` proprietà della chiamata di creazione o aggiornamento è simile alla seguente:

```json
{
  "xdm:name": "credit card"
} 
```

Consultate [Aggiornamento e patch delle istanze](#updating-and-patching-instances) per l’intera sintassi cURL. Il `schemaId` parametro deve essere `https://ns.adobe.com/experience/offer-management/tag`.


È possibile creare un&#39;istanza di offerta con l&#39;elenco di riferimenti di tag come:

```json
{
  "xdm:name": "ABC Bank Credit Card",
  "xdm:tags": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f2df943c428b6f7"
  ]
}
```

In alternativa, è possibile applicare una patch a un&#39;offerta per modificare l&#39;elenco dei tag:

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:tags/-",
    "value": "xcore:tag:f66f677ad3c0ba7" 
  }
]' 
```

Per entrambi i casi, consultate [Aggiornamento e patch delle istanze](#updating-and-patching-instances) per l’intera sintassi cURL. Il `schemaId` parametro deve essere `https://ns.adobe.com/experience/offer-management/personalized-offer`.

Tenere presente che la `xdm:tags` proprietà deve già esistere perché l&#39;operazione di aggiunta abbia esito positivo. Non esistono tag in un&#39;istanza. L&#39;operazione PATCH può prima aggiungere la proprietà array e quindi aggiungere un riferimento tag a tale array.

### Definire i filtri per le raccolte di offerte

Le istanze del filtro vengono create con l&#39;identificatore dello schema https://ns.adobe.com/experience/offer-management/offer-filter. La `_instance` proprietà della chiamata di creazione o aggiornamento potrebbe essere:

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "allTags",
  "ids": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f66f677ad3c0ba7"
  ]
}
```

Consultate [Aggiornamento e patch delle istanze](#updating-and-patching-instances) per l’intera sintassi cURL. Il `schemaId` parametro deve essere `https://ns.adobe.com/experience/offer-management/offer-filter`.

- **`xdm:filterType`** - Questa proprietà indica se il filtro è impostato utilizzando i tag o facendo riferimento direttamente alle offerte in base ai relativi ID. Quando il filtro è impostato per l’utilizzo di tag, il tipo di filtro può indicare ulteriormente se tutti i tag devono corrispondere ai tag di una particolare offerta o se uno dei tag specificati è sufficiente affinché l’offerta possa beneficiare del filtro. I valori validi di questa proprietà enum sono:
   - `offers`
   - `anyTags`
   - `allTags`
- **`ids`** - Una proprietà contiene un array di URI che fanno riferimento a istanze di offerte o tag, a seconda del valore di `xdm:filterType`. .

La seguente chiamata illustra l’aspetto della `_instance` proprietà per la chiamata di creazione o aggiornamento nel caso in cui alle offerte venga fatto riferimento direttamente:

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "offers",
  "ids": [
    "xcore:personalized-offer:f85e8298e53398d",
    "xcore:personalized-offer:f83a85c2bca3f1f",
    "xcore:personalized-offer:f9195bd412180b1",
    "xcore:personalized-offer:f67be37b6ad6ee6",
    "xcore:personalized-offer:f87bcc710ba6e93",
    "xcore:personalized-offer:f8855c30c0b20f8",
    "xcore:personalized-offer:f67bca7032d6ee5",
    "xcore:personalized-offer:f67bab756ed6ee4",
    "xcore:personalized-offer:f65281d506d6edf"
  ] 
} 
```

## Gestione delle attività

Un&#39;attività di offerta viene utilizzata per controllare il processo decisionale. Specifica il filtro di offerta applicato all&#39;inventario totale per restringere le offerte per argomento/categoria, la posizione per restringere l&#39;inventario a quelle offerte che rientrano nello spazio riservato e specifica un&#39;opzione di fallback qualora i vincoli combinati non qualifichino tutte le opzioni di personalizzazione (offerte) disponibili.

Le istanze dell&#39;attività vengono create con l&#39;identificatore`https://ns.adobe.com/experience/offer-management/offer-activity`dello schema. La `_instance` proprietà della chiamata di creazione o aggiornamento è simile alla seguente:

```json
{
  "xdm:name": "Call center IVR Personalization",
  "xdm:startDate": "2019-03-01T05:59:59.999Z",
  "xdm:endDate":   "2019-12-27T00:00:00.000Z",
  "xdm:status":    "live",
  "xdm:placement": "xcore:offer-placement:f652486959731ff",
  "xdm:filter":    "xcore:offer-filter:f6998eb62ed6f15",
  "xdm:fallback":  "xcore:fallback-offer:f6529b31b3c0ba6"
}
```

Consultate [Aggiornamento e patch delle istanze](#updating-and-patching-instances) per l’intera sintassi cURL. Il `schemaId` parametro deve essere `https://ns.adobe.com/experience/offer-management/offer-activity`.

- **`xdm:name`** - Questa proprietà obbligatoria contiene il nome dell&#39;attività. Il nome viene visualizzato in varie interfacce utente.
- **`xdm:status`** - Questa proprietà viene utilizzata per la gestione del ciclo di vita dell&#39;istanza. Il valore rappresenta uno stato del flusso di lavoro utilizzato per indicare se l&#39;attività è ancora in costruzione (valore = bozza), può essere generalmente considerata dal runtime (valore = live) o se non deve più essere utilizzata (valore = archiviata).
- **`xdm:placement`** - Una proprietà obbligatoria contenente un riferimento a un posizionamento di offerte applicato all&#39;inventario quando viene presa una decisione nel contesto di questa attività. Il valore è l’URI (`@id`) del posizionamento dell’offerta utilizzato.
- **`xdm:filter`** - Una proprietà obbligatoria contenente un riferimento a un filtro di offerta applicato all&#39;inventario quando viene presa una decisione nel contesto di questa attività. Il valore è l’URI (`@id`) del filtro offerte utilizzato.
- **`xdm:fallback`** - Una proprietà obbligatoria contenente un riferimento a un&#39;offerta di fallback. Un&#39;offerta di fallback viene utilizzata quando si decide per questa attività e non si qualifica nessuna delle offerte di personalizzazione. Il valore è l&#39;URI (`@id`) di un&#39;istanza di offerta di fallback.

### Gestione delle offerte di fallback

Prima che le istanze di attività possano essere create, deve esistere un&#39;offerta di fallback idonea per il posizionamento dell&#39;attività. Le istanze dell&#39;offerta di fallback vengono create con l&#39;identificatore`https://ns.adobe.com/experience/offer-management/fallback-offer`dello schema. La `_instance` proprietà della chiamata di creazione o aggiornamento contiene le stesse proprietà generali di un’offerta di personalizzazione, ma non può presentare altri vincoli.

```json
{
  "xdm:name": "Default for Kiosk Placements",
  "xdm:status": "approved",
  "xdm:representations": [
    {
      "xdm:placement": "xcore:offer-placement:e91afcf81bad130"
      "xdm:components": [
        {
          "dc:language": ["en" ],
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-html",
          "dc:format": "text/html"
        }
      ]
    }
  ]
}  
```

Consultate [Aggiornamento e patch delle istanze](#updating-and-patching-instances) per l’intera sintassi cURL. Il `schemaId` parametro deve essere `https://ns.adobe.com/experience/offer-management/fallback-offer`.

