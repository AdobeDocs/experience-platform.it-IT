---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Nozioni di base sulla composizione dello schema
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '2761'
ht-degree: 0%

---


# Nozioni di base sulla composizione dello schema

Questo documento fornisce un&#39;introduzione agli schemi del modello dati esperienza (XDM) e ai blocchi costitutivi, ai principi e alle procedure ottimali per la composizione degli schemi da utilizzare in  Adobe Experience Platform. Per informazioni generali su XDM e come viene utilizzato in Platform, consultate la panoramica [di sistema](../home.md)XDM.

## Informazioni sugli schemi

Uno schema è un insieme di regole che rappresentano e convalidano la struttura e il formato dei dati. A un livello elevato, gli schemi forniscono una definizione astratta di un oggetto reale (ad esempio una persona) e delineano quali dati includere in ciascuna istanza di tale oggetto (ad esempio nome, cognome, compleanno e così via).

Oltre a descrivere la struttura dei dati, gli schemi applicano vincoli e aspettative ai dati in modo che possano essere convalidati man mano che si spostano tra i sistemi. Queste definizioni standard consentono l&#39;interpretazione coerente dei dati, indipendentemente dall&#39;origine, e rimuovono la necessità di una traduzione tra le applicazioni.

 Experience Platform mantiene questa normalizzazione semantica attraverso gli schemi. Gli schemi sono il modo standard per descrivere i dati in  Experience Platform, consentendo a tutti i dati conformi agli schemi di essere riutilizzabili senza conflitti all&#39;interno di un&#39;organizzazione e persino di essere condivisibili tra più organizzazioni.

### Tabelle relazionali e oggetti incorporati

Quando si utilizzano i database relazionali, le best practice prevedono la normalizzazione dei dati o la suddivisione di un&#39;entità in parti distinte che vengono visualizzate in più tabelle. Per leggere i dati nel loro insieme o aggiornare l&#39;entità, le operazioni di lettura e scrittura devono essere eseguite in più singole tabelle utilizzando JOIN.

Utilizzando gli oggetti incorporati, gli schemi XDM possono rappresentare direttamente dati complessi e archiviarli in documenti indipendenti con struttura gerarchica. Uno dei principali vantaggi di questa struttura è che consente di eseguire query sui dati senza dover ricostruire l&#39;entità tramite join costosi a più tabelle denormalizzate.

### Schemi e grandi dati

I sistemi digitali moderni generano una vasta quantità di segnali comportamentali (dati sulle transazioni, registri web, Internet di cose, visualizzazione e così via). Questi grandi dati offrono straordinarie opportunità di ottimizzare le esperienze, ma sono difficili da utilizzare a causa della scala e della varietà dei dati. Al fine di ottenere valore dai dati, la struttura, il formato e le definizioni devono essere standardizzati in modo che possano essere elaborati in modo coerente ed efficiente.

Gli schemi risolvono questo problema consentendo l&#39;integrazione dei dati da più fonti, standardizzati attraverso strutture e definizioni comuni e condivisi tra soluzioni. Questo consente ai processi e ai servizi successivi di rispondere a qualsiasi tipo di domanda posta sui dati, allontanandosi dall&#39;approccio tradizionale alla modellazione dei dati, dove tutte le domande che verranno poste sui dati sono note in anticipo e i dati sono modellati per conformarsi a tali aspettative.

### Flussi di lavoro basati su schema in  Experience Platform

La standardizzazione è un concetto chiave dietro  Experience Platform. XDM, guidato da Adobe, è uno sforzo per standardizzare i dati sull&#39;esperienza cliente e definire schemi standard per la gestione dell&#39;esperienza cliente.

L&#39;infrastruttura su cui  è stato creato Experience Platform, nota come XDM System, semplifica i flussi di lavoro basati su schema e include il Registro di sistema dello schema, l&#39;Editor di schema, i metadati dello schema e i pattern di consumo del servizio. See the [XDM System overview](../home.md) for more information.

## Pianificazione dello schema

Il primo passaggio nella creazione di uno schema consiste nel determinare il concetto, o oggetto reale, che si sta tentando di acquisire all&#39;interno dello schema. Una volta identificato il concetto che si sta cercando di descrivere, è possibile iniziare a pianificare lo schema pensando a cose come il tipo di dati, campi di identità potenziali e come lo schema potrebbe evolvere in futuro.

