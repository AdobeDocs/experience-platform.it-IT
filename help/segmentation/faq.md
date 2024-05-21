---
title: Domande frequenti sui tipi di pubblico
description: Trova le risposte alle domande più frequenti su tipi di pubblico e altri concetti correlati alla segmentazione.
exl-id: 79d54105-a37d-43f7-adcb-97f2b8e4249c
source-git-commit: 6088dc06af6db2ce1a86a9638df23453184864b2
workflow-type: tm+mt
source-wordcount: '4056'
ht-degree: 0%

---

# Domande frequenti

Adobe Experience Platform [!DNL Segmentation Service] fornisce un’interfaccia utente e un’API RESTful che consente di creare tipi di pubblico tramite le definizioni dei segmenti o altre origini dal tuo [!DNL Real-Time Customer Profile] dati. Questi tipi di pubblico sono configurati e gestiti centralmente su Platform e sono facilmente accessibili da qualsiasi soluzione Adobe. Di seguito è riportato un elenco di domande frequenti relative a tipi di pubblico e segmentazione.

## Audience Portal

Nella sezione seguente sono elencate le domande relative ad Audience Portal.

### Posso accedere a Audience Portal e alla Composizione del pubblico?

Audience Portal e Audience Composition sono disponibili per tutti i clienti Real-Time CDP Prime e Ultimate (edizioni B2C, B2B e B2P) e per i clienti Journey Optimizer Select, Prime, Ultimate Starter e Ultimate.

Al momento, sono supportati solo i tipi di pubblico basati sul profilo. Il supporto per i tipi di pubblico basati sull’account verrà aggiunto in una versione successiva.

### Audience Portal supporta tipi di pubblico predefiniti generati esternamente?

Sì, i tipi di pubblico predefiniti generati esternamente sono supportati con Audience Portal. A questo punto puoi importare un pubblico generato esternamente tramite un file CSV. In futuro, potrai aggiungere tipi di pubblico tramite connettori di origine in batch o basati su streaming.

### Quali autorizzazioni devo avere per caricare i tipi di pubblico generati esternamente?

Per caricare tipi di pubblico generati esternamente, devi disporre delle autorizzazioni &quot;Visualizza segmenti&quot;, &quot;Gestisci segmenti&quot; e &quot;Importa tipi di pubblico&quot;. Non sono necessari controlli specifici basati sul ruolo per caricare tipi di pubblico generati esternamente.

### Cosa succede quando carico un pubblico generato esternamente?

Quando carichi un pubblico generato esternamente, vengono creati i seguenti elementi:

- Set di dati
   - Il set di dati sarà visibile all’interno dell’inventario dei set di dati e il nome del set di dati sarà **uguale** come nome del pubblico generato esternamente e caricato.
- Processo batch
   - Un processo batch **automaticamente** eseguito quando carichi un pubblico generato esternamente. Ciò significa che lo fai **non** per attivare il pubblico generato esternamente, devi attendere l’esecuzione del processo di segmentazione giornaliero.
- Schema ad hoc
   - A **nuovo** Lo schema XDM verrà creato per l’utilizzo con il pubblico generato esternamente. Ai campi in questo schema XDM viene assegnato un namespace per l’utilizzo con il set di dati creato a sua volta.

### Di cosa è composto un pubblico generato esternamente e cosa accade a questi dati quando vengono importati in Platform?

Durante il flusso di lavoro di importazione di un pubblico esterno, devi specificare quale colonna nel file CSV corrisponde al **Identità primaria**. Un esempio di identità primaria include l’indirizzo e-mail, l’ECID o uno spazio dei nomi di identità personalizzato specifico per l’organizzazione.

I dati associati a questa colonna di identità primaria sono **solo** dati allegati al profilo. Se non sono presenti profili corrispondenti ai dati nella colonna dell’identità primaria, viene creato un nuovo profilo. Tuttavia, questo profilo è essenzialmente un profilo orfano poiché **no** attributi o eventi di esperienza sono associati a questo profilo.

