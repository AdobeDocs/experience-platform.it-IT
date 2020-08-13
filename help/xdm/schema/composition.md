---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Nozioni di base sulla composizione dello schema
topic: overview
translation-type: tm+mt
source-git-commit: dae86df3ca4fcc9c5951068e905081df29e3b5f2
workflow-type: tm+mt
source-wordcount: '2758'
ht-degree: 0%

---


# Nozioni di base sulla composizione dello schema

Questo documento fornisce un&#39;introduzione agli schemi [!DNL Experience Data Model] (XDM) e ai blocchi costitutivi, ai principi e alle procedure ottimali per la composizione degli schemi da utilizzare in Adobe Experience Platform. Per informazioni generali su XDM e come viene utilizzato all&#39;interno [!DNL Platform], consultate la panoramica [di sistema](../home.md)XDM.

## Informazioni sugli schemi

Uno schema è un insieme di regole che rappresentano e convalidano la struttura e il formato dei dati. A un livello elevato, gli schemi forniscono una definizione astratta di un oggetto reale (ad esempio una persona) e delineano quali dati includere in ciascuna istanza di tale oggetto (ad esempio nome, cognome, compleanno e così via).

Oltre a descrivere la struttura dei dati, gli schemi applicano vincoli e aspettative ai dati in modo che possano essere convalidati man mano che si spostano tra i sistemi. Queste definizioni standard consentono l&#39;interpretazione coerente dei dati, indipendentemente dall&#39;origine, e rimuovono la necessità di una traduzione tra le applicazioni.

[!DNL Experience Platform] mantiene questa normalizzazione semantica attraverso l&#39;uso di schemi. Gli schemi sono il modo standard per descrivere i dati in [!DNL Experience Platform], consentendo a tutti i dati conformi agli schemi di essere riutilizzabili senza conflitti all&#39;interno di un&#39;organizzazione e persino di essere condivisibili tra più organizzazioni.

### Tabelle relazionali e oggetti incorporati

Quando si utilizzano i database relazionali, le best practice prevedono la normalizzazione dei dati o la suddivisione di un&#39;entità in parti distinte che vengono visualizzate in più tabelle. Per leggere i dati nel loro insieme o aggiornare l&#39;entità, le operazioni di lettura e scrittura devono essere eseguite in più singole tabelle utilizzando JOIN.

Utilizzando gli oggetti incorporati, gli schemi XDM possono rappresentare direttamente dati complessi e archiviarli in documenti indipendenti con struttura gerarchica. Uno dei principali vantaggi di questa struttura è che consente di eseguire query sui dati senza dover ricostruire l&#39;entità tramite join costosi a più tabelle denormalizzate.

### Schemi e grandi dati

I sistemi digitali moderni generano una vasta quantità di segnali comportamentali (dati sulle transazioni, registri web, Internet di cose, visualizzazione e così via). Questi grandi dati offrono straordinarie opportunità di ottimizzare le esperienze, ma sono difficili da utilizzare a causa della scala e della varietà dei dati. Al fine di ottenere valore dai dati, la struttura, il formato e le definizioni devono essere standardizzati in modo che possano essere elaborati in modo coerente ed efficiente.

Gli schemi risolvono questo problema consentendo l&#39;integrazione dei dati da più fonti, standardizzati attraverso strutture e definizioni comuni e condivisi tra soluzioni. Questo consente ai processi e ai servizi successivi di rispondere a qualsiasi tipo di domanda posta sui dati, allontanandosi dall&#39;approccio tradizionale alla modellazione dei dati, dove tutte le domande che verranno poste sui dati sono note in anticipo e i dati sono modellati per conformarsi a tali aspettative.

### Flussi di lavoro basati su schema in [!DNL Experience Platform]

La standardizzazione è un concetto chiave dietro [!DNL Experience Platform]. XDM, guidato da  Adobe, è uno sforzo per standardizzare i dati sull&#39;esperienza cliente e definire schemi standard per la gestione dell&#39;esperienza cliente.

L&#39;infrastruttura su cui [!DNL Experience Platform] viene creata, nota come [!DNL XDM System], facilita i flussi di lavoro basati su schemi e include i pattern di utilizzo dei servizi, [!DNL Schema Registry], [!DNL Schema Editor]i metadati dello schema e i relativi pattern. See the [XDM System overview](../home.md) for more information.

## Pianificazione dello schema