### Comportamenti dei dati in  Experience Platform

I dati da utilizzare in  Experience Platform sono raggruppati in due tipi di comportamento:

* **Record data**: Fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.
* **Dati** serie temporali: Fornisce un&#39;istantanea del sistema al momento in cui un&#39;azione è stata eseguita direttamente o indirettamente da un soggetto del record.

Tutti gli schemi XDM descrivono i dati che possono essere classificati come record o serie temporali. Il comportamento dei dati di uno schema è definito dalla **classe** dello schema, che viene assegnata a uno schema al momento della sua creazione. Le classi XDM sono descritte in dettaglio più avanti in questo documento.

Gli schemi di record e di serie temporali contengono una mappa di identità (`xdm:identityMap`). Questo campo contiene la rappresentazione di identità di un oggetto, ricavata dai campi contrassegnati come &quot;Identità&quot; come descritto nella sezione successiva.

### Identità

Gli schemi vengono utilizzati per assimilare i dati in  Experience Platform. Questi dati possono essere utilizzati tra più servizi per creare una singola vista unificata di una singola entità. Pertanto, è importante, quando si pensa agli schemi, pensare a &quot;Identità&quot; e a quali campi è possibile utilizzare per identificare un oggetto, indipendentemente da dove i dati provengano.

Per facilitare questo processo, i campi chiave possono essere contrassegnati come &quot;Identità&quot;. Al momento dell&#39;inserimento dei dati, i dati contenuti in tali campi saranno inseriti nel &quot;Grafico identità&quot; per l&#39;individuo in questione. I dati del grafico sono quindi accessibili dal profilo [cliente in tempo](../../profile/home.md) reale e da altri servizi Experience Platform  per fornire una visualizzazione unica di ciascun cliente.

