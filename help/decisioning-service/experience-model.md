---
keywords: Experience Platform;home;popular topics;decision events;decision event;Decision events
solution: Experience Platform
title: Modello di dominio per la decodifica delle esperienze
topic: overview
description: In questa sezione vengono illustrati i componenti di Disioning Service e le modalità di interazione di tali componenti. I concetti e le loro relazioni formano il *Dominio* del problema decisionale. Questi componenti fondamentali vengono attivati indipendentemente da come si utilizza il servizio di gestione delle decisioni].
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 0%

---


# Modello di dominio esperienza [!DNL Decisioning]

In questa sezione vengono illustrati i componenti di [!DNL Decisioning Service] e le modalità di interazione di tali componenti. I concetti e le loro relazioni costituiscono il *dominio* del problema decisionale. Questi componenti fondamentali vengono riprodotti indipendentemente da come vengono utilizzati [!DNL Decisioning Service].

## Opzioni decisione

Un&#39;opzione ** decisionale relativa all&#39;esperienza è un&#39;esperienza potenziale che può essere presentata a un cliente specifico. Un&#39;opzione è anche detta scelta o alternativa. Quando si decide l&#39;opzione migliore successiva per un cliente, [!DNL Decisioning Service] considera le opzioni da ***d<sub>1</sub>*** a ***<sub>dN</sub>*** tra un insieme limitato di opzioni **`D`**.

Le decisioni vengono prese individuando la migliore opzione tra una serie di opzioni disponibili. Un approccio consiste nell&#39;eliminare in successione le opzioni *di* decisione ***<sub>di</sub>*** ID ***dal set*** Dfino a quando non ne viene lasciata una sola e quindi scegliere un &quot;vincitore&quot; in modo casuale dal set rimanente. Un&#39;altra forma di processo decisionale consiste nel classificare le opzioni di decisione rimanenti (ammissibili) in base ai risultati attesi.

### Set finito di opzioni di decisione

Nel dominio Experience Decisioning le opzioni da cui uno o più sono selezionati esistono a priori e il calcolo di una decisione non crea al volo nuove opzioni. Diciamo che il dominio delle opzioni è finito al momento delle decisioni. Questo potrebbe sembrare un limite, ma un insieme limitato di opzioni dà origine alla possibilità di utilizzare algoritmi di machine learning e tecniche simili per decidere quale delle opzioni è &quot;quella migliore&quot;. Molti algoritmi di apprendimento non sarebbero in grado di produrre una soluzione ottimale tra un insieme di infinite alternative che non possono essere confrontate l&#39;una con l&#39;altra e per le quali non esistono dati di esempio.

## Risultati decisione

È importante distinguere tra i risultati della decisione `d` e i risultati `o`, ossia i risultati previsti dalla decisione. Una decisione spesso non può produrre un risultato diretto. La decisione è solo selezionare (o proporre) l&#39;opzione con il miglior risultato previsto. Tra proposizioni e risultati si verificano molti eventi e interazioni, spesso ritardati di giorni o settimane. In termini più formali, il risultato è una funzione della decisione `o = f(d)`.

Per trovare la decisione ottimale a ogni risultato viene assegnato un valore ****** di utilità `U(o) = U(f(d))`.
Per il caso di utilizzo di Offer Decisioning, tale funzione calcolerebbe il costo per soddisfare l&#39;offerta, e il valore ottenuto dall&#39;azienda quando l&#39;offerta viene accettata dal cliente. Il risultato sarebbe utilizzato per trovare la decisione ottimale (offerta) massimizzando il valore dell&#39;utilità su tutte le opzioni (offerte).

In genere non è possibile prevedere con certezza quale sarà l&#39;esito di una particolare decisione e quindi è necessario un approccio probabilistico. Il valore ***di*** utilità `U(o)` diventa il valore di utilità ***previsto di un&#39;opzione di decisione*** `EU(d)`

## Proposte Decisionali

Una proposta di *decisione* è una selezione di opzioni di decisione che è stata fatta in risposta a una richiesta di decisione effettiva. Come già detto, i risultati di una decisione possono verificarsi molto più tardi e i risultati non possono essere raggiunti neanche in un unico passaggio. È quindi importante tenere traccia delle proposte attraverso una serie di eventi *di* esperienza, in modo che possano essere riconducibili alle opzioni decisionali. Questo ciclo di feedback è utilizzato per migliorare la precisione di previsione per `EU(d)`.

Una proposizione è persistente come entità e ha quindi un identificatore. L&#39;entità contiene riferimenti alle opzioni selezionate e può registrare i dati contestuali utilizzati per prendere la decisione. La presenza di un identificatore consente anche ad altre entità di farvi riferimento. Una di tali entità è l&#39;evento ** decisionale. Contiene la marca temporale, segnando quando è stata presa la sua decisione (proposta). Un evento decisionale è un evento registrato dell&#39;azione di esecuzione della decisione. Altri eventi che fanno riferimento all&#39;entità proposizione sono eventi di esperienza. Ogni evento di esperienza può essere esteso per fare riferimento a una proposta di decisione. L&#39;interpretazione di ciò è che l&#39;evento di esperienza può essere attribuito in tutto o in parte alla proposta della decisione.

## Strategia decisionale - Algoritmo

