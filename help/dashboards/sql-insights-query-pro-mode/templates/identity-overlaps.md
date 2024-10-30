---
title: Sovrapposizioni di identità del pubblico
description: Scopri come analizzare le sovrapposizioni di identità del pubblico utilizzando la dashboard Sovrapposizioni identità pubblico. Filtra i tipi di pubblico, specifica i criteri di unione ed esamina le relazioni di identità per prendere decisioni basate sui dati.
source-git-commit: 90d5f00648a80d735b92c3bdc540f1ad18ff38f5
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 1%

---

# Sovrapposizioni di identità del pubblico

Analizza le sovrapposizioni di identità per i tipi di pubblico selezionati con il dashboard [!UICONTROL Sovrapposizioni identità pubblico]. Puoi utilizzare le informazioni dettagliate sul modo in cui le diverse identità all&#39;interno di un pubblico si relazionano tra loro per ottimizzare le strategie di cucitura, ridurre la ridondanza e migliorare l&#39;accuratezza del Segmentazione del cliente. Sviluppa strategie di targeting efficaci e snellisci le interazioni dei clienti con una migliore comprensione della sovrapposizione tra i tipi di identità.

## Filtrare i tipi di pubblico {#filter-audiences}

Utilizza filtri personalizzati per un’analisi mirata di tipi di pubblico e tipi di identità specifici per garantire che i dati presentati siano in linea con gli obiettivi di analisi. Per avviare l&#39;analisi, selezionare l&#39;icona del filtro (![Icona del filtro.](../../../images/icons/filter-icon-white.png)).

