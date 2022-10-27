---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Glossario Adobe Experience Platform
topic-legacy: getting started
description: Un glossario di terminologia importante in Experience Platform.
exl-id: 00eae5f5-7dfa-45ac-aff9-9e1769a3a53a
source-git-commit: b9b33a6c1df0810db32f3253205221fed8957dd5
workflow-type: tm+mt
source-wordcount: '7435'
ht-degree: 0%

---

# Glossario di Adobe Experience Platform {#adobe-experience-platform-glossary}

## A

**Controllo dell&#39;accesso**: Il controllo degli accessi basato su ruoli consente agli amministratori di assegnare accesso e autorizzazioni agli utenti di Experience Platform. Le autorizzazioni includono la possibilità di visualizzare e/o utilizzare funzionalità di Experience Platform, ad esempio la creazione di sandbox, la definizione di schemi e la gestione di set di dati.

**ID chiave di accesso**: Un ID chiave di accesso è un identificatore univoco associato a un [!DNL Amazon] Chiave di accesso segreto S3. L&#39;ID chiave di accesso e la chiave di accesso segreta sono utilizzati insieme per firmare [!DNL Amazon Web Services] Richieste (AWS).

**Azione**: Nel contesto dei tag, un’azione è un tipo specifico di componente regola che definisce cosa deve accadere dopo che si verifica un evento e le condizioni vengono valutate e passate.

**Attiva**: Attiva è l’azione intrapresa da un utente per mappare un segmento o più profili a una destinazione come [!DNL Oracle Eloqua], [!DNL Google]oppure [!DNL Salesforce Marketing Cloud].

**Attività**: In [!DNL Offer Decisioning], un’attività contiene la logica che informa la selezione di un’offerta.

**Amministratore**: Uno o più utenti dell’organizzazione che possono configurare e personalizzare le autorizzazioni, ad Experience Platform in Adobe Admin Console.

**Adobe Admin Console**: Adobe Admin Console fornisce una posizione centrale per la gestione delle adesioni ai prodotti Adobe e l’accesso per la tua organizzazione. Tramite la console, gli amministratori possono concedere a gruppi di utenti autorizzazioni di accesso per varie funzionalità di Platform, ad esempio &quot;Gestisci set di dati&quot;, &quot;Visualizza set di dati&quot; o &quot;Gestisci profili&quot;.

**Adobe Experience Platform**: Adobe Experience Platform standardizza dati e contenuti a livello aziendale, fornendo profili di consumo in tempo reale, consentendo la scienza dei dati e accelerando la velocità dei contenuti per stimolare la personalizzazione dell’esperienza nel percorso di clienti.

**Servizio query Adobe Experience Platform**: Consente agli analisti di dati di eseguire query su eventi e profili da utilizzare in analisi e machine learning. Con Query Service, gli scienziati e gli analisti dei dati possono richiamare tutti i loro set di dati memorizzati in Experience Platform (inclusi i dati comportamentali, i POS (Point-of-sale), la gestione delle relazioni con i clienti (Customer Relationship Management, CRM) e molto altro) ed eseguire query su tali set di dati per rispondere a domande specifiche sui dati.

**Servizio di segmentazione di Adobe Experience Platform**: Abilita la creazione di segmenti e la generazione di tipi di pubblico dai dati del profilo cliente in tempo reale. Questi tipi di pubblico possono quindi essere esportati nei propri set di dati all’interno del Data Lake.

**Adobe Intelligent Services**: I servizi intelligenti come Attribution AI e Customer AI sono modelli di apprendimento automatico basati su intelligenza artificiale progettati appositamente e che richiedono Experienci Platform per funzionare e funzionare.

**Adobe I/O**: Adobe I/O fa parte di Experience Platform e fornisce l’accesso a tutto ciò che gli sviluppatori devono integrare, estendere e personalizzare Platform, incluse API, eventi, console per sviluppatori e utili strumenti.

**Adobe Sensei**: Adobe Sensei è il framework di intelligence che alimenta l&#39;Experience Platform. Fornisce inoltre un set di servizi di intelligenza artificiale che consentono ai brand di migliorare la loro capacità di fornire esperienze cliente personalizzate in tempo reale.

**bucket Amazon S3**: [!DNL Amazon S3] i bucket sono i contenitori fondamentali per i dati memorizzati in [!DNL Amazon] ecosistema. I bucket contengono oggetti, ogni oggetto viene memorizzato e recuperato utilizzando una chiave univoca assegnata agli sviluppatori.

**Connettore Amazon S3**: La [!DNL Amazon] Il connettore S3 consente ai clienti di Experience Platform di connettersi e accedere in modo sicuro ai propri [!DNL Amazon] Dati S3.

**Aggiungi strategia di salvataggio**: La strategia di salvataggio &quot;append&quot; è un’opzione utilizzata quando si specificano dati di terze parti da acquisire tramite una connessione e si aggiungono nuovi dati o righe alla fine del set di dati. Le righe precedentemente acquisite non vengono toccate e solo le righe create dall’ultima esecuzione pianificata vengono assimilate ad Experience Platform. Tutte le righe modificate nel sistema di origine rimangono invariate, ad Experience Platform.

**Array**: Gli array vengono utilizzati per gli elementi ordinati con lo stesso tipo di dati.

**Intelligenza artificiale**: L&#39;intelligenza artificiale è una teoria e sviluppo di sistemi informatici in grado di eseguire compiti che normalmente richiedono intelligenza umana, come la percezione visiva, il riconoscimento vocale, il processo decisionale e la traduzione tra le lingue.

**Attributi**: Gli attributi sono caratteristiche specificate che rappresentano un profilo.

**Unione attributi**: Quando si definisce un criterio di unione utilizzando l&#39;API del profilo cliente in tempo reale, il `attributeMerge` l&#39;oggetto indica il modo in cui il criterio di unione darà priorità agli attributi del profilo in caso di conflitti di dati. Equivale a selezionare un [!UICONTROL Metodo Merge] quando si definisce un criterio di unione nell’interfaccia utente di Platform.

**Attribution AI**: [!DNL Attribution AI] è un servizio intelligente basato su Adobe Sensei che offre funzionalità di attribuzione algoritmica multicanale per l’intero ciclo di vita del cliente.

**Pubblico**: Un pubblico è il set risultante di profili che soddisfano i criteri di una definizione di segmento.

**Dimensione del pubblico**: Una dimensione di pubblico è il numero totale di profili che soddisfano i criteri di una definizione di segmento e si qualificano per l’appartenenza al pubblico.

**Istantanea del pubblico**: Uno snapshot di pubblico acquisisce tutti i profili idonei per i criteri del segmento al momento della segmentazione.

## B

**Backfill**: Per le origini pianificate, l’opzione di backfill consente l’acquisizione di dati storici.

**Periodo di recupero**: Il periodo di backfill è un’opzione che consente di impostare il periodo di tempo necessario per l’acquisizione dei dati storici di terze parti tramite una connessione sorgente. Quando si seleziona un periodo di recupero di dati di tipo &quot;per sempre&quot;, viene acquisita ad Experience Platform l’intera cronologia dei dati di origine.

**Batch**: Un batch è un insieme di dati raccolti in un periodo di tempo ed elaborati insieme come una singola unità. I set di dati sono composti da più batch.

