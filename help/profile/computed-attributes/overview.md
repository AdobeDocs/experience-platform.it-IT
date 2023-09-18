---
title: Panoramica degli attributi calcolati
description: Gli attributi calcolati sono funzioni per aggregare i dati a livello di evento negli attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate in segmentazione, attivazione e personalizzazione.
source-git-commit: 7ed473750b673eefd84b8d727043ad6ea35c3a8e
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 1%

---


# Panoramica degli attributi calcolati

La personalizzazione basata sul comportamento degli utenti è un requisito chiave affinché gli esperti di marketing massimizzino l’impatto della personalizzazione. Ad esempio, puoi personalizzare l’e-mail di marketing con il prodotto visualizzato più di recente per favorire la conversione o la pagina web in base al totale degli acquisti effettuati dagli utenti per promuovere la fidelizzazione.

Gli attributi calcolati consentono di convertire rapidamente i dati comportamentali del profilo in valori aggregati a livello di profilo senza dipendere dalle risorse tecniche per:

- Abilitazione della personalizzazione mirata uno-a-uno o in batch con attivazione degli aggregati comportamentali per le destinazioni Real-time Customer Data Platform e l’utilizzo in Adobe Journey Optimizer
- Segmentazione del pubblico semplificata con archiviazione di aggregati comportamentali come attributi di profilo
- Standardizzazione dei dati comportamentali aggregati del profilo da utilizzare su piattaforme e app diverse
- Migliore gestione dei dati con consolidamento dei dati dei vecchi eventi di profilo in informazioni comportamentali significative

Questi aggregati vengono calcolati in base ai set di dati Experience Event abilitati per il profilo e acquisiti in Adobe Experience Platform. Ogni attributo calcolato è un attributo di profilo creato nello schema di unione profili e viene raggruppato nel gruppo di campi &quot;SystemComputedAttribute&quot; nello schema di unione.

I casi d’uso di esempio includono:

- Personalizzazione delle e-mail di marketing con punti premio totali per congratularsi con gli utenti per essere stati promossi a un livello superiore
- Personalizzazione delle comunicazioni agli utenti in base al numero di acquisti e alla frequenza
- Personalizzazione delle e-mail di conservazione in base alle date di scadenza dell’abbonamento
- Nuovo targeting degli utenti che hanno visualizzato ma non hanno acquistato un prodotto con l’ultimo prodotto visualizzato
- Attivazione di aggregazioni di eventi tramite attributi calcolati in un sistema a valle utilizzando Destinazioni di Real-Time CDP
- Compressione di più tipi di pubblico basati su eventi in un gruppo più compatto di attributi calcolati
- Nuovo targeting degli utenti non autenticati fuori sede utilizzando ID partner recenti da eventi

Questa guida ti aiuterà a comprendere meglio il ruolo degli attributi calcolati in Platform, oltre a spiegare le nozioni di base degli attributi calcolati.

## Informazioni sugli attributi calcolati

Adobe Experience Platform consente di importare e unire facilmente i dati provenienti da più origini per generare [!DNL Real-Time Customer Profiles]. Ogni profilo contiene informazioni importanti relative a un individuo, come le informazioni di contatto, le preferenze e la cronologia degli acquisti, fornendo una visualizzazione a 360 gradi del cliente.

Alcune delle informazioni raccolte nel profilo sono facilmente comprensibili durante la lettura diretta dei campi di dati (ad esempio, &quot;nome&quot;), mentre altri dati richiedono l’esecuzione di più calcoli o l’affidamento su altri campi e valori per generare le informazioni (ad esempio, &quot;totale acquisti per tutta la durata della vita&quot;). Per semplificare la comprensione immediata di questi dati, [!DNL Platform] consente di creare attributi calcolati che eseguono automaticamente questi riferimenti e calcoli, restituendo il valore nel campo appropriato.

Gli attributi calcolati includono la creazione di un’espressione, o &quot;regola&quot;, che funziona sui dati in arrivo e memorizza il valore risultante in un attributo di profilo. Le espressioni possono essere definite in più modi diversi, consentendoti di specificare su quali eventi aggregare, funzioni di aggregazione o le durate del lookback.

### Funzioni

Gli attributi calcolati consentono di definire gli aggregati di eventi in modo autonomo sfruttando funzioni predefinite. I dettagli su queste funzioni sono disponibili qui sotto:

| Funzione | Descrizione | Tipi di dati supportati | Esempio di utilizzo |
| -------- | ----------- | -------------------- | ------------- |
| SOMMA | Una funzione che **somme** il valore specificato per gli eventi qualificati. | Interi, numeri, lunghezze | Somma di tutti gli acquisti degli ultimi 7 giorni |
| COUNT | Una funzione che **conteggi** il numero di eventi che si sono verificati per la regola specificata. | N/D | Numero di acquisti negli ultimi 3 mesi |
| MIN | Una funzione che trova **minimo** valore per gli eventi qualificati. | Interi, Numeri, Lunghi, Marca temporale | Dati del primo acquisto negli ultimi 7 giorni<br/>Importo minimo dell’ordine nelle ultime 4 settimane |
| MAX | Una funzione che trova **massimo** valore per gli eventi qualificati. | Interi, Numeri, Lunghi, Marca temporale | Ultimi dati di acquisto negli ultimi 7 giorni<br/>Importo massimo dell’ordine nelle ultime 4 settimane |
| MOST_RECENT | Funzione che trova il valore di attributo specificato dall&#39;ultimo evento qualificato. Questa funzione offre **entrambi** il valore e la marca temporale dell’attributo. | Tutti i valori primitivi, matrici di valori primitivi | Ultimo prodotto visualizzato negli ultimi 7 giorni |

### Periodi di lookback

Gli attributi calcolati vengono calcolati in batch, consentendo di mantenere aggiornati gli aggregati e utilizzando gli eventi più recenti. Per supportare questi scenari quasi in tempo reale, la frequenza di aggiornamento varia a seconda del periodo di lookback dell’evento.

Il periodo di lookback si riferisce alla quantità di tempo che viene esaminata durante l’aggregazione di Eventi esperienza per l’attributo calcolato. Questo periodo di tempo può essere definito in ore, giorni, settimane o mesi.

La frequenza di aggiornamento si riferisce alla frequenza con cui gli attributi calcolati vengono aggiornati. Questo valore dipende dal periodo di lookback e viene impostato automaticamente.

| Periodo di lookback | Refresh frequency (Frequenza di aggiornamento) |
| --------------- | ----------------- |
| Fino a 24 ore | Oraria |
| Fino a 7 giorni | Giornaliero |
| Fino a 4 settimane | Settimanale |
| Fino a 6 mesi | Mensile |

Ad esempio, se l’attributo calcolato ha un periodo di lookback degli ultimi 7 giorni, questo valore verrà calcolato in base ai valori degli ultimi 7 giorni e quindi aggiornato su base giornaliera.

>[!NOTE]
>
>Sia le settimane che i mesi sono considerati **settimane di calendario** e **mesi calendario** quando utilizzato nei lookback di eventi. La settimana del calendario inizia il **Domenica** e termina il **Sabato** della settimana.

**Aggiornamento rapido** {#fast-refresh}

L’aggiornamento rapido consente di mantenere aggiornati gli attributi. L’abilitazione di questa opzione consente di aggiornare gli attributi calcolati su base giornaliera, anche per periodi di lookback più lunghi, per poter reagire rapidamente alle attività degli utenti.

>[!NOTE]
>
>L’abilitazione dell’aggiornamento rapido varia la durata del lookback dell’evento, in quanto il periodo di lookback viene riavviato rispettivamente su base settimanale o mensile.
>
>Se crei un attributo calcolato con un periodo di lookback di due settimane con aggiornamento rapido abilitato, il periodo di lookback iniziale sarà di due settimane. Tuttavia, con ogni aggiornamento giornaliero, il periodo di lookback includerà gli eventi del giorno aggiuntivo. L’aggiunta di giorni continuerà fino all’inizio della settimana di calendario successiva, durante la quale l’intervallo di lookback verrà rinnovato e tornerà a due settimane.
>
>Ad esempio, se si è verificato un periodo di lookback di due settimane a partire dal 15 marzo (domenica) con aggiornamento rapido abilitato, con aggiornamento giornaliero, il periodo di lookback continuerà a espandersi inclusivamente fino al 22 marzo, giorno in cui verrà ripristinato su due settimane. In breve, l’attributo calcolato è **aggiornato** ogni giorno, con il periodo di lookback che aumenta da **due** settimane a **tre** settimane durante la settimana, e quindi di nuovo a **due** settimane.

## Passaggi successivi

Per ulteriori informazioni sulla creazione e la gestione degli attributi calcolati, consultare [guida API per attributi calcolati](./api.md) o [guida dell’interfaccia utente per attributi calcolati](./ui.md).
