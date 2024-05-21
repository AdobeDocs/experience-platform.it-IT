---
title: Assistente AI per Adobe Experience Platform
description: Scopri come utilizzare l’Assistente AI per navigare e comprendere i concetti di Experienci Platform e Real-time Customer Data Platform e le informazioni sull’utilizzo degli oggetti.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 8be1c222-3ccd-4a41-978e-33ac9b730f8c
source-git-commit: 6beaefb23f4deb382b7844fcf58efbd72b1da2ec
workflow-type: tm+mt
source-wordcount: '3122'
ht-degree: 0%

---

# Assistente AI per Adobe Experience Platform

>[!NOTE]
>
>L’Assistente AI per Adobe Experience Platform è attualmente in versione beta. La funzione e la documentazione sono soggette a modifiche.

L’Assistente AI è una funzione dell’interfaccia utente che consente di navigare e comprendere i concetti e le informazioni di utilizzo di Adobe Experience Platform e Real-time Customer Data Platform relativi agli oggetti.

È possibile eseguire una query su Assistente IA per ottenere informazioni quali:

* Linee guida su come eseguire attività relative a dati e tipi di pubblico.
* Stati e metriche degli oggetti dati esistenti nell’organizzazione.
* Esempi di casi d’uso e sfumature per comprendere meglio gli oggetti dati, inclusi attributi, tipi di pubblico, flussi di dati, set di dati, destinazioni, schemi e origini.

Leggi la guida seguente per scoprire come utilizzare l’Assistente AI per navigare e comprendere i flussi di lavoro di Experienci Platform e Real-Time CDP.

>[!BEGINSHADEBOX]

**Come funziona l’Assistente AI?**

L&#39;Assistente AI risponde alle domande inviate eseguendo una query su un database e quindi traducendo i dati dal database in una risposta leggibile.

Questa rappresentazione interna dei dati sottostanti è nota anche come Knowledge Graph (Grafico della conoscenza), un web completo di concetti, dati e metadati per una determinata risposta.

Il Knowledge Graph è costituito da sottografi a cui viene fatto riferimento ogni volta che vengono inviate query:

* Dati sull’utilizzo del cliente.
* Dati sull’utilizzo dei clienti nei vari meta-store.
* Documentazione di Experience League.

Prima di eseguire una query su Assistente IA, è necessario considerare due classi di domande:

* **Domande sui concetti**: le domande sui concetti riguardano concetti Adobi relativi a dati o tipi di pubblico. Alcuni esempi di domande sui concetti includono:
   * Qual è la differenza tra segmentazione in batch e segmentazione in streaming?
   * Esistono modelli di dati di settore e come li utilizzo?
   * Per che cosa si usa meglio Real-Time CDP?
* **Domande sull’utilizzo**: le domande sull’utilizzo riguardano gli oggetti dati all’interno dell’organizzazione. Alcuni esempi di domande sull’utilizzo includono:
   * Quanti set di dati ho?
   * Quanti attributi dello schema non sono mai stati utilizzati?
   * Quale pubblico è stato attivato?

>[!ENDSHADEBOX]

## Obiettivi che puoi raggiungere con l’Assistente AI {#objectives}

È possibile utilizzare l&#39;Assistente IA per obiettivi quali:

| Obiettivo | Descrizione | Esempio |
| --- | --- | --- |
| Concetti di apprendimento e flussi di lavoro continui | <ul><li>In qualità di utente principiante, puoi utilizzare l’Assistente AI per apprendere i concetti di Real-Time CDP e Adobe Journey Optimizer e integrarti in prodotti e funzionalità che non conosci.</li><li>In qualità di utente esperto, puoi utilizzare l’Assistente IA per risolvere un caso limite che potrebbe bloccare il flusso di lavoro. | <ul><li>Come si imposta una dashboard in Analytics di Percorso?</li><li>Dimmi alcuni casi d’uso per Real-Time CDP.</li></ul> |
| Risoluzione dei problemi | Utilizza l’Assistente AI per scoprire come eseguire il debug degli errori di base che potrebbero verificarsi nel flusso di lavoro. | <ul><li>Cos’è questo errore {ERROR_MESSAGE} Cioè?</li><li>Perché non sono in grado di eliminare il pubblico denominato &quot;Luma: E-mail Audience&quot;?</li></ul> |
| Igiene delle sandbox | Utilizza l’Assistente AI per identificare eventuali oggetti duplicati o inutilizzati in modo da poter gestire la sandbox in modo efficiente. | <ul><li>Puoi mostrarmi tipi di pubblico simili?</li><li>Esistono schemi a cui non è associato un set di dati?</li></ul> |
| Analisi del valore | Utilizza l’Assistente AI per identificare gli oggetti dati più utilizzati e valutare eventuali indicatori di prestazioni o trovare gli oggetti dati più importanti. | <ul><li>Quanti profili ci sono nella definizione del segmento &quot;Luma: Pubblico e-mail&quot;?</li><li>Quando sono stati attivati i tipi di pubblico per la destinazione Tipi di pubblico di Experience Cloud?</li></ul> |
| Ricerca | Utilizza l’Assistente AI per trovare oggetti Experienci Platform supportati come tipi di pubblico, set di dati, destinazioni, schemi e origini. | <ul><li>Elencare i tipi di pubblico contenenti &quot;Luma&quot; nel nome creati nell’ultimo trimestre.</li><li>Quali attributi sono presenti nello schema XDM &quot;Luma: Azioni personalizzate&quot;?</li></ul> |
| Analisi dell&#39;impatto | Utilizza l’Assistente AI per identificare gli oggetti dati utilizzati in alcuni flussi di lavoro in modo da poter valutare l’impatto di eventuali modifiche. | <ul><li>Quali tipi di pubblico utilizzano `homeAddress.city` nello schema &quot;Luma: PersonProfiles&quot;?</li><li>Quali set di dati sono `consents.marketing.push.val` attributo profilo memorizzato in?</li></ul> |

## Accedere all’Assistente AI nell’interfaccia utente di Experienci Platform

Per avviare l&#39;Assistente IA, selezionare **[!UICONTROL Icona Assistente AI]** dall’intestazione superiore dell’interfaccia utente di Experienci Platform.

![La pagina Home dell’Experience Platform, con l’icona Assistente AI selezionata e l’interfaccia Assistente AI aperta.](./images/ai-assistant/ai-assistant.png)

Viene visualizzata l’interfaccia di AI Assistant, che fornisce immediatamente le informazioni necessarie per iniziare. Puoi utilizzare le opzioni fornite in [!UICONTROL Idee per iniziare] per rispondere a domande e comandi quali:

* [!UICONTROL Quale dei miei tipi di pubblico viene attivato?]
* [!UICONTROL Che cos’è uno schema?]
* [!UICONTROL Alcuni casi d’uso comuni per Real-Time CDP]

![La sezione &quot;Idee per iniziare&quot; di AI Assistant.](./images/ai-assistant/ideas-to-get-started.png)

Per interagire con l&#39;Assistente AI, utilizzare la casella di input per digitare le query o i comandi. È inoltre possibile utilizzare (**`+`**) per utilizzare la funzione di completamento automatico e l&#39;icona del segnalibro per accedere alle query e ai comandi con segnalibro.

