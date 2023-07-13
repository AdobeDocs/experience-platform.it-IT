---
keywords: Experience Platform;home;argomenti popolari;schema;schema;enum;mixin;gruppo di campi;gruppi di campi;mixin;tipo di dati;tipi di dati;tipi di dati;tipo di dati;identità primaria;identità primaria;profilo individuale XDM;campi XDM;enum datatype;Experience event;XDM ExperienceEvent;experienceEvent;experienceevent;XDM Experienceevent;schema design;classe;classi;classi;classi;tipo di dati;tipo di dati;tipo di dati;schemi;schema;mappa identità;mappa identità;mappa identità;schema;schema;mappa schema;mappa;schema;mappa;unione unione
solution: Experience Platform
title: Nozioni di base sulla composizione dello schema
description: Questo documento fornisce un’introduzione agli schemi Experience Data Model (XDM) e ai blocchi predefiniti, ai principi e alle best practice per la composizione degli schemi da utilizzare in Adobe Experience Platform.
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: 4ff003b8f4e98fa7af7f12271aa990c8e5f49f14
workflow-type: tm+mt
source-wordcount: '4140'
ht-degree: 6%

---

# Nozioni di base sulla composizione dello schema

Questo documento fornisce un’introduzione a [!DNL Experience Data Model] Schemi (XDM) e gli elementi di base, i principi e le best practice per la composizione degli schemi da utilizzare in Adobe Experience Platform. Per informazioni generali su XDM e su come viene utilizzato in [!DNL Platform], vedere [Panoramica del sistema XDM](../home.md).

## Informazioni sugli schemi

Uno schema è un set di regole che rappresentano e convalidano la struttura e il formato dei dati. A un livello avanzato, gli schemi forniscono una definizione astratta di un oggetto reale (ad esempio una persona) e delineano quali dati includere in ogni istanza di tale oggetto (ad esempio nome, cognome, compleanno e così via).

Oltre a descrivere la struttura dei dati, gli schemi applicano vincoli e aspettative ai dati in modo che possano essere convalidati durante gli spostamenti tra sistemi diversi. Queste definizioni standard consentono di interpretare i dati in modo coerente, indipendentemente dall’origine, ed eliminano la necessità di traduzione tra le applicazioni.

[!DNL Experience Platform] mantiene questa normalizzazione semantica utilizzando gli schemi. Gli schemi sono il modo standard per descrivere i dati in [!DNL Experience Platform], che consente di riutilizzare in un’organizzazione tutti i dati conformi agli schemi senza conflitti, o anche di condividerli tra più organizzazioni.

