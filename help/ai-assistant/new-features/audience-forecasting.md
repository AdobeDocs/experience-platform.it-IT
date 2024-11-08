---
title: Monitoraggio di modifiche significative e previsione del pubblico con l’Assistente AI
description: Scopri come utilizzare l’Assistente AI per monitorare modifiche significative e prevedere i tipi di pubblico in Adobe Experience Platform.
badge: Alpha
source-git-commit: 37d2886cc5d7b3a019d23f76973d79547865298b
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 0%

---

# Monitorare cambiamenti significativi e prevedere la crescita del pubblico con AI Assistant

>[!AVAILABILITY]
>
>Questa funzione è disponibile in Alpha e potrebbe non essere disponibile per la tua organizzazione. Per partecipare al programma di Alpha e accedere a questa funzione, contatta il team del tuo account Adobe.

Nell’attuale panorama di marketing basato sui dati, è essenziale disporre di informazioni tempestive e accurate. Che tu sia un utente aziendale o un utente nelle operazioni di marketing, devi poter interagire in modo coerente con il pubblico e apportare modifiche rapide e di impatto sulla base di informazioni chiare. Per mantenere l’allineamento o raggiungere gli obiettivi aziendali, è necessario disporre delle informazioni utilizzabili necessarie per promuovere campagne efficaci e ottimizzare le risorse.

Puoi utilizzare AI Assistant per Adobe Experience Platform per monitorare modifiche significative e fornire previsioni di crescita per il pubblico e le dimensioni dei set di dati. Potrai quindi utilizzare queste informazioni per garantire l’integrità dei dati sul pubblico e offrire proiezioni lungimiranti per supportare processi decisionali basati sui dati.

Leggi questo documento per scoprire come monitorare modifiche significative e prevedere la crescita e le fluttuazioni del pubblico utilizzando l’Assistente AI.

## Terminologia e definizioni chiave {#key-terminology-and-definitions}

Per un elenco di terminologie importanti e delle relative definizioni, consulta la tabella seguente.

| Terminologia | Definizione |
| --- | --- |
| Modifica significativa | Una modifica significativa è un’ampia modifica basata su percentuale delle dimensioni del pubblico o del set di dati, definita da soglie specifiche (ad esempio, 10% per i tipi di pubblico di grandi dimensioni). Modifiche significative aiutano a identificare le anomalie che influiscono sulla stabilità dei dati. |
| Anomalie | Le anomalie sono variazioni impreviste nei dati, ad esempio una crescita improvvisa del 20% in un pubblico di **acquirenti di valore elevato**. Un’anomalia può essere causata da un potenziale problema di acquisizione dei dati o da una modifica nella definizione del pubblico. |
| Dati storici | I dati storici si riferiscono a dati a lungo termine, di solito da uno a tre anni. Puoi utilizzare i dati storici per tenere traccia dei pattern. **Nota**: durante la fase di Alpha, l&#39;Assistente IA fornisce dati storici fino a 13 mesi. |
| Dati emergenti/recenti | I dati emergenti o recenti si riferiscono a punti di dati osservati in un breve periodo, in genere per una settimana o fino a 30 giorni. Puoi utilizzare dati emergenti o recenti per evidenziare tendenze immediate e apportare modifiche rapide. |
| Previsione | Le previsioni sono previsioni del pubblico futuro o della dimensione del set di dati in base alle tendenze passate. È possibile utilizzare i dati di previsione per supportare la pianificazione a lungo termine. |
| Dimensione pubblico | La dimensione del pubblico si riferisce al numero totale di profili all’interno di un pubblico. La dimensione del pubblico viene aggiornata a ogni iterazione di acquisizione dei dati. |
| Intervallo di tempo per il confronto | L’Assistente IA utilizza intervalli di tempo di confronto predefiniti. Per impostazione predefinita, le anomalie recenti si ripetono dopo sette giorni, mentre quelle passate durano 30 giorni. Le tendenze storiche si estendono su un periodo di 13 mesi. |

{style="table-layout:auto"}

## Esempi di casi d’uso {#use-case-examples}

La capacità di AI Assistant di monitorare cambiamenti significativi e prevedere i tipi di pubblico può essere particolarmente utile per i seguenti casi d’uso:

### Operazioni di marketing

I professionisti delle operazioni di marketing (operazioni di marketing) hanno la responsabilità di garantire l’integrità e la coerenza dei dati sul pubblico. In qualità di membro di un team di addetti al marketing, le tue responsabilità possono includere il monitoraggio della qualità dei dati, la risposta a spostamenti imprevisti e il mantenimento di una base stabile per tutte le attività di marketing. Puoi utilizzare il rilevamento delle anomalie dell’Assistente AI per rilevare e risolvere modifiche significative a livello di pubblico o set di dati, evitando in tal modo interruzioni che potrebbero influire sulle prestazioni della campagna.

### Utenti aziendali e addetti al marketing

In qualità di utente aziendale e di addetto al marketing, puoi contare su informazioni accurate sul pubblico per prendere decisioni basate sui dati e garantire che le campagne raggiungano efficacemente il pubblico a cui sono destinate. Con le funzionalità di previsione di AI Assistant, puoi prevedere la crescita o la riduzione del pubblico e consentire adeguamenti strategici delle risorse e del targeting nel tempo.

## Funzioni chiave

>[!IMPORTANT]
>
>Le seguenti funzioni sono di Alpha e si concentrano sulle funzionalità fondamentali di monitoraggio e previsione. Poiché questa funzione si trova in Alpha, è necessario assicurarsi di verificare la precisione delle risposte ricevute dall&#39;Assistente IA.

### Monitorare cambiamenti significativi nel pubblico e nei dati

Puoi utilizzare l’Assistente AI per identificare cambiamenti significativi nelle dimensioni di pubblico e set di dati tracciando le deviazioni dai pattern tipici. Ogni modifica significativa si basa su soglie predefinite adattate alla scala del pubblico.

| Dimensione del pubblico | Numero di profili | Descrizione |
| --- | --- | --- |
| Piccoli tipi di pubblico | Da 1 a 100.000 profili | Segnala una modifica del 30% o più, a meno che non venga specificata una percentuale specifica. |
| Pubblico Medium | Da 100.000 a 500.000 profili | Segnala una modifica pari o superiore al 25%, a meno che non venga specificata una percentuale specifica. |
| Pubblico di grandi dimensioni | Da 500.000 a 1 milione di profili | Segnala una modifica di almeno il 20%, a meno che non venga specificata una percentuale specifica. |
| Pubblico molto ampio | Oltre 1 milione di profili | Segnala una modifica pari o superiore al 10%, a meno che non venga specificata una percentuale specifica. |

{style="table-layout:auto"}

>[!BEGINSHADEBOX]

#### Scenario di esempio

Modifiche significative indicano anomalie che possono influire sulla stabilità del pubblico o sull’affidabilità dei dati. Ad esempio, se un pubblico di **acquirenti di valore elevato** registra un calo improvviso del 15% delle dimensioni, l&#39;Assistente AI segnalerà questo cambiamento come significativo. Puoi quindi utilizzare queste informazioni per indagare e risolvere potenziali problemi prima che influiscano sulle campagne.

>[!ENDSHADEBOX]

>[!TIP]
>
>L’Assistente AI non notifica automaticamente il verificarsi di modifiche significative nelle dimensioni del pubblico. Devi avviare una conversazione con l’Assistente AI e chiedere quali tipi di pubblico sono cambiati in modo significativo o di un margine specifico, entro un periodo di tempo specifico.

### Previsione della crescita di pubblico e set di dati

Puoi utilizzare l’Assistente AI per fare riferimento alle tendenze cronologiche dei dati e proiettare le dimensioni future di pubblico e set di dati. Puoi quindi utilizzare queste informazioni per supportare la pianificazione delle risorse e gli adeguamenti della strategia. Al momento, puoi utilizzare l’Assistente IA per prevedere la crescita del pubblico e dei set di dati per 30 giorni. Comprendendo la crescita o il declino del pubblico previsto, puoi regolare le strategie di targeting e allocare le risorse di conseguenza.

### Informazioni sulle dimensioni storiche del pubblico

