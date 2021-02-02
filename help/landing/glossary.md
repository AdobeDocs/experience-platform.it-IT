---
keywords: ' Experience Platform;home;argomenti popolari'
solution: Experience Platform
title: Glossario di Adobe Experience Platform
topic: getting started
description: Un glossario di terminologia importante in Experience Platform.
translation-type: tm+mt
source-git-commit: a7ddba7c060e809478427ef3950360ccd67e6c60
workflow-type: tm+mt
source-wordcount: '7131'
ht-degree: 0%

---


# Glossario di Adobe Experience Platform {#adobe-experience-platform-glossary}

## A

**Controllo** di accesso: Il controllo dell&#39;accesso basato su ruolo consente agli amministratori di assegnare l&#39;accesso e le autorizzazioni agli utenti di  Experience Platform. Le autorizzazioni includono la possibilità di visualizzare e/o utilizzare  funzioni di Experience Platform, come la creazione di sandbox, la definizione di schemi e la gestione di set di dati.

**ID** chiave di accesso: Un ID chiave di accesso è un identificatore univoco associato a una chiave di accesso segreta  [!DNL Amazon] S3. L&#39;ID chiave di accesso e la chiave di accesso segreta sono utilizzati insieme per firmare le richieste [!DNL Amazon Web Services] (AWS).

**Azione**: In  [!DNL Platform Launch]un&#39;azione è un tipo specifico di componente regola che definisce cosa deve accadere dopo che si verifica un evento e le condizioni vengono valutate e passate.

**Attiva**: Attiva è l’azione eseguita da un utente per mappare uno o più segmenti a una destinazione come  [!DNL Oracle Eloqua],  [!DNL Google] o  [!DNL Salesforce Marketing Cloud].

**Attività**: In  [!DNL Offer Decisioning]un&#39;attività contiene la logica che informa la selezione di un&#39;offerta.

**Amministratore**: Uno o più utenti nell’organizzazione che possono configurare e personalizzare le autorizzazioni per  Experience Platform in Adobe Admin Console.

**Adobe Admin Console**: Adobe Admin Console fornisce una posizione centrale per la gestione delle adesioni  prodotto Adobe e l&#39;accesso per la vostra organizzazione. Tramite la console, gli amministratori possono concedere a gruppi di utenti autorizzazioni di accesso per diverse funzionalità della piattaforma, come &quot;Gestisci set di dati&quot;, &quot;Visualizza set di dati&quot; o &quot;Gestisci profili&quot;.

**Adobe Experience Platform**: Adobe Experience Platform standardizza dati e contenuti a livello aziendale, fornendo profili in tempo reale ai consumatori, consentendo la scienza dei dati e accelerando la velocità dei contenuti per promuovere la personalizzazione dell&#39;esperienza in tutto il percorso di clienti.

**Adobe Experience Platform Launch**:  [!DNL Platform Launch] è un ecosistema di gestione tag e SDK, integrato con  Experience Platform e  [!DNL Experience Cloud] applicazioni. [!DNL Platform Launch] fornisce strumenti per distribuire, unificare e gestire le integrazioni di analisi, marketing e pubblicità necessarie per fornire esperienze cliente rilevanti su tutti i dispositivi client.

**Adobe Experience Platform Query Service**: Consente agli analisti di dati di eseguire query su eventi e profili da utilizzare in analisi e machine learning. Con il servizio Query, gli esperti di analisi e analisi dei dati possono estrarre tutti i set di dati memorizzati in  Experience Platform (compresi i dati comportamentali, oltre ai punti vendita (POS), CRM (Customer Relationship Management) e altro ancora) e interrogare tali set di dati per rispondere a domande specifiche sui dati.

**Servizio** di segmentazione Adobe Experience Platform: Consente di creare segmenti e generare audience dai dati del profilo cliente in tempo reale. Tali tipi di pubblico possono quindi essere esportati nei propri dataset all&#39;interno del Data Lake.

**Servizi** intelligenti  Adobe: I servizi intelligenti come  Attribution AI e Customer AI sono modelli di machine-learning basati su intelligenza artificiale che sono progettati appositamente e richiedono  Experience Platform per funzionare e funzionare.

**Adobe I/O**:  Adobe I/O fa parte  Experience Platform e fornisce l&#39;accesso a tutto ciò che gli sviluppatori devono integrare, estendere e personalizzare la piattaforma, incluse API, eventi, console per sviluppatori e utili strumenti.

**Adobe Sensei**:  Adobe Sensei è la struttura di intelligence che dà potere  Experience Platform. Offre inoltre una serie di servizi AI che consentono ai marchi di migliorare la loro capacità di offrire esperienze cliente personalizzate in tempo reale.

**bucket** Amazon S3:  [!DNL Amazon S3] i bucket sono i contenitori di base per i dati memorizzati nell&#39; [!DNL Amazon] ecosistema. I bucket contengono oggetti, ogni oggetto viene memorizzato e recuperato utilizzando una chiave univoca assegnata dallo sviluppatore.

**connettore** Amazon S3: Il connettore  [!DNL Amazon] S3 consente ai clienti di  Experience Platform di collegarsi e accedere in modo sicuro ai dati  [!DNL Amazon] S3.

**Aggiungi strategia** di salvataggio: La strategia di salvataggio &quot;append&quot; è un&#39;opzione utilizzata quando si specificano dati di terze parti da assimilare tramite una connessione e si aggiungono nuovi dati o righe alla fine del dataset. Le righe precedentemente inserite non vengono toccate e solo le righe create dopo l&#39;ultima esecuzione pianificata vengono assimilate  Experience Platform. Tutte le righe modificate nel sistema di origine rimangono invariate  Experience Platform.

**Array**: Gli array vengono utilizzati per gli elementi ordinati con lo stesso tipo di dati.

**Intelligenza** artificiale: L&#39;intelligenza artificiale è una teoria e sviluppo di sistemi informatici in grado di eseguire attività che normalmente richiedono intelligenza umana, come la percezione visiva, il riconoscimento vocale, il processo decisionale e la traduzione tra le lingue.

**Attributi**: Gli attributi sono caratteristiche specifiche che rappresentano un profilo.

**Unione** attributi: Quando si definisce un criterio di unione utilizzando l&#39;API Profilo cliente in tempo reale, l&#39; `attributeMerge` oggetto indica il modo in cui il criterio di unione darà la priorità agli attributi del profilo in caso di conflitti di dati. Equivale a selezionare un [!UICONTROL Merge method] quando si definisce un criterio di unione nell&#39;interfaccia utente della piattaforma.

**Attribution AI**:  [!DNL Attribution AI] è un servizio intelligente  Adobe Sensei che offre funzionalità algoritmiche di attribuzione multicanale per l&#39;intero ciclo di vita del cliente.

**Pubblico**: Un&#39;audience è l&#39;insieme risultante di profili che soddisfano i criteri di una definizione di segmento.

**Dimensione** pubblico: Una dimensione di pubblico è il numero totale di profili che soddisfano i criteri di una definizione di segmento e soddisfano i requisiti per l&#39;appartenenza all&#39;audience.

**Snapshot** pubblico: Uno snapshot dell&#39;audience acquisisce tutti i profili idonei per i criteri del segmento al momento della segmentazione.

## B

