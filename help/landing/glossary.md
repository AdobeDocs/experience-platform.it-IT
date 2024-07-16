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

**Controllo degli accessi**: il controllo degli accessi basato sul ruolo consente agli amministratori di assegnare l&#39;accesso e le autorizzazioni agli utenti di Experience Platform. Le autorizzazioni includono la possibilità di visualizzare e/o utilizzare funzioni di Experience Platform, ad esempio la creazione di sandbox, la definizione di schemi e la gestione di set di dati.

**ID chiave di accesso**: un ID chiave di accesso è un identificatore univoco associato a una chiave di accesso segreta [!DNL Amazon] S3. L&#39;ID della chiave di accesso e la chiave di accesso segreta vengono utilizzati insieme per firmare le richieste di [!DNL Amazon Web Services] (AWS).

**Azione**: nel contesto dei tag, un&#39;azione è un tipo specifico di componente regola che definisce cosa deve accadere dopo che si è verificato un evento e le condizioni vengono valutate e passate.

**Attiva**: Attiva è l&#39;azione eseguita da un utente per mappare uno o più profili su una destinazione come [!DNL Oracle Eloqua], [!DNL Google] o [!DNL Salesforce Marketing Cloud].

**Attività**: in [!DNL Offer Decisioning] un&#39;attività contiene la logica utilizzata per determinare la selezione di un&#39;offerta.

**Amministratore**: uno o più utenti dell&#39;organizzazione che possono configurare e personalizzare le autorizzazioni, ad Experience Platform in Adobe Admin Console.

**Adobe Admin Console**: Adobe Admin Console fornisce una posizione centrale per la gestione delle adesioni ai prodotti Adobe e dell&#39;accesso per la tua organizzazione. Tramite la console, gli amministratori possono concedere a gruppi di utenti le autorizzazioni di accesso per varie funzionalità di Platform, ad esempio &quot;Gestisci set di dati&quot;, &quot;Visualizza set di dati&quot; o &quot;Gestisci profili&quot;.

**Adobe Experience Platform**: Adobe Experience Platform standardizza dati e contenuti a livello aziendale, fornendo profili di consumatori in tempo reale, abilitando la scienza dei dati e accelerando la velocità dei contenuti per stimolare la personalizzazione dell&#39;esperienza nel percorso del cliente.

**Adobe Experience Platform Query Service**: consente agli analisti di dati di eseguire query su eventi e profili da utilizzare in Analytics e nell&#39;apprendimento automatico. Con Query Service, data scientist e analisti possono richiamare tutti i loro set di dati memorizzati in Experience Platform (inclusi i dati comportamentali e i punti vendita, la gestione delle relazioni con i clienti e altro ancora) ed eseguire query su tali set di dati per rispondere a domande specifiche sui dati.

**Servizio di segmentazione di Adobe Experience Platform**: consente di creare segmenti e generare tipi di pubblico dai dati del profilo cliente in tempo reale. Questi tipi di pubblico possono quindi essere esportati nei propri set di dati all’interno del Data Lake.

**Adobe Intelligent Services**: i servizi intelligenti come Attribution AI e IA per l&#39;analisi dei clienti sono modelli basati sull&#39;apprendimento automatico e sull&#39;intelligenza artificiale appositamente creati e che richiedono l&#39;esecuzione e il funzionamento di Experience Platform.

**Adobe I/O**: Adobe I/O fa parte di Experience Platform e fornisce l&#39;accesso a tutto ciò di cui gli sviluppatori hanno bisogno per integrare, estendere e personalizzare Platform, inclusi API, eventi, console per sviluppatori e strumenti utili.

**Adobe Sensei**: Adobe Sensei è il framework di intelligence che attiva Experience Platform. Fornisce inoltre una serie di servizi di intelligenza artificiale che consentono ai brand di migliorare la loro capacità di fornire ai clienti esperienze personalizzate in tempo reale.

**Bucket Amazon S3**: [!DNL Amazon S3] bucket sono i contenitori fondamentali per i dati memorizzati nell&#39;ecosistema [!DNL Amazon]. I bucket contengono oggetti, ogni oggetto viene memorizzato e recuperato utilizzando una chiave univoca assegnata dagli sviluppatori.

**Connettore Amazon S3**: il connettore [!DNL Amazon] S3 consente ai clienti Experience Platform di connettersi e accedere in modo sicuro ai dati di [!DNL Amazon] S3.

