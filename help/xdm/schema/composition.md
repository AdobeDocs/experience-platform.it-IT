---
keywords: Experience Platform;home;argomenti popolari;schema;schema;enum;mixin;mixin;mixin;mixin;mixins;tipo di dati;tipi di dati;tipi di dati;tipo di dati;identità primaria;identità principale;profilo individuale XDM;campi XDM;tipo di dati enum;evento esperienza XDM;evento esperienza XDM;ExperienceEvent;experienceevent;XDM Experienceevenet;schema;progettazione;classe Classe;classi;classi;tipo di dati;tipo di dati;tipo di dati;schemi;schemi;mappa identità;mappa identità;mappa identità;progettazione schema;mappa;mappa;schema unione;schema unione
solution: Experience Platform
title: Nozioni di base sulla composizione dello schema
topic: ' - Panoramica'
description: Questo documento fornisce un’introduzione agli schemi Experience Data Model (XDM) e ai blocchi predefiniti, ai principi e alle best practice per la composizione degli schemi da utilizzare in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 8448b5dcedc42898d8a403aae1e044841bc2734c
workflow-type: tm+mt
source-wordcount: '3142'
ht-degree: 0%

---


# Nozioni di base sulla composizione dello schema

Questo documento fornisce un’introduzione agli schemi [!DNL Experience Data Model] (XDM) e ai blocchi predefiniti, ai principi e alle best practice per la composizione degli schemi da utilizzare in Adobe Experience Platform. Per informazioni generali su XDM e su come viene utilizzato in [!DNL Platform], consulta la [Panoramica del sistema XDM](../home.md).

## Informazioni sugli schemi

Uno schema è un insieme di regole che rappresentano e convalidano la struttura e il formato dei dati. Ad alto livello, gli schemi forniscono una definizione astratta di un oggetto reale (ad esempio una persona) e delineano quali dati includere in ogni istanza dell’oggetto (ad esempio nome, cognome, compleanno e così via).

Oltre a descrivere la struttura dei dati, gli schemi applicano vincoli e aspettative ai dati in modo che possano essere convalidati mentre si spostano tra i sistemi. Queste definizioni standard consentono l’interpretazione coerente dei dati, indipendentemente dall’origine, e rimuovono la necessità di tradurre tra le applicazioni.

[!DNL Experience Platform] mantiene questa normalizzazione semantica attraverso l&#39;uso di schemi. Gli schemi sono il modo standard per descrivere i dati in [!DNL Experience Platform], consentendo a tutti i dati conformi agli schemi di essere riutilizzabili senza conflitti all’interno di un’organizzazione e persino di essere condivisibili tra più organizzazioni.

### Tabelle relazionali e oggetti incorporati

Quando si lavora con database relazionali, le best practice prevedono la normalizzazione dei dati o la suddivisione di un’entità in parti discrete che vengono quindi visualizzate su più tabelle. Per leggere i dati nel loro insieme o aggiornare l&#39;entità, è necessario eseguire operazioni di lettura e scrittura in più tabelle singole utilizzando JOIN.

Utilizzando gli oggetti incorporati, gli schemi XDM possono rappresentare direttamente dati complessi e archiviarli in documenti indipendenti con struttura gerarchica. Uno dei principali vantaggi di questa struttura è che consente di eseguire query sui dati senza dover ricostruire l’entità tramite join costosi a più tabelle denormalizzate. Non vi sono restrizioni difficili al numero di livelli possibili nella gerarchia dello schema.

### Schemi e big data

I sistemi digitali moderni generano una grande quantità di segnali comportamentali (dati delle transazioni, registri web, Internet di cose, visualizzazione e così via). Questi big data offrono straordinarie opportunità di ottimizzazione delle esperienze, ma sono difficili da utilizzare a causa della scala e della varietà dei dati. Al fine di trarre valore dai dati, la struttura, il formato e le definizioni devono essere standardizzati in modo da poter essere elaborati in modo coerente ed efficiente.

Gli schemi risolvono questo problema consentendo l&#39;integrazione dei dati da più fonti, standardizzati attraverso strutture e definizioni comuni e condivisi tra le soluzioni. Ciò consente ai processi e ai servizi successivi di rispondere a qualsiasi tipo di domanda posta sui dati, allontanandosi dall’approccio tradizionale alla modellazione dei dati, in cui tutte le domande che verranno poste sui dati sono note in anticipo e i dati sono modellati per conformarsi a tali aspettative.