**Backfill**: Per le origini pianificate, l&#39;opzione di backfill consente l&#39;inserimento di dati storici.

**Periodo** di recupero: Il periodo di backfill è un&#39;opzione che consente di impostare il tempo necessario per l&#39;acquisizione di dati storici di terze parti tramite una connessione di origine. Se si seleziona un periodo di backfill pari a &quot;always&quot;, verrà acquisita l&#39;intera cronologia dei dati di origine  Experience Platform.

**Batch**: Un batch è un insieme di dati raccolti in un periodo di tempo ed elaborati insieme come un&#39;unica unità. I set di dati sono composti da più batch.

**ID** batch: Un ID batch è un identificatore generato  Adobe per un batch di dati.

**Caricamento** batch: L’assimilazione batch consente di trasferire i dati  Experience Platform come file batch. I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità.

**Segmentazione** batch: La segmentazione in batch è un&#39;alternativa a un processo continuo di selezione dei dati e sposta tutti i dati di profilo contemporaneamente attraverso le definizioni dei segmenti per produrre i tipi di pubblico corrispondenti. Una volta creato, questo segmento viene salvato e memorizzato in modo che possa essere esportato per l’uso.

**Build**: In  [!DNL Platform Launch]una build è un file o un set di file che contiene tutte le configurazioni e il codice necessari per eseguire la logica di business contenuta all&#39;interno di una libreria, che consente di distribuire tale libreria sul sito Web o l&#39;app mobile.

**Strumenti** di Business Intelligence: Gli strumenti di Business Intelligence (BI) sono integrati principalmente con  [!DNL Experience Platform Query Service]. Gli strumenti BI sono tipi di software applicativi che raccolgono ed elaborano grandi quantità di dati non strutturati da sistemi interni ed esterni.

## C

**Capping**: In  [!DNL Offer Decisioning], i limiti (o limiti di frequenza) vengono utilizzati nelle regole di decisione per definire quante volte viene presentata un&#39;offerta. Esistono due tipi di estremità: quante volte un&#39;offerta può essere proposta tra il pubblico target combinato (chiamato &quot;Global Cap&quot;) e quante volte un&#39;offerta può essere proposta allo stesso utente finale (chiamato &quot;Profile Cap&quot;).

**Catalogo**: Nel contesto delle origini e delle destinazioni, un catalogo è una galleria con le connessioni disponibili alle applicazioni  Adobe e alle tecnologie di terze parti. Da non confondere con [!DNL Catalog Service].

**[!DNL Catalog Service]**:  [!DNL Catalog Service] (talvolta denominato  [!DNL Catalog]) è il sistema di record per la posizione dei dati e la linea di origine in Adobe Experience Platform. Mentre tutti i dati acquisiti  Experience Platform vengono memorizzati nel lago di dati come file e directory, [!DNL Catalog] contiene i metadati e la descrizione di tali file e directory a scopo di ricerca, monitoraggio e gestione dei dati.

**Classe**: In Experience Data Model (XDM), una classe definisce il set di campi più piccolo utilizzato per creare uno schema e definisce il comportamento di base dell&#39;oggetto business rappresentato dallo schema.

**Client**: Un client è uno strumento o un&#39;applicazione esterna che si connette  [!DNL Query Service] tramite il protocollo PostgreSQL o l&#39;API HTTP.

**Raccolta**: In  [!DNL Offer Decisioning], le raccolte sono sottoinsiemi di offerte basate su condizioni predefinite definite da un esperto di marketing, ad esempio la categoria dell&#39;offerta.

**Combinazione con azioni** di marketing PII: Un&#39;azione di marketing che combina qualsiasi informazione identificabile personalmente (PII) con dati anonimi. I contratti per i dati originati da reti pubblicitarie, server di annunci e provider di dati di terze parti spesso includono specifici divieti contrattuali sull&#39;uso di tali dati con dati direttamente identificabili.

**Interfaccia** della riga di comando: Un&#39;interfaccia della riga di comando è uno strumento basato su testo che può essere utilizzato per connettersi  [!DNL Query Service] per l&#39;esecuzione di query non elaborate.

**Composizione**: Una composizione è un raggruppamento di componenti che formano lo schema.

**Condizione**: In  [!DNL Platform Launch]una condizione è un componente regola che valuta un&#39;istruzione logica che deve restituire  `true` o  `false`. Tutte le condizioni devono essere valutate su `true` e tutte le condizioni di eccezione devono essere valutate su `false` prima di eseguire qualsiasi azione sulla regola.

**Console**: In  [!DNL Query Service]questa console sono incluse informazioni sullo stato e sul funzionamento di una query. La console visualizza lo stato della connessione su [!DNL Query Service], le operazioni di query in esecuzione ed eventuali messaggi di errore risultanti da tali query.

**Etichette** contratto (&quot;C&quot;): Le etichette di utilizzo dei dati del contratto (&quot;C&quot;) vengono utilizzate per classificare i dati che hanno obblighi contrattuali o che sono correlati a criteri di governance dei dati del cliente.

**Etichetta** contratto C1: Un&#39;etichetta di utilizzo dei dati  `C1` del contratto specifica che i dati possono essere esportati da Adobe Experience Cloud solo in un modulo aggregato, senza includere identificatori singoli o dispositivo. Ad esempio, i dati originati dai social network.

**Etichetta** contratto C2: Un&#39;etichetta di utilizzo dei dati  `C2` del contratto specifica i dati che non possono essere esportati a terzi. Alcuni provider di dati hanno termini nei loro contratti che vietano l&#39;esportazione di dati da dove è stato originariamente raccolto. Ad esempio, i contratti con i social network spesso limitano il trasferimento di dati che ricevi da loro. C2 è più restrittivo di C1, che richiede solo aggregazione e dati anonimi.

**Etichetta** contratto C3: Un&#39;etichetta di utilizzo dei dati  `C3` del contratto specifica i dati che non possono essere combinati o altrimenti utilizzati con informazioni direttamente identificabili. Alcuni fornitori di dati hanno termini nei loro contratti che vietano la combinazione o l&#39;uso di tali dati con informazioni direttamente identificabili. Ad esempio, i contratti per i dati originati da reti pubblicitarie, server di annunci e fornitori di dati di terze parti spesso includono specifici divieti contrattuali sull&#39;uso di dati direttamente identificabili.

**Etichetta** contratto C4: Un&#39;etichetta di utilizzo dei dati del  `C4` contratto specifica che i dati non possono essere utilizzati per il targeting di annunci o contenuti, sia sul sito che tra siti. C4 è l’etichetta più restrittiva in quanto comprende le etichette C5, C6 e C7.

**Etichetta** contratto C5: Un&#39;etichetta di utilizzo dei dati del  `C5` contratto specifica che i dati non possono essere utilizzati per il targeting tra siti di contenuti o annunci basati su interessi. Il targeting basato sugli interessi, o personalizzazione, si verifica se sono soddisfatte tre condizioni: I dati raccolti sul sito sono utilizzati per trarre conclusioni circa l&#39;interesse dell&#39;utente; è utilizzato in un altro contesto, ad esempio in un altro sito o in un&#39;altra app; e viene utilizzato per selezionare quali contenuti o annunci vengono serviti in base a tali inferenze.

