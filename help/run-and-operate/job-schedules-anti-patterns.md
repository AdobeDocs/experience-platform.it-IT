---
description: Scopri come identificare e risolvere gli anti-pattern comuni di configurazione della pianificazione dei processi in Adobe Experience Platform.
solution: Experience Platform
title: Identificare gli anti-pattern di pianificazione processo
type: Tutorial
hide: true
source-git-commit: 9d170fec9b80f0f2e17fc39e8f573cbad515f823
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 0%

---


# Identificare gli anti-pattern per la pianificazione dei processi

>[!AVAILABILITY]
>
>[!UICONTROL Job schedules] sono attualmente disponibili come versione limitata e solo per i seguenti processi Real-Time CDP:
>
> * Acquisizione di un data lake batch
> * Acquisizione profilo batch
> * Segmentazione batch
> * Attivazione della destinazione batch.

La visualizzazione della timeline [Pianificazioni processi](job-schedules.md) consente di identificare i problemi di configurazione comuni che possono influire negativamente sulle prestazioni e sull&#39;affidabilità della pipeline dei dati. Questi anti-pattern spesso causano errori di lavoro, incoerenze nei dati o prestazioni del sistema ridotte. Individuando questi modelli in anticipo, è possibile riconfigurare i processi per evitare problemi prima che influiscano sulle operazioni aziendali.

## Prerequisiti {#prerequisites}

Prima di identificare gli anti-pattern, è necessario:

* Accedi a [!UICONTROL Job Schedules] con l&#39;autorizzazione **[!UICONTROL View Job Schedules]** [per il controllo degli accessi](/help/access-control/home.md#permissions).
* Conoscere l&#39;interfaccia [Pianificazioni processi](job-schedules.md#understanding-interface) e leggere la visualizzazione della sequenza temporale.
* Comprendere i concetti di base di [acquisizione batch](../ingestion/batch-ingestion/overview.md), [segmentazione](../segmentation/home.md) e [elaborazione profilo](../profile/home.md).

## Riferimento rapido {#anti-pattern-quick-reference}

