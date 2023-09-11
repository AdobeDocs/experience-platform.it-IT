---
title: Domande frequenti sui tipi di pubblico
description: Trova le risposte alle domande più frequenti su tipi di pubblico e altri concetti correlati alla segmentazione.
source-git-commit: 9a72d85bfb592012b36826135e24d28983f92e40
workflow-type: tm+mt
source-wordcount: '1935'
ht-degree: 1%

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

### È possibile riconciliare i dati sul pubblico generato esternamente con un profilo esistente in Platform?

Sì, se gli identificatori primari corrispondono, il pubblico generato esternamente verrà unito al profilo esistente in Platform. La riconciliazione di questi dati può richiedere fino a 24 ore. Se i dati del profilo non esistono già, verrà creato un nuovo profilo durante l’acquisizione dei dati.

## Posso utilizzare un pubblico generato esternamente per creare altri tipi di pubblico?

Sì, qualsiasi pubblico generato esternamente verrà visualizzato nell’inventario del pubblico e può essere utilizzato per creare tipi di pubblico all’interno di [Generatore di segmenti](./ui/segment-builder.md).

### Posso utilizzare attributi caricati esternamente come parte della segmentazione?

No, non puoi. Gli attributi del profilo devono essere attributi di lunga durata, mentre i dati del pubblico generati esternamente e caricati contengono solo dati contestuali associati a quel pubblico generato esternamente.

I dati contestuali o attributi di arricchimento del pubblico generato esternamente sono **non** duraturo, in quanto il loro ciclo di vita è legato al pubblico caricato. Di conseguenza, data la sua natura transitoria, questi attributi di arricchimento sono **non** disponibile per l’utilizzo nella segmentazione.

Tuttavia, quando mappi i tipi di pubblico a destinazioni in batch o basate su file, puoi utilizzare questi attributi di arricchimento generati esternamente per migliorare i tipi di pubblico e ulteriori attivazioni a valle.