**Etichetta** contratto C6: Un&#39;etichetta di utilizzo dei dati del  `C6` contratto specifica che i dati non possono essere utilizzati per il targeting degli annunci in sito. Il targeting degli annunci in loco include la selezione e la distribuzione di annunci pubblicitari sui siti Web o sulle app dell&#39;organizzazione, o per misurare la consegna e l&#39;efficacia di tali annunci. Ciò include l&#39;utilizzo di dati raccolti in precedenza sul sito in merito all&#39;interesse degli utenti per selezionare gli annunci, elaborare i dati su cosa gli annunci sono stati mostrati, quando e dove sono stati visualizzati, e se gli utenti hanno intrapreso qualsiasi azione correlata all&#39;annuncio, come ad esempio selezionare un annuncio o fare un acquisto.

**Etichetta** contratto C7: Un&#39;etichetta di utilizzo dei dati del  `C7` contratto specifica che i dati non possono essere utilizzati per il targeting on-site del contenuto. Il targeting dei contenuti in sito include la selezione e la distribuzione di contenuti sui siti Web o sulle app dell&#39;organizzazione, o per misurare la distribuzione e l&#39;efficacia di tali contenuti. Ciò include informazioni precedentemente raccolte sull’interesse degli utenti per la selezione del contenuto, l’elaborazione dei dati su quale contenuto è stato visualizzato, la frequenza o il periodo di visualizzazione, quando e dove è stato visualizzato, e se gli utenti hanno eseguito azioni relative al contenuto, ad esempio la selezione del contenuto.

**Etichetta** del contratto C8: Un&#39;etichetta di utilizzo dei dati del  `C8` contratto specifica che i dati non possono essere utilizzati per la misurazione dei siti Web o delle app dell&#39;organizzazione. Ciò non include il targeting basato sugli interessi, ovvero la raccolta di informazioni sull&#39;utilizzo di questo servizio per personalizzare successivamente contenuti e/o pubblicità in altri contesti.

**Etichetta** contratto C9: Un&#39;etichetta di utilizzo dei dati di un  `C9` contratto specifica che i dati non possono essere utilizzati nei flussi di lavoro di analisi dei dati. Alcuni contratti includono divieti espliciti sui dati utilizzati per la scienza dei dati. Talvolta tali termini sono formulati in termini che vietano l&#39;uso di dati per l&#39;intelligenza artificiale (AI), l&#39;apprendimento automatico (ML) o la modellazione.

**Etichetta** del contratto C10: Un&#39;etichetta di utilizzo dei dati  `C10` del contratto specifica che i dati non possono essere utilizzati per l&#39;attivazione dell&#39;identità unita. Alcuni criteri di utilizzo dei dati limitano l&#39;utilizzo di dati di identità uniti per la personalizzazione. L&#39;etichetta `C10` viene applicata automaticamente ai segmenti se i relativi criteri di unione utilizzano l&#39;opzione &quot;grafico privato&quot;.

**Colonna** Data creazione: Quando si seleziona una colonna Data di creazione, è possibile specificare dati di terze parti tramite una connessione di origine. Quando si seleziona l&#39;opzione Aggiungi strategia di salvataggio e lo schema del dataset contiene più campi data, è necessario scegliere dallo schema disponibile per specificare una colonna Chiave data di creazione. L&#39;opzione Data di creazione non è disponibile quando si seleziona la strategia di salvataggio per la sovrascrittura.

**Crea tabella come Seleziona**: Crea tabella come Seleziona (CTAS) è un comando SQL che, se eseguito come parte di una query SQL completa e valida, indicherà  [!DNL Query Service] di mantenere i risultati della query in un dataset. Potete creare un nuovo set di risultati, sovrascrivere i risultati precedenti o aggiungere risultati precedenti.

**Dati** intersito: I dati intersito sono la combinazione di dati provenienti da diversi siti, tra cui una combinazione di dati on-site e dati off-site o una combinazione di dati provenienti da diverse fonti off-site.

**Azione** di marketing per targeting tra siti: Un&#39;azione di marketing che utilizza i dati per il targeting degli annunci tra siti. La combinazione di dati provenienti da diversi siti, inclusa una combinazione di dati sul sito e dati fuori sede o una combinazione di dati provenienti da più fonti esterne al sito, è definita dati intersito. I dati intersito vengono in genere raccolti ed elaborati per trarre conclusioni sugli interessi dei clienti.

**Spazio dei nomi** identità personalizzato: Gli spazi dei nomi delle identità personalizzati possono essere creati dalla vostra organizzazione per rappresentare le identità per un caso aziendale o organizzazione specifico.

**Etichette** personalizzate: Le etichette di utilizzo dei dati personalizzate consentono di creare e applicare etichette specifiche ai campi di dati che soddisfano esigenze aziendali specifiche.

**AI** cliente: Customer AI è un servizio intelligente basato su  Adobe Sensei che arricchisce i profili dei clienti con proprietà basate su AI e potenzia la segmentazione dei clienti e le attività di targeting.

## D

**Dizionario** dati: In  [!DNL Platform Launch]un dizionario dati (noto anche come mappa dati) è un insieme di elementi dati definiti all&#39;interno di una proprietà.

**Elemento** dati: In  [!DNL Platform Launch], un elemento dati è un puntatore utilizzato all&#39;interno di regole ed estensioni per puntare a una specifica parte di dati esistente sul dispositivo client.

**Caricamento** dati: L&#39;assimilazione dei dati è il processo di aggiunta di dati da un&#39;origine a  Experience Platform. I dati possono essere trasferiti in Piattaforma in diversi modi, tra cui streaming, batch o aggiunti tramite connettori sorgente.

**Livello** dati: In  [!DNL Platform Launch]un livello dati è una struttura di dati esistente sul dispositivo client che contiene metadati sul contesto in cui viene visualizzata una pagina o uno schermo.

**Governance** dei dati: La governance dei dati comprende le strategie e le tecnologie utilizzate per garantire che i dati siano conformi alle normative e alle politiche organizzative in materia di utilizzo dei dati.

**Partner** per l&#39;integrazione dei dati: I partner per l&#39;integrazione dei dati semplificano e automatizzano il caricamento e la trasformazione di grandi volumi di dati da oltre 200 fonti a  Experience Platform senza scrivere codice.

**Etichette** set di dati: Le etichette di utilizzo dei dati possono essere aggiunte ai set di dati. Tutti i campi all&#39;interno del set di dati erediteranno le etichette del set di dati.

**Area di lavoro** dati:  [!DNL Data Science Workspace] all&#39;interno  Experience Platform consente ai clienti di creare modelli di machine-learning utilizzando i dati nelle applicazioni piattaforma e  Adobe per creare segmenti intelligenti, generare informazioni e fornire previsioni, consentendo di migliorare notevolmente le esperienze digitali degli utenti finali.

**Origine** dati: Un&#39;origine dati è un&#39;origine di dati designata dall&#39;utente. Esempi di un&#39;origine dati sono un&#39;app mobile, eventi di profilo e/o esperienza, eventi di profilo del sito Web o un CRM.

**Amministratore** dati: Un amministratore dei dati è la persona responsabile della gestione, della sorveglianza e dell&#39;esecuzione delle risorse di dati di un&#39;organizzazione. Un amministratore dei dati garantisce inoltre che le politiche di governance dei dati siano salvaguardate e mantenute in modo da essere conformi alle normative e alle politiche organizzative governative.

