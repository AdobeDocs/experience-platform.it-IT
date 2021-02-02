---
keywords: ' Experience Platform;home;argomenti più comuni;schema;schema;enum;mixin;Mixin;Mixin;mixins;tipo di dati;tipi di dati;tipi di dati;tipo di dati;identità primaria;identità primaria;profilo individuale XDM;campo XDM;tipo di dati;evento esperienza XDM;evento esperienza;evento esperienza;evento esperienza;evento XDM;evento esperienza;XDM Experienceevent;schema;class Classe;classi;Classi;tipo di dati;Tipo di dati;Tipo di dati;Schemi;Mappa identità;Mappa identità;Mappa identità;Schema schema;Mappa;schema unione;unione'
solution: Experience Platform
title: Nozioni di base sulla composizione dello schema
topic: overview
description: Questo documento fornisce un'introduzione agli schemi di Experience Data Model (XDM) e ai blocchi costitutivi, ai principi e alle procedure ottimali per la composizione degli schemi da utilizzare in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '3141'
ht-degree: 0%

---


# Nozioni di base sulla composizione dello schema

Questo documento fornisce un&#39;introduzione agli schemi [!DNL Experience Data Model] (XDM) e ai blocchi di generazione, ai principi e alle procedure ottimali per la composizione degli schemi da utilizzare in Adobe Experience Platform. Per informazioni generali su XDM e come viene utilizzato all&#39;interno di [!DNL Platform], consultare la [Panoramica del sistema XDM](../home.md).

## Informazioni sugli schemi

Uno schema è un insieme di regole che rappresentano e convalidano la struttura e il formato dei dati. A un livello elevato, gli schemi forniscono una definizione astratta di un oggetto reale (ad esempio una persona) e delineano quali dati includere in ciascuna istanza di tale oggetto (ad esempio nome, cognome, compleanno e così via).

Oltre a descrivere la struttura dei dati, gli schemi applicano vincoli e aspettative ai dati in modo che possano essere convalidati man mano che si spostano tra i sistemi. Queste definizioni standard consentono l&#39;interpretazione coerente dei dati, indipendentemente dall&#39;origine, e rimuovono la necessità di una traduzione tra le applicazioni.

[!DNL Experience Platform] mantiene questa normalizzazione semantica attraverso l&#39;uso di schemi. Gli schemi sono il modo standard per descrivere i dati in [!DNL Experience Platform], consentendo a tutti i dati conformi agli schemi di essere riutilizzabili senza conflitti all&#39;interno di un&#39;organizzazione e persino di essere condivisibili tra più organizzazioni.

### Tabelle relazionali e oggetti incorporati

Quando si utilizzano i database relazionali, le best practice prevedono la normalizzazione dei dati o la suddivisione di un&#39;entità in parti distinte che vengono visualizzate in più tabelle. Per leggere i dati nel loro insieme o aggiornare l&#39;entità, le operazioni di lettura e scrittura devono essere eseguite in più singole tabelle utilizzando JOIN.

Utilizzando gli oggetti incorporati, gli schemi XDM possono rappresentare direttamente dati complessi e archiviarli in documenti indipendenti con una struttura gerarchica. Uno dei principali vantaggi di questa struttura è che consente di eseguire query sui dati senza dover ricostruire l&#39;entità tramite join costosi a più tabelle denormalizzate. Non esistono vincoli rigidi per il numero di livelli possibili per la gerarchia dello schema.

### Schemi e grandi dati

I sistemi digitali moderni generano una vasta quantità di segnali comportamentali (dati sulle transazioni, registri web, Internet di cose, visualizzazione e così via). Questi grandi dati offrono straordinarie opportunità di ottimizzare le esperienze, ma sono difficili da utilizzare a causa della scala e della varietà dei dati. Al fine di ottenere valore dai dati, la struttura, il formato e le definizioni devono essere standardizzati in modo che possano essere elaborati in modo coerente ed efficiente.

Gli schemi risolvono questo problema consentendo l&#39;integrazione dei dati da più fonti, standardizzati attraverso strutture e definizioni comuni e condivisi tra soluzioni. Questo consente ai processi e ai servizi successivi di rispondere a qualsiasi tipo di domanda posta sui dati, allontanandosi dall&#39;approccio tradizionale alla modellazione dei dati, dove tutte le domande che verranno poste sui dati sono note in anticipo e i dati sono modellati per conformarsi a tali aspettative.

