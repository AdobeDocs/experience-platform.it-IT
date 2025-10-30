---
title: Adobe Experience Platform per aziende con più marchi e aree geografiche
description: Scopri come fornire ai team di implementazione gli strumenti e le informazioni necessari per navigare efficacemente tra le complessità di Adobe Experience Platform.
source-git-commit: 6e96cf7660a9a7fe1b4eaef645bca55ed89b7673
workflow-type: tm+mt
source-wordcount: '5322'
ht-degree: 0%

---


# Adobe Experience Platform per aziende con più marchi e aree geografiche

## Introduzione

Adobe Experience Platform è all&#39;avanguardia nelle soluzioni di trasformazione, consentendoti di sfruttare appieno il potenziale dei dati e dei contenuti dei clienti. Con Experience Platform, puoi centralizzare e standardizzare i dati provenienti da diversi sistemi e applicare la potenza della data science e dell’apprendimento automatico. Il risultato è una creazione e una distribuzione migliorate di esperienze personalizzate che suonano con i tuoi consumatori.

Experience Platform consente di rappresentare la struttura e gestire i dati aziendali per implementazioni scalabili e flessibili. L’implementazione delle applicazioni Platform è un percorso significativo che richiede una pianificazione strategica e considerazioni accurate, soprattutto se si opera su domini globali, regionali e specifici del marchio o una combinazione di tutti questi aspetti.

Questo white paper funge da riferimento e offre un punto di vista del prodotto e una serie di linee guida. Il suo obiettivo principale è fornire a te e ai tuoi team di implementazione gli strumenti e le informazioni necessari per navigare efficacemente tra le complessità di Experience Platform. Fornendo un framework strutturato per la valutazione di requisiti specifici, considerazioni e casi d’uso reali, ti fornisce le conoscenze necessarie per sfruttare appieno il potenziale delle applicazioni basate su Experience Platform e piattaforma. Leggendo le sezioni seguenti, troverai informazioni preziose e consigli per semplificare il processo di implementazione e migliorare la capacità della tua organizzazione di fornire esperienze eccezionali al tuo pubblico, fornendo al contempo governance e controlli per mantenere la privacy e la conformità.

![Profilo unificato CDP](./images/whitepaper/CDPoverview.png)

## Comprensione dell&#39;azienda multi-brand e multi-region

Se gestisci un’azienda con più marchi e aree geografiche, probabilmente hai requisiti di gestione dei dati univoci per Experience Platform. Comprendere i requisiti specifici è fondamentale per adattare l’implementazione di Experience Platform alle esigenze specifiche.

Quando esplori le opzioni di implementazione, devi comprendere e considerare gli utenti tipo che interagiranno con Experience Platform e le applicazioni basate su piattaforma. Progettare la loro esperienza in base ai loro ruoli e interessi garantisce un’implementazione di successo. Di seguito sono riportati tre utenti tipo principali da considerare durante l’esplorazione delle opzioni:

**Mary, l&#39;addetto marketing:**

- Focus: acquisizione di clienti e personalizzazione delle esperienze su larga scala.
- Obiettivi: creazione di profili completi, miglioramento dell’efficienza dei contenuti multimediali.

**Ted, il tecnico**

- Focus: gestione dei dati organizzativi.
- Obiettivi: garanzia di conformità, gestione dei silos di dati, assistenza per varie linee di business.

**Dan, architetto dei dati**

- Focus: accuratezza e qualità dei dati.
- Obiettivi: garantire la privacy e l’affidabilità dei dati, progettare schemi e modelli di dati, gestire le origini dati.

### Un&#39;azienda che opera con isolamento limitato dei dati

Un principio architettonico chiave in Experience Platform è che i dati dei clienti sono limitati a una sandbox di produzione specifica basata su criteri e requisiti di governance.

Se la tua organizzazione necessita di un unico ambiente di dati per gestire la tua esperienza di marketing su larga scala, ti consigliamo di consolidare tutti i dati in un’unica sandbox Experience Platform con requisiti minimi di isolamento dei dati. All’interno di questa configurazione, i dati vengono acquisiti in una sandbox e tutte le identità correlate sono rappresentate come un unico profilo unificato, identificato da un’identità pseudonima o nota. Ciò significa che gli esperti di marketing possono accedere a tutti gli attributi del profilo e ai dati degli eventi esperienza all’interno di Experience Platform nella tua azienda. Possono utilizzare questi dati con applicazioni basate su piattaforma per creare tipi di pubblico e percorsi con la necessità minima di impedire agli addetti al marketing di utilizzare tutti i dati, indipendentemente dal marchio o dall’area geografica. Questo approccio semplifica la segmentazione e l’attivazione del pubblico nelle destinazioni supportate dalle applicazioni Experience Platform. Questa strategia funziona bene se intendi sfruttare l’intera base di clienti, indipendentemente dalle differenze regionali o specifiche del brand, per attività di marketing unificate e coese.

![Sandbox di produzione singola con architettura CDP](./images/whitepaper/Architecture-single-prod-sandbox.png)

#### Come funziona

Pianifichiamo innanzitutto l’implementazione e configuriamo l’ambiente di primo livello. Successivamente, deciderai il numero di sandbox, ruoli e autorizzazioni necessari per utilizzare in modo ottimale le applicazioni basate su Experience Platform e piattaforma per la tua azienda.

##### Configurazione generale per l’implementazione

- Configura le sandbox per abilitare la creazione di profili cliente unificati.
- Imposta i ruoli e i controlli di accesso per amministrare le sandbox e accedere alle funzionalità per ogni utente tipo.
- Gestisci il ciclo di vita dello sviluppo con una sandbox di sviluppo e strumenti sandbox.

**Sandbox**

