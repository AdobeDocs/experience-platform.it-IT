---
title: Panoramica degli attributi calcolati
description: Gli attributi calcolati sono funzioni per aggregare i dati a livello di evento negli attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate in segmentazione, attivazione e personalizzazione.
badge: "Beta"
source-git-commit: 3b4e1e793a610c9391b3718584a19bd11959e3be
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 1%

---

# Panoramica degli attributi calcolati

>[!IMPORTANT]
>
>Gli attributi calcolati sono attualmente in **beta** ed è **non** disponibile per tutti gli utenti.

La personalizzazione basata sul comportamento degli utenti è un requisito chiave affinché gli esperti di marketing massimizzino l’impatto della personalizzazione. Ad esempio, puoi personalizzare l’e-mail di marketing con il prodotto visualizzato più di recente per favorire la conversione o la pagina web in base al totale degli acquisti effettuati dagli utenti per promuovere la fidelizzazione.

Gli attributi calcolati consentono di convertire rapidamente i dati comportamentali del profilo in valori aggregati a livello di profilo senza dipendere dalle risorse tecniche per:

- Abilitazione della personalizzazione mirata con attivazione di aggregati comportamentali nelle destinazioni Real-time Customer Data Platform, utilizzo in Adobe Journey Optimizer o nella segmentazione
- Standardizzazione dei dati comportamentali aggregati del profilo da utilizzare su piattaforme e app diverse
- Migliore gestione dei dati con consolidamento dei dati dei vecchi eventi di profilo in informazioni comportamentali significative

Questi aggregati vengono calcolati in base ai set di dati Experience Event abilitati per il profilo e acquisiti in Adobe Experience Platform. Ogni attributo calcolato è un attributo di profilo creato nello schema di unione profili e viene raggruppato nel gruppo di campi &quot;Attributo calcolato&quot; nello schema di unione.

I casi d’uso di esempio includono la personalizzazione degli annunci con il nome dell’ultimo prodotto visualizzato per le persone che non hanno effettuato acquisti negli ultimi 7 giorni, la personalizzazione delle e-mail di marketing con punti premio totali ottenuti per congratularsi con gli utenti per essere stati promossi a un livello premium o il calcolo del valore del ciclo di vita di ciascun cliente per favorire un targeting migliore.

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
| MOST_RECENT | Funzione che trova il valore di attributo specificato dall’evento qualificato più recente. | Tutti i valori primitivi, matrici di valori primitivi | Ultimo prodotto visualizzato negli ultimi 7 giorni |

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
>Sia le settimane che i mesi sono considerati **settimane di calendario** e **mesi calendario** quando utilizzato nei lookback di eventi.

**Aggiornamento rapido**

>[!IMPORTANT]
>
>Massimo di **cinque** per gli attributi, in base alla sandbox, può essere abilitato l’aggiornamento rapido.

L’aggiornamento rapido consente di mantenere aggiornati gli attributi. L’abilitazione di questa opzione consente di aggiornare gli attributi calcolati su base giornaliera, anche per periodi di lookback più lunghi. Questo consente di reagire alle attività degli utenti quasi in tempo reale. Questo valore è applicabile solo per gli attributi calcolati con un periodo di lookback superiore a una base settimanale.

>[!NOTE]
>
>L’abilitazione dell’aggiornamento rapido varia la durata del lookback dell’evento, in quanto il periodo di lookback viene riavviato rispettivamente su base settimanale o mensile.
>
>Ad esempio, se crei un attributo calcolato con un periodo di lookback di due settimane con aggiornamento rapido abilitato, il periodo di lookback iniziale sarà di due settimane. Tuttavia, con ogni aggiornamento giornaliero, il periodo di lookback includerà gli eventi del giorno aggiuntivo. L’aggiunta di giorni continuerà fino all’inizio della settimana di calendario successiva, durante la quale l’intervallo di lookback verrà rinnovato e tornerà a due settimane.

## Passaggi successivi

Per ulteriori informazioni sulla creazione e la gestione degli attributi calcolati, consultare [guida API per attributi calcolati](./api.md) o [guida dell’interfaccia utente per attributi calcolati](./ui.md).