**Flusso** dati: Un flusso di dati è un insieme o una raccolta di messaggi che condividono lo stesso schema e vengono inviati dalla stessa origine.

**Tipo** di dati: Un tipo di dati è una risorsa XDM riutilizzabile che definisce un campo di tipo oggetto contenente più proprietà in una rappresentazione gerarchica.

**Etichette** di utilizzo dati: Le etichette di utilizzo dei dati consentono di classificare i dati che riflettono considerazioni relative alla privacy e condizioni contrattuali in modo da essere conformi alle normative e alle politiche aziendali. Le etichette di utilizzo dei dati aggiunte a un dataset vengono ereditate o applicate a tutti i campi all&#39;interno di tale dataset. Le etichette di utilizzo dei dati possono essere applicate direttamente ai campi.

**Flusso** di dati: Un flusso di dati è una pipeline virtuale di dati che fluisce nella piattaforma da un&#39;origine a una destinazione.

**Esecuzione** flusso di dati: Un&#39;esecuzione di un flusso di dati è un flusso di dati che arriva in  Experience Platform in base a una pianificazione specificata dall&#39;utente.

**Set** dati: Un dataset è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e campi (righe).

**ID** set di dati: Identificatore  generato dal Adobe per un set di dati assimilato.

**Output** set di dati: L&#39;output del set di dati fornisce un meccanismo per determinare l&#39;opzione &quot;Crea tabella come selezione&quot; da utilizzare per una particolare  [!DNL Query Service] esecuzione.

**Colonna** Delta: Una colonna delta consente di selezionare un campo di dati di origine che rappresenti una marca temporale per l&#39;assimilazione incrementale.

**Strategia** di salvataggio Delta: La strategia di salvataggio delta è un’opzione per l’assimilazione di dati di terze parti tramite una connessione di origine. L&#39;opzione consente all&#39;utente di specificare che le righe nuove o modificate dei dati di origine vengono assimilate  Experience Platform. Le nuove righe vengono aggiunte alla fine del dataset e le righe modificate vengono aggiornate nel dataset  Experience Platform.

**Descrittore**: In Experience Data Model (XDM), un descrittore è un set aggiuntivo di metadati relativi allo schema che descrive un comportamento specifico per un campo. I descrittori possono essere utilizzati  Experience Platform per comprendere il comportamento previsto dello schema, ad esempio la relazione tra due schemi.

**Destinazione**: Una destinazione è un termine generico per qualsiasi endpoint, ad esempio un&#39;applicazione di Adobe , una piattaforma pubblicitaria, un servizio di archiviazione cloud o un servizio di marketing, in cui un&#39;audience viene attivata e consegnata.

**Categoria** di destinazione: Una categoria di destinazione è un raggruppamento di destinazioni con caratteristiche simili.

**Catalogo** di destinazione: Un catalogo di destinazione è un elenco di destinazioni disponibili  Experience Platform.

**Regole** di chiamata diretta: In  [!DNL Platform Launch]una regola di chiamata diretta è una regola che viene eseguita quando viene chiamata direttamente dalla pagina, aggirando i sistemi di rilevamento e di ricerca degli eventi.

**Nome** visualizzato: In Experience Data Model (XDM), un nome visualizzato è un nome intuitivo per un campo mostrato nell&#39;interfaccia utente.

## E

**Offerta** ammissibile: Un&#39;offerta idonea può essere offerta in modo coerente a un profilo, in quanto soddisfa i vincoli definiti a monte.

**Regole** di ammissibilità: In  [!DNL Offer Decisioning], le regole di idoneità vengono applicate a un profilo correlato ai vincoli di calendario, pianificazione e limitazione.

**Azione** di marketing di targeting e-mail: Un&#39;azione di marketing che utilizza i dati nelle campagne di targeting delle e-mail.

**Incorpora codice**: In  [!DNL Platform Launch], il codice da incorporare è un tag script posizionato all&#39;interno dell&#39;HTML in un sito o in un ambiente. Il codice da incorporare indica al browser dove recuperare la build.

**Enumerazione**: Un&#39;enumerazione (enum) è un campo XDM vincolato a un insieme di valori predefiniti.

**Ambiente**: In  [!DNL Platform Launch]un ambiente è un insieme di istruzioni di distribuzione che specifica la consegna host e il formato file di una build. Prima di poter creare una libreria, è necessario essere associati a un ambiente.

**Diagnostica** errori: La diagnostica degli errori consente di generare messaggi di errore dettagliati per i batch assimilati. La soglia di errore consente di configurare la percentuale di errori accettabili prima che un batch abbia esito negativo.

**Evento**: In  [!DNL Platform Launch]un evento è un tipo specifico di componente regola, che è un trigger che si verifica su un dispositivo client per avviare l&#39;esecuzione di una regola.

**Entità** evento: Nel contesto della modellazione dei dati, le entità evento rappresentano concetti relativi alle azioni che un cliente può intraprendere, agli eventi di sistema o a qualsiasi altro concetto in cui desideri monitorare i cambiamenti nel tempo. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati sulla classe [!DNL XDM ExperienceEvent].

**Eventi**: Gli eventi sono i dati di comportamento associati a un profilo.

**Experience Data Model (XDM)** [!DNL Experience Data Model] (XDM) è un framework open-source che utilizza schemi standard per unificare i dati da utilizzare con  applicazioni di Experience Platform e Adobe Experience Cloud. XDM standardizza la struttura dei dati e accelera e semplifica il processo di acquisizione di informazioni da enormi quantità di dati.

**Esperimento**: Un esperimento è il processo di creazione di un modello preparato formando l&#39;istanza con una porzione campione di dati di produzione live. Questo è diverso da un modello addestrato che viene testato rispetto a un set di dati di test non valido. Questo è anche diverso dal concetto di un esperimento in alcuni contesti di machine-learning in cui in realtà significa un progetto di modellazione di esempio.

**Evento** esperienza: Un evento esperienza rappresenta un&#39;istantanea del sistema quando si verifica un&#39;interazione o un evento correlato a un&#39;esperienza cliente. Gli eventi di esperienza sono record di fatti immutabili di ciò che è accaduto e rappresentano ciò che è accaduto senza aggregazione o interpretazione. In Experience Data Model (XDM), questo concetto viene acquisito dalla classe [!DNL XDM ExperienceEvent].

**Estensione**: In  [!DNL Platform Launch]un&#39;estensione è un pacchetto di funzionalità aggiunte a una  [!DNL Platform Launch] proprietà. Un&#39;estensione è in genere incentrata su una particolare soluzione di marketing o analisi e fornisce gli strumenti necessari per implementare tale tecnologia in un ambiente client.

**Pacchetto** estensione: In  [!DNL Platform Launch], un pacchetto di estensione è un file ZIP creato e caricato da uno sviluppatore di estensioni che fornisce tutto il necessario per  [!DNL Platform Launch] gli utenti per installare l&#39;estensione all&#39;interno della loro proprietà. Un pacchetto di estensione contiene un manifesto che specifica informazioni sull&#39;estensione, il codice HTML/JavaScript necessario agli utenti finali per configurare il comportamento dell&#39;estensione [!DNL Platform Launch] e il codice JavaScript eseguibile fornito all&#39;ambiente client (se necessario).