**ID batch**: Un ID batch è un identificatore generato dall&#39;Adobe per un batch di dati.

**Acquisizione batch**: L’acquisizione in batch consente di acquisire dati in Experience Platform come file batch. I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità.

**Segmentazione in batch**: La segmentazione in batch è un’alternativa a un processo continuo di selezione dei dati e sposta tutti i dati di profilo contemporaneamente attraverso le definizioni dei segmenti per produrre i tipi di pubblico corrispondenti. Una volta creato, questo segmento viene salvato e memorizzato in modo che possa essere esportato per l’uso.

**Crea**: Nel contesto dei tag, una build è un file o un set di file che contiene tutte le configurazioni e il codice necessari per eseguire la logica di business contenuta all&#39;interno di una libreria, che consente di distribuire tale libreria sul sito web o sull&#39;app mobile.

**Strumenti di Business Intelligence**: Gli strumenti di Business Intelligence (BI) sono principalmente integrati con [!DNL Experience Platform Query Service]. Gli strumenti BI sono tipi di software applicativi che raccolgono ed elaborano grandi quantità di dati non strutturati da sistemi interni ed esterni.

## C

**Limitazione**: In [!DNL Offer Decisioning], il limite massimo (o limite di frequenza) viene utilizzato nelle regole decisionali per definire quante volte viene presentata un’offerta. Esistono due tipi di tappi: quante volte un’offerta può essere proposta tra il pubblico di destinazione combinato (chiamato &quot;Global Cap&quot;) e quante volte un’offerta può essere proposta allo stesso utente finale (chiamato &quot;Profile Cap&quot;).

**Catalogo**: Nel contesto delle origini e delle destinazioni, un catalogo è una galleria con le connessioni disponibili alle applicazioni di Adobe e alle tecnologie di terze parti. Da non confondere con [!DNL Catalog Service].

**[!DNL Catalog Service]**: [!DNL Catalog Service] (talvolta denominati [!DNL Catalog]) è il sistema di registrazione per la posizione e la derivazione dei dati all’interno di Adobe Experience Platform. Mentre tutti i dati acquisiti in Experience Platform vengono memorizzati nel lago di dati come file e directory, [!DNL Catalog] contiene i metadati e la descrizione di tali file e directory a scopo di ricerca, monitoraggio e governance dei dati.

**Classe**: In Experience Data Model (XDM), una classe definisce il set di campi più piccolo utilizzato per creare uno schema e definisce il comportamento di base dell&#39;oggetto business rappresentato dallo schema.

**Client**: Un client è uno strumento o un&#39;applicazione esterna che si connette a [!DNL Query Service] tramite [!DNL PostgreSQL] protocollo o API HTTP.

**Raccolta**: In [!DNL Offer Decisioning], le raccolte sono sottoinsiemi di offerte in base a condizioni predefinite definite da un addetto al marketing, ad esempio la categoria dell’offerta.

**Combinare con un’azione di marketing PII**: Un’azione di marketing che combina eventuali informazioni personali identificabili (PII) con dati anonimi. I contratti per i dati provenienti da reti di annunci, server di annunci e fornitori di dati di terze parti spesso includono specifici divieti contrattuali sull&#39;uso di tali dati con dati direttamente identificabili.

**Interfaccia della riga di comando**: Un&#39;interfaccia a riga di comando è uno strumento basato su testo che può essere utilizzato per connettersi a [!DNL Query Service] per l’esecuzione di query non elaborate.

**Composizione**: Una composizione è un raggruppamento di componenti che formano insieme per formare lo schema.

**Condizione**: Nel contesto dei tag, una condizione è un componente della regola che valuta un&#39;istruzione logica che deve restituire `true` o `false`. Tutte le condizioni devono valutare `true` e tutte le condizioni di eccezione devono valutare `false` prima dell&#39;esecuzione di qualsiasi azione sulla regola.

**Console**: In [!DNL Query Service], la console fornisce informazioni sullo stato e sul funzionamento di una query. Nella console viene visualizzato lo stato della connessione a [!DNL Query Service], le operazioni di query in esecuzione ed eventuali messaggi di errore risultanti da tali query.

**Etichette del contratto (&quot;C&quot;)**: Le etichette per l’utilizzo dei dati del contratto (&quot;C&quot;) vengono utilizzate per classificare i dati che hanno obblighi contrattuali o sono correlati alle politiche di governance dei dati di un cliente.

**Etichetta del contratto C1**: A `C1` l’etichetta di utilizzo dei dati del contratto specifica che i dati possono essere esportati da Adobe Experience Cloud solo in un modulo aggregato senza includere identificatori di dispositivo o singoli. Ad esempio, i dati provenienti dai social network.

**Etichetta del contratto C2**: A `C2` l’etichetta di utilizzo dei dati del contratto specifica i dati che non possono essere esportati in una terza parte. Alcuni fornitori di dati hanno termini nei loro contratti che vietano l&#39;esportazione di dati da dove sono stati originariamente raccolti. Ad esempio, i contratti di social network spesso limitano il trasferimento dei dati che ricevi da loro. C2 è più restrittivo di C1, che richiede solo l&#39;aggregazione e dati anonimi.

**Etichetta del contratto C3**: A `C3` l’etichetta di utilizzo dei dati del contratto specifica i dati che non possono essere combinati o altrimenti utilizzati con informazioni direttamente identificabili. Alcuni fornitori di dati hanno termini nei loro contratti che vietano la combinazione o l&#39;uso di tali dati con informazioni direttamente identificabili. Ad esempio, i contratti per i dati provenienti da reti di annunci, server di annunci e fornitori di dati di terze parti spesso includono specifici divieti contrattuali sull&#39;uso di dati direttamente identificabili.

**Etichetta del contratto C4**: A `C4` l’etichetta di utilizzo dei dati del contratto specifica che i dati non possono essere utilizzati per il targeting di annunci o contenuti, sia sul sito che tra siti diversi. C4 è l&#39;etichetta più restrittiva in quanto comprende le etichette C5, C6 e C7.

**Etichetta del contratto C5**: A `C5` l’etichetta di utilizzo dei dati del contratto specifica che i dati non possono essere utilizzati per il targeting intersito di contenuti o annunci basati su interessi. Il targeting basato sugli interessi, o personalizzazione, si verifica se sono soddisfatte le tre condizioni seguenti: I dati raccolti sul sito sono utilizzati per trarre conclusioni sull&#39;interesse dell&#39;utente; è utilizzato in un altro contesto, ad esempio su un altro sito o app; e viene utilizzato per selezionare quali contenuti o annunci vengono serviti in base a tali inferenze.

**Etichetta del contratto C6**: A `C6` l’etichetta di utilizzo dei dati del contratto specifica che i dati non possono essere utilizzati per il targeting degli annunci sul sito. Il targeting degli annunci in sito include la selezione e la consegna di annunci sui siti web o sulle app della tua organizzazione o per misurare la consegna e l&#39;efficacia di tali annunci. Ciò include l&#39;utilizzo di dati raccolti in precedenza sul sito relativi all&#39;interesse degli utenti per selezionare gli annunci, elaborare i dati su ciò che gli annunci sono stati mostrati, quando e dove sono stati mostrati, e se gli utenti hanno preso qualsiasi azione correlata all&#39;annuncio, come la selezione di un annuncio o l&#39;effettuazione di un acquisto.