![Il dashboard di Audience Identity si sovrappone con l&#39;icona del filtro evidenziata.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-filter-icon.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Filtri]**. Da questa vista, scegli i filtri globali per configurare il pubblico, i criteri di unione e le identità per il confronto. Seleziona le impostazioni per l&#39;analisi dal menu a discesa di ciascuna sezione

1. Seleziona un **[!UICONTROL pubblico]**: scegli il segmento di pubblico da analizzare (ad esempio, **Canada - Alberta**).
2. Specifica un **[!UICONTROL criterio di unione]**: definisci il criterio di unione che determina il modo in cui le identità vengono combinate nel pubblico selezionato (nella schermata di esempio, viene selezionato il criterio **Basato sull&#39;ora predefinita**).
3. Selezionare un&#39;identità **[!UICONTROL A]** e un&#39;identità **[!UICONTROL B]** per il confronto**: scegliere i due tipi di identità da confrontare. Nell&#39;esempio, **L&#39;identità A** è selezionata come &quot;crmId&quot; e **l&#39;identità B** è selezionata come &quot;e-mail&quot;.
4. **Imposta un intervallo di date**: scegli un intervallo predefinito come &quot;Oggi&quot; o imposta manualmente le date di inizio e di fine utilizzando i campi del calendario.

![La finestra di dialogo Filtri del dashboard Sovrapposizioni identità pubblico.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-filters-dialog.png)

>[!TIP]
>
>Per eliminare tutti i filtri globali personalizzati, selezionare **[!UICONTROL Cancella tutto]** dalla [!UICONTROL finestra di dialogo Filtri] . Per rimuovere un singolo filtro, seleziona la X a destra del nome del filtro.

Una volta scelti i filtri, selezionare **[!UICONTROL Applica]** per aggiornare il dashboard.

![La finestra di dialogo Filtri nel dashboard Audience Identity Overlaps (Identità pubblico) con Applica evidenziata.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-apply-filters.png)

## Informazioni disponibili sulla dashboard {#available-insights}

Il dashboard **Audience Identity Overlaps** fornisce diverse visualizzazioni e dati tabulati per aiutarti a comprendere le sovrapposizioni di identità e le tendenze all&#39;interno del tuo pubblico.

### Sovrapposizioni di identità del pubblico {#overlaps-table}

Nella tabella **[!UICONTROL Sovrapposizioni identità pubblico]** sono visualizzate le sovrapposizioni di identità in base ai filtri selezionati. Utilizza queste informazioni per valutare la sovrapposizione tra diversi tipi di identità e capire come vengono risolte in modo efficace le identità. La tabella seguente spiega nel dettaglio ogni colonna:

| Nome colonna | Descrizione |
|-----------------|-------------------------------|
| **[!UICONTROL Nome pubblico]** | Nome del pubblico analizzato. Questa colonna identifica quale segmento di pubblico è in revisione per garantire che le informazioni si concentrino sul gruppo di destinazione. |
| **[!UICONTROL Identità A]** e **[!UICONTROL Identità B]** | Le identità confrontate (ad esempio, `crmId` e `email`). Sapere quali tipi di identità vengono confrontati ti aiuta a identificare quali strategie di risoluzione delle identità contribuiscono alla sovrapposizione dei tipi di pubblico e a ottimizzare tali relazioni. |
| **[!UICONTROL Conteggio sovrapposizioni]** | Il conteggio dei profili in cui sono presenti entrambe le identità. Questa metrica fornisce informazioni dettagliate sul grado di sovrapposizione delle identità all&#39;interno del pubblico. Queste informazioni sono fondamentali per valutare l’efficacia con cui più identità vengono risolte in profili unificati, il che a sua volta può migliorare le strategie di targeting e personalizzazione. |
| **[!UICONTROL Numero identità A]** | Numero totale di profili nel pubblico selezionato che contengono **Identità A**. Utilizza queste informazioni per comprendere la prevalenza del tipo di identità principale all’interno del pubblico e valutarne il ruolo nell’analisi di sovrapposizione. |

![La tabella Sovrapposizioni identità pubblico nel dashboard Sovrapposizioni identità pubblico.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-chart.png)

### Suddivisione identità {#identity-breakdown}

Il **[!UICONTROL grafico di suddivisione]** identità mostra la composizione relativa delle identità all&#39;interno del pubblico selezionato. L&#39;asse X rappresenta il numero totale di identità all&#39;interno del pubblico selezionato, mentre l&#39;asse Y rappresenta il nome del pubblico analizzato. Utilizza questa visualizzazione per comprendere la prevalenza di ogni tipo di identità e valutare l&#39;impatto della tua strategia di gestione delle identità. Il grafico distingue tra i tipi di identità utilizzando colori distinti, fornendo una rapida panoramica di come le identità sono distribuite tra il pubblico.

>[!TIP]
>
>Passa il cursore sopra le colonne per visualizzare il conteggio individuale dei profili per ogni tipo di identità.

![Grafico di suddivisione identità.](../../images/sql-insights-query-pro-mode/templates/identity-breakdown-chart.png)

### Tendenze dell’identità del pubblico {#audience-identity-trends}

Il grafico **[!UICONTROL Audience Identity Trends]** fornisce informazioni approfondite sul modo in cui il numero totale di identità è cambiato nel tempo. L’asse X rappresenta l’intervallo di date in fase di analisi, mentre l’asse Y rappresenta il numero totale di identità per pubblico. Utilizza questa metrica per monitorare la crescita dell’identità, valutare la stabilità e misurare l’efficacia delle attività di gestione delle identità in corso.

>[!TIP]
>
>Passa il cursore sopra una data nel grafico per visualizzare il numero totale di identità per il pubblico in una data specifica.

![Il grafico Tendenze identità pubblico.](../../images/sql-insights-query-pro-mode/templates/audience-identity-trends-chart.png)

## Esportazione Insights {#export-insights}

Dopo aver analizzato le sovrapposizioni di identità, puoi esportare i dati per l&#39;analisi offline o la generazione di rapporti. Per esportare i dati, seleziona **[!UICONTROL Esporta]** in alto a destra nella tabella. Viene visualizzata la finestra di dialogo Stampa PDF, che consente di salvare i dati visualizzati come PDF o di stamparli.

![Il dashboard di Audience Identity si sovrappone con Esportazione evidenziata.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-export.png)

Il dashboard **Audience Identity Overlaps** fornisce informazioni essenziali sull&#39;intersezione di identità diverse tra i tipi di pubblico selezionati. Sfruttando queste informazioni, puoi perfezionare le strategie di unione delle identità, ridurre la ridondanza e garantire una segmentazione del pubblico più precisa ed efficace.

## Passaggi successivi

Dopo aver letto questo documento, hai imparato come ottenere informazioni preziose sulle sovrapposizioni di identità per i tipi di pubblico selezionati utilizzando il **dashboard Sovrapposizioni di** identità pubblico. Per migliorare ulteriormente la tua comprensione della gestione delle segmentazione del pubblico e delle identità, esplora altri modelli di Distiller dati che forniscono informazioni complete. Consulta le [guide interfaccia Tendenze](./trends.md) del pubblico, [Confronto](./comparison.md) del pubblico e [Sovrapposizioni](./overlaps.md) Avanzate pubblico per continuare a migliorare le tue strategie di targeting e coinvolgimento.