I campi generalmente contrassegnati come &quot;Identità&quot; includono: indirizzo e-mail, numero di telefono, [ID Experience Cloud (ECID)](https://docs.adobe.com/content/help/it-IT/id-service/using/home.html), ID CRM o altri campi ID univoci. È inoltre necessario considerare eventuali identificatori univoci specifici della propria organizzazione, in quanto possono essere buoni anche i campi &quot;Identità&quot;.

È importante considerare le identità dei clienti durante la fase di pianificazione dello schema, in modo da garantire che i dati vengano uniti per creare il profilo più affidabile possibile. Consulta la panoramica [del servizio](../../identity-service/home.md) identità per scoprire come le informazioni sull&#39;identità possono aiutarti a fornire esperienze digitali ai tuoi clienti.

### Principi di evoluzione dello schema {#evolution}

Mentre la natura delle esperienze digitali continua ad evolversi, devono evolversi anche gli schemi utilizzati per rappresentarle. Uno schema ben progettato è quindi in grado di adattarsi ed evolversi in base alle esigenze, senza causare modifiche distruttive alle versioni precedenti dello schema.

Poiché per l&#39;evoluzione dello schema è fondamentale mantenere la compatibilità con le versioni precedenti,  Experience Platform applica un principio di controllo delle versioni puramente additivo, in modo da garantire che qualsiasi revisione dello schema produca solo aggiornamenti e modifiche non distruttivi. In altre parole, le modifiche **di interruzione non sono supportate.**

| Modifiche supportate | Interruzione delle modifiche (non supportata) |
|------------------------------------|---------------------------------|
| <ul><li>Aggiunta di nuovi campi a uno schema esistente</li><li>Impostazione di un campo obbligatorio come facoltativo</li></ul> | <ul><li>Rimozione di campi definiti in precedenza</li><li>Introduzione di nuovi campi obbligatori</li><li>Ridenominazione o ridefinizione di campi esistenti</li><li>Rimozione o limitazione di valori di campo supportati in precedenza</li><li>Spostamento degli attributi in una diversa posizione nella struttura</li></ul> |

>[!NOTE]
>
>Se uno schema non è ancora stato utilizzato per assimilare i dati in  Experience Platform, è possibile introdurre una modifica di interruzione nello schema. Tuttavia, una volta che lo schema è stato utilizzato in Platform, deve rispettare i criteri di controllo delle versioni aggiuntivi.

### Schemi e acquisizione dei dati

Per trasferire i dati in  Experience Platform, è necessario creare prima un set di dati. I set di dati sono gli elementi costitutivi della trasformazione e del tracciamento dei dati per il servizio [](../../catalog/home.md)catalogo e generalmente rappresentano tabelle o file contenenti dati acquisiti. Tutti i set di dati si basano sugli schemi XDM esistenti, che forniscono vincoli per ciò che i dati acquisiti devono contenere e per come dovrebbero essere strutturati. Per ulteriori informazioni, consulta la panoramica sull’inserimento dei dati [Adobe Experience Platform](../../ingestion/home.md) .

## Creazione di blocchi di uno schema

 Experience Platform utilizza un approccio di composizione in cui i blocchi di generazione standard vengono combinati per creare schemi. Questo approccio promuove la riutilizzabilità dei componenti esistenti e favorisce la standardizzazione in tutto il settore per supportare schemi e componenti fornitore in Platform.

Gli schemi sono composti utilizzando la seguente formula:

**Classe + Mixin&amp;ast; = Schema XDM**

&amp;ast;Uno schema è composto da una classe e da _zero o più_ mixin. Ciò significa che è possibile comporre uno schema di set di dati senza utilizzare i mixin.

### Classe

La composizione di uno schema inizia con l&#39;assegnazione di una classe. Le classi definiscono gli aspetti comportamentali dei dati che lo schema conterrà (record o serie temporali). Inoltre, le classi descrivono il minor numero di proprietà comuni che tutti gli schemi basati su tale classe dovrebbero includere e forniscono un modo per l&#39;unione di più set di dati compatibili.

Una classe determina inoltre quali mixin saranno utilizzabili nello schema. Questo viene descritto più dettagliatamente nella sezione [mixin](#mixin) che segue.

Esistono classi standard fornite con ogni integrazione di  Experience Platform, note come classi di settore. Le classi di settore sono standard di settore generalmente accettati che si applicano a un&#39;ampia serie di casi d&#39;uso. Esempi di classi Industry includono le classi XDM Singolo profilo e XDM ExperienceEvent fornite da Adobe.

 Experience Platform consente anche classi &quot;Fornitore&quot;, che sono classi definite da  partner Experience Platform e rese disponibili a tutti i clienti che utilizzano tale servizio o applicazione fornitore all&#39;interno di Platform.

Esistono anche classi utilizzate per descrivere casi di utilizzo più specifici per singole organizzazioni all&#39;interno di Platform, denominate classi &quot;Cliente&quot;. Le classi cliente sono definite da un&#39;organizzazione quando non sono disponibili classi Settore o Fornitore per descrivere un caso di utilizzo univoco.

Ad esempio, uno schema che rappresenta i membri di un programma Fedeltà descrive i dati dei record relativi a un singolo utente e può quindi essere basato sulla classe XDM Profilo singolo, una classe di settore standard definita da Adobe.

### Mixin {#mixin}

Un mixin è un componente riutilizzabile che definisce uno o più campi che implementano determinate funzioni come i dati personali, le preferenze alberghiere o l&#39;indirizzo. Le mixine sono destinate ad essere incluse come parte di uno schema che implementa una classe compatibile.

Le combinazioni definiscono le classi con cui sono compatibili in base al comportamento dei dati che rappresentano (serie di record o temporali). Ciò significa che non tutti i mixin sono disponibili per l&#39;uso con tutte le classi.

I mixin hanno lo stesso ambito e la stessa definizione delle classi: esistono mixin di settore, mixin di fornitori e mixin di clienti definiti dalle singole organizzazioni che utilizzano Platform.  Experience Platform include molti mixer standard del settore, consentendo al contempo ai fornitori di definire mixin per i propri utenti e ai singoli utenti di definire mixin base ai propri concetti specifici.

Ad esempio, per acquisire dettagli quali &quot;Nome&quot; e &quot;Indirizzo abitazione&quot; per lo schema &quot;Membri fedeltà&quot;, sarebbe possibile utilizzare mixin standard che definiscono tali concetti comuni. Tuttavia, i concetti specifici per casi di utilizzo meno comuni (come &quot;Livello programma fedeltà&quot;) spesso non hanno un mixin predefinito. In questo caso, per acquisire queste informazioni dovete definire un mixin personalizzato.

Tenere presente che gli schemi sono composti da &quot;zero o più&quot; mixin, pertanto è possibile comporre uno schema valido senza utilizzare alcun mixin.

### Data type {#data-type}

I tipi di dati sono utilizzati come tipi di campi di riferimento in classi o schemi allo stesso modo dei campi letterali di base. La differenza principale sta nel fatto che i tipi di dati possono definire più sottocampi. Analogamente a un mixin, un tipo di dati consente l&#39;uso coerente di una struttura multi-campo, ma offre maggiore flessibilità rispetto a un mixin, perché un tipo di dati può essere incluso in qualsiasi punto dello schema aggiungendo il tipo di dati &quot;tipo&quot; di un campo.

 Experience Platform fornisce una serie di tipi di dati comuni come parte del Registro di sistema dello schema per supportare l&#39;uso di pattern standard per la descrizione delle strutture di dati comuni. Questo è spiegato più in dettaglio nelle esercitazioni del Registro di sistema dello schema, dove diventerà più chiaro man mano che si passano i passaggi per definire i tipi di dati.

### Campo

Un campo è il blocco predefinito più basilare di uno schema. I campi forniscono vincoli relativi al tipo di dati che possono contenere definendo un tipo di dati specifico. Questi tipi di dati di base definiscono un singolo campo, mentre i tipi [di](#data-type) dati precedentemente indicati consentono di definire più sottocampi e di riutilizzare la stessa struttura multi-campo in vari schemi. Pertanto, oltre a definire il &quot;tipo di dati&quot; di un campo come uno dei tipi di dati definiti nel Registro di sistema,  Experience Platform supporta tipi scalari di base come:

* Stringa
* Intero
* Numero
* Booleano
* Matrice
* Oggetto

Gli intervalli validi di questi tipi scalari possono essere ulteriormente vincolati a determinati pattern, formati, minimi/massimi o valori predefiniti. Utilizzando questi vincoli, è possibile rappresentare un&#39;ampia gamma di tipi di campo più specifici, tra cui:

* Enum
* Long
* Breve
* Byte
* Data
* Data-ora
* Mappa

>[!NOTE]
>
>Il tipo di campo &quot;map&quot; consente la creazione di dati con coppie chiave-valore, inclusi più valori per una singola chiave. Le mappe possono essere definite solo a livello di sistema, il che significa che è possibile che una mappa venga visualizzata in uno schema definito dal settore o dal fornitore, ma non è disponibile per l&#39;uso nei campi definiti dall&#39;utente. La guida [per gli sviluppatori API del Registro di](../api/getting-started.md) schema contiene ulteriori informazioni sulla definizione dei tipi di campo.

Alcune operazioni di dati utilizzate dai servizi e dalle applicazioni a valle impongono vincoli su tipi di campo specifici. I servizi interessati includono, tra l&#39;altro:

* [Profilo del cliente in tempo reale](../../profile/home.md)
* [Servizio identità](../../identity-service/home.md)
* [Segmentazione](../../segmentation/home.md)
* [Servizio query](../../query-service/home.md)
* [Area di lavoro Data Science](../../data-science-workspace/home.md)

Prima di creare uno schema da utilizzare nei servizi a valle, consultare la documentazione appropriata per tali servizi al fine di comprendere meglio i requisiti di campo e i vincoli per le operazioni di dati a cui lo schema è destinato.

### Campi XDM

Oltre ai campi di base e alla possibilità di definire i propri tipi di dati, XDM fornisce un set standard di campi e tipi di dati che vengono implicitamente compresi dai servizi Experience Platform  e che assicurano una maggiore coerenza quando utilizzato tra i componenti Platform.

Questi campi, come &quot;Nome&quot; e &quot;Indirizzo e-mail&quot; contengono connotazioni aggiunte oltre i tipi di campi scalari di base, a indicare ad Platform che tutti i campi che condividono lo stesso tipo di dati XDM si comportano allo stesso modo. Questo comportamento può essere considerato coerente, indipendentemente da dove provengano i dati, o in quale servizio Platform vengono utilizzati i dati.

Per un elenco completo dei campi XDM disponibili, consultate il dizionario [dei campi](field-dictionary.md) XDM. Si consiglia di utilizzare i campi e i tipi di dati XDM laddove possibile per supportare coerenza e standardizzazione in  Experience Platform.

## Esempio di composizione

Gli schemi rappresentano il formato e la struttura dei dati che verranno trasferiti in Platform e creati utilizzando un modello di composizione. Come già detto, questi schemi sono composti da una classe e da zero o più mixin compatibili con tale classe.

Ad esempio, uno schema che descrive gli acquisti effettuati in un negozio al dettaglio potrebbe essere denominato &quot;Store Transactions&quot;. Lo schema implementa la classe ExperienceEvent XDM insieme al mixin Commerce standard e al mixin Informazioni prodotto definito dall&#39;utente.

Un altro schema che tiene traccia del traffico del sito Web potrebbe essere denominato &quot;Visite Web&quot;. Implementa anche la classe ExperienceEvent XDM, ma questa volta combina il mixin Web standard.

Il diagramma seguente mostra questi schemi e i campi che contribuiscono a ciascun mixin. Contiene inoltre due schemi basati sulla classe Profilo singolo XDM, incluso lo schema &quot;Membri fedeltà&quot; menzionato in precedenza in questa guida.

![](../images/schema-composition/composition.png)

### Unione {#union}

 Experience Platform consente di comporre schemi per casi di utilizzo particolari, ma consente anche di visualizzare una &quot;unione&quot; di schemi per un tipo di classe specifico. Il diagramma precedente mostra due schemi basati sulla classe ExperienceEvent XDM e due schemi basati sulla classe di profilo individuale XDM. L&#39;unione, come illustrato di seguito, aggrega i campi di tutti gli schemi che condividono la stessa classe (XDM ExperienceEvent e XDM Singolo profilo, rispettivamente).

![](../images/schema-composition/union.png)

Attivando uno schema da utilizzare con il profilo cliente in tempo reale, verrà incluso nell&#39;unione per quel tipo di classe. Il profilo offre profili solidi e centralizzati degli attributi del cliente e un account con marca temporale di ogni evento che il cliente ha avuto in qualsiasi sistema integrato con Platform. Il profilo utilizza la visualizzazione unione per rappresentare questi dati e fornire una visione olistica di ciascun cliente.

Per ulteriori informazioni sull’utilizzo di Profile, consulta la panoramica [Profilo cliente in tempo](../../profile/home.md)reale.

## Mappatura dei file di dati agli schemi XDM

Tutti i file di dati acquisiti in  Experience Platform devono essere conformi alla struttura di uno schema XDM. Per ulteriori informazioni su come formattare i file di dati per conformarsi alle gerarchie XDM (inclusi i file di esempio), consultate il documento sulle trasformazioni [ETL di](../../etl/transformations.md)esempio. Per informazioni generali sull’assimilazione di file di dati in  Experience Platform, consultate la panoramica [sull’assimilazione dei](../../ingestion/batch-ingestion/overview.md)batch.

## Passaggi successivi

Ora che si conoscono le basi della composizione dello schema, è possibile iniziare a creare schemi utilizzando il Registro di sistema dello schema.

Il Registro di sistema dello schema viene utilizzato per accedere alla Libreria schema all&#39;interno  Adobe Experience Platform e fornisce un&#39;interfaccia utente e un&#39;API RESTful da cui sono accessibili tutte le risorse libreria disponibili. La Libreria schema contiene le risorse del settore definite da Adobe, le risorse del fornitore definite da  partner Experience Platform e le classi, i mixin, i tipi di dati e gli schemi che sono stati composti da membri dell&#39;organizzazione.

Per iniziare a comporre lo schema utilizzando l&#39;interfaccia utente, seguire l&#39;esercitazione [Editor](../tutorials/create-schema-ui.md) schema per creare lo schema &quot;Membri fedeltà&quot; menzionato in questo documento.

Per iniziare a utilizzare l&#39;API del Registro di sistema dello schema, iniziare leggendo la guida [per gli sviluppatori API del Registro di](../api/getting-started.md)schema. Dopo aver letto la guida per gli sviluppatori, segui i passaggi descritti nell&#39;esercitazione sulla [creazione di uno schema tramite l&#39;API](../tutorials/create-schema-api.md)del Registro di sistema dello schema.