Per ulteriori informazioni su questa funzionalità, consulta la guida su [attivazione dei dati sul pubblico nelle destinazioni di esportazione del profilo batch](../destinations/ui/activate-batch-profile-destinations.md#mapping).

### Posso attivare pubblici generati esternamente in Adobe Journey Optimizer?

A questo punto, no. Tuttavia, questa funzionalità sarà disponibile a breve.

### Posso eliminare un pubblico generato esternamente?

A questo punto, no. Al suo posto, puoi disattivare o archiviare questo pubblico. In questo stato, i profili **will** rimane attivo per l’utilizzo in applicazioni a valle. Il supporto per l’eliminazione dei tipi di pubblico generati esternamente verrà aggiunto in una versione successiva.

### Cosa rappresentano i diversi stati del ciclo di vita?

Il grafico seguente spiega i diversi stati del ciclo di vita, cosa rappresentano, dove è possibile utilizzare i tipi di pubblico con tale stato e quale impatto hanno sui guardrail di segmentazione.

| Stato | Definizione | Visibile in Audience Portal? | Visibile nelle destinazioni? | Influisce sui limiti di segmentazione? | Impatto sui tipi di pubblico basati su file | Impatto sulla valutazione del pubblico | Utilizzabile all’interno di altri tipi di pubblico? |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Bozza | Un pubblico in **Bozza** state è un pubblico che è ancora in fase di sviluppo e non è ancora pronto per essere utilizzato in altri servizi. | Sì, ma può essere nascosto. | No | Sì | Può essere importato o aggiornato durante il processo di ottimizzazione. | Può essere valutato per ottenere conteggi di pubblicazione precisi. | Sì, ma non è consigliabile utilizzarlo. |
| Data di pubblicazione | Un pubblico in **Pubblicato** state è un pubblico pronto per l’uso in tutti i servizi a valle. | Sì | Sì | Sì | Può essere importato o aggiornato. | Valutato utilizzando la segmentazione batch, in streaming o edge. | Sì |
| Inattivo | Un pubblico in **Inattivo** lo stato è un pubblico che al momento non è in uso. Esiste ancora in Platform, ma **non** essere utilizzabile fino a quando non viene contrassegnato come bozza o pubblicato. | No, ma può essere visualizzato. | No | No | No più aggiornato. | Non più valutato o aggiornato da Platform. | Sì |
| Eliminato | Un pubblico in **Eliminato** state è un pubblico che è stato eliminato. L’effettiva eliminazione dei dati potrebbe richiedere alcuni minuti. | No | No | No | I dati sottostanti vengono eliminati. | Al termine dell’eliminazione non viene eseguita alcuna valutazione o esecuzione dei dati. | No |

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

## Inventario del pubblico

Nelle sezioni seguenti sono elencate le domande relative all’inventario del pubblico all’interno di Audience Portal.

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

Il Generatore di segmenti è più adatto al pubblico **creazione** (per creare un pubblico da zero), mentre la Composizione del pubblico è più adatta per il pubblico **cura** (per creare nuovi tipi di pubblico in base a un pubblico esistente).

La tabella seguente illustra la differenza tra i due servizi:

| Generatore di segmenti | Composizione del pubblico |
| --------------- | -------------------- |
| <ul><li>Generazione di pubblico in un’unica fase</li><li>Crea i blocchi di base di tipi di pubblico da dati di profilo, serie temporali e più entità</li><li>Utilizzato per creare **uno** pubblico</li></ul> | <ul><li>Generazione di tipi di pubblico in più fasi tramite operazioni basate su set</li><li>Utilizza i tipi di pubblico creati dal Generatore di segmenti e applica opzioni di arricchimento dei dati come la classificazione degli attributi del profilo</li><li>Utilizzato per creare **multiplo** tipi di pubblico contemporaneamente</li></ul> |

Per ulteriori informazioni sul Generatore di segmenti, leggi [Guida al Generatore di segmenti](./ui/segment-builder.md). Per ulteriori informazioni sulla composizione del pubblico, leggi [Guida alla composizione del pubblico](./ui/audience-composition.md).

### Posso utilizzare tipi di pubblico generati esternamente in Composizione pubblico?

A questo punto, no. Tuttavia, questa funzionalità dovrebbe essere disponibile a breve.

### Posso inviare tipi di pubblico da Audience Composition a tutte le destinazioni e i canali a valle?

A questo punto, no. Attualmente, puoi utilizzare i tipi di pubblico da Composizione pubblico in Campagne Adobe Journey Optimizer e destinazioni di Real-time CDP. I Percorsi Adobe Journey Optimizer saranno supportati in una versione futura.

### Ci sono dei guardrail sul numero di composizioni?

In questo momento, è possibile avere solo **10** composizioni pubblicate per sandbox. Questo guardrail verrà incrementato in una versione futura.

### Quali sono i guardrail del flusso di lavoro per Audience Composition?

Il posizionamento del componente di composizione segue una struttura rigida come segue:

1. Tu **sempre** inizia con [!UICONTROL Pubblico] blocca per selezionare l’attività iniziale. Puoi avere un massimo di **uno** [!UICONTROL Pubblico] blocco.
2. Facoltativamente, puoi aggiungere una [!UICONTROL Escludi] blocco che segue il [!UICONTROL Pubblico] blocco.
3. Facoltativamente, puoi aggiungere una [!UICONTROL Arricchire] blocco che segue il [!UICONTROL Escludi] blocco.
4. Facoltativamente, puoi aggiungere una [!UICONTROL Classifica] o [!UICONTROL Dividi] blocco. È possibile **solo** avere uno di questi blocchi per composizione.
5. Tu **sempre** termina con [!UICONTROL Salva] blocca per salvare il pubblico.

Per ulteriori dettagli sull’utilizzo di Audience Composition, consulta la sezione [Guida dell’interfaccia utente di Audience Composition](./ui/audience-composition.md).

### Posso utilizzare una composizione di pubblico in un&#39;altra composizione?

No, i tipi di pubblico sono stati creati utilizzando la composizione del pubblico **non può** essere utilizzato come input in un’altra composizione di pubblico.

### Come funziona la suddivisione in Audience Composition?

La suddivisione del pubblico consente di suddividere ulteriormente il pubblico in gruppi più piccoli. Questa divisione forza l&#39;esclusività reciproca tra i gruppi. Ciò significa che se un record soddisfa i criteri di più percorsi di suddivisione, gli verrà assegnato il **primo** percorso da sinistra e **non** assegnati a uno qualsiasi degli altri percorsi.

Per ulteriori informazioni sul blocco Split, leggi [Guida dell’interfaccia utente di Audience Composition](./ui/audience-composition.md#split).

### Posso utilizzare tutti i tipi di segmentazione nel flusso di lavoro Composizione pubblico?

Sì, tutti i tipi di segmentazione ([segmentazione batch, segmentazione in streaming e segmentazione Edge](./home.md#evaluate-segments)) sono supportate nel flusso di lavoro Composizione pubblico. Tuttavia, poiché le composizioni vengono attualmente eseguite solo una volta al giorno, anche se sono inclusi i tipi di pubblico valutati in streaming o edge, il risultato sarà basato sull’iscrizione al pubblico al momento dell’esecuzione della composizione.

## Come posso confermare l’appartenenza di un profilo a un pubblico?

Per confermare l’iscrizione al pubblico di un profilo, visita la pagina dei dettagli del profilo che desideri confermare. Seleziona **[!UICONTROL Attributi]**, seguito da **[!UICONTROL Visualizza JSON]** e confermare che il `segmentMembership` L’oggetto contiene l’ID del pubblico.