Oltre a rilevare modifiche significative, puoi utilizzare l’Assistente AI per recuperare informazioni storiche e confrontare le dimensioni correnti del pubblico o dei set di dati con i dati passati. Questa funzione supporta il tracciamento delle tendenze a lungo termine e la valutazione dell’impatto delle precedenti attività di marketing.

Puoi porre all’assistente di intelligenza artificiale domande del tipo: &quot;Qual è stata la dimensione del pubblico del mese scorso dei &quot;Clienti fedeltà&quot;? per visualizzare dati storici sulla crescita o sul declino di questo pubblico specifico.

## Domande di esempio per il monitoraggio di cambiamenti significativi

Puoi inquadrare le domande dell’Assistente AI in diversi modi.

* Se la domanda include una percentuale, ad esempio **&quot;Quali tipi di pubblico sono cambiati di oltre il 30%?&quot;**, l&#39;Assistente IA utilizzerà la percentuale come punto di riferimento.
* Se la domanda non specifica una percentuale, l&#39;Assistente AI interpreterà le modifiche significative in base alle impostazioni predefinite.

Consulta le tabelle seguenti, ad esempio le query che illustrano come l’Assistente AI interpreta le modifiche significative in base alle dimensioni del pubblico:

| Informazioni sul pubblico o modifica del pubblico | Esempio |
| --- | --- |
| <ul><li>Qual è la dimensione corrente di {AUDIENCE_NAME}?</li><li>Mostra i tipi di pubblico che hanno mostrato una modifica di {PERCENT} rispetto a {DATE_DURATION}.</li></ul> | <ul><li>Qual è la dimensione attuale del pubblico di acquirenti di valore elevato?</li><li>Mostra i tipi di pubblico che hanno mostrato una modifica del 20% nell’ultima settimana.</li></ul> |

{style="table-layout:auto"}

| Query specifiche per il pubblico | Esempio |
| --- | --- |
| <ul><li>Quali tipi di pubblico hanno cambiato più di {PERCENT} in {DATE_OR_DURATION}?</li><li>Mostra i tipi di pubblico con una modifica significativa rispetto a {DATE_OR_DURATION}.</li><li>Mostra la distribuzione dei tipi di pubblico con le modifiche più grandi rispetto a {DATE_OR_DURATION}.</li><li>Mostra i tipi di pubblico che hanno subito una riduzione superiore a {PERCENT} il {DATE_OR_DURATION}.</li></ul> | <ul><li>Quali tipi di pubblico sono cambiati di più del 20% nell’ultima settimana?</li><li>Mostrami i tipi di pubblico con un cambiamento significativo negli ultimi sei mesi.</li><li>Mostrami la distribuzione dei tipi di pubblico con le modifiche più grandi dal 1° ottobre al 31 ottobre.</li><li> Mostrami tipi di pubblico che sono diminuiti di oltre il 20% dal 31 agosto. |

{style="table-layout:auto"}

## Informazioni aggiuntive

### Informazioni sulla soglia di &quot;cambiamento significativo&quot;

È possibile specificare una percentuale specifica quando si esegue una query sull&#39;Assistente IA per informazioni relative a modifiche significative. Se non fornisci una percentuale specifica, l’Assistente IA farà riferimento a un set predefinito di soglie per determinare cosa si qualifica come modifica significativa. Le soglie predefinite si basano sulle dimensioni di un determinato pubblico. Fai riferimento alla tabella seguente per informazioni su ciò che costituisce una modifica significativa, in base alla dimensione del pubblico:

| Dimensione del pubblico | Cos’è significativo? |
| --- | --- |
| 1 milione o più | 10% o superiore |
| Da 500k a 1 milione | 20% o superiore |
| da 100k a 500k | 25% o superiore |
| Inferiore a 100k | 30% o superiore |

### Timeline generiche e date specifiche

Ai Assistant supporta confronti basati sul tempo specifici e generici per le dimensioni del pubblico, interpretandoli in base al contesto fornito nella query.

>[!BEGINTABS]

>[!TAB Timeline generiche]

Le timeline generiche si riferiscono a query che utilizzano un linguaggio come &quot;questa settimana&quot; o &quot;ultima settimana&quot;. Se si pone all&#39;Assistente AI una domanda del tipo: &quot;Quali tipi di pubblico sono cambiati di oltre il 20% nell&#39;ultima settimana?&quot;, l&#39;Assistente AI calcolerà e confronterà la dimensione del **pubblico medio** nel periodo specificato.