**Etichetta del contratto C7**: A `C7` l’etichetta di utilizzo dei dati del contratto specifica che i dati non possono essere utilizzati per il targeting in sito del contenuto. Il targeting dei contenuti in sito include la selezione e la distribuzione di contenuti sui siti web o sulle app della tua organizzazione o per misurare la consegna e l’efficacia di tali contenuti. Ciò include informazioni raccolte in precedenza sull’interesse degli utenti per la selezione del contenuto, l’elaborazione dei dati su quale contenuto è stato visualizzato, la frequenza o la durata della visualizzazione, quando e dove è stato visualizzato, e se gli utenti hanno eseguito azioni correlate al contenuto, ad esempio la selezione del contenuto.

**Etichetta del contratto C8**: A `C8` l’etichetta di utilizzo dei dati del contratto specifica che i dati non possono essere utilizzati per la misurazione dei siti web o delle app dell’organizzazione. Questo non include il targeting basato sugli interessi, ovvero la raccolta di informazioni sull’utilizzo di questo servizio per personalizzare successivamente contenuti e/o pubblicità in altri contesti.

**Etichetta del contratto C9**: A `C9` l’etichetta di utilizzo dei dati del contratto specifica che i dati non possono essere utilizzati nei flussi di lavoro di scienza dei dati. Alcuni contratti includono divieti espliciti sui dati utilizzati per la scienza dei dati. A volte tali termini sono formulati in termini che vietano l’uso di dati per l’intelligenza artificiale (AI), l’apprendimento automatico (ML) o la modellazione.

**Etichetta del contratto C10**: A `C10` l’etichetta di utilizzo dei dati del contratto specifica che i dati non possono essere utilizzati per l’attivazione dell’identità unita. Alcuni criteri di utilizzo dei dati limitano l’utilizzo di dati di identità uniti per la personalizzazione. La `C10` l’etichetta viene applicata automaticamente ai segmenti se i relativi criteri di unione utilizzano l’opzione &quot;grafico privato&quot;.

**Colonna Data creazione**: Quando si seleziona una colonna Data creazione , è possibile specificare dati di terze parti tramite una connessione di origine. Quando la strategia di salvataggio dell’aggiunta è selezionata e lo schema del set di dati contiene più campi data, è necessario scegliere dallo schema disponibile per specificare una colonna chiave Data creazione. L’opzione Data creazione non è disponibile quando si seleziona la strategia di salvataggio per la sovrascrittura.

**Crea tabella come selezione**: Crea tabella come selezione (CTAS) è un comando SQL che, se eseguito come parte di una query SQL completa e valida, istruirà [!DNL Query Service] per mantenere i risultati della query in un set di dati. Puoi creare un nuovo set di risultati, sovrascrivere i risultati precedenti o aggiungere i risultati precedenti.

**Dati intersito**: I dati intersito sono la combinazione di dati provenienti da diversi siti, inclusa una combinazione di dati sul sito e dati fuori sito o una combinazione di dati provenienti da più fonti esterne al sito.

**Azione di marketing di targeting tra siti**: Un’azione di marketing che utilizza i dati per il targeting degli annunci tra siti. La combinazione di dati provenienti da più siti, compresa una combinazione di dati in loco e dati fuori sito o una combinazione di dati provenienti da più fonti esterne al sito, è definita dati intersito. I dati intersito vengono in genere raccolti ed elaborati per fare deduzioni sugli interessi dei clienti.

**Spazio dei nomi di identità personalizzato**: I namespace di identità personalizzati possono essere creati dalla tua organizzazione per rappresentare le identità per una specifica organizzazione o business case.

**Etichette personalizzate**: Le etichette di utilizzo dati personalizzate consentono di creare e applicare etichette specifiche ai campi di dati che soddisfano esigenze aziendali specifiche.

**Customer AI**: Customer AI è un servizio intelligente basato su Adobe Sensei che arricchisce i profili dei clienti con proprietà basate sull’intelligenza artificiale e potenzia la segmentazione dei clienti e le attività di targeting.

## D

**Giornaliero**: Nel contesto delle esportazioni pianificate di file, pianifica le esportazioni di file completi o incrementali una volta al giorno, ogni giorno, dalla data di inizio alla data di fine all’ora specificata dall’utente.

**Dizionario dati**: Nel contesto dei tag, un dizionario dati (noto anche come mappa dati) è un set di elementi dati definiti all&#39;interno di una proprietà.

**Elemento dati**: Nel contesto dei tag, un elemento dati è un puntatore utilizzato all&#39;interno di regole ed estensioni per puntare a uno specifico elemento di dati presente sul dispositivo client.

**Acquisizione dati**: L’inserimento dei dati è il processo che consente di aggiungere dati da un’origine all’Experience Platform. I dati possono essere acquisiti in Platform in diversi modi, compresi streaming, batch o aggiunti tramite connettori sorgente.

**Livello dati**: Nel contesto dei tag, un livello dati è una struttura dati esistente sul dispositivo client che contiene metadati sul contesto in cui viene visualizzata una pagina o una schermata.

**Governance dei dati**: La governance dei dati include le strategie e le tecnologie utilizzate per garantire che i dati siano conformi alle normative e alle politiche organizzative in materia di utilizzo dei dati.

**Partner per l’integrazione dei dati**: I partner per l&#39;integrazione dei dati semplificano e automatizzano il caricamento e la trasformazione di grandi volumi di dati da oltre 200 fonti all&#39;Experience Platform senza scrivere codice.

**Etichette set di dati**: È possibile aggiungere etichette di utilizzo dei dati ai set di dati. Tutti i campi all’interno di tale set di dati erediteranno le etichette del set di dati.

**Data Science Workspace**: [!DNL Data Science Workspace] in Experience Platform consente ai clienti di creare modelli di apprendimento automatico utilizzando i dati nelle applicazioni Platform e Adobe per creare segmenti intelligenti, generare informazioni e fornire previsioni, consentendo di migliorare notevolmente le esperienze digitali degli utenti finali.

**Origine dati**: Un’origine dati è un’origine dei dati designata dall’utente. Esempi di un’origine dati sono un’app mobile, eventi di profilo e/o di esperienza, eventi di profilo di un sito web o un sistema di gestione delle relazioni con i clienti.

**Data steward**: Un amministratore dei dati è la persona responsabile della gestione, della sorveglianza e dell&#39;applicazione delle risorse di dati di un&#39;organizzazione. Un amministratore dei dati garantisce inoltre che le politiche di governance dei dati siano salvaguardate e mantenute conformi alle normative e alle politiche organizzative governative.

**Flusso di dati**: Un flusso di dati è un insieme o una raccolta di messaggi che condividono lo stesso schema e vengono inviati dalla stessa origine.

**Tipo di dati**: Un tipo di dati è una risorsa XDM riutilizzabile che definisce un campo di tipo oggetto contenente più proprietà in una rappresentazione gerarchica.

**Etichette di utilizzo dati**: Le etichette per l’utilizzo dei dati ti consentono di classificare i dati che riflettono considerazioni relative alla privacy e condizioni contrattuali conformi alle normative e ai criteri aziendali. Le etichette di utilizzo dei dati aggiunte a un set di dati vengono ereditate o applicate a tutti i campi all’interno di tale set di dati. Le etichette di utilizzo dei dati possono essere applicate direttamente ai campi.

