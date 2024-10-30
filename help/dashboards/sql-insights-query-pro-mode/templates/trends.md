---
title: Tendenze del pubblico
description: Scopri come tracciare e analizzare le metriche del pubblico nel tempo utilizzando la dashboard Tendenze pubblico. Imposta i filtri del pubblico, analizza le tendenze di dimensioni e identità ed esporta informazioni approfondite per le decisioni basate sui dati.
source-git-commit: 5fc786058a187b161a147a8bd361d19c5f35105d
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 1%

---

# Tendenze del pubblico

Analizza come cambiano i tipi di pubblico nel tempo con visualizzazioni delle metriche chiave del pubblico nella dashboard [!UICONTROL Tendenze pubblico]. Questa dashboard consente di tenere traccia di tendenze quali la crescita del pubblico, il numero di identità e il conteggio di profili di identità singoli, e ti consente di prendere decisioni basate sui dati. Analizzando queste metriche, gli esperti di marketing possono ottimizzare le strategie di targeting, migliorare il coinvolgimento del pubblico e perfezionare gli sforzi di segmentazione per campagne più efficaci.

## Filtrare i tipi di pubblico {#filter-audiences}

Per iniziare l’analisi, utilizza il filtro globale per selezionare i tipi di pubblico specifici e l’intervallo di date che desideri analizzare. Selezionare l&#39;icona filtro (![Icona filtro.](../../../images/icons/filter-icon-white.png)) per aprire la finestra di dialogo **[!UICONTROL Filtro]**, in cui è possibile:

1. **Seleziona un pubblico**: scegli il pubblico da analizzare (nella schermata di esempio, è stato selezionato il pubblico **Amoxicillin**).
1. **Imposta un intervallo di date**: scegli un intervallo predefinito dal menu a discesa o seleziona manualmente le date di inizio e di fine utilizzando i campi del calendario.

![Finestra di dialogo Filtri nel dashboard Tendenze pubblico.](../../images/sql-insights-query-pro-mode/templates/audience-trends-filters.png)

Dopo aver impostato i filtri, seleziona **[!UICONTROL Applica]** per aggiornare il dashboard. I filtri scelti vengono applicati e vengono visualizzate le informazioni mirate sui tipi di pubblico selezionati durante un determinato periodo di tempo. I filtri personalizzati garantiscono che i dati siano rilevanti per gli obiettivi di analisi.

![Dashboard delle tendenze del pubblico con filtro segmento Amoxicilin applicato ed evidenziato.](../../images/sql-insights-query-pro-mode/templates/audience-trends-applied-filters.png)

## Grafici di tendenza del pubblico disponibili {#available-charts}

Esistono tre grafici principali per comprendere le metriche del pubblico nel tempo. Per ogni grafico, è possibile selezionare l&#39;ellisse (`...`) in alto a destra seguita da [!UICONTROL Visualizza altro] per visualizzare una tabella dei risultati o scaricare i dati come file CSV da visualizzare in un foglio di calcolo. Per ulteriori dettagli, fare riferimento alla [Guida per ulteriori informazioni](../view-more.md).

>[!TIP]
>
>Puoi passare il cursore sopra una data specifica in qualsiasi grafico per visualizzare il conteggio dei singoli profili in una finestra di dialogo.

### Tendenze dimensione pubblico {#audience-size-trends}

Il grafico **[!UICONTROL Tendenze dimensioni pubblico]** mostra il numero di profili all&#39;interno del pubblico selezionato nel tempo. Consente di tenere traccia della crescita o della riduzione del pubblico. Puoi utilizzare questo grafico per monitorare l’efficacia del coinvolgimento e comprendere le modifiche nelle dimensioni del pubblico.

![Grafico delle tendenze delle dimensioni del pubblico.](../../images/sql-insights-query-pro-mode/templates/audience-size-trends-chart.png)

### Tendenze delle identità del pubblico {#audience-identities-trends}

Il grafico **[!UICONTROL Audience Identities trends]** fornisce informazioni sul numero totale di identità all&#39;interno del segmento di pubblico. Usa questo grafico per comprendere in che modo le identità univoche contribuiscono alle dimensioni complessive del pubblico. Fornisce un’indicazione di stabilità e coinvolgimento del pubblico.

![Grafico di tendenza delle identità del pubblico.](../../images/sql-insights-query-pro-mode/templates/audience-identities-trends.png)

### Tendenze dimensioni pubblico a identità singola {#single-identity-audience-size-trends}

Il grafico **[!UICONTROL Tendenze dimensioni pubblico per identità singola]** mostra il numero di membri del pubblico con una sola identità. Questa metrica è utile per comprendere la composizione del pubblico, in particolare in termini di unicità dell’identità, e aiuta a misurare l’efficacia degli sforzi di unione delle identità.

![Grafico delle tendenze delle dimensioni del pubblico con identità singola.](../../images/sql-insights-query-pro-mode/templates/single-identity-audience-size-trends.png)

## Esporta approfondimenti {#export-insights}

Dopo aver analizzato le metriche e applicato i filtri rilevanti, puoi esportare i dati per ulteriori finalità di analisi o reporting offline. A questo scopo, seleziona **[!UICONTROL Esporta]** in alto a destra nella tabella. Viene visualizzata la finestra di dialogo PDF di stampa. Da tale finestra di dialogo è possibile salvare i dati visualizzati come PDF o stamparli.

![Dashboard delle tendenze del pubblico con Esportazione evidenziata.](../../images/sql-insights-query-pro-mode/templates/audience-trends-export.png)

## Passaggi successivi

Dopo aver letto questo documento, hai imparato a ottenere informazioni utili sul comportamento del pubblico nel tempo dalla dashboard **Audience Trends**. Per informazioni su altri modelli di Data Distiller che possono aiutarti a prendere decisioni informate, ottimizzare la segmentazione e migliorare le strategie di coinvolgimento, consulta le guide all&#39;interfaccia utente di [Audience Comparison](./comparison.md), [Audience Identity Overlaps](./identity-overlaps.md) e [Advanced Audience Overlaps](./overlaps.md).