| Anti-pattern | Cosa visualizzerai sulla timeline | Impatto primario | Gravità |
|--------------|----------------------------------|----------------|----------|
| [Sovrapposizione pianificazione](#schedule-overlap-pattern) | Più processi in esecuzione simultaneamente | Conflitti di risorse ed errori di processo | Alto |
| [Densità processi pianificata](#scheduled-density) | Molti set di dati con batch raggruppati nella stessa ora | Colli di bottiglia della pipeline e segmentazione incompleta | Alto |
| [Batch eccessivi per set di dati](#excessive-batches-per-dataset) | Set di dati singolo con decine di batch giornalieri | Elaborazione inefficiente e complessità operativa | Canale |

## Sovrapposizione pianificazione {#schedule-overlap-pattern}

**Gravità impatto**: elevata | **Problema principale**: conflitto di risorse

**Cosa cercare**: più processi pianificati per l&#39;esecuzione simultanea o in stretta successione, in particolare quando si sovrappongono processi che richiedono molte risorse.

In questo esempio, puoi vedere i processi di acquisizione batch in esecuzione contemporaneamente a un processo di segmentazione pianificato. Ciò crea conflitti di risorse perché entrambe le operazioni richiedono una notevole potenza di elaborazione e memoria.

**Perché questo è problematico**:

* **Conflitto di risorse**: quando vengono eseguiti contemporaneamente più processi che richiedono un uso intensivo delle risorse, questi sono in competizione per le risorse di sistema (CPU, memoria, I/O), rallentando l&#39;esecuzione di tutti i processi.
* **Prestazioni imprevedibili**: la durata del processo diventa incoerente, rendendo difficile la pianificazione di pianificazioni affidabili.
* **Ritardi a cascata**: se i processi richiedono più tempo del previsto, possono ritardare i processi dipendenti a valle, creando un effetto increspatura in tutta la pipeline.
* **Maggiore rischio di errore**: l&#39;esaurimento delle risorse può causare il timeout o il fallimento completo dei processi.

**Come correggerlo**:

* **Pianificazioni processi scaglionati**: garantire l&#39;esecuzione sequenziale delle operazioni che richiedono un uso intensivo delle risorse anziché simultanea.
* **Aggiungi tempo buffer**: lascia una spaziatura adeguata tra i processi per tenere conto dell&#39;elaborazione delle varianti.
* **Verifica dipendenze**: identifica quali processi devono essere completati prima che gli altri possano iniziare in modo sicuro.

## Densità di lavoro programmata {#scheduled-density}

**Gravità impatto**: elevata | **Problema primario**: colli di bottiglia della pipeline

**Cosa cercare**: troppi set di dati con più batch pianificati nella stessa ora, in particolare quando questi batch sono impilati vicini tra loro e pianificati in prossimità di finestre di elaborazione critiche, come gli orari di inizio della segmentazione.

In questo modello, vengono visualizzati i seguenti elementi:

* Più set di dati ciascuno con più batch al giorno
* Processi ETL (acquisizione di data lake e acquisizione di profili) raggruppati nella stessa ora
* Acquisizione in batch programmata immediatamente prima o durante le finestre di segmentazione pianificate

**Perché questo è problematico**:

* **Collo di bottiglia della pipeline**: quando numerosi batch di set di dati diversi vengono impilati in un breve intervallo di tempo, si crea un collo di bottiglia di elaborazione che può sopraffare la pipeline di acquisizione.
* **Disponibilità ritardata del profilo**: i processi di acquisizione del profilo troppo vicini a orari di inizio segmentazione potrebbero non essere completati in tempo, causando valutazioni del pubblico incomplete o non aggiornate.
* **Segmentazione imprevedibile**: se i processi di acquisizione a monte sono ancora in esecuzione all&#39;inizio della segmentazione, si rischia di valutare i tipi di pubblico rispetto a dati incompleti, con conseguente iscrizione errata al pubblico.
* **Errori a cascata**: un singolo batch ritardato in una pianificazione ad alta densità può causare un effetto domino, ritardando tutti i batch e i processi a valle successivi.
* **Vincolo risorse**: il sistema potrebbe avere difficoltà ad allocare risorse sufficienti durante l&#39;elaborazione di troppi processi di acquisizione simultanei, rallentando i tempi di elaborazione o causando errori.

**Come correggerlo**:

* **Consolidare i batch**: ridurre la frequenza dei batch combinando più batch di piccole dimensioni in un numero minore di batch più grandi per set di dati.
* **Distribuisci uniformemente**: distribuisci i processi di acquisizione nell&#39;arco della giornata anziché raggrupparli in ore specifiche.
* **Aggiungi tempo buffer**: assicurati che siano trascorse almeno 1-2 ore tra il completamento dell&#39;acquisizione del profilo e l&#39;inizio della segmentazione.
* **Verifica requisiti**: valuta se tutti i set di dati necessitano effettivamente di più batch giornalieri. Molti casi d&#39;uso funzionano con aggiornamenti meno frequenti.

## Batch eccessivi per set di dati {#excessive-batches-per-dataset}

**Gravità impatto**: Medium | **Problema principale**: elaborazione inefficiente

**Cosa cercare**: un singolo set di dati con un numero eccessivo di singoli processi batch pianificati nel corso della giornata, creando una lunga serie verticale di processi sulla timeline.

In questo modello, viene visualizzata una riga di set di dati con molti processi di acquisizione batch singoli pianificati a intervalli frequenti, a volte decine di batch al giorno per un singolo set di dati.

**Perché questo è problematico**:

* **Elaborazione inefficiente**: ogni processo batch ha costi comuni (inizializzazione, convalida, aggiornamenti metadati). L&#39;elaborazione di molti batch di piccole dimensioni è notevolmente meno efficiente rispetto all&#39;elaborazione di un numero inferiore di batch di grandi dimensioni.
* **Superficie di errore aumentata**: più processi significano più opportunità di errore. Ogni batch che non va a buon fine richiede un&#39;analisi e una potenziale rielaborazione.
* **Carico di sistema non necessario**: i batch di piccole dimensioni spesso mantengono il sistema costantemente occupato con le attività di overhead anziché con l&#39;elaborazione effettiva dei dati, riducendo il throughput complessivo.
* **Disponibilità dei dati ritardata**: paradossalmente, l&#39;esecuzione di molti batch di piccole dimensioni può ritardare la disponibilità dei dati per i processi a valle rispetto ai batch consolidati.
* **Ispezione difficile**: il monitoraggio del successo e delle prestazioni di decine di singoli processi batch per set di dati diventa complesso dal punto di vista operativo e richiede tempo.
* **Ritardo elaborazione profilo**: ogni batch di acquisizione profilo attiva l&#39;elaborazione del profilo. Piccoli batch frequenti possono causare l’esecuzione quasi continua dell’elaborazione del profilo, impedendo un’ottimizzazione batch efficiente.

**Come correggerlo**:

* **Ridurre la frequenza batch**: consolidare un numero inferiore di batch al giorno per set di dati per la maggior parte dei casi d&#39;uso.
* **Aumenta dimensione batch**: accumula più dati prima di attivare l&#39;acquisizione anziché effettuarla immediatamente.
* **Allinea alle esigenze aziendali**: verificare se gli aggiornamenti orari sono effettivamente necessari o se sono sufficienti gli aggiornamenti giornalieri/due volte al giorno.
* **Usa lo streaming per il tempo reale**: passa allo streaming ingestion per requisiti di tempo reale autentici invece di simularlo con batch frequenti.

## Passaggi successivi {#next-steps}

Dopo aver identificato gli anti-pattern nei programmi di lavoro:

* Visualizza [dettagli processo](job-schedules-details.md) per analizzare set di dati ed esecuzioni di processi specifici che potrebbero causare problemi.
* Rivedi la [Panoramica sugli Schedules per i processi](job-schedules.md) per comprendere le funzionalità di interfaccia e ispezione.
* Scopri le [acquisizioni batch](../ingestion/batch-ingestion/overview.md) per ottimizzare le pianificazioni di caricamento dei dati.
* Comprendi le [pianificazioni di segmentazione](../segmentation/home.md) per garantire la tempistica corretta delle valutazioni del pubblico.
* Esplora [il monitoraggio dei flussi di dati di destinazione](../dataflows/ui/monitor-destinations.md) per la visibilità della pipeline end-to-end.