**Flusso di dati**: Un flusso di dati è una pipeline virtuale di dati che fluisce in Platform da un’origine a una destinazione.

**Esecuzione del flusso di dati**: Un&#39;esecuzione del flusso di dati è un flusso di dati che arriva in Experience Platform in base a una pianificazione specificata dall&#39;utente.

**Set di dati**: Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e campi (righe).

**ID set di dati**: Identificatore generato da un Adobe per un set di dati acquisito.

**Uscita set di dati**: L&#39;output del set di dati fornisce un meccanismo per determinare l&#39;opzione &quot;Crea tabella come selezione&quot; da utilizzare per una particolare [!DNL Query Service] esegui.

**Chiave di deduplicazione**: Chiave primaria definita dall&#39;utente che determina l&#39;identità in base alla quale gli utenti desiderano che i loro profili vengano deduplicati. &#x200B;

**Colonna delta**: Una colonna delta consente di selezionare un campo dati di origine per rappresentare una marca temporale per l’acquisizione incrementale.

**strategia di salvataggio delta**: La strategia di salvataggio delta è un’opzione per l’acquisizione di dati di terze parti tramite una connessione sorgente. L’opzione consente all’utente di specificare come Experience Platform le righe nuove o modificate dei dati di origine. Le nuove righe vengono aggiunte alla fine del set di dati e le righe modificate vengono aggiornate nel set di dati all’Experience Platform.

**Descrittore**: In Experience Data Model (XDM), un descrittore è un set aggiuntivo di metadati relativi allo schema che descrive un comportamento specifico per un campo. I descrittori possono essere utilizzati dall’Experience Platform per comprendere il comportamento dello schema previsto, ad esempio la relazione tra due schemi.

**Destinazione**: Una destinazione è un termine generale per qualsiasi endpoint, ad Adobe applicazione, piattaforma pubblicitaria, servizio di archiviazione cloud o servizio di marketing, in cui un pubblico viene attivato e consegnato.

**Categoria di destinazione**: Una categoria di destinazione è un raggruppamento di destinazioni con caratteristiche simili.

**Catalogo di destinazione**: Un catalogo di destinazione è un elenco di destinazioni disponibili, ad Experience Platform.

**Regole di chiamata diretta**: Nel contesto dei tag, una regola di chiamata diretta è una regola che viene eseguita quando viene chiamata direttamente dalla pagina, bypassando i sistemi di rilevamento degli eventi e di ricerca.

**Nome visualizzato**: In Experience Data Model (XDM), un nome visualizzato è un nome descrittivo per un campo visualizzato nell’interfaccia utente.

## E

**Offerta idonea**: Un’offerta idonea può essere offerta in modo coerente a un profilo, in quanto soddisfa i vincoli definiti a monte.

**Regole di idoneità**: In [!DNL Offer Decisioning], le regole di idoneità vengono applicate a un profilo relativo a vincoli di calendario, pianificazione e limitazione di massimale.

**Azione di marketing di targeting e-mail**: Un’azione di marketing che utilizza i dati nelle campagne di targeting e-mail.

**Codice di incorporamento**: Nel contesto dei tag , il codice di incorporamento è un tag script posizionato all’interno di HTML in un sito o in un ambiente. Il codice di incorporamento indica al browser dove recuperare la build.

**Enumerazione**: Un’enumerazione (enum) è un campo XDM vincolato a un set di valori predefiniti.

**Ambiente**: Nel contesto dei tag, un ambiente è un insieme di istruzioni di distribuzione che specifica la consegna host e il formato di file di una build. Una libreria deve essere associata a un ambiente prima di poter essere generata.

**Diagnostica degli errori**: La diagnostica degli errori consente di generare messaggi di errore dettagliati per i batch acquisiti. La soglia di errore consente di configurare la percentuale di errori accettabili prima che un batch non riesca.

**Evento**: Nel contesto dei tag, un evento è un tipo specifico di componente regola, che è un trigger che si verifica su un dispositivo client per avviare l&#39;esecuzione di una regola.

**Entità evento**: Nel contesto della modellazione dei dati, le entità evento rappresentano concetti relativi alle azioni che un cliente può intraprendere, agli eventi di sistema o a qualsiasi altro concetto in cui desideri tenere traccia dei cambiamenti nel tempo. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati su [!DNL XDM ExperienceEvent] classe.

**Eventi**: Gli eventi sono i dati di comportamento associati a un profilo.

**Experience Data Model (XDM)** [!DNL Experience Data Model] (XDM) è un framework open-source che utilizza schemi standard per unificare i dati da utilizzare con le applicazioni Experience Platform e Adobe Experience Cloud. XDM standardizza il modo in cui i dati sono strutturati e accelera e semplifica il processo di acquisizione di informazioni da massicce quantità di dati.

**Esperimento**: Un esperimento è il processo di creazione di un modello addestrato formando l&#39;istanza con una porzione campione di dati di produzione live. Questo è diverso da un modello addestrato che viene testato rispetto a un set di dati di test holdout. Questo è anche diverso dal concetto di esperimento in alcuni framework di apprendimento automatico in cui significa in realtà un progetto di modellazione campione.

**Evento esperienza**: Un evento esperienza rappresenta un’istantanea del sistema quando si verifica un’interazione o un evento correlato a un’esperienza del cliente. Gli eventi di esperienza sono documenti di fatto immutabili di ciò che è accaduto e rappresentano ciò che è accaduto senza aggregazione o interpretazione. In Experience Data Model (XDM), questo concetto viene acquisito da [!DNL XDM ExperienceEvent] classe.

**Esporta file completo**: Un file di esportazione contenente uno snapshot completo di tutte le qualifiche di profilo per il segmento selezionato.

**Esportare file incrementali**: Una serie di file esportati in cui il primo file è uno snapshot completo di tutte le qualifiche di profilo per il segmento selezionato e i file successivi sono qualifiche di profilo incrementali rispetto all’esportazione precedente.

**Estensione**: Nel contesto dei tag, un&#39;estensione è un pacchetto di funzionalità aggiunte a una proprietà tag. Un’estensione si concentra solitamente su una particolare soluzione di marketing o analisi e fornisce gli strumenti necessari per distribuire tale tecnologia in un ambiente client.

**Pacchetto di estensione**: Nel contesto dei tag, un pacchetto di estensione è un file ZIP creato e caricato da uno sviluppatore di estensioni che fornisce tutto il necessario affinché gli utenti dei tag installino l&#39;estensione all&#39;interno della loro proprietà. Un pacchetto di estensione contiene un manifesto che specifica le informazioni sull&#39;estensione, HTML/JavaScript necessari agli utenti finali per configurare il comportamento dell&#39;estensione tag e il JavaScript eseguibile consegnato all&#39;ambiente client (se necessario).

## F

**Offerte di fallback**: Un’offerta di fallback è l’offerta predefinita visualizzata quando un utente finale non è idoneo per nessuna delle offerte della raccolta utilizzata.

**Mappatura delle funzioni**: La mappatura delle funzioni si riferisce al processo di mappatura delle funzioni dai dati alle funzioni di input e target richieste da un modello di apprendimento automatico.

