---
title: Sovrapposizioni del pubblico avanzate
description: Scopri come analizzare le intersezioni del pubblico e prendere decisioni basate sui dati utilizzando la dashboard Advanced Audience Overlaps. Filtra i tipi di pubblico, confronta le sovrapposizioni ed esporta informazioni approfondite per migliorare le strategie di targeting.
source-git-commit: 90d5f00648a80d735b92c3bdc540f1ad18ff38f5
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 2%

---

# Sovrapposizioni del pubblico avanzate

Ottieni informazioni utili per ottimizzare la segmentazione del pubblico e le strategie di targeting analizzando il modo in cui i diversi segmenti di pubblico si intersecano con la dashboard [!UICONTROL Advanced Audience Overlaps]. Esamina le metriche tabulate per identificare le sovrapposizioni, perfezionare la segmentazione e ridurre i messaggi ridondanti. In ultima analisi, puoi utilizzare queste informazioni per creare campagne più mirate e attività di marketing efficienti. In questa dashboard puoi rivedere le intersezioni del pubblico, applicare filtri ed eseguire analisi di sovrapposizione dettagliate per prendere decisioni basate sui dati e migliorare i risultati del coinvolgimento.

## Filtra tipi di pubblico {#filter-audiences}

Per filtrare tipi di pubblico specifici per l&#39;analisi di sovrapposizione, selezionare l&#39;icona del filtro (![Icona del filtro.](../../../images/icons/filter-icon-white.png)) per aprire la finestra di dialogo [!UICONTROL Filtro]. Da qui, puoi aggiungere o rimuovere i tipi di pubblico dal modello di sovrapposizione per perfezionare l’analisi.

![La visualizzazione del pubblico avanzato si sovrappone con l&#39;icona del filtro evidenziata.](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-filter-icon.png)

Viene visualizzata la finestra di dialogo [!UICONTROL Filtri]. Per scegliere un pubblico per l&#39;analisi di sovrapposizione, seleziona un nome di pubblico dal menu a discesa **[!UICONTROL Pubblico]**. Il nome di qualsiasi pubblico aggiunto viene visualizzato con un tag sotto il menu a discesa. Una volta aggiunto, puoi selezionare la &quot;X&quot; dal suo nome per rimuoverlo. Per rimuovere tutti i filtri applicati, selezionare **[!UICONTROL Cancella tutto]**.

## Filtri applicati {#applied-filters}

Una volta applicato un filtro ([!UICONTROL Segmento amoxicilina] nell&#39;esempio della schermata), i dati del pubblico visualizzati vengono ridotti. Eventuali altri tipi di pubblico che scegli di aggiungere vengono visualizzati accanto al tag [!UICONTROL Filtro per] sopra il grafico [!UICONTROL Sovrapposizioni pubblico avanzate].

![Il dashboard di Advanced Audience si sovrappone con il filtro per segmento di Amoxicilin evidenziato.](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-applied-filters.png)

## Tabella Advanced Audience Overlaps {#advanced-audience-overlaps-table}

La sezione principale del dashboard visualizza la tabella [!UICONTROL Advanced Audience Overlaps], che fornisce un confronto dettagliato delle sovrapposizioni di pubblico tra segmenti diversi. Le colonne della tabella sono le seguenti:

| Nome colonna | Descrizione |
|------------------------------------|----------------------------------------------------------------------------------------------|
| **[!UICONTROL Nome_Segmento_Source]** | Il pubblico originale in fase di analisi (ad esempio, &quot;Segmento di amoxicilina&quot;). |
| **[!UICONTROL Nome_Segmento_Sovrapposizione]** | Il pubblico le cui sovrapposizioni vengono confrontate con (ad esempio, &quot;Glucosio ematico > 100&quot;). |
| **[!UICONTROL Conteggio_Pubblico_Segmento_Source]** | Numero totale di profili del pubblico sorgente. |
| **[!UICONTROL Conteggio_Pubblico_Segmento_Sovrapposizione]** | La dimensione del pubblico sovrapposto, che varia a seconda della sovrapposizione. |
| **[!UICONTROL Conteggio_pubblico_sovrapposizione]** | Dimensione del pubblico effettivo sovrapposto tra il pubblico sorgente e quello sovrapposto. |

{style="table-layout:auto"}

## Esporta approfondimenti {#export-insights}

Dopo aver filtrato e analizzato i tipi di pubblico, puoi esportare i dati per ulteriori attività di analisi offline o a scopo di reporting. Per esportare le tue informazioni, seleziona **[!UICONTROL Esporta]** in alto a destra nella tabella. Viene visualizzata la finestra di dialogo Stampa PDF, che consente di salvare i dati come PDF o di stamparli.

![Visualizzazione sovrapposta pubblico avanzato con Esportazione evidenziata.](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-export.png)

Per tornare alla panoramica del [!UICONTROL Modello], selezionare **[!UICONTROL Modelli]**.

![La visualizzazione del pubblico avanzato si sovrappone ai modelli evidenziati.](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-navigation.png)

## Passaggi successivi

Dopo aver letto questo documento, hai imparato ad analizzare le intersezioni del pubblico e a prendere decisioni basate sui dati utilizzando la dashboard **[!UICONTROL Advanced Audience Overlaps]**. Per ottimizzare ulteriormente la segmentazione del pubblico e le strategie di targeting, esplora altri modelli di Data Distiller che forniscono informazioni utili. Consulta le [guide per l&#39;interfaccia utente Tendenze pubblico](./trends.md), [Confronto pubblico](./comparison.md) e [Sovrapposizioni identità pubblico](./identity-overlaps.md) per continuare a migliorare il coinvolgimento del pubblico e le attività di segmentazione.

