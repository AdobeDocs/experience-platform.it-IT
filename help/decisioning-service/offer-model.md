---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Offer Decisition Domain Model
topic: overview
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '2614'
ht-degree: 0%

---


# Panoramica sul modello di dominio di decisione offerta

La decisione dell&#39;offerta è un caso d&#39;uso [!DNL Decisioning Service] entro il quale si formalizzano e si gestiscono centralmente le regole e le previsioni utilizzate per coinvolgere i clienti nelle offerte. La decisione dell&#39;offerta è considerata un tipo di decisione _**sul**_ contenuto. In questo caso d’uso, le opzioni _****_ decisionali sono denominate _**offerte**_ e sono caratterizzate in quanto tali dal contenuto ad esse allegato. Per un&#39;introduzione al modello a oggetti utilizzato dal [!DNL Decisioning Service], fare riferimento a [Decisioning Service Domain Model](experience-model.md).

L&#39;obiettivo è quello di presentare all&#39;utente finale una &quot;Migliore offerta&quot; in qualsiasi canale basata su criteri di targeting, vincoli di costi e di frequenza, nonché interazioni preliminari tra i canali, comprese le offerte precedenti.

Come per tutti i casi di utilizzo di decisioni, le opzioni di decisione (offerte) vengono gestite in un archivio condiviso da un numero qualsiasi di applicazioni. Le offerte possono essere create da diversi dipartimenti dell&#39;organizzazione o da partner, e tali offerte possono essere aggiunte e rimosse ogni giorno.

Le offerte sono visivamente posizionate in esperienze più grandi dall&#39;applicazione che fornisce l&#39;esperienza. _**I posizionamenti**_, talvolta denominati punti o slot, sono componenti importanti per la creazione di una strategia. La progettazione di una strategia di offerta spesso inizia con la definizione di tali posizionamenti. In genere, un&#39;offerta presenta più rappresentazioni _**di**_ contenuto in modo che possa essere correttamente integrata in una varietà di esperienze, ognuna delle quali presenta vincoli dimensionali o di altro tipo e richiede formati multimediali diversi.

Le offerte hanno spesso un&#39;associazione con i beni o servizi fisici e il calcolo dei costi comporta. Un&#39;organizzazione deve essere in grado di limitare le risorse consumate dalle offerte e deve quindi essere in grado di _**limitare**_ il numero totale di volte che un&#39;offerta può essere proposta.

Il valore previsto di un&#39;offerta accettata all&#39;organizzazione è il criterio di ottimizzazione e si oppone al costo di fare un&#39;offerta. Costo, probabilità di accettazione e valore previsto viene utilizzato per classificare le offerte. L&#39;offerta migliore è quella con il maggiore impatto positivo previsto sugli obiettivi delle attività dell&#39;offerta.

La decisione dell&#39;offerta considera le interazioni che un utente finale ha avuto, _**su molti canali**_ e applicazioni, sfruttando i dati evento del profilo e dell&#39;esperienza dell&#39;utente finale. Ad esempio, un’applicazione call center può utilizzare la funzione di decodifica delle offerte per attivare o disattivare un’offerta basata sugli acquisti effettuati e sulle revisioni pubblicate dall’utente finale; oppure un&#39;applicazione di gestione e-mail può basarsi sulla decisione dell&#39;offerta per selezionare la prossima offerta migliore in una newsletter settimanale, in base alla cronologia di navigazione di un sito Web.

Le offerte hanno altre proprietà interessanti. Spesso, esiste un _**programma**_ o un intervallo di date e ore definito quando l&#39;offerta è valida e quando l&#39;offerta deve essere annullata.

Infine, l&#39;appello di un&#39;offerta si degrada con la frequenza con cui viene presentata. Un&#39;offerta che non viene accettata dopo essere stata ripetutamente proposta è un&#39;opportunità persa, perché una diversa offerta avrebbe potuto essere presentata. Per questo motivo, è _**necessario gestire la stanchezza**_ dell&#39;utente finale.

## Strategia di decisione dell&#39;offerta