Con una serie finita di alternative tra cui scegliere, ogni strategia ** decisionale è essenzialmente un algoritmo - o una funzione - che prende le opzioni di **`N`** decisione *{d<sub>1</sub>, d<sub>2</sub>, ...<sub>dN</sub>* *<sub></sub><sub></sub><sub></sub>* }come input e produce un elenco classifica di opzioni di decisione(dr1, 2, prev.la prima opzione di decisione nell&#39;elenco è considerata ottimale in base a un&#39;utilità prevista, la seconda opzione nell&#39;elenco dei risultati viene quindi considerata la seconda opzione migliore e così via. In genere, il set avrà una maggiore cardinalità rispetto all&#39;elenco di classifica risultante, in quanto l&#39;algoritmo di decisione elimina le opzioni non idonee e un algoritmo potrebbe essere configurato per restituire solo le **`K`** opzioni principali, arrestandosi dopo aver trovato abbastanza opzioni.
Il quadro decisionale generale è riportato nel seguente diagramma.

![Fig. 1](./images/decisioning-optimization.png)

## Attività decisionali

*Le attività* decisionali configurano l&#39;algoritmo e forniscono i parametri per una strategia decisionale specifica. I parametri della strategia includono i vincoli applicati alle opzioni e alla funzione di classificazione. Tutte le decisioni vengono prese nel contesto di un&#39;attività. [!DNL Decisioning Service] ospita molte attività e le attività possono essere riutilizzate tra i canali. In qualsiasi momento, l&#39;opzione migliore viene valutata in base al set più recente di vincoli, regole e modelli.

Un&#39;attività di decisione definisce la raccolta delle opzioni di decisione da prendere in considerazione. Consente di filtrare il sottoinsieme di tutte le opzioni che interessano questa attività. Questo consente [!DNL Decisioning service] di gestire le categorie topiche all&#39;interno del catalogo di tutte le opzioni.

Un&#39;attività di decisione specifica un&#39;opzione *di* fallback qualora i vincoli combinati non qualificassero tutte le altre opzioni. Ciò significa che c&#39;è sempre una risposta alla domanda: Qual è attualmente l&#39;opzione &quot;migliore&quot;?

Le attività decisionali possono specificare il luogo in cui viene distribuita l&#39;esperienza. Ciò riduce ulteriormente il numero di opzioni decisionali che possono essere prese in considerazione ed è un&#39;altra limitazione imposta dall&#39;attività decisionale. Questo è detto vincolo *di* posizionamento. Saranno prese in considerazione solo le opzioni di decisione il cui contenuto soddisfa questo vincolo di posizionamento. Tale valutazione viene effettuata nelle prime fasi della strategia decisionale. Quando le definizioni cambiano i vincoli di posizionamento di ciascuna attività di decisione vengono rivalutati e l&#39;opzione di decisione può entrare o cadere fuori considerazione per una o più attività di decisione.

## Contesto decisione

Fino ad ora, è stata descritta solo la *logica* aziendale che influisce sulla decisione. Ma ancora più incisivo è il *dato* della decisione. Questi dati sono denominati contesto ** decisionale ed è diverso per ogni utente e ogni volta che viene presa una decisione, a differenza di vincoli, regole e modelli che sono gli stessi per utenti diversi per la stessa attività. Anche regole, vincoli e modelli cambiano con minore frequenza. Per le decisioni in tempo reale, il contesto decisionale dovrà essere determinato anche in tempo reale.

I dati contestuali alle decisioni possono essere suddivisi in dati relativi al profilo utente, dati aziendali e dati raccolti internamente.

- *Le entità* di profilo vengono utilizzate per rappresentare i dati dell&#39;utente finale, ma non tutte le entità di profilo rappresentano un individuo. Potrebbe essere una famiglia, un gruppo sociale, o qualsiasi altro argomento. Gli eventi di esperienza sono record di dati relativi alla serie temporale associati a un profilo. Se esiste un&#39;esperienza, questi dati sono l&#39; *oggetto* di questa esperienza.
- Dall&#39;altro lato, ci sono le entità ** aziendali. Possono essere considerati come *oggetti* delle interazioni. Tali entità sono spesso utilizzate come riferimento negli eventi di esperienza delle entità di profilo. Esempi di entità aziendali sono siti Web e pagine, store, dettagli di prodotto, contenuto digitale, dati di inventario dei prodotti e così via.
- L&#39;ultima categoria di dati nel contesto della decisione è costituita da dati creati durante l&#39;operazione del [!DNL Decisioning Service]. Ogni evento di decisione rientra in quella categoria, insieme alle risposte dei clienti, i dati della proposta formano un set di dati interno denominato cronologia ** proposizione-risposta.

Esistono tre percorsi che i dati possono seguire per entrare a far parte del contesto decisionale. I dati di registrazione e serie temporale possono essere caricati tramite file di set di dati. Questo percorso è destinato principalmente alla sincronizzazione in massa con i sistemi esterni. È inoltre possibile eseguire lo streaming dei dati di record e delle serie temporali in [!DNL Platform] cui i dati vengono indicizzati e uniti alle entità del modulo. Attraverso il terzo percorso, i dati contestuali possono essere passati come parametri alla richiesta di decisione. Questa forma di dati è effimera e riguarda solo la decisione richiesta. Non è persistente come entità e non è disponibile per altre richieste.