### Flussi di lavoro basati su schema in [!DNL Experience Platform]

La standardizzazione è un concetto chiave dietro [!DNL Experience Platform]. XDM, guidato da  Adobe, è uno sforzo per standardizzare i dati sull&#39;esperienza cliente e definire schemi standard per la gestione dell&#39;esperienza cliente.

L&#39;infrastruttura su cui è costruito [!DNL Experience Platform], nota come [!DNL XDM System], semplifica i flussi di lavoro basati su schema e include i [!DNL Schema Registry], [!DNL Schema Editor], i metadati dello schema e i pattern di consumo del servizio. Per ulteriori informazioni, vedere [Panoramica del sistema XDM](../home.md).

La creazione e l&#39;utilizzo di schemi in [!DNL Experience Platform] presenta diversi vantaggi principali. In primo luogo, gli schemi consentono una migliore governance dei dati e una minimizzazione dei dati, che è particolarmente importante con le normative sulla privacy. In secondo luogo, la creazione di schemi con  Adobe  componenti standard consente di ottenere informazioni dettagliate e l&#39;utilizzo dei servizi AI/ML con personalizzazioni minime. Infine, gli schemi forniscono infrastrutture per la condivisione dei dati e un&#39;orchestrazione efficiente.

## Pianificazione dello schema

Il primo passaggio nella creazione di uno schema consiste nel determinare il concetto, o oggetto reale, che si sta tentando di acquisire all&#39;interno dello schema. Una volta identificato il concetto che si sta cercando di descrivere, è possibile iniziare a pianificare lo schema pensando a cose come il tipo di dati, campi di identità potenziali e come lo schema potrebbe evolvere in futuro.

### Comportamenti dei dati in [!DNL Experience Platform]

I dati destinati all&#39;uso in [!DNL Experience Platform] sono raggruppati in due tipi di comportamento:

* **Record data**: Fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.
* **Dati** serie temporali: Fornisce un&#39;istantanea del sistema al momento in cui un&#39;azione è stata eseguita direttamente o indirettamente da un soggetto del record.

Tutti gli schemi XDM descrivono i dati che possono essere classificati come record o serie temporali. Il comportamento dei dati di uno schema è definito dalla classe dello schema, che viene assegnata a uno schema al momento della sua prima creazione. Le classi XDM sono descritte in dettaglio più avanti in questo documento.

Gli schemi di record e di serie temporali contengono una mappa di identità (`xdm:identityMap`). Questo campo contiene la rappresentazione di identità di un oggetto, ricavata dai campi contrassegnati come &quot;Identità&quot; come descritto nella sezione successiva.

### [!UICONTROL Identity] {#identity}

Gli schemi vengono utilizzati per l&#39;assimilazione dei dati in [!DNL Experience Platform]. Questi dati possono essere utilizzati tra più servizi per creare una singola vista unificata di una singola entità. Pertanto, è importante, quando si pensa agli schemi, pensare alle identità dei clienti e ai campi che possono essere utilizzati per identificare un oggetto, a prescindere da dove i dati provengano.

Per facilitare questo processo, i campi chiave negli schemi possono essere contrassegnati come identità. Al momento dell&#39;inserimento dei dati, i dati contenuti in tali campi vengono inseriti nel campo &quot;[!UICONTROL Identity Graph]&quot; per l&#39;individuo in questione. I dati del grafico sono quindi accessibili da [[!DNL Real-time Customer Profile]](../../profile/home.md) e da altri servizi [!DNL Experience Platform] per fornire una visualizzazione unita di ciascun cliente.

I campi generalmente contrassegnati come &quot;[!UICONTROL Identity]&quot; includono: indirizzo e-mail, numero di telefono, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), ID CRM o altri campi ID univoci. È inoltre necessario considerare eventuali identificatori univoci specifici della propria organizzazione, in quanto possono essere buoni anche i campi &quot;[!UICONTROL Identity]&quot;.

È importante considerare le identità dei clienti durante la fase di pianificazione dello schema, in modo da garantire che i dati vengano uniti per creare il profilo più affidabile possibile. Consulta la panoramica su [Adobe Experience Platform Identity Service](../../identity-service/home.md) per saperne di più su come le informazioni sull&#39;identità possono aiutarti a fornire esperienze digitali ai tuoi clienti.

#### xdm:identityMap {#identityMap}