L&#39;approccio generale consiste nel limitare la selezione delle offerte fino al soddisfacimento di tutti i vincoli, quindi applicare il modello di classificazione alle opzioni rimanenti, e quindi ottimizzarlo tra più attività utilizzando Vincoli di maschiatura (deduplicazione ed eliminazione delle scelte di fallback).

| Componente Strategia | Realizzato come |
| --- | --- |
| Attività decisionali | Attività di offerta |
| Opzioni decisionali | Offerta con rappresentazioni dei contenuti |
| Opzioni di fallback | Offerta di fallback con rappresentazioni dei contenuti |
| Set definitivo di opzioni decisionali | Inventario delle offerte (alias libreria di offerte) |
| Categorie argomenti | Filtro delle offerte basato su tag e identificatori delle offerte |
| Uscite decisionali | Proposta di un&#39;offerta per attività, per più attività contemporaneamente |
| Risultati della decisione | Evento esperienza previsto con riferimento all&#39;offerta, ad esempio `eventType='opened'` |
| Algoritmo decisionale | Logica interna del servizio, con parametri |
| Vincoli | Vincoli di posizionamento, vincoli di calendario, vincoli globali e per ogni limite utente, vincoli di deduplicazione |
| Norme di decisione | Eligibility rules (Regole di idoneità) |
| Modello per utilità *prevista* | Livello o priorità dell&#39;offerta |

Il numero totale di offerte nell&#39;inventario delle opzioni è in genere abbastanza grande (nell&#39;ordine di 10.000) e ogni attività di offerta può essere focalizzata su offerte che rientrano in una categoria diversa (argomento). La strategia di decisione dell&#39;offerta consente di allegare un filtro dell&#39;offerta a un&#39;attività dell&#39;offerta. Ulteriori vincoli saranno valutati al momento della richiesta della decisione.
Nelle sezioni seguenti vengono descritti in dettaglio i componenti per il dominio di decisione delle offerte.

## Offerte generali

Le offerte generali, denominate anche offerte personalizzate, sono le opzioni al centro delle attività decisionali dell&#39;offerta. Hanno attributi come nome e stato. L&#39;attributo status indica se l&#39;entità è pronta per essere inclusa nell&#39;elenco delle offerte approvate attive. Le offerte generali avranno diversi vincoli aggiunti. Ulteriori informazioni su questo argomento nella sezione ‎ Vincoli [di seguito](#offer-constraints).

## Contenuto nelle offerte

### Posizioni dell&#39;offerta

I posizionamenti definiscono i vincoli di contenuto e vengono utilizzati con un&#39;attività per specificare il punto in cui viene distribuita l&#39;esperienza migliore successiva. Questo riduce ulteriormente il numero di opzioni che possono essere considerate ed è un altro vincolo imposto dall&#39;attività. Questo è detto vincolo di posizionamento. Saranno prese in considerazione solo le opzioni il cui contenuto soddisfa un vincolo di posizionamento, come le offerte. Tale valutazione viene effettuata nelle prime fasi della strategia decisionale. Quando gli oggetti di opzione modificano i vincoli di posizionamento di ogni attività vengono rivalutati e l&#39;opzione può prendere in considerazione o cadere per una o più attività.

Non è responsabilità della [!DNL Decisioning Service] formalizzazione dei dettagli complessi delle dipendenze dei contenuti. Al contrario, ogni client identificherà l&#39;elenco dei posizionamenti tra tutti i canali e assegnerà a tali posizionamenti identificatori e nomi univoci. Facendo riferimento a una posizione particolare, il designer afferma che il contenuto specificato rientrerà nella posizione.

Quando si sviluppa il contenuto, l&#39;esperto di marketing dell&#39;offerta e il progettista dei contenuti concorderanno semplicemente (devono) su un &quot;contratto implicito&quot; che sta dietro il nome &quot;Home Page Hero Image&quot; o &quot;Service Call Opening Script&quot;. Il primo può essere concordato come un&#39;immagine di larghezza di 600 px e altezza di 350 px e il secondo può limitare il contenuto al testo in due varianti linguistiche che non sia più di 50 parole in tre o quattro frasi con una struttura semantica. Posizionamento per non memorizzare tutti i significati del contratto nascosto.