Il primo passaggio nella creazione di uno schema consiste nel determinare il concetto, o oggetto reale, che si sta tentando di acquisire all&#39;interno dello schema. Una volta identificato il concetto che si sta cercando di descrivere, è possibile iniziare a pianificare lo schema pensando a cose come il tipo di dati, campi di identità potenziali e come lo schema potrebbe evolvere in futuro.

### Comportamenti dei dati in [!DNL Experience Platform]

I dati destinati all&#39;uso in [!DNL Experience Platform] sono raggruppati in due tipi di comportamento:

* **Record data**: Fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.
* **Dati** serie temporali: Fornisce un&#39;istantanea del sistema al momento in cui un&#39;azione è stata eseguita direttamente o indirettamente da un soggetto del record.

Tutti gli schemi XDM descrivono i dati che possono essere classificati come record o serie temporali. Il comportamento dei dati di uno schema è definito dalla **classe** dello schema, che viene assegnata a uno schema al momento della sua creazione. Le classi XDM sono descritte in dettaglio più avanti in questo documento.

Gli schemi di record e di serie temporali contengono una mappa di identità (`xdm:identityMap`). Questo campo contiene la rappresentazione di identità di un oggetto, ricavata dai campi contrassegnati come &quot;Identità&quot; come descritto nella sezione successiva.

### [!UICONTROL Identity]

Gli schemi vengono utilizzati per assimilare i dati in [!DNL Experience Platform]. Questi dati possono essere utilizzati tra più servizi per creare una singola vista unificata di una singola entità. Pertanto, è importante, quando si pensa agli schemi, pensare alle identità dei clienti e ai campi che possono essere utilizzati per identificare un oggetto, a prescindere da dove i dati provengano.

Per facilitare questo processo, i campi chiave negli schemi possono essere contrassegnati come identità. Al momento dell&#39;inserimento dei dati, i dati contenuti in tali campi vengono inseriti nel campo &quot;[!UICONTROL Identity Graph]&quot; di tale individuo. I dati del grafico sono quindi accessibili da [!DNL Real-time Customer Profile](../../profile/home.md) e da altri [!DNL Experience Platform] servizi per fornire una visualizzazione unita di ogni singolo cliente.