`xdm:identityMap` è un campo del tipo di mappa che descrive i vari valori di identità di un individuo, insieme ai relativi spazi dei nomi associati. Questo campo può essere utilizzato per fornire informazioni di identità per gli schemi, invece di definire valori di identità all&#39;interno della struttura dello schema stesso.

Esempio di mappa identità semplice:

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

Come illustrato nell&#39;esempio precedente, ogni chiave dell&#39;oggetto `identityMap` rappresenta uno spazio dei nomi di identità. Il valore di ciascuna chiave è un array di oggetti che rappresenta i valori di identità (`id`) per il rispettivo namespace. Fare riferimento alla documentazione [!DNL Identity Service] per un [elenco di spazi dei nomi identità standard](../../identity-service/troubleshooting-guide.md#standard-namespaces) riconosciuti dalle applicazioni  Adobe.

>[!NOTE]
>
>Per ogni valore di identità è possibile specificare anche un valore booleano che indica se il valore è un&#39;identità primaria (`primary`). Le identità principali devono essere impostate solo per gli schemi destinati a essere utilizzati in [!DNL Real-time Customer Profile]. Per ulteriori informazioni, vedere la sezione relativa agli [schemi di unione](#union).

### Principi di evoluzione dello schema {#evolution}

Mentre la natura delle esperienze digitali continua ad evolversi, devono evolversi anche gli schemi utilizzati per rappresentarle. Uno schema ben progettato è quindi in grado di adattarsi ed evolversi in base alle esigenze, senza causare modifiche distruttive alle versioni precedenti dello schema.

Poiché il mantenimento della compatibilità con le versioni precedenti è fondamentale per l&#39;evoluzione dello schema, [!DNL Experience Platform] applica un principio di controllo delle versioni puramente additivo, in modo da garantire che qualsiasi revisione dello schema produca solo aggiornamenti e modifiche non distruttive. In altre parole, le **modifiche di interruzione non sono supportate.**

| Modifiche supportate | Interruzione delle modifiche (non supportata) |
|------------------------------------|---------------------------------|
| <ul><li>Aggiunta di nuovi campi a uno schema esistente</li><li>Impostazione di un campo obbligatorio come facoltativo</li></ul> | <ul><li>Rimozione di campi definiti in precedenza</li><li>Introduzione di nuovi campi obbligatori</li><li>Ridenominazione o ridefinizione di campi esistenti</li><li>Rimozione o limitazione di valori di campo supportati in precedenza</li><li>Spostamento degli attributi in una diversa posizione nella struttura</li></ul> |

>[!NOTE]
>
>Se uno schema non è ancora stato utilizzato per assimilare i dati in [!DNL Experience Platform], è possibile introdurre una modifica di interruzione nello schema. Tuttavia, una volta che lo schema è stato utilizzato in [!DNL Platform], deve rispettare i criteri di controllo delle versioni aggiuntivi.

### Schemi e acquisizione dei dati

Per acquisire i dati in [!DNL Experience Platform], è necessario creare prima un set di dati. I set di dati sono i blocchi costitutivi per la trasformazione e il tracciamento dei dati per [[!DNL Catalog Service]](../../catalog/home.md) e generalmente rappresentano tabelle o file contenenti dati acquisiti. Tutti i set di dati si basano sugli schemi XDM esistenti, che forniscono vincoli per ciò che i dati acquisiti devono contenere e per come dovrebbero essere strutturati. Per ulteriori informazioni, vedere la panoramica su [Adobe Experience Platform Data Ingestion](../../ingestion/home.md).

## Creazione di blocchi di uno schema

[!DNL Experience Platform] utilizza un approccio di composizione in cui i blocchi di generazione standard vengono combinati per creare schemi. Questo approccio promuove la riutilizzabilità dei componenti esistenti e favorisce la standardizzazione in tutto il settore per supportare schemi e componenti fornitore in [!DNL Platform].

Gli schemi sono composti utilizzando la seguente formula:

**Classe + Mixin&amp;ast; = Schema XDM**

&amp;ast;Uno schema è composto da una classe e da zero o più mixin. Ciò significa che è possibile comporre uno schema di set di dati senza utilizzare i mixin.

### Classe {#class}

La composizione di uno schema inizia con l&#39;assegnazione di una classe. Le classi definiscono gli aspetti comportamentali dei dati che lo schema conterrà (record o serie temporali). Inoltre, le classi descrivono il minor numero di proprietà comuni che tutti gli schemi basati su tale classe dovrebbero includere e forniscono un modo per l&#39;unione di più set di dati compatibili.

