---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Operazioni con il runtime di Decisioning Service tramite API
topic: tutorial
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '1985'
ht-degree: 0%

---


# Operazioni con il runtime di Decisioning Service tramite API

Questo documento fornisce un&#39;esercitazione per lavorare con i servizi di runtime sull&#39; [!DNL Decisioning Service] utilizzo  API di Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei [!DNL Experience Platform] servizi coinvolti nelle decisioni e nella determinazione della migliore offerta da presentare durante le esperienze dei clienti. Prima di iniziare questa esercitazione, consulta la documentazione per i seguenti elementi:

- [!DNL Decisioning Service](./../home.md): Fornisce il framework per l&#39;aggiunta e la rimozione di offerte e la creazione di algoritmi per la scelta dei migliori da presentare durante l&#39;esperienza del cliente.
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Framework standard con cui Platform organizza i dati sull&#39;esperienza dei clienti.
- [!DNL Profile Query Language (PQL)](../../segmentation/pql/overview.md): PQL viene utilizzato per definire regole e filtri.
- [Gestione di oggetti e regole di disattivazione tramite API](./entities.md): Prima di utilizzare il runtime di Decisioning Services, sarà necessario configurare le entità correlate.

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

>[!NOTE] Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione [sulla panoramica della](../../tutorials/authentication.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

Necessario anche per le richieste di runtime:

- x-request-id: `{UUID}`

>[!NOTE] `UUID` è una stringa in formato UUID che è univoca a livello globale e non deve essere riutilizzata per chiamate API diverse

[!DNL Decisioning Service] è controllato da una serie di oggetti business correlati tra loro. Tutti gli oggetti aziendali sono memorizzati nell&#39;archivio oggetti [!DNL Platform’s] aziendali, XDM Core Object Repository. Una caratteristica chiave di questo repository è che le API sono ortogonali al tipo di oggetto business. Invece di utilizzare un&#39;API POST, GET, PUT, PATCH o DELETE che indica il tipo di risorsa nel suo endpoint API, ci sono solo 6 endpoint generici, ma accettano o restituiscono un parametro che indica il tipo di oggetto quando è necessario tale parametro. Lo schema deve essere registrato con l&#39;archivio, ma oltre a questo, l&#39;archivio è utilizzabile per un set di tipi di oggetto aperto.

I percorsi endpoint per tutte le API dell&#39;archivio oggetti di base XDM iniziano con `https://platform.adobe.io/data/core/ode/`.

Il primo elemento di percorso successivo è l&#39;endpoint `containerId`. Questo identificatore viene ottenuto tramite l&#39;endpoint principale dell&#39;archivio oggetti di base XDM `GET https://platform.adobe.io/data/core/xcore/`.

## Compilazione di modelli decisionali

L&#39;attivazione delle entità business logic avviene automaticamente e in modo continuo. Non appena viene salvata una nuova opzione nella directory archivio e contrassegnata come &quot;approvata&quot;, sarà possibile includere la serie di opzioni disponibili. Non appena una regola di decisione viene aggiornata, il ruleset verrà riassemblato e preparato per l&#39;esecuzione in fase di esecuzione. In questa fase di attivazione automatica, verranno valutati tutti i vincoli definiti dalla logica aziendale che non dipendono dal contesto di runtime. I risultati di questo passaggio di attivazione vengono inviati a una cache in cui sono disponibili per il [!DNL Decisioning Service] runtime.

### Effetti di posizionamenti, filtri e stati del ciclo di vita

Le offerte vengono create in modo continuo, lo stato del ciclo di vita subisce modifiche o possono ottenere nuove rappresentazioni dei contenuti. Il filtro delle offerte di un&#39;attività può cambiare, corrispondere o filtrare le offerte i cui set di tag sono stati aggiornati. Questo processo può essere abbastanza coinvolto e le applicazioni e i servizi devono sapere quale sarà l&#39;insieme di candidati di un&#39;attività risultante. Il runtime di decisione fornisce un&#39;API activity-to-offer che filtra offerte non approvate, non corrispondono al filtro dell&#39;offerta o non hanno una rappresentazione per il posizionamento a cui fa riferimento l&#39;attività.

**Richiesta**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/offers?activityId={ACTIVITY_URI}' \
  -H 'Accept: application/vnd.adobe.xdm+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

**Risposta**

Il parametro `activityId` può essere ripetuto nell&#39;URL e fino a 30 riferimenti di attività diversi possono essere forniti in una richiesta. La risposta sarà utile per individuare eventuali circostanze impreviste risultanti dalla configurazione e avrà l&#39;aspetto seguente:

```json
{
  "xdm:activityOffers": [
    {
      "xdm:offerActivity": {
        "@id": "{ACTIVITY_URI}",
        "_links": {
          "self": {
            "href": "{repository_endpoint}/{CONTAINER_ID}/instances/{ACTIVITY_INSTANCE_ID}"
          }
        },
        "repo:etag": "1"
      },
      "xdm:offers": [
        {
          "@id": "{OFFER_URI_1}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_1}"
            }
          },
          "repo:etag": "15"
        },
        {
          "@id": "{OFFER_URI_2}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_2}"
            }
          },
          "repo:etag": "5"
        }
      ],
      "xdm:fallbackOffer": {
        "@id": "{FALLBACK_URI}",
        "_links": {
          "self": {
            "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{FALLBACK_INSTANCE_ID}"
          }
        },
        "repo:etag": "2"
      }
    }
  ]
}
```

Si verifica un piccolo ritardo di alcuni secondi tra il momento in cui gli oggetti sono stati aggiornati e il momento in cui la risposta API riflette la mappatura attività-offerte. La revisione di ciascun oggetto viene fornita nella risposta in modo che i client possano verificare se è presente un aggiornamento degli oggetti che non è stato riflesso.

### API di diagnostica e risoluzione dei problemi

Le attività, le offerte e le regole di idoneità sono compilate in un formato interno (catalogo delle offerte in fase di esecuzione) utilizzato dal runtime del servizio decisionale. La compilazione potrebbe rilevare errori che non sono stati rilevati dai controlli eseguiti al momento della memorizzazione degli oggetti e i collegamenti sono stati stabiliti nel repository degli oggetti core XDM.

Viene fornita un&#39;API di diagnostica per ottenere eventuali errori di compilazione che si sono verificati in quel passaggio e, nel caso in cui non ci siano errori per ottenere informazioni su quando le regole e le attività sono state ricompilate per l&#39;ultima volta.

**Richiesta**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/diagnostics \
  -H 'Accept: application/vnd.adobe.xdm+json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

L&#39;unico parametro per questa chiamata API è `containerId`. I risultati sono tutti gli aggiornamenti di tutti i client che hanno modificato le regole decisionali, le offerte, le attività o i filtri delle offerte in quel contenitore. Si verifica un piccolo ritardo di alcuni secondi tra il momento in cui gli oggetti sono stati aggiornati e il momento in cui la compilazione termina. La marca temporale dell&#39;ultimo aggiornamento e gli eventuali errori vengono restituiti nella risposta alla chiamata di diagnostica.

**Risposta**

```json
{
  "xdm:operations": {
    "xdm:offerCatalogUpdate": {
      "xdm:date": "2019-06-19T23:28:44.855Z",
      "xdm:errors": []
    },
    "xdm:activitiesUpdate": {
      "xdm:date": "2019-06-19T23:28:40.114Z",
      "xdm:errors": []
    }
  }
}
```

## Chiamate REST API per eseguire le decisioni

L&#39;API REST è una delle route per le applicazioni in esecuzione [!DNL Platform] per ottenere la migliore esperienza successiva in base a regole, modelli e vincoli impostati dall&#39;organizzazione per i propri utenti. Le applicazioni inviano una delle identità del profilo (ID profilo e namespace identità), [!DNL Decisioning Service] cercheranno il profilo e le informazioni verranno utilizzate per applicare la logica aziendale. I dati contestuali aggiuntivi possono essere passati alla richiesta e, se specificati nelle regole aziendali, saranno inclusi nei dati per prendere la decisione.

Le applicazioni possono ottenere prestazioni migliori richiedendo una decisione fino a 30 attività alla volta. Gli URI delle attività vengono passati nella stessa richiesta. REST API è sincrona e restituirà le opzioni proposte per tutte queste attività o l&#39;opzione di fallback se nessuna opzione di personalizzazione soddisfa i vincoli.

È possibile che due diverse attività abbiano la stessa opzione del loro &quot;meglio&quot;. Per evitare di ripetere un&#39;esperienza composta, per impostazione predefinita, [!DNL Decisioning Service] si arbitra tra le attività a cui si fa riferimento nella stessa richiesta. Arbitrazione significa che per ciascuna attività le loro opzioni top-N sono prese in considerazione, ma nessuna opzione sarà proposta più di una volta in tali attività. Se due attività hanno la stessa opzione in classifica superiore, una di esse sarà selezionata per utilizzare la seconda scelta o la terza migliore e così via. Tali regole di deduplicazione tentano di evitare che una qualsiasi delle attività debba utilizzare la propria opzione di fallback.

La richiesta di decisione contiene gli argomenti relativi al corpo di una richiesta POST. Il corpo è formattato come valore di `Content-Type` intestazione JSON `application/vnd.adobe.xdm+json; schema="{REQUEST_SCHEMA_AND_VERSION}"`

Al momento, lo schema e la versione della richiesta sono supportati `https://ns.adobe.com/experience/offer-management/decision-request;version=0.9`. In futuro verranno forniti ulteriori schemi di richiesta o versioni.

**Richiesta**

```shell
curl -X POST {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/decisions \
  -H 'Accept: application/json, application/problem+json \
  -H '
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '{
  "xdm:dryRun": {DRY_RUN_TRUE_FALSE},
  "xdm:validateContextData": {VALIDATE_CONTEXT_DATA_TRUE_FALSE},

  "xdm:offerActivities":[
    {
      "xdm:offerActivity": "{ACTIVITY_URI_1}"
    },
  ],
  "xdm:identityMap":{
    "{PROFILE_ID_NAMESPACE_CODE}":[
      {
        "xdm:id":"{PROFILE_ID}"
      }
    ]
  },
  "xdm:profileModel":"{PROFILE_MODEL}",
  "xdm:contextData": [
    {
      "@type": "{CONTEXT_DATASSCHEMA_ID}"
      "xdm:data": { JSON PROPERTIES OF CONTEXT ENTITY }
    }
  ] ,
  "xdm:allowDuplicatePropositions": {
    "xdm:acrossActivities": {DUPLICATE_OFFER_IDS_OF_TRUE_FALSE},
  }
}’
```

- **`xdm:dryRun`** - Quando il valore di questa proprietà facoltativa è impostato su true, la richiesta di decisione obbedisce ai vincoli di limite massimo ma non li disegna, è previsto che il chiamante non intenda mai presentare la proposta al profilo. La proposta non [!DNL Decisioning Service] verrà registrata come evento di decisione XDM ufficiale e non verrà visualizzata nei set di dati di reporting. Il valore predefinito di questa proprietà è false e quando la proprietà viene omessa, la decisione non viene considerata un&#39;esecuzione di test e deve quindi essere presentata all&#39;utente finale.
- **`xdm:validateContextData`** - Questa proprietà opzionale attiva o disattiva la convalida dei dati contestuali. Se la convalida è attivata, per ogni elemento di dati contestuali fornito lo schema (basato sul `@type` campo) viene recuperato dal Registro di sistema XDM e l&#39; `xdm:data` oggetto viene convalidato.

La richiesta per questo schema contiene un array di URI che fanno riferimento alle attività dell&#39;offerta, un&#39;identità di profilo e un array di elementi di dati contestuali:

- **`xdm:offerActivities`** - Questa proprietà obbligatoria è un array di oggetti in cui ogni elemento contiene dati sull&#39;attività dell&#39;offerta. L&#39;attività dell&#39;offerta ha le seguenti proprietà:
   - **`xdm:offerActivity`** - L&#39;identificatore univoco (URI) dell&#39;attività. Questo è il valore della `@id` proprietà dell&#39;attività dell&#39;offerta.
- **`xdm:identityMap`** - Una proprietà obbligatoria contenente un oggetto JSON conforme allo schema XDM `https://ns.adobe.com/xdm/context/identitymap`. La proprietà definisce una mappa in cui la chiave è un codice dello spazio dei nomi dell&#39;identità e il valore è un elenco di identificatori dell&#39;utente finale nello spazio dei nomi specificato. Se m.
- **`xdm:contextData`** - Una proprietà opzionale che contiene elementi descritti da un riferimento al relativo schema. Ciascun elemento dei dati contestuali nell&#39;array deve avere le seguenti proprietà:
   - **`@type`** - Una proprietà obbligatoria che fa riferimento allo schema XDM dell&#39;oggetto in questo elemento.
   - **`xdm:data`** - Una proprietà obbligatoria contenente le proprietà dell&#39;oggetto in base allo schema XDM fornito nella `@type` proprietà.

## Dati contestuali dinamici nelle richieste di decisione

La sezione precedente mostra come gli oggetti XDM possono essere passati a una richiesta di decisione. Esempio di array di oggetti contestuali:

```json
"xdm:contextData": [
  {
    "@type":" https://ns.adobe.com/{TENANT_ID_OF_ORG}/schemas/{NUMERIC_SCHEMA_ID};version=1",
    "xdm:data":{ 
      "{TENANT_ID_OF_ORG}": {
        "productDetails":{ 
          "xdm:gender":      "unisex",
          "xdm:fabrication": "leather",
          "xdm:category":    "wallets",
        }
      }
    }
  }
]
```

Lo schema deve essere stato costruito dall&#39;organizzazione. Per informazioni sulla creazione di schemi, fare riferimento all&#39;esercitazione [Editor](../../xdm/tutorials/create-schema-ui.md)schema. Lo schema sarà in uno spazio dei nomi `https://ns.adobe.com/{TENANT_ID}/schemas`.

La guida [per gli sviluppatori API del Registro di](../../xdm/tutorials/create-schema-api.md) schema spiega come è possibile accedere agli schemi a livello di programmazione e come uno sviluppatore ottiene l’ID tenant e l’identificatore numerico dello schema. Il numero di versione è obbligatorio ed è fornito anche dalle API del Registro di sistema dello schema.

Uno schema definito da un&#39;organizzazione avrà in genere una proprietà principale denominata `_{TENANT_ID}`, denominata anche stringa dello spazio dei nomi del tenant.
Le proprietà utilizzate da un componente schema globale, ad esempio _`https://ns.adobe.com/xdm/context/product` , hanno il prefisso namespace `xdm:`. In questo caso, la proprietà definita dall&#39;organizzazione `productDetails` è stata costruita con tale tipo di dati. Mentre le proprietà tenant sono nidificate in una proprietà denominata dopo lo spazio nomi tenant, i tipi di dati disponibili a livello globale utilizzano il prefisso riservato `xdm:` per evitare conflitti tra i nomi delle proprietà.

Più oggetti dati possono essere elencati nella `xdm:contextData` proprietà. Ciascun oggetto deve identificarne il tipo tramite la `@type` proprietà.
I valori degli oggetti dati contestuali sono disponibili per essere utilizzati nelle espressioni PQL, ad esempio nella condizione di una regola di idoneità. L&#39;oggetto dati contestuali deve essere indirizzato tramite l&#39;espressione di riferimento percorso speciale `@{schemaId}`. Le espressioni che seguono questa espressione di riferimento sono espressioni di percorso regolari che accedono alle proprietà dell&#39;oggetto dati:

```json
{
  "xdm:name": "Eligible for a free gender-specific item of interest",
  "xdm:condition": {
    "xdm:value":
      "gender in (\"female\",\"non-specific\")  
       and (
         select p from
           @{https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}._{TENANT_ID}
         select e from xEvent 
            where e.type = \"productSearch\" 
              and e.category = p.category 
              and p.gender in (\"female\",\"unisex\")
       )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

Nell&#39;esempio precedente, la variabile `p` viene iterata sull&#39;array di oggetti contrassegnati con `@type` = `https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}`.

La sintassi PQL non utilizza i prefissi nei nomi delle proprietà. Per impostazione predefinita, alle proprietà globali viene fatto riferimento semplicemente senza il `xdm:` prefisso. Le proprietà definite dall&#39;organizzazione sono nidificate all&#39;interno di una proprietà **aggiuntiva** denominata dopo lo spazio dei nomi del tenant (nell&#39;esempio indicato dalla variabile `{TENANT_ID}`). Per poter fare riferimento direttamente alle proprietà definite dall&#39;utente, la variabile `p` è associata al risultato del percorso che fa riferimento alla proprietà di nidificazione aggiuntiva.

## Utilizzo dei record di profilo

Tutti i record per le entità evento profilo ed esperienza sono già gestiti nell&#39;archivio profili. Passando una o più identità di profilo alla richiesta, il profilo per tali identità sarà identificato e cercato dal negozio. I dati vengono quindi automaticamente resi disponibili alle regole decisionali e ai modelli valutati dalla strategia decisionale.

Per recuperare i record di profilo ed esperienza, viene applicato il criterio di unione predefinito.
Si noti che dopo aver caricato i record del profilo nel [!DNL Platform] database si verifica un leggero ritardo fino a quando i record del profilo non possono essere cercati. Lo stesso vale per l&#39;acquisizione di record di profilo ed esperienza tramite le API di streaming, solo dopo pochi secondi i dati saranno disponibili per la valutazione delle regole decisionali che valutano i dati di profilo ed esperienza dell&#39;evento.