I campi generalmente contrassegnati come &quot;[!UICONTROL Identity]&quot; includono: indirizzo e-mail, numero di telefono, [!DNL Experience Cloud ID (ECID)](https://docs.adobe.com/content/help/it-IT/id-service/using/home.html), ID CRM o altri campi ID univoci. È inoltre necessario considerare eventuali identificatori univoci specifici della propria organizzazione, in quanto possono essere buoni anche &quot;[!UICONTROL Identity]&quot; campi.

È importante considerare le identità dei clienti durante la fase di pianificazione dello schema, in modo da garantire che i dati vengano uniti per creare il profilo più affidabile possibile. Consulta la panoramica su [Adobe Experience Platform Identity Service](../../identity-service/home.md) per ulteriori informazioni su come le informazioni sull&#39;identità possono aiutarti a fornire esperienze digitali ai tuoi clienti.

#### xdm:identityMap

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

Come illustrato nell&#39;esempio precedente, ogni chiave dell&#39; `identityMap` oggetto rappresenta uno spazio dei nomi di identità. Il valore di ciascuna chiave è un array di oggetti che rappresenta i valori di identità (`id`) per il rispettivo namespace. Fare riferimento alla [!DNL Identity Service] documentazione per un [elenco di spazi dei nomi](../../identity-service/troubleshooting-guide.md#standard-namespaces) di identità standard riconosciuti dalle applicazioni  Adobe.

>[!NOTE]
>
>È possibile specificare un valore booleano per specificare se il valore è un&#39;identità primaria (`primary`) anche per ciascun valore di identità. Le identità primarie devono essere impostate solo per gli schemi destinati a essere utilizzati in [!DNL Real-time Customer Profile]. Per ulteriori informazioni, vedere la sezione sugli schemi [](#union) di unione.

### Principi di evoluzione dello schema {#evolution}

Mentre la natura delle esperienze digitali continua ad evolversi, devono evolversi anche gli schemi utilizzati per rappresentarle. Uno schema ben progettato è quindi in grado di adattarsi ed evolversi in base alle esigenze, senza causare modifiche distruttive alle versioni precedenti dello schema.

Poiché il mantenimento della compatibilità con le versioni precedenti è fondamentale per l&#39;evoluzione dello schema, [!DNL Experience Platform] applica un principio di controllo delle versioni puramente additivo, in modo da garantire che qualsiasi revisione dello schema produca solo aggiornamenti e modifiche non distruttivi. In altre parole, le modifiche **di interruzione non sono supportate.**

| Modifiche supportate | Interruzione delle modifiche (non supportata) |
|------------------------------------|---------------------------------|
| <ul><li>Aggiunta di nuovi campi a uno schema esistente</li><li>Impostazione di un campo obbligatorio come facoltativo</li></ul> | <ul><li>Rimozione di campi definiti in precedenza</li><li>Introduzione di nuovi campi obbligatori</li><li>Ridenominazione o ridefinizione di campi esistenti</li><li>Rimozione o limitazione di valori di campo supportati in precedenza</li><li>Spostamento degli attributi in una diversa posizione nella struttura</li></ul> |

>[!NOTE]
>
>Se uno schema non è ancora stato utilizzato per assimilare i dati in [!DNL Experience Platform], è possibile introdurre una modifica di interruzione nello schema. Tuttavia, una volta utilizzato in [!DNL Platform], lo schema deve rispettare i criteri di controllo delle versioni aggiuntivi.

### Schemi e acquisizione dei dati

Per acquisire i dati in [!DNL Experience Platform], è necessario creare prima un set di dati. I set di dati sono gli elementi costitutivi della trasformazione e del tracciamento dei dati per [!DNL Catalog Service](../../catalog/home.md)e generalmente rappresentano tabelle o file contenenti dati acquisiti. Tutti i set di dati si basano sugli schemi XDM esistenti, che forniscono vincoli per ciò che i dati acquisiti devono contenere e per come dovrebbero essere strutturati. Per ulteriori informazioni, consulta la panoramica su [Adobe Experience Platform Data Ingestion](../../ingestion/home.md) .

## Creazione di blocchi di uno schema

[!DNL Experience Platform] utilizza un approccio di composizione in cui i blocchi di generazione standard vengono combinati per creare schemi. Questo approccio promuove la riutilizzabilità dei componenti esistenti e favorisce la standardizzazione in tutto il settore per supportare schemi e componenti dei fornitori in [!DNL Platform].

Gli schemi sono composti utilizzando la seguente formula:

**Classe + Mixin&amp;ast; = Schema XDM**

&amp;ast;Uno schema è composto da una classe e da _zero o più_ mixin. Ciò significa che è possibile comporre uno schema di set di dati senza utilizzare i mixin.

### Classe

La composizione di uno schema inizia con l&#39;assegnazione di una classe. Le classi definiscono gli aspetti comportamentali dei dati che lo schema conterrà (record o serie temporali). Inoltre, le classi descrivono il minor numero di proprietà comuni che tutti gli schemi basati su tale classe dovrebbero includere e forniscono un modo per l&#39;unione di più set di dati compatibili.

Una classe determina inoltre quali mixin saranno utilizzabili nello schema. Questo viene descritto più dettagliatamente nella sezione [mixin](#mixin) che segue.

Esistono classi standard fornite con ogni integrazione di classi [!DNL Experience Platform], note come &quot;Industria&quot;. Le classi di settore sono standard di settore generalmente accettati che si applicano a un&#39;ampia serie di casi d&#39;uso. Esempi di classi Industry includono le [!DNL XDM Individual Profile] classi e [!DNL XDM ExperienceEvent] le classi fornite dal Adobe .

[!DNL Experience Platform] consente anche classi &quot;Fornitore&quot;, che sono classi definite dai [!DNL Experience Platform] partner e rese disponibili a tutti i clienti che utilizzano il servizio o l&#39;applicazione del fornitore all&#39;interno [!DNL Platform].

Esistono anche classi utilizzate per descrivere casi di utilizzo più specifici per singole organizzazioni all&#39;interno delle classi [!DNL Platform], denominate &quot;Customer&quot;. Le classi cliente sono definite da un&#39;organizzazione quando non sono disponibili classi Settore o Fornitore per descrivere un caso di utilizzo univoco.

Ad esempio, uno schema che rappresenta i membri di un programma Fedeltà descrive i dati dei record relativi a un singolo e può quindi essere basato sulla [!DNL XDM Individual Profile] classe, una classe Industry standard definita da  Adobe.

### Mixin {#mixin}

Un mixin è un componente riutilizzabile che definisce uno o più campi che implementano determinate funzioni come i dati personali, le preferenze alberghiere o l&#39;indirizzo. Le mixine sono destinate ad essere incluse come parte di uno schema che implementa una classe compatibile.

Le combinazioni definiscono le classi con cui sono compatibili in base al comportamento dei dati che rappresentano (serie di record o temporali). Ciò significa che non tutti i mixin sono disponibili per l&#39;uso con tutte le classi.

I mixin hanno lo stesso ambito e la stessa definizione delle classi: esistono mixin di settore, mixin di fornitori e mixin di clienti definiti dalle singole organizzazioni che utilizzano [!DNL Platform]. [!DNL Experience Platform] include molti mixer standard di settore, consentendo al contempo ai fornitori di definire mixin per i propri utenti e ai singoli utenti di definire mixin base ai propri concetti specifici.

Ad esempio, per acquisire dettagli quali &quot;[!UICONTROL First Name]&quot; e &quot;[!UICONTROL Home Address]&quot; per lo schema &quot;[!UICONTROL Loyalty Members]&quot;, potreste utilizzare mixin standard che definiscono questi concetti comuni. Tuttavia, i concetti specifici per casi di utilizzo meno comuni (come &quot;[!UICONTROL Loyalty Program Level]&quot;) spesso non hanno un mixin predefinito. In questo caso, per acquisire queste informazioni dovete definire un mixin personalizzato.

Tenere presente che gli schemi sono composti da &quot;zero o più&quot; mixin, pertanto è possibile comporre uno schema valido senza utilizzare alcun mixin.

### Data type {#data-type}

I tipi di dati sono utilizzati come tipi di campi di riferimento in classi o schemi allo stesso modo dei campi letterali di base. La differenza principale sta nel fatto che i tipi di dati possono definire più sottocampi. Analogamente a un mixin, un tipo di dati consente l&#39;uso coerente di una struttura multi-campo, ma offre maggiore flessibilità rispetto a un mixin, perché un tipo di dati può essere incluso in qualsiasi punto dello schema aggiungendo il tipo di dati &quot;tipo&quot; di un campo.

[!DNL Experience Platform] fornisce una serie di tipi di dati comuni come parte del [!DNL Schema Registry] supporto all&#39;uso di pattern standard per la descrizione di strutture di dati comuni. Questo è spiegato più dettagliatamente nelle [!DNL Schema Registry] esercitazioni, dove diventerà più chiaro man mano che si passano i passaggi per definire i tipi di dati.

### Campo

Un campo è il blocco predefinito più basilare di uno schema. I campi forniscono vincoli relativi al tipo di dati che possono contenere definendo un tipo di dati specifico. Questi tipi di dati di base definiscono un singolo campo, mentre i tipi [di](#data-type) dati precedentemente indicati consentono di definire più sottocampi e di riutilizzare la stessa struttura multi-campo in vari schemi. Pertanto, oltre a definire il &quot;tipo di dati&quot; di un campo come uno dei tipi di dati definiti nel registro, [!DNL Experience Platform] supporta tipi scalari di base come:

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

* [!DNL Real-time Customer Profile](../../profile/home.md)
* [!DNL Identity Service](../../identity-service/home.md)
* [!DNL Segmentation](../../segmentation/home.md)
* [!DNL Query Service](../../query-service/home.md)
* [!DNL Data Science Workspace](../../data-science-workspace/home.md)

Prima di creare uno schema da utilizzare nei servizi a valle, consultare la documentazione appropriata per tali servizi al fine di comprendere meglio i requisiti di campo e i vincoli per le operazioni di dati a cui lo schema è destinato.

### Campi XDM

Oltre ai campi di base e alla possibilità di definire i propri tipi di dati, XDM fornisce un set standard di campi e tipi di dati che vengono implicitamente compresi dai [!DNL Experience Platform] servizi e che assicurano una maggiore coerenza quando vengono utilizzati tra [!DNL Platform] i componenti.

Questi campi, come &quot;Nome&quot; e &quot;Indirizzo e-mail&quot; contengono connotazioni aggiunte oltre i tipi di campi scalari di base, a indicare [!DNL Platform] che tutti i campi che condividono lo stesso tipo di dati XDM si comportano allo stesso modo. Questo comportamento può essere considerato coerente, indipendentemente da dove provengano i dati, o in quale [!DNL Platform] servizio vengono utilizzati i dati.

Per un elenco completo dei campi XDM disponibili, consultate il dizionario [dei campi](field-dictionary.md) XDM. Si consiglia di utilizzare i campi e i tipi di dati XDM laddove possibile per supportare coerenza e standardizzazione in tutti [!DNL Experience Platform].

## Esempio di composizione

Gli schemi rappresentano il formato e la struttura dei dati che verranno assimilati [!DNL Platform]e creati utilizzando un modello di composizione. Come già detto, questi schemi sono composti da una classe e da zero o più mixin compatibili con tale classe.

Ad esempio, uno schema che descrive gli acquisti effettuati in un negozio al dettaglio potrebbe essere denominato &quot;[!UICONTROL Store Transactions]&quot;. Lo schema implementa la [!DNL XDM ExperienceEvent] classe combinata con il [!UICONTROL Commerce] mixin standard e un [!UICONTROL Product Info] mixin definito dall&#39;utente.

Un altro schema che tiene traccia del traffico del sito Web potrebbe essere denominato &quot;[!UICONTROL Web Visits]&quot;. Implementa anche la [!DNL XDM ExperienceEvent] classe, ma questa volta combina il [!UICONTROL Web] mixin standard.

Il diagramma seguente mostra questi schemi e i campi che contribuiscono a ciascun mixin. Contiene inoltre due schemi basati sulla [!DNL XDM Individual Profile] classe, incluso lo schema &quot;[!UICONTROL Loyalty Members]&quot; menzionato in precedenza in questa guida.

![](../images/schema-composition/composition.png)

### Unione {#union}

Anche se [!DNL Experience Platform] consente di comporre schemi per casi di utilizzo particolari, è anche possibile visualizzare una &quot;unione&quot; di schemi per un tipo di classe specifico. Il diagramma precedente mostra due schemi basati sulla classe ExperienceEvent XDM e due schemi basati sulla [!DNL XDM Individual Profile] classe. L&#39;unione, come illustrato di seguito, aggrega i campi di tutti gli schemi che condividono la stessa classe ([!DNL XDM ExperienceEvent] e, rispettivamente, [!DNL XDM Individual Profile]).

![](../images/schema-composition/union.png)

Abilitando uno schema da utilizzare con [!DNL Real-time Customer Profile], esso sarà incluso nell&#39;unione per quel tipo di classe. [!DNL Profile] fornisce profili affidabili e centralizzati degli attributi del cliente e un account con marca temporale di ogni evento che il cliente ha avuto in qualsiasi sistema integrato con [!DNL Platform]. [!DNL Profile] utilizza la visualizzazione unione per rappresentare questi dati e fornire una visione olistica di ciascun cliente.

Per ulteriori informazioni sull&#39;utilizzo [!DNL Profile], consulta la panoramica [Profilo cliente](../../profile/home.md)in tempo reale.

## Mappatura dei file di dati agli schemi XDM

Tutti i file di dati acquisiti [!DNL Experience Platform] devono essere conformi alla struttura di uno schema XDM. Per ulteriori informazioni su come formattare i file di dati per conformarsi alle gerarchie XDM (inclusi i file di esempio), consultate il documento sulle trasformazioni [ETL di](../../etl/transformations.md)esempio. Per informazioni generali sull’assimilazione di file di dati in [!DNL Experience Platform], consultate la panoramica [sull’assimilazione](../../ingestion/batch-ingestion/overview.md)batch.

## Passaggi successivi

Ora che si conoscono le nozioni di base della composizione dello schema, è possibile iniziare a creare schemi utilizzando l&#39; [!DNL Schema Registry].

L&#39; [!DNL Schema Registry] interfaccia viene utilizzata per accedere all&#39; [!DNL Schema Library] interno di Adobe Experience Platform e fornisce un&#39;interfaccia utente e un&#39;API RESTful da cui sono accessibili tutte le risorse libreria disponibili. Il [!DNL Schema Library] contiene risorse del settore definite da  Adobe, risorse del fornitore definite dai [!DNL Experience Platform] partner e classi, mixin, tipi di dati e schemi che sono stati composti da membri dell&#39;organizzazione.

Per iniziare a comporre lo schema utilizzando l&#39;interfaccia utente, seguire l&#39;esercitazione [Editor](../tutorials/create-schema-ui.md) schema per creare lo schema &quot;Membri fedeltà&quot; menzionato in questo documento.

Per iniziare a utilizzare l&#39; [!DNL Schema Registry] API, iniziare leggendo la guida per lo sviluppatore di API del Registro di [schema](../api/getting-started.md). Dopo aver letto la guida per gli sviluppatori, segui i passaggi descritti nell&#39;esercitazione sulla [creazione di uno schema tramite l&#39;API](../tutorials/create-schema-api.md)del Registro di sistema dello schema.