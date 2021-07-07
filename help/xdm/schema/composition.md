---
keywords: Experience Platform;home;argomenti popolari;schema;schema;enum;mixin;gruppo di campi;gruppi di campi;mixins;tipo di dati;tipi di dati;tipi di dati;tipo di dati;identità primaria;profilo individuale XDM;campi XDM;tipo di dati enum;evento esperienza XDM;evento esperienza XDM ExperienceEvent;experienceEvent;XDM Experienceevent;XDM Experienceevenet;schema;classe;Classe classi;Classi;tipo di dati;tipo di dati;tipo di dati;schemi;schemi;mappa identità;mappa identità;mappa identità;progettazione schema;mappa;mappa;schema unione;schema unione
solution: Experience Platform
title: Nozioni di base sulla composizione dello schema
topic-legacy: overview
description: Questo documento fornisce un’introduzione agli schemi Experience Data Model (XDM) e ai blocchi predefiniti, ai principi e alle best practice per la composizione degli schemi da utilizzare in Adobe Experience Platform.
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '3726'
ht-degree: 0%

---

# Nozioni di base sulla composizione dello schema

Questo documento fornisce un’introduzione agli schemi [!DNL Experience Data Model] (XDM) e ai blocchi predefiniti, ai principi e alle best practice per la composizione degli schemi da utilizzare in Adobe Experience Platform. Per informazioni generali su XDM e su come viene utilizzato in [!DNL Platform], consulta la [Panoramica del sistema XDM](../home.md).

## Informazioni sugli schemi

Uno schema è un insieme di regole che rappresentano e convalidano la struttura e il formato dei dati. Ad alto livello, gli schemi forniscono una definizione astratta di un oggetto reale (ad esempio una persona) e delineano quali dati includere in ogni istanza dell’oggetto (ad esempio nome, cognome, compleanno e così via).

Oltre a descrivere la struttura dei dati, gli schemi applicano vincoli e aspettative ai dati in modo che possano essere convalidati mentre si spostano tra i sistemi. Queste definizioni standard consentono l’interpretazione coerente dei dati, indipendentemente dall’origine, e rimuovono la necessità di tradurre tra le applicazioni.

[!DNL Experience Platform] mantiene questa normalizzazione semantica utilizzando gli schemi. Gli schemi sono il modo standard per descrivere i dati in [!DNL Experience Platform], consentendo il riutilizzo di tutti i dati conformi agli schemi in un&#39;organizzazione senza conflitti o anche condivisi tra più organizzazioni.

