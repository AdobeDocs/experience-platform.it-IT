---
title: Guida al dashboard dei profili account
description: Adobe Experience Platform fornisce una dashboard attraverso la quale puoi visualizzare informazioni importanti sui profili dell’account B2B della tua organizzazione.
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 79966442f5333363216da17342092a71335a14f0
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 0%

---

# [!UICONTROL Profili account] dashboard

L’interfaccia utente di Adobe Experience Platform fornisce una dashboard attraverso la quale puoi visualizzare informazioni importanti sui profili dell’account, acquisite durante un’istantanea giornaliera. Questa guida illustra come accedere e utilizzare [!UICONTROL Profili account] nell’interfaccia utente e fornisce ulteriori informazioni sulle visualizzazioni visualizzate nel dashboard.

Per una panoramica di tutte le funzioni all’interno dell’interfaccia utente del profilo dell’account, visita [guida dell’interfaccia utente del profilo account](../../rtcdp/accounts/account-profile-ui-guide.md).

## Introduzione

Devi avere diritto a [Adobe Real-time Customer Data Platform B2B Edition](../../rtcdp/b2b-overview.md) per accedere al B2B [!UICONTROL Profili account] dashboard.

## Dati dei profili account

Il [!UICONTROL Profili account] la dashboard mostra un’istantanea delle informazioni unificate sull’account provenienti dalle diverse origini nei vari canali di marketing e nei diversi sistemi attualmente utilizzati dalla tua organizzazione per archiviare le informazioni sull’account del cliente.

I dati di profilo nello snapshot mostrano i dati esattamente come vengono visualizzati nel momento specifico in cui lo snapshot è stato creato. In altre parole, l&#39;istantanea non è un&#39;approssimazione o un campione dei dati e [!UICONTROL Profili account] la dashboard non viene aggiornata in tempo reale.

>[!NOTE]
>
>Eventuali modifiche o aggiornamenti apportati ai dati dal momento in cui è stata acquisita l’istantanea non verranno riflessi nel dashboard fino all’acquisizione dell’istantanea successiva.

## Esplora [!UICONTROL Profili account] dashboard

Per passare al [!UICONTROL Profili account] nell’interfaccia utente di Platform, seleziona **[!UICONTROL Profili]** in [!UICONTROL Account] nel pannello di navigazione a sinistra.

![L’interfaccia utente di Platform con i Profili account nella barra di navigazione a sinistra è evidenziata e viene visualizzata la scheda Panoramica.](../images/account-profiles/account-profiles-dashboard.png)

