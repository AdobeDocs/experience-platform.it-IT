---
title: Dashboard dei profili account
description: Adobe Experience Platform fornisce una dashboard attraverso la quale puoi visualizzare informazioni importanti sui profili dell’account B2B della tua organizzazione.
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 8b6cd84a31f9cdccef9f342df7f7b8450c2405dc
workflow-type: tm+mt
source-wordcount: '1800'
ht-degree: 0%

---

# [!UICONTROL Profili account] dashboard

L’interfaccia utente di Adobe Experience Platform fornisce una dashboard attraverso la quale puoi visualizzare informazioni importanti sui profili dell’account, acquisite durante un’istantanea giornaliera. Questa guida illustra come accedere e utilizzare [!UICONTROL Profili account] nell’interfaccia utente e fornisce ulteriori informazioni sulle visualizzazioni visualizzate nel dashboard.

Questo documento fornisce una panoramica delle funzioni di [!UICONTROL Profili account] dashboard e fornisce dettagli sulle informazioni standard disponibili. Consulta la [[!UICONTROL Profili account] Guida all’interfaccia utente](../../rtcdp/accounts/account-profile-ui-guide.md) per informazioni complete sulle funzioni disponibili.

## Introduzione

Devi avere diritto a [Adobe Real-time Customer Data Platform B2B Edition](../../rtcdp/b2b-overview.md) per accedere al B2B [!UICONTROL Profili account] dashboard.

## Dati dei profili account {#data}

Il [!UICONTROL Profili account] nel dashboard viene visualizzata un&#39;istantanea delle informazioni dell&#39;account unificato. Queste informazioni sull’account provengono dalle diverse origini nei vari canali di marketing e dai diversi sistemi attualmente utilizzati dalla tua organizzazione per archiviare le informazioni sull’account del cliente.

I dati di profilo nello snapshot mostrano i dati esattamente come vengono visualizzati nel momento specifico in cui lo snapshot è stato creato. In altre parole, l&#39;istantanea non è un&#39;approssimazione o un campione dei dati e [!UICONTROL Profili account] la dashboard non viene aggiornata in tempo reale.

>[!NOTE]
>
>Eventuali modifiche o aggiornamenti apportati ai dati dal momento in cui è stata acquisita l’istantanea non verranno riflessi nel dashboard fino all’acquisizione dell’istantanea successiva.

## Esplora [!UICONTROL Profili account] dashboard {#explore}

Per passare al [!UICONTROL Profili account] nell’interfaccia utente di Platform, seleziona **[!UICONTROL Profili]** in [!UICONTROL Account] nel pannello di navigazione a sinistra.

![L’interfaccia utente di Platform con i Profili account nella barra di navigazione a sinistra è evidenziata e viene visualizzata la scheda Panoramica.](../images/account-profiles/account-profiles-dashboard.png)