Gli schemi XDM sono ideali per l’archiviazione di grandi quantità di dati complessi in un formato autonomo. Per ulteriori informazioni su come XDM esegue questa operazione, consulta le sezioni sugli [oggetti incorporati](#embedded) e [big data](#big-data) nell&#39;appendice di questo documento.

### Flussi di lavoro basati su schema in [!DNL Experience Platform]

La standardizzazione è un concetto chiave alla base di [!DNL Experience Platform]. XDM, guidato da un Adobe, è uno sforzo per standardizzare i dati sulla customer experience e definire schemi standard per la gestione della customer experience.

L&#39;infrastruttura su cui è generato [!DNL Experience Platform], nota come [!DNL XDM System], agevola i flussi di lavoro basati su schema e include i pattern di consumo del servizio [!DNL Schema Registry], [!DNL Schema Editor], i metadati dello schema e i modelli di consumo del servizio. Per ulteriori informazioni, consulta la [Panoramica del sistema XDM](../home.md) .

There are several key benefits to leveraging schemas in [!DNL Experience Platform]. First, schemas allow for better data governance and data minimization, which is especially important with privacy regulations. Second, building schemas with Adobe&#39;s standard components allows for out-of-the-box insights and use of AI/ML services with minimal customizations. Infine, gli schemi forniscono un’infrastruttura per la condivisione dei dati insights e un’orchestrazione efficiente.

## Pianificazione dello schema

Il primo passaggio nella creazione di uno schema consiste nel determinare il concetto, o oggetto reale, che si sta tentando di acquisire all&#39;interno dello schema. Una volta identificato il concetto che si sta tentando di descrivere, è possibile iniziare a pianificare lo schema pensando a elementi quali il tipo di dati, i campi di identità potenziali e l&#39;evoluzione dello schema in futuro.

### Data behaviors in [!DNL Experience Platform]

I dati destinati a essere utilizzati in [!DNL Experience Platform] sono raggruppati in due tipi di comportamento:

* **Dati** record: Fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.
* **Time series data**: Provides a snapshot of the system at the time an action was taken either directly or indirectly by a record subject.

Tutti gli schemi XDM descrivono i dati che possono essere classificati come record o serie temporali. Il comportamento dei dati di uno schema è definito dalla classe dello schema, che viene assegnata a uno schema quando viene creato per la prima volta. Le classi XDM sono descritte più avanti in questo documento.

Gli schemi di record e serie temporali contengono una mappa di identità (`xdm:identityMap`). Questo campo contiene la rappresentazione di identità di un oggetto, tratta dai campi contrassegnati come &quot;Identità&quot; come descritto nella sezione successiva.

### [!UICONTROL Identità] {#identity}

Gli schemi vengono utilizzati per acquisire i dati in [!DNL Experience Platform]. Questi dati possono essere utilizzati in più servizi per creare una singola visualizzazione unificata di una singola entità. Pertanto, è importante, quando pensi agli schemi, pensare alle identità dei clienti e a quali campi può essere utilizzato per identificare un soggetto indipendentemente da dove i dati potrebbero provenire.

Per facilitare questo processo, i campi chiave all’interno degli schemi possono essere contrassegnati come identità. Al momento dell’inserimento dei dati, i dati contenuti in tali campi vengono inseriti nel &quot;[!UICONTROL Grafico identità]&quot; per tale individuo. I dati del grafico sono quindi accessibili da [[!DNL Real-time Customer Profile]](../../profile/home.md) e da altri servizi [!DNL Experience Platform] per fornire una visualizzazione unita di ogni singolo cliente.

I campi comunemente contrassegnati come &quot;[!UICONTROL Identity]&quot; includono: indirizzo e-mail, numero di telefono, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=it), ID CRM o altri campi ID univoci. È inoltre necessario considerare eventuali identificatori univoci specifici dell&#39;organizzazione, in quanto potrebbero essere validi anche i campi &quot;[!UICONTROL Identity]&quot;.

È importante considerare le identità dei clienti durante la fase di pianificazione dello schema, in modo da garantire che i dati vengano raggruppati per creare il profilo più solido possibile. Per ulteriori informazioni su come le informazioni sull’identità possono aiutarti a fornire esperienze digitali ai tuoi clienti, consulta la panoramica su [Servizio Adobe Experience Platform Identity](../../identity-service/home.md) .

Esistono due modi per inviare i dati di identità a Platform:

1. Aggiunta di descrittori di identità ai singoli campi tramite l&#39; [interfaccia utente dell&#39;Editor di schema](../ui/fields/identity.md) o utilizzando l&#39; [API del Registro di sistema dello schema](../api/descriptors.md#create)
1. Utilizzo di un campo [`identityMap`](#identityMap)

#### `identityMap` {#identityMap}

`identityMap` è un campo di tipo mappa che descrive i vari valori di identità di un individuo, insieme ai relativi namespace associati. Questo campo può essere utilizzato per fornire informazioni di identità per gli schemi, anziché definire valori di identità all’interno della struttura dello schema stesso.

Il principale svantaggio dell&#39;utilizzo di `identityMap` è che le identità vengono incorporate nei dati e diventano meno visibili di conseguenza. Se acquisisci dati non elaborati, devi invece definire campi di identità individuali all’interno della struttura dello schema effettiva. Anche gli schemi che utilizzano `identityMap` non possono partecipare alle relazioni.

Tuttavia, le mappe di identità possono risultare particolarmente utili se si inseriscono dati provenienti da origini che memorizzano le identità insieme (ad esempio [!DNL Airship] o Adobe Audience Manager) o se è presente un numero variabile di identità per uno schema. Inoltre, le mappe di identità sono necessarie se utilizzi l&#39; [SDK di Adobe Experience Platform Mobile](https://aep-sdks.gitbook.io/docs/).

Un esempio di mappa di identità semplice è simile al seguente:

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": false
    }
  ],
  "ECID": [
    {
      "id": "87098882279810196101440938110216748923",
      "primary": false
    },
    {
      "id": "55019962992006103186215643814973128178",
      "primary": false
    }
  ],
  "loyaltyId": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": true
    }
  ]
}
```

Come illustrato nell’esempio precedente, ogni chiave dell’oggetto `identityMap` rappresenta uno spazio dei nomi di identità. Il valore di ciascuna chiave è una matrice di oggetti che rappresenta i valori di identità (`id`) per il rispettivo namespace. Consulta la documentazione [!DNL Identity Service] relativa a un [elenco di spazi dei nomi di identità standard](../../identity-service/troubleshooting-guide.md#standard-namespaces) riconosciuti dalle applicazioni Adobe.

>[!NOTE]
>
>Per ogni valore di identità è inoltre possibile specificare un valore booleano che indica se il valore è un&#39;identità primaria (`primary`). È necessario impostare le identità principali solo per gli schemi destinati a essere utilizzati in [!DNL Real-time Customer Profile]. Per ulteriori informazioni, consulta la sezione sugli [schemi di unione](#union) .

### Principi di evoluzione dello schema {#evolution}

Poiché la natura delle esperienze digitali continua ad evolversi, devono evolversi anche gli schemi utilizzati per rappresentarle. Uno schema ben progettato è quindi in grado di adattarsi ed evolvere in base alle esigenze, senza causare modifiche distruttive alle versioni precedenti dello schema.

Poiché il mantenimento della compatibilità con le versioni precedenti è fondamentale per l’evoluzione dello schema, [!DNL Experience Platform] applica un principio di controllo delle versioni puramente additivo. Questo principio assicura che qualsiasi revisione dello schema si traduca solo in aggiornamenti e modifiche non distruttivi. In altre parole, le **modifiche di interruzione non sono supportate.**

>[!NOTE]
>
>Se uno schema non è ancora stato utilizzato per acquisire i dati in [!DNL Experience Platform] e non è stato abilitato per l’utilizzo in Profilo cliente in tempo reale, puoi introdurre una modifica di interruzione a tale schema. Tuttavia, una volta che lo schema è stato utilizzato in [!DNL Platform], deve rispettare i criteri di controllo delle versioni aggiuntive.

La tabella seguente suddivide le modifiche supportate durante la modifica di schemi, gruppi di campi e tipi di dati:

| Modifiche supportate | Interruzione delle modifiche (non supportata) |
| --- | --- |
| <ul><li>Aggiunta di nuovi campi alla risorsa</li><li>Impostazione di un campo obbligatorio come facoltativo</li><li>Modifica del nome visualizzato e della descrizione della risorsa</li><li>Abilitazione dello schema per partecipare al profilo</li></ul> | <ul><li>Rimozione di campi definiti in precedenza</li><li>Introduzione di nuovi campi obbligatori</li><li>Ridenominazione o ridefinizione dei campi esistenti</li><li>Rimozione o limitazione dei valori di campo supportati in precedenza</li><li>Spostamento di campi esistenti in una posizione diversa nella struttura</li><li>Eliminazione dello schema</li><li>Disabilitazione dello schema dalla partecipazione al profilo</li></ul> |

### Schemi e acquisizione dati

Per acquisire i dati in [!DNL Experience Platform], è necessario creare prima un set di dati. I set di dati sono gli elementi costitutivi della trasformazione e del tracciamento dei dati per [[!DNL Catalog Service]](../../catalog/home.md) e generalmente rappresentano tabelle o file contenenti dati acquisiti. Tutti i set di dati si basano sugli schemi XDM esistenti, che forniscono vincoli per ciò che i dati acquisiti devono contenere e per come devono essere strutturati. Per ulteriori informazioni, consulta la panoramica su [Acquisizione dati Adobe Experience Platform](../../ingestion/home.md) .

## Blocco di uno schema

[!DNL Experience Platform] utilizza un approccio di composizione in cui i blocchi predefiniti standard vengono combinati per creare schemi. Questo approccio promuove la riutilizzabilità dei componenti esistenti e favorisce la standardizzazione in tutto il settore per supportare schemi e componenti dei fornitori in [!DNL Platform].

Schemas are composed using the following formula:

**Classe + Schema Field Group&amp;ast; = Schema XDM**

&amp;ast;Uno schema è composto da una classe e da zero o più gruppi di campi dello schema. Ciò significa che è possibile comporre uno schema di set di dati senza utilizzare affatto i gruppi di campi.

### Classe {#class}

La composizione di uno schema inizia con l’assegnazione di una classe. Le classi definiscono gli aspetti comportamentali dei dati che lo schema conterrà (record o serie temporali). In addition to this, classes describe the smallest number of common properties that all schemas based on that class would need to include and provide a way for multiple compatible datasets to be merged.

A schema&#39;s class determines which field groups will be eligible for use in that schema. This is discussed in more detail in the [next section](#field-group).

Adobe fornisce diverse classi XDM standard (&quot;core&quot;). Due di queste classi, [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent], sono necessarie per quasi tutti i processi della piattaforma a valle. Inoltre, puoi creare classi personalizzate per descrivere casi d’uso più specifici per la tua organizzazione. Le classi personalizzate sono definite da un&#39;organizzazione quando non sono disponibili classi principali definite da Adobi per descrivere un caso d&#39;uso univoco.

La schermata seguente illustra come le classi sono rappresentate nell’interfaccia utente di Platform. Poiché lo schema di esempio mostrato non contiene gruppi di campi, tutti i campi visualizzati sono forniti dalla classe dello schema ([!UICONTROL Profilo individuale XDM]).

![](../images/schema-composition/class.png)

Per l&#39;elenco più aggiornato delle classi XDM standard disponibili, fare riferimento al [repository XDM ufficiale](https://github.com/adobe/xdm/tree/master/components/classes). In alternativa, se preferisci visualizzare le risorse nell’interfaccia utente, puoi consultare la guida sull’ [esplorazione dei componenti XDM](../ui/explore.md) .

### Gruppo di campi {#field-group}

Un gruppo di campi è un componente riutilizzabile che definisce uno o più campi che implementano determinate funzioni quali dettagli personali, preferenze alberghiere o indirizzo. I gruppi di campi devono essere inclusi come parte di uno schema che implementa una classe compatibile.

I gruppi di campi definiscono le classi con cui sono compatibili in base al comportamento dei dati che rappresentano (record o serie temporali). Ciò significa che non tutti i gruppi di campi sono disponibili per l&#39;uso con tutte le classi.

[!DNL Experience Platform] include molti gruppi di campi di Adobe standard, consentendo al contempo ai fornitori di definire gruppi di campi per i propri utenti e ai singoli utenti di definire gruppi di campi per i propri concetti specifici.

Ad esempio, per acquisire dettagli quali &quot;[!UICONTROL Nome]&quot; e &quot;[!UICONTROL Indirizzo iniziale]&quot; per lo schema &quot;[!UICONTROL Membri fedeltà]&quot;, puoi utilizzare gruppi di campi standard che definiscono tali concetti comuni. Tuttavia, i concetti specifici dei casi di utilizzo meno comuni (come &quot;[!UICONTROL Livello di programma fedeltà]&quot;) spesso non dispongono di un gruppo di campi predefinito. In questo caso, è necessario definire un proprio gruppo di campi per acquisire queste informazioni.

Gli schemi sono composti da gruppi di campi &quot;zero o più&quot;, pertanto è possibile comporre uno schema valido senza utilizzare alcun gruppo di campi.

La schermata seguente illustra come i gruppi di campi sono rappresentati nell’interfaccia utente di Platform. Un singolo gruppo di campi ([!UICONTROL Dettagli demografici]) viene aggiunto a uno schema in questo esempio, che fornisce un raggruppamento di campi alla struttura dello schema.

![](../images/schema-composition/field-group.png)

Per l&#39;elenco più aggiornato dei gruppi di campi XDM standard disponibili, consulta l&#39; [archivio XDM ufficiale](https://github.com/adobe/xdm/tree/master/components/fieldgroups). In alternativa, se preferisci visualizzare le risorse nell’interfaccia utente, puoi consultare la guida sull’ [esplorazione dei componenti XDM](../ui/explore.md) .

### Tipo di dati {#data-type}

I tipi di dati vengono utilizzati come tipi di campi di riferimento in classi o schemi allo stesso modo dei campi letterali di base. La differenza principale consiste nel fatto che i tipi di dati possono definire più campi secondari. Analogamente a un gruppo di campi, un tipo di dati consente l’utilizzo coerente di una struttura a più campi, ma offre una flessibilità maggiore rispetto a un gruppo di campi, in quanto un tipo di dati può essere incluso in qualsiasi punto di uno schema, aggiungendolo come &quot;tipo di dati&quot; di un campo.

[!DNL Experience Platform] fornisce una serie di tipi di dati comuni come parte del  [!DNL Schema Registry] per supportare l&#39;uso di pattern standard per descrivere le strutture di dati comuni. Questo è spiegato più dettagliatamente nelle [!DNL Schema Registry] esercitazioni, dove diventerà più chiaro man mano che segui i passaggi per definire i tipi di dati.

La schermata seguente illustra come i tipi di dati sono rappresentati nell’interfaccia utente di Platform. Uno dei campi forniti dal gruppo di campi [!UICONTROL Dettagli demografici] utilizza il tipo di dati &quot;[!UICONTROL Nome persona]&quot;, come indicato dal testo che segue il carattere barra verticale (`|`) accanto al nome del campo. Questo particolare tipo di dati fornisce diversi sottocampi relativi al nome di una singola persona, un costrutto che può essere riutilizzato per altri campi in cui il nome di una persona deve essere catturato.

![](../images/schema-composition/data-type.png)

Per l&#39;elenco più aggiornato dei tipi di dati XDM standard disponibili, consulta l&#39; [archivio XDM ufficiale](https://github.com/adobe/xdm/tree/master/components/datatypes). In alternativa, se preferisci visualizzare le risorse nell’interfaccia utente, puoi consultare la guida sull’ [esplorazione dei componenti XDM](../ui/explore.md) .

### Campo

Un campo è il blocco predefinito più basilare di uno schema. I campi forniscono vincoli relativi al tipo di dati che possono contenere definendo un tipo di dati specifico. Questi tipi di dati di base definiscono un singolo campo, mentre i [tipi di dati](#data-type) menzionati in precedenza consentono di definire più campi secondari e di riutilizzare la stessa struttura a più campi in vari schemi. Pertanto, oltre a definire il &quot;tipo di dati&quot; di un campo come uno dei tipi di dati definiti nel Registro di sistema, [!DNL Experience Platform] supporta tipi scalari di base come:

* Stringa
* Intero
* Doppio
* Booleano
* Array
* Oggetto

>[!TIP]
>
>Per informazioni sui pro e i contro dell’utilizzo di campi modulo liberi rispetto ai campi di tipo oggetto, consultare l’ [appendice](#objects-v-freeform) .

Gli intervalli validi di questi tipi scalari possono essere ulteriormente vincolati a determinati pattern, formati, valori minimi/massimi o valori predefiniti. Utilizzando questi vincoli, è possibile rappresentare un’ampia gamma di tipi di campo più specifici, tra cui:

* Enum
* Lunga
* Breve
* Byte
* Data
* Data e ora
* Mappa

>[!NOTE]
>
>Il tipo di campo &quot;map&quot; consente la creazione di dati con coppia chiave-valore, inclusi più valori per una singola chiave. Le mappe possono essere definite solo a livello di sistema, il che significa che è possibile incontrare una mappa in uno schema definito dal settore o dal fornitore, ma non è disponibile per l’uso nei campi definiti dall’utente. La [Guida per gli sviluppatori API del Registro di sistema dello schema](../api/getting-started.md) contiene ulteriori informazioni sulla definizione dei tipi di campo.

Alcune operazioni di dati utilizzate dai servizi e dalle applicazioni a valle impongono vincoli su tipi di campi specifici. I servizi interessati includono, tra l&#39;altro:

* [[!DNL Real-time Customer Profile]](../../profile/home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!DNL Segmentation]](../../segmentation/home.md)
* [[!DNL Query Service]](../../query-service/home.md)
* [[!DNL Data Science Workspace]](../../data-science-workspace/home.md)

Prima di creare uno schema da utilizzare nei servizi a valle, controlla la documentazione appropriata per tali servizi al fine di comprendere meglio i requisiti e i vincoli dei campi per le operazioni relative ai dati a cui è destinato lo schema.

### Campi XDM

Oltre ai campi di base e alla possibilità di definire i propri tipi di dati, XDM fornisce un set standard di campi e tipi di dati che sono implicitamente compresi dai servizi [!DNL Experience Platform] e forniscono una maggiore coerenza quando utilizzato tra i componenti [!DNL Platform].

Questi campi, come &quot;Nome&quot; e &quot;Indirizzo e-mail&quot; contengono connotazioni aggiunte oltre i tipi di campi scalari di base, indicando a [!DNL Platform] che tutti i campi che condividono lo stesso tipo di dati XDM si comportano allo stesso modo. Tale comportamento può essere considerato coerente indipendentemente da dove provengono i dati o in cui vengono utilizzati i dati [!DNL Platform].

Per un elenco completo dei campi XDM disponibili, vedere il [dizionario dei campi XDM](field-dictionary.md) . Si consiglia di utilizzare campi e tipi di dati XDM laddove possibile per supportare coerenza e standardizzazione in [!DNL Experience Platform].

## Esempio di composizione

Gli schemi rappresentano il formato e la struttura dei dati che verranno acquisiti in [!DNL Platform] e vengono generati utilizzando un modello di composizione. Come accennato in precedenza, questi schemi sono composti da una classe e da zero o più gruppi di campi compatibili con tale classe.

Ad esempio, uno schema che descrive gli acquisti effettuati in un negozio al dettaglio potrebbe essere denominato &quot;[!UICONTROL Archivia transazioni]&quot;. Lo schema implementa la classe [!DNL XDM ExperienceEvent] combinata con il gruppo di campi [!UICONTROL Commerce] standard e un gruppo di campi [!UICONTROL Informazioni prodotto] definito dall&#39;utente.

Un altro schema che tiene traccia del traffico del sito web potrebbe essere denominato &quot;[!UICONTROL Visite web]&quot;. Implementa anche la classe [!DNL XDM ExperienceEvent], ma questa volta combina il gruppo di campi [!UICONTROL Web] standard.

Il diagramma seguente mostra questi schemi e i campi a cui contribuiscono ciascun gruppo di campi. Contiene inoltre due schemi basati sulla classe [!DNL XDM Individual Profile], incluso lo schema &quot;[!UICONTROL Membri fedeltà]&quot; menzionato in precedenza in questa guida.

![](../images/schema-composition/composition.png)

### Unione {#union}

Sebbene [!DNL Experience Platform] ti consenta di comporre schemi per casi d’uso particolari, ti consente anche di visualizzare un’&quot;unione&quot; di schemi per un tipo di classe specifico. Il diagramma precedente mostra due schemi basati sulla classe ExperienceEvent XDM e due schemi basati sulla classe [!DNL XDM Individual Profile] . L’unione, come illustrato di seguito, aggrega i campi di tutti gli schemi che condividono la stessa classe ([!DNL XDM ExperienceEvent] e [!DNL XDM Individual Profile], rispettivamente).

![](../images/schema-composition/union.png)

Attivando uno schema da utilizzare con [!DNL Real-time Customer Profile], verrà incluso nell&#39;unione per quel tipo di classe. [!DNL Profile] fornisce profili affidabili e centralizzati degli attributi del cliente e un account con marca temporale di ogni evento che il cliente ha avuto in qualsiasi sistema integrato con  [!DNL Platform]. [!DNL Profile] utilizza la visualizzazione unione per rappresentare questi dati e fornire una visualizzazione olistica di ogni singolo cliente.

Per ulteriori informazioni sulle operazioni con [!DNL Profile], consulta la [Panoramica sul profilo cliente in tempo reale](../../profile/home.md).

## Mappatura di file di dati su schemi XDM

Tutti i file di dati acquisiti in [!DNL Experience Platform] devono essere conformi alla struttura di uno schema XDM. Per ulteriori informazioni su come formattare i file di dati per conformarsi alle gerarchie XDM (inclusi i file di esempio), consulta il documento sulle [trasformazioni ETL di esempio](../../etl/transformations.md). Per informazioni generali sull’acquisizione di file di dati in [!DNL Experience Platform], consulta la [panoramica sull’acquisizione batch](../../ingestion/batch-ingestion/overview.md).

## Schemi per segmenti esterni

Se porti segmenti da sistemi esterni in Platform, devi utilizzare i seguenti componenti per acquisirli negli schemi:

* [[!UICONTROL Classe ] di definizione del segmento](../classes/segment-definition.md): Utilizza questa classe standard per acquisire gli attributi chiave di una definizione di segmento esterna.
* [[!UICONTROL Gruppo di campi ] dettagli](../field-groups/profile/segmentation.md) appartenenza al segmento: Aggiungi questo gruppo di campi al tuo  [!UICONTROL schema ] Profileschema individuale XDM per associare i profili dei clienti a segmenti specifici.

## Passaggi successivi

Ora che conosci le nozioni di base della composizione dello schema, sei pronto per iniziare a esplorare e creare schemi utilizzando il [!DNL Schema Registry].

Per esaminare la struttura delle due classi XDM principali e dei relativi gruppi di campi compatibili di uso comune, consulta la seguente documentazione di riferimento:

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

L’ [!DNL Schema Registry] viene utilizzato per accedere a [!DNL Schema Library] all’interno di Adobe Experience Platform e fornisce un’interfaccia utente e un’API RESTful da cui sono accessibili tutte le risorse della libreria disponibili. Il [!DNL Schema Library] contiene le risorse di settore definite da Adobe, le risorse del fornitore definite dai partner [!DNL Experience Platform] e le classi, i gruppi di campi, i tipi di dati e gli schemi che sono stati composti da membri dell&#39;organizzazione.

Per iniziare a comporre lo schema utilizzando l&#39;interfaccia utente, segui insieme all&#39; [tutorial Editor di schema](../tutorials/create-schema-ui.md) per creare lo schema &quot;Membri fedeltà&quot; menzionato in questo documento.

Per iniziare a utilizzare l&#39;API [!DNL Schema Registry], leggi la [Guida per gli sviluppatori dell&#39;API del Registro di sistema ](../api/getting-started.md). Dopo aver letto la guida per gli sviluppatori, segui i passaggi descritti nell&#39;esercitazione su [creazione di uno schema utilizzando l&#39;API del Registro di sistema dello schema](../tutorials/create-schema-api.md).

## Appendice

Le sezioni seguenti contengono informazioni aggiuntive relative ai principi di composizione dello schema.

### Tabelle relazionali e oggetti incorporati {#embedded}

Quando si lavora con database relazionali, le best practice prevedono la normalizzazione dei dati o la suddivisione di un’entità in parti discrete che vengono quindi visualizzate su più tabelle. Per leggere i dati nel loro insieme o aggiornare l&#39;entità, è necessario eseguire operazioni di lettura e scrittura in più tabelle singole utilizzando JOIN.

Utilizzando gli oggetti incorporati, gli schemi XDM possono rappresentare direttamente dati complessi e archiviarli in documenti indipendenti con struttura gerarchica. Uno dei principali vantaggi di questa struttura è che consente di eseguire query sui dati senza dover ricostruire l’entità tramite join costosi a più tabelle denormalizzate. Non vi sono restrizioni difficili al numero di livelli possibili nella gerarchia dello schema.

### Schemi e big data {#big-data}

I sistemi digitali moderni generano una grande quantità di segnali comportamentali (dati delle transazioni, registri web, Internet di cose, visualizzazione e così via). Questi big data offrono straordinarie opportunità di ottimizzazione delle esperienze, ma sono difficili da utilizzare a causa della scala e della varietà dei dati. Al fine di trarre valore dai dati, la struttura, il formato e le definizioni devono essere standardizzati in modo da poter essere elaborati in modo coerente ed efficiente.

Gli schemi risolvono questo problema consentendo l&#39;integrazione dei dati da più fonti, standardizzati attraverso strutture e definizioni comuni e condivisi tra le soluzioni. Ciò consente ai processi e ai servizi successivi di rispondere a qualsiasi tipo di domanda posta sui dati, allontanandosi dall’approccio tradizionale alla modellazione dei dati, in cui tutte le domande che verranno poste sui dati sono note in anticipo e i dati sono modellati per conformarsi a tali aspettative.

### Oggetti e campi a forma libera {#objects-v-freeform}

Durante la progettazione degli schemi, è necessario tenere in considerazione alcuni fattori chiave nella scelta degli oggetti rispetto ai campi a forma libera:

| Oggetti | Campi in formato libero |
| --- | --- |
| Aumenta la nidificazione | Minore o nessuna nidificazione |
| Crea raggruppamenti di campi logici | I campi sono posizionati in posizioni ad hoc |

{style=&quot;table-layout:auto&quot;}

#### Oggetti

Di seguito sono elencati i pro e i contro dell’utilizzo degli oggetti nei campi a forma libera.

**Pro**:

* Gli oggetti vengono utilizzati al meglio quando si desidera creare un raggruppamento logico di determinati campi.
* Gli oggetti organizzano lo schema in modo più strutturato.
* Gli oggetti contribuiscono indirettamente alla creazione di una buona struttura di menu nell’interfaccia utente del Generatore di segmenti. I campi raggruppati all’interno dello schema si riflettono direttamente nella struttura delle cartelle fornita nell’interfaccia utente del Generatore di segmenti.

**Cons**:

* I campi diventano più nidificati.
* Quando si utilizza [Adobe Experience Platform Query Service](../../query-service/home.md), è necessario fornire stringhe di riferimento più lunghe ai campi di query nidificati negli oggetti.

#### Campi in formato libero

Di seguito sono elencati i pro e i contro dell’uso dei campi modulo libero sugli oggetti.

**Pro**:

* I campi in formato libero vengono creati direttamente sotto l&#39;oggetto principale dello schema (`_tenantId`), aumentando la visibilità.
* Le stringhe di riferimento per i campi a forma libera tendono a essere più corte quando si utilizza Query Service.

**Cons**:

* La posizione dei campi in formato libero all’interno dello schema è ad hoc, il che significa che vengono visualizzati in ordine alfabetico all’interno dell’Editor di schema. In questo modo gli schemi possono essere meno strutturati e campi modulo gratuiti simili possono risultare molto separati a seconda dei loro nomi.