![Viene evidenziata la casella di input dell&#39;Assistente AI.](./images/ai-assistant/interact.png)

## Esempio di utilizzo: utilizza l’Assistente IA per accelerare il processo di creazione dello schema

>[!NOTE]
>
>Il seguente flusso di lavoro è un esempio che utilizza il processo di creazione dello schema dell’evento esperienza per illustrare come utilizzare l’Assistente AI quando si utilizza l’interfaccia utente di Experienci Platform.

Considera un caso d’uso in cui stai creando una **Schema permuta dispositivo in evento**. Durante il processo di creazione dello schema dell’evento esperienza, ti imbatti nel `eventType` campo. &quot;A questo punto, puoi scegliere di uscire dal flusso di lavoro e fare riferimento a [nozioni di base su una composizione di schema](../xdm/schema/composition.md) oppure puoi utilizzare l’Assistente AI per recuperare le risposte alle tue domande e trovare risorse aggiuntive tramite i collegamenti alla documentazione consigliati dall’Assistente AI.&quot;

Per iniziare, immettere la domanda nella casella di testo fornita. Nell’esempio seguente, l’Assistente AI riceve la domanda: &quot;**Qual è il campo eventType in uno schema ExperienceEvent?**&quot;

![Assistente IA, ad Experience Platform, con la seguente domanda preparata per la query: &quot;Qual è il campo eventType in uno schema ExperienceEvent?](./images/ai-assistant/question.png)

L&#39;Assistente IA esegue quindi una query sulla knowledge base e calcola una risposta. Dopo alcuni istanti, l’Assistente IA restituisce una risposta e i suggerimenti correlati che puoi utilizzare come prompt di follow-up.

![Assistente IA, ad Experience Platform con una risposta alla query precedente.](./images/ai-assistant/answer.png)

Dopo aver ricevuto una risposta dall’Assistente AI, puoi scegliere tra una serie di opzioni per decidere come procedere.

### Salvare la query {#save-your-query}

+++Selezionare questa opzione per visualizzare un esempio di come salvare una query

Per salvare la query, selezionare l&#39;icona del segnalibro accanto alla domanda.

![Schermata di un segnalibro selezionato.](./images/ai-assistant/save-your-query.png)

Per accedere alle query salvate, seleziona l’icona del segnalibro sotto la casella di input, quindi seleziona la query da eseguire.

![Schermata dell’icona del segnalibro e un elenco delle query salvate.](./images/ai-assistant/bookmarks.png)

+++

### Visualizzare i dati nella sandbox {#view-data-in-your-sandbox}

+++Seleziona per visualizzare l’esempio

A seconda della query, l’Assistente AI fornisce informazioni aggiuntive relative ai dati nella sandbox. Per visualizzare il modo in cui la risposta alla query si applica alla sandbox, seleziona **[!UICONTROL Nella sandbox].**

Durante questo passaggio, l’Assistente AI può fornire collegamenti diretti alle pagine dell’interfaccia utente di determinati oggetti in questione. Nell’esempio seguente, l’Assistente AI fornisce collegamenti diretti al [!UICONTROL Schemi] e [!UICONTROL Segmenti] Pagine dell’interfaccia utente.

![Schermata dell’opzione &quot;Nella sandbox&quot;.](./images/ai-assistant/in-your-sandbox.png)

+++

### Verifica la risposta {#verify-the-response}

+++Seleziona per visualizzare un esempio di come visualizzare le sorgenti

Per visualizzare le citazioni e convalidare la risposta dell’Assistente AI, seleziona **[!UICONTROL Mostra origini]**. L’Assistente AI fornisce collegamenti alla documentazione che ne conferma la risposta. È inoltre possibile utilizzare le query fornite dall’Assistente IA in [!UICONTROL Suggerimenti correlati] per esplorare ulteriormente gli argomenti relativi alla query originale.

![Schermata di &quot;Show sources&quot; (Mostra sorgenti).](./images/ai-assistant/show-sources.png)

+++

### Dati e visualizzazione di utilizzo {#usage-data-and-visualization}

+++Seleziona per visualizzare un esempio di domande sui dati di utilizzo e visualizzazione dei dati

Affinché l’Assistente AI risponda a una query sui dati di utilizzo all’interno della tua organizzazione, devi trovarti in una sandbox attiva.

Nell’esempio seguente, l’Assistente AI viene fornito con la seguente query: **&quot;Mostra le definizioni dei segmenti con più di 1000 profili e includi lo stato di attivazione.&quot;** L’Assistente AI risponde quindi con un grafico che visualizza i dati di segmenti e profili.

![Rispondi alla domanda sui dati di utilizzo.](./images/ai-assistant/data-usage-question.png)

Puoi passare il cursore sopra una singola barra per visualizzare dati specifici. È inoltre possibile selezionare l&#39;icona di espansione per ingrandire la visualizzazione del grafico.

![Segui la domanda che illustra la visualizzazione dei dati.](./images/ai-assistant/data-visualization.png)

Viene visualizzata una vista espansa della visualizzazione. Puoi utilizzare la finestra modale espansa per esaminare ulteriormente i dati ed è particolarmente utile quando la visualizzazione restituisce un numero elevato di colonne.

![Grafico espanso.](./images/ai-assistant/chart-expanded.png)

Quando viene richiesta una domanda relativa ai dati di utilizzo, l’Assistente AI spiega in che modo ha calcolato la risposta. Nell’esempio seguente, l’Assistente AI illustra i passaggi necessari per visualizzare le definizioni dei segmenti con più di 1000 profili e i rispettivi stati di attivazione.

![Rispondi alla domanda sulle definizioni dei segmenti che illustra come l’Assistente AI ha calcolato la risposta.](./images/ai-assistant/results-explained.png)

Puoi anche fornire filtri e modifiche alle query e istruire l’Assistente AI affinché esegua il rendering dei risultati in base ai filtri inclusi. Ad esempio, puoi chiedere all’Assistente AI di mostrare una tendenza delle definizioni dei segmenti di conteggio nell’ordine della data di creazione, rimuovere le definizioni dei segmenti con profili totali pari a zero e utilizzare i nomi dei mesi invece dei numeri interi durante la visualizzazione dei dati.

+++

### Usa completamento automatico {#use-auto-complete}

+++Seleziona per visualizzare un esempio di completamento automatico

È possibile utilizzare la funzione di completamento automatico per ricevere un elenco di oggetti dati esistenti nella sandbox. I consigli di completamento automatico sono disponibili per i seguenti domini: pubblico, schemi, set di dati, origini e destinazioni.

È possibile utilizzare il completamento automatico includendo il simbolo più (**`+`**) nella query. In alternativa, è possibile selezionare il segno più (**`+`**) che si trova nella parte inferiore della casella di immissione testo. Viene visualizzata una finestra con un elenco degli oggetti dati consigliati dalla sandbox.

![Esempio di completamento automatico](./images/ai-assistant/auto-complete-one.png)

Quindi, selezionare l&#39;oggetto dati di cui si desidera eseguire la query per completare la domanda e inviare la domanda.

![Esempio di completamento automatico con domanda e risposta](./images/ai-assistant/auto-complete-two.png)

+++

### Usa multi-giro {#use-multi-turn}

+++Selezionare per visualizzare un esempio di tornitura multipla

È possibile utilizzare le funzionalità multi-turn di AI Assistant per avere una conversazione più naturale durante la tua esperienza. L’Assistente AI è in grado di rispondere alle domande di follow-up, fornite. tale contesto può essere dedotto da un’interazione precedente.

Nell’esempio seguente, a AI Assistant viene richiesto il numero totale di flussi di dati nell’organizzazione corrente.

![Esempio di multi-turn](./images/ai-assistant/multi-turn-one.png)

Successivamente, l’Assistente IA riceve un’altra richiesta di follow-up. Questa volta, l’Assistente IA risponde elencando i flussi di dati attualmente presenti nell’organizzazione.

![Esempio di multi-turn con domanda e risposta](./images/ai-assistant/multi-turn-two.png)

+++

## Documentazione {#documentation}

Attualmente, l’indice della documentazione copre Adobe Experience Platform (Real-Time CDP e Audiences). L’indice viene aggiornato periodicamente.

Il modello di recupero della documentazione di è addestrato su Experienci Platform (Real-Time CDP e Audiences). Non è possibile rispondere a domande che esulano dall’ambito di Adobe Experience Platform, come ad esempio domande su altri prodotti Adobe come Adobe Target e la suite di Creative Cloud.

## Dati di utilizzo {#usage-date}

Puoi anche porre domande all’Assistente AI sui dati di utilizzo nei seguenti domini:

* Attributi
* Tipi di pubblico
* Flussi di dati
* Set di dati
* Destinazioni _Al momento non è possibile rispondere ad alcune domande relative agli account e al flusso di dati._
* Schemi _Al momento non è possibile rispondere alle domande relative ai gruppi di campi._
* Sorgenti _(Al momento non è possibile rispondere alle domande relative ai conti)._

Per le query di dati di utilizzo, le risposte potrebbero non riflettere lo stato corrente dell’interfaccia utente. I dati che supportano queste domande vengono aggiornati una volta ogni 24 ore. Ad esempio, le modifiche apportate dagli utenti in Real-Time CDP durante il giorno vengono sincronizzate con gli archivi dati di notte e quindi diventano disponibili per le domande degli utenti di mattina. Inoltre, dovrai accedere a una sandbox per informazioni su dati specifici relativi a oggetti come tipi di pubblico, schemi, set di dati, attributi e destinazioni.

### Esempi di domande sui dati di utilizzo {#example-usage-data-questions}

+++Seleziona per visualizzare un elenco di esempi di domande sui dati di utilizzo

Leggi la tabella seguente per esempi di domande sui dati di utilizzo e i rispettivi casi di utilizzo:

| Tipo di domanda | Caso d’uso | Esempi |
| --- | --- | --- | 
| Derivazione dei dati | Tracciare l&#39;utilizzo di uno o più oggetti tra altri oggetti Experienci Platform | <ul><li>Quali set di dati utilizzano lo schema &quot;schema ACME&quot;?</li><li>Quanti set di dati sono stati acquisiti utilizzando lo stesso schema?</li><li>Quali set di dati sono stati utilizzati nei tipi di pubblico attivati?</li><li>Elencare gli schemi con attributi utilizzati nei tipi di pubblico attivati.</li><li>Mostra i tipi di pubblico attivati su &quot;Destinazioni ACME&quot; e con più di 1000 profili.</li><li>Mostra gli attributi utilizzati nei tipi di pubblico attivati che sono stati modificati dopo gennaio 2023.</li><li>Quali sono i set di dati acquisiti tramite l’origine &quot;ACME Amazon S3&quot;?</li><li>Quali flussi di dati sono associati a &quot;Flusso di dati sulla fedeltà ACME&quot;?</li><li>Elencare gli schemi relativi ai tipi di pubblico attivati e creati nell’ultimo anno.</li></ul> |
| Distribuzione e aggregazioni | Domande basate su riepilogo sull&#39;utilizzo degli oggetti di Experience Platform | <ul><li>Qual è la percentuale di pubblico attivato?</li><li>Quanti campi vengono utilizzati nella segmentazione?</li><li>Quali tipi di pubblico vengono attivati nel maggior numero di destinazioni?</li><li>Elencare tipi di pubblico duplicati.</li><li>Mostra i tipi di pubblico attivati in &quot;Destinazioni ACME&quot; e classificali in base alla dimensione del profilo.</li><li>Qual è la percentuale di tipi di pubblico che non sono stati attivati ma hanno più di 100 profili. Mostratemi i loro nomi.</li><li>Elenca i 3 connettori di origine che acquisiscono i dati nei miei set di dati.</li><li>Elencami i primi 5 attributi utilizzati nei tipi di pubblico attivati in base alla loro occorrenza.</li></ul> |
| Ricerca oggetto | Recuperare o accedere a un oggetto Experience Platform o alle relative proprietà. | <ul><li>A quali set di dati non è associato alcuno schema</li><li>Elencare gli attributi utilizzati per &quot;Pubblico ACME&quot;?</li><li>Dammi l’elenco degli schemi abilitati per il profilo ma non modificati dalla loro creazione.</li><li>Quali tipi di pubblico sono stati modificati nell&#39;ultima settimana?</li><li>Elencami i tipi di pubblico che hanno le stesse definizioni di segmenti insieme alla loro data di creazione.</li><li>Quali set di dati sono abilitati per il profilo e includono anche quanti tipi di pubblico sono stati creati da ciascun set di dati.</li><li>Quali account di origine sono associati al set di dati XYZ?</li><li>Visualizza la definizione del segmento e la data di modifica di &quot;Pubblico ACME&quot;.</li></ul> |
| Confronto degli oggetti | Identifica tipi di pubblico duplicati. | <ul><li>In base alla definizione del segmento, elenca i tipi di pubblico che sono duplicati.</li><li>Quali tipi di pubblico duplicati vengono attivati nelle &quot;Destinazioni ACME&quot;.</li></ul> |

+++

## Formulazione delle domande {#phrasing-your-questions}

Per ottenere una risposta il più accurata possibile, è necessario formulare le domande all’Assistente IA con chiarezza e contesto. Consulta il seguente elenco di suggerimenti per indicazioni su come porre una domanda chiara con il contesto:

* Dichiara il tuo compito e/o la tua domanda in modo conciso.
* Evita un linguaggio ambiguo o una sintassi troppo complessa per facilitare la comprensione.
* Fornisci un contesto rilevante relativo all’attività e/o alla domanda, in quanto il contesto può aiutare l’Assistente AI a generare risposte più rilevanti.

Leggi la tabella seguente per ulteriori indicazioni sulle best practice da seguire quando si pongono domande all’Assistente IA:

| Esegui | Esempio |
| --- | --- |
| <ul><li>Specificare l&#39;oggetto o le informazioni da recuperare o analizzare.</li><li>Provare a inserire i nomi degli oggetti dati tra virgolette. Se si conosce solo una parte del nome dell&#39;oggetto, è possibile specificarlo nella domanda.</li><li>Utilizzare [completamento automatico dell&#39;oggetto](./ui-guide.md#use-auto-complete) per aiutare l’Assistente AI a comprendere meglio il contesto della query.</li></ul> | <ul><li>Quali set di dati utilizzano lo schema &quot;Luma - Fedeltà&quot;?</li><li>Mostrami i segmenti attivati il cui nome contiene &quot;Luma&quot;. Classificale in base al numero di profili.</li></ul> |
| <ul><li>Evita ambiguità e usa un linguaggio chiaro</li><li>Utilizza una terminologia precisa per garantire una maggiore chiarezza nella query.</li><li>Quando fai domande su Adobe Experience Platform, prova a utilizzare la terminologia specifica di Experienci Platform per migliorare la pertinenza delle risposte.</li></ul> | <ul><li>Quanti profili ho in &quot;Pubblico ACME&quot;.</li><li>Mostra i primi 5 attributi XDM utilizzati nei tipi di pubblico attivati.</li></ul> |
| <ul><li>Fornisci contesto o specifica un criterio per filtrare i risultati.</li><li>Utilizza un criterio di filtro nelle domande per limitare il volume di dati nella risposta.</li></ul> | <ul><li>Mostra i tipi di pubblico che non sono stati attivati e che sono stati creati più di 6 mesi fa e che non sono mai stati modificati.</li><li>Mostra i tipi di pubblico attivati su &quot;Destinazione ACME&quot; e con più di 10000 profili.</li></ul> |

{style="table-layout:auto"}

| Non | Esempio |
| --- | --- |
| Utilizza un linguaggio vago o ambiguo. | <ul><li>Datemi informazioni sui set di dati.</li><li>Quanti utenti ho in &quot;ACME Audience&quot;?</li><li>Mostra segmenti.</li><li>Attributi elenco.</li></ul> |
| Eseguire richieste incomplete. | &quot;Luma - Set di dati fedeltà&quot; |
| Acquisisci conoscenza senza contesto. | <ul><li>Pubblico negli ultimi 6 mesi.</li><li>Crea una query per me.</li></ul> |
| Formulare query eccessivamente complesse. | Fornisci un’analisi completa della derivazione dei dati tra tutti gli oggetti e le loro dipendenze. |
| Omettere criteri o parametri. | Mostra i set di dati. |

{style="table-layout:auto"}

## Fornire feedback {#feedback}

>[!BEGINSHADEBOX]

**Richiesta del feedback**

In questa fase di Alpha, ti invitiamo a fornire un feedback sulle risposte ricevute dall’Assistente AI. Tutte le risposte e i feedback inviati vengono esaminati per continuare a migliorare l’esperienza di AI Assistant.

Per fornire un feedback, seleziona Miniature in alto o Miniature in basso dopo aver ricevuto una risposta dall’Assistente AI, quindi inserisci il tuo feedback nella casella di testo fornita. Quindi, seleziona **[!UICONTROL Invia feedback]** da inviare.

>[!ENDSHADEBOX]

+++Fornisci feedback

>[!BEGINTABS]

>[!TAB Miniature in alto]

Seleziona l’icona miniature in alto per fornire un feedback su ciò che è andato bene con la tua esperienza con l’Assistente AI.

![La finestra di feedback positivo.](./images/ai-assistant/thumbs-up.png)

>[!TAB Miniature in basso]

Seleziona l’icona miniature verso il basso per fornire feedback su cosa potrebbe essere migliorato in base alla tua esperienza con l’Assistente AI. Durante questo passaggio, puoi anche fornire commenti specifici relativi alla tua esperienza. Il feedback fornito nei commenti viene rivisto ogni giorno.

![La finestra di feedback negativo.](./images/ai-assistant/thumbs-down.png)

>[!TAB Contrassegno]

Seleziona l’icona del flag per fornire ulteriori rapporti sulla tua esperienza utilizzando l’Assistente AI.

![Finestra dei risultati del rapporto.](./images/ai-assistant/flag.png)

>[!ENDTABS]

+++

## Informazioni aggiuntive {#additional-information}

Fai riferimento a questa sezione per ulteriori informazioni sull’Assistente IA, ad Experience Platform.

### Avvertenze e limitazioni {#caveats-and-limitations}

La sezione seguente illustra le avvertenze e le limitazioni correnti da considerare quando si utilizza l’Assistente IA.

#### Piccolo talk limitato

Puoi partecipare a una piccola conversazione con l’Assistente AI, ma al momento questa capacità è limitata.

#### Domande sulle funzionalità

L’Assistente AI può fornire un’impressione imprecisa di ciò che è in grado di fare. Potrebbe rispondere erroneamente ai seguenti tipi di domande:

| Domanda di esempio | Nota |
| --- | --- |
| &quot;Puoi rispondere a domande su {ENTITY}?&quot; | Se l’Assistente AI è in grado di trovare una singola pagina che fa riferimento a una determinata entità nel suo indice, risponderà sì. |
| &quot;Lo sai che **x** lingua?&quot; | L’Assistente per l’intelligenza artificiale attualmente supporta solo l’inglese, ma potrebbe rispondere &quot;sì&quot; a causa del fatto che il modello sottostante è in grado di supportarlo. |
| &quot;Puoi fare...?&quot; | L’Assistente AI può rispondere di sì, anche se non è possibile. |

### Suggerimenti {#tips}

La sezione seguente illustra alcuni suggerimenti e soluzioni da prendere in considerazione quando si utilizza l’Assistente IA.

#### È possibile rispondere alle domande con un&#39;informazione errata

In alcuni casi, quando si pongono domande sui dati di utilizzo, si può ottenere una risposta in base alla documentazione. Ciò si verifica perché l’Assistente AI può instradare erroneamente la domanda all’origine delle informazioni errata. Per evitare questo problema:

* Riformulare la domanda per utilizzare un linguaggio più simile a quello SQL
* Chiamando in modo esplicito l&#39;origine delle informazioni da utilizzare.

Leggi la tabella seguente per alcuni esempi:

| Domanda errata | Buona domanda | Note |
| --- | --- | --- |
| Qual è il mio pubblico più grande? | Qual è il mio pubblico più grande? Utilizzo dei dati. | Indica esplicitamente all’Assistente IA che desideri che la risposta sia basata sui dati. |
| Qual è il mio pubblico più grande? | Elencate il mio pubblico più grande. | Esistono casi in cui una domanda &quot;cosa...&quot; può essere scambiata per una domanda basata su documentazione. L’utilizzo di un comando come &quot;list&quot; è un indicatore più forte del fatto che ti stai ponendo una domanda con i dati nel contesto. |
| Quanti set di dati ho? | Conta i miei set di dati. | La domanda originale funziona per i tipi di pubblico, ma potrebbe non funzionare con i set di dati. |