## F

**Offerte** di fallback: Un&#39;offerta di fallback è l&#39;offerta predefinita visualizzata quando un utente finale non è idoneo per nessuna delle offerte della raccolta utilizzata.

**Mappatura** delle funzioni: Per mappatura delle funzioni si intende il processo di mappatura delle funzioni dai dati alle funzioni di input e destinazione richieste da un modello di apprendimento automatico.

**Campo**: Un campo è l&#39;elemento di livello più basso di un dataset, come definito dallo schema XDM del dataset. Ogni campo ha un nome a scopo di riferimento e un tipo per indicare il tipo di dati che contiene. I tipi di campo possono includere (ma non essere limitati a) numeri interi, stringhe, booleani e oggetti.

**Etichette** campo: Le etichette dei campi sono etichette di governance dei dati ereditate da un set di dati o applicate direttamente a un campo.

**Nome** campo: Un nome di campo viene utilizzato per fare riferimento al valore di un campo nelle query e nei servizi a valle.

**Frequenza**: In  [!DNL Query Service], la frequenza determina la frequenza con cui verrà eseguita una query pianificata ricorrente.

## G

**Geofence**: Una geofence è un limite geografico virtuale, definito dalla tecnologia GPS o RFID, che consente al software di attivare una risposta quando un dispositivo mobile entra o esce da un&#39;area particolare.

**GDPR (Regolamento generale sulla protezione dei dati)**: Il regolamento generale sulla protezione dei dati (GDPR) è un quadro giuridico che definisce le linee guida per la raccolta e il trattamento di informazioni personali di individui all&#39;interno dell&#39;Unione europea (UE). Il GDPR stabilisce i principi per la gestione dei dati e i diritti dei singoli e copre tutte le società che si occupano dei dati dei cittadini dell&#39;UE.

## H

**Host**: In  [!DNL Platform Launch]un host specifica il percorso, il dominio e le credenziali utente necessarie  [!DNL Platform Launch] per distribuire una build.

## I

**Identità**: Un&#39;identità è un identificatore che rappresenta in modo univoco un singolo cliente, ad esempio un ID cookie, un ID dispositivo o un ID e-mail.

**Campi** identità: I campi di identità sono campi XDM utilizzati per unire informazioni sui singoli clienti provenienti da più origini dati. Affinché lo schema sia abilitato per l&#39;uso nel profilo cliente in tempo reale, è necessario definire una singola identità primaria.

**Etichette** identità (&quot;I&quot;): Le etichette di utilizzo dei dati di identità (&quot;I&quot;) vengono utilizzate per classificare i dati in grado di identificare o contattare una persona specifica.

**Grafico** identità: Un grafico di identità è una mappa di relazioni tra identità unite e unite esistenti per un singolo cliente. Ogni grafico di identità si aggiorna in tempo quasi reale con l&#39;attività del cliente. La struttura comune delle relazioni di identità nei dati è rappresentata dalla [!UICONTROL Private Graph], che funge da modello strutturale per ogni singolo grafico di identità.

**Spazio dei nomi** identità: Uno spazio dei nomi di identità definisce il contesto di un identificatore, ad esempio un indirizzo e-mail o un ID CRM.

**Servizio** identità:  [!DNL Experience Platform Identity Service] consente la creazione e la gestione di tipi di identità, consentendo di collegare le identità dei clienti tra dispositivi e canali. La capacità del servizio di collegare le identità permette al profilo cliente in tempo reale di fornire una rappresentazione completa di ogni singolo cliente.

**Cucitura** identità: L&#39;unione delle identità è il processo di identificazione dei frammenti di dati e di unione dei frammenti per formare un record di profilo completo.

**Simbolo** di identità: Un simbolo di identità è un&#39;abbreviazione di uno spazio nomi di identità che può essere utilizzato come riferimento nelle API.

**Valore** identità: Un valore di identità, combinato con uno spazio dei nomi di identità, è un identificatore che rappresenta un singolo, un&#39;organizzazione o una risorsa univoca. Quando i dati del record corrispondono tra i frammenti di profilo, lo spazio nomi e il valore dell&#39;identità devono corrispondere.

**Etichetta** utilizzo dati I1: L&#39;etichetta di utilizzo  `I1` dei dati viene utilizzata per classificare i dati in grado di identificare o contattare direttamente una persona specifica anziché un dispositivo.

**Etichetta** utilizzo dati I2: L&#39;etichetta di utilizzo  `I2` dei dati viene utilizzata per classificare i dati utilizzabili in combinazione con qualsiasi altro dato per identificare o contattare indirettamente una persona specifica.

**Organizzazione** IMS: Un&#39;organizzazione IMS (a volte denominata IMS Org) è il nome utilizzato per identificare una società o un gruppo specifico all&#39;interno di una società attraverso  prodotti di Adobe. Gli amministratori possono configurare e gestire l&#39;accesso e le autorizzazioni delle funzioni per gli utenti di un&#39;organizzazione.

**Ingestione**: Vedere assimilazione dei dati.

**Pianificazione** di ingestione: Una pianificazione dell’assimilazione fornisce opzioni basate sul tempo durante l’assimilazione da un’origine a  un Experience Platform.

**Funzione** di ingresso: Una funzione di input è specificata nella mappatura delle funzioni e utilizzata da un modello di apprendimento automatico per fare previsioni.

**[!DNL Intelligent Services]**:  [!DNL Intelligent Services] come  [!DNL Attribution AI] e  [!DNL Customer AI] sono modelli di machine-learning, basati sull&#39;intelligenza artificiale che richiedono l&#39;esecuzione e il funzionamento di  Experience Platform (o applicazioni integrate sulla piattaforma come Real-time Customer Data Platform).

**Targeting o personalizzazione** basate sugli interessi: Il targeting basato sugli interessi, noto anche come personalizzazione, si verifica se sono soddisfatte tre condizioni:

1. I dati raccolti sul sito vengono utilizzati per ricavare deduzioni sull&#39;interesse dell&#39;utente.
1. I dati vengono utilizzati in un altro contesto, ad esempio in un altro sito o in un&#39;altra app (fuori sito).
1. I dati vengono utilizzati per selezionare quali contenuti o annunci vengono serviti in base a tali inferenze.

## J

**[!DNL JupyterLab]**: Interfaccia open-source basata su Web per Project  [!DNL Jupyter] integrata nell’interfaccia utente della piattaforma.

**[!DNL Jupyter Notebook]**: Integrato con JupyterLab, Jupyter Notebooks consente di eseguire la pulizia e la trasformazione dei dati, la simulazione numerica, la modellazione statistica, la visualizzazione dei dati, l&#39;apprendimento automatico e altro ancora sui dati del Experience Platform  in diverse lingue come Python, Scala e PySpark.

## K

## L

**Libreria**: In  [!DNL Platform Launch], una libreria è un insieme di logica di business che contiene istruzioni sul funzionamento della  [!DNL Platform Launch] libreria sul dispositivo client.

**Entità** di ricerca: Nel contesto della modellazione dei dati, le entità di ricerca rappresentano concetti che possono essere correlati a una singola persona, ma che non possono essere utilizzati direttamente per identificare l&#39;individuo. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati su classi XDM (Experience Data Model) personalizzate.

