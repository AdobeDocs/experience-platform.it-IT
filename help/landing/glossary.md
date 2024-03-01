---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Glossario di Adobe Experience Platform
description: Un glossario di terminologia importante in Experience Platform.
exl-id: 00eae5f5-7dfa-45ac-aff9-9e1769a3a53a
source-git-commit: b16eae9698de6c20022fdf1a3ff659df35e440f6
workflow-type: tm+mt
source-wordcount: '7996'
ht-degree: 0%

---

# Glossario di Adobe Experience Platform {#adobe-experience-platform-glossary}

## A

**Controllo degli accessi**: il controllo degli accessi basato sul ruolo consente agli amministratori di assegnare accesso e autorizzazioni agli utenti di Experienci Platform. Le autorizzazioni includono la possibilità di visualizzare e/o utilizzare funzioni di Experience Platform, ad esempio la creazione di sandbox, la definizione di schemi e la gestione di set di dati.

**ID chiave di accesso**: un ID della chiave di accesso è un identificatore univoco associato a un [!DNL Amazon] Chiave di accesso segreta S3. L’ID della chiave di accesso e la chiave di accesso segreta vengono utilizzati insieme per firmare [!DNL Amazon Web Services] (AWS) richieste.

**Azione**: nel contesto dei tag, un’azione è un tipo specifico di componente regola che definisce cosa deve accadere dopo che si è verificato un evento e le condizioni vengono valutate e passate.

**Attiva**: attivazione è l’azione intrapresa da un utente per mappare uno o più segmenti su una destinazione, ad esempio [!DNL Oracle Eloqua], [!DNL Google], o [!DNL Salesforce Marketing Cloud].

**Attività**: In [!DNL Offer Decisioning], un’attività contiene la logica necessaria per determinare la selezione di un’offerta.

**Amministratore**: uno o più utenti dell’organizzazione che possono configurare e personalizzare le autorizzazioni, ad Experience Platform in Adobe Admin Console.

**Adobe Admin Console**: Adobe Admin Console fornisce una posizione centrale per la gestione delle adesioni ai prodotti Adobe e dell’accesso per la tua organizzazione. Tramite la console, gli amministratori possono concedere a gruppi di utenti le autorizzazioni di accesso per varie funzionalità di Platform, ad esempio &quot;Gestisci set di dati&quot;, &quot;Visualizza set di dati&quot; o &quot;Gestisci profili&quot;.

**Adobe Experience Platform**: Adobe Experience Platform standardizza dati e contenuti a livello aziendale, fornendo profili di consumatori in tempo reale, consentendo l’utilizzo della scienza dei dati e accelerando la velocità dei contenuti per stimolare la personalizzazione dell’esperienza nel percorso del cliente.

**Servizio query Adobe Experience Platform**: consente agli analisti di dati di eseguire query su eventi e profili da utilizzare in Analytics e nell’apprendimento automatico. Con Query Service, data scientist e analisti possono richiamare tutti i loro set di dati memorizzati in Experienci Platform (inclusi i dati comportamentali e i punti vendita, la gestione delle relazioni con i clienti e altro ancora) ed eseguire query su tali set di dati per rispondere a domande specifiche sui dati.

**Servizio di segmentazione di Adobe Experience Platform**: consente di creare segmenti e generare tipi di pubblico dai dati del profilo cliente in tempo reale. Questi tipi di pubblico possono quindi essere esportati nei propri set di dati all’interno del Data Lake.

**Adobe Intelligent Services**: i servizi intelligenti come Attribution AI e IA per l’analisi dei clienti sono modelli basati sull’apprendimento automatico e sull’intelligenza artificiale appositamente progettati e che richiedono l’esecuzione e il funzionamento di Experienci Platform.

**Adobe I/O**: Adobe I/O fa parte di Experienci Platform e fornisce l’accesso a tutto ciò di cui gli sviluppatori hanno bisogno per integrare, estendere e personalizzare Platform, inclusi API, eventi, console per sviluppatori e strumenti utili.

**Adobe Sensei**: Adobe Sensei è il framework di intelligence che potenzia gli Experienci Platform. Fornisce inoltre una serie di servizi di intelligenza artificiale che consentono ai brand di migliorare la loro capacità di fornire ai clienti esperienze personalizzate in tempo reale.

**Bucket Amazon S3**: [!DNL Amazon S3] I bucket sono i contenitori fondamentali per i dati memorizzati nel [!DNL Amazon] ecosistema. I bucket contengono oggetti, ogni oggetto viene memorizzato e recuperato utilizzando una chiave univoca assegnata dagli sviluppatori.

**Connettore Amazon S3**: Il [!DNL Amazon] Il connettore S3 consente ai clienti di Experienci Platform di connettersi e accedere in modo sicuro ai [!DNL Amazon] Dati S3.

