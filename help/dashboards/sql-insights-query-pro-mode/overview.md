---
title: Informazioni SQL per il reporting esteso delle app
description: Scopri come utilizzare le query SQL per generare insights per le dashboard personalizzate.
exl-id: c60a9218-4ac0-4638-833b-bdbded36ddf5
source-git-commit: 9f4ce2a3a8af72342683c859caa270662b161b7d
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 1%

---

# Approfondimenti SQL per il reporting esteso delle app

Utilizza query SQL personalizzate per estrarre in modo efficace informazioni approfondite da diversi set di dati strutturati. Gli utenti tecnici possono utilizzare la modalità query pro per eseguire analisi complesse con SQL e quindi condividere questa analisi con utenti non tecnici tramite grafici nel dashboard personalizzato o esportarle in file CSV. Questo metodo di creazione di insight è adatto per tabelle con relazioni chiare e consente un maggiore grado di personalizzazione all’interno delle informazioni approfondite e dei filtri che possono essere adatti a casi d’uso di nicchia.

>[!IMPORTANT]
>
>La modalità Query Pro è disponibile solo per gli utenti che hanno acquistato lo SKU [Data Distiller](../../query-service/data-distiller/overview.md).

Per generare informazioni da SQL, è necessario innanzitutto creare un dashboard.

## Creare un dashboard personalizzato {#create-custom-dashboard}

Per creare un dashboard personalizzato, selezionare **[!UICONTROL Dashboards]** dal pannello di navigazione a sinistra per aprire l&#39;area di lavoro Dashboard. Quindi, seleziona **[!UICONTROL Create dashboard]**.

![Inventario dashboard con dashboard di creazione evidenziato.](../images/sql-insights-query-pro-mode/create-dashboard.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Create dashboard]**. Sono disponibili due opzioni per scegliere il metodo di creazione del dashboard. Per creare le tue informazioni, puoi utilizzare un modello dati esistente con [[!UICONTROL Guided design mode]](../standard-dashboards.md) oppure la tua istruzione SQL con [!UICONTROL Query pro mode].

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

L&#39;utilizzo di un modello dati esistente offre i vantaggi di fornire un framework strutturato, efficiente e scalabile personalizzato in base alle esigenze aziendali specifiche. Per informazioni su come [creare approfondimenti da un modello dati esistente](../standard-dashboards.md#create-widget), consulta la guida del dashboard personalizzato.

Le informazioni generate dalle query SQL offrono maggiore flessibilità e personalizzazione. Gli utenti tecnici possono utilizzare la modalità query pro per eseguire analisi complesse su SQL e quindi condividere questa analisi con utenti non tecnici tramite questa funzionalità del dashboard. Seleziona **[!UICONTROL Query pro mode]** seguito da **[!UICONTROL Save]**.

>[!NOTE]
>
>Una volta effettuata la selezione, non è possibile modificarla all&#39;interno del dashboard. È invece necessario creare un nuovo dashboard con un metodo di creazione diverso.

![La finestra di dialogo [!UICONTROL Create dashboard] con modalità Query Pro e Salva evidenziata.](../images/sql-insights-query-pro-mode/query-pro-mode.png)

## Panoramica sulla modalità Query pro {#query-pro-mode}

La modalità Query pro è un flusso di lavoro basato su editor SQL che ti guida attraverso il processo di generazione di informazioni approfondite con query SQL personalizzate nell’interfaccia utente di Adobe Experience Platform. Prima di poter generare insights con query SQL personalizzate, è necessario creare un dashboard.

## Componi SQL {#compose-sql}

Dopo aver scelto di creare un dashboard con modalità query pro, viene visualizzata la finestra di dialogo **[!UICONTROL Enter SQL]**. Seleziona un database (modello dati approfondimenti) da interrogare dal menu a discesa e inserisci una query adatta per il set di dati nell’editor query pro.

>[!NOTE]
>
>La modalità Query pro è disponibile solo per gli utenti che hanno acquistato lo SKU di Data Distiller. [[!UICONTROL Guided design mode]](../standard-dashboards.md) è disponibile per tutti gli utenti per creare insights da un modello di dati esistente.

Per informazioni sugli elementi dell&#39;interfaccia utente, consultare la [Guida utente di Query Editor](../../query-service/ui/user-guide.md#query-authoring).