**Campo**: Un campo è l’elemento di livello più basso di un set di dati, come definito dallo schema XDM del set di dati. Ogni campo ha un nome a scopo di riferimento e un tipo per indicare il tipo di dati che contiene. I tipi di campo possono includere (ma non sono limitati a) numeri interi, numeri, stringhe, booleani e oggetti.

**Gruppo di campi**: Vedere &quot;Gruppo di campi schema&quot;.

**Etichette per i campi**: Le etichette dei campi sono etichette di governance dei dati ereditate da un set di dati o applicate direttamente a un campo.

**Nome campo**: Un nome di campo viene utilizzato per fare riferimento al valore di un campo nelle query e nei servizi a valle.

**Frequenza**: In [!DNL Query Service], la frequenza determina la frequenza di esecuzione di una query pianificata ricorrente.

## G

**Geofence**: Un recinto geografico è un limite geografico virtuale, definito dalla tecnologia GPS o RFID, che consente al software di attivare una risposta quando un dispositivo mobile entra o esce da una determinata area.

**RGPD (Regolamento generale sulla protezione dei dati)**: Il Regolamento generale sulla protezione dei dati (RGPD) è un quadro giuridico che stabilisce le linee guida per la raccolta e il trattamento di informazioni personali di persone all’interno dell’Unione europea (UE). Il RGPD stabilisce i principi per la gestione dei dati e i diritti dei singoli e copre tutte le aziende che si occupano dei dati dei cittadini dell&#39;UE.

**Guardrail**: Le guardrail sono soglie che forniscono indicazioni sull’utilizzo dei dati e del sistema, sull’ottimizzazione delle prestazioni e sull’eliminazione di errori o risultati imprevisti in Adobe Experience Platform. I guardrail possono fare riferimento all&#39;uso o al consumo di dati e al trattamento in relazione alle autorizzazioni per le licenze.

## H

**Host**: Nel contesto dei tag, un host specifica la posizione, il dominio e le credenziali utente necessarie affinché il sistema possa distribuire una build.

**Orario**: Nel contesto delle esportazioni pianificate di file, pianifica le esportazioni incrementali di file ogni 3, 6, 8 o 12 ore.

## I

**Identità**: Un’identità è un identificatore che rappresenta in modo univoco un singolo cliente, ad esempio un ID cookie, un ID dispositivo o un ID e-mail.

**Campi di identità**: I campi di identità sono campi XDM utilizzati per unire informazioni sui singoli clienti provenienti da più origini dati. Affinché lo schema sia abilitato per l’utilizzo in Profilo cliente in tempo reale, è necessario definire una singola identità principale.

**Etichette di identità (&quot;I&quot;)**: Le etichette di utilizzo dei dati di identità (&quot;I&quot;) vengono utilizzate per classificare i dati che possono identificare o contattare una persona specifica.

**Grafico di identità**: Un grafico delle identità è una mappa delle relazioni tra le identità collegate e unite esistenti per un singolo cliente. Ogni grafico delle identità viene aggiornato in tempo quasi reale con l’attività del cliente. La struttura comune delle relazioni di identità nei dati è rappresentata da [!UICONTROL Grafico privato], che funge da modello strutturale per ogni singolo grafico di identità.

**Spazio dei nomi identità**: Uno spazio dei nomi di identità definisce il contesto di un identificatore, ad esempio un indirizzo e-mail o un ID CRM.

**Servizio identità**: [!DNL Experience Platform Identity Service] consente la creazione e la gestione di tipi di identità, consentendo di collegare le identità dei clienti tra dispositivi e canali. La capacità del servizio di collegare le identità insieme consente al Profilo del cliente in tempo reale di fornire una rappresentazione completa di ogni singolo cliente.

**Unione identità**: L’unione delle identità è il processo di identificazione dei frammenti di dati e di unione dei frammenti per formare un record di profilo completo.

**Simbolo di identità**: Un simbolo di identità è un&#39;abbreviazione di uno spazio dei nomi di identità che può essere utilizzato come riferimento nelle API.

**Valore identità**: Un valore di identità, combinato con uno spazio dei nomi di identità, è un identificatore che rappresenta un singolo utente, un&#39;organizzazione o una risorsa univoca. Quando i dati dei record corrispondono a diversi frammenti di profilo, lo spazio dei nomi e il valore dell’identità devono corrispondere.

**Etichetta di utilizzo dati I1**: La `I1` l’etichetta di utilizzo dei dati viene utilizzata per classificare i dati che possono identificare o contattare direttamente una persona specifica anziché un dispositivo.

**Etichetta di utilizzo dati I2**: La `I2` l’etichetta di utilizzo dei dati viene utilizzata per classificare i dati che possono essere utilizzati in combinazione con qualsiasi altro dato per identificare o contattare indirettamente una persona specifica.

**Organizzazione IMS**: Un’organizzazione IMS (a volte definita organizzazione IMS) è il nome utilizzato per identificare un’azienda o un gruppo specifico all’interno di un’azienda nei diversi prodotti Adobe. Gli amministratori possono configurare e gestire l’accesso e le autorizzazioni delle funzionalità per gli utenti di un’organizzazione.

**Acquisizione**: Vedi inserimento dei dati.

**Pianificazione dell’acquisizione**: Una pianificazione dell’acquisizione fornisce opzioni basate sul tempo durante l’acquisizione da un’origine all’Experience Platform.

**Funzione di ingresso**: Una funzione di input è specificata nella mappatura delle funzioni e viene utilizzata da un modello di apprendimento automatico per fare previsioni.

**[!DNL Intelligent Services]**: [!DNL Intelligent Services] quali [!DNL Attribution AI] e [!DNL Customer AI] sono modelli di apprendimento automatico basati su intelligenza artificiale che richiedono l’esecuzione e il funzionamento di Experienci Platform (o applicazioni integrate in Platform come Adobe Real-time Customer Data Platform).

**Targeting o personalizzazione basati su interessi**: Il targeting basato sugli interessi, noto anche come personalizzazione, si verifica se sono soddisfatte le tre condizioni seguenti:

1. I dati raccolti sul sito vengono utilizzati per fare deduzioni sull&#39;interesse dell&#39;utente.
1. I dati vengono utilizzati in un altro contesto, ad esempio su un altro sito o app (fuori sito).
1. I dati vengono utilizzati per selezionare quali contenuti o annunci vengono serviti in base a tali inferenze.

## J

**[!DNL JupyterLab]**: Interfaccia open-source basata su Web per Project [!DNL Jupyter] integrata nell’interfaccia utente di Platform.

**[!DNL Jupyter Notebook]**: Integrato con JupyterLab, Jupyter Notebooks consente di eseguire la pulizia e la trasformazione dei dati, la simulazione numerica, la modellazione statistica, la visualizzazione dei dati, l&#39;apprendimento automatico e altro ancora sui dati Experienci Platform in diverse lingue come Python, Scala e PySpark.

## K

## L

**Libreria**: Nel contesto dei tag , una libreria è un set di regole di business che contiene istruzioni sul comportamento della libreria di tag sul dispositivo client.

**Entità di ricerca**: Nel contesto della modellazione dei dati, le entità di ricerca rappresentano concetti che possono riferirsi a una singola persona, ma che non possono essere utilizzati direttamente per identificare l’individuo. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati su classi XDM (Experience Data Model) personalizzate.

## M