### Rappresentazioni offerte

Per garantire che un&#39;offerta possa essere presentata correttamente nei vari parametri dei posizionamenti nei canali, è necessario creare diverse rappresentazioni di tale offerta. Il contenuto associato alle offerte è raggruppato per posizionamenti. Ogni offerta può avere una o più rappresentazioni, ognuna delle quali fa riferimento a uno dei posizionamenti definiti. Ogni rappresentazione in un&#39;offerta deve utilizzare un posizionamento diverso. Più rappresentazioni un&#39;offerta ha più opportunità esiste per utilizzare l&#39;offerta in contesti di posizionamento diversi.

Un posizionamento limita il tipo di elementi di contenuto che è possibile aggiungere alla rappresentazione.

## Offerte di fallback

Le offerte di fallback sono opzioni decisionali che non presentano vincoli aggiuntivi, ad eccezione delle regole di posizionamento. Le offerte di fallback presentano rappresentazioni di contenuto associate a posizionamenti, proprio come qualsiasi altra offerta.

Le offerte di fallback sono specificate nelle attività per indicare un&#39;esperienza di contenuto valida da utilizzare quando vincoli combinati non qualificano tutte le opzioni ridotte. Poiché non dipende dal contesto di runtime o dal profilo, il vincolo di posizionamento può essere controllato in anticipo al momento dell&#39;assemblaggio dell&#39;attività. Utilizzando le offerte di fallback, esiste sempre una risposta alla domanda: Qual è attualmente l&#39;offerta migliore?

## Vincoli offerta

### Limiti calendario

Nel dominio di decisione delle offerte, le offerte hanno un periodo di validità. Ciò significa che l&#39;offerta non può essere proposta prima che sia trascorsa la data e l&#39;ora di inizio e non può più essere proposta dopo che sia trascorsa la data e l&#39;ora di fine. L&#39;entità dell&#39;offerta ha una struttura semplice che definisce tali vincoli del calendario.

Periodicamente, le offerte scadute verranno rimosse dall&#39;elenco delle opzioni considerate. Tuttavia, il filtro calendario viene applicato correttamente al momento della richiesta della decisione, in modo che i vincoli vengano applicati con precisione.

### Limiti di ritaglio

Le offerte possono avere un vincolo di capping facoltativo. È costituito da due valori:

- Il valore cap globale limita la frequenza con cui un&#39;offerta può essere proposta all&#39;interno dell&#39;intero gruppo di profili (pubblico con targeting).

- Il limite per profilo e determina la frequenza con cui l&#39;offerta può essere proposta allo stesso profilo.

### Vincoli di duplicazione

Quando viene richiesta una decisione, il cliente può chiedere proposte per più attività alla volta. Questo è uno scenario tipico nel processo di decisione dei contenuti. Ogni attività fornisce una o più opzioni di contenuto all&#39;esperienza complessiva. A causa dell&#39;aspetto della composizione, le decisioni devono essere arbitrate tra le attività per evitare duplicazioni, a meno che le attività non selezionino un sottoinsieme diverso dell&#39;inventario complessivo delle opzioni. Un&#39;opzione di alto livello sarà probabilmente classificata alta in tutte le attività e sarebbe scarsa esperienza se tutte le attività proponessero la stessa opzione. D&#39;altro canto, se un sistema di consegna vuole sapere quale sia la prossima migliore conversione tra tutti i canali e non ci sono vincoli di limite, potrebbe essere possibile proporre la stessa opzione tra diverse attività.

I vincoli di duplicazione non sono attualmente scritti nell&#39;archivio oggetti aziendali. Al contrario, la deduplicazione è la strategia predefinita in fase di esecuzione. Un parametro di richiesta può ignorare il comportamento predefinito per eliminare il passaggio di deduplicazione.