### Flussi di lavoro basati su schema in [!DNL Experience Platform]

La standardizzazione è un concetto chiave alla base di [!DNL Experience Platform]. XDM, guidato da un Adobe, è uno sforzo per standardizzare i dati sulla customer experience e definire schemi standard per la gestione della customer experience.

L&#39;infrastruttura su cui è generato [!DNL Experience Platform], nota come [!DNL XDM System], agevola i flussi di lavoro basati su schema e include i pattern di consumo del servizio [!DNL Schema Registry], [!DNL Schema Editor], i metadati dello schema e i modelli di consumo del servizio. Per ulteriori informazioni, consulta la [Panoramica del sistema XDM](../home.md) .

Ci sono diversi vantaggi principali nella creazione e nell’utilizzo degli schemi in [!DNL Experience Platform]. In primo luogo, gli schemi consentono una migliore governance dei dati e una minimizzazione dei dati, che è particolarmente importante con le normative sulla privacy. In secondo luogo, la creazione di schemi con componenti standard di Adobe consente di ottenere informazioni predefinite e l’utilizzo di servizi AI/ML con personalizzazioni minime. Infine, gli schemi forniscono un’infrastruttura per la condivisione dei dati insights e un’orchestrazione efficiente.

## Pianificazione dello schema

Il primo passaggio nella creazione di uno schema consiste nel determinare il concetto, o oggetto reale, che si sta tentando di acquisire all&#39;interno dello schema. Una volta identificato il concetto che si sta tentando di descrivere, è possibile iniziare a pianificare lo schema pensando a elementi quali il tipo di dati, i campi di identità potenziali e l&#39;evoluzione dello schema in futuro.

### Comportamenti dei dati in [!DNL Experience Platform]

I dati destinati all&#39;uso in [!DNL Experience Platform] sono raggruppati in due tipi di comportamento:

* **Dati** record: Fornisce informazioni sugli attributi di un soggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.
* **Dati** serie temporali: Fornisce un&#39;istantanea del sistema nel momento in cui un&#39;azione è stata eseguita direttamente o indirettamente da un soggetto del record.

Tutti gli schemi XDM descrivono i dati che possono essere classificati come record o serie temporali. Il comportamento dei dati di uno schema è definito dalla classe dello schema, che viene assegnata a uno schema quando viene creato per la prima volta. Le classi XDM sono descritte in dettaglio più avanti in questo documento.

Gli schemi di record e serie temporali contengono una mappa di identità (`xdm:identityMap`). Questo campo contiene la rappresentazione di identità di un soggetto, ricavata dai campi contrassegnati come &quot;Identità&quot; come descritto nella sezione successiva.

### [!UICONTROL Identity] {#identity}

Gli schemi vengono utilizzati per assimilare i dati in [!DNL Experience Platform]. Questi dati possono essere utilizzati in più servizi per creare una singola vista unificata di una singola entità. Pertanto, quando si pensa agli schemi, è importante pensare all&#39;identità dei clienti e a quali campi è possibile utilizzare per identificare un soggetto, indipendentemente da dove i dati provengono.

Per facilitare questo processo, i campi chiave all&#39;interno degli schemi possono essere contrassegnati come identità. Al momento dell&#39;assimilazione dei dati, i dati contenuti in tali campi vengono inseriti in &quot;[!UICONTROL Identity Graph]&quot; per tale persona. I dati del grafico possono quindi essere utilizzati da [[!DNL Real-time Customer Profile]](../../profile/home.md) e da altri [!DNL Experience Platform] servizi per fornire una visione unificata di ciascun singolo cliente.

I campi generalmente contrassegnati come &quot;[!UICONTROL Identity]&quot; includono: indirizzo e-mail, numero di telefono, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), ID CRM o altri campi ID univoci. È inoltre consigliabile prendere in considerazione eventuali identificatori univoci specifici dell&#39;organizzazione, in quanto potrebbero essere validi anche i campi &quot;[!UICONTROL Identity]&quot;.

È importante considerare le identità dei clienti durante la fase di pianificazione dello schema per garantire che i dati vengano riuniti per creare il profilo più affidabile possibile. Consulta la panoramica su [Adobe Experience Platform Identity Service](../../identity-service/home.md) per saperne di più su come le informazioni sull&#39;identità possono aiutarti a distribuire esperienze digitali ai tuoi clienti.

