---
title: Creare un filtro globale
description: Scopri come filtrare le informazioni sui dati con un filtro personalizzato applicato a livello globale.
source-git-commit: b95616263d5a6dd26f7fce61d5d0b33c2d470c46
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Creare un filtro globale {#create-global-filter}

Per creare un filtro globale, seleziona innanzitutto **[!UICONTROL Aggiungi filtro]** dalla vista del dashboard, quindi **[!UICONTROL Filtro globale]** dal menu a discesa.

>[!IMPORTANT]
>
>Assicurati di mappare i filtri globali a tutti i tuoi grafici. Questo non è un processo automatico. Per utilizzare un filtro globale, è necessario includere [parametro query](../../../../query-service/ui/parameterized-queries.md) nell’istruzione SQL del grafico, [abilitare il filtro globale](#enable-global-filter) nel compositore widget, e [seleziona un valore runtime](#select-global-filter) per il parametro nella finestra di dialogo filtro globale. Per informazioni su come modificare il codice SQL se è necessario incorporare un parametro di query, consulta la guida di query pro.

![Un dashboard personalizzato con Aggiungi filtro e il relativo menu a discesa evidenziato.](../../../images/customizable-insights/add-filter.png)

È possibile modificare rapidamente le informazioni fornite dall&#39;istruzione SQL mediante filtri globali personalizzati.

Il [!UICONTROL Creare un filtro globale] viene visualizzata una finestra di dialogo. La creazione di un filtro globale segue lo stesso processo della creazione di un approfondimento con SQL. Innanzitutto, seleziona un database (modello dati approfondimenti) per la query, quindi inserisci le istruzioni SQL personalizzate nell’editor delle query e infine seleziona l’icona Esegui (![Icona di esecuzione.](../../../images/customizable-insights/run-icon.png)).

>[!IMPORTANT]
>
>Quando crei un filtro globale, devi includere un ID e un valore. I valori di esempio consentono di eseguire l&#39;istruzione SQL e generare il grafico. I valori di esempio forniti durante la composizione dell’istruzione vengono sostituiti dai valori effettivi selezionati per la data o il filtro globale in fase di esecuzione.

Dopo aver eseguito correttamente la query, nella scheda dei risultati vengono visualizzati i risultati. Seleziona **[!UICONTROL Avanti]**.

![Il [!UICONTROL Creare una finestra di dialogo di filtro globale] con il menu a discesa set di dati, evidenziano l’icona Esegui e Successivo.](../../../images/customizable-insights/global-filter.png)

Il passaggio finale del flusso di lavoro per la creazione di filtri globali richiede l’aggiunta di un’etichetta per il filtro. Aggiungi un’etichetta al **[!UICONTROL Etichetta filtro]** e selezionare un tipo di filtro dalla casella a discesa.

>[!NOTE]
>
>Solo il [!UICONTROL Casella combinata] l’opzione del tipo di filtro è attualmente supportata.

Infine, seleziona **[!UICONTROL Seleziona]** per tornare alla vista dashboard.

![Il [!UICONTROL Creare una finestra di dialogo di filtro globale] con Seleziona e l’input del testo dell’etichetta del filtro evidenziato.](../../../images/customizable-insights/global-filter-label.png)

## Abilita il filtro globale per ogni informazione approfondita {#enable-global-filter}

>[!TIP]
>
>Attiva i filtri globali in ogni grafico creato. In questo modo i valori scelti come filtro globale verranno visualizzati in tutti i grafici.

Dopo aver creato il filtro globale per il dashboard, l’interruttore per tale filtro globale diventa disponibile come parte del compositore widget.

![Il compositore widget con l’interruttore Filtro globale evidenziato.](../../../images/customizable-insights/global-filter-consent.png)

>[!IMPORTANT]
>
>Assicurati che il parametro del filtro globale sia incluso nell’istruzione SQL di ogni informazione approfondita.

## Seleziona un filtro globale {#select-global-filter}

Per aprire [!UICONTROL Filtri] nella finestra di dialogo in cui sono elencati tutti i filtri personalizzati, seleziona l’icona del filtro (![Icona di filtro.](../../../images/customizable-insights/filter.png)) a sinistra del dashboard. Quindi, per applicare gli effetti alle informazioni della dashboard, scegli un’opzione dal menu a discesa del filtro globale, quindi seleziona **[!UICONTROL Applica]**.

![Dashboard personalizzato con la finestra di dialogo del filtro evidenziata.](../../../images/customizable-insights/custom-filters.png)