### [!DNL Profile] vincoli - Regole di idoneità

Finora, i vincoli discussi sono stati applicabili indipendentemente da chi sia stata effettuata la selezione dell&#39;offerta. La decodifica delle esperienze supporta anche un caso di utilizzo in cui la personalizzazione delle proposizioni si basa sugli eventi record e sulle serie temporali di un cliente. Le regole vengono valutate per profilo, per decidere se un&#39;offerta è qualificata o deve essere soppressa per quell&#39;utente. A tale scopo, è possibile associare a ogni offerta una regola di idoneità. Oltre agli eventi di profilo e di esperienza di un utente finale, la regola di idoneità prenderà in considerazione i dati contestuali in tempo reale. Tali dati vengono forniti dal servizio di consegna e possono assumere la forma di dati non correlati a un profilo come livelli di scorte, condizioni meteorologiche, orari di volo.

È importante distinguere tra regole di targeting e segmentazione, e tra regole di idoneità e regole di priorità per le decisioni. Per il targeting di un set di profili è l&#39;output (selezione dell&#39;audience) per l&#39;idoneità, un set di opzioni (offerte consentite) è l&#39;output della valutazione.

## Raccolte offerte

L&#39;inventario è l&#39;insieme complessivo di opzioni che vengono prese in considerazione per la decisione. L&#39;inventario può essere ulteriormente diviso in categorie o raccolte. Una raccolta di opzioni è rappresentata da un tag comune presente in tali opzioni. I filtri vengono utilizzati per verificare se le offerte rientrano in una determinata categoria, o più specificamente, condividono gli stessi tag o gli stessi tag.

### Tag

I tag consentono di indicare che un gruppo di opzioni appartiene a una categoria.

Un&#39;opzione può contenere più tag e può quindi essere associata a più categorie contemporaneamente. Le categorie possono anche sovrapporsi o contenerne un&#39;altra. Quando una categoria &quot;S&quot; è definita da offerte con il tag &quot;A&quot; e la categoria &quot;R&quot; è definita da opzioni con entrambi i tag &quot;A&quot; e &quot;B&quot;, allora &quot;S&quot; sarà un superset di &quot;R&quot;.

### Filtri

I filtri vengono utilizzati per definire i criteri per un set di opzioni che appartiene a una categoria. I filtri possono essere considerati come query rispetto all&#39;inventario delle offerte generali. Esistono due modi principali per creare un filtro: indicando che un&#39;offerta ha uno o più tag e selezionando esplicitamente il set di offerte. Il primo metodo può essere configurato per indicare che un&#39;offerta in quella raccolta deve avere tutti i tag specificati o che un&#39;opzione è qualificata quando dispone di almeno uno dei tag specificati.

Quando le opzioni vengono posizionate in modo esplicito in una raccolta, il relativo set di tag viene ignorato per tale raccolta.

## Attività offerta

Le attività configurano e controllano il processo decisionale. Attualmente, la strategia di decisione è principalmente predeterminata, ma le future iterazioni del modello di dominio di Offer Decisioning consentiranno la selezione di modelli, regole aggiuntive e vincoli.

Un&#39;esperienza può essere assemblata utilizzando più attività contemporaneamente. Attualmente, fino a 30 attività possono essere affrontate in un&#39;unica richiesta di decisione. Se più di 30 attività o slot in un&#39;esperienza devono essere riempiti di contenuto, è possibile effettuare più richieste per lo stesso profilo. Tuttavia, quando le attività sono incluse nella stessa richiesta di decisione, la deduplicazione delle proposte di offerta sarà effettuata tra tali attività.

Se le attività sono definite in un modo che selezionano tra i set di offerte disgiunti, non fa molta differenza se le attività vengono combinate nella stessa richiesta o suddivise in richieste separate. Tuttavia, i vincoli relativi ai tempi di rete e di risposta possono richiedere la combinazione di attività nella stessa richiesta. Poiché diverse richieste possono essere indirizzate a nodi di servizio diversi, potrebbe essere necessario recuperare gli stessi dati di profilo in nodi diversi. Questo riduce l&#39;effettiva larghezza di banda I/O disponibile per altre richieste.