Vengono considerati tutti gli altri dati all’interno del pubblico generato esternamente **attributi payload**. Questi attributi possono **solo** essere utilizzati per la personalizzazione e l&#39;arricchimento durante l&#39;attivazione e sono **non** associato a un profilo. Tuttavia, questi attributi vengono memorizzati nel data lake.

Anche se è possibile fare riferimento al pubblico generato esternamente durante la creazione di tipi di pubblico utilizzando il Generatore di segmenti, i singoli attributi di profilo **non può** essere utilizzati.

### È possibile riconciliare i dati sul pubblico generato esternamente con un profilo esistente in Platform?

Sì, se gli identificatori primari corrispondono, il pubblico generato esternamente verrà unito al profilo esistente in Platform. La riconciliazione di questi dati può richiedere fino a 24 ore. Se i dati del profilo non esistono già, verrà creato un nuovo profilo durante l’acquisizione dei dati.

### Posso utilizzare un pubblico generato esternamente per creare altri tipi di pubblico?

Sì, qualsiasi pubblico generato esternamente verrà visualizzato nell’inventario del pubblico e può essere utilizzato per creare tipi di pubblico all’interno di [Generatore di segmenti](./ui/segment-builder.md).

### Posso utilizzare attributi caricati esternamente come parte della segmentazione?

No, non puoi. Gli attributi del profilo devono essere attributi di lunga durata, mentre i dati del pubblico generati esternamente e caricati contengono solo dati contestuali associati a quel pubblico generato esternamente.

I dati contestuali o attributi di arricchimento del pubblico generato esternamente sono **non** duraturo, in quanto il loro ciclo di vita è legato al pubblico caricato. Di conseguenza, data la sua natura transitoria, questi attributi di arricchimento sono **non** disponibile per l’utilizzo nella segmentazione.

Tuttavia, quando mappi i tipi di pubblico a destinazioni in batch o basate su file, puoi utilizzare questi attributi di arricchimento generati esternamente per migliorare i tipi di pubblico e ulteriori attivazioni a valle.