Dalla sezione [!UICONTROL Profili account] dashboard, puoi effettuare le seguenti operazioni [sfoglia i profili account acquisiti nell’organizzazione](#browse-account-profiles), o [visualizzare immediatamente tutti i dati del profilo account utilizzando i widget](#standard-widgets).

### Filtro data {#date-filter}

Il [!UICONTROL Panoramica] La scheda è composta da widget che forniscono metriche di sola lettura per trasmettere informazioni importanti sui profili dell’account. Seleziona l&#39;icona o le date del calendario per modificare il filtro data globale per i widget.

>[!IMPORTANT]
>
>L’intervallo di date selezionato nel calendario a discesa influisce su tutte le informazioni eccetto i due widget di punteggio predittivo ([distribuzione](#predictive-scoring-distribution) e [principali fattori influenti](#predictive-scoring-top-influential-factors)).

![La scheda Panoramica dei profili account con il selettore di data e l’icona del filtro evidenziati.](../images/account-profiles/date-filter.png)

### Configurare il lead per il servizio di corrispondenza account {#lead-to-account-matching-service}

Seleziona **[!UICONTROL Impostazioni]** per configurare il lead per il servizio di corrispondenza account da [!UICONTROL Impostazioni account] . Per informazioni complete su come configurare la corrispondenza tra lead e account, vedi [Guida all’interfaccia utente](../../rtcdp/accounts/account-profile-ui-guide.md#configure-lead-to-account-matching). Per ulteriori informazioni sulla corrispondenza tra lead e account, consulta [lead per corrispondenza account nella documentazione B2B di Real-Time CDP](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

![La dashboard Profili account con le impostazioni evidenziate.](../images/account-profiles/settings.png)

## Sfogliare i profili account {#browse-account-profiles}

Dalla sezione [!UICONTROL Sfoglia] , puoi cercare e visualizzare i profili dell’account di sola lettura acquisiti nell’organizzazione. Utilizzare un ID account da un&#39;origine aziendale connessa oppure immettere direttamente i dettagli dell&#39;origine. Da questa area di lavoro puoi visualizzare informazioni importanti appartenenti al profilo dell’account, tra cui nome, settore, ricavi e pubblico.

Seleziona la [!UICONTROL ID profilo] dai risultati visualizzati sul [!UICONTROL Sfoglia] per aprire [!UICONTROL Dettagli] per il profilo dell’account.

![La scheda Sfoglia profili account presenta i risultati ed evidenzia l’ID profilo.](../images/account-profiles/account-profiles-browse-tab.png)

Le informazioni sul profilo account visualizzate nel [!UICONTROL Dettagli] La scheda è stata unita da più frammenti di profilo per formare un’unica vista del singolo account. Consulta la documentazione su [esplorazione dei profili account in Adobe Real-time Customer Data Platform](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) per ulteriori informazioni sulle funzionalità di visualizzazione del profilo account nell’interfaccia utente di Platform.

## Widget standard {#standard-widgets}

Questo Adobe fornisce widget standard che puoi utilizzare per visualizzare diverse metriche relative ai profili del tuo account.

>[!IMPORTANT]
>
>Se non fornisci un filtro per date, il comportamento predefinito di Insights analizza i dati aggiunti dall’anno precedente fino a oggi.

Per ulteriori informazioni su ciascuno dei widget standard disponibili, selezionare il nome di un widget dall&#39;elenco seguente:

* [Profili account aggiunti](#account-profiles-added)
* [Nuovi account per settore](#accounts-by-industry)
* [Nuovi account per tipo](#accounts-by-type)
* [Opportunità aggiunte](#opportunities-added)
* [Nuove opportunità per ruolo persona](#opportunities-by-person-role)
* [Nuove opportunità in base ai ricavi](#opportunities-by-revenue)
* [Nuove opportunità per stato e fase](#opportunities-by-status-&-stage)
* [Nuove opportunità realizzate](#opportunities-won)
* [Distribuzione del punteggio predittivo](#predictive-scoring-distribution)
* [Fattori influenti principali con punteggio predittivo](#predictive-scoring-top-influential-factors)
* [Totale account per settore](#total-accounts-by-industry)

### Profili account aggiunti {#account-profiles-added}

Il [!UICONTROL Profili account aggiunti] il widget utilizza un grafico a linee per visualizzare il numero di profili di conto aggiunti ogni giorno in un periodo di tempo. Utilizza il filtro data globale che si trova nella parte superiore del dashboard per determinare il periodo di analisi. Se non viene fornito alcun filtro di data, il comportamento predefinito elenca i profili di account aggiunti per l’anno precedente a oggi. I risultati possono essere utilizzati per dedurre una tendenza nel numero di profili di account aggiunti.

![Il widget Profili account aggiunto.](../images/account-profiles/account-profiles-added.png)

### Nuovi account per settore {#accounts-by-industry}

Il [!UICONTROL Nuovi account per settore] widget mostra il numero totale di account in una singola metrica all’interno di un grafico ad anello. Il grafico ad anello illustra la composizione relativa dei diversi settori che compongono questo totale. Un codice colore fornisce una suddivisione di tutti i settori inclusi. I conteggi individuali per ciascun settore vengono visualizzati in una finestra di dialogo quando il cursore passa sopra la rispettiva sezione del grafico ad anello.

![I nuovi account per widget di settore.](../images/account-profiles/new-accounts-by-industry.png)

### Nuovi account per tipo {#accounts-by-type}

Il [!UICONTROL Nuovi account per tipo] widget mostra il numero totale di account in una singola metrica all’interno di un grafico ad anello. Il grafico ad anello illustra la composizione relativa dei diversi tipi di conto che compongono questo totale. Una chiave con codice colore fornisce un raggruppamento di tutti i tipi di conto inclusi. I conteggi individuali per ciascun tipo di account vengono visualizzati in una finestra di dialogo quando il cursore passa sopra la rispettiva sezione del grafico ad anello.

![Il widget Nuovi account per tipo.](../images/account-profiles/new-accounts-by-type.png)

### Opportunità aggiunte {#opportunities-added}

Il [!UICONTROL Opportunità aggiunte] il widget utilizza un grafico a linee per visualizzare il numero di opportunità aggiunte ogni giorno in un periodo di tempo. Utilizza il filtro data globale che si trova nella parte superiore del dashboard per determinare il periodo di analisi. Se non viene fornito alcun filtro di data, il comportamento predefinito elenca le opportunità aggiunte per l’anno precedente a oggi. I risultati possono essere utilizzati per dedurre una tendenza nel numero di opportunità aggiunte.

<!-- Link to date filter documentation from Annamalai -->

![Il widget Opportunità aggiunto.](../images/account-profiles/opportunities-added.png)

### Nuove opportunità per ruolo persona {#opportunities-by-person-role}

Il [!UICONTROL Nuove opportunità per ruolo persona] widget mostra il numero totale di opportunità in una singola metrica all’interno di un grafico ad anello. Il grafico ad anello illustra la composizione relativa dei ruoli che compongono questo numero totale di opportunità. Una chiave con codice colore fornisce un raggruppamento di tutti i ruoli inclusi. I conteggi individuali per ciascun ruolo vengono visualizzati in una finestra di dialogo quando il cursore passa sopra la rispettiva sezione del grafico ad anello.

>[!NOTE]
>
>Il [!UICONTROL Nessun dato trovato] o [!UICONTROL Impossibile caricare] si verifica un errore quando la tabella bridge &quot;Opportunity-Person&quot; non viene utilizzata nello schema. Se la tua informazione mostra uno di questi errori, controlla lo schema di unione e assicurati che il gruppo di campi &quot;Opportunità-Persona&quot; acquisisca i dati.

![Il widget Nuove opportunità per ruolo persona.](../images/account-profiles/new-opportunities-by-person-role.png)

### Nuove opportunità in base ai ricavi {#opportunities-by-revenue}

Il [!UICONTROL Nuove opportunità in base ai ricavi] widget utilizza un grafico a barre per illustrare la quantità totale stimata di ricavi generati dalle opportunità. Il widget supporta fino a sei opportunità.

Per visualizzare una finestra di dialogo contenente il totale dei ricavi specifici di un’opportunità, utilizza il cursore per passare il puntatore del mouse sulle singole barre.

![Il widget Nuove opportunità per ricavi.](../images/account-profiles/new-opportunities-by-revenue.png)

### Nuove opportunità per stato e fase {#opportunities-by-status-&-stage}

Questo widget utilizza un grafico a barre per illustrare il numero di opportunità aperte o chiuse in tutte le fasi del funnel marketing/vendite. Il widget utilizza i colori per differenziare lo stadio delle opportunità. Una chiave con codice colore indica le fasi disponibili per le opportunità.

![Il widget Nuove opportunità per stato e fase.](../images/account-profiles/new-opportunities-by-status-&-stage.png)

### Nuove opportunità realizzate {#opportunities-won}

Il [!UICONTROL Nuove opportunità realizzate] widget mostra il numero totale di opportunità finalizzate correttamente in una singola metrica all’interno di un grafico ad anello. Il grafico ad anello illustra la composizione relativa delle opportunità che vengono vinte o meno. Una chiave con codice colore distingue tra opportunità realizzate e opportunità non realizzate. I conteggi individuali per ciascun ruolo vengono visualizzati in una finestra di dialogo quando il cursore passa sopra la rispettiva sezione del grafico ad anello.

![Il widget Nuove opportunità ha vinto.](../images/account-profiles/new-opportunities-won.png)

### Distribuzione del punteggio predittivo {#predictive-scoring-distribution}

Il [!UICONTROL Distribuzione del punteggio predittivo] widget mostra la distribuzione del punteggio di tutti i profili di account per aiutarti a comprendere lo stato della pipeline delle vendite in breve. I dati di punteggio vengono trasmessi attraverso un grafico ad anello e un istogramma.

Il grafico ad anello illustra la proporzione dei profili di conto totali in ciascuno dei periodi fissi di propensione elevata, media e bassa all’acquisto. La chiave fornisce ulteriori dettagli sulle sezioni codificate per colore, inclusi gli intervalli di bucket di punteggio e il numero di profili account in tale intervallo.

L’istogramma fornisce una suddivisione più granulare del punteggio. Ogni colonna mostra il numero di profili conto in ciascuno dei 20 bucket con incrementi di cinque punti.

Il menu a discesa all’interno del widget consente di selezionare il modello di punteggio dell’account.

>[!NOTE]
>
>I filtri per l’intervallo di date globale non si applicano agli approfondimenti di valutazione predittiva. I widget con punteggio predittivo analizzano i dati in base al modello di punteggio dell’account selezionato nel menu a discesa.

![Il widget Distribuzione punteggio predittivo.](../images/account-profiles/predictive-scoring-distribution.png)

### Fattori influenti principali con punteggio predittivo {#predictive-scoring-top-influential-factors}

Il [!UICONTROL Fattori influenti principali con punteggio predittivo] widget consente di comprendere i fattori più significativi che determinano i punteggi per ogni bucket di propensione.

Questo widget mostra i principali fattori di influenza per ciascuno dei bucket di propensione alta, media e bassa. Una barra per ciascun fattore influente indica la percentuale dei profili conto in quel bucket di propensione che contiene il fattore influente specifico.

Il menu a discesa all’interno del widget consente di selezionare il modello di punteggio dell’account.

>[!NOTE]
>
>I filtri per l’intervallo di date globale non si applicano agli approfondimenti di valutazione predittiva. I widget con punteggio predittivo analizzano i dati in base al modello di punteggio dell’account selezionato nel menu a discesa.

![Widget dei fattori influenti principali con punteggio predittivo.](../images/account-profiles/predictive-scoring-top-influential-factors.png)

### Totale account per settore {#total-accounts-by-industry}

Questo widget visualizza il numero totale di conti in una singola metrica e utilizza un grafico ad anello per illustrare le dimensioni proporzionali dei conteggi per i settori che compongono il numero complessivo. La chiave fornisce informazioni di codifica del colore per i diversi settori che compongono il grafico ad anello.

>[!NOTE]
>
>Le informazioni visualizzate da questa informazione dipendono dall’intervallo di date specificato dall’utente. Se non fornisci un filtro per date, il comportamento predefinito di Insight analizza i dati aggiunti dall’anno precedente fino a oggi.

I conteggi individuali per i diversi settori vengono visualizzati in una finestra di dialogo quando il cursore passa sopra la rispettiva sezione del grafico ad anello.

![Il totale dei conti per widget di settore.](../images/account-profiles/total-accounts-by-industry-widget.png)

## Passaggi successivi

Seguendo questo documento, ora dovresti sapere come individuare [!UICONTROL Profili account] e comprendere anche le metriche visualizzate nei widget disponibili. Per ulteriori informazioni sull’utilizzo dei profili account come parte dei dati B2B nell’interfaccia utente di Experienci Platform, consulta [panoramica dei profili account](../../rtcdp/accounts/account-profile-overview.md) per Adobe Real-Time CDP, edizione B2B.