Utilizza questo approccio per avere una visione più ampia dei cambiamenti del pubblico nel tempo, consentendoti di comprendere meglio le tendenze entro intervalli settimanali o mensili.

>[!TAB Date specifiche]

Se la domanda fa riferimento a una data specifica, l&#39;Assistente AI confronterà le **dimensioni esatte del pubblico** in ciascuna delle date specificate.

Utilizza questo preciso confronto per analizzare i cambiamenti tra punti specifici del tempo e ottenere chiarezza su come la dimensione del pubblico può evolvere in giorni particolari.

>[!ENDTABS]

Puoi sfruttare questa flessibilità per comprendere meglio le dinamiche del pubblico in intervalli di tempo ampi e precisi. Che tu stia tenendo traccia delle tendenze generali o analizzando spostamenti esatti tra date specifiche, puoi utilizzare il meccanismo adattivo di AI Assistant per recuperare il confronto più relativo per la query.

## Domande frequenti {#faq}

Leggi questa sezione per le risposte alle domande più frequenti sul monitoraggio di modifiche significative e sulla previsione del pubblico con l’Assistente AI.

### Quanti dati storici posso esaminare per vedere l’aumento o la diminuzione delle dimensioni del pubblico?

Ai Assistant conserva 12 mesi di dati cronologici sulle dimensioni del pubblico. In questo intervallo di tempo puoi porre domande sui cambiamenti del pubblico per comprendere i pattern di crescita o declino nell’ultimo anno.

### Quanto indietro nella storia posso andare per vedere i cambiamenti del pubblico?

L’Assistente AI tiene traccia delle modifiche del pubblico dal giorno in cui è abilitato nell’organizzazione fino all’ultima modifica della definizione del pubblico. Una volta abilitata, l’Assistente AI monitora e registra continuamente le modifiche di definizione per un massimo di 12 mesi, consentendo il tracciamento e il confronto futuri dei dati.

### Quanti dati storici sono necessari per una previsione?

Sono necessari almeno 30 giorni di dati per una previsione affidabile a partire dall’ultima modifica di definizione del pubblico. In alcuni casi, ad esempio le previsioni per [!DNL Black Friday], l&#39;Assistente IA può richiedere fino a 12 mesi di dati storici.

### In che modo l’Assistente AI interpreta &quot;di recente&quot;?

L’Assistente AI interpreta &quot;recentemente&quot; come gli ultimi sette giorni. Per le domande che fanno riferimento a modifiche recenti, l’Assistente AI considera i dati di questo periodo di tempo per identificare tendenze o spostamenti.

### In che modo l’Assistente AI confronta le dimensioni del pubblico?

Quando sono menzionate date specifiche, l’Assistente AI confronta le dimensioni del pubblico in tali giorni specifici. Per domande più generali, ad esempio quelle che fanno riferimento agli &quot;ultimi tre mesi&quot; o alla &quot;settimana scorsa&quot;, l’Assistente AI confronta la dimensione media di quel periodo con la media del giorno più recente.

### Quanto sono attuali i dati sul pubblico dell’Assistente AI?

Potrebbero essere necessarie da 24 a 48 ore affinché l’Assistente AI aggiorni i dati da Real-time Customer Data Platform. Quindi, per le domande che fanno riferimento a &quot;ieri&quot;, l’Assistente AI interpreta questo come un giorno prima che siano disponibili i dati più recenti di cui dispone.

## Funzioni fuori ambito

Le seguenti funzionalità non sono attualmente supportate:

### root cause analysis avanzata

L’Assistente AI è in grado di identificare modifiche significative, ma al momento non è in grado di fornire un’analisi dettagliata della causa principale di tali spostamenti. Le iterazioni future di AI Assistant mirano a specificare quali set di dati o attributi contribuiscono a cambiamenti significativi nei tipi di pubblico.

### Dimensioni complete dei set di dati storici

Al momento, il tracciamento cronologico completo delle dimensioni dei dati non è supportato. Attualmente, l’Assistente AI fornisce cronologia di pubblico e set di dati per un massimo di 13 mesi.