## M

**Apprendimento automatico (ML)**: L&#39;apprendimento automatico è il campo di studio che consente ai computer di imparare senza essere esplicitamente programmati.

**Modello** di apprendimento automatico: Un modello di machine-learning è un&#39;istanza di una ricetta di machine-learning che viene formata utilizzando dati storici e configurazioni per risolvere un caso d&#39;uso aziendale. In Adobe Experience Platform Data Science Workspace, i modelli di apprendimento automatico sono denominati ricette.

**Mapping**: La mappatura dei dati è il processo di mappatura dei campi di dati di origine ai campi di destinazione correlati in una destinazione.

**Azione** di marketing: Nel framework di governance dei dati, un&#39;azione di marketing (nota anche come caso d&#39;uso del marketing) è un&#39;azione che un consumatore di dati  Experience Platform assume, per la quale è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati.

**Metodo** Merge: Quando si definisce un criterio di unione utilizzando l&#39;interfaccia utente della piattaforma, il metodo di unione specifica in che modo i frammenti di dati devono avere priorità in caso di conflitto. Quando si utilizza l&#39;API Profilo cliente in tempo reale per definire un criterio di unione, il metodo di unione viene determinato utilizzando l&#39;oggetto `attributeMerge`.

**Unisci criterio**: I criteri di unione sono regole utilizzate  Experience Platform per determinare in che modo i frammenti di dati del cliente provenienti da più origini verranno combinati per creare un singolo profilo. Quando si verifica un conflitto di dati, il criterio di unione determina quali dati devono essere classificati come priorità per l&#39;inclusione nel profilo.

**Mixin**: In Experience Data Model (XDM), un mixin consente agli utenti di estendere i campi riutilizzabili per definire uno o più attributi destinati ad essere inclusi in uno schema.

**Modulo**: In  [!DNL Platform Launch], un modulo è un frammento di codice JavaScript eseguibile fornito da un&#39;estensione, che esegue azioni in un ambiente client senza dover creare una regola.

## N

**Sandbox** non di produzione: Le sandbox non di produzione sono sandbox solitamente utilizzate per esperimenti di sviluppo, test o test. A differenza delle sandbox di produzione, le sandbox non di produzione possono essere reimpostate ed eliminate.

**[!DNL Notebooks]**:  [!DNL Notebooks] sono creati utilizzando  [!DNL Jupyter Notebook] e possono essere eseguiti per eseguire l&#39;analisi dei dati.

## O

**Offerta**: Un&#39;offerta è un messaggio di marketing contenente una proposta commerciale o di vendita a un (potenziale) cliente. Le offerte hanno spesso regole specifiche che determinano chi può visualizzarle o riceverle.

**[!DNL Offer Decisioning]**:  [!DNL Offer Decisioning] consente agli esperti di marketing di gestire le regole e i modelli formati di proposte quando interagiscono con gli utenti finali in base ai dati raccolti tra canali e applicazioni.

**Libreria** offerta: La libreria delle offerte è una libreria centrale utilizzata per gestire offerte personalizzate e di fallback, regole decisionali e attività.

**Azione** di marketing per la personalizzazione di siti: Un&#39;azione di marketing che utilizza i dati per la personalizzazione dei contenuti on-site. Per personalizzazione in sito si intende qualsiasi dato utilizzato per fare deduzioni sugli interessi degli utenti e utilizzato per selezionare quali contenuti o annunci vengono serviti in base a tali inferenze.

**Azione** di marketing di targeting on-site: Un&#39;azione di marketing che utilizza i dati per gli annunci sul sito, compresa la selezione e la consegna di annunci pubblicitari sui siti Web o sulle app dell&#39;organizzazione, o per misurare la consegna e l&#39;efficacia di tali annunci.

**Sovrascrivi strategia** di salvataggio: La strategia di salvataggio &quot;Sovrascrivi&quot; è un&#39;opzione per l&#39;acquisizione di dati di terze parti tramite una connessione, in cui è possibile specificare se i dati acquisiti verranno sovrascritti in base a una pianificazione specificata.

## P

**assimilazione** parziale: L&#39;assimilazione parziale consente l&#39;inserimento di record validi di dati batch entro una soglia di errore specificata. È possibile scaricare o accedere alla diagnostica degli errori per i record non riusciti in [!UICONTROL Monitoring] o [!UICONTROL Sources] panoramica dell&#39;esecuzione del flusso di dati.

**Parquet, file**: Un file Parquet è un formato di file di memorizzazione columnar con complesse strutture di dati nidificate. I file di parquet sono necessari per aggiungere dati per compilare un set di dati dello schema.

**Offerte** personalizzate: Un&#39;offerta personalizzata è un messaggio di marketing personalizzabile basato su regole e vincoli di idoneità.

**Posizionamenti**: Un posizionamento è la posizione e il contesto in cui un&#39;offerta viene visualizzata per un utente finale.

**Area di lavoro** Criteri: Area di lavoro nell’interfaccia utente della piattaforma che consente agli amministratori dei dati di visualizzare e gestire le etichette e i criteri di utilizzo dei dati per la propria organizzazione.

**Criteri**: Un criterio di utilizzo dei dati è una regola che specifica le azioni di marketing limitate in base all&#39;applicazione di etichette di utilizzo applicate ai dati della piattaforma.

**Applicazione** delle regole: Consente di applicare criteri di utilizzo dei dati con azioni di marketing applicate per impedire operazioni di dati che costituiscono violazioni dei criteri all&#39;interno di un&#39;organizzazione.

**Chiave** principale: Una chiave primaria è una designazione in uno schema per identificare in modo univoco tutti i record.

**Priorità**: In  [!DNL Offer Decisioning], la priorità viene utilizzata per classificare le offerte che soddisfano tutti i vincoli, ad esempio i requisiti di idoneità, il calendario e i limiti.

**Grafico** di identità privata: Il grafico dell&#39;identità privata (a volte denominato grafico privato) è una mappa privata delle relazioni tra identità unite e collegate, basata sui dati di prime parti ed è visibile solo dalla vostra organizzazione. Esiste un solo grafico privato per ciascuna organizzazione e funge da modello strutturale per i grafici identità generati per ciascun cliente che interagisce con il proprio marchio.

**Profilo** di prodotto: I profili di prodotto consentono agli amministratori di concedere agli utenti l&#39;accesso a tutti i servizi associati a  Experience Platform o a un sottoinsieme di essi.

**Sandbox** produzione: Una sandbox di produzione è una sandbox destinata all&#39;utilizzo nell&#39;ambiente di produzione. A differenza delle sandbox non di produzione, non è possibile ripristinare o eliminare le sandbox di produzione.

**Profilo**: Da non confondere con il profilo cliente in tempo reale come servizio, un profilo è una rappresentazione completa di un singolo cliente, costruito da record uniti e dati di serie temporali provenienti da più origini.

**Accesso** profilo: L&#39; `/entities` endpoint nell&#39;API del profilo cliente in tempo reale consente di accedere ai dati dei record e agli eventi delle serie temporali nell&#39;archivio dati del profilo. Vedi anche: Entità profilo

**Dati** profilo: I dati del profilo si riferiscono a tutti i dati presenti nell&#39;archivio dati del profilo.