**APA**: [[!DNL Australia Privacy Act (Privacy Act)]](https://www.oaic.gov.au/privacy/the-privacy-act) promuove e protegge la privacy degli individui e regola il modo in cui le agenzie governative australiane e l&#39;organizzazione gestiscono le informazioni personali. [!DNL Privacy Act] include i principi applicabili alle organizzazioni del settore privato. Ad esempio, gli utenti hanno il diritto di comprendere il motivo per cui le informazioni personali vengono raccolte e come verranno utilizzate, la possibilità di accedere ai loro dati, cancellarli e correggerli.

**Aggiungi strategia di salvataggio**: la strategia di salvataggio &quot;aggiungi&quot; è un&#39;opzione utilizzata quando si specificano dati di terze parti da acquisire tramite una connessione e si aggiungono nuovi dati o righe alla fine del set di dati. Le righe precedentemente acquisite rimangono intatte e solo le righe create dall’ultima esecuzione pianificata vengono acquisite in Experience Platform. Tutte le righe modificate nel sistema di origine rimangono invariate all&#39;Experience Platform.

**Array**: gli array vengono utilizzati per gli elementi ordinati con lo stesso tipo di dati.

**Intelligenza artificiale**: l&#39;intelligenza artificiale è una teoria e uno sviluppo di sistemi informatici in grado di eseguire attività che normalmente richiedono intelligenza umana, come la percezione visiva, il riconoscimento vocale, il processo decisionale e la traduzione tra lingue diverse.

**Attributi**: gli attributi sono caratteristiche specificate che rappresentano un profilo.

**Unione attributi**: quando si definisce un criterio di unione utilizzando Real-Time Customer Profile API, l&#39;oggetto `attributeMerge` indica il modo in cui il criterio di unione assegnerà priorità agli attributi di profilo in caso di conflitti di dati. Equivale a selezionare un [!UICONTROL metodo di unione] durante la definizione di un criterio di unione nell&#39;interfaccia utente di Platform.

**Attribution AI**: [!DNL Attribution AI] è un servizio intelligente basato su Adobe Sensei che fornisce funzionalità algoritmiche di attribuzione multicanale nell&#39;intero ciclo di vita del cliente.

**Pubblico**: un pubblico è il set risultante di profili che soddisfano i criteri di una definizione di segmento.

**Dimensione pubblico**: una dimensione pubblico è il numero totale di profili che soddisfano i criteri di una definizione di segmento e sono idonei per l&#39;iscrizione al pubblico.

**Snapshot del pubblico**: uno snapshot del pubblico acquisisce tutti i profili idonei per i criteri del segmento al momento della segmentazione.

## B

**Backfill**: per le origini pianificate, l&#39;opzione di backfill consente l&#39;acquisizione di dati storici.

**Periodo di backfill**: il periodo di backfill è un&#39;opzione che consente di impostare il periodo di tempo per l&#39;acquisizione di dati storici di terze parti tramite una connessione di origine. Selezionando un periodo di backfill di &quot;per sempre&quot; acquisirà l’intera cronologia dei dati sorgente in Experience Platform.

**Batch**: un batch è un insieme di dati raccolti in un periodo di tempo ed elaborati insieme come una singola unità. I set di dati sono composti da più batch.

**ID batch**: un ID batch è un identificatore generato dall&#39;Adobe per un batch di dati.

**Acquisizione batch**: l&#39;acquisizione batch ti consente di acquisire dati in Experience Platform come file batch. I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità.

**Segmentazione batch**: la segmentazione batch è un&#39;alternativa a un processo di selezione dati in corso e sposta tutti i dati del profilo contemporaneamente attraverso le definizioni dei segmenti per produrre tipi di pubblico corrispondenti. Una volta creato, il segmento viene salvato e memorizzato in modo da poterlo esportare per l’utilizzo.

**Build**: nel contesto dei tag, una build è un file o un set di file che contiene tutte le configurazioni e il codice necessari per eseguire la logica di business contenuta in una libreria, consentendo di distribuire tale libreria sul sito Web o sull&#39;app mobile.

**Strumenti di Business Intelligence**: gli strumenti di Business Intelligence (BI) sono principalmente integrati con [!DNL Experience Platform Query Service]. Gli strumenti BI sono tipi di software applicativo che raccolgono ed elaborano grandi quantità di dati non strutturati da sistemi interni ed esterni.

## C

**Limitazione**: in [!DNL Offer Decisioning], nelle regole di decisione viene utilizzato il limite (noto anche come limite di frequenza) per definire quante volte viene presentata un&#39;offerta. Esistono due tipi di limite: uno indica quante volte un’offerta può essere proposta al pubblico target combinato (denominato &quot;limite globale&quot;) e l’altro indica quante volte un’offerta può essere proposta allo stesso utente finale (denominato &quot;limite del profilo&quot;).

**Catalogo**: nel contesto di origini e destinazioni, un catalogo è una raccolta con connessioni disponibili ad applicazioni Adobe e tecnologie di terze parti. Da non confondere con [!DNL Catalog Service].

**[!DNL Catalog Service]**: [!DNL Catalog Service] (talvolta denominato [!DNL Catalog]) è il sistema di registrazione per la posizione e la derivazione dei dati in Adobe Experience Platform. Mentre tutti i dati acquisiti in Experience Platform vengono memorizzati nel data lake come file e directory, [!DNL Catalog] contiene i metadati e le descrizioni di tali file e directory a scopo di ricerca, monitoraggio e governance dei dati.

**CCPA**: [[!DNL California Consumer Privacy Act (CCPA)]](https://oag.ca.gov/privacy/ccpa) migliora i diritti sulla privacy e la protezione dei consumatori per i residenti in California, Stati Uniti. Il CCPA conferisce ai residenti della California nuovi diritti sulla privacy dei dati, tra cui il diritto di accesso e cancellazione dei propri dati personali, di sapere se i propri dati personali vengono venduti o divulgati (e a chi), e il diritto di non acconsentire alla vendita dei propri dati a terzi.

**Classe**: in Experience Data Model (XDM), una classe definisce il set di campi più piccolo utilizzato per creare uno schema e definisce il comportamento di base dell&#39;oggetto business rappresentato dallo schema.

**Client**: un client è uno strumento o un&#39;applicazione esterna che si connette a [!DNL Query Service] tramite il protocollo [!DNL PostgreSQL] o API HTTP.

**Raccolta**: in [!DNL Offer Decisioning] le raccolte sono sottoinsiemi di offerte basate su condizioni predefinite definite da un addetto marketing, ad esempio la categoria dell&#39;offerta.

**Combina con azione di marketing PII**: azione di marketing che combina qualsiasi informazione personale identificabile (PII) con dati anonimi. I contratti per i dati provenienti da reti di annunci, server di annunci e fornitori di dati di terze parti spesso includono divieti contrattuali specifici sull’utilizzo di tali dati con dati direttamente identificabili.

**Interfaccia della riga di comando**: un&#39;interfaccia della riga di comando è uno strumento basato su testo che può essere utilizzato per connettersi a [!DNL Query Service] per l&#39;esecuzione di query non elaborate.

**Composizione**: una composizione è un raggruppamento di componenti che si formano insieme per formare lo schema.

**Condizione**: nel contesto dei tag, una condizione è un componente regola che valuta un&#39;istruzione logica che deve restituire `true` o `false`. Tutte le condizioni devono restituire `true` e tutte le condizioni di eccezione devono restituire `false` prima dell&#39;esecuzione di qualsiasi azione sulla regola.

**Console**: in [!DNL Query Service] la console fornisce informazioni sullo stato e sul funzionamento di una query. La console visualizza lo stato della connessione a [!DNL Query Service], le operazioni di query in esecuzione ed eventuali messaggi di errore risultanti da tali query.

**Etichette contratto (&quot;C&quot;)**: le etichette di utilizzo dei dati del contratto (&quot;C&quot;) vengono utilizzate per categorizzare i dati che hanno obblighi contrattuali o sono correlati ai criteri di governance dei dati della tua organizzazione.

**CPRA**: [[!DNL California Consumer Privacy Rights Act (CPRA)]](https://cppa.ca.gov/regulations/consumer_privacy_act.html) espande e modifica parti di [!DNL California Consumer Privacy Act (CCPA)]. [!DNL CPRA] stabilisce una nuova linea di base per la privacy dei dati dei consumatori in California aumentando i diritti dei consumatori e ampliando il tipo di dati coperti da una definizione più ampia di informazioni personali sensibili. Inoltre, [!DNL CPRA] ha istituito la California Privacy Protection Agency, una nuova agenzia dedicata all&#39;implementazione e all&#39;applicazione delle regole sulla privacy dei dati.

**Etichetta contratto C1**: un&#39;etichetta di utilizzo dei dati del contratto `C1` specifica che i dati possono essere esportati da Adobe Experience Cloud solo in un formato aggregato senza includere identificatori individuali o di dispositivo. Ad esempio, dati provenienti dai social network.

**Etichetta contratto C2**: un&#39;etichetta di utilizzo dei dati del contratto `C2` specifica i dati che non possono essere esportati in terze parti. Alcuni fornitori di dati hanno clausole nei loro contratti che vietano l’esportazione di dati da dove sono stati raccolti originariamente. Ad esempio, i contratti per i social network spesso limitano il trasferimento dei dati che ricevi da loro. C2 è più restrittivo di C1, che richiede solo aggregazione e dati anonimi.

**Etichetta contratto C3**: un&#39;etichetta di utilizzo dei dati del contratto `C3` specifica dati che non possono essere combinati o altrimenti utilizzati con informazioni direttamente identificabili. Alcuni fornitori di dati hanno clausole nei loro contratti che vietano la combinazione o l’uso di tali dati con informazioni direttamente identificabili. Ad esempio, i contratti per i dati provenienti da reti di annunci, server di annunci e fornitori di dati di terze parti spesso includono divieti contrattuali specifici sull’utilizzo di dati direttamente identificabili.

**Etichetta contratto C4**: un&#39;etichetta di utilizzo dei dati del contratto `C4` specifica che i dati non possono essere utilizzati per il targeting di annunci o contenuti, né nel sito né tra siti diversi. C4 è l&#39;etichetta più restrittiva in quanto include le etichette C5, C6 e C7.

**Etichetta contratto C5**: un&#39;etichetta di utilizzo dei dati del contratto `C5` specifica che i dati non possono essere utilizzati per il targeting intersito di contenuti o annunci basati su interessi. Il targeting basato sull’interesse, o personalizzazione, si verifica se vengono soddisfatte le tre condizioni seguenti: i dati raccolti sul sito vengono utilizzati per trarre conclusioni sull’interesse di un utente; vengono utilizzati in un altro contesto, ad esempio su un altro sito o un’altra app; e vengono utilizzati per selezionare quali contenuti o annunci vengono distribuiti in base a tali conclusioni.

**Etichetta contratto C6**: un&#39;etichetta di utilizzo dei dati del contratto `C6` specifica che i dati non possono essere utilizzati per il targeting degli annunci nel sito. Il targeting degli annunci nel sito include la selezione e la consegna di annunci sui siti web o sulle app della tua organizzazione o per misurare la consegna e l’efficacia di tali annunci. Ciò include l’utilizzo di dati sul sito raccolti in precedenza che mostrano l’interesse degli utenti a selezionare annunci, elaborare dati su quali annunci sono stati mostrati, quando e dove sono stati mostrati e se gli utenti hanno intrapreso azioni relative all’annuncio, ad esempio selezionando un annuncio o effettuando un acquisto.

**Etichetta contratto C7**: un&#39;etichetta di utilizzo dei dati del contratto `C7` specifica che i dati non possono essere utilizzati per il targeting del contenuto nel sito. Il targeting dei contenuti nel sito include la selezione e la distribuzione dei contenuti sui siti web o sulle app della tua organizzazione o per misurare la distribuzione e l’efficacia di tali contenuti. Ciò include informazioni raccolte in precedenza sull’interesse degli utenti a selezionare il contenuto, sull’elaborazione dei dati su quale contenuto è stato visualizzato, sulla frequenza o la durata della visualizzazione, su quando e dove è stato visualizzato e se gli utenti hanno intrapreso azioni relative al contenuto, inclusa ad esempio la selezione del contenuto.

**Etichetta contratto C8**: un&#39;etichetta di utilizzo dei dati del contratto `C8` specifica che i dati non possono essere utilizzati per la misurazione dei siti Web o delle app dell&#39;organizzazione. Questo non include il targeting basato sugli interessi, che è la raccolta di informazioni sull’utilizzo di questo servizio per personalizzare successivamente contenuti e/o pubblicità in altri contesti.

**Etichetta contratto C9**: un&#39;etichetta di utilizzo dei dati del contratto `C9` specifica che i dati non possono essere utilizzati nei flussi di lavoro di data science. Alcuni contratti includono divieti espliciti sui dati utilizzati per la scienza dei dati. A volte queste sono formulate in termini che vietano l’uso di dati per l’intelligenza artificiale (IA), l’apprendimento automatico (ML) o la modellazione.

**Etichetta contratto C10**: un&#39;etichetta di utilizzo dei dati del contratto `C10` specifica che i dati non possono essere utilizzati per l&#39;attivazione dell&#39;identità unita. Alcuni criteri di utilizzo dei dati limitano l’utilizzo di dati di identità uniti per la personalizzazione. L&#39;etichetta `C10` viene applicata automaticamente ai segmenti se i criteri di unione utilizzano l&#39;opzione &quot;Private Graph&quot;.

**Colonna Data di creazione**: la selezione di una colonna Data di creazione è un&#39;opzione che consente di specificare dati di terze parti tramite una connessione di origine. Quando si seleziona la strategia di salvataggio di accodamento e lo schema del set di dati contiene più campi di data, è necessario scegliere dallo schema disponibile per specificare una colonna chiave Data di creazione. L’opzione Data di creazione non è disponibile quando è selezionata la strategia di salvataggio di sovrascrittura.

**Crea tabella come selezione**: Crea tabella come selezione (CTAS) è un comando SQL che, se eseguito come parte di una query SQL completa e valida, indica a [!DNL Query Service] di mantenere i risultati della query in un set di dati. È possibile creare una nuova serie di risultati, sovrascrivere i risultati precedenti o aggiungere ai risultati precedenti.

**Dati intersito**: i dati intersito sono la combinazione di dati provenienti da più siti, inclusa una combinazione di dati nel sito e dati esterni al sito o una combinazione di dati provenienti da più origini esterne al sito.

**Azione di marketing per targeting intersito**: azione di marketing che utilizza i dati per il targeting di annunci intersito. La combinazione di dati provenienti da diversi siti, compresa una combinazione di dati nel sito e dati esterni al sito o una combinazione di dati provenienti da diverse fonti esterne al sito, è definita dati intersito. I dati tra siti vengono generalmente raccolti ed elaborati per trarre conclusioni sugli interessi dei clienti.

**Spazio dei nomi identità personalizzato**: gli spazi dei nomi di identità personalizzati possono essere creati dall&#39;organizzazione per rappresentare le identità per un&#39;organizzazione o un caso di business specifico.

**Etichette personalizzate**: le etichette personalizzate di utilizzo dei dati consentono di creare e applicare etichette specifiche ai campi dati che soddisfano esigenze aziendali specifiche.

**IA per l&#39;analisi dei clienti**: IA per l&#39;analisi dei clienti è un servizio intelligente basato su Adobe Sensei che arricchisce i profili dei clienti con dati di propensione basati sull&#39;intelligenza artificiale e potenzia la segmentazione dei clienti e le attività di targeting.

## D

**Giornaliero**: nel contesto delle esportazioni di file pianificate, pianifica le esportazioni di file complete o incrementali una volta al giorno, ogni giorno, dalla data di inizio alla data di fine all&#39;ora specificata dall&#39;utente.

**Dizionario dati**: nel contesto dei tag, un dizionario dati (noto anche come mappa dati) è un insieme di elementi dati definiti all&#39;interno di una proprietà.

**Elemento dati**: nel contesto dei tag, un elemento dati è un puntatore utilizzato all&#39;interno di regole ed estensioni per puntare a dati specifici presenti nel dispositivo client.

**Acquisizione dei dati**: l&#39;acquisizione dei dati è il processo di aggiunta di dati da un&#39;origine all&#39;Experience Platform. I dati possono essere acquisiti in Platform in diversi modi, tra cui streaming, batch o aggiunti tramite connettori di origine.

**Livello dati**: nel contesto dei tag, un livello dati è una struttura di dati esistente sul dispositivo client che contiene metadati sul contesto in cui viene visualizzata una pagina o una schermata.

**Governance dei dati**: la governance dei dati include le strategie e le tecnologie utilizzate per garantire la conformità dei dati alle normative e alle politiche organizzative relative all&#39;utilizzo dei dati.

**Partner di integrazione dei dati**: i partner di integrazione dei dati semplificano e automatizzano il caricamento e la trasformazione di grandi volumi di dati da oltre 200 origini all&#39;Experience Platform senza scrivere codice.

**Etichette set di dati**: è possibile aggiungere etichette di utilizzo dati ai set di dati. Tutti i campi all’interno di tale set di dati ereditano le etichette del set di dati.

**Data Science Workspace**: [!DNL Data Science Workspace] in Experience Platform consente ai clienti di creare modelli di apprendimento automatico utilizzando i dati nelle applicazioni Platform e Adobe per creare segmenti intelligenti, generare informazioni approfondite e fornire previsioni, consentendo di migliorare notevolmente le esperienze digitali degli utenti finali.

**Origine dati**: un&#39;origine dati è un&#39;origine dei dati designata dall&#39;utente. Esempi di un’origine dati sono un’app mobile, eventi di profilo e/o esperienza, eventi di profilo del sito web o un CRM.

**Data Steward**: un data steward è la persona responsabile della gestione, della supervisione e dell&#39;applicazione delle risorse dati di un&#39;organizzazione. Un data steward garantisce inoltre che i criteri di governance dei dati siano salvaguardati e mantenuti in modo da essere conformi alle normative e ai criteri organizzativi governativi.

**Flusso di dati**: un flusso di dati è un insieme o una raccolta di messaggi che condividono lo stesso schema e sono inviati dalla stessa origine.

**Tipo di dati**: un tipo di dati è una risorsa XDM riutilizzabile che definisce un campo di tipo oggetto contenente più proprietà in una rappresentazione gerarchica.

**Etichette di utilizzo dati**: le etichette di utilizzo dati consentono di categorizzare i dati che riflettono considerazioni relative alla privacy e condizioni contrattuali conformi alle normative e ai criteri aziendali. Le etichette di utilizzo dei dati aggiunte a un set di dati vengono ereditate o applicate a tutti i campi all’interno di tale set di dati. Le etichette di utilizzo dei dati possono essere applicate direttamente ai campi.

**Flusso di dati**: un flusso di dati è una pipeline virtuale di dati che fluisce in Platform da un&#39;origine e in uscita verso le destinazioni.

**Esecuzione del flusso di dati**: un&#39;esecuzione del flusso di dati è un flusso di dati che termina in Experience Platform in base a una pianificazione specificata dall&#39;utente.

**Set di dati**: un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e campi (righe).

**ID set di dati**: identificatore generato dall&#39;Adobe per un set di dati acquisito.

**Output del set di dati**: l&#39;output del set di dati fornisce un meccanismo per determinare quale opzione &quot;Crea tabella come selezionata&quot; verrà utilizzata per una particolare esecuzione di [!DNL Query Service].

**Chiave di deduplicazione**: chiave primaria definita dall&#39;utente che determina l&#39;identità in base alla quale gli utenti desiderano deduplicare i propri profili.&#x200B;

**Colonna delta**: una colonna delta consente di selezionare un campo dati di origine per rappresentare una marca temporale per l&#39;acquisizione incrementale.

**Strategia di salvataggio delta**: la strategia di salvataggio delta è un&#39;opzione per acquisire dati di terze parti tramite una connessione di origine. L’opzione consente all’utente di specificare che le righe di dati di origine nuove o modificate vengono acquisite in Experience Platform. Alla fine del set di dati vengono aggiunte nuove righe e quelle modificate vengono aggiornate nel set di dati in Experience Platform.

**Descrittore**: in Experience Data Model (XDM), un descrittore è un set aggiuntivo di metadati relativi allo schema che descrive un comportamento specifico per un campo. I descrittori possono essere utilizzati da Experience Platform per comprendere il comportamento dello schema desiderato, ad esempio la relazione tra due schemi.

**Destinazione**: una destinazione è un termine generale per qualsiasi endpoint, ad esempio un&#39;applicazione di Adobe, una piattaforma pubblicitaria, un servizio di archiviazione cloud o un servizio di marketing, in cui viene attivato e recapitato un pubblico.

**Categoria di destinazione**: una categoria di destinazione è un raggruppamento di destinazioni con caratteristiche simili.

**Catalogo di destinazione**: un catalogo di destinazione è un elenco di destinazioni disponibili in Experience Platform.

**Regole di chiamata diretta**: nel contesto dei tag, una regola di chiamata diretta è una regola che viene eseguita quando viene chiamata direttamente dalla pagina, ignorando i sistemi di rilevamento degli eventi e di ricerca.

**Nome visualizzato**: in Experience Data Model (XDM), un nome visualizzato è un nome descrittivo per un campo visualizzato nell&#39;interfaccia utente.

## E

**Offerta idonea**: un&#39;offerta idonea può essere offerta in modo coerente a un profilo, in quanto soddisfa i vincoli definiti a monte.

**Regole di idoneità**: in [!DNL Offer Decisioning], le regole di idoneità vengono applicate a un profilo correlato ai vincoli di calendario, pianificazione e limite.

**Azione di marketing targeting e-mail**: azione di marketing che utilizza i dati nelle campagne di targeting e-mail.

**Codice di incorporamento**: nel contesto dei tag, il codice di incorporamento è un tag script inserito nel HTML in un sito o in un ambiente. Il codice di incorporamento indica al browser dove recuperare la build.

**Enumerazione**: un&#39;enumerazione (enum) è un campo XDM vincolato a un set di valori predefiniti.

**Ambiente**: nel contesto dei tag, un ambiente è un insieme di istruzioni di distribuzione che specifica la consegna host e il formato di file di una build. Prima di poter essere generata, una libreria deve essere associata a un ambiente.

**Diagnostica errori**: la diagnostica degli errori consente la generazione di messaggi di errore dettagliati per i batch acquisiti. La soglia di errore consente di configurare la percentuale di errori accettabili prima che un batch abbia esito negativo.

**Evento**: nel contesto dei tag, un evento è un tipo specifico di componente regola, ovvero un trigger che si verifica su un dispositivo client per iniziare l&#39;esecuzione di una regola.

**Entità evento**: nel contesto della modellazione dati, le entità evento rappresentano concetti relativi alle azioni che un cliente può intraprendere, agli eventi di sistema o a qualsiasi altro concetto in cui si possa voler tenere traccia delle modifiche nel tempo. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati sulla classe [!DNL XDM ExperienceEvent].

**Eventi**: gli eventi sono i dati di comportamento associati a un profilo.

**Experience Data Model (XDM)** [!DNL Experience Data Model] (XDM) è un framework open-source che utilizza schemi standard per unificare i dati da utilizzare con le applicazioni Experience Platform e Adobe Experience Cloud. XDM standardizza la struttura dei dati, velocizza e semplifica il processo di acquisizione di informazioni da enormi quantità di dati.

**Esperimento**: un esperimento è il processo di creazione di un modello addestrato addestrando l&#39;istanza con una porzione campione di dati di produzione live. È diverso da un modello addestrato che viene testato in base a un set di dati di prova di sospensione. Questo è anche diverso dal concetto di esperimento in alcuni framework di apprendimento automatico dove in realtà significa un progetto di modellazione campione.

**Evento esperienza**: un evento esperienza rappresenta un&#39;istantanea del sistema quando si verifica un&#39;interazione o un evento correlato a un&#39;esperienza del cliente. Gli Eventi di esperienza sono record di fatti immutabili di ciò che è accaduto e rappresentano ciò che è accaduto senza aggregazione o interpretazione. In Experience Data Model (XDM), questo concetto viene acquisito dalla classe [!DNL XDM ExperienceEvent].

**Esporta file completo**: file di esportazione contenente uno snapshot completo di tutte le qualifiche di profilo per il segmento selezionato.

**Esporta file incrementali**: una serie di file esportati in cui il primo file è un&#39;istantanea completa di tutte le qualifiche di profilo per il segmento selezionato e i file successivi sono qualifiche di profilo incrementali dall&#39;esportazione precedente.

**Estensione**: nel contesto dei tag, un&#39;estensione è un pacchetto di funzionalità aggiunto a una proprietà tag. Un’estensione si concentra solitamente su una particolare soluzione di marketing o analisi e fornisce gli strumenti necessari per distribuire tale tecnologia in un ambiente client.

**Pacchetto di estensione**: nel contesto dei tag, un pacchetto di estensione è un file ZIP creato e caricato da uno sviluppatore di estensioni che fornisce tutto il necessario affinché gli utenti dei tag possano installare l&#39;estensione all&#39;interno della propria proprietà. Un pacchetto di estensione contiene un manifesto che specifica le informazioni sull’estensione, le HTML/JavaScript necessarie agli utenti finali per configurare il comportamento dell’estensione tag e l’eseguibile JavaScript consegnato all’ambiente client (se necessario).

## F

**Offerte di fallback**: un&#39;offerta di fallback è l&#39;offerta predefinita visualizzata quando un utente finale non è idoneo per nessuna delle offerte della raccolta utilizzata.

**Mappatura delle funzionalità**: la mappatura delle funzionalità fa riferimento al processo di mappatura delle funzionalità dai dati alle funzionalità di input e di destinazione richieste da un modello di apprendimento automatico.

**Campo**: un campo è l&#39;elemento di livello inferiore di un set di dati, come definito dallo schema XDM del set di dati. Ogni campo ha un nome a scopo di riferimento e un tipo per indicare il tipo di dati che contiene. I tipi di campo possono includere (ma non sono limitati a) numero intero, numero, stringa, booleano e oggetto.

**Gruppo di campi**: vedere &quot;Gruppo di campi schema&quot;.

**Etichette campo**: le etichette campo sono etichette di governance dei dati ereditate da un set di dati o applicate direttamente a un campo.

**Nome campo**: un nome di campo viene utilizzato per fare riferimento al valore di un campo nelle query e nei servizi a valle.

**Frequenza**: in [!DNL Query Service], la frequenza determina la frequenza con cui verrà eseguita una query pianificata ricorrente.

## G

**Recinto geografico**: un recinto geografico virtuale è un confine geografico virtuale, definito dalla tecnologia GPS o RFID, che consente al software di attivare una risposta quando un dispositivo mobile entra o esce da una determinata area.

**RGPD (Regolamento generale sulla protezione dei dati)**: il regolamento generale sulla protezione dei dati (RGPD) è un quadro giuridico che definisce le linee guida per la raccolta e l&#39;elaborazione di informazioni personali di persone all&#39;interno dell&#39;Unione europea (UE). Il RGPD stabilisce i principi per la gestione dei dati e i diritti dei singoli e copre tutte le aziende che trattano dati di cittadini dell’UE.

**Guardrail**: i guardrail sono soglie che forniscono indicazioni per l&#39;utilizzo dei dati e del sistema, l&#39;ottimizzazione delle prestazioni e la prevenzione di errori o risultati imprevisti in Adobe Experience Platform. I guardrail possono fare riferimento all’utilizzo o al consumo di dati e all’elaborazione in relazione alle licenze concesse.

## H

**HIPAA**: [[!DNL Health Insurance Portability and Accountability Act (HIPAA)]](https://www.hhs.gov/hipaa/index.html) è una legge federale degli Stati Uniti creata per migliorare l&#39;efficienza dell&#39;assistenza sanitaria, migliorare la portabilità dell&#39;assicurazione sanitaria e proteggere la privacy dei pazienti e dei membri del piano sanitario. In base all&#39;HIPAA, le persone hanno il diritto di accedere alle proprie informazioni e di modificarle, nonché di ottenere copie delle proprie cartelle cliniche o informazioni sulla salute. Le entità coperte e i soci d&#39;affari delle entità coperte devono seguire le normative HIPAA.

**Host**: nel contesto dei tag, un host specifica la posizione, il dominio e le credenziali utente necessari affinché il sistema distribuisca una build.

**Oraria**: nel contesto delle esportazioni di file pianificate, pianifica le esportazioni di file incrementali ogni 3, 6, 8 o 12 ore.

## I

**Identità**: un&#39;identità è un identificatore che rappresenta in modo univoco un singolo cliente, ad esempio un ID cookie, un ID dispositivo o un ID e-mail.

**Campi di identità**: i campi di identità sono campi XDM utilizzati per unire informazioni su singoli clienti provenienti da più origini dati. È necessario definire una singola identità primaria affinché lo schema possa essere abilitato per l’utilizzo in Real-Time Customer Profile.

**Etichette di identità (&quot;I&quot;)**: le etichette di utilizzo dei dati di identità (&quot;I&quot;) vengono utilizzate per categorizzare i dati che possono identificare o contattare una persona specifica.

**Grafo identità**: un grafo identità è una mappa delle relazioni tra identità collegate e unite esistenti per un singolo cliente. Ogni grafo di identità viene aggiornato quasi in tempo reale con l’attività del cliente. La struttura comune delle relazioni di identità nei dati è rappresentata dal [!UICONTROL grafico privato], che funge da blueprint strutturale per ogni singolo grafico di identità.

**Spazio dei nomi identità**: uno spazio dei nomi identità definisce il contesto di un identificatore, ad esempio un indirizzo e-mail o un ID CRM.

**Identity Service**: [!DNL Experience Platform Identity Service] consente la creazione e la gestione di tipi di identità, consentendo di collegare le identità dei clienti tra dispositivi e canali diversi. La capacità del servizio di collegare le identità consente a Real-Time Customer Profile di fornire una rappresentazione completa di ogni singolo cliente.

**Unione identità**: l&#39;unione identità è il processo di identificazione dei frammenti di dati e di loro unione per formare un record di profilo completo.

**Simbolo di identità**: un simbolo di identità è un&#39;abbreviazione di uno spazio dei nomi di identità che può essere utilizzato come riferimento nelle API.

**Valore identità**: un valore identità, combinato con uno spazio dei nomi identità, è un identificatore che rappresenta un individuo, un&#39;organizzazione o una risorsa univoca. Quando si abbinano i dati del record tra i frammenti di profilo, lo spazio dei nomi e il valore dell’identità devono corrispondere.

**I1 etichetta di utilizzo dati**: l&#39;etichetta di utilizzo dati `I1` viene utilizzata per classificare i dati che possono identificare o contattare direttamente una persona specifica anziché un dispositivo.

**Etichetta di utilizzo dati I2**: l&#39;etichetta di utilizzo dati `I2` viene utilizzata per classificare i dati che possono essere utilizzati in combinazione con altri dati per identificare o contattare indirettamente una persona specifica.

**Organizzazione IMS**: un&#39;organizzazione IMS (a volte indicata come organizzazione IMS) è il nome utilizzato per identificare un&#39;azienda o un gruppo specifico all&#39;interno di un&#39;azienda in tutti i prodotti Adobe. Gli amministratori possono configurare e gestire l’accesso e le autorizzazioni delle funzioni per gli utenti di un’organizzazione.

**Acquisizione**: vedi l&#39;acquisizione dei dati.

**Pianificazione acquisizione**: una pianificazione dell&#39;acquisizione fornisce opzioni basate sul tempo per l&#39;acquisizione da un&#39;origine all&#39;Experience Platform.

**Funzione di input**: una funzione di input è specificata nella mappatura delle caratteristiche ed è utilizzata da un modello di apprendimento automatico per effettuare previsioni.

**[!DNL Intelligent Services]**: [!DNL Intelligent Services] come [!DNL Attribution AI] e [!DNL Customer AI] sono modelli basati sull&#39;intelligenza artificiale e sull&#39;apprendimento automatico che richiedono l&#39;esecuzione di Experience Platform (o di applicazioni basate su Platform come Adobe Real-time Customer Data Platform) e il loro funzionamento.

**Impostazione destinazione basata su interessi o personalizzazione**: il targeting basato su interessi, noto anche come personalizzazione, si verifica se vengono soddisfatte le tre condizioni seguenti:

1. I dati raccolti sul sito vengono utilizzati per trarre conclusioni sull’interesse di un utente.
1. I dati vengono utilizzati in un altro contesto, ad esempio in un altro sito o in un’altra app (fuori dal sito).
1. I dati vengono utilizzati per selezionare il contenuto o gli annunci da distribuire in base a tali inferenze.

## J

**[!DNL JupyterLab]**: interfaccia open-source basata su Web per il progetto [!DNL Jupyter] integrata nell&#39;interfaccia utente di Platform.

**[!DNL Jupyter Notebook]**: Integrato con JupyterLab, Jupyter Notebooks consente di eseguire operazioni di pulizia e trasformazione dei dati, simulazione numerica, modellazione statistica, visualizzazione dei dati, apprendimento automatico e altro ancora sui dati Experienci Platform in diversi linguaggi quali Python, Scala e PySpark.

## K

## L

**LGPD**: [[!DNL Lei Geral de Proteção de Dados (LGPD)]](https://gdpr.eu/gdpr-vs-lgpd/) ha lo scopo di regolamentare il trattamento dei dati personali di tutti gli individui o persone fisiche in Brasile. L&#39;LGPD conferisce ai cittadini brasiliani il diritto di accedere ai propri dati personali e di cancellarli, di sapere se i propri dati personali vengono venduti o divulgati (e a chi), e il diritto di non acconsentire alla vendita dei propri dati a terzi.

**Libreria**: nel contesto dei tag, una libreria è un set di regole business che contiene istruzioni sul comportamento della libreria di tag nel dispositivo client.

**Entità di ricerca**: nel contesto della modellazione dati, le entità di ricerca rappresentano concetti che possono essere correlati a una singola persona, ma non possono essere utilizzati direttamente per identificare l&#39;individuo. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati su classi XDM (Experience Data Model) personalizzate e collegate a un&#39;entità profilo tramite una [relazione schema](../xdm/tutorials/relationship-ui.md).

## M

**Apprendimento automatico (ML)**: l&#39;apprendimento automatico è il campo di studio che consente ai computer di apprendere senza essere programmati in modo esplicito.

**Modello di apprendimento automatico**: un modello di apprendimento automatico è un&#39;istanza di una ricetta di apprendimento automatico che viene addestrata utilizzando dati e configurazioni storici da risolvere per un caso d&#39;uso aziendale. In Adobe Experience Platform Data Science Workspace, i modelli di apprendimento automatico sono chiamati ricette.

**Attributo obbligatorio**: casella di controllo abilitata per l&#39;utente che assicura che tutti i record di profilo contengano l&#39;attributo selezionato. Ad esempio: tutti i profili esportati contengono un indirizzo e-mail.

**Mappatura**: la mappatura dei dati è il processo di mappatura dei campi dei dati di origine ai campi di destinazione correlati in una destinazione.

**Azione di marketing**: nel framework di governance dei dati, un&#39;azione di marketing (nota anche come caso di utilizzo di marketing) è un&#39;azione intrapresa da un consumatore di dati Experience Platform, per la quale è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati.

**Metodo di unione**: quando si definisce un criterio di unione utilizzando l&#39;interfaccia utente di Platform, il metodo di unione specifica il modo in cui assegnare la priorità ai frammenti di dati quando si verifica un conflitto. Quando si utilizza l&#39;API Real-Time Customer Profile per definire un criterio di unione, il metodo di unione viene determinato utilizzando l&#39;oggetto `attributeMerge`.

**Criterio di unione**: i criteri di unione sono regole utilizzate da Experience Platform per determinare come i frammenti di dati dei clienti provenienti da più origini verranno combinati per creare un singolo profilo. Quando si verifica un conflitto di dati, il criterio di unione determina i dati a cui assegnare la priorità per l’inclusione nel profilo.

**MHMDAa**: [[!DNL Washington My Health My Data Act]](https://app.leg.wa.gov/RCW/default.aspx?cite=19.373&amp;full=true) migliora i diritti di privacy per i consumatori relativi ai dati di integrità. Impone la divulgazione, il consenso dei consumatori e i diritti di cancellazione per i dati sanitari e vieta la vendita di dati sanitari senza autorizzazione. Inoltre, la legge rende illegale l&#39;uso di recinti geografici intorno alle strutture sanitarie.

**Mixin**: vedere &quot;Gruppo di campi schema&quot;.

**Modulo**: nel contesto dei tag, un modulo è uno snippet di JavaScript eseguibile fornito da un&#39;estensione, che esegue azioni in un ambiente client senza dover creare una regola.

## N

**[!DNL New Zealand Privacy Act]**: [[!DNL New Zealand Privacy Act]](https://www.privacy.org.nz/privacy-act-2020/privacy-principles/) controlla come le agenzie possono raccogliere, utilizzare, divulgare, archiviare e consentire l&#39;accesso alle informazioni personali di cittadini e organizzazioni della Nuova Zelanda. Nel 2020 l&#39;ultima versione della legge ha introdotto aggiornamenti significativi a tali leggi sulla privacy, tra cui nuove infrazioni, aumento delle ammende, notifiche obbligatorie per le violazioni dei dati e aumento dei poteri del commissario per la privacy.

**Sandbox non di produzione**: le sandbox non di produzione sono in genere utilizzate per esperimenti di sviluppo, test o test. A differenza delle sandbox di produzione, le sandbox non di produzione possono essere reimpostate ed eliminate.

**[!DNL Notebooks]**: [!DNL Notebooks] sono creati con [!DNL Jupyter Notebook] e possono essere eseguiti per eseguire l&#39;analisi dei dati.

## O

**Offerta**: un&#39;offerta è un messaggio di marketing contenente una proposta commerciale o di vendita per un (potenziale) cliente. Le offerte spesso dispongono di regole specifiche che determinano chi è idoneo a visualizzarle o riceverle.

**[!DNL Offer Decisioning]**: [!DNL Offer Decisioning] consente agli addetti al marketing di gestire regole e modelli di proposte di offerte addestrati quando interagiscono con gli utenti finali in base ai dati raccolti tra canali e applicazioni.

**Libreria di offerte**: la libreria di offerte è una libreria centrale utilizzata per gestire offerte personalizzate e di fallback, regole di decisione e attività.

**Azione di marketing per la personalizzazione nel sito**: azione di marketing che utilizza i dati per la personalizzazione del contenuto nel sito. Per personalizzazione nel sito si intende qualsiasi dato utilizzato per trarre conclusioni sugli interessi degli utenti e per selezionare i contenuti o gli annunci da distribuire in base a tali conclusioni.

**Azione di marketing per targeting nel sito**: azione di marketing che utilizza i dati per gli annunci nel sito, inclusa la selezione e la distribuzione di annunci sui siti Web o sulle app della tua organizzazione, oppure per misurare la distribuzione e l&#39;efficacia di tali annunci.

**Una volta**: nel contesto delle esportazioni di file pianificate, pianifica un&#39;esportazione di file completa una tantum su richiesta.

**Sovrascrivi strategia di salvataggio**: la strategia di salvataggio &quot;Sovrascrivi&quot; è un&#39;opzione per l&#39;acquisizione di dati di terze parti tramite una connessione, in cui è possibile specificare se i dati acquisiti verranno sovrascritti in base a una pianificazione specificata.

## P

**Acquisizione parziale**: l&#39;acquisizione parziale consente l&#39;acquisizione di record validi di dati batch entro una soglia di errore specificata. È possibile scaricare o accedere alla diagnostica degli errori per i record non riusciti in [!UICONTROL Monitoraggio] o [!UICONTROL Panoramica sull&#39;esecuzione del flusso di dati origini].

**File Parquet**: un file Parquet è un formato di file di archiviazione a colonne con strutture di dati nidificate complesse. I file Parquet sono necessari per aggiungere dati per popolare un set di dati di schema.

**PDPA**: la [[!DNL Personal Data Protection Act (PDPA)]](https://www.pdpc.gov.sg/Overview-of-PDPA/The-Legislation/Personal-Data-Protection-Act) è stata introdotta per proteggere i proprietari di dati thailandesi dalla raccolta, dall&#39;utilizzo o dalla divulgazione illegali dei loro dati personali. Ispirandosi al regolamento generale sulla protezione dei dati (RGPD) dell&#39;Unione Europea, il regolamento garantisce ai cittadini thailandesi il diritto di richiedere l&#39;accesso o la cancellazione dei propri dati personali memorizzati.

<!-- Not yet released
**PDPD**: The [[!DNL Personal Data Protection Decree] (PDPD) 
-->

**Offerte personalizzate**: un&#39;offerta personalizzata è un messaggio di marketing personalizzabile basato su regole e vincoli di idoneità.

**Posizionamenti**: per posizionamento si intende la posizione e/o il contesto in cui un’offerta viene visualizzata da un utente finale.

**Area di lavoro criteri**: area di lavoro nell&#39;interfaccia utente di Platform che consente agli amministratori dei dati di visualizzare e gestire le etichette e i criteri di utilizzo dei dati per l&#39;organizzazione.

**Criterio**: un criterio di utilizzo dati è una regola che specifica azioni di marketing soggette a restrizioni in base all&#39;applicazione di etichette di utilizzo applicate ai dati di Platform.

**Applicazione dei criteri**: consente di applicare criteri di utilizzo dei dati con azioni di marketing applicate per impedire operazioni sui dati che costituiscono violazioni dei criteri all&#39;interno di un&#39;organizzazione.

**Chiave primaria**: una chiave primaria è una designazione in uno schema che identifica in modo univoco tutti i record.

**Priorità**: in [!DNL Offer Decisioning], la priorità viene utilizzata per classificare le offerte che soddisfano tutti i vincoli, come idoneità, calendario e limiti.

**Grafo di identità privata**: il grafo di identità privata (a volte denominato grafo privato) è una mappa privata delle relazioni tra identità collegate e unite, creata in base ai dati di prime parti e visibile solo dall&#39;organizzazione. Esiste un solo grafico privato per ogni organizzazione e funge da blueprint strutturale per i singoli grafici di identità generati per ogni cliente che interagisce con il tuo marchio.

**Profilo di prodotto**: i profili di prodotto consentono agli amministratori di concedere l&#39;accesso utente a tutti i servizi associati ad Experience Platform o a un sottoinsieme di essi.

**Sandbox di produzione**: una sandbox di produzione è una sandbox destinata all&#39;utilizzo nell&#39;ambiente di produzione. A differenza delle sandbox non di produzione, le sandbox di produzione non possono essere reimpostate o eliminate.

**Profilo**: da non confondere con Real-Time Customer Profile as a service, un profilo è una rappresentazione completa di un singolo cliente, costruita da record uniti e dati di serie temporali provenienti da più origini.

**Accesso profilo**: l&#39;endpoint `/entities` nell&#39;API Profilo cliente in tempo reale consente di accedere ai dati dei record e agli eventi della serie temporale nell&#39;archivio dati del profilo. Vedere anche: Entità profilo

**Dati profilo**: i dati profilo si riferiscono a qualsiasi dato presente nell&#39;archivio dati profilo.

**Archivio dati profilo**: l&#39;archivio dati profilo (talvolta denominato archivio profili) è un sistema di archiviazione dati separato dal data lake, utilizzato da Real-Time Customer Profile per creare e archiviare profili.

**Entità profilo**: le entità profilo rappresentano attributi relativi a una singola persona, in genere un cliente. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati sulla classe [!DNL XDM Individual Profile]. Vedi anche: Accesso al profilo

**Esportazione profilo**: l&#39;esportazione [!DNL Profile] è uno dei due tipi di destinazioni in Experience Platform. L&#39;esportazione di [!DNL Profile] genera un file contenente profili e attributi e utilizza dati PII non elaborati con le e-mail per l&#39;integrazione con le piattaforme di marketing e automazione delle e-mail.

**Frammento di profilo**: un frammento di profilo è costituito dalle informazioni di profilo relative a una sola identità dell&#39;elenco di identità esistenti per un cliente specifico.

**ID profilo**: un ID profilo è un identificatore generato automaticamente associato a un tipo di identità e rappresenta un profilo.

**Proprietà**: nel contesto dei tag, una proprietà è un contenitore per tutto ciò che è necessario per distribuire un set di tag.

## Q

**Query**: le query sono richieste di dati provenienti da tabelle di database.

**Query Editor**: Query Editor è uno strumento per la scrittura, la convalida e l&#39;invio di istruzioni SQL in [!DNL Query Service].

## R

**Real-time Customer Data Platform**: Adobe Real-time Customer Data Platform (Real-Time CDP) riunisce dati noti e sconosciuti dei clienti per creare profili cliente affidabili con integrazione semplificata, segmentazione intelligente e attivazione in tempo reale nel percorso di clienti digitali.

**Profilo cliente in tempo reale**: Profilo cliente in tempo reale (talvolta denominato Profilo) fornisce una visualizzazione olistica di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i dati dei clienti in singoli profili, offrendo account fruibili e con marca temporale per ogni interazione con il cliente.

**Ricetta**: una ricetta è il termine Adobe per una specifica di modello ed è un contenitore di livello superiore che rappresenta processi di apprendimento automatico specifici, algoritmi di intelligenza artificiale, logica di elaborazione e parametri di configurazione necessari per generare ed eseguire un modello addestrato e quindi contribuire a risolvere problemi di business specifici.

**Record**: un record è costituito da dati che persistono come righe in un set di dati.

**Dati record**: fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.

**Ricorrenza**: in [!DNL Query Service], una ricorrenza definisce se è pianificata l&#39;esecuzione di una query una sola volta o su base ricorrente.

**Rappresentazione**: in [!DNL Offer Decisioning] per rappresentazione si intendono le informazioni utilizzate da un canale per visualizzare un&#39;offerta, ad esempio la posizione o la lingua.

**Risorsa**: nel contesto dei tag, una risorsa è un termine generico che fa riferimento alle opzioni che l&#39;utente tagsa può configurare all&#39;interno dell&#39;ambiente client, inclusi estensioni, elementi dati e regole.

**Controllo dell&#39;accesso basato sul ruolo**: il controllo dell&#39;accesso basato sul ruolo consente agli amministratori di assegnare l&#39;accesso e le autorizzazioni agli utenti di Experience Platform. Le autorizzazioni includono la possibilità di visualizzare e/o utilizzare funzioni di Experience Platform, ad esempio la creazione di sandbox, la definizione di schemi e la gestione di set di dati.

**Regola**: nel contesto dei tag, una regola è una raccolta di componenti che definiscono un set specifico di eventi, condizioni e azioni da raggruppare in modo logico.

**Componente regola**: nel contesto dei tag, i componenti regola sono gli eventi, le condizioni e le azioni che costituiscono una regola.

**Runtime**: Runtime specifica un ambiente di runtime per una ricetta di apprendimento automatico. I runtime [!DNL Python], R, [!DNL Spark], PySpark e Tensorflow consentono di inserire un URL in un’immagine Docker per un’origine di ricetta.

## S

**Dati di esempio**: i dati di esempio sono un&#39;anteprima di un file di dati, in genere le prime 100 righe, che fornisce a un data scientist o a un ingegnere un&#39;idea dello schema o dei dati presenti nel file di dati.

**Sandbox**: una sandbox è un costrutto virtuale che suddivide una singola istanza Platform in un ambiente virtuale separato, al fine di agevolare lo sviluppo e l&#39;evoluzione delle applicazioni di esperienza digitale.

**Ripristino sandbox**: con un ripristino sandbox vengono eliminati tutti i dati, inclusi dati, profili e segmenti all&#39;interno di una sandbox. I ripristini delle sandbox possono influire sui dati connessi a destinazioni interne o esterne.

**Commutatore sandbox**: il controllo del commutatore sandbox in Experience Platform consente agli utenti di spostarsi tra le sandbox a cui hanno accesso. Il passaggio a una sandbox modificherà tutto il contenuto e l’accesso alle funzioni in base alle autorizzazioni.

**Pianificazione**: una pianificazione è una specifica definita dall&#39;utente relativa alla frequenza o alla frequenza di acquisizione dei dati da un&#39;origine dati di terze parti a Adobe Experience Platform.

**Punteggio**: il punteggio è il processo di generazione di informazioni dai dati utilizzando un modello addestrato.

**Schema**: uno schema è un insieme di regole che rappresentano e convalidano la struttura e il formato dei dati. Uno schema è composto da una classe e da gruppi di campi facoltativi e viene utilizzato per creare set di dati e flussi di dati. Uno schema può includere attributi comportamentali, marche temporali, identità, definizioni di attributi, relazioni e altro ancora.

**Gruppo di campi dello schema**: in Experience Data Model (XDM), un gruppo di campi dello schema consente agli utenti di estendere i campi riutilizzabili per definire uno o più attributi da includere in uno schema.

**Libreria schemi**: la libreria schemi contiene le risorse XDM standard del settore rese disponibili da Adobe, nonché le risorse personalizzate definite dall&#39;organizzazione.

**Schema Registry**: Schema Registry fornisce un&#39;interfaccia utente e un&#39;API RESTful utilizzate per visualizzare e gestire tutte le risorse relative allo schema nella Raccolta schemi.

**Chiave di accesso segreta**: una chiave di accesso segreta è una chiave S3 [!DNL Amazon] utilizzata insieme all&#39;ID della chiave di accesso per firmare le richieste AWS.

**Segmento**: un segmento è un insieme di regole che includono attributi e dati evento che qualificano un certo numero di profili per diventare un pubblico.

**Generatore di segmenti**: [!DNL Segment Builder] è un ambiente di sviluppo visivo utilizzato per creare le definizioni dei segmenti. Funge da componente comune di tutte le applicazioni che utilizzano Experience Platform Segmentation Service.

**Definizione segmento**: una definizione segmento è il set di regole utilizzato per descrivere le caratteristiche o il comportamento chiave di un pubblico di destinazione. Una volta concettualizzate, le regole delineate in una definizione di segmento vengono utilizzate per determinare i membri del pubblico idonei per un segmento.

**Metodo di valutazione del segmento**: esistono due metodi di valutazione del segmento: pianificato e su richiesta. La valutazione pianificata consente una pianificazione ricorrente per l’esecuzione di un processo di esportazione in un momento specifico, mentre la valutazione on-demand comporta la creazione di un processo di segmentazione per generare immediatamente il pubblico.

**Esportazione del segmento**: l&#39;esportazione del segmento è uno dei due tipi di destinazioni in Experience Platform. Con l’esportazione dei segmenti, puoi inviare i profili idonei e mappati sulla destinazione. Utilizza ID di segmenti e utenti e dati pseudonimi e in genere si integra con i social network e altre piattaforme di destinazione di contenuti multimediali digitali.

**ID segmento**: un ID segmento è un identificatore generato automaticamente associato a un segmento.

**Appartenenza a un segmento**: l&#39;appartenenza a un segmento visualizza i segmenti di cui fa attualmente parte un profilo.

**Regole segmento**: le regole segmento definiscono le condizioni che determinano se un profilo è idoneo per un segmento.

**Segmentazione**: la segmentazione è il processo di suddivisione di un ampio gruppo di clienti, potenziali clienti o consumatori in gruppi più piccoli che condividono attributi simili e rispondono in modo simile a specifiche strategie di marketing.

**Sensei ML Framework**: Sensei ML Framework è un framework di apprendimento automatico unificato che sfrutta i dati Experienci Platform per consentire ai data scientist di sviluppare servizi di intelligence basati su apprendimento automatico in modo più veloce, scalabile e riutilizzabile.

**Etichette sensibili (&quot;S&quot;)**: le etichette sensibili (&quot;S&quot;) vengono utilizzate per categorizzare i dati ritenuti sensibili, ad esempio diversi tipi di dati comportamentali o geografici che si desidera contrassegnare come sensibili.

**Servizi**: un potente framework per rendere operativi i servizi di intelligenza artificiale e machine learning sfruttando Adobe Intelligent Services. I servizi forniscono esperienze cliente personalizzate in tempo reale o rendono operativi servizi intelligenti personalizzati.

**Azione di marketing di personalizzazione identità singola**: azione di marketing che utilizza i dati per la personalizzazione del contenuto nel sito. Per personalizzazione nel sito si intende qualsiasi dato utilizzato per trarre conclusioni sugli interessi degli utenti e per selezionare i contenuti o gli annunci da distribuire in base a tali conclusioni.

**Etichetta di utilizzo dati S1**: un&#39;etichetta di utilizzo dati `S1` viene utilizzata per classificare i dati che specificano latitudine e longitudine e che possono essere utilizzati per determinare la posizione esatta di un dispositivo.

**Etichetta di utilizzo dati S2**: un&#39;etichetta di utilizzo dati `S2` viene utilizzata per classificare i dati che possono essere utilizzati per determinare un&#39;area recinto geografico definita in modo ampio.

**Source**: un&#39;origine è un termine generale per qualsiasi connettore di input in Platform. Vedi anche: Connettore Source

**Attributo Source**: un attributo di origine è un campo nel set di dati di origine. Gli attributi Source sono mappati sui campi schema di destinazione.

**Catalogo Source**: il catalogo di origine è l&#39;elenco dei connettori di origine disponibili in Experience Platform.

**Categoria Source**: una categoria di origine è un raggruppamento di origini con caratteristiche simili.

**Connettore Source**: i connettori Source (noti anche come origini) consentono agli utenti di acquisire facilmente dati da più origini, consentendo la strutturazione, l&#39;etichettatura e il miglioramento dei dati tramite i servizi Experience Platform. I dati possono essere acquisiti da diverse origini, ad esempio archiviazione basata su cloud, software di terze parti e sistemi di gestione delle relazioni con i clienti.

**Connessione in streaming**: una connessione in streaming è un endpoint univoco fornito da Adobe e associato alla tua organizzazione per lo streaming dei dati in Experience Platform.

**Spazio dei nomi identità standard**: gli spazi dei nomi identità standard sono spazi dei nomi identità predefiniti forniti da Adobe, che rappresentano soluzioni standard del settore comunemente utilizzate per identificare i clienti.

**Acquisizione in streaming**: l&#39;acquisizione in streaming ti consente di inviare dati da dispositivi lato client e lato server all&#39;Experience Platform in tempo reale.

**Segmentazione in streaming**: la segmentazione in streaming è un processo di selezione dati continuo che aggiorna i segmenti in risposta all&#39;attività dell&#39;utente. Dopo aver generato e salvato un segmento, la definizione del segmento viene applicata ai dati in arrivo in [!DNL Real-Time Customer Profile]. Le aggiunte e le rimozioni dei segmenti vengono elaborate regolarmente, garantendo la rilevanza del pubblico di destinazione.

**Visualizzazione sistema**: Visualizzazione sistema è una rappresentazione visiva dei set di dati di origine che passano attraverso [!DNL Real-Time Customer Profile] alle destinazioni.

## T

**Tag**: in Adobe Experience Platform, i tag forniscono gli strumenti necessari per distribuire, unificare e gestire le integrazioni di analisi, marketing e annunci pubblicitari necessarie per fornire ai clienti esperienze personalizzate su tutti i dispositivi client.

**Funzioni di destinazione**: nella mappatura delle funzioni, una funzione di destinazione è quella prevista da un modello.

**Dati della serie temporale**: i dati della serie temporale forniscono un&#39;istantanea del sistema nel momento in cui un oggetto record ha eseguito un&#39;azione direttamente o indirettamente.

**Modello addestrato**: un modello addestrato rappresenta l&#39;output eseguibile di un processo di apprendimento del modello, in cui un set di dati di addestramento è stato applicato all&#39;istanza del modello. Un modello addestrato conserverà un riferimento a qualsiasi servizio web intelligente creato da esso. Un modello addestrato è adatto per il punteggio e la creazione di un servizio web intelligente.

**Token**: un token è un tipo di sicurezza di autenticazione a due fattori che può essere utilizzato per autorizzare l&#39;utilizzo di servizi computer con [!DNL Query Service].

## U

**UCPA**: [[!DNL Utah Consumer Privacy Act]](https://le.utah.gov/~2022/bills/static/SB0227.html) crea il diritto per un consumatore di sapere quali dati personali un&#39;azienda raccoglie, in che modo utilizza i suoi dati personali e se l&#39;azienda vende i suoi dati personali. I consumatori possono richiedere all&#39;azienda di cancellare o smettere di vendere i propri dati personali.

**Schema di unione**: uno schema di unione è un consolidamento di schemi che condividono la stessa classe e sono stati abilitati per [!DNL Real-Time Customer Profile]. Per un’organizzazione possono esistere più schemi di unione, ma può esistere un solo schema di unione per classe.

## V

**VCDPA**: [[!DNL Virginia Consumer Data Protection Act (VCDPA)]](https://lis.virginia.gov/cgi-bin/legp604.exe?212+sum+HB2307) fornisce nuovi diritti sulla privacy dei dati ai residenti della Virginia (&quot;Consumatori&quot;), incluso il diritto di accesso, eliminazione e correzione dei dati personali. I consumatori hanno anche il diritto di non acconsentire alla vendita di dati personali, di non acconsentire alla profilazione basata su dati personali e al trattamento di finalità pubblicitarie personali.

## L

## X

**XDM**: vedi Experience Data Model (XDM).

**Evento decisione XDM**: Evento decisione XDM è una classe basata su serie temporali utilizzata per acquisire osservazioni sul risultato e il contesto di un&#39;attività di decisione. Ciò include informazioni su come è stata presa la decisione, quando si è verificata, quali opzioni sono state proposte (e scelte) e quale stato contestuale esisteva che ha influenzato la decisione o poteva essere osservato durante il processo decisionale.

**XDM ExperienceEvent**: XDM ExperienceEvent è una classe basata su serie temporali utilizzata per acquisire lo stato del sistema quando si è verificato un evento (o un set di eventi), inclusi il momento e l&#39;identità del soggetto interessato. Vedi anche: Evento esperienza

**Profilo individuale XDM**: XDM [!DNL Individual Profile] è una classe basata su record che costituisce una singola rappresentazione degli attributi sia dei soggetti identificati che parzialmente identificati. I profili altamente identificati possono essere utilizzati per comunicazioni personali o impegni mirati e possono contenere informazioni personali dettagliate come nome, genere, data di nascita, posizione e informazioni di contatto, inclusi numeri di telefono e indirizzi e-mail.

**Sistema XDM**: il sistema XDM rappresenta il framework che rende operativi gli schemi XDM da utilizzare nei servizi di Experience Platform a valle.

## Y

## Z
