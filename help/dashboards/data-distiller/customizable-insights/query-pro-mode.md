---
title: Modalità Query Pro
description: Scopri come utilizzare le query SQL nell’interfaccia utente di Adobe Experience Platform per generare grafici per le dashboard personalizzate.
source-git-commit: 17ad52864bbca09844c0241b6451e6811bd8f413
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 0%

---

# Modalità Query Pro {#query-pro-mode}

La modalità Query pro è un flusso di lavoro basato su editor SQL che ti guida attraverso il processo di generazione di informazioni approfondite con query SQL personalizzate nell’interfaccia utente di Adobe Experience Platform. Prima di poter generare insights con query SQL personalizzate, è necessario [creare un dashboard](./overview.md#create-custom-dashboard).

## Componi SQL {#compose-sql}

Dopo aver scelto di creare un dashboard con modalità query pro, **[!UICONTROL Immetti SQL]** viene visualizzata. Seleziona un database (modello dati approfondimenti) da interrogare dal menu a discesa e inserisci una query adatta per il set di dati nell’editor query pro.

>[!NOTE]
>
>La modalità Query pro è disponibile solo per gli utenti che hanno acquistato lo SKU di Data Distiller. Il [[!UICONTROL Modalità di progettazione guidata]](../../user-defined-dashboards.md) è disponibile per tutti gli utenti per creare insights da un modello di dati esistente.

Consulta la [Guida utente di Query Editor](../../../query-service/ui/user-guide.md#query-authoring) per informazioni sugli elementi dell’interfaccia utente.

![Il [!UICONTROL Immetti SQL] finestra di dialogo con il menu a discesa del set di dati e icona Esegui evidenziata, la finestra di dialogo contiene una query SQL compilata e viene visualizzata la scheda Parametri query.](../../images/customizable-insights/enter-sql-database-dropdown.png)

### Parametri di query {#query-parameters}

Da includere [globale](./filters/global-filter.md) o [filtri data](./filters/date-filter.md) query **deve** utilizzare i parametri di query. Quando componi l’istruzione in modalità query pro, devi fornire valori di esempio se la query utilizza parametri di query. I valori di esempio consentono di eseguire l&#39;istruzione SQL e generare il grafico. I valori di esempio forniti durante la composizione dell’istruzione vengono sostituiti dai valori effettivi selezionati per la data o il filtro globale in fase di esecuzione.



>[!IMPORTANT]
>
>Se si desidera utilizzare un filtro globale, è necessario inserire un parametro di query nell&#39;istruzione SQL e quindi collegare tale parametro di query al filtro globale nel compositore widget. Nella schermata seguente, `CONSENT_VALUE_FILTER` viene utilizzato nel linguaggio SQL come parametro di query per un filtro globale. Consulta la [documentazione del filtro globale](./filters/global-filter.md#enable-global-filter) per ulteriori informazioni su come eseguire questa operazione.

Per eseguire la query, seleziona l’icona Esegui (![Icona di esecuzione.](../../images/customizable-insights/run-icon.png)). Nell&#39;Editor query viene visualizzata la scheda dei risultati. Quindi, per confermare la configurazione e aprire il compositore widget, seleziona **[!UICONTROL Seleziona]**.

>[!TIP]
>
>Se la query utilizza parametri di query, eseguirla una sola volta per precompilare tutte le chiavi dei parametri di query utilizzate. La query non riuscirà, ma l’interfaccia utente visualizza automaticamente la scheda Parametri query ed elenca tutte le chiavi incluse. Aggiungi i valori appropriati per le chiavi.

![Il [!UICONTROL Immetti SQL] finestra di dialogo con input SQL, scheda dei risultati visualizzata e Seleziona evidenziato.](../../images/customizable-insights/enter-sql-select.png)

## Popolare widget {#populate-widget}

Il compositore widget ora è popolato con le colonne dell&#39;SQL eseguito. Il tipo di dashboard è indicato in alto a sinistra, in questo caso è [!UICONTROL Immissione SQL manuale]. Seleziona l’icona della matita (![Un’icona a forma di matita.](../../images/customizable-insights/edit-icon.png)) per modificare l&#39;istruzione SQL in qualsiasi punto.

>[!TIP]
>
>Gli attributi disponibili sono colonne ricavate dall&#39;istruzione SQL eseguita.

Per creare il widget, utilizza gli attributi elencati nella [!UICONTROL Attributi] colonna. È possibile utilizzare la barra di ricerca per cercare attributi o scorrere l&#39;elenco.

![Il compositore widget con il metodo di creazione e la colonna attributo evidenziati.](../../images/customizable-insights/creation-method-and-attribute-column.png)

### Aggiungi attributi {#add-attributes}

Per aggiungere un attributo al widget, seleziona l’icona più (![Un&#39;icona più.](../../images/customizable-insights/add-icon.png)) accanto al nome di un attributo. Il menu a discesa visualizzato consente di aggiungere un attributo al grafico dalle opzioni determinate dall&#39;istruzione SQL. Diversi tipi di grafico dispongono di opzioni diverse, ad esempio un elenco a discesa degli assi X e Y.

In questo esempio di grafico ad anello, le opzioni sono dimensione e colore. Il colore suddivide i risultati del grafico ad anello e la dimensione corrisponde alla metrica effettiva utilizzata. Aggiungi un attributo al [!UICONTROL Colore] per dividere i risultati in colori diversi in base alla composizione dell&#39;attributo.

>[!TIP]
>
>Seleziona l’icona freccia su e freccia giù (![Icona freccia su e freccia giù.](../../images/customizable-insights/switch-axis-icon.png)) per cambiare la disposizione degli assi X e Y sui grafici a barre o a linee.

![Il compositore di widget con le frecce a discesa dell’icona del componente aggiuntivo evidenziate.](../../images/customizable-insights/add-icon-and-switch-arrows.png)

Per modificare il tipo di grafico o il grafico del widget, seleziona tra le opzioni disponibili del [!UICONTROL Indicatori] a discesa. Le opzioni includono [!UICONTROL Linea], [!UICONTROL Anello], [!UICONTROL Numero grande], e [!UICONTROL Barre]. Una volta selezionata, viene generata una visualizzazione di anteprima delle impostazioni correnti del widget.

![Il compositore widget con l&#39;anteprima widget evidenziata.](../../images/customizable-insights/widget-preview.png)

## Proprietà widget {#properties}

Seleziona l’icona delle proprietà (![Icona delle proprietà.](../../images/customizable-insights/properties-icon.png)) nella barra a destra per aprire il pannello proprietà. In [!UICONTROL Proprietà] , immettere un nome per il widget nel **[!UICONTROL Titolo widget]** campo di testo. È inoltre possibile rinominare vari aspetti del grafico.

>[!NOTE]
>
>I campi specifici disponibili nella barra laterale delle proprietà variano a seconda del tipo di grafico che si sta modificando.

![Il compositore widget con l&#39;icona delle proprietà e il campo del titolo widget evidenziati.](../../images/customizable-insights/widget-properties-title-text.png)

## Salvare il widget {#save-widget}

Se si salva nel compositore widget, il widget viene salvato localmente nel dashboard. Per salvare il lavoro e riprenderlo in un secondo momento, selezionare **[!UICONTROL Salva]**. Un&#39;icona di spunta sotto il nome del widget indica che il widget è stato salvato. In alternativa, quando si è soddisfatti del widget, selezionare **[!UICONTROL Salva e chiudi]** per rendere il widget disponibile a tutti gli altri utenti con accesso al dashboard. Seleziona Annulla per abbandonare il lavoro e tornare al dashboard personalizzato.

![Il compositore di widget con Salva, Widget salvato e Salva e chiudi evidenziato.](../../images/customizable-insights/insight-saved.png)

## Modificare dashboard e grafici {#edit}

Seleziona **[!UICONTROL Modifica]** per modificare l’intero dashboard o qualsiasi informazione. Dalla modalità di modifica è possibile ridimensionare i widget, modificare le istruzioni SQL o creare e applicare filtri globali e temporali. Questi filtri vincolano i dati visualizzati nei widget del dashboard. È un modo comodo per aggiornare e perfezionare rapidamente le informazioni per diversi casi d’uso.

![Dashboard personalizzato con Modifica evidenziato.](../../images/customizable-insights/edit-dashboard.png)

Seleziona **[!UICONTROL Aggiungi filtro]** per creare una [[!UICONTROL Filtro data]](#create-date-filter) o un [[!UICONTROL Filtro globale]](#create-global-filter). Una volta creati, tutti i filtri globali e quelli relativi alla data sono disponibili da [icona del filtro](#select-global-filter) (![Icona di filtro.](../../images/customizable-insights/filter.png)) del dashboard.

![Dashboard personalizzato con il menu a discesa Aggiungi filtro evidenziato.](../../images/customizable-insights/add-filter.png)

## Modificare, duplicare o eliminare un approfondimento

Per istruzioni su come eseguire questa operazione, consulta la guida alla dashboard personalizzata. [modificare, duplicare o eliminare un widget esistente](../../user-defined-dashboards.md#duplicate).

## Passaggi successivi

Dopo aver letto questo documento, ora sai come scrivere query SQL nell’interfaccia utente di Adobe Experience Platform per generare grafici per le dashboard personalizzate. Successivamente, dovresti scoprire come arricchire ulteriormente i tuoi dati con [creazione di un filtro data](./filters/date-filter.md), o [creazione di un filtro globale](./filters/global-filter.md).

Puoi anche saperne di più su altre funzioni di Approfondimenti personalizzati, tra cui [le diverse opzioni di visualizzazione per i dati analizzati SQL](./view-more.md) o come [visualizzare le istruzioni SQL alla base delle informazioni personalizzate](./view-sql.md).
