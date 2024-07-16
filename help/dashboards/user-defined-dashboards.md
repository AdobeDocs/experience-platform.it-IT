---
title: Dashboard personalizzati
description: Scopri come creare e gestire dashboard personalizzate che consentono di creare, aggiungere e modificare widget personalizzati per visualizzare le metriche chiave.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: 17ad52864bbca09844c0241b6451e6811bd8f413
workflow-type: tm+mt
source-wordcount: '1624'
ht-degree: 3%

---

# Dashboard personalizzati

Utilizza le dashboard di Adobe Experience Platform per velocizzare le informazioni e personalizzare la visualizzazione tramite la funzione Dashboard. Utilizza questa funzione per creare e gestire dashboard personalizzate che consentono di creare, aggiungere e modificare widget personalizzati per visualizzare metriche chiave rilevanti per la tua organizzazione.


<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## Creare un dashboard personalizzato

Per creare un dashboard personalizzato, passa innanzitutto all’inventario del dashboard. Seleziona **[!UICONTROL Dashboard]** dalla navigazione a sinistra dell&#39;interfaccia utente di Platform, seguito da **[!UICONTROL Crea dashboard]**.

![Inventario dashboard con dashboard nel menu di navigazione a sinistra ed evidenziata l&#39;opzione &quot;Crea dashboard&quot;.](./images/user-defined-dashboards/create-dashboard.png)

Prima di aggiungere un dashboard personalizzato, l’inventario dei dashboard è vuoto e viene visualizzato il messaggio &quot;Nessun dashboard trovato&quot;. messaggio. Una volta creati, tutti i dashboard vengono elencati nell’inventario dei dashboard.

<!-- >[!NOTE]
>
>To edit an existing dashboard, select the dashboard name from the inventory list followed by the pencil icon (![A pencil icon.](./images/user-defined-dashboards/edit-icon.png))
>![A custom inventory listed in the dashboard inventory.](./images/user-defined-dashboards/dashbaord-inventory.png "A custom inventory listed in the dashboard inventory."){width="100" zoomable="yes"} -->

Viene visualizzata la finestra di dialogo [!UICONTROL Crea dashboard]. Immettere un nome descrittivo per la raccolta di widget che si desidera creare e selezionare **[!UICONTROL Salva]**.

![Finestra di dialogo Crea dashboard.](./images/user-defined-dashboards/create-dashboard-dialog.png)

Gli utenti che hanno acquistato lo SKU di Data Distiller possono utilizzare query SQL personalizzate per ottenere informazioni approfondite. Per istruzioni su questo flusso di lavoro, consulta la [Guida alla creazione di Insight personalizzabile](./data-distiller/customizable-insights/overview.md).

La nuova dashboard vuota creata viene visualizzata con il nome scelto nell&#39;angolo superiore sinistro della visualizzazione.

## Creare un widget {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Numero massimo di widget"
>abstract="Il servizio dashboard supporta fino a dieci widget. Dopo aver aggiunto dieci widget alla dashboard, l’opzione [!UICONTROL Aggiungi nuovo widget] è disabilitata e appare grigia."

Dalla nuova visualizzazione del dashboard, seleziona **[!UICONTROL Aggiungi nuovo widget]** per iniziare il processo di creazione del widget.

>[!IMPORTANT]
>
>Ogni dashboard supporta fino a dieci widget. Dopo aver aggiunto dieci widget alla dashboard, l’opzione [!UICONTROL Aggiungi nuovo widget] è disabilitata e appare grigia.

![Il nuovo dashboard vuoto con Aggiungi nuovo widget evidenziato.](./images/user-defined-dashboards/add-new-widget.png)

### Compositore widget

Viene visualizzata l&#39;area di lavoro del compositore widget. Quindi, seleziona **[!UICONTROL Seleziona dati]** per scegliere il modello di dati da cui aggiungere gli attributi ai widget.

![Area di lavoro del compositore widget.](./images/user-defined-dashboards/widget-composer.png)

#### Seleziona modello dati {#select-data-model}

Viene visualizzata la finestra di dialogo [!UICONTROL Seleziona modello dati]. Seleziona un modello dati dalla colonna a sinistra per visualizzare un elenco di anteprima di tutte le tabelle disponibili. Il modello dati preconfigurato per Real-time Customer Data Platform è denominato [!UICONTROL CDPInsights].

>[!TIP]
>
>Selezionare l&#39;icona delle informazioni (![Un&#39;icona delle informazioni.](./images/user-defined-dashboards/info-icon.png)) per visualizzare il nome completo del modello dati se è troppo lungo per essere visualizzato nella barra dei dati.

![Finestra di dialogo Seleziona dati.](./images/user-defined-dashboards/select-data-model-dialog.png)

L’elenco di anteprima fornisce dettagli sulle tabelle contenute nel modello dati. La tabella seguente fornisce le descrizioni dei campi colonna e dei relativi valori potenziali.

| Campo colonna | Descrizione |
|---|---|
| [!UICONTROL Titolo] | Nome della tabella. |
| [!UICONTROL Tipo di tabella] | Tipo di tabella. I tipi potenziali includono: `fact`, `dimension` e `none`. |
| [!UICONTROL Record] | Numero di record associati alla tabella selezionata. |
| [!UICONTROL Ricerche] | Numero di tabelle unite alla tabella selezionata. |
| [!UICONTROL Attributi] | Numero di attributi per la tabella selezionata. |

Seleziona **[!UICONTROL Avanti]** per confermare la scelta del modello dati. Nella vista successiva viene visualizzato un elenco delle tabelle disponibili nella barra a sinistra. Seleziona una tabella per visualizzare una suddivisione completa dei dati contenuti nella tabella selezionata.

### Popolare widget {#populate-widget}

Il pannello [!UICONTROL Anteprima] contiene schede per [!UICONTROL Record di esempio] e [!UICONTROL Attributi]. La scheda [!UICONTROL Record di esempio] fornisce un sottoinsieme dei record della tabella selezionata in una vista a tabella. La scheda [!UICONTROL Attributi] fornisce il nome attributo, il tipo di dati e la tabella di origine per ogni attributo associato alla tabella selezionata.

Seleziona una tabella dall&#39;elenco disponibile nella barra a sinistra per fornire i dati per il widget, quindi seleziona **[!UICONTROL Seleziona]** per tornare al compositore widget.

![Finestra di dialogo Seleziona dati con selezione evidenziata.](./images/user-defined-dashboards/select-a-table.png)

Il compositore widget ora è compilato con i dati della tabella scelta.

Il modello dati e la tabella attualmente selezionata vengono visualizzati nella parte superiore della barra a sinistra e gli attributi disponibili per la creazione del widget sono elencati nella colonna [!UICONTROL Attributi]. È possibile utilizzare la barra di ricerca per cercare attributi anziché scorrere l&#39;elenco oppure modificare il modello dati scelto selezionando l&#39;icona della matita (![icona della matita.](./images/user-defined-dashboards/edit-icon.png)) nella barra a sinistra.

![Un widget popolato con dati all&#39;interno del compositore widget.](./images/user-defined-dashboards/populated-widget-composer.png)

#### Aggiungere e filtrare gli attributi {#add-and-filter-attributes}

Selezionare l&#39;icona di aggiunta (![Un&#39;icona di aggiunta.](./images/user-defined-dashboards/add-icon.png)) accanto al nome di un attributo per aggiungere un attributo al widget. Il menu a discesa visualizzato consente di aggiungere un attributo come asse X, asse Y, colore o filtro per il widget. L&#39;attributo [!UICONTROL Color] consente di differenziare i risultati degli indicatori dell&#39;asse X e Y in base al colore. A tale scopo, i risultati vengono suddivisi in colori diversi in base alla composizione di un terzo attributo.

>[!TIP]
>
>Se si desidera invertire la disposizione dell&#39;asse X e Y, selezionare l&#39;icona freccia su e freccia giù (![icona freccia su e freccia giù.](./images/user-defined-dashboards/switch-axis-icon.png)) per cambiare la loro disposizione.

![Il compositore widget con il menu a discesa dell&#39;icona del componente aggiuntivo evidenziato.](./images/user-defined-dashboards/attributes-dropdown.png)

Per modificare il tipo di grafico o il grafico del widget, seleziona il menu a discesa [!UICONTROL Indicatori] e scegli tra le opzioni disponibili. Le opzioni includono barre, punti, segni di graduazione, linee o area. Una volta selezionata, viene generata una visualizzazione di anteprima delle impostazioni correnti del widget.

![Il compositore widget con l&#39;elenco a discesa Indicatori evidenziato.](./images/user-defined-dashboards/marks-dropdown.png)

Aggiungendo un attributo come filtro, è possibile selezionare i valori da includere o escludere dal widget. Dopo aver aggiunto un filtro dall&#39;elenco degli attributi, viene visualizzata la finestra di dialogo [!UICONTROL Filtro] in cui è possibile selezionare o deselezionare i valori utilizzando le relative caselle di controllo.

![Finestra di dialogo del filtro per filtrare i valori dal widget.](./images/user-defined-dashboards/filter-dialog.png)

#### Escludi i dati storici {#filter-historical-data}

Per filtrare i dati storici dalle informazioni generate dal widget, aggiungi l&#39;attributo `date_key` come filtro e seleziona **[!UICONTROL Data recente]** seguita da **[!UICONTROL Applica]**. Questo filtro assicura che i dati utilizzati per derivare informazioni vengano ricavati dall’istantanea di sistema più recente.

![Finestra di dialogo [!UICONTROL Filtro: date_key] con [!UICONTROL Data recente] e [!UICONTROL Applica] evidenziata.](./images/user-defined-dashboards/recent-date.png)

In alternativa, puoi creare un periodo personalizzato in base al quale filtrare i dati. Seleziona **[!UICONTROL Seleziona date]** per estendere la finestra di dialogo con un elenco di date disponibili. Utilizza la casella di controllo **[!UICONTROL Seleziona tutto]** per abilitare o disabilitare tutte le opzioni disponibili oppure seleziona la casella di controllo singolarmente per ogni giorno. Infine, seleziona **[!UICONTROL Applica]** per confermare le scelte effettuate.

>[!NOTE]
>
>Se l&#39;attributo `date_key` è già stato aggiunto come filtro, seleziona i puntini di sospensione seguiti da **[!UICONTROL Modifica]** dalle opzioni a discesa per modificare il periodo del filtro.

![La finestra di dialogo [!UICONTROL Filtro: date_key] con caselle di controllo per i singoli giorni è selezionata e deselezionata.](./images/user-defined-dashboards/select-dates.png)

### Proprietà widget

Selezionare l&#39;icona delle proprietà (![Icona delle proprietà.](./images/user-defined-dashboards/properties-icon.png)) nella barra a destra per aprire il pannello proprietà. Nel pannello [!UICONTROL Proprietà], immetti un nome per il widget nel campo di testo [!UICONTROL Titolo widget].

![Il pannello delle proprietà con l&#39;icona delle proprietà e il campo del titolo del widget evidenziato.](./images/user-defined-dashboards/properties-panel.png)

Dal pannello delle proprietà del widget, puoi modificare diversi aspetti del widget. È disponibile il controllo completo per modificare la posizione della legenda del widget. Per spostare la legenda, selezionare il menu a discesa [!UICONTROL Posizione legenda] e scegliere la posizione desiderata dall&#39;elenco delle opzioni disponibili. È inoltre possibile rinominare l&#39;etichetta associata alla legenda e l&#39;asse X o Y immettendo un nuovo nome rispettivamente nel campo di testo [!UICONTROL Titolo legenda] o [!UICONTROL Etichetta asse].

#### Salvare il widget {#save-widget}

Se si salva nel compositore widget, il widget viene salvato localmente nel dashboard. Se desideri salvare il lavoro e riprenderlo in un secondo momento, seleziona **[!UICONTROL Salva]**. Un&#39;icona di spunta sotto il nome del widget indica che il widget è stato salvato. In alternativa, se si è soddisfatti del widget, selezionare **[!UICONTROL Salva e chiudi]** per rendere il widget disponibile a tutti gli altri utenti con accesso al dashboard. Seleziona **[!UICONTROL Annulla]** per abbandonare il lavoro e tornare al dashboard personalizzato.

![Conferma salvataggio nuovo widget.](./images/user-defined-dashboards/save-confirmation.png)

>[!TIP]
>
>Selezionare l&#39;icona delle proprietà (![Icona delle proprietà.](./images/user-defined-dashboards/properties-icon.png)) accanto al nome del dashboard per visualizzare i dettagli sulla sua creazione. Puoi modificare il nome del dashboard nella finestra di dialogo visualizzata.

I widget possono essere ridisposti e ridimensionati mentre si trovano in questa area di lavoro. Seleziona **[!UICONTROL Salva]** per mantenere il nome del dashboard e il layout configurato.

![Dashboard definito dall&#39;utente con widget personalizzato e pulsante Salva evidenziato.](./images/user-defined-dashboards/user-defined-dashboard.png)

Per garantire che ogni query per un dashboard di approfondimenti di Adobe Real-time Customer Data Platform disponga di risorse sufficienti per essere eseguita in modo efficiente, l’API tiene traccia dell’utilizzo delle risorse assegnando slot di concorrenza a ogni query. Il sistema può elaborare fino a quattro query simultanee, pertanto sono disponibili quattro slot di query simultanee in un dato momento. Le query vengono inserite in una coda in base agli slot di concorrenza, quindi attendi nella coda fino a quando non sono disponibili abbastanza slot di concorrenza.

### Modificare, duplicare o eliminare un widget {#duplicate}

Dopo aver creato un widget, è possibile modificarlo, duplicarlo o eliminarlo completamente dal dashboard personalizzato.

>[!TIP]
>
>Per passare da un dashboard personalizzato all’altro, seleziona Dashboard nella barra di navigazione a sinistra, quindi seleziona il nome del dashboard dall’elenco di inventario.

Selezionare l&#39;icona della matita (![Un&#39;icona della matita.](./images/user-defined-dashboards/edit-icon.png)) dall&#39;alto a destra del dashboard personalizzato per accedere alla modalità di modifica.

![Dashboard personalizzato con l&#39;icona della matita evidenziata.](./images/user-defined-dashboards/edit-mode.png)

Quindi, seleziona i puntini di sospensione in alto a destra del widget che desideri modificare, copiare o eliminare. Seleziona l’azione appropriata dal menu a discesa.

![Un widget in un dashboard personalizzato con i puntini di sospensione e i widget duplicati evidenziati.](./images/user-defined-dashboards/duplicate.png)

>[!NOTE]
>
>La duplicazione consente di personalizzare gli attributi di un approfondimento per creare un widget univoco senza dover iniziare da zero. Se si duplica un widget, questo viene visualizzato nel dashboard personalizzato. Puoi quindi selezionare i puntini di sospensione del nuovo widget, seguiti da **[!UICONTROL Modifica]**, per personalizzare le informazioni.

## Passaggi successivi e risorse aggiuntive

La lettura di questo documento consente di comprendere meglio come creare un dashboard personalizzato e come creare, modificare e aggiornare i widget personalizzati per tale dashboard.

Per scoprire le metriche e le visualizzazioni preconfigurate disponibili per i dashboard [profili](./guides/profiles.md#standard-widgets), [segmenti](./guides/audiences.md#standard-widgets) e [destinazioni](./guides/destinations.md#standard-widgets), consulta l&#39;elenco dei widget standard nella rispettiva documentazione.

Per approfondire la comprensione delle dashboard in Experience Platform, guarda il video seguente:

>[!VIDEO](https://video.tv.adobe.com/v/3409637?quality=12&learn=on)
