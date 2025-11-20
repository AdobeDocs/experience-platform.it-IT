---
title: Dashboard standard
description: Scopri come creare e gestire dashboard personalizzate che consentono di creare, aggiungere e modificare widget personalizzati per visualizzare le metriche chiave.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 1%

---

# Dashboard standard

Utilizza le dashboard di Adobe Experience Platform per velocizzare le informazioni e personalizzare la visualizzazione tramite la funzione Dashboard. Utilizza questa funzione per creare e gestire dashboard personalizzate che consentono di creare, aggiungere e modificare widget personalizzati per visualizzare metriche chiave rilevanti per la tua organizzazione.


<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## Creare un dashboard personalizzato

Per creare un dashboard personalizzato, passa innanzitutto all’inventario del dashboard. Seleziona **[!UICONTROL Dashboards]** dal menu di navigazione a sinistra dell&#39;interfaccia utente di Experience Platform, seguito da **[!UICONTROL Create dashboard]**.

![Inventario dashboard con dashboard nel menu di navigazione a sinistra ed evidenziata l&#39;opzione &quot;Crea dashboard&quot;.](./images/standard-dashboards/create-dashboard.png)

Prima di aggiungere un dashboard personalizzato, l’inventario dei dashboard è vuoto e viene visualizzato il messaggio &quot;Nessun dashboard trovato&quot;. messaggio. Una volta creati, tutti i dashboard vengono elencati nell’inventario dei dashboard.

<!-- >[!NOTE]
>
>To edit an existing dashboard, select the dashboard name from the inventory list followed by the pencil icon (![A pencil icon.](/help/images/icons/edit.png))
>![A custom inventory listed in the dashboard inventory.](./images/standard-dashboards/dashbaord-inventory.png "A custom inventory listed in the dashboard inventory."){width="100" zoomable="yes"} -->

Viene visualizzata la finestra di dialogo [!UICONTROL Create dashboard]. Immettere un nome descrittivo per la raccolta di widget che si desidera creare e selezionare **[!UICONTROL Save]**.

![Finestra di dialogo Crea dashboard.](./images/standard-dashboards/create-dashboard-dialog.png)

Gli utenti che hanno acquistato lo SKU di Data Distiller possono utilizzare query SQL personalizzate per ottenere informazioni approfondite. Per istruzioni su questo flusso di lavoro, consulta la [panoramica sulla modalità query pro](./sql-insights-query-pro-mode/overview.md).

La nuova dashboard vuota creata viene visualizzata con il nome scelto nell&#39;angolo superiore sinistro della visualizzazione.

## Creare un widget {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Numero massimo di widget"
>abstract="Il servizio dashboard supporta fino a dieci widget. Dopo aver aggiunto dieci widget al dashboard, l&#39;opzione [!UICONTROL Add new widget] è disabilitata e appare grigia."

Dalla nuova visualizzazione del dashboard, seleziona **[!UICONTROL Add new widget]** per avviare il processo di creazione del widget.

>[!IMPORTANT]
>
>Ogni dashboard supporta fino a dieci widget. Dopo aver aggiunto dieci widget al dashboard, l&#39;opzione [!UICONTROL Add new widget] è disabilitata e appare grigia.

![Il nuovo dashboard vuoto con Aggiungi nuovo widget evidenziato.](./images/standard-dashboards/add-new-widget.png)

### Compositore widget

Viene visualizzata l&#39;area di lavoro del compositore widget. Quindi, selezionare **[!UICONTROL Select data]** per scegliere il modello dati da cui aggiungere gli attributi ai widget.

![Area di lavoro del compositore widget.](./images/standard-dashboards/widget-composer.png)

#### Seleziona modello dati {#select-data-model}

Viene visualizzata la finestra di dialogo [!UICONTROL Select data model]. Seleziona un modello dati dalla colonna a sinistra per visualizzare un elenco di anteprima di tutte le tabelle disponibili. Il modello dati preconfigurato per Real-Time Customer Data Platform è denominato [!UICONTROL CDPInsights].

>[!TIP]
>
>Selezionare l&#39;icona delle informazioni (![Un&#39;icona delle informazioni.](/help/images/icons/info.png)) per visualizzare il nome completo del modello dati se è troppo lungo per essere visualizzato nella barra dei dati.

![Finestra di dialogo Seleziona dati.](./images/standard-dashboards/select-data-model-dialog.png)

L’elenco di anteprima fornisce dettagli sulle tabelle contenute nel modello dati. La tabella seguente fornisce le descrizioni dei campi colonna e dei relativi valori potenziali.

| Campo colonna | Descrizione |
|---|---|
| [!UICONTROL Title] | Nome della tabella. |
| [!UICONTROL Table type] | Tipo di tabella. I tipi potenziali includono: `fact`, `dimension` e `none`. |
| [!UICONTROL Records] | Numero di record associati alla tabella selezionata. |
| [!UICONTROL Lookups] | Numero di tabelle unite alla tabella selezionata. |
| [!UICONTROL Attributes] | Numero di attributi per la tabella selezionata. |

Seleziona **[!UICONTROL Next]** per confermare la scelta del modello dati. Nella vista successiva viene visualizzato un elenco delle tabelle disponibili nella barra a sinistra. Seleziona una tabella per visualizzare una suddivisione completa dei dati contenuti nella tabella selezionata.

### Popolare widget {#populate-widget}

Il pannello [!UICONTROL Preview] contiene schede per [!UICONTROL Sample records] e [!UICONTROL Attributes]. La scheda [!UICONTROL Sample records] fornisce un sottoinsieme dei record della tabella selezionata in una vista a tabella. La scheda [!UICONTROL Attributes] fornisce il nome attributo, il tipo di dati e la tabella di origine per ogni attributo associato alla tabella selezionata.

Selezionare una tabella dall&#39;elenco disponibile nella barra a sinistra per fornire i dati per il widget e selezionare **[!UICONTROL Select]** per tornare al compositore widget.

![Finestra di dialogo Seleziona dati con selezione evidenziata.](./images/standard-dashboards/select-a-table.png)

Il compositore widget ora è compilato con i dati della tabella scelta.

Il modello dati e la tabella attualmente selezionata vengono visualizzati nella parte superiore della barra a sinistra e gli attributi disponibili per la creazione del widget sono elencati nella colonna [!UICONTROL Attributes]. È possibile utilizzare la barra di ricerca per cercare attributi anziché scorrere l&#39;elenco oppure modificare il modello dati scelto selezionando l&#39;icona della matita (![icona della matita.](/help/images/icons/edit.png)) nella barra a sinistra.

![Un widget popolato con dati all&#39;interno del compositore widget.](./images/standard-dashboards/populated-widget-composer.png)

#### Aggiungere e filtrare gli attributi {#add-and-filter-attributes}

Selezionare l&#39;icona di aggiunta (![Un&#39;icona di aggiunta.](/help/images/icons/add-circle.png)) accanto al nome di un attributo per aggiungere un attributo al widget. Il menu a discesa visualizzato consente di aggiungere un attributo come asse X, asse Y, colore o filtro per il widget. L&#39;attributo [!UICONTROL Color] consente di differenziare i risultati dei segni dell&#39;asse X e Y in base al colore. A tale scopo, i risultati vengono suddivisi in colori diversi in base alla composizione di un terzo attributo.

>[!TIP]
>
>Se si desidera invertire la disposizione dell&#39;asse X e Y, selezionare l&#39;icona freccia su e freccia giù (![icona freccia su e freccia giù.](/help/images/icons/switch.png)) per cambiare la loro disposizione.

![Il compositore widget con il menu a discesa dell&#39;icona del componente aggiuntivo evidenziato.](./images/standard-dashboards/attributes-dropdown.png)

Per modificare il tipo di grafico o il grafico del widget, selezionare il menu a discesa [!UICONTROL Marks] e scegliere tra le opzioni disponibili. Le opzioni includono barre, punti, segni di graduazione, linee o area. Una volta selezionata, viene generata una visualizzazione di anteprima delle impostazioni correnti del widget.

![Il compositore widget con l&#39;elenco a discesa Indicatori evidenziato.](./images/standard-dashboards/marks-dropdown.png)

Aggiungendo un attributo come filtro, è possibile selezionare i valori da includere o escludere dal widget. Dopo aver aggiunto un filtro dall&#39;elenco degli attributi, viene visualizzata la finestra di dialogo [!UICONTROL Filter] in cui è possibile selezionare o deselezionare i valori utilizzando le relative caselle di controllo.

![Finestra di dialogo del filtro per filtrare i valori dal widget.](./images/standard-dashboards/filter-dialog.png)

#### Escludi i dati storici {#filter-historical-data}

Per filtrare i dati storici dalle informazioni generate dal widget, aggiungi l&#39;attributo `date_key` come filtro e seleziona **[!UICONTROL Recent date]** seguito da **[!UICONTROL Apply]**. Questo filtro assicura che i dati utilizzati per derivare informazioni vengano ricavati dall’istantanea di sistema più recente.

![La finestra di dialogo [!UICONTROL Filter: date_key] con [!UICONTROL Recent date] e [!UICONTROL Apply] è evidenziata.](./images/standard-dashboards/recent-date.png)

In alternativa, puoi creare un periodo personalizzato in base al quale filtrare i dati. Selezionare **[!UICONTROL Select dates]** per estendere la finestra di dialogo con un elenco di date disponibili. Utilizzare la casella di controllo **[!UICONTROL Select all]** per abilitare o disabilitare tutte le opzioni disponibili oppure selezionare la casella di controllo singolarmente per ogni giorno. Infine, selezionare **[!UICONTROL Apply]** per confermare le scelte.

>[!NOTE]
>
>Se l&#39;attributo `date_key` è già stato aggiunto come filtro, seleziona i puntini di sospensione seguiti da **[!UICONTROL Edit]** dalle opzioni a discesa per modificare il periodo del filtro.

![La finestra di dialogo [!UICONTROL Filter: date_key] con singole caselle di controllo del giorno è selezionata e deselezionata.](./images/standard-dashboards/select-dates.png)

### Proprietà widget

Selezionare l&#39;icona delle proprietà (![Icona delle proprietà.](/help/images/icons/properties.png)) nella barra a destra per aprire il pannello proprietà. Nel pannello [!UICONTROL Properties], immetti un nome per il widget nel campo di testo [!UICONTROL Widget title].

![Il pannello delle proprietà con l&#39;icona delle proprietà e il campo del titolo del widget evidenziato.](./images/standard-dashboards/properties-panel.png)

Dal pannello delle proprietà del widget, puoi modificare diversi aspetti del widget. È disponibile il controllo completo per modificare la posizione della legenda del widget. Per spostare la legenda, selezionare il menu a discesa [!UICONTROL Legend placement] e scegliere la posizione desiderata dall&#39;elenco delle opzioni disponibili. È inoltre possibile rinominare l&#39;etichetta associata alla legenda e l&#39;asse X o Y immettendo un nuovo nome rispettivamente nel campo di testo [!UICONTROL Legend title] o nel campo di testo [!UICONTROL Axis label].

#### Salvare il widget {#save-widget}

Se si salva nel compositore widget, il widget viene salvato localmente nel dashboard. Se si desidera salvare il lavoro e riprendere in un secondo momento, selezionare **[!UICONTROL Save]**. Un&#39;icona di spunta sotto il nome del widget indica che il widget è stato salvato. In alternativa, se si è soddisfatti del widget, selezionare **[!UICONTROL Save and close]** per renderlo disponibile a tutti gli altri utenti con accesso al dashboard. Seleziona **[!UICONTROL Cancel]** per abbandonare il tuo lavoro e tornare al tuo dashboard personalizzato.

![Conferma salvataggio nuovo widget.](./images/standard-dashboards/save-confirmation.png)

>[!TIP]
>
>Selezionare l&#39;icona delle proprietà (![Icona delle proprietà.](/help/images/icons/properties.png)) accanto al nome del dashboard per visualizzare i dettagli sulla sua creazione. Puoi modificare il nome del dashboard nella finestra di dialogo visualizzata.

I widget possono essere ridisposti e ridimensionati mentre si trovano in questa area di lavoro. Seleziona **[!UICONTROL Save]** per mantenere il nome del dashboard e il layout configurato.

![Dashboard definito dall&#39;utente con widget personalizzato e pulsante Salva evidenziato.](./images/standard-dashboards/user-defined-dashboard.png)

Per garantire che ogni query per un dashboard di approfondimenti di Adobe Real-Time Customer Data Platform disponga di risorse sufficienti per essere eseguita in modo efficiente, l’API tiene traccia dell’utilizzo delle risorse assegnando slot di concorrenza a ogni query. Il sistema può elaborare fino a quattro query simultanee, pertanto sono disponibili quattro slot di query simultanee in un dato momento. Le query vengono inserite in una coda in base agli slot di concorrenza, quindi attendi nella coda fino a quando non sono disponibili abbastanza slot di concorrenza.

### Modificare, duplicare o eliminare un widget {#duplicate}

Dopo aver creato un widget, è possibile modificarlo, duplicarlo o eliminarlo completamente dal dashboard personalizzato.

>[!TIP]
>
>Per passare da un dashboard personalizzato all’altro, seleziona Dashboard nella barra di navigazione a sinistra, quindi seleziona il nome del dashboard dall’elenco di inventario.

Selezionare l&#39;icona della matita (![Un&#39;icona della matita.](/help/images/icons/edit.png)) dall&#39;alto a destra del dashboard personalizzato per accedere alla modalità di modifica.

![Dashboard personalizzato con l&#39;icona della matita evidenziata.](./images/standard-dashboards/edit-mode.png)

Quindi, seleziona i puntini di sospensione in alto a destra del widget che desideri modificare, copiare o eliminare. Seleziona l’azione appropriata dal menu a discesa.

![Un widget in un dashboard personalizzato con i puntini di sospensione e i widget duplicati evidenziati.](./images/standard-dashboards/duplicate.png)

>[!NOTE]
>
>La duplicazione consente di personalizzare gli attributi di un insight per creare un widget univoco senza dover iniziare da zero. Se si duplica un widget, questo viene visualizzato nel dashboard personalizzato. Puoi quindi selezionare i puntini di sospensione del nuovo widget, seguiti da **[!UICONTROL Edit]**, per personalizzare insight.

## Passaggi successivi e risorse aggiuntive

La lettura di questo documento consente di comprendere meglio come creare un dashboard personalizzato e come creare, modificare e aggiornare i widget personalizzati per tale dashboard.

Per scoprire le metriche e le visualizzazioni preconfigurate disponibili per i dashboard [profili](./guides/profiles.md#standard-widgets), [segmenti](./guides/audiences.md#standard-widgets) e [destinazioni](./guides/destinations.md#standard-widgets), consulta l&#39;elenco dei widget standard nella rispettiva documentazione.

Per approfondire la conoscenza delle dashboard in Experience Platform, guarda il video seguente:

>[!VIDEO](https://video.tv.adobe.com/v/3409637?quality=12&learn=on)