**Archivio** dati profilo: L&#39;archivio dati profilo (a volte denominato Profile Store) è un sistema di archiviazione dati separato dal lago dati, utilizzato da Real-time Customer Profile per creare e archiviare i profili.

**Entità** profilo: Le entità profilo rappresentano gli attributi relativi a una singola persona, in genere un cliente. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati sulla classe [!DNL XDM Individual Profile]. Vedi anche: Accesso profilo

**Esportazione** profilo:  [!DNL Profile] export è uno dei due tipi di destinazioni nel Experience Platform . [!DNL Profile] export genera un file contenente profili e attributi e utilizza dati PII non elaborati con e-mail per l&#39;integrazione con le piattaforme di marketing e automazione e-mail.

**Frammento** profilo: Un frammento di profilo è l&#39;informazione di profilo per una sola identità inclusa nell&#39;elenco di identità esistenti per un cliente specifico.

**ID** profilo: Un ID profilo è un identificatore generato automaticamente associato a un tipo di identità e rappresenta un profilo.

**Proprietà**: In  [!DNL Platform Launch], una proprietà è un contenitore per tutto il necessario per distribuire un set di tag.

## Q

**Query**: Le query sono richieste di dati provenienti da tabelle di database.

**Editor** query: Editor query è uno strumento per scrivere, convalidare e inviare istruzioni SQL in  [!DNL Query Service].

## R

**Piattaforma** dati cliente in tempo reale:  [!DNL Real-time Customer Data Platform] riunisce dati noti e sconosciuti dei clienti per creare profili cliente affidabili con integrazione semplificata, segmentazione intelligente e attivazione in tempo reale nel percorso di clienti digitali.

**Profilo** cliente in tempo reale: Il profilo cliente in tempo reale (talvolta denominato Profilo) fornisce una visualizzazione olistica di ogni singolo cliente combinando dati da più canali, inclusi online, offline, CRM e terze parti. Il profilo consente di consolidare i dati dei clienti in singoli profili che offrono account con marca temporale e fruibili per ogni interazione con il cliente.

**Ricetta**: Una ricetta è  termine  Adobe per una specifica di modello ed è un contenitore di primo livello che rappresenta specifici processi di machine-learning, algoritmi AI, logica di elaborazione e parametri di configurazione necessari per creare ed eseguire un modello qualificato e quindi aiutare a risolvere specifici problemi aziendali.

**Record**: Un record è un dato che persiste come righe in un dataset.

**Record data**: Fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.

**Ricorrenza**: In  [!DNL Query Service]una ricorrenza definisce se la query deve essere eseguita una sola volta o su base ricorrente.

**Rappresentazione**: In  [!DNL Offer Decisioning]una rappresentazione sono informazioni utilizzate da un canale per visualizzare un&#39;offerta, ad esempio posizione o lingua.

**Risorsa**: In  [!DNL Platform Launch]una risorsa è un termine generico che fa riferimento alle opzioni che l&#39; [!DNL Platform Launch] utente può configurare all&#39;interno dell&#39;ambiente client, incluse estensioni, elementi di dati e regole.

**Controllo** dell&#39;accesso basato sul ruolo: Il controllo dell&#39;accesso basato su ruolo consente agli amministratori di assegnare l&#39;accesso e le autorizzazioni agli utenti di  Experience Platform. Le autorizzazioni includono la possibilità di visualizzare e/o utilizzare  funzioni di Experience Platform, come la creazione di sandbox, la definizione di schemi e la gestione di set di dati.

**Regola**: In  [!DNL Platform Launch]una regola è un insieme di componenti che definiscono un set specifico di eventi, condizioni e azioni da raggruppare in modo logico.

**Componente** regola: In  [!DNL Platform Launch]i componenti regola sono gli eventi, le condizioni e le azioni che costituiscono una regola.

**Runtime**: Runtime specifica un ambiente di runtime per una ricetta di machine-learning. [!DNL Python]I runtime  [!DNL Spark], R, PySpark e Tensorflow consentono di inserire un URL a un&#39;immagine Docker per una sorgente di ricette.

## S

**Dati** di esempio: I dati di esempio sono un&#39;anteprima di un file di dati, in genere le prime 100 righe, che fornisce a un esperto di dati o a un tecnico un&#39;idea dello schema o dei dati contenuti nel file di dati.

**Sandbox**: Una sandbox è un costrutto virtuale che divide una singola istanza della piattaforma in un ambiente virtuale separato, al fine di contribuire allo sviluppo e all&#39;evoluzione di applicazioni per esperienze digitali.

**Ripristino** sandbox: Una reimpostazione sandbox elimina tutti i dati, inclusi dati, profili e segmenti, all&#39;interno di una sandbox. I predefiniti sandbox possono influenzare i dati collegati a destinazioni interne o esterne.

**Switcher** sandbox: Il controllo dello switcher sandbox in  Experience Platform consente agli utenti di spostarsi tra le sandbox a cui hanno accesso. La sostituzione di una sandbox modificherà tutto il contenuto e potrebbe modificare l&#39;accesso alle funzioni in base alle autorizzazioni.

**Pianificazione**: Una pianificazione è una specifica definita dall&#39;utente relativa alla frequenza o alla cadenza dell&#39;assimilazione dei dati da un&#39;origine dati di terze parti ad Adobe Experience Platform.

**Punteggio**: Il punteggio è il processo di generazione di informazioni dai dati utilizzando un modello qualificato.

**Schema**: Uno schema è un insieme di regole che rappresentano e convalidano la struttura e il formato dei dati. Uno schema è composto da una classe e da mixin facoltativi ed è utilizzato per creare dataset e datastreams. Uno schema può includere attributi comportamentali, marche temporali, identità, definizioni di attributi, relazioni e altro ancora.

**Libreria** schema: La Libreria schema contiene risorse XDM standard di settore rese disponibili dal Adobe , nonché risorse personalizzate definite dall&#39;organizzazione.

**Registro** schema: Il Registro di sistema dello schema fornisce un&#39;interfaccia utente e RESTful API utilizzate per visualizzare e gestire tutte le risorse relative allo schema nella Libreria schema.

**Chiave** di accesso segreta: Una chiave di accesso segreta è una chiave  [!DNL Amazon] S3 utilizzata insieme all&#39;ID della chiave di accesso per firmare le richieste AWS.

**Segmento**: Un segmento è un insieme di regole che includono attributi e dati evento che qualificano un numero di profili per diventare un pubblico.

**Generatore** di segmenti: L’ambiente di sviluppo visivo  [!DNL Segment Builder] è utilizzato per creare definizioni di segmenti. Funge da componente comune di tutte le applicazioni che utilizzano  Experience Platform Segmentation Service.

**Definizione** segmento: Per definizione del segmento si intende il set di regole utilizzato per descrivere le caratteristiche o il comportamento chiave di un&#39;audience target. Una volta concettualizzate, le regole delineate in una definizione di segmento vengono utilizzate per determinare i membri di pubblico idonei per un segmento.

**Metodo** di valutazione del segmento: Esistono due metodi di valutazione dei segmenti: pianificato e on-demand. La valutazione pianificata consente di eseguire una pianificazione periodica per eseguire un processo di esportazione in un momento specifico, mentre la valutazione su richiesta comporta la creazione di un processo di segmento per creare immediatamente l&#39;audience.