#### xdm:identityMap {#identityMap}

`xdm:identityMap` è un campo del tipo di mappa che descrive i diversi valori di identità di un singolo utente, insieme ai relativi spazi dei nomi associati. Questo campo può essere utilizzato per fornire informazioni di identità per gli schemi, anziché definire i valori di identità all&#39;interno della struttura dello schema stesso.

Un esempio di mappa di identità semplice ha il seguente aspetto:

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

Come illustrato nell&#39;esempio precedente, ogni chiave dell&#39;oggetto `identityMap` rappresenta uno spazio dei nomi Identity. Il valore di ogni chiave è un array di oggetti che rappresenta i valori di identità (`id`) per il rispettivo spazio dei nomi. Fare riferimento alla documentazione [!DNL Identity Service] per un [elenco di spazi dei nomi di identità standard ](../../identity-service/troubleshooting-guide.md#standard-namespaces) riconosciuto dalle applicazioni  Adobe.

>[!NOTE]
>
>È possibile specificare un valore booleano per indicare se il valore è un&#39;identità primaria (`primary`) anche per ogni valore di identità. Le identità principali devono essere impostate solo per gli schemi destinati a essere utilizzati in [!DNL Real-time Customer Profile]. Per ulteriori informazioni, vedere la sezione relativa agli [schemi di unione](#union).

### Principi di evoluzione dello schema {#evolution}

Mentre la natura delle esperienze digitali continua ad evolversi, devono evolversi anche gli schemi utilizzati per rappresentarle. Uno schema ben progettato è quindi in grado di adattarsi e evolvere in base alle esigenze, senza causare modifiche distruttive alle versioni precedenti dello schema.

Poiché il mantenimento della compatibilità con le versioni precedenti è fondamentale per l&#39;evoluzione dello schema, [!DNL Experience Platform] applica un principio di controllo delle versioni puramente additivo per garantire che qualsiasi revisione dello schema produca solo aggiornamenti e modifiche non distruttivi. In altre parole, le **modifiche di interruzione non sono supportate.**

| Modifiche supportate | Interruzione delle modifiche (non supportata) |
|------------------------------------|---------------------------------|
| <ul><li>Aggiunta di nuovi campi a uno schema esistente</li><li>Impostazione di un campo obbligatorio come facoltativo</li></ul> | <ul><li>Rimozione di campi definiti in precedenza</li><li>Introduzione di nuovi campi obbligatori</li><li>Ridenominazione o ridefinizione dei campi esistenti</li><li>Rimozione o limitazione dei valori di campo supportati in precedenza</li><li>Spostamento degli attributi in una posizione diversa nella struttura</li></ul> |

>[!NOTE]
>
>Se uno schema non è ancora stato utilizzato per acquisire dati in [!DNL Experience Platform], è possibile introdurre una modifica di interruzione allo schema. Tuttavia, una volta che lo schema è stato utilizzato in [!DNL Platform], deve rispettare i criteri di controllo delle versioni aggiuntive.

### Schemi e acquisizione dati

Per acquisire i dati in [!DNL Experience Platform], è necessario creare prima un set di dati. I set di dati sono gli elementi costitutivi della trasformazione e del tracciamento dei dati per [[!DNL Catalog Service]](../../catalog/home.md) e generalmente rappresentano tabelle o file contenenti dati acquisiti. Tutti i set di dati si basano sugli schemi XDM esistenti, che forniscono vincoli per ciò che i dati acquisiti devono contenere e per come devono essere strutturati. Per ulteriori informazioni, consulta la panoramica su [Acquisizione dati Adobe Experience Platform](../../ingestion/home.md) .

## Blocco di uno schema

[!DNL Experience Platform] utilizza un approccio di composizione in cui i blocchi predefiniti standard vengono combinati per creare schemi. Questo approccio promuove la riutilizzabilità dei componenti esistenti e favorisce la standardizzazione in tutto il settore per supportare schemi e componenti dei fornitori in [!DNL Platform].

Gli schemi sono composti con la seguente formula:

**Classe + Mixin&amp;ast; = Schema XDM**

&amp;ast;Uno schema è composto da una classe e da zero o più mixin. Ciò significa che puoi comporre uno schema di set di dati senza utilizzare affatto i mixin.

### Classe {#class}

