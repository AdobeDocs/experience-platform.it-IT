---
title: Modalità Query Pro
description: Scopri come utilizzare le query SQL nell’interfaccia utente di Adobe Experience Platform per generare grafici per le dashboard personalizzate.
exl-id: 15c664c4-8546-4e04-b81d-c78bf83500d3
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---

# Modalità query pro {#query-pro-mode}

La modalità Query pro è un flusso di lavoro basato su editor SQL che ti guida attraverso il processo di generazione di informazioni approfondite con query SQL personalizzate nell’interfaccia utente di Adobe Experience Platform. Prima di poter generare insights con query SQL personalizzate, devi [creare un dashboard](./overview.md#create-custom-dashboard).

## Componi SQL {#compose-sql}

Dopo aver scelto di creare un dashboard in modalità Query Pro, viene visualizzata la finestra di dialogo **[!UICONTROL Immettere SQL]**. Seleziona un database (modello dati approfondimenti) da interrogare dal menu a discesa e inserisci una query adatta per il set di dati nell’editor query pro.

>[!NOTE]
>
>La modalità Query pro è disponibile solo per gli utenti che hanno acquistato lo SKU di Data Distiller. La [[!UICONTROL modalità progettazione guidata]](../../user-defined-dashboards.md) è disponibile per tutti gli utenti per creare informazioni da un modello di dati esistente.

Per informazioni sugli elementi dell&#39;interfaccia utente, consultare la [Guida utente di Query Editor](../../../query-service/ui/user-guide.md#query-authoring).

![La finestra di dialogo [!UICONTROL Inserisci SQL] con il menu a discesa del set di dati ed icona di esecuzione evidenziata, la finestra di dialogo contiene una query SQL compilata e la scheda Parametri query visualizzata.](../../images/customizable-insights/enter-sql-database-dropdown.png)

### Parametri della query {#query-parameters}

Per includere [global](./filters/global-filter.md) o [filtri di data](./filters/date-filter.md) la query **deve** utilizzare i parametri di query. Quando componi l’istruzione in modalità query pro, devi fornire valori di esempio se la query utilizza parametri di query. I valori di esempio consentono di eseguire l&#39;istruzione SQL e generare il grafico. I valori di esempio forniti durante la composizione dell’istruzione vengono sostituiti dai valori effettivi selezionati per la data o il filtro globale in fase di esecuzione.



>[!IMPORTANT]
>
>Se si desidera utilizzare un filtro globale, è necessario inserire un parametro di query nell&#39;istruzione SQL e quindi collegare tale parametro di query al filtro globale nel compositore widget. Nella schermata seguente, `CONSENT_VALUE_FILTER` viene utilizzato nel linguaggio SQL come parametro di query per un filtro globale. Per ulteriori informazioni su come eseguire questa operazione, consulta la [documentazione del filtro globale](./filters/global-filter.md#enable-global-filter).

Per eseguire la query, selezionare l&#39;icona di esecuzione (![Icona di esecuzione.](/help/images/icons/play.png)). Nell&#39;Editor query viene visualizzata la scheda dei risultati. Quindi, per confermare la configurazione e aprire il compositore widget, seleziona **[!UICONTROL Seleziona]**.

>[!TIP]
>
>Se la query utilizza parametri di query, eseguirla una sola volta per precompilare tutte le chiavi dei parametri di query utilizzate. La query non riuscirà, ma l’interfaccia utente visualizza automaticamente la scheda Parametri query ed elenca tutte le chiavi incluse. Aggiungi i valori appropriati per le chiavi.

![La finestra di dialogo [!UICONTROL Inserisci SQL] con input SQL, la scheda dei risultati visualizzata e Seleziona evidenziata.](../../images/customizable-insights/enter-sql-select.png)

## Popolare widget {#populate-widget}

Il compositore widget ora è popolato con le colonne dell&#39;SQL eseguito. Il tipo di dashboard è indicato in alto a sinistra, in questo caso è [!UICONTROL Voce SQL manuale]. Selezionare l&#39;icona della matita (![Un&#39;icona della matita.](/help/images/icons/edit.png)) per modificare l&#39;istruzione SQL in qualsiasi momento.

>[!TIP]
>
>Gli attributi disponibili sono colonne ricavate dall&#39;istruzione SQL eseguita.

Per creare il widget, utilizza gli attributi elencati nella colonna [!UICONTROL Attributi]. È possibile utilizzare la barra di ricerca per cercare attributi o scorrere l&#39;elenco.

![Il compositore widget con il metodo di creazione e la colonna degli attributi evidenziati.](../../images/customizable-insights/creation-method-and-attribute-column.png)

### Aggiungi attributi {#add-attributes}

Per aggiungere un attributo al widget, selezionare l&#39;icona più (![A icona più.](/help/images/icons/add-circle.png)) accanto al nome di un attributo. Il menu a discesa visualizzato consente di aggiungere un attributo al grafico dalle opzioni determinate dall&#39;istruzione SQL. Diversi tipi di grafico dispongono di opzioni diverse, ad esempio un elenco a discesa degli assi X e Y.

In questo esempio di grafico ad anello, le opzioni sono dimensione e colore. Il colore suddivide i risultati del grafico ad anello e la dimensione corrisponde alla metrica effettiva utilizzata. Aggiungere un attributo al campo [!UICONTROL Colore] per dividere i risultati in colori diversi in base alla composizione dell&#39;attributo.

>[!TIP]
>
>Selezionare l&#39;icona freccia su e freccia giù (![Icona freccia su e freccia giù.](/help/images/icons/switch.png)) per cambiare la disposizione degli assi X e Y nei grafici a barre o a linee.

![Il compositore widget con l&#39;icona del componente aggiuntivo a discesa e le frecce di selezione evidenziate.](../../images/customizable-insights/add-icon-and-switch-arrows.png)

Per modificare il tipo di grafico o il grafico del widget, seleziona tra le opzioni disponibili del menu a discesa [!UICONTROL Indicatori]. Le opzioni includono [!UICONTROL Riga], [!UICONTROL Anello], [!UICONTROL Numero grande] e [!UICONTROL Barra]. Una volta selezionata, viene generata una visualizzazione di anteprima delle impostazioni correnti del widget.

![Compositore widget con anteprima widget evidenziata.](../../images/customizable-insights/widget-preview.png)

## Proprietà widget {#properties}

Selezionare l&#39;icona delle proprietà (![Icona delle proprietà.](/help/images/icons/properties.png)) nella barra a destra per aprire il pannello proprietà. Nel pannello [!UICONTROL Proprietà], immetti un nome per il widget nel campo di testo **[!UICONTROL Titolo widget]**. È inoltre possibile rinominare vari aspetti del grafico.

>[!NOTE]
>
>I campi specifici disponibili nella barra laterale delle proprietà variano a seconda del tipo di grafico che si sta modificando.

![Il compositore widget con l&#39;icona delle proprietà e il campo del titolo del widget evidenziati.](../../images/customizable-insights/widget-properties-title-text.png)

## Salvare il widget {#save-widget}

Se si salva nel compositore widget, il widget viene salvato localmente nel dashboard. Se desideri salvare il lavoro e riprenderlo in un secondo momento, seleziona **[!UICONTROL Salva]**. Un&#39;icona di spunta sotto il nome del widget indica che il widget è stato salvato. In alternativa, se si è soddisfatti del widget, selezionare **[!UICONTROL Salva e chiudi]** per rendere il widget disponibile a tutti gli altri utenti con accesso al dashboard. Seleziona Annulla per abbandonare il lavoro e tornare al dashboard personalizzato.

![Il compositore widget con Salva, Widget salvato e Salva e chiudi evidenziato.](../../images/customizable-insights/insight-saved.png)

## Modificare dashboard e grafici {#edit}

Seleziona **[!UICONTROL Modifica]** per modificare l&#39;intero dashboard o qualsiasi informazione. Dalla modalità di modifica è possibile ridimensionare i widget, modificare le istruzioni SQL o creare e applicare filtri globali e temporali. Questi filtri vincolano i dati visualizzati nei widget del dashboard. È un modo comodo per aggiornare e perfezionare rapidamente le informazioni per diversi casi d’uso.

![Dashboard personalizzato con Modifica evidenziata.](../../images/customizable-insights/edit-dashboard.png)

Seleziona **[!UICONTROL Aggiungi filtro]** per creare un [[!UICONTROL Filtro data]](#create-date-filter) o un [[!UICONTROL Filtro globale]](#create-global-filter). Dopo la creazione, tutti i filtri globali e di data sono disponibili da [icona filtro](#select-global-filter) (![icona filtro.](/help/images/icons/filter.png)) del tuo dashboard.

![Dashboard personalizzato con il menu a discesa Aggiungi filtro evidenziato.](../../images/customizable-insights/add-filter.png)

## Modificare, duplicare o eliminare un approfondimento

Per istruzioni su come [modificare, duplicare o eliminare un widget esistente](../../user-defined-dashboards.md#duplicate), consulta la guida Dashboard personalizzato.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come scrivere query SQL nell’interfaccia utente di Adobe Experience Platform per generare grafici per le dashboard personalizzate. Successivamente, dovresti scoprire come arricchire ulteriormente i tuoi dati [creando un filtro data](./filters/date-filter.md) o [creando un filtro globale](./filters/global-filter.md).

Puoi anche saperne di più su altre funzionalità di Approfondimenti personalizzati, tra cui [le diverse opzioni di visualizzazione per i dati analizzati da SQL](./view-more.md) o come [visualizzare le istruzioni SQL alla base delle tue informazioni personalizzate](./view-sql.md).