**APA**: Il [[!DNL Australia Privacy Act (Privacy Act)]](https://www.oaic.gov.au/privacy/the-privacy-act) promuove e protegge la privacy delle persone e regola il modo in cui le agenzie governative australiane e l&#39;organizzazione gestiscono le informazioni personali. Il [!DNL Privacy Act] include principi che si applicano alle organizzazioni del settore privato. Ad esempio, gli utenti hanno il diritto di comprendere il motivo per cui le informazioni personali vengono raccolte e come verranno utilizzate, la possibilità di accedere ai loro dati, cancellarli e correggerli.

**Aggiungi strategia di salvataggio**: la strategia di salvataggio &quot;append&quot; (Aggiungi) è un’opzione utilizzata quando si specificano dati di terze parti da acquisire tramite una connessione e si aggiungono nuovi dati o righe alla fine del set di dati. Le righe precedentemente acquisite rimangono intatte e solo le righe create dall’ultima esecuzione pianificata vengono acquisite in Experience Platform. Tutte le righe modificate nel sistema di origine rimangono invariate all&#39;Experience Platform.

**Array**: gli array vengono utilizzati per gli elementi ordinati con lo stesso tipo di dati.

**Intelligenza artificiale**: l’intelligenza artificiale è una teoria e uno sviluppo di sistemi informatici in grado di eseguire attività che normalmente richiedono intelligenza umana, come la percezione visiva, il riconoscimento vocale, il processo decisionale e la traduzione tra lingue diverse.

**Attributi**: gli attributi sono caratteristiche specificate che rappresentano un profilo.

**Unione attributi**: quando definisci un criterio di unione utilizzando l’API Profilo cliente in tempo reale, il `attributeMerge` object indica il modo in cui il criterio di unione assegnerà la priorità agli attributi del profilo in caso di conflitti di dati. Equivale a selezionare un [!UICONTROL Metodo di unione] durante la definizione di un criterio di unione nell’interfaccia utente di Platform.

**Attribution AI**: [!DNL Attribution AI] è un servizio intelligente basato su Adobe Sensei che fornisce funzionalità algoritmiche di attribuzione multicanale per l’intero ciclo di vita del cliente.

**Pubblico**: un pubblico è il set risultante di profili che soddisfano i criteri di una definizione di segmento.

**Dimensione pubblico**: una dimensione di pubblico è il numero totale di profili che soddisfano i criteri di una definizione di segmento e sono idonei per l’iscrizione al pubblico.

**Snapshot del pubblico**: un’istantanea del pubblico acquisisce tutti i profili idonei per i criteri del segmento al momento della segmentazione.

## B

**Backfill**: per le origini pianificate, l’opzione di backfill consente l’acquisizione di dati storici.

**Periodo di backfill**: il periodo di retrocompilazione è un’opzione che consente di impostare il periodo di tempo necessario per acquisire dati storici di terze parti tramite una connessione di origine. Selezionando un periodo di backfill di &quot;per sempre&quot; acquisirà l’intera cronologia dei dati sorgente in Experienci Platform.

**Batch**: un batch è un insieme di dati raccolti in un periodo di tempo ed elaborati insieme come una singola unità. I set di dati sono composti da più batch.

**ID batch**: un ID batch è un identificatore generato da un Adobe per un batch di dati.

**Acquisizione in batch**: l’acquisizione in batch consente di acquisire i dati in Experienci Platform come file batch. I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità.

**Segmentazione batch**: la segmentazione in batch è un’alternativa a un processo di selezione dei dati in corso e sposta tutti i dati del profilo contemporaneamente attraverso le definizioni dei segmenti per produrre pubblici corrispondenti. Una volta creato, il segmento viene salvato e memorizzato in modo da poterlo esportare per l’utilizzo.

**Genera**: nel contesto dei tag, una build è un file o un set di file che contengono tutte le configurazioni e il codice necessari per eseguire la logica di business contenuta all’interno di una libreria, che consente di distribuire tale libreria sul sito web o sull’app mobile.

**Strumenti di business intelligence**: gli strumenti di Business Intelligence (BI) sono principalmente integrati con [!DNL Experience Platform Query Service]. Gli strumenti BI sono tipi di software applicativo che raccolgono ed elaborano grandi quantità di dati non strutturati da sistemi interni ed esterni.

## C

**Limitazione**: In [!DNL Offer Decisioning], il limite (noto anche come quota limite di frequenza) viene utilizzato nelle regole di decisione per definire quante volte viene presentata un’offerta. Esistono due tipi di limite: uno indica quante volte un’offerta può essere proposta al pubblico target combinato (denominato &quot;limite globale&quot;) e l’altro indica quante volte un’offerta può essere proposta allo stesso utente finale (denominato &quot;limite del profilo&quot;).

**Catalogo**: nel contesto di origini e destinazioni, un catalogo è una galleria con connessioni disponibili ad applicazioni Adobe e tecnologie di terze parti. Da non confondere con [!DNL Catalog Service].

**[!DNL Catalog Service]**: [!DNL Catalog Service] (a volte chiamato [!DNL Catalog]) è il sistema di registrazione per la posizione e la derivazione dei dati in Adobe Experience Platform. Mentre tutti i dati acquisiti in Experienci Platform vengono memorizzati nel data lake come file e directory, [!DNL Catalog] contiene i metadati e la descrizione di tali file e directory a scopo di ricerca, monitoraggio e governance dei dati.

**CCPA**: Il [[!DNL California Consumer Privacy Act (CCPA)]](https://oag.ca.gov/privacy/ccpa) migliora i diritti alla privacy e la protezione dei consumatori dei residenti in California, Stati Uniti. Il CCPA conferisce ai residenti della California nuovi diritti sulla privacy dei dati, tra cui il diritto di accesso e cancellazione dei propri dati personali, di sapere se i propri dati personali vengono venduti o divulgati (e a chi), e il diritto di non acconsentire alla vendita dei propri dati a terzi.

**Classe**: in Experience Data Model (XDM), una classe definisce il set di campi più piccolo utilizzato per creare uno schema e il comportamento di base dell’oggetto business rappresentato dallo schema.

**Client**: un client è uno strumento o un’applicazione esterna che si connette a [!DNL Query Service] tramite [!DNL PostgreSQL] protocollo o API HTTP.

**Raccolta**: In [!DNL Offer Decisioning]Le raccolte sono sottoinsiemi di offerte basate su condizioni predefinite definite da un addetto marketing, ad esempio la categoria dell’offerta.

**Combina con azione di marketing PII**: azione di marketing che combina qualsiasi informazione personale identificabile (PII) con dati anonimi. I contratti per i dati provenienti da reti di annunci, server di annunci e fornitori di dati di terze parti spesso includono divieti contrattuali specifici sull’utilizzo di tali dati con dati direttamente identificabili.

**Interfaccia della riga di comando**: un’interfaccia della riga di comando è uno strumento basato su testo che può essere utilizzato per connettersi a [!DNL Query Service] per l’esecuzione di query non elaborate.

**Composizione**: una composizione è un raggruppamento di componenti che si formano insieme per formare lo schema.

**Condizione**: nel contesto dei tag, una condizione è un componente regola che valuta un’istruzione logica che deve restituire `true` o `false`. Tutte le condizioni devono restituire `true` e tutte le condizioni di eccezione devono restituire `false` prima di eseguire qualsiasi azione sulla regola.

**Console**: In [!DNL Query Service], la console fornisce informazioni sullo stato e sul funzionamento di una query. Nella console viene visualizzato lo stato della connessione a [!DNL Query Service], le operazioni di query in esecuzione ed eventuali messaggi di errore derivanti da tali query.

**Etichette per contratti (&quot;C&quot;)**: le etichette di utilizzo dei dati del contratto (&quot;C&quot;) vengono utilizzate per categorizzare i dati che hanno obblighi contrattuali o sono relativi ai criteri di governance dei dati della tua organizzazione.

**CPRA**: Il [[!DNL California Consumer Privacy Rights Act (CPRA)]](https://cppa.ca.gov/regulations/consumer_privacy_act.html) espande e modifica parti della [!DNL California Consumer Privacy Act (CCPA)]. Il [!DNL CPRA] Stabilisce una nuova base per la privacy dei dati dei consumatori in California aumentando i diritti dei consumatori e ampliando il tipo di dati coperti da una definizione più ampia di informazioni personali sensibili. Inoltre, la [!DNL CPRA] Ha istituito la California Privacy Protection Agency, una nuova agenzia dedicata all’implementazione e all’applicazione delle norme sulla privacy dei dati.

**Etichetta contratto C1**: A `C1` etichetta utilizzo dati contratto specifica che i dati possono essere esportati da Adobe Experience Cloud solo in un modulo aggregato senza includere identificatori individuali o di dispositivo. Ad esempio, dati provenienti dai social network.

**Etichetta contratto C2**: A `C2` etichetta utilizzo dati contratto specifica i dati che non possono essere esportati a terzi. Alcuni fornitori di dati hanno clausole nei loro contratti che vietano l’esportazione di dati da dove sono stati raccolti originariamente. Ad esempio, i contratti per i social network spesso limitano il trasferimento dei dati che ricevi da loro. C2 è più restrittivo di C1, che richiede solo aggregazione e dati anonimi.

**Etichetta contratto C3**: A `C3` etichetta utilizzo dati contratto specifica dati che non possono essere combinati o altrimenti utilizzati con informazioni direttamente identificabili. Alcuni fornitori di dati hanno clausole nei loro contratti che vietano la combinazione o l’uso di tali dati con informazioni direttamente identificabili. Ad esempio, i contratti per i dati provenienti da reti di annunci, server di annunci e fornitori di dati di terze parti spesso includono divieti contrattuali specifici sull’utilizzo di dati direttamente identificabili.

**Etichetta contratto C4**: A `C4` etichetta utilizzo dati contratto specifica che i dati non possono essere utilizzati per il targeting di annunci o contenuti, né sul sito né tra siti diversi. C4 è l&#39;etichetta più restrittiva in quanto include le etichette C5, C6 e C7.

**Etichetta contratto C5**: A `C5` etichetta utilizzo dati contratto specifica che i dati non possono essere utilizzati per il targeting tra siti di contenuti o annunci basati su interessi. Il targeting basato sull’interesse, o personalizzazione, si verifica se vengono soddisfatte le tre condizioni seguenti: i dati raccolti sul sito vengono utilizzati per trarre conclusioni sull’interesse di un utente; vengono utilizzati in un altro contesto, ad esempio su un altro sito o un’altra app; e vengono utilizzati per selezionare quali contenuti o annunci vengono distribuiti in base a tali conclusioni.

**Etichetta contratto C6**: A `C6` etichetta di utilizzo dei dati del contratto specifica che i dati non possono essere utilizzati per il targeting degli annunci nel sito. Il targeting degli annunci nel sito include la selezione e la consegna di annunci sui siti web o sulle app della tua organizzazione o per misurare la consegna e l’efficacia di tali annunci. Ciò include l’utilizzo di dati sul sito raccolti in precedenza che mostrano l’interesse degli utenti a selezionare annunci, elaborare dati su quali annunci sono stati mostrati, quando e dove sono stati mostrati e se gli utenti hanno intrapreso azioni relative all’annuncio, ad esempio selezionando un annuncio o effettuando un acquisto.

**Etichetta contratto C7**: A `C7` etichetta utilizzo dati contratto specifica che i dati non possono essere utilizzati per il targeting del contenuto nel sito. Il targeting dei contenuti nel sito include la selezione e la distribuzione dei contenuti sui siti web o sulle app della tua organizzazione o per misurare la distribuzione e l’efficacia di tali contenuti. Ciò include informazioni raccolte in precedenza sull’interesse degli utenti a selezionare il contenuto, sull’elaborazione dei dati su quale contenuto è stato visualizzato, sulla frequenza o la durata della visualizzazione, su quando e dove è stato visualizzato e se gli utenti hanno intrapreso azioni relative al contenuto, inclusa ad esempio la selezione del contenuto.

**Etichetta contratto C8**: A `C8` etichetta utilizzo dati contratto specifica che i dati non possono essere utilizzati per la misurazione dei siti web o delle app della tua organizzazione. Questo non include il targeting basato sugli interessi, che è la raccolta di informazioni sull’utilizzo di questo servizio per personalizzare successivamente contenuti e/o pubblicità in altri contesti.

**Etichetta contratto C9**: A `C9` l’etichetta di utilizzo dei dati del contratto specifica che i dati non possono essere utilizzati nei flussi di lavoro di data science. Alcuni contratti includono divieti espliciti sui dati utilizzati per la scienza dei dati. A volte queste sono formulate in termini che vietano l’uso di dati per l’intelligenza artificiale (IA), l’apprendimento automatico (ML) o la modellazione.

**Etichetta contratto C10**: A `C10` etichetta di utilizzo dei dati del contratto specifica che i dati non possono essere utilizzati per l&#39;attivazione dell&#39;identità unita. Alcuni criteri di utilizzo dei dati limitano l’utilizzo di dati di identità uniti per la personalizzazione. Il `C10` l’etichetta viene applicata automaticamente ai segmenti se i criteri di unione utilizzano l’opzione &quot;private graph&quot; (grafico privato).

**Colonna Data di creazione**: quando si specificano dati di terze parti tramite una connessione di origine, è possibile selezionare la colonna Data di creazione. Quando si seleziona la strategia di salvataggio di accodamento e lo schema del set di dati contiene più campi di data, è necessario scegliere dallo schema disponibile per specificare una colonna chiave Data di creazione. L’opzione Data di creazione non è disponibile quando è selezionata la strategia di salvataggio di sovrascrittura.

**Crea tabella come selezionata**: Create Table as Select (CTAS) è un comando SQL che, se eseguito come parte di una query SQL completa e valida, fornisce istruzioni [!DNL Query Service] per mantenere i risultati della query in un set di dati. È possibile creare una nuova serie di risultati, sovrascrivere i risultati precedenti o aggiungere ai risultati precedenti.

**Dati intersito**: i dati intersito sono la combinazione di dati provenienti da diversi siti, inclusa una combinazione di dati nel sito e dati esterni al sito o una combinazione di dati provenienti da diverse origini esterne al sito.

**Azione di marketing di targeting tra siti**: azione di marketing che utilizza i dati per il targeting di annunci tra siti. La combinazione di dati provenienti da diversi siti, compresa una combinazione di dati nel sito e dati esterni al sito o una combinazione di dati provenienti da diverse fonti esterne al sito, è definita dati intersito. I dati tra siti vengono generalmente raccolti ed elaborati per trarre conclusioni sugli interessi dei clienti.

**Spazio dei nomi identità personalizzato**: gli spazi dei nomi di identità personalizzati possono essere creati dalla tua organizzazione per rappresentare le identità per un’organizzazione specifica o un caso di business.

**Etichette personalizzate**: le etichette di utilizzo dei dati personalizzate ti consentono di creare e applicare etichette specifiche ai campi di dati che soddisfano esigenze aziendali specifiche.

**IA per l’analisi dei clienti**: IA per l’analisi dei clienti è un servizio intelligente basato su Adobe Sensei che arricchisce i profili dei clienti con dati di propensione basati sull’intelligenza artificiale e potenzia la segmentazione dei clienti e le attività di targeting.

## D

**Giornaliero**: nel contesto delle esportazioni di file pianificate, pianifica le esportazioni di file complete o incrementali una volta al giorno, ogni giorno, dalla data di inizio alla data di fine all’ora specificata dall’utente.

**Dizionario dati**: nel contesto dei tag, un dizionario di dati (noto anche come mappa di dati) è un insieme di elementi di dati definiti all’interno di una proprietà.

**Elemento dati**: nel contesto dei tag, un elemento dati è un puntatore utilizzato all’interno di regole ed estensioni per puntare a dati specifici esistenti sul dispositivo client.

**Acquisizione dei dati**: l’acquisizione dei dati è il processo di aggiunta di dati da un’origine all’Experience Platform. I dati possono essere acquisiti in Platform in diversi modi, tra cui streaming, batch o aggiunti tramite connettori di origine.

**Livello dati**: nel contesto dei tag, un livello dati è una struttura di dati esistente sul dispositivo client che contiene metadati sul contesto in cui viene visualizzata una pagina o una schermata.

**Governance dei dati**: la governance dei dati include le strategie e le tecnologie utilizzate per garantire che i dati siano conformi alle normative e alle politiche organizzative relative all’utilizzo dei dati.

**Partner di integrazione dei dati**: i partner di integrazione dei dati semplificano e automatizzano il caricamento e la trasformazione di enormi volumi di dati da oltre 200 origini all’Experience Platform senza scrivere codice.

**Etichette set di dati**: è possibile aggiungere etichette di utilizzo dei dati ai set di dati. Tutti i campi all’interno di tale set di dati ereditano le etichette del set di dati.

**Data Science Workspace**: [!DNL Data Science Workspace] all’interno di Experienci Platform consente ai clienti di creare modelli di apprendimento automatico utilizzando i dati nelle applicazioni Platform e Adobe per creare segmenti intelligenti, generare informazioni approfondite e fornire previsioni, consentendo di migliorare notevolmente le esperienze digitali degli utenti finali.

**Origine dati**: un’origine dati è un’origine dei dati designata dall’utente. Esempi di un’origine dati sono un’app mobile, eventi di profilo e/o esperienza, eventi di profilo del sito web o un CRM.

**Amministratore dati**: l’amministratore dei dati è la persona responsabile della gestione, della supervisione e dell’applicazione delle risorse dati di un’organizzazione. Un data steward garantisce inoltre che i criteri di governance dei dati siano salvaguardati e mantenuti in modo da essere conformi alle normative e ai criteri organizzativi governativi.

**Flusso di dati**: un flusso di dati è un set o una raccolta di messaggi che condividono lo stesso schema e sono inviati dalla stessa origine.

**Tipo di dati**: un tipo di dati è una risorsa XDM riutilizzabile che definisce un campo di tipo oggetto contenente più proprietà in una rappresentazione gerarchica.

**Etichette di utilizzo dati**: le etichette di utilizzo dei dati ti consentono di categorizzare i dati che riflettono considerazioni relative alla privacy e condizioni contrattuali conformi alle normative e alle politiche aziendali. Le etichette di utilizzo dei dati aggiunte a un set di dati vengono ereditate o applicate a tutti i campi all’interno di tale set di dati. Le etichette di utilizzo dei dati possono essere applicate direttamente ai campi.

**Flusso di dati**: un flusso di dati è una pipeline virtuale di dati che fluisce in Platform da un’origine e ne esce verso le destinazioni.

**Esecuzione del flusso di dati**: un’esecuzione del flusso di dati è un flusso di dati che arriva in Experienci Platform in base a una pianificazione specificata dall’utente.

**Set di dati**: un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e dei campi (righe).

**ID set di dati**: identificatore generato da un Adobe per un set di dati acquisito.

**Output del set di dati**: l’output del set di dati fornisce un meccanismo per determinare quale opzione &quot;Crea tabella come selezione&quot; verrà utilizzata per una particolare [!DNL Query Service] esegui.

**Chiave di deduplicazione**: chiave primaria definita dall’utente che determina l’identità in base alla quale gli utenti desiderano deduplicare i propri profili.&#x200B;

**Colonna delta**: una colonna delta consente di selezionare un campo dati di origine per rappresentare una marca temporale per l’acquisizione incrementale.

**Strategia di salvataggio delta**: la strategia di salvataggio delta è un’opzione per acquisire dati di terze parti tramite una connessione di origine. L’opzione consente all’utente di specificare che le righe di dati di origine nuove o modificate vengono acquisite in Experienci Platform. Alla fine del set di dati vengono aggiunte nuove righe e quelle modificate vengono aggiornate nel set di dati in Experienci Platform.

**Descrittore**: in Experience Data Model (XDM), un descrittore è un set aggiuntivo di metadati relativi allo schema che descrive un comportamento specifico per un campo. I descrittori possono essere utilizzati da Experienci Platform per comprendere il comportamento dello schema desiderato, ad esempio la relazione tra due schemi.

**Destinazione**: una destinazione è un termine generale per qualsiasi endpoint, ad esempio un’applicazione di Adobe, una piattaforma pubblicitaria, un servizio di archiviazione cloud o un servizio di marketing, in cui viene attivato e distribuito un pubblico.

**Categoria di destinazione**: una categoria di destinazione è un raggruppamento di destinazioni che hanno caratteristiche simili.

**Catalogo di destinazione**: un catalogo di destinazione è un elenco delle destinazioni disponibili in Experienci Platform.

**Regole di chiamata diretta**: nel contesto dei tag, una regola di chiamata diretta è una regola che viene eseguita quando viene chiamata direttamente dalla pagina, ignorando i sistemi di rilevamento degli eventi e di ricerca.

**Nome visualizzato**: in Experience Data Model (XDM), un nome visualizzato è un nome descrittivo per un campo visualizzato nell’interfaccia utente.

## E

**Offerta idonea**: un’offerta idonea può essere offerta in modo coerente a un profilo, in quanto soddisfa i vincoli definiti a monte.

**Regole di idoneità**: In [!DNL Offer Decisioning], le regole di idoneità vengono applicate a un profilo correlato a vincoli di calendario, pianificazione e limite.

**Azione di marketing di targeting e-mail**: azione di marketing che utilizza i dati nelle campagne di targeting e-mail.

**Codice di incorporamento**: nel contesto dei tag, il codice di incorporamento è un tag script inserito nel HTML in un sito o in un ambiente. Il codice di incorporamento indica al browser dove recuperare la build.

**Enumerazione**: un’enumerazione (enum) è un campo XDM vincolato a un set di valori predefiniti.

**Ambiente**: nel contesto dei tag, un ambiente è un set di istruzioni di distribuzione che specifica la consegna dell’host e il formato di file di una build. Prima di poter essere generata, una libreria deve essere associata a un ambiente.

**Diagnostica degli errori**: la diagnostica degli errori consente la generazione di messaggi di errore dettagliati per i batch acquisiti. La soglia di errore consente di configurare la percentuale di errori accettabili prima che un batch abbia esito negativo.

**Evento**: nel contesto dei tag, un evento è un tipo specifico di componente regola, ossia un trigger che si verifica su un dispositivo client per iniziare l’esecuzione di una regola.

**Entità evento**: nel contesto della modellazione dei dati, le entità evento rappresentano concetti relativi alle azioni che un cliente può intraprendere, agli eventi di sistema o a qualsiasi altro concetto in cui puoi voler tenere traccia delle modifiche nel tempo. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati su [!DNL XDM ExperienceEvent] classe.

**Eventi**: gli eventi sono dati comportamentali associati a un profilo.

**Experience Data Model (XDM)** [!DNL Experience Data Model] (XDM) è un framework open-source che utilizza schemi standard per unificare i dati da utilizzare con le applicazioni Experienci Platform e Adobe Experience Cloud. XDM standardizza la struttura dei dati, velocizza e semplifica il processo di acquisizione di informazioni da enormi quantità di dati.

**Esperimento**: un esperimento è il processo di creazione di un modello addestrato addestrando l’istanza con una porzione campione di dati di produzione live. È diverso da un modello addestrato che viene testato in base a un set di dati di prova di sospensione. Questo è anche diverso dal concetto di esperimento in alcuni framework di apprendimento automatico dove in realtà significa un progetto di modellazione campione.

**Evento esperienza**: un evento esperienza rappresenta un’istantanea del sistema quando si verifica un’interazione o un evento correlato a un’esperienza del cliente. Gli Eventi di esperienza sono record di fatti immutabili di ciò che è accaduto e rappresentano ciò che è accaduto senza aggregazione o interpretazione. In Experience Data Model (XDM), questo concetto viene acquisito da [!DNL XDM ExperienceEvent] classe.

**Esporta file completo**: file di esportazione contenente un’istantanea completa di tutte le qualifiche di profilo per il segmento selezionato.

**Esporta file incrementali**: serie di file esportati in cui il primo file è uno snapshot completo di tutte le qualifiche di profilo per il segmento selezionato e i file successivi sono qualifiche di profilo incrementali dall’esportazione precedente.

**Estensione**: nel contesto dei tag, un’estensione è un pacchetto di funzionalità aggiunte a una proprietà tag. Un’estensione si concentra solitamente su una particolare soluzione di marketing o analisi e fornisce gli strumenti necessari per distribuire tale tecnologia in un ambiente client.

**Pacchetto di estensione**: nel contesto dei tag, un pacchetto di estensione è un file ZIP creato e caricato da uno sviluppatore di estensioni che fornisce tutto ciò che è necessario agli utenti di tag per installare l’estensione all’interno della propria proprietà. Un pacchetto di estensione contiene un manifesto che specifica le informazioni sull’estensione, le proprietà HTML/JavaScript necessarie agli utenti finali per configurare il comportamento dell’estensione tag e l’eseguibile JavaScript consegnato all’ambiente client (se necessario).

## F

**Offerte di fallback**: un’offerta di fallback è l’offerta predefinita che viene visualizzata se un utente finale non è idoneo per nessuna delle offerte della raccolta utilizzata.

**Mappatura delle funzioni**: la mappatura delle funzioni si riferisce al processo di mappatura delle funzioni dai dati alle funzioni di input e di destinazione richieste da un modello di apprendimento automatico.

**Campo**: un campo è l’elemento di livello più basso di un set di dati, come definito dallo schema XDM del set di dati. Ogni campo ha un nome a scopo di riferimento e un tipo per indicare il tipo di dati che contiene. I tipi di campo possono includere (ma non sono limitati a) numero intero, numero, stringa, booleano e oggetto.

**Gruppo di campi**: consulta &quot;Gruppo di campi schema&quot;.

**Etichette campo**: le etichette dei campi sono etichette di governance dei dati ereditate da un set di dati o applicate direttamente a un campo.

**Nome campo**: un nome di campo viene utilizzato per fare riferimento al valore di un campo nelle query e nei servizi a valle.

**Frequenza**: In [!DNL Query Service], frequenza determina la frequenza con cui verrà eseguita una query pianificata ricorrente.

## G

**Recinto geografico**: un recinto geografico è un confine geografico virtuale, definito dalla tecnologia GPS o RFID, che consente al software di attivare una risposta quando un dispositivo mobile entra o esce da una determinata area.

**RGPD (Regolamento generale sulla protezione dei dati)**: il Regolamento generale sulla protezione dei dati (RGPD) è un quadro giuridico che definisce le linee guida per la raccolta e il trattamento di informazioni personali di persone all’interno dell’Unione europea (UE). Il RGPD stabilisce i principi per la gestione dei dati e i diritti dei singoli e copre tutte le aziende che trattano dati di cittadini dell’UE.

**Guardrail**: i guardrail sono soglie che forniscono indicazioni sull’utilizzo di dati e sistemi, sull’ottimizzazione delle prestazioni e sulla necessità di evitare errori o risultati imprevisti in Adobe Experience Platform. I guardrail possono fare riferimento all’utilizzo o al consumo di dati e all’elaborazione in relazione alle licenze concesse.

## H

**HIPAA**: Il [[!DNL Health Insurance Portability and Accountability Act (HIPAA)]](https://www.hhs.gov/hipaa/index.html) è una legge federale degli Stati Uniti creata per migliorare l&#39;efficienza dell&#39;assistenza sanitaria, migliorare la portabilità dell&#39;assicurazione sanitaria e proteggere la privacy dei pazienti e dei membri del piano sanitario. In base all&#39;HIPAA, le persone hanno il diritto di accedere alle proprie informazioni e di modificarle, nonché di ottenere copie delle proprie cartelle cliniche o informazioni sulla salute. Le entità coperte e i soci d&#39;affari delle entità coperte devono seguire le normative HIPAA.

**Host**: nel contesto dei tag, un host specifica la posizione, il dominio e le credenziali utente necessari affinché il sistema distribuisca una build.

**Ogni ora**: nel contesto di esportazioni di file pianificate, pianifica le esportazioni di file incrementali ogni 3, 6, 8 o 12 ore.

## I

**Identità**: un’identità è un identificatore che rappresenta in modo univoco un singolo cliente, ad esempio un ID cookie, un ID dispositivo o un ID e-mail.

**Campi di identità**: i campi di identità sono campi XDM utilizzati per unire informazioni su singoli clienti provenienti da più origini dati. È necessario definire una singola identità primaria affinché lo schema possa essere abilitato per l’utilizzo in Real-Time Customer Profile.

**Etichette di identità (&quot;I&quot;)**: le etichette di utilizzo dei dati di identità (&quot;I&quot;) vengono utilizzate per categorizzare i dati che possono identificare o contattare una persona specifica.

**Grafo identità**: un grafo di identità è una mappa delle relazioni tra identità collegate e unite esistenti per un singolo cliente. Ogni grafo di identità viene aggiornato quasi in tempo reale con l’attività del cliente. La struttura comune delle relazioni di identità nei dati è rappresentata da [!UICONTROL Private Graph], che funge da blueprint strutturale per ogni singolo grafico di identità.

**Spazio dei nomi dell’identità**: uno spazio dei nomi identità definisce il contesto di un identificatore, ad esempio un indirizzo e-mail o un ID del sistema di gestione delle relazioni con i clienti.

**Servizio identità**: [!DNL Experience Platform Identity Service] consente di creare e gestire i tipi di identità, consentendo di collegare le identità dei clienti tra dispositivi e canali diversi. La capacità del servizio di collegare le identità consente a Real-Time Customer Profile di fornire una rappresentazione completa di ogni singolo cliente.

**Unione identità**: l’unione di identità è il processo di identificazione dei frammenti di dati e di loro unione per formare un record di profilo completo.

**Simbolo di identità**: un simbolo di identità è un’abbreviazione di uno spazio dei nomi dell’identità che può essere utilizzato come riferimento nelle API.

**Valore identità**: un valore di identità, combinato con uno spazio dei nomi di identità, è un identificatore che rappresenta un individuo, un’organizzazione o una risorsa univoca. Quando si abbinano i dati del record tra i frammenti di profilo, lo spazio dei nomi e il valore dell’identità devono corrispondere.

**Etichetta utilizzo dati I1**: Il `I1` l’etichetta di utilizzo dei dati viene utilizzata per classificare i dati che possono identificare o contattare direttamente una persona specifica anziché un dispositivo.

**Etichetta utilizzo dati I2**: Il `I2` l’etichetta di utilizzo dei dati viene utilizzata per classificare i dati che possono essere utilizzati in combinazione con altri dati per identificare o contattare indirettamente una persona specifica.

**Organizzazione IMS**: un’organizzazione IMS (a volte indicata come organizzazione IMS) è il nome utilizzato per identificare un’azienda o un gruppo specifico all’interno di un’azienda nei vari prodotti di Adobe. Gli amministratori possono configurare e gestire l’accesso e le autorizzazioni delle funzioni per gli utenti di un’organizzazione.

**Acquisizione**: consulta acquisizione di dati.

**Pianificazione di acquisizione**: una pianificazione dell’acquisizione fornisce opzioni basate sul tempo per l’acquisizione da un’origine all’Experience Platform.

**Funzione di input**: una funzione di input viene specificata nella mappatura della funzione e utilizzata da un modello di apprendimento automatico per effettuare previsioni.

**[!DNL Intelligent Services]**: [!DNL Intelligent Services] come [!DNL Attribution AI] e [!DNL Customer AI] sono modelli basati sull’apprendimento automatico e sull’intelligenza artificiale che richiedono l’esecuzione e il funzionamento di Experienci Platform (o di applicazioni basate su Platform, come Adobe Real-time Customer Data Platform).

**Targeting o personalizzazione basata sugli interessi**: il targeting basato sugli interessi, noto anche come personalizzazione, si verifica se vengono soddisfatte le tre condizioni seguenti:

1. I dati raccolti sul sito vengono utilizzati per trarre conclusioni sull’interesse di un utente.
1. I dati vengono utilizzati in un altro contesto, ad esempio in un altro sito o in un’altra app (fuori dal sito).
1. I dati vengono utilizzati per selezionare il contenuto o gli annunci da distribuire in base a tali inferenze.

## J

**[!DNL JupyterLab]**: interfaccia open-source basata su Web per Project [!DNL Jupyter] che è integrato nell’interfaccia utente di Platform.

**[!DNL Jupyter Notebook]**: integrato con JupyterLab, Jupyter Notebooks consente di eseguire operazioni di pulizia e trasformazione dei dati, simulazione numerica, modellazione statistica, visualizzazione dei dati, apprendimento automatico e altro ancora sui dati Experienci Platform in diversi linguaggi, come Python, Scala e PySpark.

## K

## L

**LGPD**: Il [[!DNL Lei Geral de Proteção de Dados (LGPD)]](https://gdpr.eu/gdpr-vs-lgpd/) mira a regolamentare il trattamento dei dati personali di tutte le persone fisiche o fisiche in Brasile. L&#39;LGPD conferisce ai cittadini brasiliani il diritto di accedere ai propri dati personali e di cancellarli, di sapere se i propri dati personali vengono venduti o divulgati (e a chi), e il diritto di non acconsentire alla vendita dei propri dati a terzi.

**Libreria**: nel contesto dei tag, una libreria è un set di regole business che contiene istruzioni sul comportamento della libreria di tag nel dispositivo client.

**Entità di ricerca**: nel contesto della modellazione dei dati, le entità di ricerca rappresentano concetti che possono essere correlati a una singola persona, ma non possono essere utilizzati direttamente per identificarla. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati su classi XDM (Experience Data Model) personalizzate e collegate a un’entità profilo tramite un [relazione schema](../xdm/tutorials/relationship-ui.md).

## M

**Apprendimento automatico (ML)**: l’apprendimento automatico è il campo di studio che consente ai computer di imparare senza essere esplicitamente programmati.

**Modello di apprendimento automatico**: un modello di apprendimento automatico è un’istanza di una ricetta di apprendimento automatico che viene addestrata utilizzando dati e configurazioni storici per risolvere un caso d’uso aziendale. In Adobe Experience Platform Data Science Workspace, i modelli di apprendimento automatico sono chiamati ricette.

**Attributo obbligatorio**: casella di controllo abilitata dall’utente che assicura che tutti i record di profilo contengano l’attributo selezionato. Ad esempio: tutti i profili esportati contengono un indirizzo e-mail.

**Mappatura**: la mappatura dei dati è il processo di mappatura dei campi dati di origine ai campi di destinazione correlati in una destinazione.

**Azione di marketing**: nel framework di governance dei dati, un’azione di marketing (nota anche come caso di utilizzo di marketing) è un’azione eseguita da un consumatore di dati Experience Platform, per la quale è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati.

**Metodo di unione**: quando si definisce un criterio di unione utilizzando l’interfaccia utente di Platform, il metodo di unione specifica il modo in cui assegnare la priorità ai frammenti di dati in caso di conflitto. Quando si utilizza l’API Real-Time Customer Profile per definire un criterio di unione, il metodo di unione viene determinato utilizzando `attributeMerge` oggetto.

**Criterio di unione**: i criteri di unione sono regole che Experienci Platform utilizza per determinare in che modo i frammenti di dati dei clienti provenienti da più origini verranno combinati per creare un singolo profilo. Quando si verifica un conflitto di dati, il criterio di unione determina i dati a cui assegnare la priorità per l’inclusione nel profilo.

**MHMDAa**: Il [[!DNL Washington My Health My Data Act]](https://app.leg.wa.gov/RCW/default.aspx?cite=19.373&amp;full=true) migliora i diritti dei consumatori alla privacy in relazione ai loro dati sanitari. Impone la divulgazione, il consenso dei consumatori e i diritti di cancellazione per i dati sanitari e vieta la vendita di dati sanitari senza autorizzazione. Inoltre, la legge rende illegale l&#39;uso di recinti geografici intorno alle strutture sanitarie.

**Mixin**: consulta &quot;Gruppo di campi schema&quot;.

**Modulo**: nel contesto dei tag, un modulo è uno snippet di JavaScript eseguibile fornito da un’estensione, che esegue azioni in un ambiente client senza dover creare una regola.

## N

**[!DNL New Zealand Privacy Act]**: Il [[!DNL New Zealand Privacy Act]](https://www.privacy.org.nz/privacy-act-2020/privacy-principles/) controlla come le agenzie possono raccogliere, utilizzare, divulgare, archiviare e dare accesso ai dati personali di cittadini e organizzazioni della Nuova Zelanda. Nel 2020 l&#39;ultima versione della legge ha introdotto aggiornamenti significativi a tali leggi sulla privacy, tra cui nuove infrazioni, aumento delle ammende, notifiche obbligatorie per le violazioni dei dati e aumento dei poteri del commissario per la privacy.

**Sandbox non di produzione**: le sandbox non di produzione sono in genere utilizzate per esperimenti di sviluppo, test o test. A differenza delle sandbox di produzione, le sandbox non di produzione possono essere reimpostate ed eliminate.

**[!DNL Notebooks]**: [!DNL Notebooks] sono creati utilizzando [!DNL Jupyter Notebook] e possono essere eseguiti per eseguire l’analisi dei dati.

## O

**Offerta**: un’offerta è un messaggio di marketing contenente una proposta commerciale o di vendita per un (potenziale) cliente. Le offerte spesso dispongono di regole specifiche che determinano chi è idoneo a visualizzarle o riceverle.

**[!DNL Offer Decisioning]**: [!DNL Offer Decisioning] consente agli addetti al marketing di gestire regole e modelli di proposte di offerta specifici per interagire con gli utenti finali in base ai dati raccolti tra canali e applicazioni.

**Libreria di offerte**: la libreria di offerte è una libreria centrale utilizzata per gestire offerte personalizzate e di fallback, regole di decisione e attività.

**Azione di marketing di personalizzazione nel sito**: azione di marketing che utilizza i dati per la personalizzazione dei contenuti nel sito. Per personalizzazione nel sito si intende qualsiasi dato utilizzato per trarre conclusioni sugli interessi degli utenti e per selezionare i contenuti o gli annunci da distribuire in base a tali conclusioni.

**Azione di marketing di targeting nel sito**: azione di marketing che utilizza i dati per gli annunci nel sito, inclusa la selezione e la consegna di annunci sui siti web o sulle app della tua organizzazione, o per misurare la consegna e l’efficacia di tali annunci.

**Una volta**: nel contesto di esportazioni di file pianificate, pianifica un’esportazione di file una tantum, su richiesta, completa.

**Sovrascrivi strategia di salvataggio**: la strategia di salvataggio &quot;Sovrascrivi&quot; è un’opzione per acquisire dati di terze parti tramite una connessione, in cui puoi specificare se i dati acquisiti verranno sovrascritti in una pianificazione specificata.

## P

**Acquisizione parziale**: l’acquisizione parziale consente l’acquisizione di record validi di dati batch all’interno di una soglia di errore specificata. È possibile scaricare o accedere alla diagnostica degli errori per i record non riusciti in [!UICONTROL Monitorare] o [!UICONTROL Sorgenti] panoramica dell’esecuzione del flusso di dati.

**File Parquet**: un file Parquet è un formato di file di archiviazione a colonne con strutture di dati nidificate complesse. I file Parquet sono necessari per aggiungere dati per popolare un set di dati di schema.

**PDPA**: Il [[!DNL Personal Data Protection Act (PDPA)]](https://www.pdpc.gov.sg/Overview-of-PDPA/The-Legislation/Personal-Data-Protection-Act) è stata introdotta per tutelare i proprietari di dati thailandesi dalla raccolta, dall&#39;utilizzo o dalla divulgazione illeciti dei loro dati personali. Ispirandosi al regolamento generale sulla protezione dei dati (RGPD) dell&#39;Unione Europea, il regolamento garantisce ai cittadini thailandesi il diritto di richiedere l&#39;accesso o la cancellazione dei propri dati personali memorizzati.

<!-- Not yet released
**PDPD**: The [[!DNL Personal Data Protection Decree] (PDPD) 
-->

**Offerte personalizzate**: un’offerta personalizzata è un messaggio di marketing personalizzabile basato su regole e vincoli di idoneità.

**Posizionamenti**: il posizionamento corrisponde a posizione e contesto in cui un’offerta viene mostrata a un utente finale.

**Area di lavoro Criteri**: area di lavoro nell’interfaccia utente di Platform che consente agli amministratori dei dati di visualizzare e gestire le etichette e i criteri di utilizzo dei dati per la tua organizzazione.

**Policy**: un criterio di utilizzo dei dati è una regola che specifica le azioni di marketing soggette a restrizioni in base all’applicazione delle etichette di utilizzo applicate ai dati di Platform.

**Applicazione dei criteri**: consente di applicare i criteri di utilizzo dei dati con le azioni di marketing applicate per impedire operazioni sui dati che costituiscono violazioni dei criteri all’interno di un’organizzazione.

**Chiave primaria**: una chiave primaria è una designazione in uno schema che identifica in modo univoco tutti i record.

**Priorità**: In [!DNL Offer Decisioning], priorità viene utilizzato per classificare le offerte che soddisfano tutti i vincoli, come idoneità, calendario e limiti.

**Grafo di identità privata**: il grafico dell’identità privata (talvolta denominato grafico privato) è una mappa privata delle relazioni tra identità collegate e unite, basata sui dati di prime parti e visibile solo all’organizzazione. Esiste un solo grafico privato per ogni organizzazione e funge da blueprint strutturale per i singoli grafici di identità generati per ogni cliente che interagisce con il tuo marchio.

**Profilo di prodotto**: i profili di prodotto consentono agli amministratori di concedere l’accesso utente a tutti i servizi associati ad Experienci Platform o a un sottoinsieme di essi.

**Sandbox di produzione**: una sandbox di produzione è una sandbox destinata all’utilizzo nell’ambiente di produzione. A differenza delle sandbox non di produzione, le sandbox di produzione non possono essere reimpostate o eliminate.

**Profilo**: da non confondere con Real-Time Customer Profile as a service, un profilo è una rappresentazione completa di un singolo cliente, costruita sulla base di dati di record e serie temporali uniti provenienti da più origini.

**Accesso al profilo**: Il `/entities` L’endpoint nell’API del profilo cliente in tempo reale consente di accedere ai dati dei record e agli eventi della serie temporale nell’archivio dati del profilo. Vedere anche: Entità profilo

**Dati profilo**: i dati del profilo si riferiscono a qualsiasi dato che si trova all’interno dell’archivio dati del profilo.

**Archivio dati profilo**: l’archivio dati Profile (talvolta denominato archivio profili) è un sistema di archiviazione dati separato dal data lake, utilizzato da Real-Time Customer Profile per creare e memorizzare profili.

**Entità profilo**: le entità profilo rappresentano attributi relativi a una singola persona, in genere un cliente. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati su [!DNL XDM Individual Profile] classe. Vedi anche: Accesso al profilo

**Esportazione profilo**: [!DNL Profile] export è uno dei due tipi di destinazioni in Experienci Platform. [!DNL Profile] l’esportazione genera un file contenente profili e attributi e utilizza dati PII non elaborati con le e-mail per l’integrazione con le piattaforme di marketing e automazione delle e-mail.

**Frammento di profilo**: un frammento di profilo è costituito dalle informazioni di profilo per una sola identità presente nell’elenco delle identità esistenti per un particolare cliente.

**ID profilo**: un ID profilo è un identificatore generato automaticamente associato a un tipo di identità e rappresenta un profilo.

**Proprietà**: nel contesto dei tag, una proprietà è un contenitore per tutto ciò che è necessario per distribuire un set di tag.

## Q

**Query**: le query sono richieste di dati provenienti da tabelle di database.

**Editor query**: Query Editor è uno strumento per scrivere, convalidare e inviare istruzioni SQL in [!DNL Query Service].

## R

**Real-time Customer Data Platform**: Adobe Real-time Customer Data Platform (Real-Time CDP) riunisce dati noti e non noti dei clienti per creare profili cliente affidabili con integrazione semplificata, segmentazione intelligente e attivazione in tempo reale nel percorso di clienti digitali.

**Profilo cliente in tempo reale**: Real-Time Customer Profile (talvolta denominato Profile) fornisce una visualizzazione olistica di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i dati dei clienti in singoli profili, offrendo account fruibili e con marca temporale per ogni interazione con il cliente.

**Ricetta**: una ricetta è il termine di Adobe per una specifica di modello ed è un contenitore di livello superiore che rappresenta processi di apprendimento automatico specifici, algoritmi di intelligenza artificiale, logica di elaborazione e parametri di configurazione necessari per creare ed eseguire un modello addestrato e contribuire quindi a risolvere problemi di business specifici.

**Registra**: un record è dato che persiste come righe in un set di dati.

**Registra dati**: fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.

**Ricorrenza**: In [!DNL Query Service], una ricorrenza definisce se una query è pianificata per essere eseguita una sola volta o su base periodica.

**Rappresentazione**: In [!DNL Offer Decisioning], una rappresentazione è un’informazione utilizzata da un canale per visualizzare un’offerta, ad esempio posizione o lingua.

**Risorsa**: nel contesto dei tag, una risorsa è un termine generico che fa riferimento alle opzioni che l’utente di tag può configurare all’interno dell’ambiente client, tra cui estensioni, elementi dati e regole.

**Controllo degli accessi basato sul ruolo**: il controllo degli accessi basato sul ruolo consente agli amministratori di assegnare accesso e autorizzazioni agli utenti di Experienci Platform. Le autorizzazioni includono la possibilità di visualizzare e/o utilizzare funzioni di Experience Platform, ad esempio la creazione di sandbox, la definizione di schemi e la gestione di set di dati.

**Regola**: nel contesto dei tag, una regola è una raccolta di componenti che definiscono un set specifico di eventi, condizioni e azioni che devono essere raggruppati in modo logico.

**Componente regola**: nel contesto dei tag, i componenti regola sono gli eventi, le condizioni e le azioni che compongono una regola.

**Runtime**: Runtime specifica un ambiente di runtime per una ricetta di apprendimento automatico. [!DNL Python], R, [!DNL Spark]I runtime di, PySpark e Tensorflow consentono di inserire un URL in un’immagine Docker per un’origine di ricetta.

## S

**Dati di esempio**: i dati di esempio sono un’anteprima di un file di dati, in genere le prime 100 righe, che fornisce a un data scientist o a un ingegnere un’idea dello schema o dei dati presenti nel file di dati.

**Sandbox**: una sandbox è un costrutto virtuale che suddivide una singola istanza Platform in un ambiente virtuale separato, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

**Ripristino della sandbox**: con il ripristino di una sandbox vengono eliminati tutti i dati, inclusi dati, profili e segmenti all’interno di una sandbox. I ripristini delle sandbox possono influire sui dati connessi a destinazioni interne o esterne.

**Commutatore sandbox**: il controllo del commutatore sandbox in Experienci Platform consente agli utenti di spostarsi tra le sandbox a cui hanno accesso. Il passaggio a una sandbox modificherà tutto il contenuto e l’accesso alle funzioni in base alle autorizzazioni.

**Pianificazione**: una pianificazione è una specifica definita dall’utente sulla frequenza o la frequenza dell’acquisizione di dati da un’origine dati di terze parti a Adobe Experience Platform.

**Punteggio**: il punteggio è il processo di generazione di informazioni dai dati utilizzando un modello addestrato.

**Schema**: uno schema è un set di regole che rappresentano e convalidano la struttura e il formato dei dati. Uno schema è composto da una classe e da gruppi di campi facoltativi e viene utilizzato per creare set di dati e flussi di dati. Uno schema può includere attributi comportamentali, marche temporali, identità, definizioni di attributi, relazioni e altro ancora.

**Gruppo di campi schema**: in Experience Data Model (XDM), un gruppo di campi schema consente agli utenti di estendere i campi riutilizzabili per definire uno o più attributi da includere in uno schema.

**Libreria schemi**: la libreria di schemi contiene risorse XDM standard di settore rese disponibili da Adobe, nonché risorse personalizzate definite dalla tua organizzazione.

**Registro schema**: il registro dello schema fornisce un’interfaccia utente e un’API RESTful utilizzate per visualizzare e gestire tutte le risorse relative allo schema nella libreria degli schemi.

**Chiave di accesso segreta**: una chiave di accesso segreta è un [!DNL Amazon] Chiave S3 utilizzata insieme all’ID della chiave di accesso per firmare le richieste di AWS.

**Segmento**: un segmento è un insieme di regole che includono attributi e dati evento che qualificano diversi profili affinché diventino un pubblico.

**Generatore di segmenti**: Il [!DNL Segment Builder] è un ambiente di sviluppo visivo utilizzato per creare le definizioni dei segmenti. Funge da componente comune di tutte le applicazioni che utilizzano Experienci Platform Segmentation Service.

**Definizione del segmento**: una definizione di segmento è il set di regole utilizzato per descrivere le caratteristiche o il comportamento chiave di un pubblico target. Una volta concettualizzate, le regole delineate in una definizione di segmento vengono utilizzate per determinare i membri del pubblico idonei per un segmento.

**Metodo di valutazione del segmento**: esistono due metodi di valutazione dei segmenti: pianificato e on-demand. La valutazione pianificata consente una pianificazione ricorrente per l’esecuzione di un processo di esportazione in un momento specifico, mentre la valutazione on-demand comporta la creazione di un processo di segmentazione per generare immediatamente il pubblico.

**Esportazione segmento**: l’esportazione del segmento è uno dei due tipi di destinazioni di Experienci Platform. Con l’esportazione dei segmenti, puoi inviare i profili idonei e mappati sulla destinazione. Utilizza ID di segmenti e utenti e dati pseudonimi e in genere si integra con i social network e altre piattaforme di destinazione di contenuti multimediali digitali.

**ID segmento**: un ID segmento è un identificatore generato automaticamente associato a un segmento.

**Iscrizione al segmento**: l’iscrizione al segmento mostra di quali segmenti fa attualmente parte un profilo.

**Regole del segmento**: le regole del segmento definiscono le condizioni che determinano se un profilo è idoneo per un segmento.

**Segmentazione**: la segmentazione è il processo di suddivisione di un ampio gruppo di clienti, potenziali o consumatori in gruppi più piccoli che condividono attributi simili e rispondono in modo simile a specifiche strategie di marketing.

**Framework ML Sensei**: Sensei ML Framework è un framework di apprendimento automatico unificato (ML) che sfrutta i dati Experienci Platform per consentire ai data scientist di sviluppare servizi di intelligence basati sull’apprendimento automatico in modo più veloce, scalabile e riutilizzabile.

**Etichette sensibili (&quot;S&quot;)**: le etichette sensibili (&quot;S&quot;) vengono utilizzate per categorizzare i dati ritenuti sensibili, ad esempio i diversi tipi di dati comportamentali o geografici che desideri contrassegnare come sensibili.

**Servizi**: framework potente per rendere operativi i servizi di intelligenza artificiale e machine learning sfruttando Adobe Intelligent Services. I servizi forniscono esperienze cliente personalizzate in tempo reale o rendono operativi servizi intelligenti personalizzati.

**Azione di marketing per la personalizzazione di una singola identità**: azione di marketing che utilizza i dati per la personalizzazione del contenuto nel sito. Per personalizzazione nel sito si intende qualsiasi dato utilizzato per trarre conclusioni sugli interessi degli utenti e per selezionare i contenuti o gli annunci da distribuire in base a tali conclusioni.

**Etichetta utilizzo dati S1**: un `S1` l’etichetta di utilizzo dei dati viene utilizzata per classificare i dati che specificano la latitudine e la longitudine e che possono essere utilizzati per determinare la posizione esatta di un dispositivo.

**Etichetta utilizzo dati S2**: un `S2` l’etichetta di utilizzo dei dati viene utilizzata per classificare i dati che possono essere utilizzati per determinare un’area recintata in modo ampio.

**Sorgente**: sorgente è un termine generale per qualsiasi connettore di input in Platform. Vedere anche: Connettore di origine

**Attributo di origine**: un attributo di origine è un campo nel set di dati di origine. Gli attributi di origine sono mappati sui campi dello schema di destinazione.

**Catalogo di origine**: il catalogo di origine è l’elenco dei connettori di origine disponibili in Experienci Platform.

**Categoria di origine**: una categoria di origine è un raggruppamento di origini che hanno caratteristiche simili.

**Connettore sorgente**: i connettori di sorgenti (noti anche come sorgenti) consentono agli utenti di acquisire facilmente dati da più sorgenti, consentendo la strutturazione, l’etichettatura e il miglioramento dei dati utilizzando i servizi di Experience Platform. I dati possono essere acquisiti da diverse origini, ad esempio archiviazione basata su cloud, software di terze parti e sistemi di gestione delle relazioni con i clienti.

**Connessione streaming**: una connessione in streaming è un endpoint univoco fornito da Adobe e associato alla tua organizzazione per lo streaming di dati in Experienci Platform.

**Spazio dei nomi identità standard**: gli spazi dei nomi di identità standard sono spazi dei nomi di identità predefiniti forniti da Adobe, che rappresentano soluzioni standard del settore comunemente utilizzate per identificare i clienti.

**Acquisizione in streaming**: l’acquisizione in streaming ti consente di inviare in tempo reale dati da dispositivi lato client e lato server all’Experience Platform.

**Segmentazione in streaming**: la segmentazione in streaming è un processo continuo di selezione dei dati che aggiorna i segmenti in risposta all’attività dell’utente. Una volta creato e salvato un segmento, la definizione del segmento viene applicata ai dati in arrivo in [!DNL Real-Time Customer Profile]. Le aggiunte e le rimozioni dei segmenti vengono elaborate regolarmente, garantendo la rilevanza del pubblico di destinazione.

**Vista sistema**: la Vista sistema è una rappresentazione visiva dei set di dati di origine che passano attraverso [!DNL Real-Time Customer Profile] alle destinazioni.

## T

**Tag**: in Adobe Experience Platform, i tag forniscono gli strumenti necessari per distribuire, unificare e gestire le integrazioni di analisi, marketing e annunci pubblicitari necessarie per fornire ai clienti esperienze personalizzate su tutti i dispositivi client.

**Funzioni di destinazione**: nella mappatura delle feature, una feature di destinazione è la feature prevista da un modello.

**Dati delle serie temporali**: i dati delle serie temporali forniscono un’istantanea del sistema nel momento in cui un oggetto record ha eseguito un’azione, direttamente o indirettamente.

**Modello addestrato**: un modello addestrato rappresenta l’output eseguibile di un processo di apprendimento del modello, in cui un set di dati di addestramento è stato applicato all’istanza del modello. Un modello addestrato conserverà un riferimento a qualsiasi servizio web intelligente creato da esso. Un modello addestrato è adatto per il punteggio e la creazione di un servizio web intelligente.

**Token**: un token è un tipo di sicurezza di autenticazione a due fattori che può essere utilizzato per autorizzare l’utilizzo di servizi informatici con [!DNL Query Service].

## U

**UCPA**: Il [[!DNL Utah Consumer Privacy Act]](https://le.utah.gov/~2022/bills/static/SB0227.html) crea il diritto per un consumatore di sapere quali dati personali raccoglie un&#39;azienda, in che modo utilizza i suoi dati personali e se l&#39;azienda vende i suoi dati personali. I consumatori possono richiedere all&#39;azienda di cancellare o smettere di vendere i propri dati personali.

**Schema di unione**: uno schema di unione è un consolidamento di schemi che condividono la stessa classe e sono stati abilitati per [!DNL Real-Time Customer Profile]. Per un’organizzazione possono esistere più schemi di unione, ma può esistere un solo schema di unione per classe.

## V

**VCDPA**: Il [[!DNL Virginia Consumer Data Protection Act (VCDPA)]](https://lis.virginia.gov/cgi-bin/legp604.exe?212+sum+HB2307) fornisce ai residenti della Virginia (&quot;Consumatori&quot;) nuovi diritti sulla privacy dei dati, compreso il diritto di accesso, cancellazione e correzione dei dati personali. I consumatori hanno anche il diritto di non acconsentire alla vendita di dati personali, di non acconsentire alla profilazione basata su dati personali e al trattamento di finalità pubblicitarie personali.

## W

## X

**XDM**: consulta Experience Data Model (XDM).

**Evento decisione XDM**: XDM Decision Event è una classe basata su serie temporali utilizzata per acquisire osservazioni sul risultato e il contesto di un’attività decisionale. Ciò include informazioni su come è stata presa la decisione, quando si è verificata, quali opzioni sono state proposte (e scelte) e quale stato contestuale esisteva che ha influenzato la decisione o poteva essere osservato durante il processo decisionale.

**XDM ExperienceEvent**: XDM ExperienceEvent è una classe basata su serie temporali utilizzata per acquisire lo stato del sistema quando si è verificato un evento (o un set di eventi), inclusi il momento e l’identità del soggetto interessato. Vedi anche: Evento esperienza

**Profilo individuale XDM**: XDM [!DNL Individual Profile] è una classe basata su record che costituisce una singola rappresentazione degli attributi sia dei soggetti identificati che parzialmente identificati. I profili altamente identificati possono essere utilizzati per comunicazioni personali o impegni mirati e possono contenere informazioni personali dettagliate come nome, genere, data di nascita, posizione e informazioni di contatto, inclusi numeri di telefono e indirizzi e-mail.

**Sistema XDM**: il sistema XDM rappresenta il framework che operazionalizza gli schemi XDM da utilizzare nei servizi di Experience Platform a valle.

## S

## Z