**Apprendimento automatico (ML)**: L&#39;apprendimento automatico è il campo di studio che consente ai computer di imparare senza essere esplicitamente programmato.

**Modello di apprendimento automatico**: Un modello di apprendimento automatico è un&#39;istanza di una ricetta di apprendimento automatico formata utilizzando dati storici e configurazioni per risolvere un caso d&#39;uso aziendale. In Adobe Experience Platform Data Science Workspace, i modelli di apprendimento automatico sono chiamati ricette.

**Attributo obbligatorio**: Casella di controllo abilitata dall’utente che assicura che tutti i record di profilo contengano l’attributo selezionato. Ad esempio: tutti i profili esportati contengono un indirizzo e-mail.

**Mappatura**: La mappatura dei dati è il processo di mappatura dei campi dei dati di origine su campi di destinazione correlati in una destinazione.

**Azione di marketing**: Nel framework di governance dei dati, un’azione di marketing (nota anche come caso d’uso del marketing) è un’azione eseguita da un consumatore di dati di Experience Platform, per la quale è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati.

**Metodo Merge**: Quando si definisce un criterio di unione utilizzando l’interfaccia utente di Platform, il metodo di unione specifica la priorità dei frammenti di dati in caso di conflitto. Quando si utilizza l’API Profilo cliente in tempo reale per definire un criterio di unione, il metodo di unione viene determinato utilizzando la variabile `attributeMerge` oggetto.

**Criteri di unione**: I criteri di unione sono regole utilizzate da Experience Platform per determinare in che modo i frammenti di dati del cliente provenienti da più origini verranno combinati per creare un singolo profilo. Quando si verifica un conflitto di dati, il criterio di unione determina quali dati devono avere la priorità per l’inclusione nel profilo.

**Mixina**: Vedere &quot;Gruppo di campi schema&quot;.

**Modulo**: Nel contesto dei tag, un modulo è un frammento di JavaScript eseguibile fornito da un&#39;estensione, che esegue azioni in un ambiente client senza dover creare una regola.

## N

**Sandbox non di produzione**: Le sandbox non di produzione sono sandbox solitamente utilizzate per esperimenti di sviluppo, test o test. A differenza delle sandbox di produzione, le sandbox non di produzione possono essere reimpostate ed eliminate.

**[!DNL Notebooks]**: [!DNL Notebooks] sono creati utilizzando [!DNL Jupyter Notebook] e può essere eseguito per eseguire l’analisi dei dati.

## O

**Offerta**: Un’offerta è un messaggio di marketing contenente una proposta commerciale o di vendita a un (potenziale) cliente. Le offerte hanno spesso regole specifiche che determinano chi è idoneo a visualizzarle o riceverle.

**[!DNL Offer Decisioning]**: [!DNL Offer Decisioning] consente agli addetti al marketing di gestire regole e modelli addestrati di proposte di offerta quando interagiscono con gli utenti finali in base ai dati raccolti tra canali e applicazioni.

**Libreria offerte**: La libreria delle offerte è una libreria centrale utilizzata per gestire offerte personalizzate e di fallback, regole decisionali e attività.

**Azione di marketing per la personalizzazione sul sito**: Un’azione di marketing che utilizza i dati per la personalizzazione dei contenuti sul sito. Per personalizzazione in sito si intende qualsiasi dato utilizzato per fare deduzioni sugli interessi degli utenti e utilizzato per selezionare quali contenuti o annunci vengono serviti in base a tali deduzioni.

**Azione di marketing di targeting sul sito**: Un’azione di marketing che utilizza i dati per gli annunci sul sito, inclusa la selezione e la consegna di annunci pubblicitari sui siti web o sulle app della tua organizzazione, o per misurare la consegna e l’efficacia di tali annunci.

**Una volta**: Nel contesto delle esportazioni di file pianificati, pianifica un’esportazione di file completi una tantum, su richiesta.

**Sovrascrivi strategia di salvataggio**: La strategia di salvataggio &quot;Sovrascrivi&quot; è un’opzione per l’acquisizione di dati di terze parti tramite una connessione, dove puoi specificare se i dati acquisiti verranno sovrascritti in base a una pianificazione specifica.

## P

**Acquisizione parziale**: L’acquisizione parziale consente l’inserimento di record validi di dati batch entro una determinata soglia di errore. È possibile scaricare o accedere alla diagnostica degli errori per i record non riusciti in [!UICONTROL Monitoraggio] o [!UICONTROL Origini] panoramica dell’esecuzione del flusso di dati.

**File di parquet**: Un file Parquet è un formato di file di archiviazione colonna con strutture di dati nidificate complesse. I file di parquet sono necessari per aggiungere dati per compilare un set di dati di schema.

**Offerte personalizzate**: Un’offerta personalizzata è un messaggio di marketing personalizzabile basato su regole e vincoli di idoneità.

**Posizionamenti**: il posizionamento corrisponde a posizione e contesto in cui un’offerta viene mostrata a un utente finale.

**Area di lavoro dei criteri**: Area di lavoro nell’interfaccia utente di Platform che consente agli amministratori di dati di visualizzare e gestire le etichette e i criteri di utilizzo dei dati per la tua organizzazione.

**Criterio**: Un criterio di utilizzo dei dati è una regola che specifica le azioni di marketing limitate in base all’applicazione di etichette di utilizzo applicate ai dati di Platform.

**Applicazione delle politiche**: Consente di applicare i criteri di utilizzo dei dati con le azioni di marketing applicate per impedire operazioni di dati che costituiscono violazioni dei criteri all’interno di un’organizzazione.

**Chiave principale**: Una chiave primaria è una designazione in uno schema per identificare in modo univoco tutti i record.

**Priorità**: In [!DNL Offer Decisioning], la priorità viene utilizzata per classificare le offerte che soddisfano tutti i vincoli, ad esempio idoneità, calendario e limiti.

**Grafico a identità privata**: Il grafico dell’identità privata (a volte denominato grafico privato) è una mappa privata delle relazioni tra identità unite e collegate, creata in base ai dati di prime parti ed è visibile solo dalla tua organizzazione. Esiste un solo grafico privato per ogni organizzazione e funge da modello strutturale per i grafici di identità individuali generati per ogni cliente che interagisce con il tuo marchio.

**Profilo di prodotto**: I profili di prodotto consentono agli amministratori di concedere all’utente l’accesso a tutti i servizi associati all’Experience Platform o a un sottoinsieme di essi.

**Sandbox di produzione**: Una sandbox di produzione è una sandbox destinata all’utilizzo nell’ambiente di produzione. A differenza delle sandbox non di produzione, le sandbox di produzione non possono essere reimpostate o eliminate.

**Profilo**: Da non confondere con Profilo cliente in tempo reale come servizio, un profilo è una rappresentazione completa di un singolo cliente, costruito da record uniti e dati di serie temporali provenienti da più sorgenti.

**Accesso al profilo**: La `/entities` L’endpoint nell’API del profilo cliente in tempo reale consente di accedere ai dati di record e agli eventi relativi a serie temporali nell’archivio dati del profilo. Vedi anche: Entità del profilo

**Dati profilo**: I dati del profilo si riferiscono a qualsiasi dato presente nell’archivio dati del profilo.

**Archiviazione dati profilo**: L’archivio dati Profilo (talvolta denominato Archivio profili) è un sistema di archiviazione dati separato dal lago dati, utilizzato da Profilo cliente in tempo reale per creare e memorizzare i profili.