![La finestra di dialogo [!UICONTROL Enter SQL] con il menu a discesa del set di dati e l&#39;icona Esegui evidenziata, la finestra di dialogo contiene una query SQL compilata e la scheda Parametri query visualizzata.](../images/sql-insights-query-pro-mode/enter-sql-database-dropdown.png)

### Parametri della query {#query-parameters}

Per includere [global](./filters/global-filter.md) o [filtri di data](./filters/date-filter.md) la query **deve** utilizzare i parametri di query. Quando componi l’istruzione in modalità query pro, devi fornire valori di esempio se la query utilizza parametri di query. I valori di esempio consentono di eseguire l&#39;istruzione SQL e generare il grafico. I valori di esempio forniti durante la composizione dell’istruzione vengono sostituiti dai valori effettivi selezionati per la data o il filtro globale in fase di esecuzione.

>[!IMPORTANT]
>
>Se si desidera utilizzare un filtro globale, è necessario inserire un parametro di query nell&#39;istruzione SQL e quindi collegare tale parametro di query al filtro globale nel compositore widget. Nella schermata seguente, `CONSENT_VALUE_FILTER` viene utilizzato nel linguaggio SQL come parametro di query per un filtro globale. Per ulteriori informazioni su come eseguire questa operazione, consulta la [documentazione del filtro globale](./filters/global-filter.md#enable-global-filter).

Per eseguire la query, selezionare l&#39;icona di esecuzione (![Icona di esecuzione.](/help/images/icons/play.png)). Nell&#39;Editor query viene visualizzata la scheda dei risultati. Quindi, per confermare la configurazione e aprire il compositore widget, selezionare **[!UICONTROL Select]**.

>[!TIP]
>
>Se la query utilizza parametri di query, eseguirla una sola volta per precompilare tutte le chiavi dei parametri di query utilizzate. La query non riuscirà, ma l’interfaccia utente visualizza automaticamente la scheda Parametri query ed elenca tutte le chiavi incluse. Aggiungi i valori appropriati per le chiavi.

![La finestra di dialogo [!UICONTROL Enter SQL] con input SQL, la scheda dei risultati visualizzata e l&#39;opzione Seleziona evidenziata.](../images/sql-insights-query-pro-mode/enter-sql-select.png)

## Popolare widget {#populate-widget}

Il compositore widget ora è popolato con le colonne dell&#39;SQL eseguito. Il tipo di dashboard è indicato in alto a sinistra, in questo caso è [!UICONTROL Manual SQL Entry]. Selezionare l&#39;icona della matita (![Un&#39;icona della matita.](/help/images/icons/edit.png)) per modificare l&#39;istruzione SQL in qualsiasi momento.

>[!TIP]
>
>Gli attributi disponibili sono colonne ricavate dall&#39;istruzione SQL eseguita.

Per creare il widget, utilizzare gli attributi elencati nella colonna [!UICONTROL Attributes]. È possibile utilizzare la barra di ricerca per cercare attributi o scorrere l&#39;elenco.

![Il compositore widget con il metodo di creazione e la colonna degli attributi evidenziati.](../images/sql-insights-query-pro-mode/creation-method-and-attribute-column.png)

### Aggiungi attributi {#add-attributes}

Per aggiungere un attributo al widget, selezionare l&#39;icona più (![A icona più.](/help/images/icons/add-circle.png)) accanto al nome di un attributo. Il menu a discesa visualizzato consente di aggiungere un attributo al grafico dalle opzioni determinate dall&#39;istruzione SQL. Diversi tipi di grafico dispongono di opzioni diverse, ad esempio un elenco a discesa degli assi X e Y.

In questo esempio di grafico ad anello, le opzioni sono dimensione e colore. Il colore suddivide i risultati del grafico ad anello e la dimensione corrisponde alla metrica effettiva utilizzata. Aggiungere un attributo al campo [!UICONTROL Color] per dividere i risultati in colori diversi in base alla composizione dell&#39;attributo.

>[!TIP]
>
>Selezionare l&#39;icona freccia su e freccia giù (![Icona freccia su e freccia giù.](/help/images/icons/switch.png)) per cambiare la disposizione degli assi X e Y nei grafici a barre o a linee.

![Il compositore widget con l&#39;icona del componente aggiuntivo a discesa e le frecce di selezione evidenziate.](../images/sql-insights-query-pro-mode/add-icon-and-switch-arrows.png)

Per modificare il tipo di grafico o il grafico del widget, selezionare una delle opzioni disponibili nel menu a discesa [!UICONTROL Marks]. Le opzioni includono [!UICONTROL Line], [!UICONTROL Donut], [!UICONTROL Big number] e [!UICONTROL Bar]. Una volta selezionata, viene generata una visualizzazione di anteprima delle impostazioni correnti del widget.

![Compositore widget con anteprima widget evidenziata.](../images/sql-insights-query-pro-mode/widget-preview.png)

## Attributi di tabella avanzati {#advanced-attributes}

Per applicare le funzionalità di ordinamento automatico a una o a tutte le colonne delle tabelle, selezionare **[!UICONTROL Edit]** per modificare l&#39;intero dashboard.

![Dashboard personalizzato con Modifica evidenziata.](../images/sql-insights-query-pro-mode/advanced-edit-dashboard.png)

Selezionare i puntini di sospensione (`...`) nel grafico a tabella in cui si desidera aggiungere l&#39;ordinamento delle colonne, quindi selezionare **[!UICONTROL Edit]**.

![Tabella che mostra il menu con i puntini di sospensione evidenziata da Modifica.](../images/sql-insights-query-pro-mode/advanced-table-edit.png)

Per abilitare l&#39;ordinamento per qualsiasi colonna, selezionare le caselle **[!UICONTROL Sortable]**.

![Pagina di modifica tabella con caselle di controllo ordinabili evidenziate.](../images/sql-insights-query-pro-mode/advanced-table-sortable.png)

Selezionare l&#39;icona delle proprietà (![Icona delle proprietà.](/help/images/icons/properties.png)) nella barra a destra per aprire il pannello [!UICONTROL Properties]. Nel pannello **[!UICONTROL Properties]**, utilizza il menu a discesa per selezionare la colonna **[!UICONTROL Default sort]**, quindi utilizza il menu a discesa per selezionare **[!UICONTROL Sort direction]**. Infine, selezionare **[!UICONTROL Save and close]**.

![Il compositore widget con l&#39;icona delle proprietà, l&#39;ordinamento predefinito, la direzione dell&#39;ordinamento, il salvataggio e la chiusura evidenziati.](../images/sql-insights-query-pro-mode/advanced-table-properties.png)

Per ulteriori informazioni sull&#39;utilizzo delle funzionalità di ordinamento, ridimensionamento delle colonne e impaginazione, vedere [Ulteriori informazioni](./view-more.md).

## Proprietà widget {#properties}

Selezionare l&#39;icona delle proprietà (![Icona delle proprietà.](/help/images/icons/properties.png)) nella barra a destra per aprire il pannello proprietà. Nel pannello [!UICONTROL Properties], immetti un nome per il widget nel campo di testo **[!UICONTROL Widget title]**. È inoltre possibile rinominare vari aspetti del grafico.

>[!NOTE]
>
>I campi specifici disponibili nella barra laterale delle proprietà variano a seconda del tipo di grafico che si sta modificando.

![Il compositore widget con l&#39;icona delle proprietà e il campo del titolo del widget evidenziati.](../images/sql-insights-query-pro-mode/widget-properties-title-text.png)

## Salvare il widget {#save-widget}

Se si salva nel compositore widget, il widget viene salvato localmente nel dashboard. Se si desidera salvare il lavoro e riprendere in seguito, selezionare **[!UICONTROL Save]**. Un&#39;icona di spunta sotto il nome del widget indica che il widget è stato salvato. In alternativa, se si è soddisfatti del widget, selezionare **[!UICONTROL Save and close]** per renderlo disponibile a tutti gli altri utenti con accesso al dashboard. Seleziona Annulla per abbandonare il lavoro e tornare al dashboard personalizzato.

![Il compositore widget con Salva, Widget salvato e Salva e chiudi evidenziato.](../images/sql-insights-query-pro-mode/insight-saved.png)

## Modificare dashboard e grafici {#edit}

Seleziona **[!UICONTROL Edit]** per modificare l&#39;intero dashboard o qualsiasi informazione. Dalla modalità di modifica è possibile ridimensionare i widget, modificare le istruzioni SQL o creare e applicare filtri globali e temporali. Questi filtri vincolano i dati visualizzati nei widget del dashboard. È un modo comodo per aggiornare e perfezionare rapidamente le informazioni per diversi casi d’uso.

![Dashboard personalizzato con Modifica evidenziata.](../images/sql-insights-query-pro-mode/edit-dashboard.png)

Selezionare **[!UICONTROL Add filter]** per creare [[!UICONTROL Date filter]](#create-date-filter) o [[!UICONTROL Global filter]](#create-global-filter). Dopo la creazione, tutti i filtri globali e di data sono disponibili da [icona filtro](#select-global-filter) (![icona filtro.](/help/images/icons/filter.png)) del tuo dashboard.

![Dashboard personalizzato con il menu a discesa Aggiungi filtro evidenziato.](../images/sql-insights-query-pro-mode/add-filter.png)

## Modificare, duplicare o eliminare un’insight

Per istruzioni su come [modificare, duplicare o eliminare un widget esistente](../standard-dashboards.md#duplicate), consulta la guida Dashboard personalizzato.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come scrivere query SQL nell’interfaccia utente di Adobe Experience Platform per generare grafici per le dashboard personalizzate. Successivamente, dovresti scoprire come arricchire ulteriormente i tuoi dati [creando un filtro data](./filters/date-filter.md) o [creando un filtro globale](./filters/global-filter.md).

Puoi anche saperne di più su altre funzionalità di Approfondimenti personalizzati, tra cui [le diverse opzioni di visualizzazione per i dati analizzati da SQL](./view-more.md) o come [visualizzare le istruzioni SQL alla base delle tue informazioni personalizzate](./view-sql.md).
