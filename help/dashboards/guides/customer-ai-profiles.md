---
title: Widget di IA per l’analisi dei clienti della dashboard dei profili
description: Scopri in che modo IA per l’analisi dei clienti fornisce informazioni importanti sull’abbandono o la propensione all’utilizzo dei dati Real-Time Customer Profile della tua organizzazione.
hide: true
hidefromtoc: true
source-git-commit: 162ef470751b9fb252658cff4b43595ddb7fe5d5
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 2%

---

# Widget di IA per l’analisi dei clienti della dashboard dei profili {#customer-ai-profiles-widgets}

Customer AI viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su grande scala. IA per l’analisi dei clienti esegue questa operazione analizzando i dati esistenti dell’evento esperienza del consumatore per prevedere **punteggi di tendenza di abbandono o conversione**. Questi modelli di propensione dei clienti ad alta precisione consentono segmentazione e targeting più precisi. Il [distribuzione dei punteggi](#customer-ai-distribution-of-scores) e [riepilogo punteggio](#customer-ai-scoring-summary) approfondimenti dimostrano la divisione del pubblico. Evidenzia quali profili hanno una propensione elevata/bassa/media e come sono distribuiti nei conteggi dei profili.

<!-- 
The links when required:
* [[!UICONTROL Customer AI scoring summary]](#customer-ai-scoring-summary)
* [[!UICONTROL Customer AI distribution of scores]](#customer-ai-distribution-of-scores) 
-->

## [!UICONTROL Distribuzione dei punteggi in IA per l’analisi dei clienti] {#customer-ai-distribution-of-scores}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_distributionOfScores"
>title="Distribuzione dei punteggi"
>abstract="Questo widget visualizza la distribuzione del numero totale di profili in base ai punteggi di tendenza, con incrementi del 5%. La distribuzione del conteggio dei profili è determinata dal modello di IA e dal criterio di unione selezionati. Puoi modificare il modello di IA dal menu a discesa sotto il titolo del widget."

Il [!UICONTROL Distribuzione dei punteggi in IA per l’analisi dei clienti] il widget categorizza il numero totale di profili in base ai loro punteggi di propensione. La distribuzione del conteggio dei profili è determinata dal modello di IA e dal criterio di unione selezionato, quindi viene visualizzata con incrementi del 5% che ne indicano la propensione. Il conteggio dei profili viene fornito lungo l’asse Y e i punteggi di propensione vengono forniti lungo l’asse X.

>[!NOTE]
>
>Se la visualizzazione è un punteggio di propensione alla conversione, i punteggi alti sono in verde e quelli bassi in rosso. Se prevedi una propensione all’abbandono, questo viene capovolto, i punteggi alti sono in rosso e i punteggi bassi in verde. Il bucket medio rimane giallo indipendentemente dal tipo di propensione scelto.

Il modello di intelligenza artificiale che determina i punteggi di tendenza viene scelto dal selettore a discesa sotto il titolo del widget. Il menu a discesa contiene un elenco di tutti i modelli di IA per l’analisi dei clienti configurati. Seleziona il modello di intelligenza artificiale appropriato per l’analisi dall’elenco dei modelli disponibili. Se non è disponibile alcun modello di IA per l’analisi dei clienti, un messaggio all’interno del widget indica di configurare almeno un modello di IA per l’analisi dei clienti e fornisce un collegamento ipertestuale alla pagina di configurazione del modello di IA per l’analisi dei clienti. Per istruzioni su, consulta la documentazione di [come configurare un’istanza di Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md).

>[!NOTE]
>
>Seleziona il menu a discesa immediatamente sotto la scheda della panoramica per modificare il criterio di unione che determina quali profili includere nell’analisi. Consulta la sezione su [criteri di unione](#merge-policies) per una breve descrizione o [panoramica dei criteri di unione](../../profile/merge-policies/overview.md) per ulteriori dettagli.

Per passare alla pagina approfondimenti dettagliata per il modello di IA per l’analisi dei clienti selezionato, seleziona **[!UICONTROL Visualizza dettagli modello]**.

![Il dashboard Tipi di pubblico di Experience Platform con [!UICONTROL Distribuzione dei punteggi in IA per l’analisi dei clienti] widget [!UICONTROL Visualizza dettagli modello] evidenziato.](../images/segments/customer-ai-distribution-of-scores.png)

Viene visualizzata la pagina dettagliata Approfondimenti modello.

![La pagina delle informazioni per IA per l’analisi dei clienti.](../images/profiles/customer-ai-insights-page.png)

Ulteriori informazioni su Customer AI sono disponibili sul sito [guida all’interfaccia utente di insights](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

## [!UICONTROL Riepilogo punteggio di Customer AI] {#customer-ai-scoring-summary}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_scoringSummary"
>title="Riepilogo punteggio"
>abstract="Questo widget visualizza il numero totale di profili con punteggio e li categorizza in contenitori contenenti propensione alta, media e bassa. Il grafico ad anello illustra la composizione proporzionale dei profili totali con propensione alta, media e bassa."

Questo widget visualizza il numero totale di profili valutati e li categorizza in contenitori contenenti propensione alta, media e bassa rispettivamente come verde, giallo e rosso. Un grafico ad anello illustra la composizione proporzionale dei profili tra propensione alta, media e bassa. Un profilo può avere una propensione elevata superiore a 75, una propensione media compresa tra 25 e 74 e una bassa propensione inferiore a 24. Una legenda indica il codice del colore e le soglie di propensione. I conteggi dei profili per le propensione alta, media e bassa vengono visualizzati in una finestra di dialogo quando il cursore passa sopra la rispettiva sezione del grafico ad anello.

>[!NOTE]
>
>Se la visualizzazione è un punteggio di propensione alla conversione, i punteggi alti sono in verde e quelli bassi in rosso. Se prevedi una propensione all’abbandono, questo viene capovolto, i punteggi alti sono in rosso e i punteggi bassi in verde. Il bucket medio rimane giallo indipendentemente dal tipo di propensione scelto.

Il menu a discesa sotto il titolo del widget fornisce un elenco di tutti i modelli di IA per l’analisi dei clienti configurati. Seleziona il modello di intelligenza artificiale appropriato per l’analisi dall’elenco dei modelli disponibili. Se non è disponibile alcun modello di IA per l’analisi dei clienti, un messaggio all’interno del widget indica di configurare almeno un modello di IA per l’analisi dei clienti e fornisce un collegamento ipertestuale alla pagina di configurazione del modello di IA per l’analisi dei clienti. Consulta la documentazione su [come configurare un’istanza di Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md) per istruzioni dettagliate.

>[!NOTE]
>
>Il numero totale di profili calcolati dipende dal criterio di unione scelto. Per modificare il criterio di unione utilizzato, seleziona il menu a discesa immediatamente sotto la scheda della panoramica. Consulta la sezione su [criteri di unione](#merge-policies) per una breve descrizione o [panoramica dei criteri di unione](../../profile/merge-policies/overview.md) per ulteriori dettagli.

![La dashboard Tipi di pubblico di Experience Platform con il widget di riepilogo del punteggio di IA per l’analisi dei clienti evidenziato.](../images/segments/customer-ai-scoring-summary.png)

Per passare alla pagina approfondimenti dettagliata per il modello di IA per l’analisi dei clienti selezionato, seleziona **[!UICONTROL Visualizza dettagli modello]**. Ulteriori informazioni su Customer AI sono disponibili sul sito [guida all’interfaccia utente di insights](../../intelligent-services/customer-ai/user-guide/discover-insights.md).