**Esportazione** segmento: L&#39;esportazione dei segmenti è uno dei due tipi di destinazioni nel Experience Platform . Con l’esportazione dei segmenti, potete inviare i profili idonei e mappati sulla destinazione. Utilizza gli ID di segmento e utente e i dati pseudonimi e si integra solitamente con i social network e altre piattaforme di destinazione per i media digitali.

**ID** segmento: Un ID segmento è un identificatore generato automaticamente associato a un segmento.

**Appartenenza** al segmento: L&#39;appartenenza al segmento indica i segmenti di cui un profilo fa attualmente parte.

**Regole** segmento: Le regole del segmento definiscono le condizioni che determinano se un profilo è idoneo per un segmento.

**Segmentazione**: La segmentazione è il processo che consente di dividere un ampio gruppo di clienti, potenziali o consumatori in gruppi più piccoli che condividono attributi simili e risponderanno in modo simile a strategie di marketing specifiche.

**Sensei ML Framework**: Sensei ML Framework è un framework di machine-learning unificato (ML) che sfrutta  dati di Experience Platform per consentire agli scienziati dei dati di sviluppare servizi di intelligence guidati da ML in modo più veloce, scalabile e riutilizzabile.

**Etichette** sensibili (&quot;S&quot;): Le etichette sensibili (&quot;S&quot;) vengono utilizzate per classificare i dati ritenuti riservati, ad esempio tipi diversi di dati comportamentali o geografici che si desidera contrassegnare come sensibili.

**Servizi**: Un framework potente per l&#39;operazionalizzazione dei servizi AI e ML sfruttando  Adobe Intelligent Services. I servizi offrono esperienze cliente personalizzate in tempo reale o offrono servizi intelligenti personalizzati.

**Singola azione** di marketing per la personalizzazione delle identità: Un&#39;azione di marketing che utilizza i dati per la personalizzazione dei contenuti on-site. Per personalizzazione in sito si intende qualsiasi dato utilizzato per fare deduzioni sugli interessi degli utenti e utilizzato per selezionare quali contenuti o annunci vengono serviti in base a tali inferenze.

**Etichetta** di utilizzo dati S1: Un&#39;etichetta di utilizzo  `S1` dei dati viene utilizzata per classificare i dati che specificano latitudine e longitudine, utilizzabili per determinare la posizione esatta di un dispositivo.

**Etichetta** di utilizzo dati S2: Un&#39;etichetta di utilizzo  `S2` dei dati viene utilizzata per classificare i dati che possono essere utilizzati per determinare un&#39;area geografica definita in senso ampio.

**Origine**: Un&#39;origine è un termine generico per qualsiasi connettore di ingresso in Platform. Vedi anche: Connettore origine

**Attributo** di origine: Un attributo di origine è un campo nel set di dati di origine. Gli attributi di origine sono mappati ai campi dello schema di destinazione.

**Catalogo** di origine: Il catalogo di origine è l&#39;elenco dei connettori di origine disponibili nel Experience Platform .

**Categoria** di origine: Una categoria di origine è un raggruppamento di origini con caratteristiche simili.

**Connettore** di origine: I connettori di origine (noti anche come sorgenti) consentono agli utenti di acquisire facilmente dati da più origini, consentendo la strutturazione, l&#39;etichettatura e il miglioramento dei dati mediante  servizi di Experience Platform. I dati possono essere acquisiti da una varietà di fonti, come l&#39;archiviazione basata su cloud, il software di terze parti e i sistemi CRM.

**Connessione** di streaming: Una connessione di streaming è un endpoint univoco fornito da  Adobe e collegato all&#39;organizzazione IMS di un cliente per lo streaming dei dati in  Experience Platform.

**Spazio dei nomi** identità standard: Gli spazi dei nomi di identità standard sono spazi dei nomi di identità predefiniti forniti da  Adobe, che rappresentano soluzioni standard di settore comunemente utilizzate per identificare i clienti.

**Caricamento** streaming: L’assimilazione dello streaming consente di inviare dati dai dispositivi lato client e lato server al Experience Platform  in tempo reale.

**Segmentazione** in streaming: La segmentazione in streaming è un processo continuo di selezione dei dati che aggiorna i segmenti in risposta all&#39;attività degli utenti. Una volta creato e salvato un segmento, la definizione del segmento viene applicata rispetto ai dati in arrivo a [!DNL Real-time Customer Profile]. L&#39;aggiunta e l&#39;eliminazione di segmenti vengono elaborati regolarmente, garantendo che il pubblico di destinazione rimanga rilevante.

**Vista** di sistema: Vista di sistema è una rappresentazione visiva dei set di dati sorgente che scorrono  [!DNL Real-time Customer Profile] verso le destinazioni.

## T

**Funzioni** di destinazione: Nella mappatura delle feature, una feature di destinazione è la feature prevista da un modello.

**Dati** serie temporali: I dati relativi alle serie temporali forniscono un&#39;istantanea del sistema nel momento in cui un&#39;azione è stata eseguita direttamente o indirettamente da un soggetto del record.

**Modello** formato: Un modello preparato rappresenta l&#39;output eseguibile di un processo di formazione basato su modelli, in cui un insieme di dati di formazione è stato applicato all&#39;istanza del modello. Un modello qualificato manterrà un riferimento a qualsiasi servizio Web intelligente creato da esso. Un modello qualificato è adatto per il punteggio e la creazione di un servizio Web intelligente.

**Token**: Un token è un tipo di protezione di autenticazione a due fattori che può essere utilizzato per autorizzare l&#39;uso di servizi computer con  [!DNL Query Service].

## U

**Schema** unione: Uno schema unione è un consolidamento di schemi che condividono la stessa classe e per i quali sono stati abilitati  [!DNL Real-time Customer Profile]. Possono esistere più schemi di unione per un&#39;organizzazione, ma può essere presente un solo schema di unione per classe.

## V

## W

## X

**XDM**: Consulta Experience Data Model (XDM).

**Evento** decisionale XDM: XDM Decision Event è una classe basata su serie temporale utilizzata per acquisire le osservazioni sul risultato e il contesto di un&#39;attività decisionale. Ciò include informazioni su come è stata presa la decisione, quando si è verificata, quali opzioni sono state proposte (e scelte), e quale stato contestuale esisteva che ha influenzato la decisione o poteva essere osservato durante il processo decisionale.

**XDM ExperienceEvent**: XDM ExperienceEvent è una classe basata su serie temporale utilizzata per acquisire lo stato del sistema quando si verifica un evento (o un set di eventi), incluso il punto nel tempo e l&#39;identità dell&#39;oggetto interessato. Vedi anche: Evento esperienza

**Profilo** individuale XDM: XDM  [!DNL Individual Profile] è una classe basata su record che forma una singola rappresentazione degli attributi di soggetti identificati e parzialmente identificati. I profili altamente identificati possono essere utilizzati per comunicazioni personali o per impegni mirati e possono contenere informazioni personali dettagliate come nome, sesso, data di nascita, luogo e informazioni di contatto, inclusi numeri di telefono e indirizzi e-mail.

**Sistema** XDM: XDM System rappresenta il framework che rende operativi gli schemi XDM da utilizzare nei servizi  Experienci Platform a valle.

## Y

## Z