La classe di uno schema determina quali mixin saranno utilizzabili in tale schema. Questo argomento viene discusso più in dettaglio nella sezione [successiva](#mixin).

 Adobe fornisce due classi XDM standard (&quot;core&quot;): [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent]. Inoltre, è possibile creare classi personalizzate per descrivere casi d&#39;uso più specifici per l&#39;organizzazione. Le classi personalizzate sono definite da un&#39;organizzazione quando non sono disponibili  classi di base definite dal Adobe per descrivere un caso d&#39;uso univoco.

### Mixin {#mixin}

Un mixin è un componente riutilizzabile che definisce uno o più campi che implementano determinate funzioni come i dati personali, le preferenze alberghiere o l&#39;indirizzo. Le mixine sono destinate ad essere incluse come parte di uno schema che implementa una classe compatibile.

Le combinazioni definiscono le classi con cui sono compatibili in base al comportamento dei dati che rappresentano (record o serie temporali). Ciò significa che non tutti i mixin sono disponibili per l&#39;uso con tutte le classi.

[!DNL Experience Platform] include molti mixer standard  Adobe, consentendo al contempo ai fornitori di definire mixin per i propri utenti e ai singoli utenti di definire mixin base ai propri concetti specifici.

Ad esempio, per acquisire dettagli quali &quot;[!UICONTROL First Name]&quot; e &quot;[!UICONTROL Home Address]&quot; per lo schema &quot;[!UICONTROL Loyalty Members]&quot;, sarebbe possibile utilizzare mixin standard che definiscono tali concetti comuni. Tuttavia, i concetti specifici per casi di utilizzo meno comuni (come &quot;[!UICONTROL Loyalty Program Level]&quot;) spesso non hanno un mixin predefinito. In questo caso, per acquisire queste informazioni dovete definire un mixin personalizzato.

Tenere presente che gli schemi sono composti da &quot;zero o più&quot; mixin, pertanto è possibile comporre uno schema valido senza utilizzare alcun mixin.

Per un elenco di tutti i mixin standard correnti, fare riferimento al [repository ufficiale XDM](https://github.com/adobe/xdm/tree/master/components/mixins).

### Tipo di dati {#data-type}

I tipi di dati sono utilizzati come tipi di campi di riferimento in classi o schemi allo stesso modo dei campi letterali di base. La differenza principale sta nel fatto che i tipi di dati possono definire più sottocampi. Analogamente a un mixin, un tipo di dati consente l&#39;uso coerente di una struttura multi-campo, ma offre maggiore flessibilità rispetto a un mixin, perché un tipo di dati può essere incluso in qualsiasi punto dello schema aggiungendo il tipo di dati &quot;tipo&quot; di un campo.

>[!NOTE]
>
>Per ulteriori informazioni sulle differenze tra i mixini e i tipi di dati, vedere l&#39; [appendice](#mixins-v-datatypes) e i pro e i contro dell&#39;uso di uno sopra l&#39;altro per casi d&#39;uso simili.

[!DNL Experience Platform] fornisce una serie di tipi di dati comuni come parte del  [!DNL Schema Registry] supporto all&#39;uso di pattern standard per la descrizione di strutture di dati comuni. Questo è spiegato più dettagliatamente nelle [!DNL Schema Registry] esercitazioni, dove diventerà più chiaro man mano che si passano i passaggi per definire i tipi di dati.

### Campo

Un campo è il blocco predefinito più basilare di uno schema. I campi forniscono vincoli relativi al tipo di dati che possono contenere definendo un tipo di dati specifico. Questi tipi di dati di base definiscono un singolo campo, mentre i [tipi di dati](#data-type) precedentemente citati consentono di definire più sottocampi e di riutilizzare la stessa struttura multi-campo in vari schemi. Pertanto, oltre a definire il &quot;tipo di dati&quot; di un campo come uno dei tipi di dati definiti nel Registro di sistema, [!DNL Experience Platform] supporta tipi scalari di base come:

* Stringa
* Intero
* Doppio
* Booleano
* Matrice
* Oggetto

>[!TIP]
>
>Per informazioni sui pro e i contro dell&#39;utilizzo di campi modulo gratuiti rispetto ai campi di tipo oggetto, vedere l&#39; [appendice](#objects-v-freeform).

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
>Il tipo di campo &quot;map&quot; consente la creazione di dati con coppie chiave-valore, inclusi più valori per una singola chiave. Le mappe possono essere definite solo a livello di sistema, il che significa che è possibile che una mappa venga visualizzata in uno schema definito dal settore o dal fornitore, ma non è disponibile per l&#39;uso nei campi definiti dall&#39;utente. La [Guida per gli sviluppatori API del Registro di sistema dello schema](../api/getting-started.md) contiene ulteriori informazioni sulla definizione dei tipi di campo.

Alcune operazioni di dati utilizzate dai servizi e dalle applicazioni a valle impongono vincoli su tipi di campo specifici. I servizi interessati includono, tra l&#39;altro:

* [[!DNL Real-time Customer Profile]](../../profile/home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!DNL Segmentation]](../../segmentation/home.md)
* [[!DNL Query Service]](../../query-service/home.md)
* [[!DNL Data Science Workspace]](../../data-science-workspace/home.md)

Prima di creare uno schema da utilizzare nei servizi a valle, consultare la documentazione appropriata per tali servizi al fine di comprendere meglio i requisiti di campo e i vincoli per le operazioni di dati a cui lo schema è destinato.

### Campi XDM

Oltre ai campi di base e alla possibilità di definire i propri tipi di dati, XDM fornisce un set standard di campi e tipi di dati che vengono implicitamente compresi dai servizi [!DNL Experience Platform] e che assicurano una maggiore coerenza se utilizzati tra i componenti [!DNL Platform].

Questi campi, come &quot;Nome&quot; e &quot;Indirizzo e-mail&quot; contengono connotazioni aggiunte oltre i tipi di campi scalari di base, a [!DNL Platform] per indicare che tutti i campi che condividono lo stesso tipo di dati XDM si comportano allo stesso modo. Questo comportamento può essere considerato coerente, indipendentemente da dove provengono i dati, o in cui vengono utilizzati i dati [!DNL Platform].

Per un elenco completo dei campi XDM disponibili, vedere il [dizionario dei campi XDM](field-dictionary.md). Si consiglia di utilizzare i campi e i tipi di dati XDM laddove possibile per supportare coerenza e standardizzazione in [!DNL Experience Platform].

## Esempio di composizione

Gli schemi rappresentano il formato e la struttura dei dati che verranno assimilati in [!DNL Platform] e vengono generati utilizzando un modello di composizione. Come già detto, questi schemi sono composti da una classe e da zero o più mixin compatibili con tale classe.

Ad esempio, uno schema che descrive gli acquisti effettuati in uno store per la vendita al dettaglio potrebbe essere denominato &quot;[!UICONTROL Store Transactions]&quot;. Lo schema implementa la classe [!DNL XDM ExperienceEvent] combinata con il mixin [!UICONTROL Commerce] standard e un mixin [!UICONTROL Product Info] definito dall&#39;utente.

Un altro schema che tiene traccia del traffico del sito Web potrebbe essere denominato &quot;[!UICONTROL Web Visits]&quot;. Implementa anche la classe [!DNL XDM ExperienceEvent], ma questa volta combina il mixin [!UICONTROL Web] standard.

Il diagramma seguente mostra questi schemi e i campi che contribuiscono a ciascun mixin. Contiene inoltre due schemi basati sulla classe [!DNL XDM Individual Profile], incluso lo schema &quot;[!UICONTROL Loyalty Members]&quot; menzionato in precedenza in questa guida.

![](../images/schema-composition/composition.png)

### Unione {#union}

[!DNL Experience Platform] consente di comporre gli schemi per casi di utilizzo particolari, ma consente anche di visualizzare una &quot;unione&quot; di schemi per un tipo di classe specifico. Il diagramma precedente mostra due schemi basati sulla classe ExperienceEvent XDM e due schemi basati sulla classe [!DNL XDM Individual Profile]. L&#39;unione, come illustrato di seguito, aggrega i campi di tutti gli schemi che condividono la stessa classe ([!DNL XDM ExperienceEvent] e [!DNL XDM Individual Profile], rispettivamente).

![](../images/schema-composition/union.png)

Abilitando uno schema da utilizzare con [!DNL Real-time Customer Profile], lo schema verrà incluso nell&#39;unione per quel tipo di classe. [!DNL Profile] fornisce profili affidabili e centralizzati degli attributi del cliente e un account con marca temporale di ogni evento che il cliente ha avuto in qualsiasi sistema integrato con  [!DNL Platform]. [!DNL Profile] utilizza la visualizzazione unione per rappresentare questi dati e fornire una visione olistica di ciascun cliente.

Per ulteriori informazioni sull&#39;utilizzo di [!DNL Profile], vedere la [Panoramica sul profilo cliente in tempo reale](../../profile/home.md).

## Mappatura dei file di dati agli schemi XDM

Tutti i file di dati acquisiti in [!DNL Experience Platform] devono essere conformi alla struttura di uno schema XDM. Per ulteriori informazioni su come formattare i file di dati per conformarsi alle gerarchie XDM (inclusi i file di esempio), consultare il documento sulle [trasformazioni ETL di esempio](../../etl/transformations.md). Per informazioni generali sull&#39;assimilazione di file di dati in [!DNL Experience Platform], vedere la [panoramica sull&#39;inserimento dei batch](../../ingestion/batch-ingestion/overview.md).

## Passaggi successivi

Ora che si conoscono le nozioni di base della composizione dello schema, è possibile iniziare a esplorare e a creare gli schemi utilizzando la [!DNL Schema Registry].

Per esaminare la struttura delle due classi XDM di base e i rispettivi mixin compatibili comunemente utilizzati, consulta la seguente documentazione di riferimento:

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

[!DNL Schema Registry] viene utilizzato per accedere a [!DNL Schema Library] in Adobe Experience Platform e fornisce un&#39;interfaccia utente e RESTful API da cui sono accessibili tutte le risorse libreria disponibili. Il [!DNL Schema Library] contiene risorse del settore definite dal Adobe , risorse del fornitore definite dai partner [!DNL Experience Platform] e classi, mixin, tipi di dati e schemi che sono stati composti da membri dell&#39;organizzazione.

Per iniziare a comporre lo schema utilizzando l&#39;interfaccia utente, seguire l&#39;esercitazione [Editor di schema](../tutorials/create-schema-ui.md) per creare lo schema &quot;Membri fedeltà&quot; menzionato in questo documento.

Per iniziare a utilizzare l&#39;API [!DNL Schema Registry], leggete la [Guida per gli sviluppatori di API del Registro di sistema ](../api/getting-started.md). Dopo aver letto la guida per gli sviluppatori, segui i passaggi descritti nell&#39;esercitazione sulla creazione di uno schema utilizzando l&#39;API del Registro di sistema dello schema](../tutorials/create-schema-api.md).[

## Appendice

La sezione seguente contiene informazioni aggiuntive sui principi della composizione dello schema.

### Oggetti e campi a forma libera {#objects-v-freeform}

Durante la progettazione degli schemi, è necessario tenere in considerazione alcuni fattori chiave nella scelta degli oggetti rispetto ai campi a forma libera:

| Oggetti | Campi per modulo libero |
| --- | --- |
| Aumenta la nidificazione | Minore o nessuna nidificazione |
| Crea raggruppamenti di campi logici | I campi vengono inseriti in posizioni ad hoc |

#### Oggetti

Di seguito sono elencati i pro e i contro dell&#39;uso degli oggetti nei campi a forma libera.

**Pros**:

* Gli oggetti sono utili per creare un raggruppamento logico di determinati campi.
* Gli oggetti organizzano lo schema in modo più strutturato.
* Gli oggetti facilitano indirettamente la creazione di una buona struttura di menu nell’interfaccia utente di Generatore di segmenti. I campi raggruppati nello schema si riflettono direttamente nella struttura di cartelle fornita nell’interfaccia utente di Segment Builder.

**Cons**:

* I campi diventano più nidificati.
* Quando si utilizza [Adobe Experience Platform Query Service](../../query-service/home.md), è necessario fornire stringhe di riferimento più lunghe ai campi di query nidificati negli oggetti.

#### Campi per modulo libero

Di seguito sono elencati i pro e i contro dell&#39;utilizzo di campi a forma libera sugli oggetti.

**Pros**:

* I campi a forma libera vengono creati direttamente sotto l&#39;oggetto principale dello schema (`_tenantId`), aumentando la visibilità.
* Le stringhe di riferimento per i campi a forma libera tendono ad essere più corte quando si utilizza il servizio Query.

**Cons**:

* La posizione dei campi a forma libera all&#39;interno dello schema è ad hoc, ovvero sono visualizzati in ordine alfabetico nell&#39;Editor di schema. In questo modo gli schemi potrebbero risultare meno strutturati e campi gratuiti simili potrebbero risultare molto separati a seconda dei nomi.