**Entità del profilo**: Le entità profilo rappresentano gli attributi relativi a una singola persona, in genere un cliente. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati su [!DNL XDM Individual Profile] classe. Vedi anche: Accesso al profilo

**Esportazione del profilo**: [!DNL Profile] l’esportazione è uno dei due tipi di destinazioni nell’Experience Platform. [!DNL Profile] export genera un file contenente profili e attributi e utilizza dati PII non elaborati con le e-mail per integrarsi con le piattaforme di marketing e automazione delle e-mail.

**Frammento di profilo**: Un frammento di profilo è l’informazione di profilo per una sola identità inclusa nell’elenco di identità esistenti per un particolare cliente.

**ID profilo**: Un ID profilo è un identificatore generato automaticamente associato a un tipo di identità e rappresenta un profilo.

**Proprietà**: Nel contesto dei tag, una proprietà è un contenitore per tutto ciò che è necessario per distribuire un set di tag.

## Q

**Query**: Le query sono richieste di dati da tabelle di database.

**Editor query**: Query Editor è uno strumento per scrivere, convalidare e inviare istruzioni SQL in [!DNL Query Service].

## R

**Real-time Customer Data Platform**: Adobe Real-time Customer Data Platform (Real-Time CDP) riunisce dati noti e sconosciuti dei clienti per creare profili cliente affidabili con integrazione semplificata, segmentazione intelligente e attivazione in tempo reale nel percorso cliente digitale.

**Profilo cliente in tempo reale**: Il Profilo cliente in tempo reale (talvolta denominato Profilo) fornisce una visualizzazione olistica di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i dati dei clienti in profili individuali offrendo account con marca temporale e fruibili per ogni interazione con il cliente.

**Ricetta**: Una ricetta è un termine Adobe per una specifica di modello ed è un contenitore principale che rappresenta specifici processi di apprendimento automatico, algoritmi AI, logica di elaborazione e parametri di configurazione necessari per creare ed eseguire un modello qualificato e quindi contribuire a risolvere specifici problemi di business.

**Record**: Un record è costituito da dati che persistono come righe in un set di dati.

**Registra dati**: Fornisce informazioni sugli attributi di un oggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo.

**Ricorrenza**: In [!DNL Query Service], una ricorrenza definisce se è prevista l’esecuzione di una query una sola volta o su base ricorrente.

**Rappresentazione**: In [!DNL Offer Decisioning], una rappresentazione è un’informazione utilizzata da un canale per visualizzare un’offerta, ad esempio posizione o lingua.

**Risorsa**: Nel contesto dei tag, una risorsa è un termine generico che fa riferimento alle opzioni che l’utente di tag può configurare all’interno dell’ambiente client, incluse estensioni, elementi dati e regole.

**Controllo degli accessi basato sul ruolo**: Il controllo degli accessi basato su ruoli consente agli amministratori di assegnare accesso e autorizzazioni agli utenti di Experience Platform. Le autorizzazioni includono la possibilità di visualizzare e/o utilizzare funzionalità di Experience Platform, ad esempio la creazione di sandbox, la definizione di schemi e la gestione di set di dati.

**Regola**: Nel contesto dei tag, una regola è una raccolta di componenti che definiscono un set specifico di eventi, condizioni e azioni che devono essere raggruppate logicamente.

**Componente regola**: Nel contesto dei tag, i componenti regola sono gli eventi, le condizioni e le azioni che compongono una regola.

**Runtime**: Runtime specifica un ambiente di runtime per una ricetta di apprendimento automatico. [!DNL Python]R, [!DNL Spark]I tempi di esecuzione di , PySpark e Tensorflow consentono di inserire un URL a un’immagine Docker per una sorgente di ricette.

## S

**Dati di esempio**: I dati di esempio sono un’anteprima di un file di dati, in genere le prime 100 righe, che fornisce a un esperto di dati o a un tecnico un’idea dello schema o dei dati presenti nel file di dati.

**Sandbox**: Una sandbox è un costrutto virtuale che divide una singola istanza di Platform in un ambiente virtuale separato, al fine di contribuire allo sviluppo e all’evoluzione di applicazioni di esperienza digitale.

**Ripristino della sandbox**: Una reimpostazione della sandbox elimina tutti i dati, inclusi dati, profili e segmenti, all’interno di una sandbox. I reinsiemi sandbox possono influenzare i dati collegati a destinazioni interne o esterne.

**Switcher sandbox**: Il controllo del commutatore sandbox in Experience Platform consente agli utenti di navigare tra le sandbox a cui hanno accesso. Il passaggio a una sandbox cambierà tutto il contenuto e potrebbe modificare l’accesso alle funzioni in base alle autorizzazioni.

**Pianificazione**: Una pianificazione è una specifica definita dall’utente relativa alla frequenza o alla frequenza dell’acquisizione dei dati da un’origine dati di terze parti a Adobe Experience Platform.

**Punteggio**: Il punteggio è il processo di generazione di informazioni dai dati utilizzando un modello qualificato.

**Schema**: Uno schema è un insieme di regole che rappresentano e convalidano la struttura e il formato dei dati. Uno schema è composto da una classe e da gruppi di campi facoltativi e viene utilizzato per creare set di dati e datastreams. Uno schema può includere attributi comportamentali, marche temporali, identità, definizioni di attributi, relazioni e altro ancora.

**Gruppo di campi schema**: In Experience Data Model (XDM), un gruppo di campi schema consente agli utenti di estendere i campi riutilizzabili per definire uno o più attributi destinati a essere inclusi in uno schema.

**Libreria schema**: La Libreria schema contiene risorse XDM standard di settore, rese disponibili da Adobe, nonché risorse personalizzate definite dalla tua organizzazione.

**Registro di sistema dello schema**: Il Registro di sistema dello schema fornisce un&#39;interfaccia utente e l&#39;API RESTful utilizzate per visualizzare e gestire tutte le risorse correlate allo schema nella Libreria schema.

**Chiave di accesso segreta**: Una chiave di accesso segreta è [!DNL Amazon] Chiave S3 utilizzata insieme all’ID chiave di accesso per firmare le richieste AWS.

**Segmento**: Un segmento è un insieme di regole che includono attributi e dati evento che qualificano un numero di profili come pubblico.

**Generatore di segmenti**: La [!DNL Segment Builder] è un ambiente di sviluppo visivo utilizzato per creare le definizioni dei segmenti. Funge da componente comune di tutte le applicazioni che utilizzano Experience Platform Segmentation Service.

**Definizione del segmento**: Una definizione di segmento è il set di regole utilizzato per descrivere le caratteristiche o il comportamento chiave di un pubblico target. Una volta concettualizzate, le regole descritte in una definizione di segmento vengono utilizzate per determinare i membri del pubblico qualificati per un segmento.

**Metodo di valutazione dei segmenti**: Esistono due metodi di valutazione dei segmenti: programmato e on-demand. La valutazione pianificata consente di eseguire una pianificazione ricorrente per eseguire un processo di esportazione in un momento specifico, mentre la valutazione su richiesta comporta la creazione di un processo di segmento per creare il pubblico immediatamente.