Gli schemi XDM sono ideali per memorizzare grandi quantità di dati complessi in un formato autonomo. Consulta le sezioni relative a [oggetti incorporati](#embedded) e [big data](#big-data) nell’appendice di questo documento per ulteriori informazioni su come XDM esegue questa operazione.

### Flussi di lavoro basati su schema in [!DNL Experience Platform]

La standardizzazione è un concetto chiave [!DNL Experience Platform]. XDM, guidato da Adobe, è un tentativo di standardizzare i dati sull’esperienza del cliente e definire schemi standard per la gestione della customer experience.

L&#39;infrastruttura su cui [!DNL Experience Platform] è stato generato, noto come [!DNL XDM System], semplifica i flussi di lavoro basati su schema e include [!DNL Schema Registry], [!DNL Schema Editor], metadati di schema e modelli di consumo del servizio. Consulta la [Panoramica del sistema XDM](../home.md) per ulteriori informazioni.

Esistono diversi vantaggi chiave per sfruttare gli schemi in [!DNL Experience Platform]. In primo luogo, gli schemi consentono una migliore governance dei dati e la loro minimizzazione, il che è particolarmente importante con le normative sulla privacy. In secondo luogo, la creazione di schemi con i componenti standard di Adobe consente di ottenere informazioni predefinite e l’utilizzo di servizi AI/ML con personalizzazioni minime. Infine, gli schemi forniscono l’infrastruttura necessaria per condividere informazioni approfondite sui dati e orchestrare in modo efficiente.

## Pianificazione dello schema

Il primo passaggio nella creazione di uno schema consiste nel determinare il concetto, o oggetto reale, che si sta tentando di acquisire all’interno dello schema. Dopo aver identificato il concetto che si sta tentando di descrivere, è possibile iniziare a pianificare lo schema pensando a elementi quali il tipo di dati, i potenziali campi di identità e l&#39;evoluzione futura dello schema.

### Comportamenti dei dati in [!DNL Experience Platform]

Dati destinati all’utilizzo in [!DNL Experience Platform] è raggruppato in due tipi di comportamento:

* **Registra dati**: fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.
* **Dati delle serie temporali**: fornisce un’istantanea del sistema nel momento in cui un oggetto record ha eseguito un’azione, direttamente o indirettamente.

Tutti gli schemi XDM descrivono dati che possono essere classificati come record o serie temporali. Il comportamento dei dati di uno schema è definito dalla classe dello schema, che viene assegnata a uno schema al momento della creazione. Le classi XDM sono descritte più avanti in questo documento.

Sia gli schemi di record che quelli di serie temporali contengono una mappa di identità (`xdm:identityMap`). Questo campo contiene la rappresentazione dell’identità di un soggetto, tratta dai campi contrassegnati come &quot;Identità&quot; come descritto nella sezione successiva.

### [!UICONTROL Identità] {#identity}

>[!CONTEXTUALHELP]
>id="platform_schemas_identities"
>title="Identità negli schemi"
>abstract="Le identità sono campi chiave di uno schema che possono essere utilizzati per identificare un soggetto, ad esempio un indirizzo e-mail o un ID di marketing. Questi campi vengono utilizzati per creare il grafo delle identità per ogni singolo utente e generare profili cliente. Per ulteriori informazioni sulle identità negli schemi, consulta la documentazione."

Gli schemi vengono utilizzati per acquisire i dati in [!DNL Experience Platform]. Questi dati possono essere utilizzati in più servizi per creare una singola vista unificata di una singola entità. Pertanto, è importante, quando si pensa agli schemi, pensare alle identità dei clienti e ai campi che possono essere utilizzati per identificare un soggetto indipendentemente da dove possono provenire i dati.

Per facilitare questo processo, i campi chiave all’interno degli schemi possono essere contrassegnati come identità. Al momento dell’acquisizione dei dati, i dati contenuti in tali campi vengono inseriti nel file &quot;[!UICONTROL Grafico delle identità]&quot; per quell’individuo. È quindi possibile accedere ai dati del grafico tramite [[!DNL Real-Time Customer Profile]](../../profile/home.md) e altro [!DNL Experience Platform] per fornire una visualizzazione combinata di ogni singolo cliente.

Campi comunemente contrassegnati come &quot;[!UICONTROL Identità]&quot; include: indirizzo e-mail, numero di telefono, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=it), ID CRM o altri campi ID univoci. Dovresti anche considerare eventuali identificatori univoci specifici per la tua organizzazione, in quanto potrebbero essere validi &quot;.[!UICONTROL Identità]&quot;.

È importante considerare le identità dei clienti durante la fase di pianificazione dello schema, al fine di garantire che i dati vengano raccolti per creare il profilo più solido possibile. Consulta la panoramica su [Servizio Adobe Experience Platform Identity](../../identity-service/home.md) per ulteriori informazioni su come le informazioni sulle identità possono aiutarti a fornire esperienze digitali ai tuoi clienti.

Esistono due modi per inviare dati di identità a Platform:

