---
title: Dashboard definiti dall'utente
description: Scopri come creare e gestire dashboard personalizzate che consentono di creare, aggiungere e modificare widget personalizzati per visualizzare le metriche chiave.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: b3bd7a5ba1847518beafd12240c0d3a433a891d0
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 4%

---

# Dashboard definite dall’utente

Le dashboard di Adobe Experience Platform consentono di velocizzare le informazioni e personalizzare la visualizzazione tramite la funzione delle dashboard definite dall’utente. Questa funzione ti consente di creare e gestire dashboard personalizzate in cui creare, aggiungere e modificare widget personalizzati per visualizzare metriche chiave rilevanti per la tua organizzazione.

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## Creare un dashboard personalizzato

Per creare un dashboard personalizzato, passa innanzitutto all’inventario del dashboard. Seleziona **[!UICONTROL Dashboard]** dalla barra di navigazione a sinistra dell’interfaccia utente di Platform, seguita da **[!UICONTROL Crea dashboard]**.

![Inventario delle dashboard con le dashboard nella barra di navigazione a sinistra ed evidenziata l’opzione &quot;Crea dashboard&quot;.](./images/user-defined-dashboards/create-dashboard.png)

Prima di aggiungere un dashboard personalizzato, l’inventario dei dashboard è vuoto e viene visualizzato il messaggio &quot;Nessun dashboard trovato&quot;. messaggio. Una volta creati, tutti i dashboard definiti dall’utente sono elencati nell’inventario dei dashboard.

>[!NOTE]
>
>Per modificare un dashboard esistente, seleziona il nome del dashboard dall’elenco di inventario seguito dall’icona a forma di matita (![Un’icona a forma di matita.](./images/user-defined-dashboards/edit-icon.png))

Il [!UICONTROL Crea dashboard] viene visualizzata. Immettete un nome descrittivo per la raccolta di widget che intendete creare e selezionate **[!UICONTROL Salva]**.

![Finestra di dialogo Crea dashboard.](./images/user-defined-dashboards/create-dashboard-dialog.png)

La nuova dashboard vuota creata viene visualizzata con il nome scelto nell&#39;angolo superiore sinistro della visualizzazione.

## Creare un widget {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Numero massimo di widget"
>abstract="Le dashboard definite dall’utente supportano fino a dieci widget. Dopo aver aggiunto dieci widget alla dashboard, l’opzione [!UICONTROL Aggiungi nuovo widget] è disabilitata e appare grigia."

Dalla nuova vista del dashboard, seleziona **[!UICONTROL Aggiungi nuovo widget]** per avviare il processo di creazione del widget.

>[!IMPORTANT]
>
>Le dashboard definite dall’utente supportano fino a dieci widget. Dopo aver aggiunto dieci widget alla dashboard, l’opzione [!UICONTROL Aggiungi nuovo widget] è disabilitata e appare grigia.

![Il nuovo dashboard vuoto con Aggiungi nuovo widget evidenziato.](./images/user-defined-dashboards/add-new-widget.png)

### Compositore widget

Viene visualizzata l&#39;area di lavoro del compositore widget. Quindi, seleziona **[!UICONTROL Seleziona dati]** per scegliere il modello dati da cui aggiungere attributi ai widget.

![Area di lavoro del compositore widget.](./images/user-defined-dashboards/widget-composer.png)

#### Seleziona modello dati {#select-data-model}

Il [!UICONTROL Seleziona modello dati] viene visualizzata. Seleziona un modello dati dalla colonna a sinistra per visualizzare un elenco di anteprima di tutte le tabelle disponibili. Il modello dati preconfigurato per Real-time Customer Data Platform è denominato [!UICONTROL CDPInsights].

>[!TIP]
>
>Seleziona l’icona delle informazioni (![Icona delle informazioni.](./images/user-defined-dashboards/info-icon.png)) per visualizzare il nome completo del modello dati, se è troppo lungo per essere visualizzato nella barra dei dati.

![La finestra di dialogo Seleziona dati.](./images/user-defined-dashboards/select-data-model-dialog.png)

L’elenco di anteprima fornisce dettagli sulle tabelle contenute nel modello dati. La tabella seguente fornisce le descrizioni dei campi colonna e dei relativi valori potenziali.

| Campo colonna | Descrizione |
|---|---|
| [!UICONTROL Titolo] | Nome della tabella. |
| [!UICONTROL Tipo di tabella] | Tipo di tabella. I tipi potenziali includono: `fact`, `dimension`, e `none`. |
| [!UICONTROL Record] | Numero di record associati alla tabella selezionata. |
| [!UICONTROL Ricerche] | Numero di tabelle unite alla tabella selezionata. |
| [!UICONTROL Attributi] | Numero di attributi per la tabella selezionata. |

Seleziona **[!UICONTROL Successivo]** per confermare la scelta del modello dati. Nella vista successiva viene visualizzato un elenco delle tabelle disponibili nella barra a sinistra. Seleziona una tabella per visualizzare una suddivisione completa dei dati contenuti nella tabella selezionata.