Per ulteriori informazioni su questa funzionalità, consulta la guida su [attivazione dei dati sul pubblico nelle destinazioni di esportazione del profilo batch](../destinations/ui/activate-batch-profile-destinations.md#mapping).

### Esiste un criterio di unione specifico per i tipi di pubblico generati esternamente?

Il criterio di unione predefinito specifico per l’organizzazione viene applicato automaticamente durante il caricamento di tipi di pubblico generati esternamente. Tuttavia, puoi modificare il criterio di unione applicato al pubblico generato esternamente durante il flusso di lavoro di importazione del pubblico.

### Dove posso attivare i tipi di pubblico generati esternamente in?

Un pubblico generato esternamente può essere mappato su qualsiasi destinazione RTCDP e può essere utilizzato nelle campagne Adobe Journey Optimizer.

### Quando saranno pronti per l’attivazione i tipi di pubblico generati esternamente?

Se attivati in una destinazione di streaming, i dati del pubblico generato esternamente saranno disponibili entro due ore.

Se attivati in una destinazione batch, i dati del pubblico generato esternamente verranno sincronizzati con il successivo processo di segmentazione di 24 ore.

### Posso eliminare un pubblico generato esternamente?

Sì! I tipi di pubblico generati esternamente possono essere eliminati in Audience Portal.

### Cosa devo fare se ho caricato accidentalmente un pubblico generato esternamente?

Se hai caricato accidentalmente un pubblico generato esternamente e desideri rimuovere i dati, puoi cancellare i profili associati al pubblico caricando un file CSV con una riga e senza dati.

### Per quanto tempo durano i tipi di pubblico generati esternamente?

La scadenza corrente dei dati per i tipi di pubblico generati esternamente è **30 giorni**. Questa scadenza dei dati è stata scelta per ridurre la quantità di dati in eccesso archiviati all’interno dell’organizzazione.

Al termine del periodo di scadenza dei dati, il set di dati associato sarà ancora visibile all’interno dell’inventario dei set di dati, ma **non** essere in grado di attivare il pubblico e il conteggio dei profili verrà visualizzato come zero.

### In che modo Audience Portal e Audience Composition interagiranno con il rilascio di Real-Time CDP Partner Data?

Audience Portal e Audience Composition interagiranno con i dati dei partner in due modi:

1. Se acquisisci un elenco di potenziali clienti fornito dal partner utilizzando la classe e il flusso di lavoro Prospect Profile, i potenziali clienti verranno mantenuti **separatamente** da unire i profili cliente in Profile Service. Di conseguenza, gli elenchi di potenziali clienti **non** sono disponibili in Audience Portal o in Audience Composition.
2. Se utilizzi gli attributi forniti dal partner per arricchire **esistente** profili di prime parti, tipi di pubblico arricchiti di dati dei partner **will** sono disponibili sia in Audience Portal che in Audience Composition.

### Come posso utilizzare attributi aggiuntivi con i miei tipi di pubblico?

Con i tipi di pubblico, ci sono **due** è possibile aggiungere diversi tipi di attributi aggiuntivi: attributi payload (contestuali) e attributi di arricchimento.

Gli attributi del payload sono attributi che vengono acquisiti come parte del caricamento CSV di un pubblico generato esternamente. Questi attributi sono **non** acquisito in Real-Time Customer Profile, ma può essere utilizzato come parte di una destinazione a valle.

Gli attributi di arricchimento sono attributi che provengono da un set di dati e sono uniti a un pubblico in Composizione pubblico. Al momento questi attributi possono essere utilizzati solo nelle campagne Adobe Journey Optimizer. Il supporto per i percorsi Adobe Journey Optimizer sarà presto disponibile, con il supporto per le destinazioni a valle in attesa della versione futura.

| Canale di attivazione | Tipi di pubblico da caricamento personalizzato CSV | Tipi di pubblico da Composizione pubblico |
| --- | --- | --- |
| Destinazioni Real-Time CDP | È possibile attivare sia gli attributi del payload che i tipi di pubblico. | È possibile attivare solo il pubblico. Attributi di arricchimento **non può** essere attivato. |
| Campagne Adobe Journey Optimizer | Non è possibile attivare né gli attributi del pubblico né quelli del payload. | È possibile attivare sia gli attributi di pubblico che quelli di arricchimento. |

## Stati del ciclo di vita {#lifecycle-states}

Nella sezione seguente sono elencate le domande relative agli stati del ciclo di vita e alla gestione dello stato del ciclo di vita all’interno di Audience Portal.

### Cosa rappresentano i diversi stati del ciclo di vita?

Il grafico seguente spiega i diversi stati del ciclo di vita, cosa rappresentano, dove è possibile utilizzare i tipi di pubblico con tale stato e quale impatto hanno sui guardrail di segmentazione.

| Stato | Definizione | Visibile in Audience Portal? | Visibile nelle destinazioni? | Influisce sui limiti di segmentazione? | Impatto sui tipi di pubblico basati su file | Impatto sulla valutazione del pubblico | Utilizzabile all’interno di altri tipi di pubblico? | Modificabile |
| --- | --- | --- | --- | --- | --- | --- | --- | -- |
| Bozza | Un pubblico in **Bozza** state è un pubblico che è ancora in fase di sviluppo e non è ancora pronto per essere utilizzato in altri servizi. | Sì, ma può essere nascosto. | No | Sì | Può essere importato o aggiornato durante il processo di ottimizzazione. | Può essere valutato per ottenere conteggi di pubblicazione precisi. | Sì, ma non è consigliabile utilizzarlo. | Sì |
| Pubblicato | Un pubblico in **Pubblicato** state è un pubblico pronto per l’uso in tutti i servizi a valle. | Sì | Sì | Sì | Può essere importato o aggiornato. | Valutato utilizzando la segmentazione batch, in streaming o edge. | Sì | Sì |
| Inattivo | Un pubblico in **Inattivo** lo stato è un pubblico che al momento non è in uso. Esiste ancora in Platform, ma **non** essere utilizzabile fino a quando non viene contrassegnato come bozza o pubblicato. | No, ma può essere visualizzato. | No | No | Non più aggiornato. | Non più valutato o aggiornato da Platform. | Sì | Sì |
| Eliminato | Un pubblico in **Eliminato** state è un pubblico che è stato eliminato. L’effettiva eliminazione dei dati potrebbe richiedere alcuni minuti. | No | No | No | I dati sottostanti vengono eliminati. | Al termine dell’eliminazione non viene eseguita alcuna valutazione o esecuzione dei dati. | No | No |

### In quali stati posso modificare i tipi di pubblico in?

I tipi di pubblico possono essere modificati nei seguenti stati del ciclo di vita:

- **Bozza**: se un pubblico viene modificato nello stato di bozza, rimane nello stato di bozza a meno che non venga esplicitamente pubblicato.
- **Pubblicato**: se un pubblico viene modificato nello stato di pubblicazione, rimane pubblicato e il pubblico viene aggiornato automaticamente.
- **Inattivo**: se un pubblico viene modificato nello stato inattivo, rimane inattivo. Ciò significa che non verrà valutato o aggiornato. Se devi aggiornare il pubblico, devi pubblicarlo.

Una volta eliminato un pubblico, **non può** essere modificata.

### In quali stati del ciclo di vita posso spostare un pubblico?

I possibili stati del ciclo di vita in cui un pubblico può essere spostato dipendono dallo stato corrente del pubblico.

![Un diagramma che illustra le possibili transizioni dello stato del ciclo di vita disponibili per i tipi di pubblico.](./images/faq/lifecycle-state-transition.png)

Se il pubblico è in stato di bozza, puoi pubblicarlo o eliminarlo se non ha dipendenti.

Se il pubblico è in stato pubblicato, puoi disattivarlo o eliminarlo se non ha dipendenti.

Se il pubblico è inattivo, puoi ripubblicarlo o eliminarlo se non ha dipendenti.

### Esistono avvertenze per i tipi di pubblico in alcuni stati del ciclo di vita?

I tipi di pubblico con stato di pubblicazione possono essere spostati in un altro stato solo se il pubblico lo fa **non** ha qualsiasi familiare a carico. Ciò significa che se il pubblico viene utilizzato in un servizio a valle, non può essere disattivato o eliminato.

Se un pubblico valutato tramite la segmentazione in batch viene ripubblicato, ossia quando un pubblico passa da inattivo a pubblicato, il pubblico viene aggiornato **dopo** il processo batch giornaliero. Quando viene ripubblicato per la prima volta, i profili e i dati saranno **uguale** come quando il pubblico è stato reso inattivo.

### Come si inserisce un pubblico nello stato di bozza?

Il metodo per inserire un pubblico nello stato di bozza dipende dall’origine del pubblico.

Per i tipi di pubblico creati con Segment Builder (Generatore di segmenti), puoi impostare il pubblico sullo stato Bozza selezionando &quot;[!UICONTROL Salva come bozza]&quot; nel Generatore di segmenti.

Per i tipi di pubblico creati in Composizione pubblico, i tipi di pubblico vengono salvati automaticamente come bozza fino alla pubblicazione.

Per i tipi di pubblico creati esternamente, i tipi di pubblico vengono pubblicati automaticamente.

Quando un pubblico si trova nello stato pubblicato, **non può** riporta il pubblico originale allo stato di bozza. Tuttavia, se copi il pubblico, quello appena copiato sarà in stato di bozza.

### Come si mette un pubblico nello stato pubblicato?

Per i tipi di pubblico creati con il Generatore di segmenti o la Composizione del pubblico, puoi impostare il pubblico sullo stato pubblicato selezionando &quot;[!UICONTROL Pubblica]&quot; nelle rispettive interfacce utente.

I tipi di pubblico creati esternamente vengono automaticamente impostati su pubblicato.

### Come si mette un pubblico in stato inattivo?

Per rendere inattivo un pubblico pubblicato, apri il menu Azioni rapide in Audience Portal e seleziona &quot;[!UICONTROL Disattiva]&quot;.

### Come si ripubblica un pubblico?

>[!NOTE]
>
>Lo stato &quot;ripubblicato&quot; è lo stesso dello stato pubblicato per il comportamento del pubblico.

Puoi ripubblicare un pubblico selezionando un pubblico che si trova nello stato inattivo, aprendo il menu Azioni rapide in Audience Portal e selezionando [!UICONTROL Pubblica].

### Come posso impostare un pubblico come eliminato?

>[!IMPORTANT]
>
>Puoi eliminare solo i tipi di pubblico che sono **non** utilizzato in qualsiasi attivazione a valle. Inoltre, non puoi eliminare un pubblico a cui viene fatto riferimento in un altro pubblico. Se non puoi eliminare il pubblico, assicurati di **non** utilizzarlo in qualsiasi servizio a valle o come elemento costitutivo di un altro pubblico.

Puoi impostare un pubblico in stato di eliminazione aprendo il menu Azioni rapide in Audience Portal e selezionando [!UICONTROL Elimina].

### Esistono avvertenze per le transizioni dello stato del ciclo di vita?

Sì, è necessario prestare attenzione ad alcune avvertenze che si verificano quando si utilizzano tipi di pubblico nei servizi a valle, come Adobe Journey Optimizer, o tipi di pubblico non basati sul cliente, come i tipi di pubblico basati sull’account.

In questo momento, **deve** verifica manualmente se il pubblico viene utilizzato a valle in Adobe Journey Optimizer, in quanto questo stato non è attualmente controllato automaticamente.

Inoltre, puoi **deve** controlla manualmente se il pubblico viene utilizzato come componente di un pubblico basato sull’account, poiché anche questo stato non viene attualmente controllato automaticamente.

### L’utilizzo di un pubblico come pubblico secondario influisce sulle transizioni dello stato del ciclo di vita?

>[!NOTE]
>
>Un pubblico principale è un pubblico che **utilizza** un altro pubblico come dipendenza per il pubblico.
>
>Un pubblico secondario è un pubblico che **utilizzato come** una dipendenza per il pubblico.

Sì, l’utilizzo di un pubblico come pubblico secondario influisce sugli stati del ciclo di vita che il pubblico secondario e quello principale possono intraprendere.

Per spostare un pubblico secondario allo stato pubblicato, tutto il pubblico principale **deve** essere in stato di pubblicazione. I tipi di pubblico principali possono essere pubblicati prima della pubblicazione del pubblico secondario oppure, se l’utente conferma, possono essere pubblicati automaticamente al momento della pubblicazione del pubblico secondario.

Per spostare il pubblico principale allo stato inattivo o eliminato, tutti i relativi tipi di pubblico secondari **deve** essere disattivate o eliminate.

### Posso fare riferimento a un pubblico che si trova in uno stato del ciclo di vita diverso?

Sì! Se il pubblico è attualmente in stato di bozza, puoi fare riferimento a tipi di pubblico in stato pubblicato o inattivo. Tuttavia, per pubblicare questo pubblico, **deve** pubblica gli altri tipi di pubblico principali.

## Inventario del pubblico

Nella sezione seguente sono elencate le domande relative all’inventario del pubblico all’interno di Audience Portal.

### Sono necessarie autorizzazioni aggiuntive per utilizzare le funzioni di inventario del pubblico?

No, non è vero. Se disponi delle autorizzazioni di modifica per i tipi di pubblico, potrai creare, aggiornare e gestire le cartelle e i tag nel Portale pubblico. Per ulteriori informazioni sulla gestione delle autorizzazioni, consulta [guida alla gestione delle autorizzazioni](../access-control/ui/permissions.md).

### Esiste un limite al numero di cartelle che è possibile creare?

No, non esiste alcun limite al numero di cartelle che è possibile creare. Per ulteriori informazioni sulle cartelle, leggere [sezione audience inventory](./ui/overview.md#folders) della panoramica dell’interfaccia utente del servizio di segmentazione.

### Esiste un limite al numero di tag che possono essere aggiunti a un pubblico?

No, non esiste alcun limite al numero di tag che possono essere aggiunti a un pubblico. Per ulteriori informazioni sui tag, consulta [sezione audience inventory](./ui/overview.md#tags) della panoramica dell’interfaccia utente del servizio di segmentazione.

### Esiste un limite al numero di tag che è possibile creare?

No, non esiste alcun limite al numero di tag che è possibile creare. Tuttavia, puoi creare un massimo di **100** categorie da applicare per i tag. Per ulteriori informazioni sulla gestione dei tag, consulta [Guida alla gestione dei tag](../administrative-tags/ui/managing-tags.md).

### Quando si cerca un pubblico per nome o per tag in una cartella principale, è possibile eseguire ricerche anche nelle cartelle secondarie correlate?

No, questo comportamento non è supportato. Tuttavia, puoi modificare la visualizzazione dell’inventario del pubblico in modo da esaminare **Tutti i tipi di pubblico**, quindi esegui la ricerca in tutte le cartelle. Per ulteriori informazioni sull’utilizzo della ricerca nell’inventario del pubblico, consulta la sezione [sezione di ricerca](./ui/overview.md#search) della panoramica dell’interfaccia utente del servizio di segmentazione.

### È possibile assegnare automaticamente un pubblico a una cartella al momento della creazione?

A questo punto, no. Tuttavia, questa funzionalità potrebbe essere disponibile in futuro.

### È possibile spostare più tipi di pubblico in una cartella contemporaneamente?

A questo punto, no. Tuttavia, questa funzionalità potrebbe essere disponibile in futuro.

## Composizione del pubblico

Nella sezione seguente sono elencate le domande relative alla composizione del pubblico.

### Quando dovrei usare la composizione del pubblico invece di usare il Generatore di segmenti?

Sia Audience Composition che Segment Builder hanno ruoli importanti nella creazione di tipi di pubblico in Platform.

Il Generatore di segmenti è più adatto al pubblico **creazione** (per creare un pubblico da zero), mentre la Composizione del pubblico è più adatta per il pubblico **cura e personalizzazione** (per creare nuovi tipi di pubblico in base a un pubblico esistente).

La tabella seguente illustra la differenza tra i due servizi:

| Generatore di segmenti | Composizione del pubblico |
| --------------- | -------------------- |
| <ul><li>Generazione di pubblico in un’unica fase</li><li>Crea i blocchi di base di tipi di pubblico da dati di profilo, serie temporali e più entità</li><li>Utilizzato per creare **uno** pubblico</li></ul> | <ul><li>Generazione di tipi di pubblico in più fasi tramite operazioni basate su set</li><li>Utilizza i tipi di pubblico creati dal Generatore di segmenti e applica opzioni di arricchimento dei dati, come la classificazione degli attributi del profilo e la suddivisione in tipi di pubblico secondari</li><li>Utilizzato per creare **multiplo** tipi di pubblico contemporaneamente</li></ul> |

Per ulteriori informazioni sul Generatore di segmenti, leggi [Guida al Generatore di segmenti](./ui/segment-builder.md). Per ulteriori informazioni sulla composizione del pubblico, leggi [Guida alla composizione del pubblico](./ui/audience-composition.md).

### Posso utilizzare tipi di pubblico generati esternamente in Composizione pubblico?

A questo punto, no. Tuttavia, questa funzionalità dovrebbe essere disponibile a breve.

### Posso inviare tipi di pubblico da Audience Composition a tutte le destinazioni e i canali a valle?

A questo punto, no. Attualmente, puoi utilizzare i tipi di pubblico da Composizione pubblico nelle campagne Adobe Journey Optimizer e nelle destinazioni Real-Time CDP. I Percorsi Adobe Journey Optimizer saranno supportati in una versione futura.

### Ci sono dei guardrail sul numero di composizioni?

In questo momento, è possibile avere solo **10** composizioni pubblicate per sandbox. Questo guardrail verrà incrementato in una versione futura.

### Quali sono i guardrail del flusso di lavoro per Audience Composition?

Il posizionamento del componente di composizione segue una struttura rigida come segue:

1. Tu **sempre** inizia con [!UICONTROL Pubblico] blocca per selezionare l’attività iniziale. Puoi avere un massimo di **uno** [!UICONTROL Pubblico] blocco.
2. Facoltativamente, puoi aggiungere una [!UICONTROL Escludi] blocco che segue il [!UICONTROL Pubblico] blocco.
3. Facoltativamente, puoi aggiungere una [!UICONTROL Arricchire] blocco che segue il [!UICONTROL Escludi] blocco. È possibile utilizzare solo **uno** [!UICONTROL Arricchire] blocco per composizione.
4. Facoltativamente, puoi aggiungere una [!UICONTROL Classifica] o [!UICONTROL Dividi] blocco. È possibile **solo** avere uno di questi blocchi per composizione.
5. Tu **sempre** termina con [!UICONTROL Salva] blocca per salvare il pubblico.

Inoltre, le seguenti restrizioni(?) applica quando si utilizzano questi blocchi:

- Dividi blocco
   - Questo blocco supporta solo **Stringa** tipi di dati. Il blocco di suddivisione **non** supportano il tipo di dati date o boolean.
   - Inoltre, questo blocco **non** supportano gli attributi di arricchimento.
- Escludi blocco
   - Questo blocco non **non** supportano il tipo di dati date o boolean.
- Blocco della classificazione
   - Questo blocco non **non** supportano gli attributi di arricchimento.

Per ulteriori dettagli sull’utilizzo di Audience Composition, consulta la sezione [Guida dell’interfaccia utente di Audience Composition](./ui/audience-composition.md).

### Quando vengono salvati e valutati i tipi di pubblico creati con Composizione pubblico?

I tipi di pubblico vengono salvati automaticamente durante la loro creazione in Composizione pubblico. L’ora di creazione del pubblico sarà la prima volta che si verifica questo salvataggio automatico.

Una volta creato il pubblico, la sua valutazione può richiedere fino a 24 ore.

### Quando posso utilizzare il pubblico che ho creato?

Il pubblico creato in Composizione pubblico **immediatamente** viene visualizzato in Audience Portal. Tuttavia, per utilizzarlo in Adobe Journey Optimizer, è necessario attendere almeno 24 ore dopo la valutazione.

### I processi di valutazione sono visibili nella sezione di monitoraggio?

Al momento, i processi di valutazione sono **non** visualizzato nell’interfaccia utente di monitoraggio.

### Posso utilizzare una composizione di pubblico in un&#39;altra composizione?

No, i tipi di pubblico sono stati creati utilizzando la composizione del pubblico **non può** essere utilizzato come input in un’altra composizione di pubblico.

### Come funziona la suddivisione in Audience Composition?

La suddivisione del pubblico consente di suddividere ulteriormente il pubblico in gruppi più piccoli.

La suddivisione per attributo comporta l&#39;esclusività reciproca tra i gruppi. Ciò significa che se un record soddisfa i criteri di più percorsi di suddivisione, gli verrà assegnato il **primo** percorso da sinistra e **non** assegnati a uno qualsiasi degli altri percorsi.

Quando si suddivide in percentuale, le suddivisioni sono **in modo casuale** completato. Ciò significa che i profili verranno assegnati in modo casuale a ciascun percorso. La divisione è **non** persistente, in modo che il profilo possa trovarsi in un pubblico secondario diverso a ogni valutazione.

Per ulteriori informazioni sul blocco Split, leggi [Guida dell’interfaccia utente di Audience Composition](./ui/audience-composition.md#split).

### Posso utilizzare tutti i tipi di segmentazione nel flusso di lavoro Composizione pubblico?

Sì, tutti i tipi di segmentazione ([segmentazione batch, segmentazione in streaming e segmentazione Edge](./home.md#evaluate-segments)) sono supportate nel flusso di lavoro Composizione pubblico. Tuttavia, poiché le composizioni vengono attualmente eseguite solo una volta al giorno, anche se sono inclusi i tipi di pubblico valutati in streaming o edge, il risultato sarà basato sull’iscrizione al pubblico al momento dell’esecuzione della composizione.

## Iscrizione al pubblico

Nella sezione seguente sono elencate le domande relative all’iscrizione al pubblico.

### Come posso confermare l’appartenenza di un profilo a un pubblico?

Per confermare l’iscrizione al pubblico di un profilo, visita la pagina dei dettagli del profilo che desideri confermare. Seleziona **[!UICONTROL Attributi]**, seguito da **[!UICONTROL Visualizza JSON]** e confermare che il `segmentMembership` L’oggetto contiene l’ID del pubblico.

### In che modo la segmentazione batch risolve l’appartenenza al profilo?

I tipi di pubblico valutati utilizzando la segmentazione in batch si risolvono quotidianamente, registrando i risultati dell’iscrizione al pubblico nel `segmentMembership` attributo. Le ricerche di profilo generano una nuova versione del profilo al momento della ricerca, ma ciò accade **non** aggiorna i risultati della segmentazione batch.

Di conseguenza, quando vengono apportate modifiche al profilo, ad esempio l’unione di due profili, tali modifiche **will** nel profilo quando viene cercato, ma **non** essere riflessi nel `segmentMembership` finché il processo di valutazione del segmento non viene eseguito nuovamente.

Ad esempio, supponiamo che tu abbia creato due tipi di pubblico reciprocamente esclusivi: il pubblico A è per le persone che vivono a Washington e il pubblico B è per le persone che lo fanno **non** vive a Washington. Ci sono due profili: il profilo 1 per una persona che vive a Washington e il profilo 2 per una persona che vive in Oregon.

Quando viene eseguito il processo di valutazione della segmentazione batch, il profilo 1 passa al pubblico A, mentre il profilo 2 passa al pubblico B. Successivamente, ma prima dell’esecuzione del processo di valutazione della segmentazione batch del giorno successivo, entra in Platform un evento che riconcilia i due profili. Di conseguenza, viene creato un singolo profilo unito contenente i profili 1 e 2.

Fino all’esecuzione del successivo processo di valutazione del segmento batch, il nuovo profilo unito avrà l’iscrizione al pubblico in **entrambi** profilo 1 e profilo 2. Di conseguenza, questo significa che sarà membro di **entrambi** Pubblico A e Pubblico B, nonostante il fatto che questi tipi di pubblico abbiano definizioni contraddittorie. Per l’utente finale, è il **identica situazione** come prima i profili erano collegati, poiché c’era sempre solo l’unica persona coinvolta, e Platform lo ha appena fatto **non** disporre di informazioni sufficienti per collegare i due profili.

Se utilizzi la ricerca dei profili per recuperare il nuovo profilo creato e osservarne l’iscrizione al pubblico, questo dimostrerà che è un membro di **entrambi** Pubblico A e Pubblico B, nonostante il fatto che entrambi questi tipi di pubblico abbiano definizioni contraddittorie. Una volta eseguito il processo di valutazione della segmentazione batch giornaliera, l’iscrizione al pubblico verrà aggiornata per riflettere questo stato aggiornato dei dati del profilo.

Se hai bisogno di una risoluzione del pubblico in tempo reale, utilizza lo streaming o la segmentazione Edge.

### Quanto tempo ci vuole affinché i dati in streaming siano disponibili nei flussi di lavoro di segmentazione batch?

Potrebbero essere necessarie fino a tre ore per la disponibilità dei dati in streaming nei flussi di lavoro di segmentazione batch.

Ad esempio, se un processo di segmentazione batch viene eseguito alle 21:00, può contenere anche dati acquisiti in streaming **fino a** 18:00. Streaming dei dati acquisiti che sono stati acquisiti dopo le 18 ma prima delle 21 **maggio** essere inclusi.

