---
title: Stima Del Linguaggio Naturale Con L’Assistente Ai
description: Scopri come utilizzare le funzionalità di stima del linguaggio naturale di AI Assistant.
badge: Alpha
source-git-commit: aef3be05ca23abe9ed8275aa562fdd3313a7e2d0
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 0%

---

# Stima del linguaggio naturale con IA Assistant

>[!AVAILABILITY]
>
>Questa funzione è disponibile in Alpha e potrebbe non essere disponibile per la tua organizzazione. Per partecipare al programma di Alpha e accedere a questa funzione, contatta il team del tuo account Adobe.

Puoi utilizzare le funzionalità di Stima del linguaggio naturale di AI Assistant per Adobe Experience Platform per stimare le dimensioni del pubblico e prevedere le propensione del pubblico in base a domande semplici e conversazionali. Con questa funzione, puoi rendere gli approfondimenti sul pubblico più accessibili e intuitivi. Questo può essere particolarmente utile per i casi di utilizzo delle operazioni di marketing e aziendali, soprattutto se gestisci i tipi di pubblico quotidianamente e ti avvali di queste informazioni per definire strategie di marketing efficaci.

Con le funzionalità di elaborazione in linguaggio naturale di AI Assistant, puoi porre domande del tipo: &quot;Quanti profili ho in California tra i 25 e i 35 anni&quot; o &quot;Quanti clienti di alto valore abbiamo?&quot; o anche &quot;Quale percentuale del mio pubblico potrà acquistare entro il prossimo mese?&quot; L’Assistente AI interpreta quindi queste domande e restituisce stime o punteggi di tendenza da utilizzare per prendere decisioni basate sui dati.

Leggi questo documento per scoprire come utilizzare le funzionalità di stima del linguaggio naturale di AI Assistant.

## Terminologia e definizioni chiave {#key-terminology-and-definitions}

Per un elenco di terminologie importanti e delle relative definizioni, consulta la tabella seguente.

| Terminologia | Definizione |
| --- | --- |
| Stima della dimensione del pubblico | Il processo di calcolo del numero di membri all’interno di un pubblico specifico in base a criteri definiti. Puoi basare le stime delle dimensioni sui dati di profilo, inclusi i profili non in un pubblico. Inoltre, puoi recuperare le stime delle dimensioni del pubblico senza dover prima creare un pubblico. Utilizza questa informazione per comprendere la portata delle campagne mirate. |
| Stima della tendenza | Una previsione della probabilità che i membri di un pubblico esibiscano comportamenti specifici (ad esempio: effettuare un acquisto, abbandono) entro un determinato intervallo di tempo. La stima della propensione è specifica per i tipi di pubblico all’interno di Real-time Customer Data Platform, ma può includere i dati di profilo, inclusi i profili in in qualsiasi pubblico. Puoi fare riferimento a questa informazione durante l’ottimizzazione delle campagne e la gestione delle strategie di conservazione del pubblico. |
| Elaborazione in linguaggio naturale | La capacità dell’Assistente AI di interpretare e rispondere alle domande poste nel linguaggio quotidiano, consentendoti di interagire conversando e ricevere informazioni rilevanti senza utilizzare query tecniche. |
| Intervalli di tempo predefiniti | Intervalli di tempo standard ( &quot;ultimo mese&quot;, &quot;prossimi 30 giorni&quot;) supportati da AI Assistant per la stima delle dimensioni e delle tendenze del pubblico. **Nota**: gli intervalli di tempo personalizzati potrebbero non essere completamente supportati durante la fase di Alpha. |
| Dati snapshot | Set di dati utilizzato dall’Assistente AI per fornire stime. Questi dati vengono aggiornati da Real-time Customer Data Platform ogni 24-48 ore e pertanto le informazioni potrebbero non riflettere i cambiamenti del pubblico in tempo reale. |

{style="table-layout:auto"}

## Esempi di casi d’uso {#use-case-examples}

Le funzionalità di stima del linguaggio naturale di AI Assistant possono essere particolarmente utili per i seguenti casi d’uso:

### Operazioni di marketing

In qualità di professionista delle operazioni di marketing, le tue responsabilità possono includere la gestione e il monitoraggio dei dati sul pubblico per garantire che siano in linea con gli obiettivi aziendali. Con la funzione di stima del linguaggio naturale di AI Assistant, puoi raccogliere rapidamente informazioni sulle dimensioni e sulle tendenze del pubblico senza dover creare prima un pubblico o una conoscenza approfondita dell’analisi dei dati.

aiutandoli a mantenere un approccio coerente e basato sui dati nei loro flussi di lavoro.

### Utenti aziendali e addetti al marketing

In qualità di utente aziendale e di addetto al marketing, l’accesso rapido ai dati sul pubblico può essere fondamentale per il successo della pianificazione, del targeting e della valutazione delle campagne. Con la funzione di stima del linguaggio naturale di AI Assistant, puoi semplificare l’accesso alle informazioni sul pubblico, porre domande semplici e ricevere informazioni fruibili utili per la creazione del pubblico e l’ottimizzazione della campagna.

## Funzioni chiave

>[!IMPORTANT]
>
>Le seguenti funzioni sono di Alpha e si concentrano sulle funzionalità fondamentali della stima del linguaggio naturale. Poiché questa funzione si trova in Alpha, è necessario assicurarsi di verificare la precisione delle risposte ricevute dall&#39;Assistente IA.

### Stima della dimensione del pubblico

Puoi utilizzare le query in linguaggio naturale per chiedere all’Assistente AI di stimare la dimensione di tipi di pubblico specifici. Questa funzione può essere particolarmente utile per valutare la portata e l’impatto dei tipi di pubblico target. Ad esempio, in qualità di stratega del marketing, puoi porre domande quali:

* &quot;Quanti profili vivono a New York?&quot;
* &quot;Quanti profili ho con un’e-mail e ho acconsentito?&quot;

Utilizza questa funzione per semplificare il processo di stima delle dimensioni del pubblico e ottenere risposte immediate senza dover navigare in filtri di dati o definizioni di segmenti complessi.

### Stima della propensione del pubblico

>[!TIP]
>
>Per utilizzare le funzionalità di stima della propensione dell&#39;Assistente all&#39;intelligenza artificiale, è necessario eseguire il provisioning del tuo account di Experience Platform con [IA per l&#39;analisi dei clienti](../../intelligent-services/customer-ai/overview.md).

Puoi utilizzare la stima della propensione del pubblico per identificare la probabilità di comportamenti o azioni specifici all’interno di un pubblico. Ad esempio, puoi porre domande quali:

* &quot;Quale percentuale del mio pubblico attuale potrebbe acquistare nel prossimo mese?&quot;
* &quot;Quanti profili ho con una tendenza elevata a convertire?&quot;

Ponendo domande in linguaggio naturale, puoi recuperare i punteggi di tendenza che indicano la percentuale o la probabilità che alcuni membri del pubblico esibiscano determinati comportamenti, per poter apportare modifiche proattive alle campagne o alle strategie di fidelizzazione.

## Domande di esempio sulle dimensioni del pubblico e sulla stima della propensione

Di seguito sono riportate alcune domande di esempio che puoi porre all’Assistente AI per comprendere le dimensioni del pubblico e le tendenze comportamentali:

### Stima dimensione pubblico

* &quot;Quanti profili ho con e-mail o numero di telefono cellulare?&quot;
* &quot;Quanti profili ho a New York?&quot;
* &quot;Quali sono i primi 5 stati in cui vivono i miei clienti?&quot;

### Stima della propensione del pubblico

* &quot;Quale percentuale del mio pubblico potrà acquistare entro il prossimo mese?&quot;
* &quot;Quanti clienti ci si aspetta di trovare per il prossimo trimestre?&quot;

Puoi sfruttare la flessibilità offerta dalle query in linguaggio naturale per ottenere informazioni rapide sulle dinamiche del pubblico senza dover disporre di competenze tecniche.

## Domande frequenti

Leggi questa sezione per le risposte alle domande frequenti sulla stima del linguaggio naturale con l’Assistente AI.

### Con quale frequenza l’Assistente AI aggiorna i dati sul pubblico?

I dati di AI Assistant vengono aggiornati ogni 24-48 ore. Pertanto, le stime possono riflettere un leggero ritardo. Ciò significa che quando chiedi informazioni sui dati &quot;correnti&quot;, la risposta riflette l’istantanea più recente, che può risalire a un massimo di 48 ore.

### Posso chiedere dimensioni o propensione del pubblico con intervalli di date personalizzati?

Attualmente, l’Assistente AI supporta intervalli di date predefiniti, ad esempio &quot;ultimo mese&quot; o &quot;prossimi 30 giorni&quot;. Gli intervalli di date personalizzati oltre queste opzioni predefinite non sono completamente supportati nella fase di Alpha. Se è richiesto un intervallo di tempo personalizzato, l’Assistente AI fornirà informazioni in base all’intervallo di tempo disponibile più vicino.

### In che modo l’Assistente AI calcola i punteggi di tendenza?

I punteggi di tendenza vengono calcolati utilizzando [IA per l&#39;analisi dei clienti](../../intelligent-services/customer-ai/overview.md). L’Assistente AI utilizza modelli di apprendimento automatico per prevedere la probabilità di comportamenti specifici del pubblico, come acquisti e abbandono, entro l’intervallo di tempo richiesto. Durante la fase di Alpha, il calcolo del punteggio di tendenza nell’Assistente IA non utilizza eventi di esperienza o dati comportamentali.

### L’Assistente AI stimerà le dimensioni o le tendenze del pubblico in base ai dati in tempo reale?

No, al momento non sono disponibili dati in tempo reale. Le stime si basano su istantanee di dati recenti, aggiornate ogni 24-48 ore. Gli aggiornamenti in tempo reale non rientrano nell’ambito di applicazione durante la fase di Alpha.

### Come vengono calcolate le propensione?

L’Assistente AI si basa sui modelli di IA per l’analisi dei clienti per rispondere a qualsiasi punteggio di probabilità o tendenza.

## Funzioni fuori ambito

Le seguenti funzionalità non sono attualmente supportate:

### Stime delle dimensioni del pubblico in base all’evento dei dati comportamentali

L&#39;Assistente per l&#39;intelligenza artificiale non è attualmente in grado di rispondere a domande basate su dati comportamentali quali **&quot;Quanti utenti hanno aggiunto un prodotto al carrello negli ultimi 30 giorni&quot;**. Tuttavia, puoi creare in Real-Time CDP un attributo calcolato che potrebbe precalcolare tali valori. Questi attributi calcolati sono quindi disponibili in AI Assistant. Per ulteriori informazioni, consulta la documentazione su [attributi calcolati](../../profile/computed-attributes/overview.md).

### Aggiornamenti dei dati in tempo reale

Le stime fornite da AI Assistant si basano su istantanee di dati recenti, ma non in tempo reale. I dati vengono aggiornati ogni 24-48 ore, pertanto le informazioni riflettono questo ritardo. Questo limite significa che gli utenti non possono ricevere aggiornamenti istantanei se un segmento o un set di dati cambia in modo significativo in un breve intervallo di tempo.