Le attività vengono utilizzate per inserire il contenuto in un&#39;esperienza. Per facilitare (non garantire) la corretta inclusione degli elementi di contenuto, un&#39;attività fa riferimento a una singola posizione. Notate che un posizionamento non è sempre un luogo/slot in cemento ma più come un&#39;astrazione di quei luoghi/slot. Ad esempio, in una pagina Web con una griglia di sezioni ogni sezione potrebbe essere regolata dalla stessa posizione, purché abbia tutte una forma e una dimensione simili e possa contenere contenuto simile. Tuttavia, una singola sezione viene in genere fornita dalla propria attività.

La figura seguente illustra come le entità aziendali sono correlate tra loro:

![](./images/figure-10.png)

Quando i client creano e collegano il grafico degli oggetti per le decisioni, in genere ci saranno tre flussi di lavoro diversi. Si tratta dei seguenti elementi:

- Impostazione delle entità di supporto come tag e posizionamenti. Tali entità vengono utilizzate per strutturare, filtrare e raggruppare altre entità. Vengono inoltre utilizzati per fornire un certo coordinamento tra il secondo e il terzo flusso di lavoro. Questo flusso di lavoro costituisce un lavoro iniziale, ma in qualsiasi momento è possibile apportare dei miglioramenti alla configurazione. Anche se i tag sono relativamente semplici, i posizionamenti richiedono una pianificazione leggermente maggiore. Almeno un&#39;azienda deve fare un inventario di tutti i luoghi in cui viene presentata una decisione.

- Creazione di offerte con le varie rappresentazioni e regole aziendali (vincoli). Questo flusso di lavoro centrale offre le opzioni tra cui è necessario selezionare quelle migliori. I tag del primo flusso di lavoro vengono utilizzati per classificare le offerte e i posizionamenti indicano quali opzioni possono essere presentate e dove.

   - Questo flusso di lavoro definisce anche i vincoli assoluti per le offerte. Sono assoluti perché saranno sempre applicati e non influenzeranno solo la classifica tra una serie di offerte. Ad esempio, quando viene impostato un vincolo di calendario, l&#39;offerta non verrà mai selezionata prima della data/ora di inizio impostata e mai dopo la data/ora di fine. I vincoli che verranno impostati in questo flusso di lavoro sono i vincoli del [calendario](#calendar-constraints), i vincoli [di](#capping-constraints) limite massimo e i vincoli di [idoneità](#profile-constraints---eligibility-rules). Un flusso di lavoro secondario è la definizione di regole aggiuntive che determinano chi può ricevere una determinata offerta.

      - Contemporaneamente vengono creati vincoli per un&#39;offerta, vengono selezionate le relative rappresentazioni. Questo flusso di lavoro presuppone che il contenuto sia già stato creato da qualche parte e che sia semplicemente caricato e scelto dall&#39;archivio dei contenuti. Ecco dove vengono riprodotti i posizionamenti del primo flusso di lavoro. Un&#39;offerta può selezionare i posizionamenti e associare il contenuto sotto tale [posizione](#offer-placements).

      - La creazione di offerte di fallback adeguate è l&#39;ultimo passaggio di questo flusso di lavoro. Un&#39;offerta di fallback è molto simile a un&#39;offerta generale senza vincoli.

- L&#39;ultimo flusso di lavoro riguarda la creazione di attività. Tuttavia, questo passaggio non si verifica necessariamente in sequenza dopo il flusso di lavoro per la creazione delle offerte. Entrambi i processi sono in corso e simultanei. Le attività sono utilizzate per limitare l&#39;ambito delle opzioni per argomento e per luogo in cui vengono presentate le decisioni. Un&#39;attività fa riferimento a una [raccolta](#offer-collections) e a una posizione. Deve inoltre specificare un&#39;offerta [di](#fallback-offers) fallback utilizzata nei casi in cui non è possibile determinare un&#39;offerta di qualificazione.