**Esportazione del segmento**: L’esportazione del segmento è uno dei due tipi di destinazioni nell’Experience Platform. Con l’esportazione dei segmenti, puoi inviare i profili qualificati e mappati alla destinazione. Utilizza ID di segmenti e utenti e dati pseudonimi e si integra in genere con i social network e altre piattaforme di destinazione dei media digitali.

**ID segmento**: Un ID segmento è un identificatore generato automaticamente associato a un segmento.

**Iscrizione al segmento**: L’appartenenza al segmento mostra i segmenti di cui un profilo fa attualmente parte.

**Regole del segmento**: Le regole del segmento definiscono le condizioni che determinano se un profilo si qualifica per un segmento.

**Segmentazione**: La segmentazione è il processo di divisione di un gruppo elevato di clienti, potenziali o consumatori in gruppi più piccoli che condividono attributi simili e risponderanno in modo simile a strategie di marketing specifiche.

**Framework ML di Sensei**: Sensei ML Framework è un framework di machine-learning (ML) unificato che sfrutta i dati Experienci Platform per consentire agli scienziati dei dati di sviluppare servizi di intelligence guidati da ML in modo più rapido, scalabile e riutilizzabile.

**Etichette sensibili (&quot;S&quot;)**: Le etichette sensibili (&quot;S&quot;) vengono utilizzate per classificare i dati ritenuti sensibili, ad esempio diversi tipi di dati comportamentali o geografici che si desidera contrassegnare come sensibili.

**Servizi**: Un potente framework per l&#39;operazionalizzazione dei servizi AI e ML sfruttando i servizi intelligenti Adobe. I servizi offrono esperienze cliente personalizzate in tempo reale o consentono di gestire servizi intelligenti personalizzati.

**Azione di marketing per la personalizzazione di una singola identità**: Un’azione di marketing che utilizza i dati per la personalizzazione dei contenuti sul sito. Per personalizzazione in sito si intende qualsiasi dato utilizzato per fare deduzioni sugli interessi degli utenti e utilizzato per selezionare quali contenuti o annunci vengono serviti in base a tali deduzioni.

**Etichetta di utilizzo dei dati S1**: Un `S1` l’etichetta di utilizzo dei dati viene utilizzata per classificare i dati specificando latitudine e longitudine che possono essere utilizzate per determinare la posizione precisa di un dispositivo.

**Etichetta di utilizzo dati S2**: Un `S2` l’etichetta per l’utilizzo dei dati viene utilizzata per classificare i dati che possono essere utilizzati per determinare un’area geografica ampiamente definita.

**Origine**: Una sorgente è un termine generico per qualsiasi connettore di ingresso in Platform. Vedi anche: Connettore sorgente

**Attributo di origine**: Un attributo di origine è un campo nel set di dati di origine. Gli attributi di origine sono mappati ai campi dello schema di destinazione.

**Catalogo di origine**: Il catalogo sorgente è l’elenco dei connettori sorgente disponibili nell’Experience Platform.

**Categoria di origine**: Una categoria di origine è un raggruppamento di origini con caratteristiche simili.

**Connettore sorgente**: I connettori sorgente (noti anche come sorgenti) consentono agli utenti di acquisire facilmente dati da più sorgenti, consentendo la strutturazione, l’etichettatura e il miglioramento dei dati tramite i servizi Experience Platform. I dati possono essere acquisiti da una varietà di fonti come l’archiviazione basata su cloud, il software di terze parti e i sistemi CRM.

**Connessione streaming**: Una connessione in streaming è un endpoint univoco fornito da Adobe e associato all’organizzazione IMS di un cliente per lo streaming dei dati in Experience Platform.

**Spazio dei nomi di identità standard**: I namespace di identità standard sono spazi dei nomi di identità predefiniti forniti da Adobe, che rappresentano soluzioni standard di settore comunemente utilizzate per identificare i clienti.

**Acquisizione in streaming**: L’acquisizione in streaming ti consente di inviare in tempo reale dati da dispositivi lato client e lato server all’Experience Platform.

**Segmentazione streaming**: La segmentazione in streaming è un processo continuo di selezione dei dati che aggiorna i segmenti in risposta all’attività dell’utente. Una volta generato e salvato un segmento, la definizione del segmento viene applicata ai dati in arrivo a [!DNL Real-time Customer Profile]. Gli aggiornamenti e le rimozioni dei segmenti vengono elaborati regolarmente, garantendo che il pubblico di destinazione rimanga rilevante.

**Vista di sistema**: La Vista sistema è una rappresentazione visiva dei set di dati di origine che scorrono [!DNL Real-time Customer Profile] verso le destinazioni.

## T

**Tag**: In Adobe Experience Platform, i tag forniscono strumenti per distribuire, unificare e gestire le integrazioni di analisi, marketing e pubblicità necessarie per fornire ai clienti esperienze personalizzate su tutti i dispositivi client.

**Funzioni di Target**: Nella mappatura delle funzioni, una feature di destinazione è la feature prevista da un modello.

**Dati della serie temporale**: I dati delle serie temporali forniscono un&#39;istantanea del sistema nel momento in cui un&#39;azione è stata eseguita direttamente o indirettamente da un soggetto del record.

**Modello addestrato**: Un modello addestrato rappresenta l&#39;output eseguibile di un processo di formazione del modello, in cui un set di dati di formazione è stato applicato all&#39;istanza del modello. Un modello qualificato manterrà un riferimento a qualsiasi servizio Web intelligente creato da esso. Un modello qualificato è adatto per il punteggio e la creazione di un servizio web intelligente.

**Token**: Un token è un tipo di protezione di autenticazione a due fattori che può essere utilizzato per autorizzare l&#39;uso di servizi computer con [!DNL Query Service].

## U

**Schema dell&#39;unione**: Uno schema di unione è un consolidamento di schemi che condividono la stessa classe e sono stati abilitati per [!DNL Real-time Customer Profile]. Possono esistere più schemi di unione per un&#39;organizzazione, ma può esserci un solo schema di unione per classe.

## V

## W

## X

**XDM**: Consulta Experience Data Model (XDM).

**Evento decisionale XDM**: XDM Decision Event è una classe basata su serie temporale utilizzata per acquisire osservazioni sul risultato e il contesto di un&#39;attività decisionale. Ciò include informazioni su come è stata presa la decisione, quando si è verificato, quali opzioni sono state proposte (e scelte), e quale stato contestuale esisteva che ha influenzato la decisione o può essere osservato durante il processo decisionale.

**ExperienceEvent XDM**: XDM ExperienceEvent è una classe basata su serie temporale utilizzata per acquisire lo stato del sistema quando si è verificato un evento (o un set di eventi), incluso il punto nel tempo e l’identità dell’oggetto coinvolto. Vedi anche: Evento esperienza

**Profilo individuale XDM**: XDM [!DNL Individual Profile] è una classe basata su record che forma una singola rappresentazione degli attributi di soggetti identificati e parzialmente identificati. I profili altamente identificati possono essere utilizzati per comunicazioni personali o per impegni mirati e possono contenere informazioni personali dettagliate come nome, genere, data di nascita, ubicazione e informazioni di contatto, compresi i numeri di telefono e gli indirizzi e-mail.

**Sistema XDM**: XDM System rappresenta il framework che rende operativi gli schemi XDM da utilizzare nei servizi di Experience Platform a valle.

## S

## Z