Le sandbox sono partizioni virtuali all’interno di una singola istanza di Experience Platform, che consentono un’integrazione perfetta con il processo di sviluppo delle applicazioni di esperienza digitale. Tutti i contenuti e le azioni eseguite all’interno di una sandbox sono limitati a tale sandbox e non influiscono su nessun’altra sandbox, inclusi i dati e l’accesso ai dati. In Experience Platform sono supportati due tipi di sandbox:

- **Sandbox di produzione**: una sandbox di produzione deve essere utilizzata con i profili nell&#39;ambiente di produzione. Experience Platform consente di creare più sandbox di produzione per fornire la funzionalità dati corretta mantenendo al contempo l’isolamento operativo.

- **Sandbox di sviluppo**: una sandbox di sviluppo può essere utilizzata esclusivamente per lo sviluppo e il test con profili non di produzione.

È possibile creare più sandbox di qualsiasi tipo; per questo tipo di azienda verrà utilizzata una sandbox di produzione e una sandbox di sviluppo per illustrare come eseguire e gestire questo tipo di azienda.

![CDP-Crea una sandbox](./images/whitepaper/Create-sandbox.png)

Nella sandbox di produzione, ci aspettiamo che tu acquisisca il profilo di produzione e i dati dell’evento esperienza per creare un profilo unificato per le attività di marketing. Per ulteriori dettagli su come combinare dati noti e anonimi provenienti da più origini aziendali per creare profili cliente da utilizzare per fornire ai clienti esperienze personalizzate in tempo reale su tutti i canali e dispositivi, consulta la [documentazione di Adobe Real-Time Customer Data Platform](https://experienceleague.adobe.com/it/docs/experience-platform/rtcdp/home).

**Controlli di accesso**

Puoi definire i controlli di accesso con ruoli e autorizzazioni per controllare l’accesso alle risorse dell’applicazione in base all’utente tipo e alle relative funzionalità richieste. Inoltre, puoi limitare l’accesso a campi specifici dei dati del profilo. È necessario considerare attentamente questo passaggio per gestire meglio l’utilizzo di Experience Platform, delle applicazioni basate su piattaforma e dei dati dei clienti.

Considera un data engineer che potrebbe non avere bisogno di accedere a tutte le funzionalità delle applicazioni basate su Experience Platform e piattaforma. In genere sono responsabili della creazione di definizioni di dati (schemi), della configurazione delle origini dati per l’acquisizione dei dati e della creazione di set di dati. Tuttavia, potrebbe non essere la stessa persona che crea e attiva i tipi di pubblico per esperienze cliente personalizzate. Per questo utente tipo, crea un ruolo, aggiungi le autorizzazioni appropriate e concedi l’accesso solo alle funzionalità richieste. Al contrario, un addetto al marketing non creerebbe schemi e acquisirebbe dati, ma piuttosto si concentrerebbe sulla creazione e l’attivazione di tipi di pubblico per abilitare esperienze cliente personalizzate.

Se lo desideri, puoi aggiungere controlli di accesso granulari per limitare l’accesso a campi specifici nel profilo cliente unificato con funzionalità di controllo dell’accesso basato su attributi/controllo dell’accesso a livello di campo. Si tratta di meccanismi di governance in Experience Platform che consentono di limitare l’accesso agli attributi dei dati in base a etichette predefinite. Con il controllo degli accessi a livello di campo, è possibile gestire i dati personali identificabili e limitare l’accesso a tutti i flussi di lavoro di Experience Platform e delle applicazioni. Per ulteriori dettagli sulle funzionalità di controllo degli accessi, consulta la [documentazione sul controllo degli accessi](https://experienceleague.adobe.com/it/docs/experience-platform/access-control/home).

![Controlli di accesso CDP, Configura autorizzazioni ruolo](./images/whitepaper/Access-Controls-Configure-RolePermissions.png)

**Ciclo di vita dello sviluppo con sandbox di sviluppo**

Una sandbox di sviluppo si comporta come una sandbox di produzione in tutti gli aspetti funzionali. È diverso in quanto avrà alcune protezioni contrattuali che ti terranno entro i limiti della tua licenza. È progettato esclusivamente per lo sviluppo e il test con profili non di produzione, che supportano fino al 10% dell’impegno del profilo concesso in licenza (misurato cumulativamente in tutte le sandbox di sviluppo autorizzate). Per ulteriori dettagli e guardrail, consulta la [documentazione panoramica sulle sandbox](https://experienceleague.adobe.com/it/docs/experience-platform/sandbox/home) e la [pagina di descrizione del prodotto](https://helpx.adobe.com/it/legal/product-descriptions.html) per i dettagli di adesione.

Per il ciclo di vita di sviluppo e test, in questo esempio aziendale possono essere presenti più sandbox di sviluppo (fino a 4 in quanto viene utilizzata una sola sandbox di produzione).

**Esportazione e importazione di pacchetti con strumenti sandbox**

La funzione di strumenti sandbox consente agli utenti con le autorizzazioni appropriate di creare un pacchetto del loro lavoro da una sandbox di sviluppo ed esportarlo in un archivio. Questo archivio è accessibile ad altri utenti, che possono importare questi pacchetti nelle rispettive sandbox designate. Questa funzionalità garantisce configurazioni coerenti tra le sandbox, semplificando i processi di esportazione e importazione.

L’utilizzo di strumenti sandbox migliora in modo significativo la precisione della configurazione e riduce il tempo necessario per l’implementazione. Consente lo spostamento efficiente delle configurazioni di successo tra sandbox diverse.

Con la funzione di strumenti sandbox, puoi selezionare vari oggetti ed esportarli in un pacchetto. Un pacchetto può includere uno o più oggetti, ma tutti gli oggetti devono provenire dalla stessa sandbox.

**Automazione sandbox tramite API**

Puoi utilizzare le API di Experience Platform per automatizzare le distribuzioni sandbox e le attività di configurazione. Le API consentono il controllo programmabile per attività ripetitive come l’esportazione, l’importazione o la modifica di configurazioni sandbox, fornendo flessibilità se si preferiscono flussi di lavoro automatizzati.

Per ulteriori dettagli sugli strumenti sandbox, consulta la [documentazione sugli strumenti sandbox](https://experienceleague.adobe.com/it/docs/experience-platform/sandbox/ui/sandbox-tooling).

| ![CDP-Crea pacchetto](./images/whitepaper/create-package.png) | ![Pacchetti elenco CDP](./images/whitepaper/list-packages.png) |
| --- | --- |

### Isolamento dei dati per area geografica o marchio

Se hai bisogno di un isolamento completo (ad es., regionale o basato su marchio), puoi operare in base a criteri di accesso ai dati rigidi o a requisiti legali che limitano l’accesso dei team del tuo marchio ai dati specifici delle rispettive aree geografiche o dei rispettivi marchi. Puoi definire modelli di accesso in base a dati specifici per area geografica o marchio, garantendo la conformità con i protocolli interni, normativi e di governance dei dati. Questo approccio è fondamentale se operi in settori altamente regolamentati (ad esempio, la gestione dei dati PII) o se devi mantenere dati distinti e segmentati per diverse aree geografiche o identità del marchio.

![Sandbox di produzione multiple con architettura CDP](./images/whitepaper/Architecture-multiple-prod-sandbox.png)

#### Come funziona

Pianifichiamo innanzitutto l’implementazione, configuriamo l’ambiente di livello principale e decidiamo quante sandbox, ruoli e autorizzazioni sono necessari per utilizzare in modo ottimale le applicazioni basate su Experience Platform e piattaforma per la tua azienda.

##### Configurazione generale per l’implementazione di più sandbox

- Configura più sandbox di produzione per abilitare la creazione di profili cliente unificati in ciascuna sandbox.

- Imposta i ruoli e i controlli di accesso per amministrare le sandbox e accedere alle funzionalità per ogni utente tipo.

- Gestisci il ciclo di vita dello sviluppo con gli strumenti sandbox.

- Reporting e attivazione globali (aggregazione di dati da più sandbox per insights interorganizzativi con Customer Journey Analytics).

**Sandbox**

A differenza di una configurazione con una singola sandbox di produzione, se hai bisogno di un isolamento completo dei dati e dei flussi di lavoro potrebbe essere necessario un approccio più complesso. Qui entrano in gioco più sandbox di produzione, ciascuna delle quali rappresenta un’unità di isolamento personalizzata in base alle tue esigenze specifiche.

Come accennato, ogni sandbox è una partizione virtuale all’interno di una singola istanza della piattaforma. Queste sandbox consentono di gestire dati, flussi di lavoro e processi in un ambiente controllato che non interferisce con altre sandbox. Mentre le sandbox di sviluppo sono destinate ad attività di test e sviluppo con profili non di produzione, le sandbox di produzione sono la spina dorsale delle operazioni live e supportano l’acquisizione di dati di produzione effettivi per attività di marketing reali.

Vantaggi chiave dell’isolamento pulito nelle sandbox di produzione:

1. **Governance e conformità dei dati:** Se operi in settori regolamentati o in aree geografiche con leggi rigorose sulla privacy dei dati, devi assicurarti che i dati di una regione o di un marchio rimangano isolati. Più sandbox di produzione consentono di rispettare i requisiti di governance o gli standard specifici di settore garantendo che i dati siano accessibili solo all’interno della sandbox appropriata.

2. **Efficienza operativa:** isolando i dati e i flussi di lavoro, puoi gestire le operazioni in modo più efficiente. I team responsabili di diverse aree geografiche o marchi possono lavorare in modo indipendente all’interno delle sandbox dedicate senza preoccuparsi di perdite di dati accidentali o accessi non autorizzati.

3. **Flussi di lavoro personalizzati:** è possibile personalizzare ogni sandbox di produzione in base alle esigenze specifiche della propria regione o al marchio che rappresenta. Questo consente di implementare flussi di lavoro personalizzati, modelli di dati e strategie di marketing ottimizzati per quel segmento.

4. **Scalabilità:** con la crescita, puoi creare facilmente ulteriori sandbox di produzione per soddisfare nuove aree geografiche o marchi. Questa scalabilità assicura che la piattaforma sia in grado di adattarsi alle esigenze in continua evoluzione senza compromettere l’integrità dei dati o le prestazioni.

5. **Controllo avanzato:** Con più sandbox di produzione, gli amministratori dispongono di un controllo preciso sulle autorizzazioni di accesso, l&#39;acquisizione dei dati e l&#39;esecuzione dei flussi di lavoro. In questo modo è possibile adottare un approccio più sicuro e organizzato alla gestione di operazioni complesse all&#39;interno dell&#39;azienda globale.

**Controlli di accesso**

Nel contesto di più sandbox di produzione, i controlli di accesso rimangono un componente critico della gestione dei dati e dei flussi di lavoro all’interno di Experience Platform. Tuttavia, la complessità aumenta in quanto gli amministratori devono garantire che gli utenti possano accedere solo alle sandbox pertinenti ai loro ruoli, consentendo al contempo operazioni tra sandbox per gli utenti che lo richiedono, ad esempio i team di marketing che si trovano in più aree geografiche o i data engineer responsabili dell’acquisizione e della modellazione globale dei dati.

**Definizione dei ruoli e delle autorizzazioni nelle sandbox:**

Proprio come nel singolo scenario sandbox di produzione, puoi definire i criteri di controllo di accesso con ruoli e autorizzazioni personalizzati per le esigenze di diversi utenti tipo. Tuttavia, è necessario considerare in che modo questi ruoli si estendono su sandbox diverse in un ambiente con più sandbox.

Ad esempio:

- **Addetti marketing regionali:** se gli addetti al marketing operano in più aree geografiche, i loro ruoli potrebbero dover occupare più di una sandbox. Puoi concedere loro le autorizzazioni necessarie per accedere alle risorse in più sandbox, garantendo al contempo che il loro accesso sia ancora limitato ai dati e ai flussi di lavoro appropriati all’interno di ogni sandbox.

- **Ingegneri dei dati:** Gli ingegneri dei dati responsabili della creazione di modelli di dati, della definizione di schemi e della gestione dell&#39;acquisizione dei dati potrebbero dover accedere a tutte le sandbox. Puoi progettare i loro ruoli in modo che possano funzionare sull’intera piattaforma, limitando al contempo il loro accesso solo alle funzionalità e ai dati pertinenti per le loro attività. Ad esempio, un ingegnere dati che lavora su modelli di dati per Europa e Nord America può accedere alle sandbox di produzione per queste aree geografiche con l’autorizzazione di modificare gli schemi e acquisire i dati. Tuttavia, non avrebbero la possibilità di accedere a funzioni di marketing come la creazione e l’attivazione di tipi di pubblico.

**Considerazioni sul controllo degli accessi granulari:**

In un ambiente con più sandbox, il controllo granulare dell’accesso diventa ancora più critico. Il controllo degli accessi basato su attributi (controllo degli accessi a livello di campo/controllo degli accessi a livello di oggetto) consente di limitare ulteriormente l’accesso a campi di dati specifici all’interno di profili o determinati tipi di pubblico, garantendo la protezione delle informazioni sensibili o di identificazione personale (PII) in tutte le sandbox. Ad esempio:

- È possibile limitare l’accesso a determinati campi di dati all’interno di una sandbox solo agli utenti all’interno di tale area. In questo modo i dati PII o sensibili sono visibili solo a chi ne ha bisogno, in linea con le normative sulla privacy e le politiche di governance interne.

- Per gli utenti con accesso tra sandbox diverse, il controllo dell’accesso basato su attributi garantisce che, anche se hanno accesso a più sandbox, la visibilità dei dati sensibili sia limitata dal loro ruolo e dalla necessità di sapere.

Vantaggi dei controlli degli accessi basati su ruoli e attributi:

1. Controllando l&#39;accesso in base a ruoli e attributi, è possibile ridurre in modo significativo il rischio di accesso non autorizzato ai dati, garantendo che solo chi dispone delle autorizzazioni appropriate possa visualizzare o manipolare informazioni riservate.

2. Ruoli e autorizzazioni chiari e ben definiti semplificano le operazioni, in quanto ogni utente ha accesso alle funzionalità e ai dati necessari senza elementi inutili o rischi. Questa chiarezza supporta flussi di lavoro efficienti e riduce gli attriti.

3. Man mano che la tua azienda cresce ed evolve, i controlli di accesso possono essere regolati per adattarsi a nuove aree geografiche, nuovi marchi o nuovi ruoli. La flessibilità di modificare l’accesso senza interrompere i flussi di lavoro esistenti è fondamentale per ridimensionare le operazioni.

4. Gli amministratori possono mantenere un controllo centralizzato su tutte le sandbox, garantendo la coerenza delle modalità di applicazione dei controlli di accesso all’interno dell’azienda e consentendo al contempo la personalizzazione per diverse aree geografiche o marchi.

**Ciclo di vita dello sviluppo con sandbox di sviluppo**

La gestione del ciclo di vita dello sviluppo in più aree geografiche e marchi all’interno di Experience Platform richiede un approccio solido che garantisca coerenza, efficienza e scalabilità. Le sandbox di sviluppo supportano il ciclo di vita dello sviluppo in un ambiente complesso con numerose sandbox di produzione. Sono migliorate dalla funzione di strumenti sandbox, che consente la condivisione e l’implementazione senza interruzioni della configurazione in ambienti diversi.

Le sandbox di sviluppo svolgono un ruolo cruciale nel ciclo di vita dello sviluppo. Queste sandbox forniscono un ambiente isolato in cui sviluppatori e data engineer possono creare, testare e ripetere configurazioni senza influire sui dati di produzione. Anche se funzionalmente simili alle sandbox di produzione, le sandbox di sviluppo sono diverse perché sono destinate a test con profili non di produzione e sono disciplinate da limiti contrattuali, ad esempio il supporto fino al 10% dell’impegno del profilo concesso in licenza in tutte le sandbox di sviluppo autorizzate.

Puoi creare più sandbox di sviluppo per supportare team o aree geografiche diverse. Questo consente a ciascun team di sperimentare flussi di lavoro specifici per la propria area geografica o il proprio marchio, garantendo che gli ambienti di produzione rimangano stabili e sicuri durante lo sviluppo. Se disponi di molte sandbox di produzione, ti consigliamo di utilizzare un pool di sandbox di sviluppo per supportare più aree geografiche/marchi.

**Esportazione e importazione di pacchetti con strumenti sandbox**

La funzione di strumenti sandbox è uno strumento utile per la gestione di più sandbox. Consente agli sviluppatori, ai data engineer e agli esperti di marketing di creare pacchetti del loro lavoro in una sandbox di sviluppo, inclusi schemi, modelli di dati e altre configurazioni, per poi esportarli in un archivio. Da lì, altri utenti possono accedere a questi pacchetti e importarli nelle loro sandbox designate, facilitando la condivisione e l’implementazione fluide di configurazioni di successo in tutta l’azienda.

Ad esempio, un ingegnere dati che lavora in una sandbox di sviluppo per l’area Nord America può creare uno schema e assemblarlo con tutte le relative dipendenze. Un altro data engineer in un’area diversa, come l’Europa, può accedere a questo pacchetto e importarlo nella propria sandbox regionale. Questo processo garantisce la coerenza della modellazione e della configurazione dei dati nell&#39;intera azienda, riducendo il rischio di errori e migliorando l&#39;efficienza operativa.

Vantaggi degli strumenti sandbox in un ambiente con più sandbox:

1. Gli strumenti sandbox semplificano il ciclo di vita dello sviluppo consentendo di condividere facilmente le configurazioni corrette su più sandbox. Questo riduce la duplicazione degli sforzi e garantisce che le best practice siano implementate in modo coerente in tutte le aree geografiche o in tutti i marchi.

2. La possibilità di esportare e importare pacchetti tra diverse sandbox migliora l’interoperabilità all’interno dell’azienda. I team di diverse aree geografiche possono collaborare in modo più efficace, garantendo che le loro configurazioni siano in linea con gli obiettivi aziendali generali e soddisfacendo al contempo requisiti regionali o specifici del marchio.

3. Man mano che le aziende crescono e aggiungono più sandbox per accogliere nuove aree geografiche o nuovi marchi, gli strumenti sandbox forniscono la scalabilità necessaria per gestire questi ambienti in modo efficiente. Le nuove sandbox possono essere configurate rapidamente utilizzando i pacchetti esistenti, accelerando il processo di onboarding e riducendo il tempo necessario per la pubblicazione.

4. Creando pacchetti di configurazioni e dipendenze in una sandbox di sviluppo e quindi distribuendole alle sandbox di produzione, le aziende possono garantire configurazioni precise e coerenti in tutti i settori. Questo riduce la probabilità di errori e migliora l’affidabilità complessiva della piattaforma.

5. Con gli strumenti sandbox, la transizione dallo sviluppo alla produzione è fluida e controllata. Una volta testate e convalidate le configurazioni in una sandbox di sviluppo, è possibile esportarle e importarle in una sandbox di produzione con la certezza che funzioneranno come previsto.

**Reporting globale e attivazione**

Ciò comporta l’aggregazione di dati da più sandbox per informazioni cross-organization, spesso richiedendo una sandbox di reporting dedicata per l’integrazione con Customer Journey Analytics.

L&#39;approccio sandbox di produzione multipla offre chiaramente vantaggi di isolamento per le operazioni regionali e specifiche del marchio, ma introduce anche sfide che richiedono soluzioni creative. Una sfida chiave è la capacità di analizzare i dati tra sandbox diverse a scopo di reporting globale e di campagna globale. Le aziende spesso devono comprendere il percorso dei clienti a livello globale, il che comporta l’integrazione di dati da più sandbox e l’abilitazione di attività di marketing tra sandbox diverse. Di seguito vengono delineati gli approcci per affrontare queste sfide.

**Generazione di rapporti globali tra sandbox**

Quando un’azienda opera con più sandbox di produzione, ciascuna delle quali rappresenta una regione o un marchio, l’analisi dei dati dei clienti in tutte le sandbox diventa complessa. Ad esempio, la creazione di una visione unificata del percorso dei clienti tra marchi diversi richiede il consolidamento dei dati provenienti da questi ambienti isolati.

**Sandbox globale dedicata**

![Sandbox di reporting globale dedicata a CDP](./images/whitepaper/dedicated-global-reporting-sandbox.png)

Questa sandbox funge da archivio centrale in cui vengono consolidati i dati di singole sandbox regionali o specifiche del brand. Una soluzione comune consiste nell’utilizzare Query Service all’interno di ogni sandbox per estrarre i dati rilevanti del cliente. Ciò può includere profili ed eventi di esperienza che devono essere analizzati in diverse aree geografiche o marchi. Una volta preparati i dati da ogni sandbox, questi vengono acquisiti nella sandbox di reporting globale per l’analisi e la creazione di tipi di pubblico.

Utilizza Customer Journey Analytics per eseguire analisi cross-market e cross-brand sui dati aggregati nella sandbox globale per ottenere una visione completa delle interazioni dei clienti tra tutti i marchi e aree geografiche. Questo consente loro di generare informazioni importanti, ad esempio identificare i clienti che interagiscono con più marchi e creare tipi di pubblico per più marchi o aree geografiche. Queste informazioni possono essere utilizzate per vari scopi, tra cui l’attivazione di strategie di marketing, la personalizzazione delle esperienze dei clienti e la promozione della crescita aziendale.

**Condivisione del pubblico**

La sandbox globale consente inoltre ai team di marketing globale di definire e gestire i tipi di pubblico su una scala più ampia. Utilizzando gli strumenti sandbox, questi tipi di pubblico globali (solo definizioni, non dati) possono essere esportati dalla sandbox globale a singoli marchi o sandbox regionali, consentendo ai team di marketing locali di valutarli e attivarli nei rispettivi mercati.

Inoltre, puoi utilizzare Experience Platform Segment Match, una funzione in Platform che consente la condivisione di segmenti (pubblico qualificato) tra sandbox diverse unità organizzative o entità aziendali.

Questo servizio di condivisione dei segmenti consente a due o più utenti di scambiarsi i dati dei segmenti in modo sicuro, gestito e rispettoso della privacy.

Per ulteriori dettagli sulla funzione Segment Match, consulta la [documentazione di Segment Match](https://experienceleague.adobe.com/it/docs/experience-platform/segmentation/ui/segment-match/overview).

### Una combinazione di approcci per le operazioni globali, regionali e specifici per il brand

Molte aziende multimarca operano su scala globale e, come tali, cercano spesso una combinazione di approcci di gestione dei dati unificati e isolati. In questo scenario, cercano di separare i dati per più regioni o paesi. I brand all’interno dell’organizzazione possono aspettarsi di operare esclusivamente sui dati associati al proprio marchio specifico, il tutto all’interno degli stessi limiti di dati di una geografia o di un paese. Questo approccio consente la gestione centralizzata dei dati regionali o nazionali, facilitando al tempo stesso le operazioni di marketing e di dati specifiche per il brand. Si tratta di un modello che combina i vantaggi della gestione unificata dei dati con la necessità di un isolamento specifico per il marchio e l’area geografica.

Riconoscendo questi diversi requisiti, Experience Platform può essere configurato per fornire una soluzione di gestione dei dati altamente adattabile e flessibile, garantendo che le aziende con più marchi e aree geografiche possano rappresentare efficacemente la tua azienda all’interno della piattaforma. Che si tratti di massimizzare i dati collettivi dei clienti, mantenere un rigido isolamento dei dati o raggiungere un equilibrio tra i due, Experience Platform è in grado di soddisfare le diverse esigenze della tua azienda.

![CDP-Architecture Un approccio misto](./images/whitepaper/Architecture-blend-sandbox.png)

#### Come funziona

Pianifichiamo innanzitutto l’implementazione, configuriamo l’ambiente di livello principale e decidiamo quante sandbox, ruoli e autorizzazioni sono necessari per utilizzare in modo ottimale le applicazioni basate su Experience Platform e piattaforma per questa azienda.

##### Impostazione generale per questa organizzazione

- Configura più sandbox di produzione per abilitare la creazione dei profili cliente unificati.

- Imposta i ruoli e i controlli di accesso per amministrare le sandbox e accedere alle funzionalità per ogni utente tipo.

- Impostare il controllo degli accessi basato su attributi: controllo degli accessi a livello di campo/controllo degli accessi a livello di oggetto per i controlli granulari sugli attributi di profilo e sui tipi di pubblico.

- Gestisci il ciclo di vita dello sviluppo con sandbox di sviluppo e strumenti sandbox.

- Reporting globale.

**Sandbox**

Imposta una sandbox per marchio/area geografica. Per la creazione di più sandbox di produzione, consulta le sezioni precedenti.

**Controlli di accesso**

Ruoli e autorizzazioni utente:

- Crea il ruolo &quot;**Addetto marketing—Global**&quot; e concedi l&#39;autorizzazione per creare, visualizzare e gestire i tipi di pubblico. Inoltre, questo ruolo otterrà l’autorizzazione per visualizzare tutti i dati dei clienti.

- Crea ruoli e concedi l’accesso solo a determinate funzioni per l’utente tipo corretto. Ad esempio, i ruoli utente &quot;**Addetto marketing—Germania**&quot; e &quot;**Addetto marketing—Francia**&quot; otterrebbero l&#39;autorizzazione solo per creare, visualizzare e gestire tipi di pubblico sui dati del paese abilitati da una combinazione di controllo dell&#39;accesso a livello di campo, controllo dell&#39;accesso a livello di oggetto e tipi di pubblico predefiniti.

- Crea il ruolo &quot;**Technologist—Global**&quot; e concedi le autorizzazioni giuste per creare e gestire schemi, set di dati, criteri, origini e così via. Questo ruolo sarebbe responsabile di tutte le operazioni di amministrazione e configurazione necessarie.

###### Progettazione dello schema e controllo dell&#39;accesso basato su attributi: controllo dell&#39;accesso a livello di campo

**Experience Data Model (XDM)**

Schema dati standardizzato in Experience Platform che garantisce una struttura coerente dei dati e l’interoperabilità in tutte le applicazioni basate su piattaforma.

**Controllo dell&#39;accesso basato su attributi: controllo dell&#39;accesso a livello di campo e opzione di modellazione dati:**

- Crea un modello dati per includere campi XDM (PII) specifici del tenant che devono essere limitati per ogni paese.

- Crea e applica etichette di paese ai campi XDM. Etichette = Germania, Francia, Irlanda, Paesi Bassi, ecc.

- Aggiungi etichette al ruolo appropriato. Ad esempio, aggiungi l’etichetta Germania al ruolo &quot;Addetto marketing - Germania&quot;.

Schema profilo individuale XDM:

```
\- PII
\- Germany
    \- name --> Label: "Germany"
    \- email --> Label: "Germany"
    \- birthdate --> Label: "Germany"

\- France
    \- name --> Label: "France"
    \- email --> Label: "France"
    \- birthdate --> Label: "France"

\- Netherland
    \- name --> Label: "Netherland", "Germany"
    \- email --> Label: "Netherland", "Germany"
    \- birthdate --> Label: "Netherland", "Germany"

\- Loyalty
    \- member
    \- registrationDate
```

###### Tipi di pubblico: utilizzare il controllo degli accessi basato su attributi: controllo degli accessi a livello di oggetto per controllare l’accesso a tipi di pubblico specifici per il marchio o il paese

**Controllo dell&#39;accesso basato su attributi: controllo dell&#39;accesso a livello di oggetto per i tipi di pubblico:**

- Crea tipi di pubblico e controlla chi può visualizzarli.

- Crea e applica etichette di paese ai tipi di pubblico. Labels = Germania, Francia, Irlanda, Paesi Bassi e così via.

- Aggiungi etichette al ruolo appropriato. Ad esempio, aggiungi l’etichetta &quot;Germania&quot; al ruolo &quot;Addetto marketing - Germania&quot;.

![Tipi di pubblico con etichetta CDP](./images/whitepaper/label-audience.png)

###### Includere un pubblico predefinito durante la creazione di tipi di pubblico specifici per il marchio o il paese

**Pubblico predefinito: alternativa al controllo degli accessi a livello di riga:**

- Attualmente, il generatore di pubblico consente di includere i tipi di pubblico esistenti come blocchi predefiniti nel processo di creazione del pubblico.

- Il risultato viene derivato dal pubblico, seguito da attributi ed eventi.

- Non esiste un meccanismo per aggiungere automaticamente uno o più tipi di pubblico al momento della composizione.

![CDP-Aggiungi un pubblico predefinito](./images/whitepaper/default-audience.png)

###### Attivazione e filtro dei profili a livello di marchio/paese

**Opzione criterio di consenso personalizzato:**

Questo consente di controllare o filtrare i profili al momento dell’attivazione:

- Crea un’azione di marketing.

- Creare una destinazione e associare l’azione di marketing.

- Crea un criterio di consenso personalizzato.

>[!NOTE]
>
> Lo SKU di Privacy and Security Shield è necessario per creare i criteri di consenso.

![Criteri di consenso personalizzati CDP e filtro attivazione](./images/whitepaper/custom-consent-policy.png)

Attivazione di più marchi e complessità dei criteri di consenso:

La gestione dell’attivazione del pubblico tra più marchi richiede la governance dettagliata dei criteri di consenso, garantendo il rispetto dei requisiti specifici di ogni marchio. Inoltre, Adobe Privacy and Security Shield (una funzione di conformità in Experience Platform che applica le policy di protezione dei dati e garantisce l’allineamento normativo tra i vari canali di attivazione) può imporre limitazioni specifiche sul modo in cui le policy di consenso vengono applicate tra i diversi canali di attivazione. È necessario valutare attentamente queste considerazioni e implementare i framework di governance per mantenere la conformità e l&#39;efficienza operativa.

Devi anche navigare attentamente tra le complessità relative alle configurazioni dei criteri di consenso e alle attivazioni specifiche per il canale. La definizione esplicita dei criteri di consenso per ogni area geografica o marchio e la gestione coerente di tali configurazioni sono fondamentali per la conformità e l’efficienza operativa.

## Considerazioni generali

In alcuni scenari, è possibile scegliere di distribuire applicazioni basate su Experience Platform e piattaforma su più ID organizzazione anziché utilizzare un singolo ID organizzazione con più sandbox. Questo approccio può offrire vantaggi in termini di residenza dei dati, sicurezza e amministrazione, ma introduce anche complessità. Di seguito sono riportate alcune considerazioni chiave per determinare quando può essere appropriato un approccio multiorganizzazione.

### Che cos’è un ID organizzazione

- Un ID organizzazione è l’implementazione di Adobe di Federated ID e del protocollo OAuth 2.0.

- Un ID organizzazione è una raccolta di tutte le applicazioni, gli utenti e le autorizzazioni a cui un’organizzazione ha i diritti in base ai termini contrattuali di Adobe.

- Gli account utente e le autorizzazioni vengono gestiti tramite Admin Console di ogni organizzazione.

- Gli ID organizzazione determinano anche il modo in cui le soluzioni Adobe interagiscono tra loro. Le soluzioni all&#39;interno della stessa organizzazione possono essere interoperabili.

- In generale, un ID organizzazione viene distribuito in una singola area geografica.

![Opzione per più organizzazioni IMS con architettura CDP](./images/whitepaper/Architecture-multi-imsorg.png)

**Più ID organizzazione: vantaggi e considerazioni&#x200B;**

| Vantaggi | Considerazioni |
| -------- | -------------- |
| Di seguito è riportato un elenco dei vantaggi derivanti dall&#39;utilizzo di più ID organizzazione: <ul><li>Flessibilità di memorizzazione dei dati in determinate aree globali.</li><li>&#x200B;Accesso utente separato per istanza - ovvero, Wholefoods non può accedere ad Audible.&#x200B;</li><li>Endpoint API dedicati che consentono a ogni Market/UB di creare connessioni personalizzate in base alle esigenze nel proprio ambiente&#x200B;</li><li>Ogni business unit disporrà di chiavi gestite dal cliente&#x200B;</li><li>Le richieste RGPD possono essere effettuate per unità aziendale&#x200B;.</li><li>Storage e elaborazione completamente isolati tra le unità aziendali&#x200B;.</li><li>Allevia alcuni guardrail/limiti delle prestazioni a livello di organizzazione&#x200B;.</li><li>Maggiore flessibilità con il provisioning e la combinazione di SKU tra unità aziendali. Ad esempio, un’organizzazione può avere una SKU diversa di Adobe Journey Optimizer rispetto a un’altra organizzazione.</li></ul> | Di seguito sono riportati alcuni aspetti da considerare quando si dispone di più ID organizzazione: <ul><li>Più ID organizzazione da gestire rispetto a uno solo&#x200B;</li><li>Più istanze/ambienti separati da gestire (integrazioni, caricamenti di dati e così via).</li><li>&#x200B;gli ECID saranno univoci per organizzazione, rendendo difficile associare i dati tra le diverse unità aziendali&#x200B;.</li><li>Dovrebbe migrare/reimplementare Analytics e Target per organizzazione, perdendo il rollup globale (se attualmente in uso)&#x200B;.</li><li>È necessaria una maggiore orchestrazione per effettuare richieste RGPD tra le business unit&#x200B;.</li><li>Alcune integrazioni di applicazioni basate su Experience Platform memorizzano i metadati a livello di organizzazione. Non tutto è &quot;in modalità sandbox&quot; per le sandbox&#x200B;.</li><li>L’ID organizzazione è fissato a un’area geografica. La posizione di hosting di Adobe AWS è attualmente solo negli Stati Uniti. Adobe non supporta la migrazione da un’area di hosting a un’altra&#x200B;</li><li>Edge non riconosce le sandbox (per l’inoltro degli eventi).</li></ul> |

**ID organizzazione singolo: vantaggi e considerazioni**

![Sandbox di produzione multiple con architettura CDP](./images/whitepaper/Architecture-multiple-prod-sandbox.png)

| Vantaggi | Considerazioni |
| -------- | -------------- |
| Di seguito è riportato un elenco dei vantaggi derivanti dall&#39;utilizzo di un singolo ID organizzazione: <ul><li>Provisioning di singole sandbox per creare una separazione logica tra le business unit all’interno di un’area implementata</li><li>Singolo ID organizzazione da gestire per l’IT per utenti, provisioning e così via.</li><li>Nessuna migrazione di tag, Target, Analytics e altro di Adobe, se si trova nello stesso ID organizzazione.</li><li>Non è richiesto alcun ripristino per gli ECID esistenti: impedisce il &quot;cliffing&quot; nei dati di Adobe Analytics.</li><li>Accesso singolo per le risorse di marketing globali.</li><li>Diritti di accesso degli utenti per controllare chi ha accesso alle sandbox, con livelli appropriati di controllo dell’accesso basato sui ruoli.</li><li>Sfrutta le istanze Global Analytics e Target e i dati della suite di rapporti.</li></ul> | Di seguito sono riportati alcuni aspetti da considerare quando si dispone di un singolo ID organizzazione: <ul><li>I dati verranno archiviati in un&#39;unica area.</li><li>Possibile necessità di consolidare i dati in un unico ID organizzazione.</li><li>Tutte le unità aziendali condividerebbero la stessa infrastruttura tra le applicazioni (core Experience Platform, Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics).</li><li>Guardrail: alcuni sono globali per organizzazione, come la segmentazione in streaming, che è 1.5k RPS.</li><li>Le richieste RGPD operano a livello di organizzazione e non possono essere indirizzate a sandbox specifiche.</li><li>Le chiavi gestite dal cliente sono impostate a livello di ID organizzazione: con questo approccio, tutte le sandbox delle unità aziendali condividerebbero la stessa chiave di crittografia.</li><li>Richiede chiarezza sulle licenze aziendali in DX e CC per garantire che le applicazioni siano fornite negli ID organizzazione corretti.</ul></li> |

**Vantaggi e considerazioni**

L’accesso degli utenti, i diritti e la segregazione dei dati a livello organizzativo sono regolati da più ID organizzazione, che a livello sandbox sono invece gestiti da un singolo ID organizzazione.

| Scenario/Requisito | ID organizzazione multipli | Più sandbox (singolo ID organizzazione) |
| ----------------------------------- | --------------------------------------------------- | ----------------------------------------------- |
| Residenza dati | Isolamento completo e ID organizzazione specifici della regione | Distribuzione per area geografica singola |
| Governance dei dati e isolamento | Separazione completa e isolamento | Isolamento operativo, ID organizzazione condivisa |
| Gestione della conformità (ad esempio, RGPD) | Richieste separate per ID organizzazione | Una singola richiesta si applica a più sandbox |
| Costi dell&#39;infrastruttura e licenze | Potenzialmente superiore a causa di configurazione duplicata | In genere sono inferiori con l&#39;amministrazione centralizzata |
| Reporting e attivazione globali | Problemi dovuti agli ambienti isolati | Rapporti e attivazione più semplici per le diverse aree geografiche |
| Complessità amministrativa | Maggiore a causa di più ID organizzazione isolati | Amministrazione centralizzata e inferiore |

## Conclusione riassuntiva

Experience Platform offre alle aziende un solido framework per centralizzare, gestire e attivare i dati dei clienti su modelli di business multi-brand e multi-area. Questo white paper ha esplorato le principali strategie di distribuzione, i modelli di governance e le best practice per ottimizzare l’implementazione di Experience Platform per le organizzazioni con esigenze operative e di isolamento dei dati diverse.

## Punti chiave da eliminare

1. **Modelli di distribuzione flessibili**

   - Le aziende possono scegliere tra **approcci a sandbox singola, a più sandbox o ibridi** in base ai requisiti operativi, di conformità e di governance.

   - **Le organizzazioni globali** possono richiedere più sandbox di produzione per soddisfare i requisiti di governance mantenendo al contempo l&#39;efficienza operativa.

2. **Governance dei dati e controllo degli accessi**

   - **Il controllo degli accessi basato su attributi, il controllo degli accessi a livello di campo e il controllo degli accessi a livello di oggetto** consentono una governance precisa dell&#39;accesso ai dati.

   - È necessario definire **ruoli e autorizzazioni chiari** per utenti tipo diversi (ad esempio, addetti al marketing, architetti di dati e team IT) per garantire un utilizzo corretto dei dati.

3. **Strumenti sandbox e automazione**

   - **Strumenti sandbox** semplifica la gestione della configurazione, consentendo ai team di esportare e importare le impostazioni in modo efficiente.

   - **L&#39;automazione basata su API** è un&#39;opzione disponibile per le aziende che desiderano semplificare le distribuzioni delle sandbox e la governance su larga scala.

4. **Strategie globali di reporting e attivazione**

   - Le aziende che sfruttano **Customer Journey Analytics** devono considerare la sincronizzazione dei dati e le implicazioni commerciali durante il consolidamento dei rapporti globali.

   - **Segment Match** fornisce un meccanismo conforme alla privacy per la condivisione del pubblico tra sandbox, garantendo attivazioni di marketing senza soluzione di continuità.

5. **Considerazioni su ID di più organizzazioni e sandbox multiple**

   - È necessario valutare attentamente se distribuire **più ID organizzazione o più sandbox** in base alla residenza dei dati, alla conformità e alle esigenze operative.

   - **Gli ID organizzazione** offrono isolamento completo&#x200B;**, mentre le impostazioni con più sandbox forniscono flessibilità operativa all&#39;interno di un framework di governance condiviso**.

## Considerazioni finali

Man mano che le aziende scalano le proprie funzionalità di esperienza digitale, Experience Platform funge da piattaforma fondamentale per promuovere attività di marketing basate sui dati, informazioni sui clienti e attivazioni cross-channel. Un&#39;implementazione di successo richiede un&#39;attenta pianificazione della **governance sandbox, dei criteri di conformità e dei flussi di lavoro operativi** per garantire efficienza e scalabilità a lungo termine.

Sfruttando le best practice descritte in questo white paper, puoi **ottimizzare Experience Platform per operazioni con più marchi e aree geografiche**, garantendo la gestione dei dati, la conformità e esperienze cliente personalizzate su larga scala.

## Riconoscimento

Questo white paper è stato sviluppato con le informazioni e i feedback degli esperti in materia in vari team, garantendo precisione, chiarezza e indicazioni pratiche. Ringraziamo tutti i colleghi per il loro prezioso contributo e la loro recensione. La loro esperienza ha contribuito a perfezionare questo documento per fornire alle aziende i servizi necessari per implementare Adobe Experience Platform in ambienti multi-brand e aree geografiche.