Dalla sezione [!UICONTROL Profili account] dashboard è possibile: [sfoglia i profili account acquisiti nell’organizzazione](#browse-account-profiles), o [visualizzare immediatamente tutti i dati del profilo account utilizzando i widget](#standard-widgets) che visualizzano aspetti dei dati.

## Sfogliare i profili account {#browse-account-profiles}

Il [!UICONTROL Sfoglia] Questa scheda ti consente di cercare e visualizzare i profili di account di sola lettura acquisiti nell’organizzazione utilizzando un ID account da un’origine enterprise connessa o immettendo direttamente i dettagli dell’origine. Da qui puoi vedere informazioni importanti appartenenti al profilo dell’account, tra cui nome, settore, ricavi e pubblico.

Seleziona la [!UICONTROL ID profilo] dai risultati visualizzati sul [!UICONTROL Sfoglia] per aprire [!UICONTROL Dettagli] per il profilo dell’account.

![La scheda Sfoglia profili account presenta i risultati ed evidenzia l’ID profilo.](../images/account-profiles/account-profiles-browse-tab.png)

Le informazioni sul profilo account visualizzate nel [!UICONTROL Dettagli] La scheda è stata unita da più frammenti di profilo per formare un’unica vista del singolo account. Consulta la documentazione su [esplorazione dei profili account in Adobe Real-time Customer Data Platform](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) per ulteriori informazioni sulle funzionalità di visualizzazione del profilo account nell’interfaccia utente di Platform.

## Il [!UICONTROL Profili account] [!UICONTROL Panoramica] {#overview}

Il [!UICONTROL Panoramica] La scheda è composta da widget che forniscono metriche di sola lettura per trasmettere informazioni importanti sui profili dell’account. Seleziona **[!UICONTROL Modifica dashboard]** per modificare l&#39;aspetto del [!UICONTROL Panoramica] spostando e ridimensionando i widget.

![La scheda Panoramica dei profili account con la dashboard Modifica evidenziata.](../images/account-profiles/modify-dashboard.png)

Consulta il documento su [modifica delle dashboard](../customize/modify.md) e [Panoramica della libreria dei widget](../customize/widget-library.md) per ulteriori informazioni.

## Widget standard {#standard-widgets}

Questo Adobe fornisce widget standard che puoi utilizzare per visualizzare diverse metriche relative ai profili del tuo account.

Per ulteriori informazioni su ciascuno dei widget standard disponibili, selezionare il nome di un widget dall&#39;elenco seguente:

* [Totale account per settore](#total-accounts-by-industry)
* [Profili account aggiunti](#account-profiles-added)
* [Distribuzione del punteggio predittivo](#predictive-scoring-distribution)
* [Fattori influenti principali con punteggio predittivo](#predictive-scoring-top-influential-factors)

### Totale account per settore {#total-accounts-by-industry}

Questo widget visualizza il numero totale di conti in una singola metrica e utilizza un grafico ad anello per illustrare le dimensioni proporzionali dei conteggi per i settori che compongono il numero complessivo. La chiave fornisce informazioni di codifica del colore per i diversi settori che compongono il grafico ad anello.

I conteggi individuali per i diversi settori vengono visualizzati in una finestra di dialogo quando il cursore passa sopra la rispettiva sezione del grafico ad anello.

![Il totale dei conti per widget di settore.](../images/account-profiles/total-accounts-by-industry-widget.png)

### Profili account aggiunti {#account-profiles-added}

Questo widget utilizza un grafico a barre codificato a colori per illustrare il numero di profili aggiunti a un account in un determinato periodo di tempo e la proporzione di settori diversi che costituiscono questi profili aggiunti. I settori sono contraddistinti da colori diversi e una chiave fornisce le informazioni di codifica dei colori per i diversi settori che compongono il grafico a barre. Il periodo di analisi viene selezionato dal menu a discesa del widget. Il grafico a barre può essere visualizzato in un periodo di 30 giorni, 90 giorni e 12 mesi.

>[!NOTE]
>
>Poiché i profili vengono aggiunti solo a un account e non vengono mai rimossi, il numero più basso possibile di profili aggiunti in un periodo di tempo è zero.

![Il widget Profili account aggiunto.](../images/account-profiles/accounts-profiles-added-widget.png)

### Distribuzione del punteggio predittivo {#predictive-scoring-distribution}

Il [!UICONTROL Distribuzione del punteggio predittivo] widget mostra la distribuzione del punteggio di tutti i profili di account per aiutarti a comprendere lo stato della pipeline delle vendite in breve. I dati di punteggio vengono trasmessi attraverso un grafico ad anello e un istogramma.

Il grafico ad anello illustra la proporzione dei profili di conto totali in ciascuno dei periodi fissi di propensione elevata, media e bassa all’acquisto. La chiave fornisce ulteriori dettagli sulle sezioni codificate per colore, inclusi gli intervalli di bucket di punteggio e il numero di profili account in tale intervallo.

L’istogramma fornisce una suddivisione più granulare del punteggio. Ogni colonna mostra il numero di profili conto in ciascuno dei 20 bucket con incrementi di cinque punti.

Il menu a discesa all’interno del widget consente di selezionare il modello di punteggio dell’account.

![Il widget Distribuzione punteggio predittivo.](../images/account-profiles/predictive-scoring-distribution.png)

### Fattori influenti principali con punteggio predittivo {#predictive-scoring-top-influential-factors}

Il [!UICONTROL Fattori influenti principali con punteggio predittivo] widget consente di comprendere i fattori più significativi che determinano i punteggi per ogni bucket di propensione.

Questo widget mostra i principali fattori di influenza per ciascuno dei bucket di propensione alta, media e bassa. Una barra per ciascun fattore influente indica la percentuale dei profili conto in quel bucket di propensione che contiene il fattore influente specifico.

Il menu a discesa all’interno del widget consente di selezionare il modello di punteggio dell’account.

![Widget dei fattori influenti principali con punteggio predittivo.](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## Passaggi successivi

Seguendo questo documento, ora dovresti sapere come individuare [!UICONTROL Profili account] dashboard. Dovresti anche comprendere le metriche visualizzate nei widget disponibili. Per ulteriori informazioni sull’utilizzo dei profili account come parte dei dati B2B nell’interfaccia utente di Experienci Platform, consulta [panoramica dei profili account](../../rtcdp/accounts/account-profile-overview.md) per Adobe Real-Time CDP, edizione B2B.