La composizione di uno schema inizia con l’assegnazione di una classe. Le classi definiscono gli aspetti comportamentali dei dati che lo schema conterrà (record o serie temporali). Inoltre, le classi descrivono il numero più piccolo di proprietà comuni che tutti gli schemi basati su tale classe dovrebbero includere e forniscono un modo per unire più set di dati compatibili.

La classe di uno schema determina quali mixin saranno idonei per essere utilizzati in tale schema. Questo è discusso più dettagliatamente nella [sezione successiva](#mixin).

Adobe fornisce due classi XDM standard (&quot;core&quot;): [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent]. Inoltre, puoi creare classi personalizzate per descrivere casi d’uso più specifici per la tua organizzazione. Le classi personalizzate sono definite da un&#39;organizzazione quando non sono disponibili classi principali definite da Adobi per descrivere un caso d&#39;uso univoco.

### Mixin {#mixin}

Un mixin è un componente riutilizzabile che definisce uno o più campi che implementano determinate funzioni come dettagli personali, preferenze alberghiere o indirizzo. I mixin devono essere inclusi come parte di uno schema che implementa una classe compatibile.

I mixin definiscono con quali classi sono compatibili in base al comportamento dei dati che rappresentano (record o serie temporali). Ciò significa che non tutti i mixin sono disponibili per l&#39;uso con tutte le classi.

[!DNL Experience Platform] include molti mixin di Adobe standard, consentendo al contempo ai fornitori di definire mixin per i propri utenti e ai singoli utenti di definire mixin base ai propri concetti specifici.

Ad esempio, per acquisire dettagli quali &quot;[!UICONTROL First Name]&quot; e &quot;[!UICONTROL Home Address]&quot; per lo schema &quot;[!UICONTROL Loyalty Members]&quot;, puoi utilizzare mixin standard che definiscono tali concetti comuni. Tuttavia, i concetti specifici dei casi di utilizzo meno comuni (come &quot;[!UICONTROL Loyalty Program Level]&quot;) spesso non hanno un mixin predefinito. In questo caso, è necessario definire il proprio mixin per acquisire queste informazioni.

Gli schemi sono composti da &quot;zero o più&quot; mixin, quindi è possibile comporre uno schema valido senza utilizzare alcun mixin.

Per un elenco di tutti i mixin standard correnti, fai riferimento al [repository XDM ufficiale](https://github.com/adobe/xdm/tree/master/components/mixins).

### Tipo di dati {#data-type}

I tipi di dati vengono utilizzati come tipi di campi di riferimento in classi o schemi allo stesso modo dei campi letterali di base. La differenza principale consiste nel fatto che i tipi di dati possono definire più campi secondari. Simile a un mixin, un tipo di dati consente l’utilizzo coerente di una struttura a più campi, ma offre maggiore flessibilità rispetto a un mixin perché un tipo di dati può essere incluso ovunque in uno schema, aggiungendolo come &quot;tipo di dati&quot; di un campo.

>[!NOTE]
>
>Per ulteriori informazioni sulle differenze tra mixin e tipi di dati, nonché sui pro e i contro dell&#39;utilizzo uno sull&#39;altro per casi d&#39;uso simili, vedere l&#39; [appendice](#mixins-v-datatypes) .

[!DNL Experience Platform] fornisce una serie di tipi di dati comuni come parte del  [!DNL Schema Registry] per supportare l&#39;uso di pattern standard per descrivere le strutture di dati comuni. Questo è spiegato più dettagliatamente nelle [!DNL Schema Registry] esercitazioni, dove diventerà più chiaro man mano che segui i passaggi per definire i tipi di dati.

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

Gli schemi rappresentano il formato e la struttura dei dati che verranno acquisiti in [!DNL Platform] e vengono generati utilizzando un modello di composizione. Come accennato in precedenza, questi schemi sono composti da una classe e da zero o più mixin compatibili con tale classe.

Ad esempio, uno schema che descrive gli acquisti effettuati in un negozio al dettaglio potrebbe essere denominato &quot;[!UICONTROL Store Transactions]&quot;. Lo schema implementa la classe [!DNL XDM ExperienceEvent] combinata con il mixin standard [!UICONTROL Commerce] e un mixin definito dall&#39;utente [!UICONTROL Product Info].

Un altro schema che tiene traccia del traffico del sito web potrebbe essere denominato &quot;[!UICONTROL Web Visits]&quot;. Implementa anche la classe [!DNL XDM ExperienceEvent], ma questa volta combina il mixin standard [!UICONTROL Web].

Il diagramma seguente mostra questi schemi e i campi a cui ciascun mixin ha contribuito. Contiene inoltre due schemi basati sulla classe [!DNL XDM Individual Profile] , incluso lo schema &quot;[!UICONTROL Loyalty Members]&quot; menzionato in precedenza in questa guida.

![](../images/schema-composition/composition.png)

### Unione {#union}

Sebbene [!DNL Experience Platform] ti consenta di comporre schemi per casi d’uso particolari, ti consente anche di visualizzare un’&quot;unione&quot; di schemi per un tipo di classe specifico. Il diagramma precedente mostra due schemi basati sulla classe ExperienceEvent XDM e due schemi basati sulla classe [!DNL XDM Individual Profile] . L’unione, come illustrato di seguito, aggrega i campi di tutti gli schemi che condividono la stessa classe ([!DNL XDM ExperienceEvent] e [!DNL XDM Individual Profile], rispettivamente).

![](../images/schema-composition/union.png)

Attivando uno schema da utilizzare con [!DNL Real-time Customer Profile], verrà incluso nell&#39;unione per quel tipo di classe. [!DNL Profile] fornisce profili affidabili e centralizzati degli attributi del cliente e un account con marca temporale di ogni evento che il cliente ha avuto in qualsiasi sistema integrato con  [!DNL Platform]. [!DNL Profile] utilizza la visualizzazione unione per rappresentare questi dati e fornire una visualizzazione olistica di ogni singolo cliente.

Per ulteriori informazioni sulle operazioni con [!DNL Profile], consulta la [Panoramica sul profilo cliente in tempo reale](../../profile/home.md).

## Mappatura di file di dati su schemi XDM

Tutti i file di dati acquisiti in [!DNL Experience Platform] devono essere conformi alla struttura di uno schema XDM. Per ulteriori informazioni su come formattare i file di dati per conformarsi alle gerarchie XDM (inclusi i file di esempio), consulta il documento sulle [trasformazioni ETL di esempio](../../etl/transformations.md). Per informazioni generali sull’acquisizione di file di dati in [!DNL Experience Platform], consulta la [panoramica sull’acquisizione batch](../../ingestion/batch-ingestion/overview.md).

## Passaggi successivi

Ora che conosci le nozioni di base della composizione dello schema, sei pronto per iniziare a esplorare e creare schemi utilizzando il [!DNL Schema Registry].

Per rivedere la struttura delle due classi XDM principali e dei rispettivi mixin compatibili comunemente utilizzati, consulta la seguente documentazione di riferimento:

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

L’ [!DNL Schema Registry] viene utilizzato per accedere a [!DNL Schema Library] all’interno di Adobe Experience Platform e fornisce un’interfaccia utente e un’API RESTful da cui sono accessibili tutte le risorse della libreria disponibili. Il [!DNL Schema Library] contiene risorse di settore definite da Adobe, risorse fornitore definite dai partner [!DNL Experience Platform] e classi, mixin, tipi di dati e schemi che sono stati composti da membri dell&#39;organizzazione.

Per iniziare a comporre lo schema utilizzando l&#39;interfaccia utente, segui insieme all&#39; [tutorial Editor di schema](../tutorials/create-schema-ui.md) per creare lo schema &quot;Membri fedeltà&quot; menzionato in questo documento.

Per iniziare a utilizzare l&#39;API [!DNL Schema Registry], leggi la [Guida per gli sviluppatori dell&#39;API del Registro di sistema ](../api/getting-started.md). Dopo aver letto la guida per gli sviluppatori, segui i passaggi descritti nell&#39;esercitazione su [creazione di uno schema utilizzando l&#39;API del Registro di sistema dello schema](../tutorials/create-schema-api.md).

## Appendice

La sezione seguente contiene informazioni aggiuntive sui principi della composizione dello schema.

### Oggetti e campi a forma libera {#objects-v-freeform}

Durante la progettazione degli schemi, è necessario tenere in considerazione alcuni fattori chiave nella scelta degli oggetti rispetto ai campi a forma libera:

| Oggetti | Campi in formato libero |
| --- | --- |
| Aumenta la nidificazione | Minore o nessuna nidificazione |
| Crea raggruppamenti di campi logici | I campi sono posizionati in posizioni ad hoc |

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