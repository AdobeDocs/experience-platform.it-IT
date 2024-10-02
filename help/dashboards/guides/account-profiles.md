---
title: Dashboard dei profili account
description: Adobe Experience Platform fornisce una dashboard attraverso la quale puoi visualizzare informazioni importanti sui profili dell’account B2B della tua organizzazione.
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 8caa10010109f9936271cb45a2166455f3678687
workflow-type: tm+mt
source-wordcount: '1827'
ht-degree: 1%

---

# Dashboard dei profili account

L’interfaccia utente di Adobe Experience Platform fornisce una dashboard attraverso la quale puoi visualizzare informazioni importanti sui profili dell’account, acquisite durante un’istantanea giornaliera. Questa guida illustra come accedere e lavorare con il dashboard [!UICONTROL Profili account] nell&#39;interfaccia utente e fornisce ulteriori informazioni sulle visualizzazioni visualizzate nel dashboard.

In questo documento viene fornita una panoramica delle funzionalità della dashboard [!UICONTROL Profili account] e vengono fornite informazioni dettagliate sulle informazioni standard disponibili. Per informazioni dettagliate complete sulle funzioni disponibili, consulta la [[!UICONTROL Guida dell&#39;interfaccia utente ]](../../rtcdp/accounts/account-profile-ui-guide.md).

## Introduzione

Devi avere diritto a [Adobe Real-time Customer Data Platform B2B Edition](../../rtcdp/b2b-overview.md) per accedere al dashboard [!UICONTROL Profili account] B2B.

## Dati dei profili account {#data}

Nel dashboard [!UICONTROL Profili account] viene visualizzata un&#39;istantanea delle informazioni dell&#39;account unificato. Queste informazioni sull’account provengono dalle diverse origini nei vari canali di marketing e dai diversi sistemi attualmente utilizzati dalla tua organizzazione per archiviare le informazioni sull’account del cliente.

I dati di profilo nello snapshot mostrano i dati esattamente come vengono visualizzati nel momento specifico in cui lo snapshot è stato creato. In altre parole, lo snapshot non è un&#39;approssimazione o un esempio dei dati e il dashboard [!UICONTROL Profili account] non viene aggiornato in tempo reale.

>[!NOTE]
>
>Eventuali modifiche o aggiornamenti apportati ai dati dal momento in cui è stata acquisita l’istantanea non verranno riflessi nel dashboard fino all’acquisizione dell’istantanea successiva.

## Esplora il dashboard [!UICONTROL Profili account] {#explore}

Per passare alla dashboard [!UICONTROL Profili account] nell&#39;interfaccia utente di Platform, selezionare **[!UICONTROL Profili]** in [!UICONTROL Account] nel pannello di navigazione a sinistra.

![L&#39;interfaccia utente di Platform con i profili account nella barra di navigazione a sinistra è evidenziata e la scheda Panoramica è visualizzata.](../images/account-profiles/account-profiles-dashboard.png)

Dal dashboard [!UICONTROL Profili account], puoi [sfogliare i profili account acquisiti nell&#39;organizzazione](#browse-account-profiles) oppure [visualizzare tutti i dati del profilo account in modo immediato utilizzando i widget](#standard-widgets).

### Filtro data {#date-filter}

La scheda [!UICONTROL Panoramica] è composta da widget che forniscono metriche di sola lettura per trasmettere informazioni importanti sui profili dell&#39;account. Seleziona l&#39;icona o le date del calendario per modificare il filtro data globale per i widget.

>[!IMPORTANT]
>
>L&#39;intervallo di date selezionato nel calendario a discesa influisce su tutte le informazioni tranne i due widget di punteggio predittivo ([distribuzione](#predictive-scoring-distribution) e [fattori influenti principali](#predictive-scoring-top-influential-factors)).

![Scheda Panoramica dei profili account con il selettore di data e l&#39;icona del filtro evidenziati.](../images/account-profiles/date-filter.png)

### Configurare il lead per il servizio di corrispondenza account {#lead-to-account-matching-service}

Seleziona **[!UICONTROL Impostazioni]** per configurare il lead per il servizio di corrispondenza account dalla finestra di dialogo [!UICONTROL Impostazioni account]. Per informazioni dettagliate su come configurare la corrispondenza tra lead e account, consulta la [guida dell&#39;interfaccia utente](../../rtcdp/accounts/account-profile-ui-guide.md#configure-lead-to-account-matching). Per ulteriori informazioni sulla corrispondenza lead-account, consulta [lead-account matching nella documentazione di Real-Time CDP B2B](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

![Dashboard dei profili account con impostazioni evidenziate.](../images/account-profiles/settings.png)

## Sfogliare i profili account {#browse-account-profiles}

Dalla scheda [!UICONTROL Sfoglia], puoi cercare e visualizzare i profili dell&#39;account di sola lettura acquisiti nell&#39;organizzazione. Utilizzare un ID account da un&#39;origine aziendale connessa oppure immettere direttamente i dettagli dell&#39;origine. Da questa area di lavoro puoi visualizzare informazioni importanti appartenenti al profilo dell’account, tra cui nome, settore, ricavi e pubblico.

Seleziona [!UICONTROL ID profilo] dai risultati visualizzati nella scheda [!UICONTROL Sfoglia] per aprire la scheda [!UICONTROL Dettagli] per il profilo account.

![Scheda Sfoglia profili account con i risultati visualizzati e l&#39;ID profilo evidenziato.](../images/account-profiles/account-profiles-browse-tab.png)

Le informazioni sul profilo account visualizzate nella scheda [!UICONTROL Dettagli] sono state unite da più frammenti di profilo per formare un&#39;unica visualizzazione del singolo account. Per ulteriori informazioni sulle funzionalità di visualizzazione dei profili dell&#39;account nell&#39;interfaccia utente di Platform, consulta la documentazione su [esplorazione dei profili dell&#39;account in Adobe Real-time Customer Data Platform](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles).

## Widget standard {#standard-widgets}

>[!CONTEXTUALHELP]
>id="platform_dashboards_accountprofiles_customersperaccountoverview"
>title="Panoramica sui clienti per account"
>abstract="Questo widget drill-through fornisce informazioni sulla struttura dei dati B2B. Consente di identificare quanti profili account non hanno profili cliente collegati o a cui sono associati uno o più profili cliente.<ul><li>Clienti diretti: sono profili cliente collegati direttamente a un account tramite il percorso `personComponents`.</li><li>Clienti indiretti: sono profili cliente collegati a un account tramite il percorso `Account-Person`.</li></ul>"

Questo Adobe fornisce widget standard che puoi utilizzare per visualizzare diverse metriche relative ai profili del tuo account.

>[!IMPORTANT]
>
>Se non fornisci un filtro per date, il comportamento predefinito di Insights analizza i dati aggiunti dall’anno precedente fino a oggi.

Per ulteriori informazioni su ciascuno dei widget standard disponibili, selezionare il nome di un widget dall&#39;elenco seguente:

* [Profili account aggiunti](#account-profiles-added)
* [Nuovi account per settore](#accounts-by-industry)
* [Nuovi account per tipo](#accounts-by-type)
* [Nuove opportunità per ruolo persona](#opportunities-by-person-role)
* [Nuove opportunità in base ai ricavi](#opportunities-by-revenue)
* [Nuove opportunità per stato e fase](#opportunities-by-status-&-stage)
* [Nuove opportunità realizzate](#opportunities-won)
* [Opportunità aggiunte](#opportunities-added)
* [Distribuzione del punteggio predittivo](#predictive-scoring-distribution)
* [Fattori influenti principali con punteggio predittivo](#predictive-scoring-top-influential-factors)

### Profili account aggiunti {#account-profiles-added}

Il widget [!UICONTROL Profili account aggiunti] utilizza un grafico a linee per visualizzare il numero di profili account aggiunti ogni giorno in un periodo di tempo. Utilizza il filtro data globale che si trova nella parte superiore del dashboard per determinare il periodo di analisi. Se non viene fornito alcun filtro di data, il comportamento predefinito elenca i profili di account aggiunti per l’anno precedente a oggi. I risultati possono essere utilizzati per dedurre una tendenza nel numero di profili di account aggiunti.

![Il widget dei profili account è stato aggiunto.](../images/account-profiles/account-profiles-added.png)

### Nuovi account per settore {#accounts-by-industry}

Il widget [!UICONTROL Nuovi account per settore] visualizza il numero totale di account in una singola metrica all&#39;interno di un grafico ad anello. Il grafico ad anello illustra la composizione relativa dei diversi settori che compongono questo totale. Un codice colore fornisce una suddivisione di tutti i settori inclusi. I conteggi individuali per ciascun settore vengono visualizzati in una finestra di dialogo quando il cursore passa sopra la rispettiva sezione del grafico ad anello.

![Nuovi account per widget settore.](../images/account-profiles/new-accounts-by-industry.png)

### Nuovi account per tipo {#accounts-by-type}

Il widget [!UICONTROL Nuovi account per tipo] visualizza il numero totale di account in una singola metrica all&#39;interno di un grafico ad anello. Il grafico ad anello illustra la composizione relativa dei diversi tipi di conto che compongono questo totale. Una chiave con codice colore fornisce un raggruppamento di tutti i tipi di conto inclusi. I conteggi individuali per ciascun tipo di account vengono visualizzati in una finestra di dialogo quando il cursore passa sopra la rispettiva sezione del grafico ad anello.

![Widget Nuovi account per tipo.](../images/account-profiles/new-accounts-by-type.png)

### Nuove opportunità per ruolo persona {#opportunities-by-person-role}

Il widget [!UICONTROL Nuove opportunità per ruolo persona] visualizza il numero totale delle opportunità in una singola metrica all&#39;interno di un grafico ad anello. Il grafico ad anello illustra la composizione relativa dei ruoli che compongono questo numero totale di opportunità. Una chiave con codice colore fornisce un raggruppamento di tutti i ruoli inclusi. I conteggi individuali per ciascun ruolo vengono visualizzati in una finestra di dialogo quando il cursore passa sopra la rispettiva sezione del grafico ad anello.

>[!NOTE]
>
>L&#39;errore [!UICONTROL Nessun dato trovato] o [!UICONTROL Impossibile caricare] si verifica quando la tabella del bridge &#39;Opportunity-Person&#39; non viene utilizzata nello schema. Se la tua informazione mostra uno di questi errori, controlla lo schema di unione e assicurati che il gruppo di campi &quot;Opportunità-Persona&quot; acquisisca i dati.

![Il widget Nuove opportunità per ruolo persona.](../images/account-profiles/new-opportunities-by-person-role.png)

### Nuove opportunità in base ai ricavi {#opportunities-by-revenue}

Il widget [!UICONTROL Nuove opportunità per ricavi] utilizza un grafico a barre per illustrare la quantità totale stimata di ricavi generati dalle opportunità. Il widget supporta fino a sei opportunità.

Per visualizzare una finestra di dialogo contenente il totale dei ricavi specifici di un’opportunità, utilizza il cursore per passare il puntatore del mouse sulle singole barre.

![Nuove opportunità per widget ricavi.](../images/account-profiles/new-opportunities-by-revenue.png)

### Nuove opportunità per stato e fase {#opportunities-by-status-&-stage}

Questo widget utilizza un grafico a barre per illustrare il numero di opportunità aperte o chiuse in tutte le fasi del funnel marketing/vendite. Il widget utilizza i colori per differenziare lo stadio delle opportunità. Una chiave con codice colore indica le fasi disponibili per le opportunità.

![Nuove opportunità per stato e widget area di visualizzazione.](../images/account-profiles/new-opportunities-by-status-&-stage.png)

### Nuove opportunità realizzate {#opportunities-won}

Il widget [!UICONTROL Nuove opportunità realizzate] mostra il numero totale di opportunità completate correttamente in una singola metrica all&#39;interno di un grafico ad anello. Il grafico ad anello illustra la composizione relativa delle opportunità che vengono vinte o meno. Una chiave con codice colore distingue tra opportunità realizzate e opportunità non realizzate. I conteggi individuali per ciascun ruolo vengono visualizzati in una finestra di dialogo quando il cursore passa sopra la rispettiva sezione del grafico ad anello.

![Il widget Nuove opportunità ha vinto.](../images/account-profiles/new-opportunities-won.png)

### Opportunità aggiunte {#opportunities-added}

Il widget [!UICONTROL Opportunità aggiunte] utilizza un grafico a linee per visualizzare il numero di opportunità aggiunte ogni giorno in un periodo di tempo. Utilizza il filtro data globale che si trova nella parte superiore del dashboard per determinare il periodo di analisi. Se non viene fornito alcun filtro di data, il comportamento predefinito elenca le opportunità aggiunte per l’anno precedente a oggi. I risultati possono essere utilizzati per dedurre una tendenza nel numero di opportunità aggiunte.

<!-- Link to date filter documentation from Annamalai -->

![Il widget Opportunità aggiunto.](../images/account-profiles/opportunities-added.png)

### Distribuzione del punteggio predittivo {#predictive-scoring-distribution}

Il widget [!UICONTROL Distribuzione con punteggio predittivo] mostra la distribuzione del punteggio di tutti i profili di account per consentirti di comprendere immediatamente lo stato della pipeline di vendita. I dati di punteggio vengono trasmessi attraverso un grafico ad anello e un istogramma.

Il grafico ad anello illustra la proporzione dei profili di conto totali in ciascuno dei periodi fissi di propensione elevata, media e bassa all’acquisto. La chiave fornisce ulteriori dettagli sulle sezioni codificate per colore, inclusi gli intervalli di bucket di punteggio e il numero di profili account in tale intervallo.

L’istogramma fornisce una suddivisione più granulare del punteggio. Ogni colonna mostra il numero di profili conto in ciascuno dei 20 bucket con incrementi di cinque punti.

Il menu a discesa all’interno del widget consente di selezionare il modello di punteggio dell’account.

>[!NOTE]
>
>I filtri per l’intervallo di date globale non si applicano agli approfondimenti di valutazione predittiva. I widget con punteggio predittivo analizzano i dati in base al modello di punteggio dell’account selezionato nel menu a discesa.

![Widget di distribuzione del punteggio predittivo.](../images/account-profiles/predictive-scoring-distribution.png)

### Fattori influenti principali con punteggio predittivo {#predictive-scoring-top-influential-factors}

Il widget [!UICONTROL Fattori influenti principali con punteggio predittivo] ti aiuta a comprendere i fattori più significativi che determinano i punteggi per ogni bucket di propensione.

Questo widget mostra i principali fattori di influenza per ciascuno dei bucket di propensione alta, media e bassa. Una barra per ciascun fattore influente indica la percentuale dei profili conto in quel bucket di propensione che contiene il fattore influente specifico.

Il menu a discesa all’interno del widget consente di selezionare il modello di punteggio dell’account.

>[!NOTE]
>
>I filtri per l’intervallo di date globale non si applicano agli approfondimenti di valutazione predittiva. I widget con punteggio predittivo analizzano i dati in base al modello di punteggio dell’account selezionato nel menu a discesa.

![Widget dei fattori influenti principali con punteggio predittivo.](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## Errore nell’operazione di caricamento dati {#errors}

Se viene visualizzato un widget *[!UICONTROL Impossibile caricare. Riprova.]* poiché non sono disponibili dati per l&#39;entità B2B. Ad esempio, il widget visualizzato di seguito [!UICONTROL Nuove opportunità per ruolo persona] mostra il messaggio &quot;[!UICONTROL Impossibile caricare. Riprova.]&quot; poiché questa sandbox non dispone di dati di opportunità disponibili.

![Errore Impossibile caricare l&#39;approfondimento.](../images/account-profiles/unable-to-load.png)

Per risolvere il problema, è necessario acquisire nella sandbox i dati dell&#39;entità B2B, ad esempio i dati di *persona opportunità*. Dopo 48 ore, i dati vengono riflessi nei widget.

## Passaggi successivi

Seguendo questo documento, ora dovresti sapere come individuare la dashboard [!UICONTROL Profili account] e capire le metriche visualizzate nei widget disponibili. Per ulteriori informazioni sull&#39;utilizzo dei profili account come parte dei dati B2B nell&#39;interfaccia utente di Experience Platform, consulta la [panoramica dei profili account](../../rtcdp/accounts/account-profile-overview.md) per Adobe Real-Time CDP, versione B2B.