### Popolare widget {#populate-widget}

Il [!UICONTROL Anteprima] il pannello contiene schede per [!UICONTROL Record di esempio] e [!UICONTROL Attributi]. Il [!UICONTROL Record di esempio] fornisce un sottoinsieme dei record della tabella selezionata in una vista a tabella. Il [!UICONTROL Attributi] fornisce il nome attributo, il tipo di dati e la tabella di origine per ogni attributo associato alla tabella selezionata.

Seleziona una tabella dall’elenco disponibile nella barra a sinistra per fornire i dati per il widget, quindi seleziona **[!UICONTROL Seleziona]** per tornare al compositore widget.

![La finestra di dialogo Seleziona dati con seleziona evidenziato.](./images/user-defined-dashboards/select-a-table.png)

Il compositore widget ora è compilato con i dati della tabella scelta.

Il modello dati e la tabella attualmente selezionata vengono visualizzati nella parte superiore della barra a sinistra e gli attributi disponibili per creare il widget sono elencati nella [!UICONTROL Attributi] colonna. È possibile utilizzare la barra di ricerca per cercare attributi invece di scorrere l’elenco oppure modificare il modello di dati scelto selezionando l’icona a forma di matita (![Icona della matita.](./images/user-defined-dashboards/edit-icon.png)) nella barra a sinistra.