1. Aggiunta di descrittori di identità ai singoli campi tramite [Interfaccia utente dell’editor schema](../ui/fields/identity.md) o utilizzando [API del registro dello schema](../api/descriptors.md#create)
1. Utilizzo di un [`identityMap` campo](#identityMap)

#### `identityMap` {#identityMap}

`identityMap` è un campo di tipo mappa che descrive i vari valori di identità di un individuo, insieme ai relativi spazi dei nomi associati. Questo campo può essere utilizzato per fornire informazioni sull’identità per gli schemi, anziché definire valori di identità all’interno della struttura dello schema stesso.

L&#39;inconveniente principale dell&#39;utilizzo `identityMap` è che le identità diventano incorporate nei dati e diventano meno visibili di conseguenza. Se acquisisci dati non elaborati, devi invece definire singoli campi di identità all’interno dell’effettiva struttura dello schema.

>[!NOTE]
>
>Uno schema che utilizza `identityMap` può essere utilizzato come schema di origine in una relazione, ma non come schema di riferimento. Questo perché tutti gli schemi di riferimento devono avere un’identità visibile che può essere mappata in un campo di riferimento all’interno dello schema di origine. Fai riferimento alla guida dell’interfaccia utente su [relazioni](../tutorials/relationship-ui.md) per ulteriori informazioni sui requisiti degli schemi di origine e di riferimento.

Tuttavia, le mappe di identità possono essere particolarmente utili se si inseriscono dati da origini che memorizzano le identità (ad esempio [!DNL Airship] o Adobe Audience Manager), o quando è presente un numero variabile di identità per uno schema. Inoltre, le mappe di identità sono necessarie se utilizzi il [SDK di Adobe Experience Platform Mobile](https://aep-sdks.gitbook.io/docs/).

Di seguito è riportato un esempio di mappa di identità semplice:

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": true
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
  "CRMID": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": false
    }
  ]
}
```

Come mostrato nell’esempio precedente, ogni chiave nel `identityMap` l&#39;oggetto rappresenta uno spazio dei nomi di identità. Il valore di ogni chiave è una matrice di oggetti, che rappresenta i valori di identità (`id`) per il rispettivo namespace. Consulta la sezione [!DNL Identity Service] documentazione per un [elenco degli spazi dei nomi di identità standard](../../identity-service/troubleshooting-guide.md#standard-namespaces) riconosciuto dalle applicazioni Adobe.

>[!NOTE]
>
>Valore booleano per specificare se si tratta di un&#39;identità primaria (`primary`) può essere fornito anche per ogni valore di identità. È necessario impostare le identità primarie solo per gli schemi da utilizzare in [!DNL Real-Time Customer Profile]. Consulta la sezione su [schemi di unione](#union) per ulteriori informazioni.

### Principi di evoluzione dello schema {#evolution}

Con l’evolversi della natura delle esperienze digitali, devono evolversi anche gli schemi utilizzati per rappresentarle. Uno schema ben progettato è quindi in grado di adattarsi ed evolvere secondo necessità, senza causare modifiche distruttive alle versioni precedenti dello schema.

Poiché mantenere la compatibilità con le versioni precedenti è fondamentale per l’evoluzione dello schema, [!DNL Experience Platform] applica un principio di controllo delle versioni puramente additivo. Questo principio garantisce che eventuali revisioni allo schema risultino solo in aggiornamenti e modifiche non distruttivi. In altre parole, **le modifiche di interruzione non sono supportate.**

>[!NOTE]
>
>Se non è ancora stato utilizzato uno schema per acquisire i dati in [!DNL Experience Platform] e non è stato abilitato per l’utilizzo in Real-Time Customer Profile; puoi introdurre una modifica che interrompe il ciclo di vita di tale schema. Tuttavia, dopo aver utilizzato lo schema in [!DNL Platform], deve rispettare i criteri di controllo delle versioni aggiuntivi.

La tabella seguente suddivide le modifiche supportate durante la modifica di schemi, gruppi di campi e tipi di dati:

| Modifiche supportate | Modifiche che causano interruzioni (non supportato) |
| --- | --- |
| <ul><li>Aggiunta di nuovi campi alla risorsa</li><li>Impostazione di un campo obbligatorio come facoltativo</li><li>Introduzione di nuovi campi obbligatori*</li><li>Modifica del nome visualizzato e della descrizione della risorsa</li><li>Abilitazione dello schema per la partecipazione al profilo</li></ul> | <ul><li>Rimozione dei campi definiti in precedenza</li><li>Ridenominazione o ridefinizione di campi esistenti</li><li>Rimozione o limitazione dei valori di campo precedentemente supportati</li><li>Spostamento dei campi esistenti in una posizione diversa nella struttura</li><li>Eliminazione dello schema</li><li>Disabilitazione dello schema dalla partecipazione al profilo</li></ul> |

\**Consulta la sezione seguente per considerazioni importanti su [impostazione di nuovi campi obbligatori](#post-ingestion-required-fields).*

### Campi obbligatori

I singoli campi dello schema possono essere [contrassegnato come obbligatorio](../ui/fields/required.md), il che significa che qualsiasi record acquisito deve contenere dati in tali campi per superare la convalida. Ad esempio, l’impostazione obbligatoria del campo di identità principale di uno schema può garantire che tutti i record acquisiti partecipino a Real-Time Customer Profile, mentre l’impostazione obbligatoria di un campo di marca temporale assicura che tutti gli eventi di serie temporali siano conservati in modo cronologico.

>[!IMPORTANT]
>
>A prescindere dal fatto che un campo schema sia obbligatorio o meno, Platform non accetta `null` o valori vuoti per qualsiasi campo acquisito. Se non è presente alcun valore per un particolare campo in un record o in un evento, la chiave per tale campo deve essere esclusa dal payload di acquisizione.

#### Impostazione dei campi come richiesto dopo l’acquisizione {#post-ingestion-required-fields}

Se un campo è stato utilizzato per acquisire i dati e non è stato originariamente impostato come richiesto, è possibile che per alcuni record sia presente un valore Null. Se imposti questo campo come obbligatorio dopo l’acquisizione, tutti i record futuri devono contenere un valore per questo campo, anche se i record storici possono essere nulli.

Quando imposti un campo precedentemente facoltativo come richiesto, tieni presente quanto segue:

1. Se esegui una query sui dati storici e scrivi i risultati in un nuovo set di dati, alcune righe non riusciranno perché contengono valori nulli per il campo richiesto.
1. Se il campo partecipa a [Profilo cliente in tempo reale](../../profile/home.md) e i dati vengono esportati prima di impostarli come richiesto, per alcuni profili potrebbero essere nulli.
1. Puoi utilizzare l’API Schema Registry per visualizzare un registro delle modifiche con marca temporale per tutte le risorse XDM in Platform, compresi i nuovi campi obbligatori. Consulta la guida sulla [endpoint del registro di controllo](../api/audit-log.md) per ulteriori informazioni.

### Schemi e acquisizione di dati

Per acquisire i dati in [!DNL Experience Platform], è prima necessario creare un set di dati. I set di dati sono i blocchi predefiniti per la trasformazione e il tracciamento dei dati per [[!DNL Catalog Service]](../../catalog/home.md)e generalmente rappresentano tabelle o file che contengono dati acquisiti. Tutti i set di dati si basano su schemi XDM esistenti, che forniscono vincoli per ciò che i dati acquisiti devono contenere e per come devono essere strutturati. Consulta la panoramica su [Acquisizione dei dati Adobe Experience Platform](../../ingestion/home.md) per ulteriori informazioni.

## Blocchi predefiniti di uno schema

[!DNL Experience Platform] utilizza un approccio di composizione in cui i blocchi predefiniti standard vengono combinati per creare schemi. Questo approccio promuove la riutilizzabilità dei componenti esistenti e favorisce la standardizzazione nel settore per supportare schemi e componenti dei fornitori in [!DNL Platform].

Gli schemi vengono composti utilizzando la seguente formula:

**Gruppo campi classe + schema; = schema XDM**

&amp;ast;Uno schema è composto da una classe e da zero o più gruppi di campi dello schema. Ciò significa che è possibile comporre uno schema di set di dati senza utilizzare affatto i gruppi di campi.

### Classe {#class}

>[!CONTEXTUALHELP]
>id="platform_schemas_class"
>title="Classe"
>abstract="Ogni schema è basato su una singola classe. La classe definisce il comportamento dello schema e le proprietà comuni che tutti gli schemi basati su tale classe devono contenere. Per ulteriori informazioni sul ruolo delle classi nella composizione dello schema, consulta la documentazione."

La composizione di uno schema inizia assegnando una classe. Le classi definiscono gli aspetti comportamentali dei dati che lo schema conterrà (record o serie temporali). Inoltre, le classi descrivono il minor numero di proprietà comuni che tutti gli schemi basati su tale classe dovrebbero includere e forniscono un modo per unire più set di dati compatibili.

La classe di uno schema determina quali gruppi di campi saranno idonei per l’utilizzo in tale schema. Questo argomento è trattato più dettagliatamente nella [sezione successiva](#field-group).

Adobe fornisce diverse classi XDM standard (&quot;core&quot;). Due di queste classi, [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent], sono necessari per quasi tutti i processi della piattaforma a valle. Oltre a queste classi principali, puoi anche creare classi personalizzate per descrivere casi d’uso più specifici per la tua organizzazione. Le classi personalizzate vengono definite da un’organizzazione quando non sono disponibili classi core definite da Adobi per descrivere un caso d’uso univoco.

La schermata seguente illustra come le classi sono rappresentate nell’interfaccia utente di Platform. Poiché lo schema di esempio visualizzato non contiene gruppi di campi, tutti i campi visualizzati vengono forniti dalla classe dello schema ([!UICONTROL Profilo individuale XDM]).

![](../images/schema-composition/class.png)

Per l’elenco più aggiornato delle classi XDM standard disponibili, consulta [archivio XDM ufficiale](https://github.com/adobe/xdm/tree/master/components/classes). In alternativa, consulta la guida su [esplorazione dei componenti XDM](../ui/explore.md) se preferisci visualizzare le risorse nell’interfaccia utente.

### Gruppo di campi {#field-group}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup"
>title="Gruppo di campi"
>abstract="I gruppi di campi sono componenti riutilizzabili che consentono di estendere gli schemi con attributi aggiuntivi. La maggior parte dei gruppi di campi è compatibile solo con determinate classi. È possibile utilizzare i gruppi di campi standard definiti da Adobe oppure definire manualmente gruppi di campi personalizzati. Per ulteriori informazioni sul ruolo dei gruppi di campi nella composizione dello schema, consulta la documentazione."

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_requiredFieldgroup"
>title="Gruppo di campi richiesto"
>abstract="Questo gruppo di campi è richiesto dall’origine in uso. Per questo motivo, non è possibile eliminarlo dallo schema."

Un gruppo di campi è un componente riutilizzabile che definisce uno o più campi che implementano determinate funzioni come i dati personali, le preferenze di hotel o l’indirizzo. I gruppi di campi sono destinati a essere inclusi come parte di uno schema che implementa una classe compatibile.

I gruppi di campi definiscono con quali classi sono compatibili in base al comportamento dei dati che rappresentano (record o serie temporali). Ciò significa che non tutti i gruppi di campi sono disponibili per l&#39;utilizzo con tutte le classi.

[!DNL Experience Platform] include molti gruppi di campi di Adobe standard, consentendo ai fornitori di definire gruppi di campi per i propri utenti e ai singoli utenti di definire gruppi di campi per concetti specifici.

Ad esempio, per acquisire dettagli quali &quot;[!UICONTROL Nome]&quot; e &quot;[!UICONTROL Indirizzo abitazione]&quot; per il tuo &quot;[!UICONTROL Membri fedeltà]&quot;, è possibile utilizzare gruppi di campi standard che definiscono tali concetti comuni. Tuttavia, concetti più specifici dell’organizzazione (ad esempio dettagli del programma fedeltà personalizzato o attributi di prodotto) che potrebbero non essere coperti dai gruppi di campi standard. In questo caso, è necessario definire un proprio gruppo di campi per acquisire queste informazioni.

>[!NOTE]
>
>Si consiglia vivamente di utilizzare gruppi di campi standard ogni volta che è possibile negli schemi, in quanto questi campi sono compresi implicitamente da [!DNL Experience Platform] e forniscono maggiore coerenza quando vengono utilizzati in [!DNL Platform] componenti.
>
>I campi forniti dai componenti standard (come &quot;Nome&quot; e &quot;Indirizzo e-mail&quot;) contengono connotazioni aggiunte oltre i tipi di campi scalari di base, che indicano [!DNL Platform] che tutti i campi che condividono lo stesso tipo di dati si comportano allo stesso modo. È affidabile che questo comportamento sia coerente indipendentemente da dove provengono i dati o in cui [!DNL Platform] servizio in cui vengono utilizzati i dati.

Gli schemi sono composti da &quot;zero o più&quot; gruppi di campi, pertanto puoi comporre uno schema valido senza utilizzare alcun gruppo di campi.

La schermata seguente illustra come i gruppi di campi sono rappresentati nell’interfaccia utente di Platform. Un singolo gruppo di campi ([!UICONTROL Dettagli demografici]) viene aggiunto a uno schema in questo esempio, che fornisce un raggruppamento di campi alla struttura dello schema.

![](../images/schema-composition/field-group.png)

Per l’elenco più aggiornato dei gruppi di campi XDM standard disponibili, fai riferimento a [archivio XDM ufficiale](https://github.com/adobe/xdm/tree/master/components/fieldgroups). In alternativa, consulta la guida su [esplorazione dei componenti XDM](../ui/explore.md) se preferisci visualizzare le risorse nell’interfaccia utente.

### Tipo di dati {#data-type}

I tipi di dati vengono utilizzati come tipi di campi di riferimento nelle classi o negli schemi allo stesso modo dei campi letterali di base. La differenza chiave è che i tipi di dati possono definire più sottocampi. Possono definire più sottocampi nello stesso modo dei gruppi di campi, ma la differenza chiave è che i tipi di dati possono essere inclusi ovunque in uno schema aggiungendolo come &quot;tipo di dati&quot; di un campo. Mentre i gruppi di campi sono compatibili solo con determinate classi, i tipi di dati possono essere inclusi in qualsiasi classe padre o gruppo di campi.

[!DNL Experience Platform] fornisce una serie di tipi di dati comuni come parte del [!DNL Schema Registry] sostenere l’uso di modelli standard per descrivere strutture di dati comuni. Questo è spiegato più dettagliatamente nel [!DNL Schema Registry] esercitazioni, dove diventerà più chiaro mentre segui i passaggi per definire i tipi di dati.

La schermata seguente illustra come i tipi di dati vengono rappresentati nell’interfaccia utente di Platform. Uno dei campi forniti da [!UICONTROL Dettagli demografici] il gruppo di campi utilizza il carattere &quot;[!UICONTROL Oggetto]&quot;tipo di dati, come indicato dal testo che segue il carattere barra verticale (`|`) accanto al nome del campo. Questo particolare tipo di dati fornisce diversi sottocampi che si riferiscono al nome di una singola persona, un costrutto che può essere riutilizzato per altri campi in cui è necessario acquisire il nome di una persona.

![](../images/schema-composition/data-type.png)

Per l’elenco più aggiornato dei tipi di dati XDM standard disponibili, consulta [archivio XDM ufficiale](https://github.com/adobe/xdm/tree/master/components/datatypes). In alternativa, consulta la guida su [esplorazione dei componenti XDM](../ui/explore.md) se preferisci visualizzare le risorse nell’interfaccia utente.

### Campo

Un campo è il blocco predefinito più semplice di uno schema. I campi forniscono vincoli relativi al tipo di dati che possono contenere definendo un tipo di dati specifico. Questi tipi di dati di base definiscono un singolo campo, mentre [tipi di dati](#data-type) precedentemente menzionato consente di definire più sottocampi e di riutilizzare la stessa struttura a più campi in vari schemi. Quindi, oltre a definire il &quot;tipo di dati&quot; di un campo come uno dei tipi di dati definiti nel Registro di sistema, [!DNL Experience Platform] supporta tipi scalari di base, ad esempio:

* Stringa
* Intero
* Doppio
* Booleano
* Array
* Oggetto

>[!TIP]
>
>Consulta la [appendice](#objects-v-freeform) per informazioni sui pro e i contro dell’utilizzo di campi in formato libero su campi di tipo oggetto.

Gli intervalli validi di questi tipi scalari possono essere ulteriormente vincolati a determinati pattern, formati, minimi/massimi o valori predefiniti. Utilizzando questi vincoli, è possibile rappresentare un&#39;ampia gamma di tipi di campo più specifici, tra cui:

* Enum
* Lungo
* Breve
* Byte
* Data
* Data-ora
* Mappa

>[!NOTE]
>
>Il tipo di campo &quot;map&quot; consente di usare dati di coppia chiave-valore, inclusi più valori per una singola chiave. Le mappe si trovano nelle classi XDM standard e nei gruppi di campi, ma puoi anche definire mappe personalizzate utilizzando l’API Schema Registry. Guarda il tutorial su [definizione di campi personalizzati](../tutorials/custom-fields-api.md#custom-maps) per ulteriori informazioni.

## Esempio di composizione

Gli schemi rappresentano il formato e la struttura dei dati che verranno acquisiti in [!DNL Platform]e vengono create utilizzando un modello di composizione. Come indicato in precedenza, questi schemi sono composti da una classe e da zero o più gruppi di campi compatibili con tale classe.

Ad esempio, uno schema che descrive gli acquisti effettuati in un negozio al dettaglio potrebbe essere denominato &quot;[!UICONTROL Memorizza transazioni]&quot;. Lo schema implementa [!DNL XDM ExperienceEvent] classe combinata con lo standard [!UICONTROL Commerce] gruppo di campi e un gruppo definito dall&#39;utente [!UICONTROL Informazioni prodotto] gruppo di campi.

È possibile chiamare un altro schema che tiene traccia del traffico del sito web &quot;[!UICONTROL Visite web]&quot;. Inoltre, implementa [!DNL XDM ExperienceEvent] ma questa volta combina lo standard [!UICONTROL Web] gruppo di campi.

Il diagramma seguente mostra questi schemi e i campi con il contributo di ciascun gruppo di campi. Contiene anche due schemi basati su [!DNL XDM Individual Profile] , inclusa la classe &quot;[!UICONTROL Membri fedeltà]&quot; menzionato in precedenza in questa guida.

![](../images/schema-composition/composition.png)

### Union {#union}

Mentre [!DNL Experience Platform] consente di comporre schemi per casi d’uso particolari, e di visualizzare un’&quot;unione&quot; di schemi per un tipo di classe specifico. Il diagramma precedente mostra due schemi basati sulla classe ExperienceEvent XDM e due schemi basati su [!DNL XDM Individual Profile] classe. L’unione, illustrata di seguito, aggrega i campi di tutti gli schemi che condividono la stessa classe ([!DNL XDM ExperienceEvent] e [!DNL XDM Individual Profile], rispettivamente).

![](../images/schema-composition/union.png)

Attivando uno schema da utilizzare con [!DNL Real-Time Customer Profile], verrà incluso nell’unione per quel tipo di classe. [!DNL Profile] fornisce profili solidi e centralizzati di attributi del cliente, nonché un account con marca temporale per ogni evento che il cliente ha avuto in qualsiasi sistema integrato con [!DNL Platform]. [!DNL Profile] utilizza la visualizzazione unione per rappresentare questi dati e fornire una visualizzazione olistica di ogni singolo cliente.

Per ulteriori informazioni sull&#39;utilizzo di [!DNL Profile], vedere [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

## Mappatura dei file di dati su schemi XDM

Tutti i file di dati acquisiti in [!DNL Experience Platform] deve essere conforme alla struttura di uno schema XDM. Per ulteriori informazioni su come formattare i file di dati per rispettare le gerarchie XDM (inclusi i file di esempio), consulta il documento su [esempio di trasformazioni ETL](../../etl/transformations.md). Per informazioni generali sull’acquisizione di file di dati in [!DNL Experience Platform], vedere [panoramica dell’acquisizione batch](../../ingestion/batch-ingestion/overview.md).

## Schemi per tipi di pubblico esterni

Se stai inserendo in Platform tipi di pubblico da sistemi esterni, devi utilizzare i seguenti componenti per acquisirli negli schemi:

* [[!UICONTROL Definizione del segmento] classe](../classes/segment-definition.md): utilizza questa classe standard per acquisire gli attributi chiave di una definizione di segmento esterna.
* [[!UICONTROL Dettagli sull’iscrizione al segmento] gruppo di campi](../field-groups/profile/segmentation.md): aggiungi questo gruppo di campi al tuo [!UICONTROL Profilo individuale XDM] per associare i profili dei clienti a tipi di pubblico specifici.

## Passaggi successivi

Ora che conosci le nozioni di base sulla composizione dello schema, puoi iniziare a esplorare e creare schemi utilizzando [!DNL Schema Registry].

Per esaminare la struttura delle due classi XDM di base e dei relativi gruppi di campi compatibili di uso comune, consulta la seguente documentazione di riferimento:

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

Il [!DNL Schema Registry] viene utilizzato per accedere a [!DNL Schema Library] in Adobe Experience Platform e fornisce un’interfaccia utente e un’API RESTful da cui tutte le risorse libreria disponibili sono accessibili. Il [!DNL Schema Library] contiene le risorse del settore definite da Adobe, le risorse del fornitore definite da [!DNL Experience Platform] partner e classi, gruppi di campi, tipi di dati e schemi composti da membri dell’organizzazione.

Per iniziare a comporre lo schema utilizzando l’interfaccia utente, segui insieme alla [Esercitazione sull’editor di schemi](../tutorials/create-schema-ui.md) per creare lo schema &quot;Membri fedeltà&quot; menzionato in questo documento.

Per iniziare a utilizzare [!DNL Schema Registry] API, inizia leggendo il [Guida per gli sviluppatori API del Registro di schema](../api/getting-started.md). Dopo aver letto la guida per sviluppatori, segui i passaggi descritti nell’esercitazione su [creazione di uno schema tramite l’API Schema Registry](../tutorials/create-schema-api.md).

## Appendice

Le sezioni seguenti contengono informazioni aggiuntive sui principi della composizione dello schema.

### Tabelle relazionali e oggetti incorporati {#embedded}

Quando si lavora con i database relazionali, le best practice prevedono la normalizzazione dei dati o la suddivisione di un’entità in parti discrete da visualizzare in più tabelle. Per leggere i dati nel loro insieme o aggiornare l&#39;entità, è necessario eseguire operazioni di lettura e scrittura in più tabelle singole utilizzando JOIN.

Mediante l’utilizzo di oggetti incorporati, gli schemi XDM possono rappresentare direttamente dati complessi e memorizzarli in documenti autonomi con una struttura gerarchica. Uno dei principali vantaggi di questa struttura è che consente di eseguire query sui dati senza dover ricostruire l’entità tramite join costosi su più tabelle denormalizzate. Non esistono restrizioni rigide sul numero di livelli consentiti per la gerarchia dello schema.

### Schemi e big data {#big-data}

I sistemi digitali moderni generano una grande quantità di segnali comportamentali (dati sulle transazioni, registri web, internet delle cose, display e così via). Questi big data offrono opportunità straordinarie per ottimizzare le esperienze, ma sono difficili da utilizzare a causa della scala e della varietà dei dati. Per ottenere valore dai dati, la struttura, il formato e le definizioni devono essere standardizzati in modo da poter essere elaborati in modo coerente ed efficiente.

Gli schemi risolvono questo problema consentendo l’integrazione dei dati da più origini, la standardizzazione attraverso strutture e definizioni comuni e la condivisione tra le diverse soluzioni. Ciò consente ai processi e ai servizi successivi di rispondere a qualsiasi tipo di domanda sui dati, abbandonando l’approccio tradizionale alla modellazione dei dati in cui tutte le domande che verranno poste sui dati sono note in anticipo e i dati vengono modellati in modo da essere conformi a tali aspettative.

### Oggetti e campi in formato libero {#objects-v-freeform}

Durante la progettazione degli schemi è necessario considerare alcuni fattori chiave per la scelta degli oggetti rispetto ai campi in formato libero:

| Oggetti | Campi in formato libero |
| --- | --- |
| Aumenta la nidificazione | Nidificazione minore o assente |
| Crea raggruppamenti di campi logici | I campi vengono inseriti in posizioni ad hoc |

{style="table-layout:auto"}

#### Oggetti

Di seguito sono elencati i pro e i contro dell’utilizzo di oggetti su campi in formato libero.

**Pro**:

* Gli oggetti vengono utilizzati in modo ottimale quando si desidera creare un raggruppamento logico di determinati campi.
* Gli oggetti organizzano lo schema in modo più strutturato.
* Gli oggetti aiutano indirettamente a creare una buona struttura di menu nell’interfaccia utente di Segment Builder. I campi raggruppati all’interno dello schema si riflettono direttamente nella struttura di cartelle fornita nell’interfaccia utente di Segment Builder.

**Contro**:

* I campi diventano più nidificati.
* Quando si utilizza [Servizio query Adobe Experience Platform](../../query-service/home.md), è necessario fornire stringhe di riferimento più lunghe per i campi di query nidificati negli oggetti.

#### Campi in formato libero

Di seguito sono elencati i pro e i contro dell’utilizzo di campi in formato libero sugli oggetti.

**Pro**:

* I campi in formato libero vengono creati direttamente sotto l’oggetto principale dello schema (`_tenantId`), aumentando la visibilità.
* Le stringhe di riferimento per i campi in formato libero tendono a essere più brevi quando si utilizza Query Service.

**Contro**:

* La posizione dei campi in formato libero all’interno dello schema è ad hoc, ovvero vengono visualizzati in ordine alfabetico nell’Editor di schema. Questo può rendere gli schemi meno strutturati e simili campi a forma libera possono finire per essere molto separati a seconda del loro nome.