![Un widget popolato con dati all&#39;interno del compositore widget.](./images/user-defined-dashboards/populated-widget-composer.png)

#### Aggiungere e filtrare gli attributi {#add-and-filter-attributes}

Seleziona l’icona Aggiungi (![Icona di aggiunta.](./images/user-defined-dashboards/add-icon.png)) accanto al nome di un attributo per aggiungere un attributo al widget. Il menu a discesa visualizzato consente di aggiungere un attributo come asse X, asse Y, colore o filtro per il widget. Il [!UICONTROL Colore] L&#39;attributo consente di differenziare i risultati degli indicatori dell&#39;asse X e Y in base al colore. A tale scopo, i risultati vengono suddivisi in colori diversi in base alla composizione di un terzo attributo.

>[!TIP]
>
>Se si desidera capovolgere la disposizione dell&#39;asse X e Y, selezionare l&#39;icona freccia su e giù (![Icona freccia su e freccia giù.](./images/user-defined-dashboards/switch-axis-icon.png)) per cambiare la loro disposizione.

![Il compositore widget con l’icona del componente aggiuntivo evidenziata a discesa.](./images/user-defined-dashboards/attributes-dropdown.png)

Per modificare il tipo di grafico o il grafico del widget, selezionare [!UICONTROL Indicatori] e scegli tra le opzioni disponibili. Le opzioni includono barre, punti, segni di graduazione, linee o area. Una volta selezionata, viene generata una visualizzazione di anteprima delle impostazioni correnti del widget.

![Il compositore widget con l’elenco a discesa Contrassegni evidenziato.](./images/user-defined-dashboards/marks-dropdown.png)

Aggiungendo un attributo come filtro, è possibile selezionare i valori da includere o escludere dal widget. Dopo l’aggiunta di un filtro dall’elenco degli attributi, il [!UICONTROL Filtro] viene visualizzata una finestra di dialogo in cui è possibile selezionare o deselezionare i valori utilizzando le relative caselle di controllo.

![Finestra di dialogo del filtro per filtrare i valori dal widget.](./images/user-defined-dashboards/filter-dialog.png)

#### Escludi i dati storici {#filter-historical-data}

Per filtrare i dati storici dalle informazioni generate dal widget, aggiungi `date_key` attributo come filtro e seleziona **[!UICONTROL Data recente]** seguito da **[!UICONTROL Applica]**. Questo filtro assicura che i dati utilizzati per derivare informazioni vengano ricavati dall’istantanea di sistema più recente.

![Il [!UICONTROL Filtro: date_key] dialogo con [!UICONTROL Data recente] e [!UICONTROL Applica] evidenziato.](./images/user-defined-dashboards/recent-date.png)

In alternativa, puoi creare un periodo personalizzato in base al quale filtrare i dati. Seleziona **[!UICONTROL Seleziona date]** per estendere la finestra di dialogo con un elenco di date disponibili. Utilizza il **[!UICONTROL Seleziona tutto]** per abilitare o disabilitare tutte le opzioni disponibili, oppure selezionare la casella di controllo singolarmente per ogni giorno. Infine, seleziona **[!UICONTROL Applica]** per confermare le scelte effettuate.

>[!NOTE]
>
>Se il `date_key` è già stato aggiunto come filtro, seleziona i puntini di sospensione seguiti da **[!UICONTROL Modifica]** dalle opzioni a discesa per modificare il periodo del filtro.

![Il [!UICONTROL Filtro: date_key] finestra di dialogo con singole caselle di controllo giorno sia selezionata che deselezionata.](./images/user-defined-dashboards/select-dates.png)

### Proprietà widget

Seleziona l’icona delle proprietà (![Icona delle proprietà.](./images/user-defined-dashboards/properties-icon.png)) nella barra a destra per aprire il pannello proprietà. In [!UICONTROL Proprietà] , immettere un nome per il widget nel [!UICONTROL Titolo widget] campo di testo.

![Il pannello delle proprietà con l’icona delle proprietà ed evidenziato il campo del titolo del widget.](./images/user-defined-dashboards/properties-panel.png)

Dal pannello delle proprietà del widget, puoi modificare diversi aspetti del widget. È disponibile il controllo completo per modificare la posizione della legenda del widget. Per spostare la legenda, selezionare [!UICONTROL Posizionamento legenda] e scegli la posizione desiderata dall’elenco delle opzioni disponibili. È inoltre possibile rinominare l&#39;etichetta associata alla legenda e l&#39;asse X o Y immettendo un nuovo nome nella [!UICONTROL Titolo legenda] campo di testo, oppure [!UICONTROL Etichetta asse] rispettivamente.

#### Salvare il widget {#save-widget}

Se si salva nel compositore widget, il widget viene salvato localmente nel dashboard. Se si desidera salvare il lavoro e riprendere in un secondo momento, selezionare **[!UICONTROL Salva]**. Un&#39;icona di spunta sotto il nome del widget indica che il widget è stato salvato. In alternativa, quando si è soddisfatti del widget, selezionare **[!UICONTROL Salva e chiudi]** per rendere il widget disponibile a tutti gli altri utenti con accesso al dashboard. Seleziona **[!UICONTROL Annulla]** per abbandonare il lavoro e tornare alla dashboard personalizzata.

![Conferma del salvataggio del nuovo widget.](./images/user-defined-dashboards/save-confirmation.png)

>[!TIP]
>
>Seleziona l’icona delle proprietà (![Icona delle proprietà.](./images/user-defined-dashboards/properties-icon.png)) accanto al nome del dashboard per visualizzare i dettagli sulla sua creazione. Puoi modificare il nome del dashboard nella finestra di dialogo visualizzata.

I widget possono essere ridisposti e ridimensionati mentre si trovano in questa area di lavoro. Seleziona **[!UICONTROL Salva]** per mantenere il nome del dashboard e il layout configurato.

![Dashboard definita dall&#39;utente con widget personalizzato ed evidenziato il pulsante Salva.](./images/user-defined-dashboards/user-defined-dashboard.png)

Per garantire che ogni query per un dashboard di approfondimenti di Adobe Real-time Customer Data Platform disponga di risorse sufficienti per essere eseguita in modo efficiente, l’API tiene traccia dell’utilizzo delle risorse assegnando slot di concorrenza a ogni query. Il sistema può elaborare fino a quattro query simultanee, pertanto sono disponibili quattro slot di query simultanee in un dato momento. Le query vengono inserite in una coda in base agli slot di concorrenza, quindi attendi nella coda fino a quando non sono disponibili abbastanza slot di concorrenza.

### Duplicare un widget

Dopo aver creato un widget, puoi duplicarne l’intero widget e personalizzarne gli attributi per creare un widget univoco senza dover iniziare da zero. Per duplicare un widget, passa innanzitutto all&#39;inventario del dashboard. Selezionare quindi il nome del dashboard dall&#39;elenco di inventario. Viene visualizzata la dashboard personalizzata.

![Nell’interfaccia utente di Platform sono evidenziati i dashboard e il nome di un dashboard personalizzato.](./images/user-defined-dashboards/dashbaord-inventory.png)

Seleziona l’icona della matita (![Un’icona a forma di matita.](./images/user-defined-dashboards/edit-icon.png)) in alto a destra nel dashboard personalizzato per accedere alla modalità di modifica.

![Dashboard personalizzato con l’icona della matita evidenziata.](./images/user-defined-dashboards/edit-mode.png)

Quindi, seleziona le ellissi in alto a destra del widget che desideri copiare, seguite da **[!UICONTROL Duplica]** dall’elenco delle opzioni disponibili.

![Un widget in un dashboard definito dall&#39;utente con i puntini di sospensione e Duplica widget evidenziati.](./images/user-defined-dashboards/duplicate.png)

Nel dashboard definito dall&#39;utente viene visualizzato un widget duplicato. Seleziona le ellissi del nuovo widget, seguite da **[!UICONTROL Modifica]**, per personalizzare il nuovo widget.

## Passaggi successivi e risorse aggiuntive

La lettura di questo documento consente di comprendere meglio come creare un dashboard personalizzato e come creare, modificare e aggiornare i widget personalizzati per tale dashboard.

Per scoprire le metriche e le visualizzazioni preconfigurate disponibili per [profili](./guides/profiles.md#standard-widgets), [segmenti](./guides/audiences.md#standard-widgets), e [destinazioni](./guides/destinations.md#standard-widgets) dashboard, consulta l’elenco dei widget standard nella rispettiva documentazione.

Per comprendere meglio le dashboard definite dall’utente in questo Experience Platform, guarda il video seguente:

>[!VIDEO](https://video.tv.adobe.com/v/3409637?quality=12&learn=on)
